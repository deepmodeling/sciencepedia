## Introduction
Transition-metal dichalcogenides (TMDs) have emerged as a cornerstone in the study of two-dimensional materials, offering a rich and versatile platform to explore novel phenomena in condensed matter physics. These atomically thin semiconductors possess a unique combination of properties—including a [direct band gap](@entry_id:147887) in the monolayer limit, strong spin-orbit coupling, and robust light-matter interactions—that sets them apart from conventional bulk materials. The central challenge and opportunity lie in understanding how these fundamental characteristics give rise to a spectacular array of emergent behaviors and how they can be harnessed for next-generation technologies. This article addresses this by providing a comprehensive theoretical overview of TMD physics.

The reader will embark on a structured journey through the world of TMDs. The first chapter, **Principles and Mechanisms**, builds the theoretical foundation from the ground up. It examines the unique [lattice dynamics](@entry_id:145448), the topological electronic structure described by the massive Dirac model, the physics of strongly-bound quasiparticles like excitons and [polarons](@entry_id:191083), and the emergent phenomena of superconductivity and moiré physics. Building on this foundation, the second chapter, **Applications and Interdisciplinary Connections**, demonstrates how these principles translate into practical utility. It explores the use of TMDs in [optoelectronics](@entry_id:144180), valley-[spintronics](@entry_id:141468), quantum optics, and [strain engineering](@entry_id:139243), highlighting the deep connections to materials science and engineering. Finally, the **Hands-On Practices** section allows you to solidify your understanding by applying these theoretical concepts to solve concrete problems, bridging the gap between abstract theory and [quantitative analysis](@entry_id:149547).

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms that govern the remarkable properties of transition-metal dichalcogenides (TMDs). We will build from the ground up, starting with their unique structural and vibrational characteristics, moving to their fascinating electronic and topological nature, exploring the rich landscape of quasiparticles and [many-body interactions](@entry_id:751663) they support, and culminating in a discussion of the emergent phenomena that arise in complex TMD systems, such as [heterostructures](@entry_id:136451) and superconductors.

### Crystalline Structure and Lattice Dynamics

The properties of any solid are fundamentally rooted in its crystal structure and the collective motions of its constituent atoms—the phonons. In TMDs, the two-dimensional, layered nature of the crystal gives rise to distinctive vibrational and structural phenomena.

#### Interlayer and Intralayer Vibrations

Monolayer TMDs are true two-dimensional crystals, where atoms are bound by strong covalent bonds. These monolayers can be stacked to form bilayer or bulk materials, held together by significantly weaker van der Waals forces. This hierarchy of interactions is directly reflected in the material's vibrational spectrum. The strong intralayer bonds lead to high-frequency [optical phonon](@entry_id:140852) modes, while the weak interlayer coupling gives rise to new, low-frequency modes that are characteristic of the layered structure.

A key example is the **rigid-layer shear mode** in a bilayer TMD. In this mode, the two layers oscillate as rigid plates in an out-of-phase, shearing motion relative to each other. We can model this system simply as two planes of mass per unit area $\sigma$ coupled by a restoring force characterized by an interlayer shear constant per unit area, $\alpha_S$. The [equations of motion](@entry_id:170720) for the in-plane displacements of the top ($u_1$) and bottom ($u_2$) layers are analogous to two coupled harmonic oscillators. By considering the relative displacement $\delta u = u_1 - u_2$, the [equation of motion](@entry_id:264286) reduces to that of a [simple harmonic oscillator](@entry_id:145764):

$$
\frac{d^2 (\delta u)}{dt^2} + \frac{2\alpha_S}{\sigma} \delta u = 0
$$

From this, we can immediately identify the [angular frequency](@entry_id:274516) of the shear mode, $\omega_S$, as $\omega_S = \sqrt{2\alpha_S/\sigma}$ [@problem_id:1214225]. The low frequency of this mode, typically measured using Raman spectroscopy, provides a direct and sensitive probe of the weak interlayer van der Waals forces.

#### Phonons and Thermal Properties in Two Dimensions

The thermal properties of a material at low temperatures are dominated by its lowest-energy acoustic phonons. For a TMD monolayer, we can adapt the **Debye model** to two dimensions. In this model, the [phonon dispersion relation](@entry_id:264229) is approximated as linear, $\omega = v_s k$, up to a cutoff Debye frequency $\omega_D$, where $v_s$ is an effective speed of sound. A monolayer TMD has three acoustic branches: one longitudinal and one transverse (in-plane), and one flexural (out-of-plane).

The calculation of the lattice specific heat per unit area, $c_A$, proceeds by first finding the [phonon density of states](@entry_id:188815) (DOS). For a 2D system with a linear dispersion, the DOS per unit area for a single branch is $D(\omega) = \omega/(2\pi v_s^2)$. With three branches, the total DOS is $D_{\text{total}}(\omega) = 3\omega/(2\pi v_s^2)$. The internal energy per unit area, $U_A$, is found by integrating the product of the DOS and the average thermal energy of a phonon mode over all frequencies. In the [low-temperature limit](@entry_id:267361) ($k_B T \ll \hbar \omega_D$), this yields a total internal energy that scales with the cube of the temperature, $U_A \propto T^3$.

The specific heat is the temperature derivative of the internal energy, $c_A = \partial U_A / \partial T$. This leads to a characteristic temperature dependence for the specific heat of a 2D material [@problem_id:1214183]:

$$
c_A = \frac{9 \zeta(3) k_B^{3} T^{2}}{\pi v_s^{2} \hbar^{2}}
$$

where $\zeta(3)$ is the Riemann zeta function of 3. The $T^2$ dependence of the [specific heat](@entry_id:136923) at low temperatures is a hallmark of a two-dimensional phonon system, in contrast to the $T^3$ dependence found in 3D bulk materials.

#### Structural Instabilities: The Peierls Distortion

While many TMDs are stable in the semiconducting $\text{2H}$ phase, others, particularly those in the metallic $\text{1T}$ phase (such as $\text{VSe}_2$), are prone to structural instabilities. One such instability is the **Peierls distortion**, which drives a transition to a [charge density wave](@entry_id:137299) (CDW) state. This mechanism is particularly clear in one-dimensional systems. Consider a 1D chain of atoms with a half-filled electronic band. Such a system is a metal. However, it can lower its total energy by undergoing a periodic lattice distortion, such as dimerization, where atoms move to form alternating short and long bonds.

This dimerization opens a gap at the Fermi level, transforming the metal into a semiconductor and lowering the total electronic energy. This electronic energy gain, however, comes at the cost of the elastic energy required to distort the lattice. The system finds a balance by adopting a distortion that minimizes the total energy. In a simplified model [@problem_id:1214170], the electronic energy gain per site $\Delta e_{el}$ for a small [dimerization](@entry_id:271116) (characterized by a change in [hopping integral](@entry_id:147296) $\delta t$) competes with an elastic energy cost $E_{ela} \propto (\delta t)^2$. The total energy change has a minimum at a non-zero value of $\delta t$, indicating that the distortion is spontaneous. The depth of this energy minimum is known as the **[condensation energy](@entry_id:195476)**, which stabilizes the distorted phase. For weak [electron-phonon coupling](@entry_id:139197), this energy takes a non-perturbative form, $E_{\text{cond}} \propto \exp(-\text{const.}/\lambda)$, where $\lambda$ is a dimensionless coupling constant, highlighting the fundamentally non-analytic nature of this many-body instability.

### Electronic Structure and Topology

The electronic properties of semiconducting TMDs (e.g., $\text{MoS}_2$, $\text{WSe}_2$) are dominated by the behavior of electrons near the corners of the hexagonal Brillouin zone, the K and K' points. The unique combination of lattice symmetry, strong [spin-orbit coupling](@entry_id:143520), and dimensionality gives rise to a rich electronic structure with non-trivial topological characteristics.

#### The Massive Dirac Hamiltonian

Near the K and K' valleys, the low-energy electronic band structure of a TMD monolayer can be remarkably well-described by a two-dimensional **massive Dirac Hamiltonian**. This effective model acts on a two-component [pseudospin](@entry_id:147053) basis, which represents the dominant atomic orbitals (e.g., the $d_{z^2}$ and $d_{xy}/d_{x^2-y^2}$ orbitals of the transition metal atom). For a given valley $\tau$ ($\tau = +1$ for K, $\tau = -1$ for K') and spin $s$ ($s = \pm 1$), the Hamiltonian takes the form:

$$
H_{\tau, s}(\vec{k}) = \hbar v_F (\tau k_x \sigma_x + k_y \sigma_y) + \frac{\Delta_{eff}}{2} \sigma_z
$$

Here, $\vec{k}=(k_x, k_y)$ is the crystal momentum measured from the valley center, $v_F$ is the Fermi velocity related to the hopping strength, and $\sigma_{x,y,z}$ are the Pauli matrices. The first term is a kinetic energy term analogous to that of a massless Dirac particle, while the second term, $\frac{\Delta_{eff}}{2}\sigma_z$, is a mass term that opens a band gap of size $\Delta_{eff}$. In TMDs, this effective gap arises from a combination of factors, including intrinsic orbital effects and, crucially, **[spin-orbit coupling](@entry_id:143520) (SOC)**. The broken inversion symmetry of the monolayer crystal lattice allows the SOC to lift the spin degeneracy, leading to spin-split bands where the effective gap depends on both the valley and spin indices, e.g., $\Delta_{eff} = \Delta + \frac{s \tau}{2}(\lambda_c + \lambda_v)$, where $\Delta$ is an intrinsic gap and $\lambda_{c,v}$ are SOC parameters [@problem_id:1214168]. This coupling of spin and valley degrees of freedom is a cornerstone of TMD physics.

#### Geometric Phase and Berry Curvature

The wavefunctions of electrons in a crystal possess not only a dynamical phase but also a [geometric phase](@entry_id:138449), or Berry phase. The local manifestation of this geometry in momentum space is the **Berry curvature**, $\Omega(\mathbf{k})$. It acts like a magnetic field in momentum space, deflecting the motion of electron wavepackets. For a generic two-band system described by $H(\mathbf{k}) = \mathbf{d}(\mathbf{k}) \cdot \boldsymbol{\sigma}$, the Berry curvature is given by:

$$
\Omega_{xy}(\mathbf{k}) = -\frac{1}{2} \frac{\mathbf{d} \cdot \left( \frac{\partial \mathbf{d}}{\partial k_x} \times \frac{\partial \mathbf{d}}{\partial k_y} \right)}{|\mathbf{d}|^3}
$$

A key insight is that a non-zero Berry curvature requires broken [time-reversal symmetry](@entry_id:138094) or broken [inversion symmetry](@entry_id:269948). In TMD monolayers, the crystal structure lacks [inversion symmetry](@entry_id:269948). Applying the formula to the massive Dirac Hamiltonian [@problem_id:1214163], where $\mathbf{d}(\mathbf{k}) = (v_F k_x, v_F k_y, M)$ with $M=\Delta/2$, we find that the Berry curvature is peaked at the valley center ($\mathbf{k}=0$) with a value of $\Omega_{xy}^{(-)}(0) = -v_F^2/(2M^2)$ for the [valence band](@entry_id:158227). This non-zero curvature is a direct consequence of the "mass" term $M$, which itself originates from broken [inversion symmetry](@entry_id:269948). Furthermore, due to [time-reversal symmetry](@entry_id:138094), the Hamiltonian for the K' valley is the time-reversed partner of the K valley, which results in a Berry curvature of the opposite sign: $\Omega^{K'}(\mathbf{k}) = -\Omega^K(-\mathbf{k})$.

#### Valley Hall Effect and Orbital Magnetic Moment

The non-zero Berry curvature has profound physical consequences. It gives rise to an [anomalous velocity](@entry_id:146502) component for an electron wavepacket, transverse to an applied electric field. This is the origin of the intrinsic **anomalous Hall effect**.

In TMDs, while the Berry curvature is opposite in the K and K' valleys, leading to a zero net charge Hall effect, it enables a **valley Hall effect**. An applied in-plane electric field drives electrons from the K and K' valleys to opposite transverse edges of the sample. The Hall conductivity for a single valley $\tau$ with a filled valence band at zero temperature is given by the integral of its Berry curvature over the Brillouin zone:

$$
\sigma_{xy}^\tau = \frac{e^2}{\hbar} \int \frac{d^2k}{(2\pi)^2} \Omega_v^\tau(\mathbf{k})
$$

For the massive Dirac model, this integral yields a quantized value for each valley, $\sigma_{xy}^{\tau} = -\frac{e^2}{2h}\tau$. The **valley Hall conductivity**, defined as $\sigma_{xy}^v = \sigma_{xy}^{K} - \sigma_{xy}^{K'}$, is then $\sigma_{xy}^v = -e^2/h$ [@problem_id:1214192]. This phenomenon, where a valley current is generated transverse to an electric field, is a central concept in **[valleytronics](@entry_id:139774)**, an emerging field that aims to use the valley index as an information carrier.

Another consequence of the band geometry is that Bloch electrons can possess an intrinsic **[orbital magnetic moment](@entry_id:159585) (OMM)**, even in the absence of an external magnetic field. This moment is also related to the Berry curvature. For a conduction band electron at the K-point ($\mathbf{k}=0$) in $\text{WSe}_2$, the OMM is directly proportional to the Berry curvature at that point and inversely proportional to the band gap [@problem_id:1214168]. The opposite OMMs in the K and K' valleys allow for optical selection and manipulation of valley-polarized states using circularly polarized light, a key tool for probing and controlling valley physics.

### Quasiparticles and Many-Body Interactions

While the single-particle electronic structure is foundational, the most striking properties of TMDs often emerge from the complex interplay of their [elementary excitations](@entry_id:140859). We now turn to these **quasiparticles** and their interactions.

#### Excitons: Bound Electron-Hole Pairs

Semiconducting TMDs are direct-gap materials with exceptionally strong [light-matter interaction](@entry_id:142166). When a photon with energy greater than the band gap is absorbed, it creates an electron-hole pair. Due to the reduced dimensionality and weak [dielectric screening](@entry_id:262031), this electron and hole are strongly bound by the Coulomb attraction to form a quasiparticle known as an **[exciton](@entry_id:145621)**. The binding energies of these [excitons](@entry_id:147299) are enormous, on the order of several hundred meV, which is an order of magnitude larger than in conventional bulk semiconductors. This ensures that [excitons](@entry_id:147299) are stable even at room temperature and dominate the [optical response](@entry_id:138303) of TMDs.

The interaction potential between the electron and hole in a 2D material embedded in a dielectric environment is not the simple $1/r$ Coulomb potential. Instead, it is described by the **Rytova-Keldysh potential**, which accounts for the fact that [electric field lines](@entry_id:277009) spread out in the surrounding 3D space. This potential behaves like $1/r$ at long distances but takes on a weaker, logarithmic form, $V(r) \propto \ln(r)$, at short distances. In the limit of strong screening, we can model the entire interaction with this logarithmic potential, $V(r) = U \ln(r/r_s)$, where $r_s$ is a screening length. Using a variational method with a Gaussian trial wavefunction, one can estimate the [ground-state energy](@entry_id:263704) of the exciton [@problem_id:1214178], providing insight into how the binding energy depends on the reduced mass $\mu$ and [interaction parameters](@entry_id:750714).

When a TMD is placed in a magnetic field perpendicular to its plane, the exciton's energy levels shift. A key contribution is the **diamagnetic shift**, which arises from the orbital motion of the electron and hole. For an exciton in its ground state, this can be calculated using [first-order perturbation theory](@entry_id:153242) with the perturbation Hamiltonian $H' = (e^2 B^2 / 8\mu) r^2$. The resulting energy shift, $\Delta E$, is proportional to $B^2$ and the expectation value of the squared [exciton](@entry_id:145621) radius, $\langle r^2 \rangle$. This shift provides an experimental measure of the [exciton](@entry_id:145621)'s spatial extent [@problem_id:1214194].

#### Electron-Phonon Coupling and Polarons

Charge carriers in polar materials like TMDs do not move as bare particles; they are "dressed" by a cloud of virtual [lattice vibrations](@entry_id:145169) (phonons). This composite quasiparticle is called a **polaron**. The interaction responsible for this is the **Fröhlich interaction** between an electron and the [macroscopic electric field](@entry_id:196409) produced by longitudinal optical (LO) phonons.

In a 2D system, the strength of this interaction is characterized by the dimensionless 2D Fröhlich [coupling constant](@entry_id:160679), $\alpha_{2D}$. The formation of the polaron lowers the electron's energy. This energy shift, or [polaron](@entry_id:137225) self-energy, can be calculated using [second-order perturbation theory](@entry_id:192858). For an electron at the bottom of the conduction band, the [self-energy](@entry_id:145608) is found to be directly proportional to the coupling constant and the LO phonon energy [@problem_id:1214175]:

$$
\Delta E = -\frac{\pi}{2} \alpha_{2D} \hbar\omega_{LO}
$$

This interaction affects not only the carrier's energy but also its effective mass and mobility, playing a crucial role in [transport properties](@entry_id:203130).

#### Screening and Collective Excitations (Plasmons)

In a conductor or a doped semiconductor, mobile charge carriers react to redistribute themselves and screen out external electric fields. In 2D materials, this screening is described by the **Thomas-Fermi theory**. The effectiveness of screening is quantified by the Thomas-Fermi [screening length](@entry_id:143797), $\lambda_{TF} = 1/q_{TF}$, where $q_{TF}$ is the Thomas-Fermi [wavevector](@entry_id:178620). This wavevector is proportional to the [electronic density of states](@entry_id:182354) at the Fermi energy, $D(E_F)$.

For a doped TMD described by the massive Dirac model, the DOS is linear in energy, $D(E) \propto E$. By relating the Fermi energy $E_F$ to the [carrier density](@entry_id:199230) $n$, we can derive an expression for the [screening length](@entry_id:143797). This shows how screening depends explicitly on the material's [band structure](@entry_id:139379) (band gap $\Delta$, Fermi velocity $v_F$) and the tunable [carrier density](@entry_id:199230) $n$ [@problem_id:1214207].

In addition to screening static fields, the sea of charge carriers can support collective oscillations known as **plasmons**. In 2D materials, [plasmons](@entry_id:146184) have a characteristic dispersion relation $\omega \propto \sqrt{q}$, where $q$ is the wavevector. This dispersion is highly sensitive to the geometry and dielectric environment. For example, for plasmons confined to a narrow strip of TMD, the dispersion is modified by the strip width $W$, acquiring a gap at $q=0$ and approaching the 2D behavior for large $q$ [@problem_id:1214143]. These [plasmons](@entry_id:146184) are of great interest for [nanophotonics](@entry_id:137892) and for concentrating light at sub-wavelength scales.

### Advanced Topics and Emergent Phenomena

Building on these fundamental principles, TMDs provide a platform for realizing more complex and often exotic [states of matter](@entry_id:139436), particularly when incorporated into [heterostructures](@entry_id:136451) or subjected to external fields.

#### Two-Dimensional Superconductivity

Certain metallic TMDs, most notably $\text{NbSe}_2$, are intrinsic superconductors. In the monolayer limit, they represent nearly ideal two-dimensional superconducting systems. Unlike in 3D, a true phase transition with [long-range order](@entry_id:155156) is forbidden in 2D at finite temperatures. Instead, the transition to a zero-resistance state is described by the **Berezinskii-Kosterlitz-Thouless (BKT) theory**. This transition is driven by the unbinding of thermally excited vortex-antivortex pairs. The transition occurs at a temperature $T_{BKT}$ determined by a universal relation involving the [superfluid stiffness](@entry_id:147718), $J(T)$: $k_B T_{BKT} = (\pi/2) J(T_{BKT})$. The stiffness itself is related to the superconducting [carrier density](@entry_id:199230). For many TMDs, $T_{BKT}$ is only slightly lower than the mean-field critical temperature $T_c$. The small difference $\Delta T = T_c - T_{BKT}$ can be directly related to the zero-temperature stiffness $J_0$ [@problem_id:1214149].

Superconductivity is destroyed by a sufficiently strong magnetic field. Within **Ginzburg-Landau theory**, the upper [critical magnetic field](@entry_id:145488), $B_{c2}$, at which superconductivity nucleates, can be calculated. For a 2D superconductor in a perpendicular field, the Cooper pairs form quantized Landau levels. The [critical field](@entry_id:143575) is determined by the condition that the energy of the lowest Landau level matches the superconducting condensation energy. This leads to a simple relationship between the zero-temperature critical field and the Ginzburg-Landau [coherence length](@entry_id:140689) $\xi_0$: $B_{c2}(0) = \hbar/(2e\xi_0^2)$ [@problem_id:1214200].

The superconducting properties can also reflect the anisotropies of the underlying crystal. In $\text{2H-NbSe}_2$, the strong SOC leads to a superconducting gap $\Delta(\mathbf{k})$ that is not isotropic but has a hexagonal "starfish" shape. This anisotropy directly impacts the behavior of devices like Josephson junctions. The critical current $I_c$ of a ballistic junction depends on the angular average of the [gap function](@entry_id:164997). The anisotropic gap leads to a [critical current](@entry_id:136685) that deviates from the simple isotropic case, providing a direct link between the microscopic pairing state and a macroscopic device characteristic [@problem_id:1214206].

#### The Role of Defects, Strain, and External Fields

Real-world materials are never perfect. Defects like atomic vacancies can significantly alter the local electronic structure. Within the **Koster-Slater model**, a single impurity with a local potential $U$ can pull a discrete electronic state out of the host material's continuous bands. If the potential is strong enough, this can create an **in-gap state** whose energy is determined by the strength of the potential and the host's Green's function [@problem_id:1214155].

Such defect-bound states can interact with the continuum of intrinsic excitations, such as [excitons](@entry_id:147299). This interference between a discrete state and a continuum gives rise to a characteristic asymmetric lineshape in [absorption spectra](@entry_id:176058) known as a **Fano resonance**. The shape of this resonance is governed by the Fano parameter $q$, which depends on the transition dipole moments of the discrete and [continuum states](@entry_id:197473) and their coupling. By analyzing how the Fano lineshape changes with the polarization of incident light, one can deduce information about the orientation of the defect's dipole moment relative to the crystal axes [@problem_id:1214185].

The properties of TMDs are also highly tunable by external knobs like mechanical strain. Applying biaxial strain, for example, modifies the interatomic distances and orbital overlaps, which in turn alters the band structure and [spin-orbit coupling](@entry_id:143520) parameters. Using [first-order perturbation theory](@entry_id:153242), one can calculate the change in the [spin-orbit splitting](@entry_id:159337) of the valence bands induced by strain, demonstrating a powerful method for engineering the electronic and spintronic properties of these materials [@problem_id:1214210].

#### Moiré Superlattices and Hybrid Excitons

Perhaps the most exciting recent development in TMD research is the advent of twisted van der Waals [heterostructures](@entry_id:136451). When two TMD monolayers are stacked with a slight twist angle or lattice mismatch, a long-wavelength interference pattern, known as a **[moiré superlattice](@entry_id:143542)**, is formed. This superlattice creates a periodic [potential landscape](@entry_id:270996) for electrons and [excitons](@entry_id:147299).

This **moiré potential** can be modeled using a continuum approach with a first-harmonic expansion. For a hexagonal lattice, this potential is a superposition of three cosine waves, creating a landscape of potential minima and maxima. The depth of this potential, defined as $V_0 = V_{\max} - V_{\min}$, can be calculated directly from the amplitude of the expansion coefficients and determines the trapping strength for quasiparticles like excitons [@problem_id:1214217].

In a twisted homobilayer (e.g., two $\text{WSe}_2$ layers), an [exciton](@entry_id:145621) can reside in either the top or bottom layer. The [moiré pattern](@entry_id:264251) not only creates a trapping potential but also modulates the tunneling between the layers. This leads to the formation of **hybrid moiré excitons**, which are bonding and anti-bonding superpositions of the intralayer excitons. At certain high-symmetry points in the moiré cell, the potential and tunneling terms conspire to create a ground-state hybrid exciton that is a symmetric combination of the two layer states. Since the optical oscillator strength is proportional to the square of the sum of the layer components, this hybridization can dramatically enhance the brightness of the lowest-energy moiré [exciton](@entry_id:145621), making it easily observable in [photoluminescence](@entry_id:147273) experiments [@problem_id:1214187].

Finally, the trapping of [excitons](@entry_id:147299) in a moiré potential opens the door to creating ordered arrays of interacting quasiparticles. Interlayer [excitons](@entry_id:147299), which consist of an electron in one layer and a hole in another, possess a large out-of-plane electric dipole moment. At high densities, these trapped, dipolar excitons can form a crystal. The [collective oscillations](@entry_id:158973) of this novel state of matter, so-called exciton [plasmons](@entry_id:146184), have a unique [dispersion relation](@entry_id:138513). Due to the long-range $1/r^3$ dipole-dipole interaction, these modes exhibit an "acoustic [plasmon](@entry_id:138021)" dispersion that scales as $\omega \propto k^{3/2}$ at long wavelengths, a distinct signature of collective behavior in a dipolar crystal [@problem_id:1214190].