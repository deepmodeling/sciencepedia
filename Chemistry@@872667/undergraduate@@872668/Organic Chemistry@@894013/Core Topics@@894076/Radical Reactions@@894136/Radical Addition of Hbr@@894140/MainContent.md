## Introduction
The addition of [hydrogen halides](@entry_id:193573) to [alkenes](@entry_id:183502) is a foundational reaction in [organic chemistry](@entry_id:137733), typically governed by Markovnikov's rule, which dictates that the hydrogen atom adds to the carbon with more hydrogen substituents. However, this predictable outcome can be dramatically reversed under specific conditions, presenting both a fascinating mechanistic puzzle and a powerful synthetic tool. When hydrogen bromide (HBr) is added to an unsymmetrical alkene in the presence of peroxides, the addition occurs with opposite regioselectivity, yielding the "anti-Markovnikov" product. This phenomenon, known as the [peroxide effect](@entry_id:183658), shifts the reaction from a standard ionic pathway to a free-[radical chain mechanism](@entry_id:180350). Understanding how to control and exploit this alternative pathway is essential for any chemist aiming to achieve precise regiochemical control in molecular synthesis.

This article provides a comprehensive exploration of the radical addition of HBr. The first chapter, **Principles and Mechanisms**, will dissect the free-[radical chain reaction](@entry_id:190806), examining the initiation, propagation, and termination steps, and explain the energetic basis for both the anti-Markovnikov regioselectivity and the reaction's unique specificity for HBr. Following this, the **Applications and Interdisciplinary Connections** chapter will demonstrate the reaction's versatility, from its role in multistep synthesis and polymer science to its use as a probe in [physical organic chemistry](@entry_id:184637). Finally, you will have the opportunity to apply your knowledge through a series of **Hands-On Practices**, reinforcing your understanding of this crucial synthetic method.

## Principles and Mechanisms

The addition of [hydrogen halides](@entry_id:193573) to alkenes is a cornerstone reaction in organic synthesis. As introduced previously, the [electrophilic addition](@entry_id:191707) of hydrogen bromide ($ \text{HBr} $) to an unsymmetrical alkene typically follows Markovnikov's rule, proceeding through the most stable [carbocation intermediate](@entry_id:204002). However, a fascinating and synthetically valuable reversal of this regioselectivity occurs under specific conditions, namely in the presence of peroxides or other radical initiators. This phenomenon, often called the **[peroxide effect](@entry_id:183658)** or the **Kharasch effect**, shifts the [reaction mechanism](@entry_id:140113) from an ionic pathway to a free-radical chain process, resulting in **anti-Markovnikov addition**. This chapter will elucidate the principles and detailed mechanism governing this alternative pathway.

### The Peroxide Effect: A Mechanistic Dichotomy

The directing influence of reaction conditions is starkly illustrated by the hydrobromination of an alkene like 3-methyl-1-pentene. When this alkene is treated with pure $ \text{HBr} $ in the absence of light and peroxides, the reaction proceeds via the familiar [electrophilic addition](@entry_id:191707) mechanism. Protonation of the terminal carbon (C1) generates a secondary carbocation at C2. This carbocation rapidly undergoes a 1,[2-hydride shift](@entry_id:198648) to form a more stable tertiary carbocation at C3, which is then trapped by the bromide ion. The major product is, therefore, 3-bromo-3-methylpentane, a rearranged Markovnikov product.

In stark contrast, when the same reaction is conducted in the presence of an organic peroxide ($ \text{ROOR} $), the major product is found to be 1-bromo-3-methylpentane [@problem_id:2193091]. Here, the bromine atom has added to the terminal carbon (C1) and the hydrogen atom to C2. This is the anti-Markovnikov product. The presence of the peroxide has completely inverted the regiochemical outcome of the addition. This switch from Markovnikov to anti-Markovnikov selectivity is the defining characteristic of the radical addition of $ \text{HBr} $. It is the peroxide's ability to initiate a free-[radical chain reaction](@entry_id:190806) that is responsible for this dramatic change in reactivity [@problem_id:2193090].

The general rule for this reaction can be stated as follows: **In the radical-initiated addition of HBr to an unsymmetrical alkene, the bromine atom adds to the $sp^2$ carbon that is bonded to the greater number of hydrogen atoms.** This regioselectivity is consistently observed across a wide range of alkene substrates, such as the addition to 4-methyl-1-pentene to yield 1-bromo-4-methylpentane [@problem_id:2193136] or the addition to 2-methylpropene to form 1-bromo-2-methylpropane [@problem_id:2193123]. To understand the origin of this rule, we must examine the stepwise mechanism of the reaction.

### The Free-Radical Chain Mechanism

The anti-Markovnikov addition of $ \text{HBr} $ is a classic example of a **free-[radical chain reaction](@entry_id:190806)**. Like other chain processes, it is characterized by three distinct phases: **initiation**, **propagation**, and **termination**.

#### Initiation

The role of the peroxide is to generate the initial radical species that start the chain. This phase consists of two steps.

1.  **Homolytic Cleavage of the Initiator:** Organic peroxides ($ \text{ROOR} $) are effective initiators because the oxygen-oxygen [single bond](@entry_id:188561) is exceptionally weak ([bond dissociation enthalpy](@entry_id:149221) typically 150-190 kJ/mol). Upon gentle heating or exposure to ultraviolet light, this bond undergoes **homolysis**—a symmetric cleavage where each atom retains one of the bonding electrons. For example, benzoyl peroxide thermally decomposes to form two benzoyloxy radicals [@problem_id:2193086].

    $$ \text{PhCO-O-O-COPh} \xrightarrow{\Delta} 2\, \text{PhCO-O}\cdot $$

2.  **Generation of the Bromine Radical:** The initial radical formed (e.g., an alkoxyl radical, $ \text{RO}\cdot $, from a dialkyl peroxide) is highly reactive. It rapidly abstracts a hydrogen atom from a molecule of hydrogen bromide to produce the crucial chain-carrying species: a **bromine radical** ($ \text{Br}\cdot $).

    $ \text{RO}\cdot + \text{HBr} \longrightarrow \text{ROH} + \text{Br}\cdot $

This second step is highly favorable and generates the electrophilic bromine radical that will directly engage with the alkene.

#### Propagation

The propagation phase consists of a repeating cycle of two steps that consumes reactants and forms the product while regenerating the chain-carrying radical. For the addition of $ \text{HBr} $ to an alkene like propene, the two propagation steps are as follows [@problem_id:2193115]:

1.  **Addition of the Bromine Radical to the Alkene:** The bromine radical adds to the $ \pi $ bond of the alkene. This is the regiochemistry-determining step. The addition can, in principle, occur at either carbon of the double bond. As we will discuss in detail later, the bromine radical adds to the less substituted carbon atom to generate the more stable alkyl radical intermediate.

    $ \text{Br}\cdot + \text{CH}_{3}\text{CH=CH}_{2} \longrightarrow \text{CH}_{3}\dot{\text{C}}\text{HCH}_{2}\text{Br} $
    (Forms a more stable secondary radical)

2.  **Hydrogen Atom Abstraction:** The alkyl radical formed in the first step then abstracts a hydrogen atom from another molecule of $ \text{HBr} $. This step forms the final alkyl bromide product and, critically, regenerates a bromine radical, which can then begin the cycle anew by reacting with another alkene molecule.

    $ \text{CH}_{3}\dot{\text{C}}\text{HCH}_{2}\text{Br} + \text{HBr} \longrightarrow \text{CH}_{3}\text{CH}_{2}\text{CH}_{2}\text{Br} + \text{Br}\cdot $

This [self-sustaining cycle](@entry_id:191058) is responsible for the high efficiency of chain reactions, where a single initiation event can lead to the formation of thousands of product molecules.

#### Termination

The [chain reaction](@entry_id:137566) is eventually stopped by **termination steps**, which are any reactions that consume radicals without generating new ones. These are relatively rare events compared to propagation steps but are inevitable, especially as the concentration of reactants decreases. Termination typically occurs through the combination of any two radicals present in the mixture.

*   Combination of two [bromine radicals](@entry_id:180220): $ \text{Br}\cdot + \text{Br}\cdot \longrightarrow \text{Br}_{2} $ [@problem_id:2193102]
*   Combination of an alkyl radical and a bromine radical: $ \text{R}\cdot + \text{Br}\cdot \longrightarrow \text{RBr} $
*   Combination of two alkyl radicals ([dimerization](@entry_id:271116)): $ \text{R}\cdot + \text{R}\cdot \longrightarrow \text{R-R} $

### The Energetic Basis of Regioselectivity and Substrate Specificity

The rules and mechanism outlined above can be rationalized by considering the stability of the intermediates and the thermodynamics of the individual reaction steps.

#### Why Anti-Markovnikov? The Stability of Radical Intermediates

The regioselectivity of the radical addition is determined in the first [propagation step](@entry_id:204825), where the bromine radical adds to the alkene. The reaction proceeds through the pathway that forms the **most stable radical intermediate**. The stability of alkyl radicals follows the same trend as that of [carbocations](@entry_id:185610):

**tertiary (3°) > secondary (2°) > primary (1°) > methyl**

This stability trend is primarily due to two factors:

1.  **Hyperconjugation:** The unpaired electron resides in a p-orbital. Adjacent C-H or C-C $ \sigma $-bonds can overlap with this p-orbital, delocalizing the unpaired electron and stabilizing the radical. The greater the number of adjacent alkyl groups, the more extensive the [hyperconjugation](@entry_id:263927) and the greater the stability.
2.  **Inductive Effects:** Alkyl groups are weakly electron-donating and can push electron density toward the electron-deficient [radical center](@entry_id:175001), providing a stabilizing effect.

Let's consider the addition of $ \text{Br}\cdot $ to 2-methyl-2-pentene. The radical can add to C2 or C3 of the double bond. Addition to C3 forms a tertiary radical at C2, which is stabilized by three alkyl groups. Addition to C2 would form a secondary radical at C3, stabilized by only two alkyl groups. The reaction therefore proceeds exclusively via the more stable tertiary radical intermediate, leading to the observed product [@problem_id:2193132]. The stability of the intermediate, dictated by hyperconjugation and inductive effects, is the fundamental reason for the anti-Markovnikov regioselectivity.

#### Why Only HBr? A Thermodynamic Perspective

A striking feature of this reaction is its specificity for hydrogen bromide. Radical-initiated additions of hydrogen chloride ($ \text{HCl} $) and hydrogen iodide ($ \text{HI} $) to [alkenes](@entry_id:183502) are not synthetically useful processes. The reason for this unique reactivity lies in the thermodynamics of the two propagation steps, which can be estimated using Bond Dissociation Enthalpies (BDEs) [@problem_id:2193129]. For a chain reaction to be efficient, both propagation steps must be exothermic or only very slightly endothermic.

Let's analyze the enthalpy changes ($ \Delta H^{\circ} $) for the two steps for each hydrogen halide ($ \text{HX} $):

**Step 1: $ \text{R-CH=CH}_{2} + \cdot\text{X} \rightarrow \text{R-}\dot{\text{C}}\text{H-CH}_{2}\text{X} $**
Here, a C=C $ \pi $-bond is broken and a C-X bond is formed. This step is exothermic for all three [halogens](@entry_id:145512) (Cl, Br, I) because the C-X bond formed is stronger than the $ \pi $-bond broken.

**Step 2: $ \text{R-}\dot{\text{C}}\text{H-CH}_{2}\text{X} + \text{H-X} \rightarrow \text{R-CH}_{2}\text{-CH}_{2}\text{X} + \cdot\text{X} $**
Here, an H-X bond is broken and a C-H bond is formed.

*   **For HCl:** The H-Cl bond (BDE $ \approx 431 $ kJ/mol) is very strong—stronger than the secondary C-H bond being formed (BDE $ \approx 413 $ kJ/mol). This makes the hydrogen abstraction step significantly **endothermic** ($ \Delta H^{\circ} \approx +18 $ kJ/mol). This high energy barrier effectively breaks the chain, rendering the overall process inefficient.

*   **For HBr:** The H-Br bond (BDE $ \approx 368 $ kJ/mol) is weaker than the C-H bond being formed. This makes the hydrogen abstraction step **exothermic** ($ \Delta H^{\circ} \approx -45 $ kJ/mol). Since both propagation steps are exothermic, the [chain reaction](@entry_id:137566) proceeds efficiently.

*   **For HI:** The H-I bond is very weak (BDE $ \approx 297 $ kJ/mol), making the second [propagation step](@entry_id:204825) highly exothermic. However, the C-I bond is also very weak. This weakness makes the *first* [propagation step](@entry_id:204825) (addition of $ \text{I}\cdot $ to the alkene) only marginally exothermic and, importantly, readily reversible. The iodine radical is not reactive enough to add irreversibly to the double bond.

Thus, only hydrogen bromide has the perfect thermodynamic balance where both propagation steps are exothermic and can proceed at a useful rate.

### Stereochemical Consequences

When the radical addition of HBr creates a new [stereocenter](@entry_id:194773), the stereochemical outcome is dictated by the geometry of the intermediate alkyl radical. The carbon atom bearing the unpaired electron is **$sp^2$-hybridized** and has a **[trigonal planar](@entry_id:147464)** geometry, with the unpaired electron occupying the p-orbital perpendicular to the plane.

Consider the addition of HBr to 2-methyl-1-butene, which forms 1-bromo-2-methylbutane, a chiral molecule. The key intermediate is a planar tertiary radical at C2. This intermediate is [achiral](@entry_id:194107). The subsequent hydrogen abstraction from HBr can occur from either face of this planar radical with equal probability. Attack from one face yields the (R)-[enantiomer](@entry_id:170403), while attack from the opposite face yields the (S)-enantiomer. Because both pathways are equally likely, the product is formed as a 50:50 mixture of enantiomers—a **racemic mixture**, which is optically inactive [@problem_id:2193111].

### Control and Inhibition of the Radical Pathway

The clear distinction between the ionic and radical pathways allows for precise control over the reaction outcome. Choosing to include or exclude a [radical initiator](@entry_id:204213) determines whether the Markovnikov or anti-Markovnikov product is formed.

Conversely, it is also possible to suppress an undesired [radical reaction](@entry_id:187711). This is achieved using **radical inhibitors** or **scavengers**. These are molecules that react with radical intermediates to form a very stable, unreactive radical that is incapable of propagating the chain. Phenolic compounds, such as Butylated hydroxytoluene (BHT), are common inhibitors. The phenolic hydrogen is easily abstracted, and the resulting phenoxy radical is highly resonance-stabilized.

If a [radical initiator](@entry_id:204213) (like AIBN) and a [radical inhibitor](@entry_id:190098) (like BHT) are both added to a reaction of an alkene and HBr, the inhibitor will quench the radical chain before it can begin. This effectively shuts down the anti-Markovnikov pathway. The reaction will then default to the slower, but now unopposed, [electrophilic addition](@entry_id:191707) mechanism, yielding the Markovnikov product [@problem_id:2193088].

A common and often unintentional [radical scavenger](@entry_id:196066) is molecular oxygen ($ \text{O}_{2} $). Oxygen is a [diradical](@entry_id:197302) in its ground state and reacts extremely rapidly with alkyl radicals ($ \text{R}\cdot $) to form a peroxy radical ($ \text{ROO}\cdot $).

$ \text{R}\cdot + \text{O}_{2} \longrightarrow \text{ROO}\cdot $

While this peroxy radical can abstract a hydrogen from HBr, it is substantially less reactive than the bromine radical towards addition to the alkene. By trapping the chain-carrying alkyl radical and converting it into a less reactive species, oxygen effectively diverts the reaction from the desired product-forming cycle, thus inhibiting the formation of the alkyl bromide [@problem_id:2193066]. For this reason, radical reactions are often performed under an [inert atmosphere](@entry_id:275393) (e.g., nitrogen or argon) to exclude oxygen.