## Introduction
Controlling the geometry of double bonds is a central challenge in [organic synthesis](@entry_id:148754). The reduction of [alkynes](@entry_id:746370) offers a direct path to alkenes, but achieving specific stereochemistry—either *cis* or *trans*—requires precise methodological choices. While [catalytic hydrogenation](@entry_id:192975) using Lindlar's catalyst reliably produces *cis*-alkenes, organic chemists require an equally dependable strategy to access their *trans*-alkene counterparts. The [dissolving metal reduction](@entry_id:191783) of [alkynes](@entry_id:746370) provides the definitive solution to this problem, offering excellent [stereoselectivity](@entry_id:198631) for the *trans* isomer.

This article provides a comprehensive examination of this fundamental transformation. The first chapter, **Principles and Mechanisms**, will unpack the stepwise radical mechanism, explaining how [solvated electrons](@entry_id:181108) and a proton source work in concert to achieve the characteristic *anti*-addition of hydrogen. The second chapter, **Applications and Interdisciplinary Connections**, will explore the reaction's strategic role in complex syntheses, its [chemoselectivity](@entry_id:149526) profile with other [functional groups](@entry_id:139479), and its connection to the spectroscopic techniques used for product verification. Finally, **Hands-On Practices** will offer exercises to apply this knowledge to practical synthetic challenges. We begin by dissecting the core principles that make this reaction a cornerstone of modern [organic chemistry](@entry_id:137733).

## Principles and Mechanisms

The partial reduction of [alkynes](@entry_id:746370) to [alkenes](@entry_id:183502) represents a fundamental transformation in organic synthesis, one where [stereochemical control](@entry_id:201531) is paramount. While an alkyne may be reduced to either a *cis*- or *trans*-alkene, the specific outcome is dictated entirely by the choice of reagents. The [dissolving metal reduction](@entry_id:191783) stands as the canonical method for the stereoselective synthesis of **_trans_*-[alkenes](@entry_id:183502)** (or *E*-[alkenes](@entry_id:183502)). This stands in direct contrast to methods like [catalytic hydrogenation](@entry_id:192975) using Lindlar's catalyst, which reliably produces *cis*-alkenes (*Z*-alkenes) via a *syn*-addition mechanism [@problem_id:2167734]. Understanding the principles and mechanisms behind the [dissolving metal reduction](@entry_id:191783) is therefore essential for rationally designing synthetic pathways that require precise control over double bond geometry.

### The Dissolving Metal System: Reagents and Roles

The archetypal conditions for this reaction involve dissolving an alkali metal, most commonly sodium (Na) or lithium (Li), in liquid ammonia (NH₃) at low temperatures (typically around $-78$ °C). When the metal dissolves, it liberates its valence electron, which becomes solvated by the polar ammonia molecules. This process generates a deep blue solution containing **[solvated electrons](@entry_id:181108)** ($e^{-}(\text{am})$), the true reducing agent in the reaction.

The overall transformation converts an internal alkyne into the corresponding *trans*-alkene. For instance, the reduction of 4,4-dimethyl-2-pentyne under these conditions selectively yields (*E*)-4,4-dimethyl-2-pentene [@problem_id:2167745].

In this system, liquid ammonia plays a crucial dual role. First, it serves as the solvent, capable of dissolving both the nonpolar alkyne and the alkali metal to create the reactive solution of [solvated electrons](@entry_id:181108). Second, it acts as the **proton source** required to complete the reduction. Although ammonia is a very weak acid (pKa ≈ 38), it is sufficiently acidic to protonate the highly basic anionic intermediates generated during the [reaction mechanism](@entry_id:140113) [@problem_id:2167713]. While stronger proton donors like ethanol can be added to accelerate the reaction, the classical system relies on ammonia alone. Alternative solvents like water are incompatible, as they react violently with [alkali metals](@entry_id:139133), while non-protic, non-polar solvents like hexane are ineffective as they cannot dissolve the metal or provide protons.

### The Stepwise Radical Mechanism

Unlike catalytic hydrogenations that occur on a metal surface, the [dissolving metal reduction](@entry_id:191783) proceeds through a stepwise mechanism in solution involving discrete single-electron transfer and protonation events. This pathway is the key to its unique stereochemical outcome.

#### Step 1: Single-Electron Transfer and the Radical Anion

The reaction is initiated by the transfer of a single [solvated electron](@entry_id:152278) to the alkyne molecule. According to [molecular orbital theory](@entry_id:137049), this incoming electron must occupy the alkyne's **Lowest Unoccupied Molecular Orbital (LUMO)**. For an alkyne, the LUMO is one of the two degenerate **π* [antibonding orbitals](@entry_id:178754)** associated with the [carbon-carbon triple bond](@entry_id:188700) [@problem_id:2167749].

$$
\text{R}-\text{C}\equiv\text{C}-\text{R}' + e^{-} (\text{am}) \longrightarrow [\text{R}-\text{C}\equiv\text{C}-\text{R}']^{\bullet -}
$$

The addition of an electron into an [antibonding orbital](@entry_id:261662) is an energetically demanding process, as it weakens the C≡C bond. Consequently, this initial single-[electron transfer](@entry_id:155709) (SET) step has a significant activation energy and is typically the **rate-determining step** of the overall reaction [@problem_id:2167695].

The immediate product of this step is a highly reactive intermediate known as a **radical anion**. This species is aptly named, as it contains both an unpaired electron (making it a radical) and a net negative charge (making it an anion) distributed across the two carbons of the original triple bond [@problem_id:2167678].

#### The Origin of *trans*-Stereoselectivity

The stereochemical outcome of the reaction is determined immediately following the formation of the radical anion. The addition of an electron into a π* orbital reduces the bond order between the two central carbons from three to approximately two-and-a-half, significantly lowering the [rotational barrier](@entry_id:153477). This allows for rapid interconversion between the *cis* and *trans* geometric arrangements of the substituents (R and R').

A [dynamic equilibrium](@entry_id:136767) is established between the *cis*-radical anion and the *trans*-radical anion. The *trans* configuration, which places the two (often sterically bulky) substituent groups on opposite sides of the incipient double bond, is **thermodynamically more stable** than the *cis* configuration due to the minimization of [steric repulsion](@entry_id:169266). Because the rate of this geometric equilibration is much faster than the rate of the subsequent protonation step, the population of the [radical anion intermediate](@entry_id:183572) is dominated by the more stable *trans* isomer [@problem_id:2167739]. It is the trapping of this more stable intermediate that dictates the stereochemistry of the final product.

#### Step 2: Protonation to a Vinylic Radical

The highly basic radical anion readily abstracts a proton from a nearby ammonia solvent molecule. This protonation occurs at the carbanionic center and neutralizes the charge, yielding a **vinylic radical**.

$$
[\text{R}-\dot{\text{C}}=\bar{\text{C}}-\text{R}']_{\text{trans}} + \text{NH}_3 \longrightarrow [\text{R}-\dot{\text{C}}=\text{CH}-\text{R}']_{\text{trans}} + \text{NH}_2^{-}
$$

Because this step proceeds from the more abundant *trans*-radical anion, the resulting vinylic radical predominantly exists with the substituents in a **trans geometry**. The unpaired electron resides in a p-orbital on the remaining sp²-hybridized carbon atom [@problem_id:2167694].

#### Steps 3 and 4: Completion of the Reduction

The mechanism concludes with two further steps that mirror the first two.

**Step 3:** A second single-electron transfer from the metal converts the neutral vinylic radical into a **vinylic anion**.

$$
[\text{R}-\dot{\text{C}}=\text{CH}-\text{R}']_{\text{trans}} + e^{-} (\text{am}) \longrightarrow [\text{R}-\bar{\text{C}}=\text{CH}-\text{R}']_{\text{trans}}
$$

**Step 4:** This vinylic anion is a strong base and is immediately quenched by a final [proton transfer](@entry_id:143444) from another ammonia molecule, yielding the neutral *trans*-alkene product and regenerating an [amide](@entry_id:184165) ion.

$$
[\text{R}-\bar{\text{C}}=\text{CH}-\text{R}']_{\text{trans}} + \text{NH}_3 \longrightarrow \text{R}-\text{CH}=\text{CH}-\text{R}'_{\text{trans}} + \text{NH}_2^{-}
$$

The overall process results in the formal **[anti-addition](@entry_id:196470)** of two hydrogen atoms across the alkyne's triple bond, one on each face of the original π system. This mechanistic rationale elegantly explains the consistent formation of *trans*-[alkenes](@entry_id:183502), such as the synthesis of (*E*)-4-methylpent-2-ene from 4-methylpent-2-yne [@problem_id:2167720].

### Scope and Limitations: The Behavior of Terminal Alkynes

A crucial limitation of the [dissolving metal reduction](@entry_id:191783) concerns its application to **terminal [alkynes](@entry_id:746370)** (R-C≡C-H). The proton on the sp-hybridized carbon of a [terminal alkyne](@entry_id:193059) is significantly more acidic (pKa ≈ 25) than protons on sp² or sp³ carbons.

When a [terminal alkyne](@entry_id:193059) is exposed to [sodium in liquid ammonia](@entry_id:189012), a competing reaction takes precedence. The [solvated electrons](@entry_id:181108) can react with the ammonia solvent to form [sodium amide](@entry_id:196058) (NaNH₂), a powerful base. The [amide](@entry_id:184165) anion (NH₂⁻) is the conjugate base of ammonia (pKa ≈ 38). Given the large difference in acidity between the [terminal alkyne](@entry_id:193059) and ammonia, a rapid and essentially irreversible [acid-base reaction](@entry_id:149679) occurs. The amide ion deprotonates the [terminal alkyne](@entry_id:193059) to form a stable **[acetylide anion](@entry_id:197597)** [@problem_id:2167721].

$$
\text{R}-\text{C}\equiv\text{C}-\text{H} \quad + \quad \text{NH}_2^{-} \quad \rightleftharpoons \quad \text{R}-\text{C}\equiv\text{C}:^{-} \quad + \quad \text{NH}_3
$$
$$
(\text{pKa} \approx 25) \qquad \qquad \qquad \qquad \qquad \qquad (\text{pKa} \approx 38)
$$

The [equilibrium constant](@entry_id:141040) for this reaction is approximately $10^{(38-25)} = 10^{13}$, meaning the reaction proceeds completely to the right. The resulting [acetylide anion](@entry_id:197597) is resistant to reduction under these conditions. Therefore, for terminal [alkynes](@entry_id:746370), deprotonation is the exclusive outcome, and the [dissolving metal reduction](@entry_id:191783) of the triple bond does not occur. This reactivity is not a failure but is itself a synthetically useful transformation for forming carbon-carbon bonds.