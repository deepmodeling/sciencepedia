## Introduction
The reaction of amines with nitrous acid ($HNO_2$) is a fundamental and versatile transformation in [organic chemistry](@entry_id:137733), serving as a powerful tool for converting a simple amino group into a wide array of other functionalities. The significance of this chemistry lies in its remarkable ability to produce dramatically different outcomes based on subtle changes in the amine's structure—whether it is primary, secondary, or tertiary, aliphatic or aromatic. This structural dependency often presents a challenge to students, as it creates a complex decision tree of possible products. This article aims to demystify these reactions by providing a clear and systematic exploration of the underlying principles and their practical consequences.

Across the following chapters, you will gain a deep understanding of this topic. The first chapter, **Principles and Mechanisms**, will dissect the core chemical processes, from the generation of the active [electrophile](@entry_id:181327) to the detailed pathways for each class of amine. The second chapter, **Applications and Interdisciplinary Connections**, will showcase the immense synthetic utility of these reactions, particularly the use of [diazonium salts](@entry_id:196239), and explore their relevance in chemical analysis, biochemistry, and toxicology. Finally, the **Hands-On Practices** section provides carefully selected problems to reinforce your grasp of these concepts and challenge your problem-solving skills.

## Principles and Mechanisms

The reaction of amines with nitrous acid ($HNO_2$) represents a rich and diverse area of organic chemistry, providing distinct and predictable outcomes based on the structure of the amine substrate. These reactions are fundamental to [synthetic chemistry](@entry_id:189310), particularly in the transformation of primary aromatic amines into versatile [diazonium salt](@entry_id:192130) intermediates. The reactivity hinges on the generation of an electrophilic nitrosating agent and the subsequent interaction with the amine's nucleophilic nitrogen atom. The classification of the amine—as primary, secondary, or tertiary, and as aliphatic or aromatic—is the principal determinant of the reaction's course and products.

### Generation of the Electrophilic Nitrosating Species

The reactions of amines with nitrous acid are typically conducted by generating the nitrous acid *in situ*. This is achieved by treating an aqueous solution of sodium nitrite ($NaNO_2$) with a strong mineral acid, such as hydrochloric acid ($HCl$), usually at low temperatures ($0-5^\circ C$).

$NaNO_2 + HCl \rightarrow HONO + NaCl$

The nitrous acid formed is a weak acid and exists in equilibrium with its protonated forms in the acidic medium. The identity of the active electrophilic species that attacks the amine is highly dependent on the pH of the solution.

In strongly acidic media (low pH), the dominant [electrophile](@entry_id:181327) is the **[nitrosonium ion](@entry_id:188211)**, $NO^+$. Its formation is a classic example of [acid catalysis](@entry_id:184694). First, the nitrite ion is protonated on one of its oxygen atoms to yield nitrous acid, $HONO$. In a strongly acidic environment, a second protonation event occurs, this time on the hydroxyl oxygen of nitrous acid. This creates a protonated intermediate, $H_2O-N=O^+$, which contains an excellent leaving group: a neutral water molecule. The subsequent loss of water generates the highly electrophilic [nitrosonium ion](@entry_id:188211) [@problem_id:2194572].

$HONO + H^+ \rightleftharpoons H_2O-N=O^+$

$H_2O-N=O^+ \rightarrow H_2O + N=O^+$

In contrast, under weakly acidic or neutral conditions, the concentration of $H^+$ is too low to facilitate the formation of the [nitrosonium ion](@entry_id:188211) efficiently. In this regime, the active nitrosating agent is **dinitrogen trioxide** ($N_2O_3$), which is formed through the self-[condensation](@entry_id:148670) or [dimerization](@entry_id:271116) of two molecules of nitrous acid.

$2 HONO \rightleftharpoons N_2O_3 + H_2O$

The different nature of the [electrophile](@entry_id:181327) under varying pH conditions gives rise to distinct kinetic profiles for nitrosation reactions. For instance, the N-nitrosation of [secondary amines](@entry_id:195221) exhibits a rate law that is second-order in $[HNO_2]$ at neutral pH (consistent with $N_2O_3$ as the electrophile) but shifts to first-order in both $[HNO_2]$ and $[H^+]$ at low pH (consistent with $NO^+$ as the electrophile) [@problem_id:2194587]. For the majority of preparative reactions discussed herein, which are run in strong acid, the [nitrosonium ion](@entry_id:188211) is considered the principal reactive species.

### Reactions of Primary Amines: The Formation of Diazonium Salts

Primary amines ($R-NH_2$) react with nitrous acid to form diazonium ions ($R-N_2^+$). However, the stability and subsequent fate of this intermediate depend profoundly on whether the R group is aliphatic or aromatic.

#### Primary Aromatic Amines

The [diazotization](@entry_id:197616) of primary aromatic amines, such as aniline, is one of the most important reactions in [synthetic organic chemistry](@entry_id:189383). When aniline is treated with nitrous acid in excess strong acid at $0-5^\circ C$, it is converted into a **benzenediazonium salt**. The overall balanced equation for this transformation using sodium nitrite and hydrochloric acid is:

$C_6H_5NH_2 + NaNO_2 + 2 HCl \rightarrow C_6H_5N_2^+Cl^- + NaCl + 2 H_2O$

This reaction proceeds through the initial formation of an N-nitrosoamine, which tautomerizes and then undergoes [acid-catalyzed dehydration](@entry_id:188594) to yield the final diazonium ion [@problem_id:2194560].

The resulting **arenediazonium salts** are notable for their moderate stability in cold aqueous solution. This stability is attributed to the [delocalization](@entry_id:183327) of the positive charge into the aromatic $\pi$-system. However, this stability is highly temperature-dependent. If the reaction mixture is allowed to warm above approximately $5-10^\circ C$, the [diazonium salt](@entry_id:192130) rapidly decomposes. The $N_2$ group, being an exceptionally stable molecule, acts as an excellent [leaving group](@entry_id:200739). In an aqueous medium, it is displaced by a water molecule, leading to the formation of a phenol and the evolution of nitrogen gas [@problem_id:2194569].

$C_6H_5N_2^+ + H_2O \xrightarrow{\Delta} C_6H_5OH + N_2 \uparrow + H^+$

This thermal [lability](@entry_id:155953) necessitates that all reactions involving arenediazonium salts be performed in an ice bath. The utility of these salts lies in their ability to be converted into a vast array of other functional groups (e.g., halides, nitriles, hydroxyls) via Sandmeyer and related reactions, where the $-N_2^+$ group is replaced.

#### Primary Aliphatic Amines

In stark contrast to their aromatic counterparts, **alkanediazonium salts**, formed from primary aliphatic amines, are exceedingly unstable, even at low temperatures. They decompose instantaneously upon formation by losing molecular nitrogen ($N_2$) to generate a [carbocation](@entry_id:199575).

$R-NH_2 \xrightarrow{NaNO_2, HCl} [R-N_2^+] \rightarrow R^+ + N_2 \uparrow$

The fate of the resulting carbocation is often complex, as it can undergo substitution, elimination, and rearrangement, leading to a mixture of products. This generally makes the reaction less synthetically useful than the [diazotization](@entry_id:197616) of aromatic amines. A compelling illustration of this behavior is the reaction of 2,2-dimethylpropan-1-amine (neopentylamine) with nitrous acid. The initially formed primary neopentyl carbocation is highly unstable. It undergoes a rapid 1,2-methyl shift to form the much more stable tertiary [carbocation](@entry_id:199575) (the *tert*-amyl cation). This rearranged carbocation is then captured by water to form an alcohol (2-methyl-2-butanol) or loses a proton to form [alkenes](@entry_id:183502) (predominantly the more substituted 2-methyl-2-butene) [@problem_id:2194568]. The products derived from the unrearranged primary carbocation are formed in only minor amounts.

#### Special Case: $\alpha$-Amino Esters

A notable exception to the instability of aliphatic diazonium species occurs with $\alpha$-amino acids and their esters. For example, when ethyl glycinate ($H_2NCH_2CO_2Et$) is treated with nitrous acid, it does not decompose with vigorous evolution of nitrogen gas like a simple primary amine such as ethylamine. Instead, it forms a relatively stable, isolable yellow compound known as ethyl diazoacetate ($N_2CHCO_2Et$) [@problem_id:2194584].

The key to this enhanced stability lies in the acidity of the proton on the carbon atom adjacent to both the newly formed diazonium group and the electron-withdrawing ester group. This $\alpha$-proton is readily removed under the reaction conditions to form a neutral **diazo compound**. This diazo compound is significantly stabilized by resonance, which delocalizes the negative charge from the carbon onto the carbonyl oxygen and distributes the charge within the diazo group itself.

$EtO_2C-CH=N^+=N^- \leftrightarrow EtO_2C-C^-H-N^+\equiv N \leftrightarrow EtO_2C(O^-)=CH-N^+\equiv N$

This [resonance stabilization](@entry_id:147454) provides an alternative, lower-energy pathway (deprotonation) that avoids the formation of an unstable [carbocation](@entry_id:199575), thus preventing immediate decomposition.

### Reactions of Secondary Amines

Secondary amines, both aliphatic and aromatic, react with nitrous acid in a clean and predictable manner to form **N-nitrosamines** ($R_2N-N=O$). The mechanism involves the [nucleophilic attack](@entry_id:151896) of the neutral secondary amine's lone pair on the [nitrosonium ion](@entry_id:188211) electrophile. The resulting intermediate, an N-nitrosammonium ion, then loses a proton to yield the stable, neutral N-nitrosamine product.

$R_2NH + NO^+ \rightarrow [R_2N(H)-N=O]^+ \rightarrow R_2N-N=O + H^+$

For example, the cyclic secondary amine pyrrolidine reacts smoothly with nitrous acid to form N-nitrosopyrrolidine [@problem_id:2194578]. N-nitrosamines are typically yellow oils or low-melting solids and are a class of compounds well-known for their potent carcinogenic activity.

### Reactions of Tertiary Amines

Tertiary amines ($R_3N$) lack an N-H bond, and thus cannot form a stable neutral nitrosamine product through the same pathway as [secondary amines](@entry_id:195221). Their reactivity is again bifurcated based on whether they are aliphatic or aromatic.

#### Tertiary Aliphatic Amines

Simple tertiary aliphatic amines, such as tripropylamine, are generally unreactive towards nitrous acid under the typical cold, acidic conditions. While they possess a lone pair, it is sterically hindered by the three alkyl groups. The primary interaction is a simple [acid-base reaction](@entry_id:149679) with the strong acid in the medium, leading to the formation of a soluble trialkylammonium salt. This results in no significant observable chemical transformation of the amine itself [@problem_id:2194563].

$(CH_3CH_2CH_2)_3N + H^+ \rightarrow (CH_3CH_2CH_2)_3NH^+$

#### Tertiary Aromatic Amines

Tertiary aromatic amines, such as N,N-diethylaniline, behave quite differently. While the nitrogen atom is also protonated in the acidic solution, rendering it non-nucleophilic, the dialkylamino group is a powerful activating group for **[electrophilic aromatic substitution](@entry_id:201966)**. The highly reactive [nitrosonium ion](@entry_id:188211) ($NO^+$) acts as a weak electrophile and attacks the electron-rich aromatic ring rather than the nitrogen atom. This reaction is known as **C-nitrosation**.

The substitution occurs predominantly at the *para* position, which is sterically more accessible than the *ortho* positions. The product, a *p*-nitroso-N,N-dialkylaniline, is often a brightly colored solid. For example, N,N-diethylaniline reacts to form N,N-diethyl-4-nitrosoaniline, which typically appears as a green solid [@problem_id:2194570] [@problem_id:2194563]. This distinct outcome serves as a useful chemical test to differentiate tertiary aliphatic from tertiary aromatic amines.

### Factors Influencing Nitrosation Reactions

Several factors critically influence the outcome and rate of reactions with nitrous acid.

#### Electronic Effects on Reactivity

In the [diazotization](@entry_id:197616) of primary aromatic amines, the [rate-determining step](@entry_id:137729) is the [nucleophilic attack](@entry_id:151896) of the amine on the nitrosating agent. Consequently, the [nucleophilicity](@entry_id:191368) of the amine nitrogen directly correlates with the reaction rate. Electron-donating groups (EDGs) on the aromatic ring, such as a methoxy group ($-OCH_3$), increase the electron density on the nitrogen atom through resonance, making the amine more nucleophilic and accelerating the reaction. Conversely, [electron-withdrawing groups](@entry_id:184702) (EWGs), such as a chloro group ($-Cl$), decrease the basicity and [nucleophilicity](@entry_id:191368) of the amine via their [inductive effect](@entry_id:140883), thus slowing the reaction down. Therefore, the order of reactivity for [diazotization](@entry_id:197616) is: *p*-chloroaniline (slowest)  aniline  *p*-anisidine (fastest) [@problem_id:2194585].

#### The Critical Role of Acidity

Proper control of acidity is paramount for successful [diazotization](@entry_id:197616). A sufficiently high concentration of strong acid is required not only to generate the [nitrosonium ion](@entry_id:188211) but also to ensure that the vast majority of the unreacted starting amine is protonated to its non-nucleophilic ammonium form ($ArNH_3^+$).

If the acid concentration is insufficient, a significant amount of the neutral, nucleophilic amine ($ArNH_2$) will coexist with the electrophilic diazonium ion product ($ArN_2^+$). Under these conditions, the neutral amine can attack the terminal nitrogen of the diazonium ion. This coupling reaction, after deprotonation, forms a triazene (e.g., 1,3-diphenyltriazene), which often precipitates as a yellow solid. This side reaction consumes both the starting material and the desired product, lowering the yield of the [diazotization](@entry_id:197616) [@problem_id:2194581].