## Introduction
The charge state of an amino acid side chain—whether it is protonated or deprotonated—is a fundamental determinant of [protein structure and function](@entry_id:272521). These ionization states dictate the electrostatic landscape of a macromolecule, controlling its folding, stability, catalytic activity, and interactions with other molecules. While the intrinsic [acid-base properties](@entry_id:190019) of isolated amino acids in water are well-understood, these properties are profoundly altered within the complex and heterogeneous environment of a folded protein. The central challenge, and the focus of this article, is to understand the principles that govern these shifts in [ionization](@entry_id:136315) behavior and to appreciate their far-reaching consequences in biology. This article will provide a graduate-level exploration of this critical topic, bridging fundamental chemistry with complex biological function.

The first chapter, **Principles and Mechanisms**, lays the theoretical groundwork. It revisits the Henderson-Hasselbalch equation and the thermodynamic basis of $\mathrm{p}K_a$, then delves into how the protein environment—through dielectric effects and specific interactions—perturbs these intrinsic values, leading to complex phenomena like coupled equilibria. The second chapter, **Applications and Interdisciplinary Connections**, illustrates the functional importance of these principles. It explores how tuned $\mathrm{p}K_a$ values drive [enzyme catalysis](@entry_id:146161), maintain [protein stability](@entry_id:137119), and create sophisticated $\mathrm{pH}$-sensitive switches in diverse fields from immunology to [neurobiology](@entry_id:269208). Finally, the **Hands-On Practices** section offers a set of targeted problems designed to solidify your understanding and apply these concepts to realistic biochemical scenarios. By progressing through these chapters, you will gain a deep, mechanistic appreciation for how proteins harness the simple chemistry of the proton to achieve complex biological outcomes.

## Principles and Mechanisms

The function of a protein is inextricably linked to its three-dimensional structure, which in turn is governed by a delicate balance of intermolecular forces. Among the most crucial of these are [electrostatic interactions](@entry_id:166363), which are profoundly influenced by the [ionization](@entry_id:136315) states of the [amino acid side chains](@entry_id:164196). Whether a side chain is protonated or deprotonated determines its charge, its capacity to act as a [hydrogen bond donor](@entry_id:141108) or acceptor, and its ability to participate in catalysis. Understanding the principles that dictate these [ionization](@entry_id:136315) states is therefore fundamental to biochemistry. This chapter will dissect the principles and mechanisms governing side chain protonation, from the thermodynamics of isolated groups in water to the complex, coupled equilibria within the heterogeneous environment of a folded protein.

### Fundamental Principles of Side Chain Ionization

The [ionization](@entry_id:136315) behavior of any chemical group is described by its [acid-base properties](@entry_id:190019). In the context of proteins, we are primarily concerned with the seven of the twenty standard [proteinogenic amino acids](@entry_id:196937) that possess side chains capable of exchanging protons with the aqueous solvent at physiologically relevant $\mathrm{pH}$ values.

#### Acid-Base Chemistry of Side Chains

According to the **Brønsted-Lowry theory**, an **acid** is a proton ($\mathrm{H}^+$) donor and a **base** is a [proton acceptor](@entry_id:150141). The ionizable [side chains](@entry_id:182203) can be classified based on the nature of their acidic form.

-   **Acidic Side Chains**: Aspartic acid (Asp) and glutamic acid (Glu) contain carboxylic acid groups. Their deprotonation reactions are of the form $\mathrm{HA} \rightleftharpoons \mathrm{A}^- + \mathrm{H}^+$, where $\mathrm{HA}$ is the neutral carboxylic acid and $\mathrm{A}^-$ is the charged carboxylate. Cysteine (Cys) with its thiol group and Tyrosine (Tyr) with its phenol group also follow this pattern.

-   **Basic Side Chains**: Lysine (Lys), with its primary amine, and Arginine (Arg), with its guanidinium group, are basic. Their conjugate acids are positively charged, and the dissociation is of the form $\mathrm{BH}^+ \rightleftharpoons \mathrm{B} + \mathrm{H}^+$. Histidine (His), with its imidazole ring, is unique in that its conjugate acid is charged ($\mathrm{BH}^+$) and its neutral form ($\mathrm{B}$) can act as both a [hydrogen bond donor and acceptor](@entry_id:193635).

The tendency of an acid to donate a proton is quantified by its **[acid dissociation constant](@entry_id:138231)**, $K_a$. For a generic acid $\mathrm{HA}$, the equilibrium is $\mathrm{HA} \rightleftharpoons \mathrm{A}^- + \mathrm{H}^+$, and the $K_a$ is defined in terms of the equilibrium activities ($a$) of the species involved:

$K_a = \frac{a(\mathrm{A}^-) a(\mathrm{H}^+)}{a(\mathrm{HA})}$

In dilute solutions, activities are often approximated by molar concentrations. For convenience, [acidity](@entry_id:137608) is typically expressed on a logarithmic scale as the **$\mathrm{p}K_a$ value**, defined as:

$\mathrm{p}K_a \equiv -\log_{10}(K_a)$

A stronger acid has a larger $K_a$ and thus a smaller $\mathrm{p}K_a$. The relationship between the $\mathrm{pH}$ of a solution, the $\mathrm{p}K_a$ of the acid, and the ratio of the [conjugate base](@entry_id:144252) to acid concentrations is given by the **Henderson-Hasselbalch equation**:

$\mathrm{pH} = \mathrm{p}K_a + \log_{10}\left(\frac{[\mathrm{A}^-]}{[\mathrm{HA}]}\right)$

This equation is central to predicting the [protonation state](@entry_id:191324) of a side chain at a given $\mathrm{pH}$. When $\mathrm{pH} = \mathrm{p}K_a$, the concentrations of the protonated and deprotonated forms are equal. When $\mathrm{pH} > \mathrm{p}K_a$, the deprotonated (base) form dominates, and when $\mathrm{pH}  \mathrm{p}K_a$, the protonated (acid) form dominates.

We can determine the intrinsic $\mathrm{p}K_a$ values for the [side chains](@entry_id:182203) by measuring the fractional protonation of small-molecule analogs in aqueous solution. For instance, if at $\mathrm{pH} = 7.0$ the deprotonated fraction $f_{\mathrm{A}^-}$ of an aspartate-like analog is measured to be $0.9992$, we can calculate its $\mathrm{p}K_a$. The ratio $[\mathrm{A}^-]/[\mathrm{HA}]$ is $f_{\mathrm{A}^-}/(1-f_{\mathrm{A}^-}) = 0.9992/0.0008 = 1249$. Rearranging the Henderson-Hasselbalch equation gives $\mathrm{p}K_a = \mathrm{pH} - \log_{10}([\mathrm{A}^-]/[\mathrm{HA}]) = 7.0 - \log_{10}(1249) \approx 3.9$. Applying this method to all seven ionizable side chains yields a set of canonical aqueous $\mathrm{p}K_a$ values that serve as our reference point [@problem_id:2572377]:

-   Aspartic Acid (Asp): $\mathrm{p}K_a \approx 3.9$
-   Glutamic Acid (Glu): $\mathrm{p}K_a \approx 4.2$
-   Histidine (His): $\mathrm{p}K_a \approx 6.0$
-   Cysteine (Cys): $\mathrm{p}K_a \approx 8.3$
-   Tyrosine (Tyr): $\mathrm{p}K_a \approx 10.1$
-   Lysine (Lys): $\mathrm{p}K_a \approx 10.5$
-   Arginine (Arg): $\mathrm{p}K_a \approx 12.5$

These values indicate that at physiological $\mathrm{pH}$ ($\approx 7.4$), Asp and Glu are almost entirely deprotonated (negatively charged), Lys and Arg are almost entirely protonated (positively charged), and His exists as a mixture of both states, making it uniquely suited to act as a [proton donor](@entry_id:149359) or acceptor during enzymatic reactions.

#### The Thermodynamic Basis of $\mathrm{p}K_a$

The $\mathrm{p}K_a$ is not merely an empirical parameter; it is a direct measure of the **standard Gibbs free energy change** ($\Delta G^\circ$) for the deprotonation reaction. The fundamental relationship between the [equilibrium constant](@entry_id:141040) $K$ of a reaction and its standard Gibbs free energy change is:

$\Delta G^\circ = -RT \ln K$

where $R$ is the [universal gas constant](@entry_id:136843) and $T$ is the [absolute temperature](@entry_id:144687). For acid [dissociation](@entry_id:144265), $K = K_a$. By substituting $K_a = 10^{-\mathrm{p}K_a}$ and using the identity $\ln(x) = \ln(10) \cdot \log_{10}(x) \approx 2.303 \log_{10}(x)$, we arrive at a direct link between the energetic cost of deprotonation and the $\mathrm{p}K_a$:

$\Delta G^\circ_{\mathrm{diss}} = -RT \ln(10^{-\mathrm{p}K_a}) = RT \ln(10) \cdot \mathrm{p}K_a \approx 2.303 RT \cdot \mathrm{p}K_a$

This equation reveals that the $\mathrm{p}K_a$ is a linear function of the standard free energy required to remove a proton from the acid and transfer it to the bulk solvent. A higher $\mathrm{p}K_a$ signifies a more positive $\Delta G^\circ_{\mathrm{diss}}$, meaning the deprotonation is less favorable. Any factor that stabilizes the conjugate acid relative to the [conjugate base](@entry_id:144252) will increase $\Delta G^\circ_{\mathrm{diss}}$ and thus raise the $\mathrm{p}K_a$ [@problem_id:2572331].

#### Structural Origins of Intrinsic $\mathrm{p}K_a$ Values

The significant variation in intrinsic $\mathrm{p}K_a$ values among the side chains arises from differences in their electronic structure, which affect the [relative stability](@entry_id:262615) of the conjugate acid and base forms. Two primary effects from [physical organic chemistry](@entry_id:184637)—**resonance** and **induction**—provide a powerful explanatory framework.

A striking example is the ~2-unit difference in $\mathrm{p}K_a$ between the [side chains](@entry_id:182203) of lysine ($\mathrm{p}K_a \approx 10.5$) and arginine ($\mathrm{p}K_a \approx 12.5$). Both [side chains](@entry_id:182203) are positively charged when protonated. However, the positive charge on the lysylammonium ion ($\mathrm{R{-}NH_3^+}$) is localized on a single nitrogen atom. In contrast, the conjugate acid of arginine, the guanidinium ion, is exceptionally stable due to **[resonance delocalization](@entry_id:197579)**. The positive charge is distributed over three nitrogen atoms via three major resonance contributors.

This delocalization significantly stabilizes the guanidinium ion (the conjugate acid) relative to the neutral guanidine base. According to our thermodynamic relationship, stabilizing the acid form makes it a weaker acid (less willing to give up its proton), thus increasing its $\mathrm{p}K_a$. The energetic benefit of this [resonance stabilization](@entry_id:147454) is substantial. The $\Delta \mathrm{p}K_a$ of $2.0$ units corresponds to a difference in deprotonation free energy of $\Delta\Delta G^\circ \approx 2.303 RT \Delta \mathrm{p}K_a \approx 2.7 \, \mathrm{kcal/mol}$ at $298 \, \mathrm{K}$, an energy difference readily attributable to strong resonance effects [@problem_id:2572332].

### Perturbations of $\mathrm{p}K_a$ in Protein Environments

The reference $\mathrm{p}K_a$ values determined in water are seldom accurate for residues buried within a protein. The protein interior is a complex, heterogeneous environment that can drastically alter the energetics of deprotonation. These perturbations are key to protein function, tuning the reactivity of catalytic residues and modulating structural stability.

#### The Role of the Dielectric Environment: Desolvation Penalty

One of the most significant differences between bulk water and the protein interior is the **dielectric constant** ($\varepsilon$), a measure of a medium's ability to screen electric fields. Water is a highly polar solvent with a high [dielectric constant](@entry_id:146714) ($\varepsilon_w \approx 80$), whereas the hydrophobic interior of a protein is a nonpolar environment with a low [dielectric constant](@entry_id:146714) ($\varepsilon_p \approx 2-4$).

Moving an electric charge from a high-dielectric medium to a low-dielectric one is energetically unfavorable because the screening of the charge's electric field is much less effective. This energetic cost is known as the **desolvation penalty**. We can estimate its magnitude using the **Born model**, which treats the ion as a charged sphere of radius $a$ and charge $q$. The standard Gibbs free energy of transferring the ion from water to the protein interior is:

$\Delta G^\circ_{\mathrm{transfer}} = \frac{q^2}{8\pi\epsilon_0 a} \left(\frac{1}{\varepsilon_p} - \frac{1}{\varepsilon_w}\right)$

where $\epsilon_0$ is the [vacuum permittivity](@entry_id:204253). Since $\varepsilon_p \ll \varepsilon_w$, this transfer energy is strongly positive, confirming the penalty.

This desolvation penalty has predictable and opposing effects on the $\mathrm{p}K_a$ values of acidic and basic residues [@problem_id:2572385] [@problem_id:2572355]:

1.  **Acidic Residues (e.g., Asp, Glu)**: The deprotonation reaction is $\mathrm{HA} \rightleftharpoons \mathrm{A}^- + \mathrm{H}^+$. The [conjugate base](@entry_id:144252) ($\mathrm{A}^-$) is charged, while the acid ($\mathrm{HA}$) is neutral. Burying this side chain in a low-dielectric environment preferentially destabilizes the charged $\mathrm{A}^-$ state. This makes deprotonation less favorable, increasing $\Delta G^\circ_{\mathrm{diss}}$ and therefore **increasing the $\mathrm{p}K_a$**.

2.  **Basic Residues (e.g., Lys, Arg)**: The deprotonation reaction is $\mathrm{BH}^+ \rightleftharpoons \mathrm{B} + \mathrm{H}^+$. Here, the acid ($\mathrm{BH}^+$) is charged and the base ($\mathrm{B}$) is neutral. Burial in the protein core destabilizes the charged $\mathrm{BH}^+$ state. This makes the acid more "eager" to lose its proton to become neutral, making deprotonation more favorable. This decreases $\Delta G^\circ_{\mathrm{diss}}$ and therefore **decreases the $\mathrm{p}K_a$**.

The magnitude of these shifts can be dramatic. For a typical carboxylate group modeled as a sphere of radius $0.4 \, \mathrm{nm}$, moving from water ($\varepsilon_w = 78.5$) to a protein cavity ($\varepsilon_p = 4.0$) can increase its $\mathrm{p}K_a$ by over 7 units. This means a buried aspartate, which is a strong acid in water, can remain protonated even at neutral $\mathrm{pH}$.

#### Specific Interactions: Hydrogen Bonds and Salt Bridges

While the continuum dielectric model provides a useful qualitative picture, $\mathrm{p}K_a$ shifts are also heavily influenced by specific, [short-range interactions](@entry_id:145678), most notably **hydrogen bonds** and **[salt bridges](@entry_id:173473)**. We can analyze their effects using a simple thermodynamic argument: any interaction that preferentially stabilizes the [conjugate base](@entry_id:144252) will make the acid stronger (lower $\mathrm{p}K_a$), while any interaction that preferentially stabilizes the conjugate acid will make it weaker (higher $\mathrm{p}K_a$).

Consider an aspartate side chain in a protein microenvironment. We can evaluate the effect of a nearby functional group by considering its state-dependent stabilization energy [@problem_id:2572317]:

-   **H-bond Donor to the Carboxylate**: If a neutral [hydrogen bond donor](@entry_id:141108) (like a backbone amide $\mathrm{N-H}$) is positioned to donate a hydrogen bond to the deprotonated carboxylate ($\mathrm{Asp}^-$) but not the protonated form ($\mathrm{AspH}$), it selectively stabilizes the [conjugate base](@entry_id:144252). This stabilization makes deprotonation more favorable, shifting the equilibrium $\mathrm{AspH} \rightleftharpoons \mathrm{Asp}^- + \mathrm{H}^+$ to the right. The result is a **decrease in the $\mathrm{p}K_a$**. If the donor group is positively charged (e.g., a Lys or Arg side chain forming a [salt bridge](@entry_id:147432)), the electrostatic attraction provides even greater stabilization, leading to a larger decrease in the $\mathrm{p}K_a$ [@problem_id:2572317].

-   **H-bond Acceptor from the Carboxylic Acid**: If a [hydrogen bond acceptor](@entry_id:139503) (like a backbone carbonyl oxygen) is positioned to accept a [hydrogen bond](@entry_id:136659) from the protonated carboxylic acid ($\mathrm{AspH}$) but not the deprotonated form, it selectively stabilizes the conjugate acid. This makes deprotonation less favorable, shifting the equilibrium to the left and causing an **increase in the $\mathrm{p}K_a$**.

These specific interactions can modulate $\mathrm{p}K_a$ values by several units and are fundamental to the fine-tuning of active sites and binding pockets in proteins.

### Coupled Equilibria and Complex Titration Behavior

In a real protein, ionizable residues rarely titrate in isolation. Their deprotonation is often coupled to the [ionization](@entry_id:136315) of other nearby sites, to conformational changes, or to [ligand binding](@entry_id:147077). These couplings lead to complex titration behavior that cannot be described by a single, constant $\mathrm{p}K_a$.

#### Macroscopic vs. Microscopic $\mathrm{p}K_a$s

When a molecule has two or more titratable sites, a bulk titration experiment measures **macroscopic dissociation constants** ($K_1, K_2, \dots$), which describe the sequential loss of protons from the molecule as a whole. However, these [macroscopic observables](@entry_id:751601) emerge from a more complex set of underlying **microscopic equilibria**.

Consider a peptide with two acidic sites, $A$ and $B$. There are four possible protonation **microstates**: $A\mathrm{H}B\mathrm{H}$ (fully protonated), $A^-B\mathrm{H}$ (A deprotonated), $A\mathrm{H}B^-$ (B deprotonated), and $A^-B^-$ (fully deprotonated). There are four corresponding **microscopic [dissociation](@entry_id:144265) constants** that describe the proton loss from a specific site, conditional on the state of the other site: $k_{A}^{B\mathrm{H}}$, $k_{B}^{A\mathrm{H}}$, $k_{A}^{B^-}$, and $k_{B}^{A^-}$ [@problem_id:2572361].

The macroscopic and microscopic constants are related. The first macroscopic constant, $K_1$, which governs the loss of the first proton, is the sum of the constants for the two parallel microscopic pathways out of the $A\mathrm{H}B\mathrm{H}$ state:

$K_1 = k_{A}^{B\mathrm{H}} + k_{B}^{A\mathrm{H}}$

The product of the macroscopic constants, $K_1K_2$, represents the overall equilibrium for losing both protons. Due to the [path-independence](@entry_id:163750) of [thermodynamic state functions](@entry_id:191389), this product must equal the product of microscopic constants along any pathway from $A\mathrm{H}B\mathrm{H}$ to $A^-B^-$:

$K_1 K_2 = k_{A}^{B\mathrm{H}} \cdot k_{B}^{A^-} = k_{B}^{A\mathrm{H}} \cdot k_{A}^{B^-}$

It is crucial to recognize that the values measured in a titration, $\mathrm{p}K_a^{(1)}$ and $\mathrm{p}K_a^{(2)}$, are macroscopic properties and are generally not equal to any of the four microscopic $\mathrm{p}K_a$ values.

#### Quantifying Electrostatic Interactions: Coupling Free Energy

The reason microscopic constants like $k_{A}^{B\mathrm{H}}$ and $k_{A}^{B^-}$ differ is the [electrostatic interaction](@entry_id:198833) between sites $A$ and $B$. For example, if both sites are carboxylates, the presence of a negative charge at site $B$ (in the $A\mathrm{H}B^-$ state) will electrostatically disfavor the formation of another negative charge at site $A$. This makes deprotonation of $A$ harder when $B$ is already deprotonated, so $k_{A}^{B^-}  k_{A}^{B\mathrm{H}}$.

This interaction can be quantified by the **coupling free energy**, $\Delta\Delta G_\mathrm{coupling}$, defined as the deviation from additivity in the free energies of deprotonation. A positive coupling energy signifies a repulsive interaction (deprotonating one site makes deprotonation of the other less favorable), while a negative coupling energy signifies an attractive interaction. This energy can be calculated from the various equilibrium constants [@problem_id:2572325]. For example, one expression is:

$\Delta\Delta G_\mathrm{coupling} = -RT \ln\left(\frac{k_{A}^{B^-}}{k_{A}^{B\mathrm{H}}}\right)$

This coupling is the energetic origin of the cooperative or anti-cooperative titration behavior observed in many proteins and is a direct measure of the [electrostatic interaction](@entry_id:198833) energy between the two sites, modulated by the protein environment.

#### Breakdown of Simple Models

The simple Henderson-Hasselbalch model, which assumes a single, independent titratable site with a constant $\mathrm{p}K_a$, systematically fails in many realistic biochemical contexts. Recognizing these scenarios is key to accurately interpreting protein behavior [@problem_id:2572348]. Common sources of failure include:

1.  **Strong Electrostatic Perturbations**: As discussed, a charge buried in a low-dielectric protein core or located near a charged membrane surface experiences profound electrostatic forces that are not captured by a simple aqueous $\mathrm{p}K_a$. The local $\mathrm{pH}$ itself can differ significantly from the bulk $\mathrm{pH}$.

2.  **Coupling to Conformational Change**: If a residue's [protonation state](@entry_id:191324) is linked to a protein's conformational equilibrium (e.g., buried in the folded state but exposed in an unfolded state), the observed titration curve will be a composite of both the ionization and conformational equilibria. The apparent $\mathrm{p}K_a$ will no longer be a simple constant.

3.  **Coupling to Ligand Binding**: The binding of a ligand, such as a metal ion, can be coupled to a residue's protonation. For example, if a histidine side chain can either bind a proton or coordinate a metal ion, the two processes are in competition. The apparent $\mathrm{p}K_a$ of the histidine will become dependent on the concentration of the metal ion.

4.  **Proton Delocalization**: In some cases, such as a proposed **[low-barrier hydrogen bond](@entry_id:176721) (LBHB)** between two residues (e.g., an Asp-His dyad), the proton may be quantum mechanically shared between the two sites. In this scenario, it is no longer meaningful to speak of the proton "belonging" to one residue or the other. The dyad titrates as a single unit, often with a highly anomalous, broad titration curve that cannot be fit by a [standard model](@entry_id:137424).

### A Rigorous Statistical Mechanics Perspective

To formalize these complex, coupled phenomena, we turn to statistical mechanics. Constant-$\mathrm{pH}$ simulation methods, such as **constant-$\mathrm{pH}$ Molecular Dynamics (MD)**, provide a powerful theoretical and computational framework for studying protonation equilibria in [biomolecules](@entry_id:176390).

These methods are properly formulated within the **[grand canonical ensemble](@entry_id:141562)**, a [statistical ensemble](@entry_id:145292) where the system can exchange both energy and particles with a large reservoir at constant temperature $T$ and constant chemical potential $\mu$. For protonation, the "particle" is the proton, and the reservoir is the bulk solvent, which fixes the **proton chemical potential**, $\mu_{\mathrm{H}^+}$.

The proton chemical potential of the reservoir is set by the macroscopic $\mathrm{pH}$ of the solution via the [fundamental thermodynamic relation](@entry_id:144320):

$\mu_{\mathrm{H}^+} = \mu_{\mathrm{H}^+}^{\circ} + RT \ln(a_{\mathrm{H}^+}) = \mu_{\mathrm{H}^+}^{\circ} - RT \ln(10) \cdot \mathrm{pH}$

where $\mu_{\mathrm{H}^+}^{\circ}$ is the standard chemical potential and $a_{\mathrm{H}^+}$ is the proton activity. This equation shows that $\mathrm{pH}$ is the experimental control variable that determines the thermodynamic driving force for proton exchange.

In a constant-$\mathrm{pH}$ simulation, a [microstate](@entry_id:156003) is defined by both the atomic coordinates ($\mathbf{R}$) and the discrete [protonation state](@entry_id:191324) of all $N$ titratable sites, represented by a vector $\mathbf{n}$. The probability of observing a particular microstate is proportional to its grand canonical [statistical weight](@entry_id:186394), which includes a term for the potential energy of the system, $U(\mathbf{R}, \mathbf{n})$, and a term for the chemical work of acquiring protons from the reservoir:

$P(\mathbf{R}, \mathbf{n}) \propto \exp\left[-\frac{1}{k_B T} \left( U(\mathbf{R}, \mathbf{n}) - \mu_{\mathrm{H}^+} N_{\mathrm{H}}(\mathbf{n}) \right) \right]$

where $N_{\mathrm{H}}(\mathbf{n})$ is the number of protons bound to the protein in state $\mathbf{n}$, and $k_B$ is the Boltzmann constant. By sampling from this distribution, these simulations can naturally capture all the complex phenomena discussed—environmental perturbations, electrostatic coupling, and links to conformational changes—providing a complete and rigorous picture of protein ionization [@problem_id:2572319]. This statistical mechanical view frames protonation not as a simple switch but as a dynamic equilibrium, where the probability of each [protonation state](@entry_id:191324) is a continuous function of $\mathrm{pH}$ and is exquisitely sensitive to the protein's conformation and environment.