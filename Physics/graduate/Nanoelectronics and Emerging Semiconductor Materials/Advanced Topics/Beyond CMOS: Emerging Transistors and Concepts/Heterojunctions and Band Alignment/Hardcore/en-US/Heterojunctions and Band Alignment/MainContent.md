## Introduction
The junction between two different semiconductor materials, known as a [heterojunction](@entry_id:196407), is a foundational concept in modern nanoelectronics and [optoelectronics](@entry_id:144180). The ability to join dissimilar materials allows for "[band structure engineering](@entry_id:143160)"—the deliberate design of the electronic energy landscape at an atomic scale. This control enables the creation of devices with performance characteristics far superior to those made from a single material. However, predicting and controlling the electronic properties at this interface presents a significant challenge, as it involves moving beyond simple bulk material properties to understand the complex physics of the junction itself.

This article provides a graduate-level exploration of heterojunctions and [band alignment](@entry_id:137089). The following chapters will systematically build your understanding of this critical topic. In "Principles and Mechanisms," we will start with the idealized Anderson's rule and progressively incorporate the complex real-world phenomena—such as interface dipoles, strain, and polarization—that truly define the band structure. Next, "Applications and Interdisciplinary Connections" will demonstrate how these principles are applied to create revolutionary devices, from high-speed transistors and low-power switches to efficient [solar cells](@entry_id:138078), and how they connect to fields like [materials characterization](@entry_id:161346) and mechanics. Finally, "Hands-On Practices" will allow you to apply your knowledge through targeted problems, solidifying your grasp of both the theory and its practical implications.

## Principles and Mechanisms

The behavior of a [semiconductor heterojunction](@entry_id:274706) is fundamentally governed by the alignment of the electronic energy bands of the constituent materials at their interface. This alignment dictates the energetic barriers and [quantum wells](@entry_id:144116) that electrons and holes experience, thereby controlling carrier confinement, transport, and recombination. In this chapter, we will develop a systematic understanding of band alignment, beginning with an idealized model and progressively incorporating the complex physical mechanisms that dominate real-world interfaces.

### The Ideal Heterojunction: Anderson's Rule

To construct a model of a [heterojunction](@entry_id:196407), we must first define the essential electronic parameters of the individual semiconductors. These parameters are typically defined with respect to the **[vacuum level](@entry_id:756402) ($E_{\text{vac}}$)**, which is the energy of a stationary electron in a vacuum just outside the material's surface.

The key band parameters are:
-   The **conduction band minimum ($E_c$)** and **valence band maximum ($E_v$)**, which represent the lowest energy states for free electrons and the highest energy states for holes, respectively.
-   The **band gap ($E_g$)**, the energy difference between these edges: $E_g = E_c - E_v$.
-   The **[electron affinity](@entry_id:147520) ($\chi$)**, the energy required to move an electron from the conduction band minimum to the vacuum level: $\chi = E_{\text{vac}} - E_c$.
-   The **Fermi level ($E_F$)**, which represents the electrochemical potential of the electrons. At absolute zero temperature, it is the energy of the highest occupied state. In a doped semiconductor, its position relative to the band edges is determined by the dopant concentration and temperature.
-   The **work function ($\Phi$)**, the energy required to move an electron from the Fermi level to the vacuum level: $\Phi = E_{\text{vac}} - E_F$.

When two semiconductors are brought into intimate electrical contact, the system must reach thermal equilibrium. The defining condition of this equilibrium is the alignment of the Fermi levels across the entire structure, resulting in a single, spatially constant Fermi level $E_F$. To achieve this alignment, charge flows from the material with the initially higher Fermi level to the one with the lower Fermi level, establishing a space-charge region and an internal electrostatic potential that bends the energy bands near the interface.

The simplest model to predict the [band alignment](@entry_id:137089) before considering this [band bending](@entry_id:271304) is **Anderson's rule**, also known as the **electron affinity rule** . This model makes a crucial simplifying assumption: the vacuum level is continuous across the interface. This concept, called **vacuum level alignment**, implies that there are no electrostatic dipoles present at the junction.

Under this assumption, the alignment of the conduction bands is determined solely by the difference in the electron affinities of the two semiconductors, labeled 1 and 2. The **[conduction band offset](@entry_id:1122863) ($\Delta E_c$)**, defined as the difference in the conduction band minima at the interface, $\Delta E_c = E_c^{(2)} - E_c^{(1)}$, is given by:
$$ \Delta E_c = (E_{\text{vac}} - \chi_2) - (E_{\text{vac}} - \chi_1) = \chi_1 - \chi_2 $$

Once the conduction band offset is known, the **[valence band offset](@entry_id:1133686) ($\Delta E_v$)**, defined as $\Delta E_v = E_v^{(2)} - E_v^{(1)}$, can be derived from the fundamental relationship between the bands:
$$ \Delta E_v = E_v^{(2)} - E_v^{(1)} = (E_c^{(2)} - E_g^{(2)}) - (E_c^{(1)} - E_g^{(1)}) $$
$$ \Delta E_v = (E_c^{(2)} - E_c^{(1)}) - (E_g^{(2)} - E_g^{(1)}) = \Delta E_c - (E_g^{(2)} - E_g^{(1)}) $$
This relationship, $\Delta E_c - \Delta E_v = \Delta E_g$, is a universal identity that holds regardless of the specific alignment mechanism.

For instance, consider a hypothetical heterojunction between two undoped semiconductors A and B with $\chi_A = 4.00 \text{ eV}$, $E_{g,A} = 1.80 \text{ eV}$, $\chi_B = 4.35 \text{ eV}$, and $E_{g,B} = 3.30 \text{ eV}$ . According to Anderson's rule, the offsets would be:
$$ \Delta E_c = \chi_A - \chi_B = 4.00 \text{ eV} - 4.35 \text{ eV} = -0.35 \text{ eV} $$
$$ \Delta E_v = \Delta E_c - (E_{g,B} - E_{g,A}) = -0.35 \text{ eV} - (3.30 \text{ eV} - 1.80 \text{ eV}) = -0.35 \text{ eV} - 1.50 \text{ eV} = -1.85 \text{ eV} $$
The negative signs indicate that both the conduction and valence band edges of material B are at lower energies than their counterparts in material A.

### Classification of Band Alignments

The relative positions of the band edges determined by $\Delta E_c$ and $\Delta E_v$ lead to three canonical types of [band alignment](@entry_id:137089), which have profoundly different implications for device operation .

**Type-I (Straddling Gap):** In this alignment, the band gap of one semiconductor is entirely contained within the band gap of the other. This creates a [quantum well](@entry_id:140115) in the narrower-gap material for both electrons and holes. This configuration is ideal for [optoelectronic devices](@entry_id:1129187) like [light-emitting diodes](@entry_id:158696) and laser diodes, where efficient recombination of electrons and holes in the same spatial region is desired. A Type-I alignment occurs when the conduction band of one material is higher and its valence band is lower than the other, which mathematically corresponds to the condition that the offsets have opposite signs: $\Delta E_c \cdot \Delta E_v  0$.

**Type-II (Staggered Gap):** In this alignment, both band edges of one material are lower (or higher) in energy than the corresponding edges of the other material. This creates a potential well for electrons in one material and for holes in the other, leading to the spatial separation of charge carriers across the interface. The Si/GaN heterojunction is an example of a Type-II system . This alignment is useful for photodetectors where separation of photogenerated carriers is desired to produce a [photocurrent](@entry_id:272634). The mathematical condition for a Type-II alignment is that the offsets have the same sign ($\Delta E_c \cdot \Delta E_v > 0$), provided that the gap is not "broken". This non-broken condition can be stated as $-E_g^{(A)}  \Delta E_c  E_g^{(B)}$.

**Type-III (Broken Gap):** This is an extreme case of a Type-II alignment where the staggering is so large that the conduction band minimum of one material lies at a lower energy than the valence band maximum of the other. This creates an energy overlap between the conduction band of one side and the valence band of the other, enabling electrons to tunnel directly from the valence band into the conduction band. Such junctions, like InAs/GaSb, are key components in tunneling field-effect transistors (TFETs) and infrared detectors. The mathematical condition for a broken gap is that the [conduction band offset](@entry_id:1122863) exceeds the band gap of one of the materials, for example, $\Delta E_c \leq -E_g^{(A)}$ or $\Delta E_c \geq E_g^{(B)}$.

### Beyond the Ideal Model: Mechanisms Modifying Band Alignment

While Anderson's rule provides a valuable conceptual starting point, its predictive power is often limited. The central assumption of [vacuum level](@entry_id:756402) alignment is frequently violated in real systems. The actual band alignment is a complex interplay of several physical mechanisms that create potential steps at the interface, independent of the bulk electron affinities. The failure of Anderson's rule is not an exception, but the norm for many technologically important [heterostructures](@entry_id:136451).

#### Interface Dipoles and Charge Redistribution

When two different materials are brought into contact, the atoms at the interface form new chemical bonds. This process involves a subtle redistribution of electronic charge on an atomic scale, creating a microscopic **[interface dipole](@entry_id:143726)**. This dipole can be conceptualized as a thin sheet of positive charge and a parallel sheet of negative charge separated by an atomic-scale distance.

This [charge distribution](@entry_id:144400), $\overline{\rho}(z)$, is highly localized to the interface plane at $z=0$. While the net charge is zero ($\int \overline{\rho}(z) dz = 0$), the distribution possesses a non-zero **dipole moment per unit area**, given by the first moment of the charge density:
$$ p_n = \int_{-\infty}^{+\infty} z \overline{\rho}(z) dz $$

From electrostatics, such a dipole sheet generates an abrupt step in the macroscopic electrostatic potential across the interface . This [potential step](@entry_id:148892), $\Delta\phi$, is directly proportional to the dipole moment per unit area: $\Delta\phi = p_n / \varepsilon_0$. Consequently, the energy of an electron, which is $-e\phi$, experiences a step of $-e\Delta\phi$. This breaks the [vacuum level](@entry_id:756402) alignment. A more direct way to express this is by defining an energy step $\Delta V$ that represents the shift in the vacuum level across the interface: $E_{\text{vac},2} - E_{\text{vac},1} = \Delta V$.

This interface-dipole-induced energy step modifies the band offsets predicted by Anderson's rule. The total [conduction band offset](@entry_id:1122863) becomes the sum of the [electron affinity](@entry_id:147520) difference and the dipole contribution :
$$ \Delta E_c = (\chi_1 - \chi_2) + \Delta V $$
Since the [dipole potential](@entry_id:268699) step rigidly shifts all energy levels of one material relative to the other, the [valence band offset](@entry_id:1133686) is modified by the same amount:
$$ \Delta E_v = \Delta E_v^{(\text{Anderson})} + \Delta V $$
The magnitude of $\Delta V$ can be significant, often on the order of several tenths of an electron-volt, and can even change the alignment type (e.g., from Type-I to Type-II). As the [interface dipole](@entry_id:143726) is a consequence of the specific chemical bonding and quantum mechanics at the junction, it cannot be predicted from bulk properties alone, necessitating more sophisticated [first-principles calculations](@entry_id:749419) or experimental measurements.

#### Fermi-Level Pinning and Interface States

At many interfaces, particularly those involving metals or those with structural imperfections, electronic states can exist at energies within the semiconductor's forbidden band gap. The presence of a high density of these **interface states** can lead to a phenomenon known as **Fermi-level pinning**.

A principal source of such states at metal-semiconductor junctions are **Metal-Induced Gap States (MIGS)**. These are not localized defect states but are evanescent electronic wavefunctions originating from the [continuum of states](@entry_id:198338) in the metal that "tunnel" a short distance into the semiconductor's band gap . These states form a U-shaped continuum across the gap, with a characteristic energy level known as the **Charge Neutrality Level (CNL)**. The CNL is an intrinsic property of the semiconductor, representing the energy at which the gap states, if filled, would result in zero net charge. It is the [branch point](@entry_id:169747) where the character of the gap states transitions from valence-band-like to conduction-band-like.

When the junction is formed, if the metal's Fermi level does not align with the semiconductor's CNL, the interface states will charge up (either by accepting electrons from the metal or donating them to it). This creates an [interface dipole](@entry_id:143726). If the density of [interface states](@entry_id:1126595) ($D_{it}$) is high enough (e.g., $> 10^{13} \text{ cm}^{-2}\text{eV}^{-1}$), even a small misalignment of $E_F$ from the CNL results in a very large dipole. This dipole grows until it shifts the bands to bring the Fermi level very close to the CNL, effectively "pinning" it there.

In this **Bardeen limit** of strong pinning, the Schottky barrier height becomes almost independent of the metal work function and is instead determined by the position of the CNL relative to the semiconductor's band edges. This contrasts with the ideal **Schottky-Mott limit** (analogous to Anderson's rule for heterojunctions), where the barrier height depends linearly on the work function. While MIGS are specific to metal contacts, other [interface states](@entry_id:1126595), such as [dangling bonds](@entry_id:137865) at a semiconductor-insulator interface, can also have an associated CNL and cause Fermi-level pinning in an analogous manner .

#### Strain Effects and Deformation Potentials

Epitaxial growth techniques often involve depositing a crystalline film onto a substrate with a slightly different lattice constant. If the film is thin enough, it grows pseudomorphically, meaning it stretches or compresses in-plane to match the substrate's lattice. This built-in **strain** is a powerful tool for "[band structure engineering](@entry_id:143160)" as it systematically alters the band edge energies.

The strain tensor, $\varepsilon_{ij}$, can be decomposed into two fundamental components:
1.  **Hydrostatic Strain ($\varepsilon_h$)**: The trace of the [strain tensor](@entry_id:193332), $\varepsilon_h = \varepsilon_{xx} + \varepsilon_{yy} + \varepsilon_{zz}$, represents the fractional change in volume. It shifts the band edges without breaking [crystal symmetry](@entry_id:138731).
2.  **Deviatoric (Shear) Strain**: The traceless part of the tensor describes distortions that lower the [crystal symmetry](@entry_id:138731), such as a tetragonal distortion in biaxially strained (001) films.

The effect of these strain components on the band energies is quantified by **deformation potentials**, parameters derived from the **Bir-Pikus Hamiltonian** . The primary effects are:
-   The conduction band minimum ($E_c$) and the average energy of the valence bands ($\Delta E_{v, \text{avg}}$) are shifted by the hydrostatic strain, proportional to the hydrostatic deformation potentials $a_c$ and $a_v$, respectively: $\Delta E_c = a_c \varepsilon_h$ and $\Delta E_{v, \text{avg}} = a_v \varepsilon_h$.
-   For cubic crystals like Si or GaAs, the valence band maximum is degenerate (comprising **heavy-hole (HH)** and **light-hole (LH)** bands). Deviatoric strain lifts this degeneracy. For [biaxial strain](@entry_id:1121545) in a (001) film, this splitting is proportional to the shear [deformation potential](@entry_id:748275) $b$.

By choosing the substrate and alloy composition, one can controllably induce tensile or compressive strain, precisely tuning the [band gaps](@entry_id:191975) and offsets to optimize device performance.

#### Polarization in Wurtzite Heterostructures

Materials like GaN, AlN, and InN, which crystallize in the [non-centrosymmetric](@entry_id:157488) [wurtzite structure](@entry_id:160078), exhibit exceptionally strong polarization effects that often dominate their [heterojunction](@entry_id:196407) properties. The total polarization $\mathbf{P}$ in these materials has two components :
1.  **Spontaneous Polarization ($P_{sp}$)**: An intrinsic, built-in polarization along the polar c-axis ($[0001]$ direction) that exists even in an unstrained crystal due to its structural asymmetry.
2.  **Piezoelectric Polarization ($P_{pz}$)**: A polarization induced by mechanical strain, which is particularly large in these materials.

At a heterojunction, such as AlGaN/GaN, there is a discontinuity in the total polarization, $\Delta\mathbf{P} = \mathbf{P}_2 - \mathbf{P}_1$. According to Maxwell's equations, this discontinuity creates a fixed **bound sheet charge** at the interface with a density given by $\sigma_b = -\hat{n} \cdot \Delta\mathbf{P}$, where $\hat{n}$ is the interface normal.

For a typical Ga-face AlGaN/GaN interface, this sheet charge is positive and extraordinarily large (on the order of $10^{13} \text{ cm}^{-2}$). The immense electric field generated by this charge sheet dramatically bends the bands, pulling the conduction band in the GaN layer far below the Fermi level. This creates a deep and narrow triangular quantum well at the interface, which confines free electrons into a **[two-dimensional electron gas](@entry_id:146876) (2DEG)**. The ability to generate such a high-density 2DEG without any intentional doping is the foundational principle behind the operation of III-nitride High Electron Mobility Transistors (HEMTs).

### A Note on Linearity and Transitivity

A natural question arises from these principles: if we know the [band offset](@entry_id:142791) between materials A and B, and between B and C, can we predict the offset between A and C? This is the question of **[transitivity](@entry_id:141148)**, which states $\Delta E_c(A/C) \stackrel{?}{=} \Delta E_c(A/B) + \Delta E_c(B/C)$.

In an ideal world governed by Anderson's rule, [transitivity](@entry_id:141148) would hold perfectly, as $\Delta E_c(A/C) = \chi_A - \chi_C = (\chi_A - \chi_B) + (\chi_B - \chi_C) = \Delta E_c(A/B) + \Delta E_c(B/C)$. However, in the real world, [transitivity](@entry_id:141148) often fails.

The validity of [transitivity](@entry_id:141148) rests on the additivity of the interface potential lineups. It fails when the dipole at an A/C interface is not simply the sum of dipoles at A/B and B/C interfaces . This failure is caused by the very mechanisms discussed in this chapter:
-   **Non-transferable chemical dipoles**: The specific bonding at the A/C interface is unique and not a superposition of A/B and B/C bonding.
-   **Polarization-induced fields**: In polar [heterostructures](@entry_id:136451), the fixed charges generate internal fields within the intermediate layer (B), adding a thickness-dependent potential drop that breaks simple additivity.
-   **Interface structure**: Differences in crystallographic orientation, strain state, or defect densities between the interfaces being compared will invalidate the rule.

The potential failure of [transitivity](@entry_id:141148) serves as a crucial reminder that band alignment is not merely a function of the bulk materials involved, but is an intrinsic property of the specific interface itself. A comprehensive understanding requires moving beyond simple rules and embracing the complex interplay of electrostatics, quantum mechanics, and materials science at the atomic scale.