## Introduction
The McLafferty rearrangement is one of the most important and diagnostically useful fragmentation reactions in [mass spectrometry](@entry_id:147216), providing deep structural insights into organic molecules. Its ability to predictably cleave a molecule based on its [functional groups](@entry_id:139479) and alkyl chain structure makes it an indispensable tool for chemists. However, mastering its application requires a deep grasp of its underlying mechanism, structural prerequisites, and its competitive nature against other fragmentation pathways. This article provides a comprehensive exploration of this reaction. The first chapter, "Principles and Mechanisms," will dissect the core process, from the crucial role of the γ-hydrogen to the kinetics that govern its competition with other cleavages. Following this, "Applications and Interdisciplinary Connections" will demonstrate how this knowledge is applied to solve real-world analytical problems, from identifying isomers to its connections with [photochemistry](@entry_id:140933) and [metabolomics](@entry_id:148375). Finally, "Hands-On Practices" will offer targeted exercises to solidify your understanding and test your ability to apply these concepts in practice.

## Principles and Mechanisms

The fragmentation of radical cations in the gas phase, as observed in [electron ionization](@entry_id:181441) mass spectrometry (EI-MS), is a rich field governed by the principles of [physical organic chemistry](@entry_id:184637). Among the most characteristic and diagnostically useful of these [unimolecular reactions](@entry_id:167301) is the **McLafferty rearrangement**. This process, a specific type of intramolecular hydrogen transfer, provides profound insight into the structure of the parent molecule. This chapter will dissect the fundamental principles and mechanisms of the McLafferty rearrangement, exploring its prerequisites, its competition with other fragmentation pathways, and its relationship to other rearrangement processes.

### The Core Mechanism: A Six-Membered Journey

The McLafferty rearrangement is a fragmentation pathway predominantly observed for odd-electron radical cations containing an unsaturated functional group, most classically a [carbonyl group](@entry_id:147570) (ketone, aldehyde, ester, or carboxylic acid), but also applicable to oximes, [amides](@entry_id:182091), and certain [aromatic systems](@entry_id:202576). The reaction's defining feature is the intramolecular transfer of a hydrogen atom to the radical cation site through a six-membered cyclic transition state.

#### The Indispensable γ-Hydrogen

The single most critical structural prerequisite for the canonical McLafferty rearrangement is the presence of an accessible **γ-hydrogen**. To understand this requirement, we must first define the standard nomenclature for positions relative to a carbonyl group. The carbon atoms in an alkyl chain attached to the carbonyl carbon are labeled with successive Greek letters:

-   The carbon atom directly bonded to the carbonyl carbon is the **α-carbon**.
-   The next carbon atom in the chain is the **β-carbon**.
-   The carbon atom following the β-carbon is the **γ-carbon**.

A hydrogen atom attached to the γ-carbon is therefore termed a γ-hydrogen. Numerically, if the carbonyl carbon is considered position 0, the γ-carbon is at position 3, reached by traversing three successive carbon-carbon bonds. The transfer of this specific hydrogen is what enables the rearrangement.

#### The Concerted Rearrangement and its Products

Upon [electron ionization](@entry_id:181441), a non-bonding electron is typically removed from the carbonyl oxygen, creating a molecular [radical cation](@entry_id:754018), $[M]^{+\bullet}$. If this ion possesses a γ-hydrogen, the McLafferty rearrangement can proceed. The mechanism is a concerted process that can be visualized with single-electron "fishhook" arrows:

1.  **Hydrogen Abstraction:** The radical on the carbonyl oxygen abstracts a γ-hydrogen atom. This involves the homolytic cleavage of the Cγ–H bond.
2.  **Bond Reorganization:** Simultaneously, the σ-bond between the α- and β-carbons cleaves, and a new π-bond is formed between the β- and γ-carbons.
3.  **Product Formation:** This concerted electronic reshuffling results in the formation of two species: a new [radical cation](@entry_id:754018) and a neutral molecule.

The overall transformation is:
$$ [\mathrm{R}{-}\mathrm{C}({=}\mathrm{O}){-}\mathrm{C}_{\alpha}\mathrm{H}_{2}{-}\mathrm{C}_{\beta}\mathrm{H}_{2}{-}\mathrm{C}_{\gamma}\mathrm{HR}']^{+\bullet} \rightarrow [\mathrm{R}{-}\mathrm{C}(\mathrm{OH}){=}\mathrm{C}_{\alpha}\mathrm{H}_{2}]^{+\bullet} + \mathrm{H}_{2}\mathrm{C}_{\beta}{=}\mathrm{C}_{\gamma}\mathrm{HR}' $$

The charged product, $[\mathrm{R}{-}\mathrm{C}(\mathrm{OH}){=}\mathrm{C}_{\alpha}\mathrm{H}_{2}]^{+\bullet}$, is an **enol radical cation**. This fragment is conventionally termed the **McLafferty ion**. The uncharged product, $\mathrm{H}_{2}\mathrm{C}_{\beta}{=}\mathrm{C}_{\gamma}\mathrm{HR}'$, is a stable **alkene**, referred to as the **neutral co-fragment**. The charge is preferentially retained by the enol fragment in accordance with **Stevenson's rule**, which posits that upon fragmentation, the positive charge remains with the fragment having the lower [ionization energy](@entry_id:136678). The [ionization energy](@entry_id:136678) of an enol is generally lower than that of a comparable alkene, thus favoring the formation of the enol radical cation. The diagnostic value of this rearrangement lies in the specific mass of the neutral alkene lost, which directly reveals the structure of the alkyl chain beyond the β-carbon.

### Structural and Conformational Prerequisites

The mere presence of a γ-hydrogen is a necessary but not [sufficient condition](@entry_id:276242) for the McLafferty rearrangement. The reaction is exquisitely sensitive to the molecule's ability to adopt the required six-membered cyclic transition state geometry.

#### Conformational Accessibility

For the γ-hydrogen to be transferred to the carbonyl oxygen, the two must come into close proximity (typically within ~1.8 Å). In flexible, acyclic molecules, such as **2-heptanone**, the [free rotation](@entry_id:191602) around carbon-carbon single bonds allows the molecule to easily adopt the required chair-like transition state conformation. Consequently, 2-heptanone exhibits a very prominent McLafferty fragment ion in its mass spectrum.

However, if the molecular architecture prevents this conformation, the rearrangement is kinetically hindered or completely blocked. Two illustrative examples demonstrate this principle:

1.  **Absence of γ-Hydrogens:** In **3,3-dimethyl-2-butanone (pinacolone)**, the carbon α to the carbonyl is a quaternary tert-butyl carbon. The methyl groups attached to it are β-carbons. There are no γ-carbons, and thus no γ-hydrogens. The McLafferty rearrangement is structurally impossible for this molecule.

2.  **Conformational Locking:** In **trans-4-tert-butylcyclohexanone**, the bulky tert-butyl group acts as a conformational anchor, locking the six-membered ring into a rigid [chair conformation](@entry_id:137492) where the tert-butyl group occupies an equatorial position. While this molecule does possess γ-hydrogens (on C-3 and C-5 of the ring), these hydrogens are held at a fixed distance from the carbonyl oxygen, far too great to allow for the formation of the transition state. Forcing the rigid ring into a high-energy twist-[boat conformation](@entry_id:169006) that would bring the atoms closer is enthalpically prohibitive. Thus, despite the presence of γ-hydrogens, the McLafferty rearrangement is effectively "gated out" by conformational restriction.

#### The Role of Ring Strain

The influence of [molecular geometry](@entry_id:137852) is even more pronounced in highly strained systems. Consider **2-ethylcyclobutanone**. This molecule possesses γ-hydrogens on the terminal methyl of its ethyl [substituent](@entry_id:183115). However, the atoms involved in forming the [six-membered transition state](@entry_id:754931) include C-1 and C-2 of the cyclobutane ring. The natural [bond angles](@entry_id:136856) in this four-membered ring are severely compressed (to ~90°). The [six-membered transition state](@entry_id:754931), in contrast, prefers angles closer to the tetrahedral ideal of 109.5°. Forcing the atoms of the cyclobutane ring into this transition state geometry would introduce an immense amount of additional angle and [torsional strain](@entry_id:195818). This creates a very large enthalpic barrier of activation ($\Delta H^{\ddagger}$), making the McLafferty rearrangement kinetically inaccessible. As a result, the fragmentation of 2-ethylcyclobutanone is dominated by other pathways, such as ring cleavage, and the McLafferty rearrangement is suppressed or absent.

### The Kinetics of Competition

The McLafferty rearrangement does not occur in isolation; it is always in competition with other fragmentation pathways. Understanding which pathway dominates requires an examination of their relative rates, which are governed by the principles of chemical kinetics.

#### McLafferty vs. α-Cleavage

The most common competitor to the McLafferty rearrangement in ketones is **[α-cleavage](@entry_id:756846)**. This is a simple homolytic cleavage of a C-C bond adjacent to the carbonyl group, which produces a stable, even-electron [acylium ion](@entry_id:201351) ($\mathrm{R}{-}\mathrm{C}{\equiv}\mathrm{O}^{+}$) and an alkyl radical.
$$ [\mathrm{R}{-}\mathrm{C}({=}\mathrm{O}){-}\mathrm{R}']^{+\bullet} \rightarrow \mathrm{R}{-}\mathrm{C}{\equiv}\mathrm{O}^{+} + \cdot\mathrm{R}' $$
[α-cleavage](@entry_id:756846) does not involve hydrogen transfer and has less stringent geometric requirements than a rearrangement. Consequently, when the McLafferty pathway is blocked for either structural or conformational reasons (as in pinacolone or trans-4-tert-butylcyclohexanone), the lower-barrier [α-cleavage](@entry_id:756846) pathway typically becomes dominant.

#### A Deeper Look: Transition State Theory

The competition between a rearrangement and a simple cleavage can be rationalized using **Transition State Theory (TST)**. The rate constant ($k$) is related to the [activation parameters](@entry_id:178534), [enthalpy of activation](@entry_id:167343) ($\Delta H^{\ddagger}$) and [entropy of activation](@entry_id:169746) ($\Delta S^{\ddagger}$).

-   The **McLafferty rearrangement** proceeds through a highly ordered, constrained, six-membered cyclic transition state. The loss of internal rotational freedom required to form this "tight" transition state results in a significant decrease in entropy, meaning $\Delta S^{\ddagger}$ is negative.
-   A simple **bond cleavage** (like α- or β-cleavage), in contrast, proceeds through a "loose" transition state where a bond is simply stretched to its breaking point. As the fragments begin to separate, they gain rotational and translational freedom, resulting in an increase in entropy, meaning $\Delta S^{\ddagger}$ is positive.

This difference in $\Delta S^{\ddagger}$ has profound consequences. The high-pressure limiting rate constant is given by the Eyring equation: $k_{\infty} = \frac{k_B T}{h} \exp(\frac{\Delta S^{\ddagger}}{R}) \exp(\frac{-\Delta H^{\ddagger}}{RT})$. The term $\exp(\frac{\Delta S^{\ddagger}}{R})$, a component of the pre-exponential factor, is much smaller for the tight McLafferty transition state than for the loose cleavage. This means that even if the McLafferty rearrangement has a lower [activation enthalpy](@entry_id:199775) ($\Delta H^{\ddagger}$), its rate increases less steeply with internal energy compared to the entropically favored simple cleavage. As we will see, this makes the [branching ratio](@entry_id:157912) between the two pathways highly dependent on the ion's internal energy.

### Influence of Experimental Conditions: The Role of Electron Energy

The internal energy of the [molecular ion](@entry_id:202152) is not fixed; it follows a distribution that is strongly influenced by the kinetic energy of the ionizing electrons ($E_e$) used in the EI source. This provides an experimental lever to control fragmentation.

-   **Standard EI ($E_e = 70\,\mathrm{eV}$):** At the conventional electron energy of $70\,\mathrm{eV}$, a large amount of energy is available, leading to a broad distribution of internal energies in the [molecular ion](@entry_id:202152) population. A significant fraction of ions are formed with very high internal energy. At these high energies, the fast, entropically-favored simple cleavage reactions tend to outcompete the slower, entropically-disfavored rearrangement reactions. Furthermore, the primary fragment ions (including the McLafferty ion) may themselves have enough internal energy to undergo secondary fragmentation. For these reasons, at $70\,\mathrm{eV}$, the relative abundance of rearrangement ions is often diminished.

-   **"Soft" EI ($E_e \approx 20\,\mathrm{eV}$):** When the electron energy is lowered to a value just above the molecule's ionization energy (e.g., $15\,\mathrm{eV}$), the amount of energy deposited into the ion is much smaller and the internal energy distribution is narrower and concentrated at lower energies. This selectively populates ions with enough energy to surpass low-energy barriers but not high-energy ones. Since rearrangements like the McLafferty pathway often have the lowest energy barriers, they become the dominant fragmentation channel under these "soft" [ionization](@entry_id:136315) conditions. High-threshold cleavages and secondary fragmentations are disproportionately suppressed, leading to a "cleaner" mass spectrum where the molecular ion and low-energy rearrangement fragments are more prominent. This phenomenon makes low-energy EI a powerful tool for enhancing diagnostic rearrangement peaks.

### Variations and Related Mechanisms

The canonical McLafferty rearrangement is the most prominent member of a family of related processes.

#### The McLafferty+1 Rearrangement

In the mass spectra of certain compounds, particularly long-chain esters and acids, a peak is observed one mass unit higher than the expected McLafferty ion. This is attributed to the **McLafferty+1 rearrangement**. This process is understood to involve the initial, canonical McLafferty rearrangement to form an intermediate ion-neutral complex. Before the two fragments separate, a second hydrogen atom is transferred from the neutral alkene fragment to the enol radical cation. This second transfer produces a protonated enol, which is a stable, **even-electron** ion. Because its composition is increased by one hydrogen atom, its mass-to-charge ratio is shifted by approximately $+1\,\mathrm{u}$ relative to the canonical McLafferty ion.

#### Distinction from Charge-Remote Fragmentation

It is crucial to distinguish the McLafferty rearrangement from another class of fragmentation known as **[charge-remote fragmentation](@entry_id:747283) (CRF)**.

-   The **McLafferty rearrangement** is a hallmark of **odd-electron** radical cations (from EI) and is a **charge-and-radical-directed** process. The reaction is initiated and mediated by the functional group bearing the charge and radical site. It typically results in a single, diagnostic neutral loss.

-   **Charge-remote fragmentation** is most prominent in the high-energy fragmentation (e.g., via [collision-induced dissociation](@entry_id:167315), CID) of **even-electron** ions, such as those formed by [electrospray ionization](@entry_id:192799) (ESI). In CRF, the charge site is chemically inert and sequestered from a long, saturated chain (like a fatty acid chain). The fragmentation occurs along the chain, remote from the charge, through a mechanism akin to a [thermal decomposition](@entry_id:202824). This process does not produce a single diagnostic loss but rather a "ladder" of fragment ions, often separated by $14\,\mathrm{u}$ (the mass of a $\mathrm{CH_2}$ group), as the chain breaks apart at multiple locations.

Therefore, switching the ionization method from EI to ESI will suppress the canonical McLafferty rearrangement (by forming even-electron ions) and can enhance [charge-remote fragmentation](@entry_id:747283) if the molecule has the appropriate structure and is subjected to energetic collisions. This distinction underscores the importance of ion structure—odd-electron versus even-electron—in dictating fragmentation behavior.