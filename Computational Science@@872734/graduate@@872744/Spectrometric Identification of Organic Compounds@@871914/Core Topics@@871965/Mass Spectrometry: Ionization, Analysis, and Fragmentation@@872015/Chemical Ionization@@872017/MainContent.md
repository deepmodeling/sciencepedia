## Introduction
In the landscape of [mass spectrometry](@entry_id:147216), the ability to determine a molecule's mass is paramount. However, high-energy techniques like Electron Ionization (EI) often shatter fragile molecules, obscuring this fundamental piece of information. Chemical Ionization (CI) emerges as a powerful solution to this problem, offering a 'soft' ionization approach that preserves the intact molecule. This technique relies on gentle gas-phase chemical reactions rather than brute-force [electron impact](@entry_id:183205), making it indispensable for identifying compounds that would otherwise remain elusive.

This article provides a comprehensive exploration of chemical ionization, designed for the graduate-level student and practicing chemist. The journey begins in the **Principles and Mechanisms** chapter, where we will dissect the fundamental physics of the high-pressure ion source, the formation of [reagent ions](@entry_id:754127), and the thermochemical rules that govern [proton transfer](@entry_id:143444) and collisional cooling. Next, the **Applications and Interdisciplinary Connections** chapter demonstrates how these principles are applied to solve real-world analytical problems, from unambiguous [molecular weight determination](@entry_id:198232) and strategic [reagent gas](@entry_id:754126) selection to the ultra-sensitive analysis enabled by Negative Chemical Ionization (NCI). Finally, the **Hands-On Practices** section solidifies this knowledge through targeted problems, challenging you to apply thermodynamic principles and predict spectral outcomes. Together, these chapters will equip you with a deep, practical understanding of one of mass spectrometry's most versatile tools.

## Principles and Mechanisms

Chemical Ionization (CI) is a [soft ionization](@entry_id:180320) technique in mass spectrometry that generates ions through gas-phase ion-molecule reactions. Unlike Electron Ionization (EI), which involves direct, high-energy [electron impact](@entry_id:183205) on analyte molecules in a high-vacuum environment, CI utilizes a fundamentally indirect approach. This chapter elucidates the core principles and mechanisms governing this powerful technique, from the instrumental setup to the rich [chemical physics](@entry_id:199585) that dictates its outcomes.

### The Fundamental Principle: Indirect Ionization in a High-Pressure Regime

The defining characteristic of chemical [ionization](@entry_id:136315) is the presence of a [reagent gas](@entry_id:754126) within the ion source at a relatively high pressure, typically in the range of $0.1$ to $2$ Torr. This is in stark contrast to the low-pressure conditions of EI (typically $\lt 10^{-5}$ Torr). This high-pressure environment is not merely an incidental condition; it is the cornerstone of the entire CI mechanism and has two profound consequences.

First, the [reagent gas](@entry_id:754126) is present in vast excess relative to the analyte, often by a factor of $10^4$ to $10^5$. When energetic electrons are introduced into the source, they are statistically far more likely to collide with and ionize the abundant [reagent gas](@entry_id:754126) molecules rather than the trace analyte molecules. This constitutes the **primary [ionization](@entry_id:136315)** step in CI, where a plasma of [reagent ions](@entry_id:754127) is created. The analyte itself largely evades direct, high-energy [electron impact](@entry_id:183205). [@problem_id:3696226]

Second, the high pressure dramatically reduces the **[mean free path](@entry_id:139563)**—the average distance a particle travels between collisions. At a typical CI pressure of $1$ Torr, the [mean free path](@entry_id:139563) is on the order of micrometers, far smaller than the dimensions of the ion source. This creates a dense, **high-collision environment**. This environment is crucial for both the evolution of the reagent ion plasma and the subsequent ionization and stabilization of the analyte. [@problem_id:3696287]

Consequently, CI is a two-stage process:
1.  **Reagent Ion Formation**: Energetic electrons ionize a [reagent gas](@entry_id:754126), and these primary ions undergo rapid ion-molecule reactions with the neutral [reagent gas](@entry_id:754126) to form a stable population of secondary, thermalized [reagent ions](@entry_id:754127).
2.  **Analyte Ionization**: These [reagent ions](@entry_id:754127) then ionize the analyte molecules through gentle, low-energy ion-molecule reactions.

The result is a "soft" ionization process that imparts minimal internal energy to the analyte, thereby suppressing fragmentation and often yielding an abundant signal for an ion related to the intact molecule, such as the protonated molecule $[M+H]^+$. This feature makes CI an invaluable tool for determining the molecular weight of compounds that fragment extensively under EI conditions.

### The Anatomy of a Chemical Ionization Source

To sustain the high-pressure regime required for CI while maintaining the high vacuum necessary for the [mass analyzer](@entry_id:200422), the CI source has a specialized design. Its key components work in concert to manage the pressure differential and orchestrate the ion-molecule chemistry. [@problem_id:3696209]

A **[reagent gas](@entry_id:754126) inlet** connected to a precision **leak valve** allows for the controlled introduction of the [reagent gas](@entry_id:754126) (e.g., methane, isobutane, or ammonia) into the ion source, meticulously regulating the pressure to the optimal range of $0.1$ to $2$ Torr. The [ionization](@entry_id:136315) volume itself is constructed to be relatively "tight" or enclosed, minimizing gas leakage.

A **heated filament**, typically made of [tungsten](@entry_id:756218) or rhenium, produces electrons via [thermionic emission](@entry_id:138033). These electrons are then accelerated by a [potential difference](@entry_id:275724) into the ion source. In Positive Chemical Ionization (PCI), the electrons are accelerated to high kinetic energies, often $100$–$200$ eV, to maximize the [ionization cross-section](@entry_id:166427) of the [reagent gas](@entry_id:754126). [@problem_id:3696209] [@problem_id:3696207]

The **ionization region** is where the magic happens. It is a confined volume where the high-pressure [reagent gas](@entry_id:754126), trace analyte, and energetic electrons mix, allowing for the cascade of collisions and reactions to occur. This region is connected to the [mass analyzer](@entry_id:200422) through a small **ion exit [aperture](@entry_id:172936)**. This aperture, along with powerful **[differential pumping](@entry_id:202626)** systems, maintains the [critical pressure](@entry_id:138833) gradient between the high-pressure source and the high-vacuum ($10^{-5}$ Torr) analyzer.

Finally, a series of **ion optics**, including a repeller electrode within the source and various extraction and focusing lenses, create electric fields that efficiently extract the newly formed analyte ions, guide them out of the source, and focus them into a beam directed towards the [mass analyzer](@entry_id:200422).

### Positive Chemical Ionization (PCI)

In Positive Chemical Ionization (PCI), the analyte is ionized by reacting with positively charged [reagent ions](@entry_id:754127). The specific reactions that occur are governed by the thermochemical properties of both the reagent and the analyte.

#### Formation of Reagent Ions: The Methane Example

Methane ($\mathrm{CH_4}$) is the most common and classic PCI [reagent gas](@entry_id:754126). When methane at $\approx 1$ Torr is bombarded with energetic electrons, the primary ions formed are $\mathrm{CH_4^+}$ and its fragment $\mathrm{CH_3^+}$. However, due to the high collision frequency, these primary ions are highly reactive and are almost instantaneously consumed in reactions with neutral methane molecules. These secondary reactions produce a stable plasma of the actual [reagent ions](@entry_id:754127). [@problem_id:3696272]

The principal reactions are:
- Formation of the methanium ion: $\mathrm{CH_4^+ + CH_4 \to CH_5^+ + CH_3^\bullet}$
- Formation of the ethyl cation: $\mathrm{CH_3^+ + CH_4 \to [C_2H_7^+]^* \to C_2H_5^+ + H_2}$

The resulting plasma is dominated by the even-electron, superacidic **methanium ion** ($\mathrm{CH_5^+}$) and the **ethyl cation** ($\mathrm{C_2H_5^+}$), which serve as the primary chemical reactants for ionizing the analyte.

#### Ion-Molecule Reaction Pathways in PCI

When an analyte molecule $M$ encounters the reagent ion plasma, several types of reactions can occur. The most common pathways include proton transfer, hydride abstraction, and [adduct formation](@entry_id:746281). [@problem_id:3696266]

1.  **Proton Transfer**: This is the most prevalent mechanism in PCI, leading to the formation of the **protonated molecule**, $[M+H]^+$. The reagent ion acts as a Brønsted acid, donating a proton to the analyte.
    $$ R\mathrm{H}^{+} + M \to M\mathrm{H}^{+} + R $$
    For example, with methane CI, the reaction is:
    $$ \mathrm{CH_5^+} + M \to [M+H]^+ + \mathrm{CH_4} $$

2.  **Hydride Abstraction**: Lewis acidic [reagent ions](@entry_id:754127), particularly [carbocations](@entry_id:185610) like $\mathrm{C_2H_5^+}$, can abstract a hydride ion ($\mathrm{H}^-$) from the analyte. This results in an $[M-H]^+$ ion.
    $$ \mathrm{C_2H_5^+} + M \to [M-H]^+ + \mathrm{C_2H_6} $$
    This pathway is common for analytes such as [alkanes](@entry_id:185193) and some alcohols.

3.  **Adduct Formation**: In some cases, the reagent ion can form a stable, non-covalent complex with the analyte molecule. This is particularly common when using ammonia as the [reagent gas](@entry_id:754126), which forms the ammonium adduct, $[M+\mathrm{NH_4}]^+$.
    $$ \mathrm{NH_4^+} + M \rightleftharpoons [M+\mathrm{NH_4}]^+ $$
    The stability of these adducts is highly dependent on collisional stabilization provided by the high-pressure bath gas.

#### The Thermodynamic Basis of Soft Ionization

The "softness" of CI, its ability to produce molecular ions with minimal fragmentation, stems from two cooperative effects: controlled energy deposition and efficient collisional cooling.

The energy imparted to the analyte ion during [proton transfer](@entry_id:143444) is governed by the reaction's exothermicity. The **[proton affinity](@entry_id:193250)** ($PA$) of a molecule is defined as the negative of the [enthalpy change](@entry_id:147639) for its gas-phase protonation ($X + H^{+} \to XH^{+}$). Using Hess's law, we can derive that the enthalpy change for the proton transfer reaction $R\mathrm{H}^{+} + M \to M\mathrm{H}^{+} + R$ is given by $\Delta H_{rxn} = PA(R) - PA(M)$. For the reaction to be exothermic and proceed favorably, the [proton affinity](@entry_id:193250) of the analyte must be greater than that of the [reagent gas](@entry_id:754126)'s [conjugate base](@entry_id:144252), i.e., **$PA(M) > PA(R)$**. [@problem_id:3696264]

The energy released, or exothermicity, is $\Delta H = -\Delta H_{rxn} = PA(M) - PA(R)$. This energy, typically on the order of $1-3$ eV, is partitioned among the products. While this is far less energy than that deposited in a $70$ eV EI collision, it can still be sufficient to cause fragmentation.

This is where the high-pressure environment plays its second critical role: **collisional cooling**. A newly formed, vibrationally excited $[M+H]^+$ ion undergoes thousands to millions of collisions per second with the cool [reagent gas](@entry_id:754126) molecules. [@problem_id:3696287] These collisions efficiently siphon off the excess internal energy, quenching the ion to a state of thermal equilibrium with the source temperature before it has a chance to dissociate. This process, also known as **[thermalization](@entry_id:142388)**, drives the internal energy distribution of the product ions towards a narrow, low-energy Boltzmann distribution, drastically reducing fragmentation and preserving the molecular ion.

#### Tuning Ionization Softness: The Role of the Reagent Gas

The magnitude of the reaction exothermicity, and thus the "softness" of the [ionization](@entry_id:136315), can be controlled by judiciously choosing the [reagent gas](@entry_id:754126). The strength of a gas-phase acid $RH^+$ is inversely proportional to the [proton affinity](@entry_id:193250) of its [conjugate base](@entry_id:144252) $R$. A [reagent gas](@entry_id:754126) with a lower PA forms a stronger acid reagent ion, resulting in a more exothermic, or "harder," [proton transfer](@entry_id:143444) reaction. [@problem_id:3696258]

A hierarchy of common reagent gases allows the analyst to tune the [ionization](@entry_id:136315) conditions:
-   **Methane** ($PA(\mathrm{CH_4}) \approx 544$ kJ mol$^{-1}$): Forms the very strong acid $\mathrm{CH_5^+}$. It will protonate almost all organic molecules, but the large exothermicity can still cause some fragmentation.
-   **Isobutane** ($PA(\text{isobutene}) \approx 824$ kJ mol$^{-1}$): Forms a much weaker acid, $t\text{-}\mathrm{C_4H_9^+}$. It provides gentler protonation than methane and is more selective, only protonating analytes with $PA > 824$ kJ mol$^{-1}$.
-   **Ammonia** ($PA(\mathrm{NH_3}) \approx 853$ kJ mol$^{-1}$): Forms the very [weak acid](@entry_id:140358) $\mathrm{NH_4^+}$. It is highly selective and provides exceptionally [soft ionization](@entry_id:180320), often yielding only the $[M+H]^+$ ion or the $[M+\mathrm{NH_4}]^+$ adduct with virtually no fragmentation for suitable analytes. [@problem_id:3696287]

By selecting a [reagent gas](@entry_id:754126) whose PA is slightly lower than the analyte's estimated PA, one can achieve efficient yet gentle ionization.

### Negative Chemical Ionization (NCI)

Negative Chemical Ionization (NCI) operates on a different principle from PCI. Instead of using reagent cations, the most common form of NCI, known as **Electron Capture Negative Ionization (ECNI)**, uses low-energy, thermalized electrons as the primary chemical reactant.

#### Generation and Role of Thermal Electrons

The goal in ECNI is to create a dense population of electrons with near-zero kinetic energy ($E \approx k_B T \approx 0.02-0.04$ eV). The cross-section for [electron capture](@entry_id:158629) by an electronegative molecule is typically largest at or near zero electron energy. [@problem_id:3696207]

To achieve this, the instrument settings are adjusted. While electrons are still generated from a filament and accelerated, they quickly lose their initial energy through multiple [inelastic collisions](@entry_id:137360) with the dense [reagent gas](@entry_id:754126), which now acts as a **moderator gas**. To enhance this **electron thermalization** process, NCI often employs higher [reagent gas](@entry_id:754126) pressures and instrumental features like a weak magnetic field or specific [ion trap](@entry_id:192565) potentials that increase the residence time and path length of electrons in the source, maximizing the number of energy-losing collisions they undergo. [@problem_id:3696207]

#### Negative Ion Formation Pathways

For an analyte $M$ with a sufficiently high **electron affinity** ($EA$)—a measure of the energy released upon binding an electron—two main [electron capture](@entry_id:158629) pathways exist. [@problem_id:3696237]

1.  **Resonance Electron Capture**: A thermal electron attaches to the analyte molecule to form a stable parent molecular anion, $M^-$.
    $$ M + e^-_{th} \to M^- $$
    This process is energetically favorable if $EA(M) > 0$. The excess energy, $E_{excess} = EA(M) + E_e$, is dissipated through collisions with the bath gas. For molecules like nitrobenzene with a positive EA, this process is efficient at near-zero electron energies.

2.  **Dissociative Electron Capture**: The attachment of an electron leads to the cleavage of a bond and the formation of a fragment anion.
    $$ AB + e^- \to A^\bullet + B^- $$
    The minimum electron energy required for this process, its energy threshold, is given by $E_{threshold} \approx D_0(A-B) - EA(B)$, where $D_0$ is the [bond dissociation energy](@entry_id:136571) and $EA(B)$ is the [electron affinity](@entry_id:147520) of the fragment that captures the electron. For a molecule like nitrobenzene ($\mathrm{C_6H_5NO_2}$), the formation of $\mathrm{NO_2^-}$ is governed by the C-N [bond energy](@entry_id:142761) and the very high electron affinity of $\mathrm{NO_2}$. The calculation reveals that this process is actually exothermic ($E_{threshold}  0$), meaning it can be initiated by thermal electrons. This pathway can be highly specific and sensitive for certain classes of compounds. [@problem_id:3696237]

### Practical Considerations: The Influence of Contaminants

The chemistry within a CI source is exquisitely sensitive to the gas composition. Even trace amounts of contaminants with high proton affinities, such as water, can dramatically alter the reagent ion plasma and the resulting mass spectrum. [@problem_id:3696252]

Water has a [proton affinity](@entry_id:193250) ($PA(\mathrm{H_2O}) \approx 691$ kJ mol$^{-1}$) that is significantly higher than that of methane. If trace water is present in a methane CI source, it will effectively scavenge protons from the primary [reagent ions](@entry_id:754127) ($\mathrm{CH_5^+}$) to form hydronium ions ($\mathrm{H_3O^+}$) and their clusters ($(H_2O)_n H^+$).

The ionization of an analyte $M$ is then governed by its reaction with this modified water-based plasma. The outcome depends critically on the analyte's [proton affinity](@entry_id:193250) relative to water's.
-   If $PA(M) \gg PA(\mathrm{H_2O})$, as for a highly basic analyte, proton transfer from $\mathrm{H_3O^+}$ will be highly exothermic. The large amount of energy released will cause any transiently formed water adducts to "boil off" their water molecules, resulting in a dominant $[M+H]^+$ signal.
-   If $PA(M)$ is only slightly greater than $PA(\mathrm{H_2O})$, the proton transfer reaction will have very low exothermicity. The small amount of excess energy is insufficient to drive rapid [dissociation](@entry_id:144265) of water adducts. Collisional stabilization can then effectively cool and preserve these clusters, leading to significant signals for ions such as $[M(H_2O)H]^+$ and $[M(H_2O)_2H]^+$.

Furthermore, these weakly bound adducts are sensitive to temperature. Increasing the source temperature will shift the equilibrium away from cluster formation, favoring the bare protonated molecule $[M+H]^+$. Understanding these effects is crucial for interpreting CI spectra and troubleshooting unexpected results in practice. [@problem_id:3696252]