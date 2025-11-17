## Introduction
The addition of [hydrogen halides](@entry_id:193573) to alkenes, known as hydrohalogenation, is a cornerstone reaction in [organic chemistry](@entry_id:137733) that transforms simple, unsaturated [hydrocarbons](@entry_id:145872) into functionalized [alkyl halides](@entry_id:192807). Its significance lies not only in its synthetic utility but also in its role as a classic model for understanding the principles of electrophilic reactions. A central puzzle this reaction presents is its regioselectivity: when an unsymmetrical alkene reacts, why does one constitutional isomer form almost exclusively over another? This article addresses this question by dissecting the rules and energetic factors that govern the reaction's outcome.

Across the following chapters, you will gain a deep, mechanistic understanding of this fundamental process. The journey begins in **Principles and Mechanisms**, where we will explore the step-by-step [electrophilic addition](@entry_id:191707) pathway, the energetic basis for Markovnikov's rule through [carbocation stability](@entry_id:149581), and crucial variations like rearrangements and the free-radical [peroxide effect](@entry_id:183658). Next, **Applications and Interdisciplinary Connections** will demonstrate how these core principles are applied to predict reactivity in complex molecules, control selectivity, and elucidate reaction mechanisms in synthetic and [physical organic chemistry](@entry_id:184637). Finally, **Hands-On Practices** will allow you to apply your knowledge to solve problems that challenge your understanding of regioselectivity, rearrangement, and competing [reaction pathways](@entry_id:269351).

## Principles and Mechanisms

The addition of [hydrogen halides](@entry_id:193573) ($HX$) to [alkenes](@entry_id:183502) represents a fundamental transformation in [organic chemistry](@entry_id:137733), serving as a prototypical example of an [electrophilic addition](@entry_id:191707) reaction. This chapter elucidates the core principles governing this reaction, focusing on the underlying mechanism that dictates its regioselectivity and stereochemical outcome. We will explore the energetic landscape of the reaction, the structural features that control its pathway, and the conditions under which alternative mechanisms can prevail.

### The General Mechanism of Electrophilic Addition

The reaction between an alkene and a hydrogen halide, such as hydrogen bromide ($HBr$), is characterized by the interaction between an electron-rich species (a nucleophile) and an electron-poor species (an [electrophile](@entry_id:181327)). In this context, the alkene's $\pi$ bond, a region of high electron density, serves as the **nucleophile**. The hydrogen halide, being a strong acid, provides an electrophilic proton ($H^{+}$).

The reaction proceeds via a two-step mechanism. The first and most critical step is the attack of the alkene's $\pi$ electrons on the hydrogen atom of the hydrogen halide. This protonation of the double bond breaks the $\pi$ bond and forms a new carbon-hydrogen $\sigma$ bond. Crucially, this step generates a high-energy, positively charged intermediate known as a **[carbocation](@entry_id:199575)**, along with a halide anion ($X^{-}$). This initial protonation step is endergonic and has the highest activation energy of the sequence, making it the **[rate-determining step](@entry_id:137729)** of the overall reaction [@problem_id:2176177].

In the second step, the halide anion, a potent nucleophile, rapidly attacks the electron-deficient carbocation center. This electron-pair donation forms a new carbon-halogen $\sigma$ bond, yielding the final alkyl halide product.

To summarize the roles of the reactants in the key rate-determining step, consider the reaction of propene with $HBr$. The propene molecule ($\text{CH}_3\text{CH=CH}_2$) donates the electron pair from its $\pi$ bond to the proton. Therefore, in this crucial first step, propene acts as the nucleophile, and the proton from $HBr$ acts as the electrophile [@problem_id:2176177].

### Regioselectivity and Markovnikov's Rule

When the reacting alkene is unsymmetrical, such as propene or 2-methylpropene, the addition of $HX$ can theoretically yield two different [constitutional isomers](@entry_id:155733). For instance, the addition of $HBr$ to propene could produce either 1-bromopropane or 2-bromopropane. However, experiments consistently show that one isomer is formed in significant preference over the other. This preference for reaction at a particular site is termed **regioselectivity**.

In the 19th century, the Russian chemist Vladimir Markovnikov observed a consistent pattern in these reactions. He formulated an empirical rule, now known as **Markovnikov's rule**, which states that in the addition of a protic acid to an unsymmetrical alkene, the hydrogen atom attaches to the carbon atom of the double bond that already bears the greater number of hydrogen atoms.

While this rule is a powerful predictive tool, the modern understanding of the reaction mechanism provides a more fundamental explanation. The regioselectivity is not determined by an arbitrary counting of hydrogen atoms, but rather by the stability of the intermediate formed in the [rate-determining step](@entry_id:137729). The modern, mechanistically sound statement of Markovnikov's rule is as follows: the [electrophilic addition](@entry_id:191707) of $HX$ to an unsymmetrical alkene proceeds via the formation of the **most stable [carbocation intermediate](@entry_id:204002)** [@problem_id:2176127]. Since the proton adds first, it will add to the carbon atom that allows the positive charge to be placed on the more substituted, and thus more stable, carbon atom.

### The Energetic Basis: Carbocation Stability and Kinetic Control

The selectivity of the reaction pathway is a matter of kinetics. The major product is the one that is formed fastest, which corresponds to the reaction pathway with the lowest activation energy ($E_a$ or $\Delta G^{\ddagger}$). According to the **Hammond Postulate**, for a single endergonic reaction step, the transition state will be structurally and energetically similar to the product of that step. In the hydrohalogenation of an alkene, the rate-determining step is the formation of the high-energy [carbocation](@entry_id:199575). Therefore, the transition state leading to the [carbocation](@entry_id:199575) resembles the carbocation itself. Consequently, factors that stabilize the [carbocation intermediate](@entry_id:204002) also stabilize the transition state leading to it, thereby lowering the activation energy for its formation [@problem_id:2176173].

The stability of [carbocations](@entry_id:185610) is governed primarily by two electronic effects:

1.  **Hyperconjugation**: This is the most significant stabilizing interaction. It involves the [delocalization](@entry_id:183327) of electron density from adjacent, filled carbon-hydrogen (C-H) or carbon-carbon (C-C) $\sigma$-bonds into the empty, unhybridized p-orbital of the $sp^2$-hybridized carbocation center. The more alkyl groups that are attached to the carbocationic carbon, the more adjacent $\sigma$-bonds are available to participate in [hyperconjugation](@entry_id:263927). This delocalization of electron density disperses the positive charge, lowering the energy of the species. As a result, the stability of [carbocations](@entry_id:185610) increases with substitution: **tertiary ($3^\circ$) > secondary ($2^\circ$) > primary ($1^\circ$) > methyl**. For example, in the protonation of propene, adding the proton to the terminal $CH_2$ group (C1) yields a secondary carbocation at C2, which is stabilized by six adjacent C-H bonds. Adding the proton to the internal $CH$ group (C2) would yield a primary carbocation at C1, stabilized by only two adjacent C-H bonds. The significantly greater stabilization afforded by [hyperconjugation](@entry_id:263927) in the secondary carbocation makes its formation the overwhelmingly preferred pathway [@problem_id:2176162] [@problem_id:2176176].

2.  **Inductive Effects**: Alkyl groups are weakly electron-donating through the $\sigma$-bond framework. This inductive donation of electron density helps to neutralize the positive charge on the [carbocation](@entry_id:199575) center, contributing to its stability. Conversely, electronegative atoms or groups, such as halogens, exert a powerful electron-withdrawing inductive effect, which destabilizes a nearby [carbocation](@entry_id:199575) by intensifying the positive charge. This effect is distance-dependent, diminishing rapidly as the number of bonds separating the group and the cationic center increases [@problem_id:2176168].

The quantitative impact of this difference in activation energy on the [product distribution](@entry_id:269160) can be significant. For two competing pathways leading to a major and minor product, the ratio of their formation is related to the difference in their activation energies ($\Delta \Delta G^{\ddagger} \approx \Delta E_a$). As shown in the reaction of propene with HBr, a difference in activation energies of just $12.5 \text{ kJ mol}^{-1}$ at room temperature ($298.15 \text{ K}$) results in the major product being formed in a ratio of approximately 155:1 relative to the minor product, illustrating the powerful effect of [kinetic control](@entry_id:154879) [@problem_id:2176138].

### A Complication: Carbocation Rearrangements

A key feature of [carbocation](@entry_id:199575) intermediates is their propensity to rearrange into more stable structures, if such a pathway is available. This can lead to products that are not predicted by a simple application of Markovnikov's rule to the initial [alkene structure](@entry_id:192411). The most common type of rearrangement is a **1,2-shift**, where an atom or group (typically a hydride ion, $H:^{-}$, or an alkyl group) on a carbon atom adjacent to the carbocationic center migrates with its bonding pair of electrons to the [carbocation](@entry_id:199575) center.

Consider the reaction of 3-methyl-1-butene with $HBr$ [@problem_id:2176144] [@problem_id:2176148].
Initial protonation follows Markovnikov's rule, with the proton adding to the terminal $CH_2$ (C1) to form the more stable of the two initial possibilities: a secondary ($2^\circ$) carbocation at C2.
$$ \underset{\text{3-methyl-1-butene}}{\text{CH}_2\text{=CH-CH(CH}_3\text{)}_2} + \text{H}^+ \rightarrow \underset{\text{secondary carbocation}}{\text{CH}_3\text{-CH}^+\text{-CH(CH}_3\text{)}_2} $$
However, the carbon atom adjacent to this secondary [carbocation](@entry_id:199575) (C3) is a tertiary center bearing a hydrogen atom. A rapid **1,[2-hydride shift](@entry_id:198648)** can occur, where this hydrogen atom migrates with its electron pair from C3 to C2.
$$ \underset{\text{secondary carbocation}}{\text{CH}_3\text{-CH}^+\text{-CH(CH}_3\text{)}_2} \xrightarrow{\text{1,2-hydride shift}} \underset{\text{tertiary carbocation}}{\text{CH}_3\text{-CH}_2\text{-C}^+\text{(CH}_3\text{)}_2} $$
This rearrangement is energetically favorable because it converts a less stable secondary carbocation into a more stable tertiary ($3^\circ$) carbocation. The subsequent attack by the bromide ion ($Br^{-}$) occurs at this rearranged tertiary [carbocation](@entry_id:199575), yielding 2-bromo-2-methylbutane as the major product. The unrearranged product, 2-bromo-3-methylbutane, is formed only as a minor product. Therefore, when predicting the major product of a hydrohalogenation reaction, one must always inspect the initially formed [carbocation](@entry_id:199575) for the possibility of a rearrangement to a more stable [carbocation](@entry_id:199575).

### Stereochemistry of Hydrohalogenation

The stereochemical outcome of a reaction is another critical aspect of its mechanism. A carbocation is $sp^2$-hybridized and possesses a trigonal planar geometry around the positively charged carbon. The empty p-orbital lies perpendicular to this plane. When the nucleophilic halide attacks, it can do so from either face of this planar intermediate with equal probability.

This has important consequences when a new stereocenter is formed. Consider the addition of $HCl$ to (E)-2-butene or (Z)-2-butene. In either case, protonation yields the same [achiral](@entry_id:194107) secondary [carbocation](@entry_id:199575), the butan-2-yl cation. The subsequent attack by the chloride ion can occur from the top face or the bottom face. These two modes of attack are [enantiotopic](@entry_id:748964), leading to the formation of (R)-2-chlorobutane and (S)-2-chlorobutane in equal amounts. The final product is therefore a **racemic mixture** [@problem_id:2176181].

This outcome allows us to classify the reaction's stereochemistry.
- A reaction is **stereospecific** if stereoisomeric starting materials yield stereoisomerically different products (e.g., *cis* alkene gives product X, *trans* alkene gives product Y). Since both (E)- and (Z)-2-butene give the same racemic product mixture, the reaction is **not stereospecific**.
- A reaction is **stereoselective** if it preferentially forms one stereoisomer over another (e.g., more R than S). Since a racemic mixture is formed, the reaction is **not stereoselective**.

The loss of stereochemical information from the starting alkene is a hallmark of mechanisms involving a planar, [achiral](@entry_id:194107) [carbocation intermediate](@entry_id:204002).

### The Peroxide Effect: A Competing Radical Mechanism

While the [electrophilic addition](@entry_id:191707) mechanism accounts for the [hydrohalogenation of alkenes](@entry_id:199827) with $HCl$, $HBr$, and $HI$ under standard conditions, the addition of $HBr$ behaves differently in the presence of peroxides (ROOR). Under these conditions, the reaction proceeds via a **free-[radical chain mechanism](@entry_id:180350)**, and the regioselectivity is reversed, yielding the **anti-Markovnikov** product.

This "[peroxide effect](@entry_id:183658)" is unique to $HBr$. The mechanism involves three stages:

1.  **Initiation**: The weak peroxide O-O bond is homolytically cleaved by heat or light to form two alkoxy radicals ($RO\cdot$). The alkoxy radical then abstracts a hydrogen atom from $HBr$ to generate a bromine radical ($Br\cdot$).
    $$
    \begin{align*}
    ROOR \rightarrow 2 RO\cdot \\
    RO\cdot + HBr \rightarrow ROH + Br\cdot
    \end{align*}
    $$
    
2.  **Propagation**: This is a two-step cycle. First, the bromine radical, an electrophilic species, adds to the alkene's $\pi$ bond. This addition occurs at the less substituted carbon in order to form the more stable carbon radical at the more substituted position. Radical stability follows the same trend as [carbocation stability](@entry_id:149581) ($3^\circ > 2^\circ > 1^\circ$). For 2-methylpropene, the $Br\cdot$ adds to the $CH_2$ carbon to form a stable tertiary radical. Second, this carbon radical abstracts a hydrogen atom from another molecule of $HBr$ to form the final product and regenerate a bromine radical, which continues the chain.
    $$
    \begin{align*}
    Br\cdot + (CH_3)_2C=CH_2 \rightarrow (CH_3)_2\dot{C}-CH_2Br \quad \text{(tertiary radical formation)} \\
    (CH_3)_2\dot{C}-CH_2Br + HBr \rightarrow (CH_3)_2CH-CH_2Br + Br\cdot
    \end{align*}
    $$
    
3.  **Termination**: The reaction ceases when two radicals combine.

As this mechanism illustrates, the species that adds first ($Br\cdot$) attaches to the carbon with more hydrogens, causing the hydrogen atom to ultimately bond to the carbon with fewer hydrogens. The result is 1-bromo-2-methylpropane, the anti-Markovnikov product. This complete reversal of regioselectivity is a direct consequence of the change from an ionic mechanism controlled by [carbocation stability](@entry_id:149581) to a radical mechanism controlled by [carbon radical stability](@entry_id:193047) [@problem_id:2176169].