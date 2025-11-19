## Introduction
The interaction between gas-phase molecules and solid surfaces is a foundational process in fields ranging from [heterogeneous catalysis](@entry_id:139401) to materials science. At the heart of this interaction lies [adsorption](@entry_id:143659), but the way a molecule initially binds to a surface can follow two profoundly different paths: it can remain intact ([non-dissociative adsorption](@entry_id:195696)) or break apart ([dissociative adsorption](@entry_id:199140)). This initial choice dictates the entire subsequent [reaction network](@entry_id:195028), influencing catalytic activity, selectivity, and [material stability](@entry_id:183933). This article addresses the critical challenge of understanding, distinguishing, and predicting these adsorption modes. Over the next three chapters, we will build a comprehensive understanding of this topic. First, **Principles and Mechanisms** will detail the fundamental differences in kinetics, thermodynamics, and electronic structure that govern these two pathways. Next, **Applications and Interdisciplinary Connections** will explore how these principles are applied to interpret catalytic data, design electrocatalysts, and guide computational materials science. Finally, **Hands-On Practices** will provide opportunities to apply this knowledge to solve realistic problems in [surface kinetics](@entry_id:185097). We begin by examining the core principles that define and differentiate these two crucial surface phenomena.

## Principles and Mechanisms

The interaction of gas-phase molecules with solid surfaces is a cornerstone of [heterogeneous catalysis](@entry_id:139401), materials science, and electrochemistry. This interaction begins with adsorption, a process that can proceed through fundamentally distinct pathways. The nature of this initial step—whether a molecule remains intact or breaks apart upon landing on the surface—profoundly dictates the subsequent reaction network, the identity of surface intermediates, and the overall catalytic performance. This chapter elucidates the principles and mechanisms of the two primary [adsorption](@entry_id:143659) modes: **non-dissociative (or molecular) adsorption** and **[dissociative adsorption](@entry_id:199140)**.

### Fundamental Stoichiometry and Kinetics

The most elementary distinction between [adsorption](@entry_id:143659) modes lies in the stoichiometry of the surface event and its translation into a kinetic rate expression. We consider an idealized uniform surface composed of identical, discrete [adsorption](@entry_id:143659) sites, denoted by $*$.

**Non-[dissociative adsorption](@entry_id:199140)** describes the process where a gas-phase molecule binds to a single surface site without the cleavage of any intramolecular bonds. For a generic monatomic or polyatomic species $B$, this is represented by the [elementary step](@entry_id:182121):

$$ B(g) + * \rightleftharpoons B^* $$

Here, $B(g)$ is the gas-phase molecule and $B^*$ is the adsorbed molecule, or **adsorbate**. According to the law of [mass action](@entry_id:194892) applied to [elementary steps](@entry_id:143394) on surfaces, the rate of [adsorption](@entry_id:143659) is proportional to the [partial pressure](@entry_id:143994) of the reactant gas, $p_B$, and the availability of vacant surface sites. If we denote the fraction of vacant sites as $\theta_*$, the rate of adsorption, $r_{\text{ads},B}$, is:

$$ r_{\text{ads},B} = k_{a} p_{B} \theta_* $$

where $k_a$ is the [adsorption rate constant](@entry_id:191108). The reverse process, desorption, is a unimolecular event involving the adsorbed species, so its rate, $r_{\text{des},B}$, is simply proportional to the fractional coverage of $B^*$, denoted $\theta_B$:

$$ r_{\text{des},B} = k_{d} \theta_B $$

where $k_d$ is the desorption rate constant. This [linear dependence](@entry_id:149638) on vacant site coverage for adsorption is a hallmark of single-site, non-dissociative mechanisms.

In stark contrast, **[dissociative adsorption](@entry_id:199140)** involves the breaking of one or more chemical bonds within the impinging molecule, resulting in two or more fragments that bind to separate surface sites. For a diatomic molecule $A_2$, the process typically requires two adjacent vacant sites and is represented as:

$$ A_2(g) + 2* \rightleftharpoons 2A^* $$

Here, one gas-phase molecule $A_2$ consumes two vacant sites to produce two individually adsorbed atoms, $A^*$. The kinetic consequences are profound. The forward reaction, adsorption, is an [elementary step](@entry_id:182121) involving one gas-phase molecule and two surface sites. Its rate is therefore proportional to the [partial pressure](@entry_id:143994) $p_{A_2}$ and the probability of finding two vacant sites available for the reaction. In the simplest [mean-field approximation](@entry_id:144121), where the states of adjacent sites are considered statistically independent, this probability is $\theta_* \times \theta_* = \theta_*^2$. The rate of [dissociative adsorption](@entry_id:199140), $r_{\text{ads},A_2}$, is therefore second-order in vacant site coverage [@problem_id:2639993]:

$$ r_{\text{ads},A_2} = k_{a}' p_{A_2} \theta_*^2 $$

The reverse process, **associative desorption**, involves the recombination of two adsorbed atoms $A^*$ to reform a gas-phase molecule $A_2$. This is a [bimolecular reaction](@entry_id:142883) with respect to the surface species. Its rate, $r_{\text{des},A_2}$, is proportional to the probability of two $A^*$ species finding each other, which in the mean-field model is proportional to the square of the atomic coverage, $\theta_A^2$:

$$ r_{\text{des},A_2} = k_{d}' \theta_A^2 $$

This quadratic dependence on both $\theta_*$ (for [adsorption](@entry_id:143659)) and $\theta_A$ (for desorption) is the essential kinetic signature of [dissociative adsorption](@entry_id:199140) of a [diatomic molecule](@entry_id:194513).

### Thermodynamic Landscape: Chemisorption, Physisorption, and Equilibrium

The kinetic formalism is deeply connected to the underlying thermodynamics of surface bonding. Adsorption can be broadly classified into two regimes based on the strength and nature of the surface-adsorbate interaction.

**Physisorption** is a process mediated by weak, non-specific van der Waals forces, analogous to [intermolecular forces](@entry_id:141785) in [non-ideal gases](@entry_id:146577). It does not involve significant electronic rearrangement or the formation of chemical bonds. Consequently, the enthalpy of physisorption is small and exothermic, typically in the range of 5–40 kJ/mol. Molecules remain intact in [physisorption](@entry_id:153189).

**Chemisorption**, on the other hand, involves the formation of true chemical bonds between the adsorbate and the surface, characterized by significant orbital overlap and electron density rearrangement. This results in a much stronger interaction, with typical adsorption enthalpies being large and exothermic, ranging from tens to hundreds of kJ/mol.

Dissociative [adsorption](@entry_id:143659) is, by its very nature, a form of chemisorption. The process involves breaking an existing chemical bond (e.g., the O–O bond in $\mathrm{O_2}$) and forming new, strong chemical bonds between the resulting fragments and the surface (e.g., metal–O bonds). Several experimental signatures confirm this classification [@problem_id:2640019]:
1.  **Large Heat of Adsorption:** The measured [heat of adsorption](@entry_id:199302) for dissociative processes is typically large (e.g., $\approx 180$ kJ/mol for $\mathrm{X_2}$ dissociation), consistent with chemical [bond formation](@entry_id:149227).
2.  **Activation Barrier:** Unlike many physisorption processes, dissociative [chemisorption](@entry_id:149998) is often an **activated process**, meaning it must overcome an energy barrier. This manifests as a [sticking probability](@entry_id:192174) that increases with temperature.
3.  **High-Temperature Desorption:** The reverse process, associative desorption, requires breaking strong [chemisorption](@entry_id:149998) bonds. This translates to a high activation energy for desorption, observed as a high-temperature peak in [temperature-programmed desorption](@entry_id:198913) (TPD) experiments.

The [equilibrium state](@entry_id:270364) of these [adsorption](@entry_id:143659) processes reveals further crucial distinctions. The [thermodynamic equilibrium](@entry_id:141660) constants, $K_{\text{mol}}$ and $K_{\text{diss}}$, can be defined from the elementary steps. In the low-coverage limit ($\theta_* \approx 1$), the relationship between surface coverage and gas pressure is markedly different for the two mechanisms [@problem_id:2639994].

For [non-dissociative adsorption](@entry_id:195696), the coverage is directly proportional to the pressure:
$$ K_{\text{mol}} = \frac{\theta_{A_2}}{p_{A_2}\theta_*} \implies \theta_{A_2} \approx K_{\text{mol}} \cdot p_{A_2} $$
(assuming [standard state](@entry_id:145000) pressure $P^\circ=1$).

For [dissociative adsorption](@entry_id:199140), the coverage is proportional to the square root of the pressure:
$$ K_{\text{diss}} = \frac{\theta_{A}^2}{p_{A_2}\theta_*^2} \implies \theta_{A} \approx \sqrt{K_{\text{diss}} \cdot p_{A_2}} $$
This difference in pressure dependence is a fundamental tool for experimentally distinguishing between the two modes.

The temperature dependence of these equilibria is governed by the van't Hoff equation, $\ln K = -\frac{\Delta H^\circ}{RT} + \frac{\Delta S^\circ}{R}$. Adsorption from a three-dimensional gas to a two-dimensional surface always involves a significant loss of translational and rotational entropy, making $\Delta S^\circ$ negative. Dissociative adsorption is often associated with a larger entropy loss than molecular adsorption ($\Delta S_{\text{diss}}^{\circ}  \Delta S_{\text{mol}}^{\circ}  0$), as it involves the immobilization of two particles on the surface and the consumption of two sites. This more negative entropy makes the equilibrium constant for [dissociation](@entry_id:144265), $K_{\text{diss}}$, smaller than $K_{\text{mol}}$ at any given temperature, assuming similar enthalpies. Furthermore, the temperature dependence of the coverage, when plotted as $\ln \theta$ versus $1/T$, yields an apparent activation energy. For the same standard [enthalpy of adsorption](@entry_id:171774) per mole of gas, $\Delta H^\circ$, the slope for [dissociative adsorption](@entry_id:199140) ($\propto -\Delta H^\circ/(2R)$) will have half the magnitude of the slope for molecular adsorption ($\propto -\Delta H^\circ/R$) [@problem_id:2639994].

### Kinetic Models of Dissociative Adsorption

To build a more detailed picture, we refine our understanding of the adsorption rate.

#### Sticking Probability and Site Availability

The rate of [adsorption](@entry_id:143659) is often discussed in terms of a **[sticking probability](@entry_id:192174)**, $S$, defined as the probability that a molecule impinging on the surface adsorbs. For [dissociative adsorption](@entry_id:199140) of $A_2$, this probability depends on two factors: the intrinsic reactivity of the molecule with the site, and the probability of the molecule encountering a suitable site (a pair of adjacent vacant sites).

The initial [sticking probability](@entry_id:192174), $S_0(\theta_*)$, can be expressed as a product of an intrinsic dissociation probability, $s_{\text{diss}}$, and the probability of finding a vacant nearest-neighbor pair, $P_{\text{nn}}^{**}$ [@problem_id:2639997]:

$$ S_0(\theta_*) = s_{\text{diss}} \cdot P_{\text{nn}}^{**} $$

In the random mixing or mean-field approximation, $P_{\text{nn}}^{**}$ is simply $\theta_*^2$. This provides a direct physical interpretation for the $\theta_*^2$ term in the rate law.

#### Macroscopic Rate Laws and Site Blocking

We can formalize a macroscopic [rate law](@entry_id:141492) for the change in coverage, $\theta$. Consider a surface lattice with [coordination number](@entry_id:143221) $z$ (each site has $z$ neighbors). The total number of nearest-neighbor pairs is $Nz/2$, where $N$ is the total number of sites. The number of vacant pairs, $N_{**}$, in the mean-field model is $(Nz/2)(1-\theta)^2$. If the rate constant per vacant pair is $k_{\text{diss}}$, the total number of adsorption events per unit time is $k_{\text{diss}} N_{**}$. Since each event fills two sites, the rate of increase of occupied sites is $2k_{\text{diss}}N_{**}$. The rate of change of coverage, $d\theta/dt$, is then [@problem_id:2639995]:

$$ \frac{d\theta}{dt} = \frac{1}{N} \frac{d(N\theta)}{dt} = \frac{2k_{\text{diss}}N_{**}}{N} = \frac{2k_{\text{diss}}}{N} \left( \frac{Nz}{2} (1-\theta)^2 \right) = k_{\text{diss}} z (1-\theta)^2 $$
This derivation rigorously confirms the quadratic dependence on the vacant site fraction, $(1-\theta) \equiv \theta_*$.

A direct and important consequence of this two-site requirement is the phenomenon of **site blocking**. If the surface is partially covered by an inert "spectator" species $B$ at a coverage $\theta_B$, the fraction of available sites is $\theta_* = 1 - \theta_B$. The rate of [dissociative adsorption](@entry_id:199140) of $A_2$ will be proportional to $\theta_*^2 = (1 - \theta_B)^2$. The rate is thus not just linearly inhibited, but quadratically. For example, to reduce the initial dissociation rate to 10% of its value on a clean surface, we require $(1 - \theta_B)^2 = 0.1$, which corresponds to a blocker coverage of $\theta_B = 1 - \sqrt{0.1} \approx 0.6838$. This demonstrates that a substantial fraction of the surface must be blocked to achieve strong inhibition, but the effect is more potent than for a single-site process, which would scale as $(1-\theta_B)$ [@problem_id:2639982].

### Beyond Ideal Models: Precursors and Correlations

The simple Langmuirian picture, while foundational, is often insufficient to describe real systems. Two key refinements are precursor-mediated mechanisms and spatial correlations.

#### Precursor-Mediated Adsorption

In many cases, [adsorption](@entry_id:143659) is not a single direct step from the gas phase to the final chemisorbed state. Instead, a molecule may first trap into a weakly bound, mobile **precursor state**. This is typically a physisorbed state from which the molecule can either desorb back to the gas phase or diffuse across the surface to find a suitable site for conversion into a more strongly bound chemisorbed state.

This competition between desorption ($k_d$) and reaction ($k_r$) from the precursor state leads to a characteristic temperature dependence for the sticking coefficient, $S_0(T)$. At low temperatures, the desorption rate is slow, and most precursors have time to find a reaction site, leading to a high [sticking probability](@entry_id:192174). As temperature increases, the desorption rate increases, causing more precursors to leave the surface before they can react, thus decreasing $S_0(T)$. However, if the conversion to the chemisorbed state is itself activated, its rate constant $k_r(T)$ will increase with temperature.

The hallmark of a precursor-mediated pathway is often a non-monotonic sticking coefficient that first increases with temperature (as the activated reaction step speeds up) and then decreases at higher temperatures (as desorption becomes dominant). In contrast, a simple, direct activated [adsorption](@entry_id:143659) process typically shows a monotonically increasing [sticking probability](@entry_id:192174) with temperature. Temperature-programmed sticking measurements are a powerful experimental tool for distinguishing these mechanisms [@problem_id:2640025].

#### Spatial Correlations

The mean-field assumption that vacant sites are randomly distributed ($\theta_*^2$ dependence) breaks down when lateral interactions between adsorbates are significant. Adsorbate-adsorbate repulsion will tend to space adsorbates apart, making vacancies more likely to be isolated. Conversely, attractive interactions will cause adsorbates to form islands, leading to clustering of vacancies.

This deviation from random mixing is quantified by a **pair-correlation factor**, $g_{**}$, defined as the ratio of the true probability of finding a vacant nearest-neighbor pair, $X_{**}$, to its [mean-field approximation](@entry_id:144121), $\theta_*^2$ [@problem_id:2640001]:

$$ g_{**} \equiv \frac{X_{**}}{\theta_*^2} $$

The corrected [dissociative adsorption](@entry_id:199140) rate is then:

$$ r_{\text{ads}} = k_{\text{ads}} p_{D_2} \theta_*^2 g_{**} $$

The physical meaning of $g_{**}$ is clear:
-   If vacancies cluster (due to attractive forces between adsorbates), there are more `**` pairs than predicted by random statistics. In this case, $g_{**}  1$, and the rate of [dissociative adsorption](@entry_id:199140) is enhanced.
-   If vacancies repel each other (due to repulsive forces between adsorbates), there are fewer `**` pairs. In this case, $g_{**}  1$, and the rate is suppressed.
-   If the arrangement is random, $g_{**} = 1$, and we recover the mean-field model.

A consistent probabilistic representation for this factor is $g_{**} = P(*|*)/\theta_*$, where $P(*|*)$ is the [conditional probability](@entry_id:151013) that a site is vacant given that its neighbor is vacant. This correction is specific to multi-site processes like [dissociative adsorption](@entry_id:199140); a single-site molecular [adsorption](@entry_id:143659) rate remains proportional to the single-site probability $\theta_*$ and does not involve $g_{**}$ [@problem_id:2640001].

### Probing Adsorption Mechanisms

A variety of advanced experimental and theoretical tools allow us to probe the intricate details of these adsorption mechanisms.

#### Kinetic Isotope Effect (KIE)

The **[kinetic isotope effect](@entry_id:143344) (KIE)**, the change in reaction rate upon [isotopic substitution](@entry_id:174631), is a powerful probe of bond-breaking in the [rate-determining step](@entry_id:137729). For the [dissociative adsorption](@entry_id:199140) of $\mathrm{H}_2$ versus $\mathrm{D}_2$, the effect arises primarily from differences in vibrational zero-point energy (ZPE).

The lighter [isotopologue](@entry_id:178073), $\mathrm{H}_2$, has a higher vibrational frequency and thus a higher ZPE than $\mathrm{D}_2$. In the transition state for [dissociation](@entry_id:144265), the H-H (or D-D) bond is elongated and weakened, leading to a lower [vibrational frequency](@entry_id:266554) and a correspondingly smaller ZPE difference between the isotopologues. Consequently, the ZPE of $\mathrm{H}_2$ drops more significantly than that of $\mathrm{D}_2$ upon moving from the initial state to the transition state. This results in a lower effective [activation barrier](@entry_id:746233) for $\mathrm{H}_2$ dissociation, causing it to react faster. This is termed a "normal" KIE ($k_H/k_D  1$). The magnitude of the KIE can be calculated using [transition state theory](@entry_id:138947) if the [vibrational frequencies](@entry_id:199185) of the initial and transition states are known [@problem_id:2639998]. For example, given gas-phase and transition-state stretching frequencies for $\mathrm{H}_2$ of $4400 \, \text{cm}^{-1}$ and $1500 \, \text{cm}^{-1}$ respectively, the KIE ratio $k_{\mathrm{H}_2}/k_{\mathrm{D}_2}$ at $300 \, \text{K}$ can be calculated as:

$$ \frac{k_{\mathrm{H}_2}}{k_{\mathrm{D}_2}} = \exp\left[ \frac{\Delta E_{\mathrm{ZPE}}^{\ddagger}(\mathrm{D}_2) - \Delta E_{\mathrm{ZPE}}^{\ddagger}(\mathrm{H}_2)}{k_B T} \right] = \exp\left[ \frac{h c}{2 k_B T} \left(1 - \frac{1}{\sqrt{2}}\right) (\tilde{\nu}_{g}^{\mathrm{H}_{2}} - \tilde{\nu}_{\ddagger}^{\mathrm{H}_{2}}) \right] \approx 7.67 $$

This large KIE is strong evidence for H-H bond cleavage being involved in the rate-limiting step of the adsorption process.

#### Electronic Structure and Reactivity Trends

Ultimately, the propensity for a surface to favor dissociative over molecular [adsorption](@entry_id:143659) is rooted in its electronic structure. The **[d-band model](@entry_id:146526)**, pioneered by Hammer and Nørskov, provides a powerful framework for understanding reactivity trends across [transition metals](@entry_id:138229). This model posits that the strength of chemisorption for electronegative species like oxygen is primarily determined by the energy of the metal's d-electron states, summarized by the **[d-band center](@entry_id:275172)** ($\varepsilon_d$) relative to the Fermi level.

The core principle is that a higher $\varepsilon_d$ (i.e., closer to the Fermi level) leads to stronger [hybridization](@entry_id:145080) with the adsorbate's orbitals. This strengthens the resulting metal-adsorbate bonds. For $\mathrm{O}_2$ adsorption, a higher $\varepsilon_d$ more effectively stabilizes the atomic oxygen products ($2\mathrm{O}^*$) and the transition state leading to them. Therefore, metals with higher d-band centers are more prone to dissociate $\mathrm{O}_2$.

This model successfully rationalizes observed reactivity trends across the late transition metals. The [d-band center](@entry_id:275172) becomes progressively lower (more negative) moving from left to right and down the periodic table (with exceptions). For example, the approximate ordering of $\varepsilon_d$ for (111) surfaces is $\mathrm{Ni}  \mathrm{Pd} \approx \mathrm{Pt}  \mathrm{Cu}  \mathrm{Au} \approx \mathrm{Ag}$. Correspondingly, the propensity for $\mathrm{O}_2$ [dissociative adsorption](@entry_id:199140) follows the same trend: Ni is highly reactive, Pd and Pt are moderately reactive, and Cu, Ag, and Au are much less reactive, often favoring weak molecular adsorption at low temperatures [@problem_id:2639992].

The [d-band model](@entry_id:146526) also explains how surface properties can be tuned. For instance, applying tensile strain to a metal surface tends to narrow the d-band, which raises its center $\varepsilon_d$. This, in turn, enhances the dissociative propensity, providing a key principle for [catalyst design](@entry_id:155343) [@problem_id:2639992].