## Introduction
The interface between two different semiconductor materials, known as a heterojunction, is a fundamental building block of modern nanoelectronics and [optoelectronics](@entry_id:144180). The way the energy bands of these materials align at the junction—the "[band offset](@entry_id:142791)"—governs the flow and confinement of charge carriers, directly dictating device performance. To engineer devices such as lasers, high-speed transistors, and efficient solar cells, we need a predictive framework for understanding this band alignment. This article addresses the challenge of predicting and understanding band offsets, starting with the simplest, most intuitive model and building towards a comprehensive, physically accurate picture.

This article provides a graduate-level exploration of the principles and applications of semiconductor [band alignment](@entry_id:137089). You will begin in the "Principles and Mechanisms" chapter by learning the foundational Anderson's [electron affinity](@entry_id:147520) rule, a model based on ideal material properties. You will then explore the rich physics that causes deviations from this simple rule, including interface dipoles, strain, and quantum states. The "Applications and Interdisciplinary Connections" chapter will demonstrate how these principles are applied to design real-world devices, from quantum well lasers to advanced transistors, and connect the theory to crucial experimental and computational validation techniques. Finally, the "Hands-On Practices" section offers concrete problems to solidify your understanding, challenging you to calculate band offsets in both ideal and non-ideal scenarios.

## Principles and Mechanisms

The behavior of charge carriers at the interface between two dissimilar semiconductor materials is fundamental to the operation of modern electronic and [optoelectronic devices](@entry_id:1129187). The relative alignment of the energy bands of the two materials dictates how electrons and holes are confined or transported across the junction. This chapter elucidates the principles governing this alignment, beginning with the foundational, idealized model known as Anderson's rule, and progressing to the complex physical mechanisms that cause deviations in real-world systems.

### The Ideal Model: Anderson's Electron Affinity Rule

To construct a model for the band alignment at a [heterojunction](@entry_id:196407), we must first establish a clear set of definitions for the relevant energy levels and material parameters. Consider a semiconductor in equilibrium with a vacuum.

- The **vacuum level**, denoted $E_{\text{vac}}$, is the energy of a stationary electron in the vacuum just outside the semiconductor's surface. It serves as a common energy reference for comparing different materials. 
- The **conduction band minimum** ($E_C$) and **valence band maximum** ($E_V$) are the energies of the bottom edge of the conduction band and the top edge of the valence band, respectively.
- The **band gap**, $E_g$, is the energy difference between these two edges: $E_g = E_C - E_V$.
- The **Fermi level**, $E_F$, represents the [electrochemical potential](@entry_id:141179) of the electrons and is constant throughout a system in thermal equilibrium. Its position within the band gap is determined by the material's [doping concentration](@entry_id:272646) and temperature.

From these energy levels, we define two critical material properties:

1.  **Electron Affinity ($\chi$)**: The **electron affinity** is the energy released when an electron is moved from the [vacuum level](@entry_id:756402) to the conduction band minimum. It is defined as the energy difference $\chi = E_{\text{vac}} - E_C$. The electron affinity is an intrinsic property of a semiconductor, largely independent of doping.

2.  **Work Function ($\Phi$)**: The **work function** is the minimum energy required to remove an electron from the solid (specifically, from the Fermi level) to the [vacuum level](@entry_id:756402). It is defined as $\Phi = E_{\text{vac}} - E_F$. Since the Fermi level $E_F$ changes with doping, the work function is a doping-dependent quantity. It can be expressed in terms of the [electron affinity](@entry_id:147520) as $\Phi = \chi + (E_C - E_F)$. 

The simplest model for predicting the [band alignment](@entry_id:137089) at a [semiconductor heterojunction](@entry_id:274706) is **Anderson's rule**, also known as the electron affinity rule. The central and most critical assumption of this model is that when two semiconductors are brought into intimate contact to form an ideal interface, their vacuum levels align and become continuous across the junction. An ideal interface is one that is atomically abrupt, clean, and free of any electrostatic dipoles or net charges. 

Under this **vacuum-level alignment** assumption, we can construct the band diagram of the heterojunction. Let us consider a junction between material A and material B. If $E_{\text{vac}}$ is continuous across the interface, we can set a common vacuum level for both materials. The conduction band offset, $\Delta E_C$, is the difference in the conduction band minima across the interface. Adopting the convention $\Delta E_C \equiv E_C^B - E_C^A$, we can derive its value:

$E_C^A = E_{\text{vac}} - \chi_A$
$E_C^B = E_{\text{vac}} - \chi_B$

Therefore, the [conduction band offset](@entry_id:1122863) is:
$\Delta E_C = E_C^B - E_C^A = (E_{\text{vac}} - \chi_B) - (E_{\text{vac}} - \chi_A) = \chi_A - \chi_B$

Similarly, the [valence band offset](@entry_id:1133686), defined as $\Delta E_V \equiv E_V^B - E_V^A$, can be found. We know that $E_V = E_C - E_g$, so:

$\Delta E_V = E_V^B - E_V^A = (E_C^B - E_g^B) - (E_C^A - E_g^A) = (E_C^B - E_C^A) - (E_g^B - E_g^A)$

This gives the important relationship:
$\Delta E_V = \Delta E_C - (E_g^B - E_g^A) = \Delta E_C + E_g^A - E_g^B$

Substituting the expression for $\Delta E_C$:
$\Delta E_V = (\chi_A - \chi_B) + (E_g^A - E_g^B)$

These two equations form the core of Anderson's rule. They state that for an ideal interface, the band offsets are determined solely by the differences in the intrinsic bulk properties of the constituent semiconductors: their electron affinities and [band gaps](@entry_id:191975). It is crucial to recognize that the offsets depend on the electron affinities ($\chi$), not the work functions ($\Phi$). Since $\Phi$ depends on doping, it cannot determine the intrinsic band lineup, which is a property of the interface itself, independent of doping far from the junction .

### Classification of Heterojunction Alignments

The relative signs and magnitudes of $\Delta E_C$ and $\Delta E_V$ determine the type of [band alignment](@entry_id:137089), which has profound consequences for carrier confinement and transport. For a quantum well structure where a layer of material A (the "well") is surrounded by material B (the "barrier"), confinement of electrons in material A requires $E_C^A  E_C^B$ (a positive offset, $\Delta E_C > 0$), and confinement of holes in material A requires $E_V^A > E_V^B$ (a negative offset, $\Delta E_V  0$). This leads to three primary classifications of heterojunctions  .

-   **Type-I (Straddling) Alignment**: In this configuration, the band gap of the narrower-gap material is entirely contained within the band gap of the wider-gap material. For a well made of material A, this corresponds to $\Delta E_C > 0$ and $\Delta E_V  0$. Both electrons and holes are confined in the same material (material A), creating a potential well for both carrier types. This spatial overlap is highly conducive to efficient [electron-hole recombination](@entry_id:187424), making Type-I heterostructures ideal for light-emitting devices like LEDs and laser diodes. For example, a hypothetical heterostructure with $\Delta E_C = +0.60 \text{ eV}$ and $\Delta E_V = -0.40 \text{ eV}$ exhibits a Type-I alignment, with both electrons and holes confined in the well material. 

-   **Type-II (Staggered) Alignment**: In a Type-II alignment, both the conduction and valence band edges of one material are lower (or higher) in energy than the corresponding edges of the other material. This corresponds to $\Delta E_C$ and $\Delta E_V$ having the same sign. For example, if $\Delta E_C > 0$ and $\Delta E_V > 0$, electrons are confined in material A while holes are confined in material B. This leads to the **spatial separation** of electrons and holes at the interface. Such "spatially indirect" [excitons](@entry_id:147299) have longer lifetimes, a property useful in photovoltaic cells and certain memory devices. A system with $\Delta E_C = +0.30 \text{ eV}$ and $\Delta E_V = +0.70 \text{ eV}$ would be classified as Type-II. 

-   **Type-III (Broken-Gap) Alignment**: This is an extreme case of a staggered alignment where the conduction band minimum of one material lies at a lower energy than the valence band maximum of the other. For instance, this can occur if $\Delta E_C > 0$ and $\Delta E_V > E_g^A$. In this scenario, there is an energy overlap between the conduction band of material A and the valence band of material B. This allows electrons to transfer from the valence band of B to the conduction band of A even in the ground state, creating a semimetallic interface with a natural accumulation of electrons and holes. Such alignments are characteristic of systems like InAs/GaSb and are exploited in tunneling devices. A heterojunction with offsets $\Delta E_C = +1.00 \text{ eV}$ and $\Delta E_V = +1.20 \text{ eV}$ for a well material with $E_g^A = 1.00 \text{ eV}$ would be Type-III, as the condition $E_g^A  \Delta E_V$ is met. 

### Electrostatics of Heterojunctions: Band Bending and Built-in Potential

Anderson's rule provides the band discontinuities right at the metallurgical interface. However, to understand the full electronic profile of a device, we must consider the electrostatics over a wider region. When two semiconductors with different doping levels (e.g., [n-type and p-type](@entry_id:151220)) are joined, they initially have different Fermi levels relative to vacuum. To achieve thermal equilibrium, a single, constant Fermi level must be established throughout the entire structure. This equalization is accomplished by a transfer of charge across the interface.

In an n-p heterojunction, electrons diffuse from the n-side to the p-side, and holes diffuse from the p-side to the n-side, until the resulting electric field counteracts further diffusion. This charge transfer leaves behind uncompensated ionized donors on the n-side and ionized acceptors on the p-side, forming a **space-charge region** or **depletion region**.

The electrostatics of this region are described by the one-dimensional Poisson equation. Within the **depletion approximation**, we assume the [space charge](@entry_id:199907) density $\rho(x)$ is constant within the depletion widths ($w_n$ on the n-side, $w_p$ on the p-side) and zero elsewhere :
$\rho(x) = \begin{cases} +qN_D  \text{ for } -w_n  x  0 \\ -qN_A  \text{ for } 0  x  w_p \\ 0  \text{ elsewhere} \end{cases}$

The Poisson equation is then $\frac{d^2\phi}{dx^2} = -\frac{\rho(x)}{\varepsilon(x)}$, where $\phi(x)$ is the electrostatic potential and $\varepsilon(x)$ is the position-dependent permittivity ($\varepsilon_A$ in material A, $\varepsilon_B$ in material B). Integrating this equation with appropriate boundary conditions (zero electric field at the edges of the depletion region and continuity of the electric displacement field $\mathbf{D}=\varepsilon\mathbf{E}$ at the interface) yields the profile of the electric field and potential.

The [total potential energy](@entry_id:185512) drop across the depletion region, $qV_{\text{bi}}$, is known as the **built-in potential**. Thermodynamically, this potential energy drop must exactly balance the initial difference in work functions between the two isolated materials:
$qV_{\text{bi}} = |\Phi_A - \Phi_B|$

It is essential to distinguish the [built-in potential](@entry_id:137446) from the band offsets.
-   **Band Offsets ($\Delta E_C, \Delta E_V$)** are quantum mechanical discontinuities occurring at the atomically sharp interface, determined (in this model) by intrinsic material properties ($\chi, E_g$).
-   **Built-in Potential ($V_{\text{bi}}$)** is a classical electrostatic potential drop that occurs over the finite width of the [space-charge region](@entry_id:136997), determined by the difference in work functions ($\Phi$), which are doping-dependent.

The total [energy band diagram](@entry_id:272375) of a heterojunction thus consists of the intrinsic band offsets at the interface superimposed upon the smooth band bending profile dictated by the [built-in potential](@entry_id:137446). 

### Deviations from the Ideal Model: The Role of the Interface

Anderson's rule provides an invaluable conceptual framework, but its quantitative accuracy is limited because real interfaces are not ideal. The most significant departure from the ideal model stems from the breakdown of the vacuum-level alignment assumption due to the formation of **interface dipoles**.

When two different materials are joined, the disruption of the crystal lattice and the formation of new chemical bonds at the interface lead to a microscopic charge rearrangement. This creates a dipole layer, which, from electrostatics, produces a sharp step in the electrostatic potential, $\Delta V_{\text{dipole}}$, right at the interface. This [potential step](@entry_id:148892) causes a discontinuity in the vacuum level, $\Delta E_{\text{vac}} = q \Delta V_{\text{dipole}}$. The [conduction band offset](@entry_id:1122863) is therefore modified from the simple Anderson prediction :
$\Delta E_C = (\chi_A - \chi_B) + \Delta E_{\text{vac}}$

The magnitude and sign of this dipole contribution are highly sensitive to the specific chemical and structural properties of the interface. This has two critical consequences:

1.  **Prediction Accuracy Varies**: The reliability of Anderson's rule depends on the system.
    -   For a nearly ideal system like a lattice-matched, isovalent, common-anion heterojunction such as **GaAs/AlAs**, the chemical differences are minimal. The [interface dipole](@entry_id:143726) is small (inducing a potential step $\lesssim 0.2 \text{ eV}$), and Anderson's rule provides a reasonable first approximation of the band offsets. 
    -   Conversely, for a chemically dissimilar interface like **Si/SiO$_2$**, the transition from a covalent semiconductor to a polar insulator involves significant changes in bonding and [electronegativity](@entry_id:147633). This creates a strong [interface dipole](@entry_id:143726), causing a large shift in the [vacuum level](@entry_id:756402) (on the order of eVs). Consequently, Anderson's rule fails dramatically, and the experimentally measured [band offset](@entry_id:142791) ($\Delta E_C \approx 3.1 \text{ eV}$) bears little resemblance to the prediction from bulk electron affinities alone. In such cases, the measured offset must be used to determine practical quantities like the effective barrier for [electron injection](@entry_id:270944) from the silicon into the oxide. 

2.  **Failure of Transitivity**: Anderson's rule, being based on bulk properties, implies that band offsets should be transitive. That is, for three materials A, B, and C, the offset between A and C should be the sum of the offsets between A/B and B/C: $\Delta E_C(A/C) = \Delta E_C(A/B) + \Delta E_C(B/C)$. However, because the [interface dipole](@entry_id:143726) contribution $\Delta E_{\text{vac}}$ is specific to each interface pair, this [transitivity](@entry_id:141148) is generally not observed in real systems. Transitivity holds if and only if the dipole contributions are themselves additive: $\Delta E_{\text{vac}}(A/C) = \Delta E_{\text{vac}}(A/B) + \Delta E_{\text{vac}}(B/C)$. Since the dipole depends on the unique chemistry of each specific interface, this condition is not generally met, and violations of [transitivity](@entry_id:141148) are a direct consequence of interface-specific effects not captured by the [electron affinity](@entry_id:147520) rule.  

### Beyond the Electron Affinity Rule: Advanced Mechanisms

To achieve more accurate predictions and a deeper understanding of [band alignment](@entry_id:137089), more sophisticated models are required that explicitly account for the physical mechanisms that Anderson's rule neglects.

#### Strain Effects in Pseudomorphic Heterostructures

When one semiconductor is grown epitaxially on a substrate with a different [lattice constant](@entry_id:158935), the resulting layer can be strained. This strain alters the interatomic distances and [crystal symmetry](@entry_id:138731), which in turn modifies the [electronic band structure](@entry_id:136694). This powerful technique, known as **[strain engineering](@entry_id:139243)**, is used to tailor the properties of [semiconductor devices](@entry_id:192345).

According to **[deformation potential theory](@entry_id:140142)**, strain affects band-edge energies. For a biaxially strained layer grown on a (001) substrate, the strain has two key effects on the valence band :
1.  **Hydrostatic Shift**: The hydrostatic component of the strain (related to the volume change) shifts the average energy of the valence bands.
2.  **Shear Splitting**: The shear component of the strain (related to the change in [crystal symmetry](@entry_id:138731)) lifts the degeneracy between the **heavy-hole (HH)** and **light-hole (LH)** bands at the Brillouin zone center.

For example, in a compressively strained $\mathrm{In}_{0.20}\mathrm{Ga}_{0.80}\mathrm{As}$ [quantum well](@entry_id:140115) on a GaAs substrate, the HH band moves to a higher energy, while the LH band moves to a lower energy. This means that the "[valence band offset](@entry_id:1133686)" is no longer a single value. Instead, we must define separate effective offsets for heavy holes and light holes, $\Delta E_{v,HH}^{\text{eff}}$ and $\Delta E_{v,LH}^{\text{eff}}$. The HH offset will be larger than the original unstrained offset, while the LH offset will be smaller. This has the critical consequence of creating a deeper [potential well](@entry_id:152140) for heavy holes, making them the dominant charge carrier for valence band confinement and transport in many strained [optoelectronic devices](@entry_id:1129187). 

#### Interface-Induced Gap States

Another important mechanism, particularly at metal-semiconductor interfaces but also relevant to some semiconductor-semiconductor junctions, is the formation of **interface-induced gap states**. When the electronic wavefunctions of one material penetrate the other, they can create a continuum of electronic states within the semiconductor's forbidden band gap. At a [metal-semiconductor interface](@entry_id:1127826), these are called **Metal-Induced Gap States (MIGS)**.

These MIGS are evanescent waves that decay exponentially away from the interface, with a [characteristic decay length](@entry_id:183295) on the order of nanometers. They possess a certain character: states originating from the valence band act as donor-like states, while those originating from the conduction band act as acceptor-like states. There exists a [specific energy](@entry_id:271007), the **[charge neutrality level](@entry_id:1122299) ($E_{\text{CNL}}$)**, at which these states, if filled, would result in zero net charge at the interface.

If the density of these interface states is sufficiently high, they can accommodate significant charge with only a small shift in energy. This effectively "pins" the Fermi level at the interface close to the $E_{\text{CNL}}$, largely independent of the properties (e.g., work function) of the contacting material. This pinning phenomenon provides a powerful alternative explanation for band alignments, especially in systems where Anderson's rule is known to fail. The study of such [interface states](@entry_id:1126595) represents a move from a simple alignment of bulk properties to a more complex picture where the interface itself plays the dominant role in determining its electronic structure. 

In summary, Anderson's rule offers an essential starting point for understanding band offsets, providing a clear, intuitive model based on bulk material properties. However, a graduate-level understanding requires a critical appreciation of its limitations and the rich physics of real interfaces, where dipoles, strain, and induced states create a more complex and ultimately more powerful set of design principles for advanced nanoelectronic devices.