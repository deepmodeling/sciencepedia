## Introduction
The synthesis of alkynes, molecules defined by their carbon-carbon triple bond, is a foundational topic in organic chemistry, opening doors to a vast array of subsequent transformations. A primary challenge for chemists is the controlled introduction of this high-energy functional group into a carbon framework. This article addresses this challenge by providing a detailed exploration of one of the most powerful and classic methods for alkyne preparation: the double elimination reaction of dihaloalkanes. This guide will take you from the fundamental principles to advanced applications. The first chapter, **Principles and Mechanisms**, will dissect the stepwise E2 reaction, explaining the role of strong bases, the nature of key intermediates like vinylic halides, and the factors governing the reaction's success. Following this, the **Applications and Interdisciplinary Connections** chapter will showcase the strategic utility of this method in multi-step synthesis, its role in constructing complex and strained ring systems, and its connections to core concepts like thermodynamics and stereoelectronics. Finally, the **Hands-On Practices** section offers a series of problems designed to solidify your understanding and hone your synthetic problem-solving skills.

## Principles and Mechanisms

The synthesis of alkynes, compounds containing a carbon-carbon triple bond, is a cornerstone of organic synthesis, providing access to a versatile functional group. While the previous chapter introduced the structure and properties of alkynes, this chapter delves into one of the most fundamental methods for their preparation: the **double dehydrohalogenation** of dihaloalkanes. This process involves the elimination of two equivalents of a hydrogen halide ($HX$) from a suitable substrate to form two new $\pi$ bonds, culminating in the creation of an alkyne. We will explore the principles governing this reaction, the stepwise mechanism through which it proceeds, and the factors that influence its outcome.

### The Double Elimination Reaction: An Overview

The core transformation in this synthesis is the conversion of a saturated carbon framework into an unsaturated one. The starting materials for this reaction are typically **dihaloalkanes**, which can be classified into two main types based on the relative positions of the two halogen atoms.

A **vicinal dihalide** is a compound in which two halogen atoms are attached to adjacent carbon atoms. A **geminal dihalide** features two halogen atoms bonded to the same carbon atom. Both types of dihalides can serve as effective precursors for alkyne synthesis. The key requirement is that two successive elimination reactions are possible.

For example, the preparation of the internal alkyne but-2-yne ($CH_3-C\equiv C-CH_3$) can be envisioned from two distinct starting materials. Treatment of the vicinal dihalide 2,3-dichlorobutane with a strong base will induce eliminations across the C2-C3 bond, yielding but-2-yne. Similarly, starting with the geminal dihalide 2,2-dibromobutane, the two eliminations will also occur to form a triple bond between C2 and C3, again producing but-2-yne. The position of the resulting triple bond is dictated by the location of the halogen atoms in the starting material, as these are the carbons from which the leaving groups depart [@problem_id:2191319]. This highlights a powerful principle: the structure of the dihalide precursor directly controls the regiochemistry of the alkyne product.

### A Stepwise Mechanism: The Vinylic Halide Intermediate

While we refer to the reaction as a "double elimination," it does not occur in a single concerted step. Instead, it is a sequence of two distinct **bimolecular elimination (E2)** reactions. Each step involves a strong base abstracting a proton while a halide leaving group departs from an adjacent carbon.

**Step 1: Formation of a Vinylic Halide**

The first E2 elimination converts the saturated alkyl dihalide into an alkene that still bears a halogen substituent. This intermediate is known as a **vinylic halide**, defined as a compound where a halogen is directly attached to one of the $sp^2$-hybridized carbons of a double bond. For instance, in the synthesis of hex-2-yne from the vicinal dihalide 2,3-dibromohexane, the first equivalent of base removes a proton from either C2 or C3, and a bromide ion is expelled from the adjacent carbon. This generates a C2=C3 double bond. The resulting intermediate would be either 2-bromohex-2-ene or 3-bromohex-2-ene, both of which are vinylic halides poised for the next step [@problem_id:2191315].

$$
\text{Alkyl Dihalide} \xrightarrow[\text{-HX}]{\text{Base, E2}} \text{Vinylic Halide}
$$

**Step 2: Formation of the Alkyne**

The second E2 elimination occurs on the vinylic halide intermediate. The base abstracts a proton from the carbon adjacent to the one bearing the halogen, leading to the formation of the second $\pi$ bond and the final alkyne product.

$$
\text{Vinylic Halide} \xrightarrow[\text{-HX}]{\text{Base, E2}} \text{Alkyne}
$$

Understanding this stepwise process is crucial, as the reaction conditions must be robust enough to drive both eliminations to completion. The second step, as we will see, presents a significantly higher kinetic barrier than the first.

### Mechanistic Nuances: Unpacking the Reaction Requirements

The successful synthesis of an alkyne via double elimination depends critically on three factors: the strength of the base, the nature of the leaving group, and the structure of the substrate.

#### The Challenge of the Second Elimination and the Need for a Strong Base

It is an experimental observation that the second elimination step (vinylic halide to alkyne) is substantially more difficult and proceeds more slowly than the first (alkyl dihalide to vinylic halide). The fundamental reason for this lies in the strength of the carbon-halogen bond being broken. In the first E2 step, the leaving group is attached to an $sp^3$-hybridized carbon. In the second step, it is attached to an $sp^2$-hybridized carbon. Orbitals with higher **s-character** form stronger, shorter bonds because the electrons are held more closely to the nucleus. An $sp^2$ orbital (33% s-character) has more s-character than an $sp^3$ orbital (25% s-character). Consequently, the $C_{sp^2}-X$ bond in the vinylic halide is stronger than the $C_{sp^3}-X$ bond in the starting dihalide. Since breaking this bond is part of the rate-determining step of the E2 reaction, a higher activation energy is required for the second elimination [@problem_id:2191326].

This increased difficulty necessitates the use of a very strong base. Common alkoxide bases, such as sodium ethoxide ($NaOCH_2CH_3$), are generally sufficient to perform the first elimination but are often too weak to effectively promote the second. When 1,2-dibromopropane is treated with sodium ethoxide, the reaction stalls at the vinylic halide stage, yielding little of the desired propyne. Although the proton on an $sp^2$ carbon is more acidic than one on an $sp^3$ carbon, this effect is not sufficient to overcome the high barrier associated with breaking the strong $C_{sp^2}-X$ bond. Thus, a base like ethoxide is simply not strong enough to achieve the second dehydrohalogenation at an appreciable rate [@problem_id:2191316].

The reagent of choice for this transformation is typically **sodium amide ($NaNH_2$)** dissolved in liquid ammonia ($NH_3$). The amide anion ($NH_2^−$) is an exceptionally strong base, far more so than an alkoxide, and is capable of driving both eliminations to completion.

#### The Influence of the Leaving Group

As with all E2 reactions, the rate is also sensitive to the identity of the halogen leaving group. The reaction proceeds faster with better leaving groups. Leaving group ability for the halogens follows the trend $I^- > Br^- > Cl^- > F^-$. This trend correlates with the stability of the halide anion and inversely with the strength of the carbon-halogen bond.

Consider the synthesis of but-1-yne from either 1,2-dichlorobutane or 1,2-diiodobutane. The reaction with 1,2-diiodobutane will proceed more readily. This is for two reasons: first, the carbon-iodine bond is significantly weaker than the carbon-chlorine bond, making it easier to break during the E2 transition state. Second, iodide ($I^−$) is a more stable anion than chloride ($Cl^−$), making it a better leaving group. Both factors contribute to a lower activation energy and a faster reaction rate for both elimination steps [@problem_id:2191322].

### Regiochemical Control: Terminal vs. Internal Alkynes

The use of a powerful base like sodium amide introduces important considerations, particularly when synthesizing **terminal alkynes** (where the triple bond is at the end of a carbon chain, $R-C\equiv C-H$).

#### Synthesis of Terminal Alkynes and the Aqueous Workup

The proton on the $sp$-hybridized carbon of a terminal alkyne is remarkably acidic (pKa ≈ 25) compared to protons on $sp^2$ or $sp^3$ carbons. The amide anion ($NH_2^−$) is the conjugate base of ammonia (pKa ≈ 38). Since ammonia is a much weaker acid than a terminal alkyne, the amide anion is a strong enough base to deprotonate a terminal alkyne.

Consequently, if a terminal alkyne is formed in the presence of excess $NaNH_2$, it will be immediately deprotonated to form an **acetylide anion**. For example, the reaction of 1,2-dibromopentane with three equivalents of $NaNH_2$ first produces pent-1-yne via double elimination (consuming two equivalents of base), which is then deprotonated by the third equivalent of base to form the sodium pentynide salt.

$$
CH_3(CH_2)_2C\equiv CH + NaNH_2 \longrightarrow CH_3(CH_2)_2C\equiv C^-Na^+ + NH_3
$$

This acetylide salt is the species present in the reaction flask at the end of the reaction. To obtain the neutral terminal alkyne product, a **protonation step** is required. This is accomplished during the reaction **workup** by adding a mild proton source, such as water or dilute aqueous acid. The water protonates the acetylide anion, regenerating the terminal alkyne, which can then be isolated [@problem_id:2191306].

$$
CH_3(CH_2)_2C\equiv C^-Na^+ + H_2O \longrightarrow CH_3(CH_2)_2C\equiv CH + NaOH
$$

#### Base-Catalyzed Alkyne Isomerization

The deprotonation of a terminal alkyne is also the first step in a process known as **base-catalyzed isomerization**. Under forcing conditions, such as prolonged heating with a strong base, the triple bond can migrate along the carbon chain. This occurs through a series of reversible deprotonation and reprotonation events, often involving an **allenyl anion** intermediate. This process allows the various positional isomers of the alkyne to interconvert.

Given enough time to reach **thermodynamic equilibrium**, the reaction mixture will be dominated by the most stable alkyne isomer. For acyclic alkynes, **internal alkynes** are more stable than terminal alkynes due to hyperconjugation and electronic effects. Therefore, if pent-1-yne is heated with sodium amide, it will gradually isomerize to the more stable internal alkyne, pent-2-yne. This phenomenon can be used strategically: if the desired product is the internal alkyne, the reaction can be run at a high temperature to promote isomerization. If the terminal alkyne is desired, milder conditions and a careful workup are essential [@problem_id:2191307].

### Stereochemical and Geometric Limitations

The E2 mechanism imposes strict stereochemical and geometric requirements that can limit the scope of this reaction.

#### Stereoelectronics of the E2 Reaction

The E2 reaction proceeds most efficiently when the proton being abstracted and the leaving group are oriented **anti-periplanar** to one another (a dihedral angle of 180°). This alignment allows for optimal overlap of the developing p-orbitals in the transition state. This requirement can be illustrated with a thought experiment involving an isotopically labeled substrate, such as (R)-1,1-dibromo-2-deuteriobutane. In the first elimination, the base will preferentially abstract the proton (H) over the deuteron (D) from C2 due to the primary **kinetic isotope effect** (C-H bonds are broken faster than C-D bonds). This leads to a vinylic bromide intermediate containing deuterium. For the second elimination to occur, the remaining deuteron on C2 must be removed anti to the bromine on C1. This results in the complete loss of the deuterium label from the molecule, and the initially formed alkyne is but-1-yne, which then isomerizes to the more stable but-2-yne. This example beautifully demonstrates how the strict stereoelectronic demands of each E2 step dictate the final outcome [@problem_id:2191324].

#### Geometric Constraints in Cyclic Systems

The most profound limitation of alkyne synthesis arises from geometric constraints, particularly in cyclic systems. The two carbon atoms of an alkyne are $sp$-hybridized, and the ideal geometry for an alkyne functional group is **linear**, with bond angles of 180°. While acyclic chains can easily adopt this geometry, incorporating a linear C-C≡C-C unit into a small or medium-sized ring introduces immense **angle strain**.

For this reason, it is impossible to synthesize a stable cycloalkyne in a small ring. An attempt to synthesize cyclohexyne from 1,1-dibromocyclohexane via double elimination will fail. The six-membered ring cannot accommodate the 180° bond angle required by the triple bond without suffering from an insurmountable level of strain [@problem_id:2191331]. The same is true for even smaller rings; 1,1-dichlorocyclopentane cannot be converted into cyclopentyne [@problem_id:2191330]. Only in larger, more flexible rings (typically eight carbons or more) does the synthesis of a cycloalkyne become feasible. Cyclooctyne is the smallest cycloalkyne that can be isolated as a stable compound, although it is still significantly strained compared to its acyclic counterparts. This principle underscores the critical interplay between reactivity and molecular geometry.