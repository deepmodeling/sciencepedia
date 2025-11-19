## Introduction
The carbon-carbon double bond, the defining feature of [alkenes](@entry_id:183502), is a region of high electron density, making it an excellent nucleophile. This inherent reactivity drives one of the most fundamental reactions in organic chemistry: the [electrophilic addition](@entry_id:191707). In this reaction, the electron-rich alkene donates its π electrons to an electron-deficient species, or electrophile, initiating a transformation that converts the double bond into two new single bonds. While seemingly straightforward, these additions follow a precise set of rules that dictate which products are formed and in what orientation. This article addresses the core mechanistic questions of *how* and *why* these reactions exhibit such high selectivity, moving from empirical rules to a deep understanding of the underlying electronic principles.

Throughout the following chapters, you will embark on a detailed exploration of this reaction class.
- In **Principles and Mechanisms**, we will dissect the step-by-step pathway of [electrophilic addition](@entry_id:191707), introducing the pivotal role of the [carbocation intermediate](@entry_id:204002), the factors governing its stability, and the energetic landscape that controls the reaction's speed and outcome.
- **Applications and Interdisciplinary Connections** will demonstrate how these fundamental principles are applied to solve real-world problems in [chemical synthesis](@entry_id:266967), explain complex biological processes, and drive large-scale industrial manufacturing.
- Finally, **Hands-On Practices** will provide an opportunity to apply your knowledge to solve challenging problems, reinforcing your ability to predict reaction products and rationalize mechanistic pathways.

## Principles and Mechanisms

The characteristic reactivity of alkenes stems from the unique nature of the carbon-carbon double bond, which consists of a strong sigma ($\sigma$) bond and a weaker, more accessible pi ($\pi$) bond. The electrons in the $\pi$ bond are located above and below the plane of the atoms and are less tightly held than the $\sigma$ electrons. This region of high electron density makes the alkene a **nucleophile**—an electron-rich species capable of donating an electron pair to form a new covalent bond. Consequently, the defining reaction of [alkenes](@entry_id:183502) is their interaction with **electrophiles**, or electron-deficient species. This chapter will dissect the fundamental principles and mechanisms governing this class of reactions, known as **electrophilic additions**.

### The Electronic Basis of Reactivity: A Frontier Molecular Orbital Perspective

To understand why and how an [electrophile](@entry_id:181327) adds to an alkene, we can turn to **Frontier Molecular Orbital (FMO) theory**. This powerful model posits that the most significant interactions between two reacting molecules occur between the **Highest Occupied Molecular Orbital (HOMO)** of the nucleophile and the **Lowest Unoccupied Molecular Orbital (LUMO)** of the electrophile. The HOMO represents the most available, highest-energy electrons the nucleophile can donate, while the LUMO represents the most accessible, lowest-energy empty orbital the [electrophile](@entry_id:181327) can use to accept those electrons.

In an [electrophilic addition](@entry_id:191707), the alkene serves as the nucleophile. Its most reactive electrons reside in the $\pi$ bonding orbital, which is therefore the **HOMO** of the alkene. Let us consider the classic reaction between propene and hydrogen bromide ($HBr$). Here, $HBr$ is the [electrophile](@entry_id:181327). The crucial orbital for accepting electrons is not a vacant atomic orbital but the **$\sigma^*$ ([sigma-star](@entry_id:200526)) [antibonding orbital](@entry_id:261662)** of the $H-Br$ bond. This $\sigma^*$ orbital is the **LUMO** of the [electrophile](@entry_id:181327).

The reaction is initiated by the overlap of the alkene's $\pi$ HOMO with the $H-Br$ $\sigma^*$ LUMO [@problem_id:2168828]. When the electron density from the $\pi$ bond flows into the $\sigma^*$ orbital, it populates an antibonding orbital, which has the immediate effect of weakening and ultimately breaking the $H-Br$ bond. Simultaneously, a new $\sigma$ bond begins to form between one of the carbon atoms of the original double bond and the hydrogen atom. This FMO analysis provides a rigorous quantum mechanical basis for the intuitive notion of the "electron-rich double bond attacking the electron-poor proton."

### The Two-Step Mechanism and the Carbocation Intermediate

Electrophilic additions of protic acids like $HBr$ to simple [alkenes](@entry_id:183502) do not occur in a single, concerted step. Instead, they proceed through a two-step mechanism involving a high-energy intermediate.

**Step 1: Protonation and Formation of a Carbocation.** In the first and slowest step of the mechanism, the alkene's $\pi$ electrons attack the [electrophile](@entry_id:181327)—in this case, the proton from the acid. This forms a new carbon-hydrogen bond and leaves the other carbon atom of the original double bond with only three bonds and a formal positive charge. This species is a **carbocation**. Because this step involves the formation of a high-energy, unstable intermediate from stable reactants, it has a high activation energy and is the **rate-determining step** of the overall reaction [@problem_id:2168803].

**Step 2: Nucleophilic Capture.** In the second, rapid step, the [carbocation](@entry_id:199575), being a powerful electrophile itself, is attacked by a nucleophile present in the reaction mixture. In the case of $HBr$ addition, the nucleophile is the bromide ion ($Br^−$) generated in the first step. The bromide ion donates a pair of electrons to the positively charged carbon, forming a new carbon-bromine bond and yielding the final, neutral addition product.

The structure of the [carbocation intermediate](@entry_id:204002) is critical to understanding the reaction's outcome. The positively charged carbon atom is bonded to three other atoms and has no lone pairs. To maximize the distance between the bonding electron pairs, the carbon atom adopts an **$sp^2$ [hybridization](@entry_id:145080)**, resulting in a **trigonal planar geometry** around the cationic center. The three substituents lie in a single plane, with bond angles of approximately $120^\circ$. Perpendicular to this plane is an empty, unhybridized $p$-orbital, which carries the positive charge and is the site of subsequent [nucleophilic attack](@entry_id:151896) [@problem_id:2168783]. The planar nature of this intermediate has important stereochemical consequences, as the nucleophile can approach the empty $p$-orbital from either face with equal probability (unless one face is sterically hindered).

### Regioselectivity: Carbocation Stability and Markovnikov's Rule

When an unsymmetrical alkene, such as 1-butene, reacts with an electrophile like $H^+$, the initial protonation can, in principle, occur at either of the two double-bonded carbons. This leads to the question of **regioselectivity**: which constitutional isomer is the major product?

Consider the protonation of 1-butene ($CH_2=CHCH_2CH_3$):
1.  **Protonation at C1:** If the proton adds to the terminal carbon (C1), the positive charge resides on C2. This carbon is bonded to two other carbon atoms, making it a **secondary carbocation**.
2.  **Protonation at C2:** If the proton adds to the internal carbon (C2), the positive charge resides on C1. This carbon is bonded to only one other carbon atom, making it a **primary [carbocation](@entry_id:199575)**.

The outcome of the reaction is dictated by the relative stabilities of these two possible intermediates. The established order of [carbocation stability](@entry_id:149581) is:

**Tertiary ($3^\circ$) > Secondary ($2^\circ$) > Primary ($1^\circ$) > Methyl**

This stability trend is primarily explained by two electronic effects:

*   **Hyperconjugation:** This is the dominant stabilizing effect. It involves the [delocalization](@entry_id:183327) of electron density from adjacent, filled $C-H$ or $C-C$ $\sigma$ bonds into the empty $p$-orbital of the [carbocation](@entry_id:199575) center. The more alkyl groups attached to the cationic carbon, the more adjacent $\sigma$ bonds are available for this stabilizing overlap. For example, in the reaction of 2-methyl-1-butene, protonation can lead to a tertiary [carbocation](@entry_id:199575) (with nine C-H bonds available for hyperconjugation on adjacent carbons) or a primary [carbocation](@entry_id:199575) (with only one adjacent C-H bond). The extensive hyperconjugation makes the tertiary [carbocation](@entry_id:199575) vastly more stable [@problem_id:2168824].
*   **Inductive Effect:** Alkyl groups are weakly electron-donating through the $\sigma$-bond framework. They push electron density toward the positive charge, helping to disperse it and stabilize the cation.

Because the secondary carbocation is more stable than the primary carbocation, the reaction pathway that forms it is energetically favored. Thus, for 1-butene, protonation occurs at C1 to form the secondary [carbocation](@entry_id:199575) at C2, which is then captured by the nucleophile [@problem_id:2168761]. This observation is summarized by the empirical guideline known as **Markovnikov's Rule**: *When a protic acid (H-X) adds to an unsymmetrical alkene, the hydrogen atom adds to the carbon of the double bond that bears the greater number of hydrogen atoms.* The halide (X) adds to the more substituted carbon.

It is crucial to remember that Markovnikov's rule is a predictive shortcut; the fundamental principle governing regioselectivity is the formation of the **most stable [carbocation intermediate](@entry_id:204002)** [@problem_id:2168814].

### Energetics, Kinetics, and the Hammond Postulate

The connection between intermediate stability and reaction rate is formally explained by **Hammond's Postulate**. This postulate states that the structure and energy of the transition state for a given reaction step can be approximated by the structure and energy of the species (reactant, intermediate, or product) to which it is closest in energy.

In [electrophilic addition](@entry_id:191707), the first step—the formation of the carbocation—is an endergonic process (it has a positive Gibbs free energy change, $\Delta G > 0$). According to Hammond's Postulate, the transition state for this step will therefore resemble the product of the step, which is the [carbocation intermediate](@entry_id:204002) [@problem_id:2168784] [@problem_id:2168803]. This "late" transition state has significant carbocationic character.

This has a profound consequence: any factor that stabilizes the [carbocation intermediate](@entry_id:204002) will also stabilize the transition state leading to it. A more stable transition state means a lower Gibbs [free energy of activation](@entry_id:182945) ($\Delta G^\ddagger$) and, therefore, a faster reaction rate. This is why the reaction of 2-methylpropene (which forms a tertiary carbocation) is significantly faster than the reaction of propene (which forms a secondary [carbocation](@entry_id:199575)) [@problem_id:2168784].

The energetic difference between competing pathways can have a dramatic effect on the [product distribution](@entry_id:269160). The relationship between the rate constants ($k$) of two competing pathways (e.g., pathway A leading to a primary [carbocation](@entry_id:199575) and pathway B leading to a secondary [carbocation](@entry_id:199575)) and their respective activation energies ($\Delta G_A^\ddagger$ and $\Delta G_B^\ddagger$) is given by the equation:

$$ \frac{k_B}{k_A} = \exp\left(-\frac{\Delta G_B^\ddagger - \Delta G_A^\ddagger}{RT}\right) $$

where $R$ is the ideal gas constant and $T$ is the temperature in [kelvin](@entry_id:136999). For the addition of HBr to propene, the activation energy for forming the secondary [carbocation](@entry_id:199575) is lower than that for the primary carbocation by approximately $15 \, \text{kJ/mol}$. At room temperature ($298.15 \, K$), this energy difference translates to a [rate ratio](@entry_id:164491):

$$ \frac{k_{\text{secondary}}}{k_{\text{primary}}} = \exp\left(\frac{15000 \, \text{J/mol}}{(8.314 \, \text{J mol}^{-1}\text{K}^{-1})(298.15 \, \text{K})}\right) \approx 425 $$

This calculation demonstrates that the reaction leading to the secondary carbocation is over 400 times faster than the one leading to the primary [carbocation](@entry_id:199575) [@problem_id:2168776]. This is why the Markovnikov product is formed almost exclusively.

### A Mechanistic Complication: Carbocation Rearrangements

The description of a stepwise mechanism featuring a [carbocation intermediate](@entry_id:204002) leads to a powerful prediction: if a more stable [carbocation](@entry_id:199575) can be formed from the initially generated one, a **rearrangement** will likely occur. Carbocations are high-energy species that will rapidly rearrange via the migration of a neighboring group to the cationic center if doing so results in a more stable cation.

The most common types of rearrangements are **1,2-shifts**, where an atom or group on an adjacent carbon migrates with its bonding electron pair to the positively charged carbon.

*   **1,2-Hydride Shift:** A hydrogen atom moves.
*   **1,2-Alkyl Shift (e.g., Methyl Shift):** An alkyl group moves.

A classic example is the reaction of **3-methyl-1-butene** with $HBr$ [@problem_id:2168779]. Following Markovnikov's principle, initial protonation at C1 generates a secondary [carbocation](@entry_id:199575) at C2. However, the adjacent carbon (C3) is tertiary. A rapid **1,[2-hydride shift](@entry_id:198648)** from C3 to C2 occurs, moving the positive charge to C3 and forming a much more stable **tertiary [carbocation](@entry_id:199575)**. The bromide ion then attacks this rearranged tertiary carbocation. The major product is 2-bromo-2-methylbutane, not the expected 2-bromo-3-methylbutane. The possibility of rearrangement is a hallmark of reactions proceeding through [carbocation](@entry_id:199575) intermediates and must always be considered when predicting products.

### Beyond the Carbocation: Bridged Intermediates

While the [carbocation](@entry_id:199575) model successfully explains a vast range of electrophilic additions, it is not universal. The nature of the intermediate can depend heavily on the electrophile. A key alternative is the formation of a **bridged ion**.

Consider the addition of bromine ($Br_2$) to an alkene. Instead of forming an open-chain [carbocation](@entry_id:199575), the reaction proceeds through a cyclic intermediate known as a **[bromonium ion](@entry_id:202803)**. In this three-membered ring, the bromine atom is simultaneously bonded to both carbons of the original double bond, and it bears the formal positive charge.

This [bridged intermediate](@entry_id:188645) differs from a classical [carbocation](@entry_id:199575) in several fundamental ways [@problem_id:2168760]:
*   **Structure and Stability:** In the [bromonium ion](@entry_id:202803), the positive charge is delocalized over three atoms (two carbons and bromine). Crucially, all non-hydrogen atoms can satisfy the octet rule, which makes the bridged ion significantly more stable than an analogous open carbocation with its electron-deficient carbon.
*   **Rearrangements:** Unlike [carbocations](@entry_id:185610), bridged bromonium ions are generally rigid and do not undergo 1,2-shifts.
*   **Stereochemistry:** Nucleophilic attack on a planar carbocation can occur from either face. In contrast, [nucleophilic attack](@entry_id:151896) on a [bromonium ion](@entry_id:202803) must occur from the side opposite the bulky bridging bromine atom in a stereospecific **[anti-addition](@entry_id:196470)** pathway.

The formation of bridged intermediates, such as bromonium ions (with $Br_2$) or mercurinium ions (in oxymercuration), represents an important mechanistic variation. Understanding when a classical [carbocation](@entry_id:199575) is formed versus when a bridged ion is preferred is key to accurately predicting the products and [stereochemistry](@entry_id:166094) of a wide array of [electrophilic addition](@entry_id:191707) reactions.