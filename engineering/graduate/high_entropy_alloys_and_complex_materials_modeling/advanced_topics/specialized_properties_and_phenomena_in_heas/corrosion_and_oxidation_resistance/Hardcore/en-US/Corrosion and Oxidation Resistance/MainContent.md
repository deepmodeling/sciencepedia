## Introduction
High-entropy alloys (HEAs) represent a paradigm shift in [materials design](@entry_id:160450), offering the potential for unprecedented performance in extreme environments where conventional alloys falter. A critical aspect of their viability is their ability to resist degradation from [high-temperature oxidation](@entry_id:197667) and aqueous corrosion. However, translating this potential into reliable engineering materials requires a deep understanding of the mechanisms governing their surface stability. This article addresses the knowledge gap by providing a graduate-level foundation in the theoretical principles that connect the unique features of HEAs—such as high [configurational entropy](@entry_id:147820) and chemical complexity—to their environmental resilience.

This structured journey will equip you with the knowledge to analyze and design next-generation corrosion-resistant alloys. In the first chapter, **Principles and Mechanisms**, you will explore the fundamental thermodynamic and kinetic drivers of protective scale formation, [passivation](@entry_id:148423), and failure. The subsequent chapter, **Applications and Interdisciplinary Connections**, bridges this theory with practice, demonstrating how these concepts are applied to solve real-world challenges in aerospace, nuclear energy, and even biomedical fields. Finally, the **Hands-On Practices** chapter provides computational problems to solidify your understanding of these complex interactions. We begin our exploration by dissecting the core scientific principles that dictate how these advanced materials withstand aggressive environments.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms governing the corrosion and oxidation resistance of high-entropy alloys (HEAs). Building upon the introductory concepts, we will explore the intricate interplay of thermodynamics, kinetics, and microstructure that dictates the performance of these complex materials in aggressive environments. Our inquiry will span from [high-temperature oxidation](@entry_id:197667) to aqueous corrosion, elucidating how the unique characteristics of HEAs, such as high [configurational entropy](@entry_id:147820) and chemical complexity, influence their degradation pathways.

### The Indirect Role of Configurational Entropy

A defining characteristic of HEAs is their high configurational entropy of mixing, which for an ideal $N$-component solution is given by the Boltzmann equation:

$$
S_{\mathrm{conf}} = -R \sum_{i=1}^{N} x_{i} \ln x_{i}
$$

where $R$ is the [universal gas constant](@entry_id:136843) and $x_i$ is the mole fraction of element $i$. This term contributes significantly to the Gibbs free energy of mixing, $\Delta G_{\mathrm{mix}} = \Delta H_{\mathrm{mix}} - T S_{\mathrm{conf}}$, where $\Delta H_{\mathrm{mix}}$ is the enthalpy of mixing and $T$ is the [absolute temperature](@entry_id:144687). A large, positive $S_{\mathrm{conf}}$ makes the entropic term $-T S_{\mathrm{conf}}$ strongly negative, which can overcome a positive or slightly negative $\Delta H_{\mathrm{mix}}$ to favor the formation of a single-phase [solid solution](@entry_id:157599) over competing [intermetallic compounds](@entry_id:157933) or phase-separated microstructures.

It is crucial to understand that the influence of [configurational entropy](@entry_id:147820) on oxidation resistance is fundamentally **indirect**. High entropy does not, for example, directly alter the intrinsic [thermodynamic stability](@entry_id:142877) of an oxide like $\mathrm{Al_2O_3}$ . Instead, its primary effect is thermodynamic stabilization of the metallic alloy phase itself. This [phase stability](@entry_id:172436) has profound consequences for oxidation behavior. By promoting a single-phase [solid solution](@entry_id:157599), high entropy suppresses the microchemical partitioning of elements. If key protective elements like aluminum or chromium were to precipitate into [intermetallic phases](@entry_id:1126621), the surrounding matrix would become depleted. This would hinder the formation of a continuous, protective oxide scale at the surface, leading to inferior oxidation resistance. Thus, by maintaining a uniform distribution of scale-forming elements, high configurational entropy ensures these elements are available at the surface to react with the environment .

A secondary, kinetic consequence often attributed to the chemical complexity stabilized by high entropy is the "sluggish diffusion" effect. The chemically disordered nature of the HEA lattice presents a diffusing atom with a complex potential energy landscape, featuring a wide distribution of energy barriers for atomic jumps. This complexity may lead to a higher effective [activation energy for diffusion](@entry_id:161603), $Q_{\mathrm{eff}}$, thereby reducing the diffusion coefficient $D = D_{0} \exp(-Q / k_{\mathrm{B}} T)$. Since the growth of a protective scale is often limited by the diffusion of cations from the alloy to the surface, a reduction in diffusivity can slow the overall oxidation rate .

However, one must not overstate the role of entropy. Oxidation resistance is primarily dictated by the alloy's composition—specifically, the type and concentration of protective scale-forming elements like Al and Cr. An off-equiatomic alloy with a high concentration of Al will generally outperform an equiatomic alloy with a lower Al content, even though the latter possesses a higher configurational entropy .

### High-Temperature Oxidation

High-temperature oxidation is a critical degradation mechanism for materials in energy, aerospace, and chemical processing applications. For HEAs, the central challenge is to promote the [selective oxidation](@entry_id:194397) of one or two elements to form a slow-growing, dense, and adherent oxide scale.

#### Thermodynamic Driving Force for Oxidation

The question of which element within an HEA will oxidize is governed by thermodynamics. Consider the formation of an oxide $\mathrm{M_aO_b}$ from an element $\mathrm{M}$ within the alloy. The reaction is $a\mathrm{M}(\mathrm{alloy}) + \frac{b}{2}\mathrm{O}_2(\mathrm{g}) \rightarrow \mathrm{M_aO_b}(\mathrm{s})$. The Gibbs free energy change for this reaction, $\Delta G_{\mathrm{rxn}}$, determines its spontaneity and is given by:

$$
\Delta G_{\mathrm{rxn}} = \Delta G_{f}^{\circ} - a RT \ln a_{\mathrm{M}} - \frac{b}{2} RT \ln(p_{\mathrm{O}_2}/p^{\circ})
$$

where $\Delta G_{f}^{\circ}$ is the standard Gibbs free energy of formation of the oxide from the pure element, $a_{\mathrm{M}}$ is the thermodynamic **activity** of element $\mathrm{M}$ in the alloy, and $p_{\mathrm{O}_2}/p^{\circ}$ is the dimensionless [oxygen partial pressure](@entry_id:171160). The activity is related to the [mole fraction](@entry_id:145460) $x_{\mathrm{M}}$ via the activity coefficient $\gamma_{\mathrm{M}}$: $a_{\mathrm{M}} = \gamma_{\mathrm{M}} x_{\mathrm{M}}$. In a [non-ideal solution](@entry_id:147368) like an HEA, $\gamma_{\mathrm{M}}$ is generally not equal to one . This equation shows that reducing the activity of a metal in the alloy (e.g., through dilution or unfavorable chemical interactions) makes its oxidation less thermodynamically favorable (i.e., makes $\Delta G_{\mathrm{rxn}}$ less negative).

Selective oxidation of a more reactive element (e.g., Al) over a less reactive one (e.g., Cr) occurs when the reaction to form its oxide is thermodynamically more favorable, meaning $\Delta G_{\mathrm{Al-oxide}} \lt \Delta G_{\mathrm{Cr-oxide}}$. At a fixed temperature and oxygen pressure, this condition simplifies to a criterion based on the standard formation energies and the activities of the elements in the alloy .

#### Quantitative Criteria for Selective Oxidation

For each oxidation reaction, we can define an **equilibrium [oxygen partial pressure](@entry_id:171160)**, $p_{\mathrm{O}_2,eq}$, at which the alloy, the oxide, and the gas phase are in equilibrium ($\Delta G_{\mathrm{rxn}} = 0$). For the formation of $\mathrm{M_2O_3}$, this pressure is given by:

$$
p_{\mathrm{O}_2,eq} = \left( \frac{1}{a_{\mathrm{M}}^2} \exp\left(\frac{\Delta G^{\circ}_{\mathrm{M_2O_3}}}{RT}\right) \right)^{2/3}
$$

An element $\mathrm{M}$ will oxidize only if the ambient [oxygen partial pressure](@entry_id:171160) $p_{\mathrm{O}_2}$ is greater than its corresponding $p_{\mathrm{O}_2,eq}$. Therefore, the condition for the [selective oxidation](@entry_id:194397) of aluminum over chromium is that the ambient oxygen pressure must lie within a specific window:

$$
p_{\mathrm{O}_2,eq,\mathrm{Al}}  p_{\mathrm{O}_2}  p_{\mathrm{O}_2,eq,\mathrm{Cr}}
$$

To illustrate this, consider a hypothetical five-component HEA at $1200\ \mathrm{K}$ containing Al and Cr. To calculate the activities $a_{\mathrm{Al}}$ and $a_{\mathrm{Cr}}$, we can employ a model such as the Wagner formalism, where the activity coefficient is related to first-order [interaction parameters](@entry_id:750714), $\epsilon_{ij}$: $\ln\gamma_i = \sum_{j}\epsilon_{ij} x_j$. By first calculating the activities of the elements based on the alloy composition and the given [interaction parameters](@entry_id:750714), one can then compute the equilibrium oxygen pressure for chromium, $p_{\mathrm{O}_2,eq,\mathrm{Cr}}$. This value represents the highest [oxygen partial pressure](@entry_id:171160) at which aluminum can be selectively oxidized without also forming a chromium oxide scale. Such calculations are critical for designing alloys and controlling processing atmospheres to achieve the desired protective oxide .

#### The Structure and Protectiveness of Oxide Scales

The thermodynamic preference for an oxide to form does not guarantee its protectiveness. The mechanical integrity of the scale is equally important. A classic, first-order metric for predicting this is the **Pilling–Bedworth Ratio (PBR)**, defined as the ratio of the volume of oxide formed to the volume of metal consumed:

$$
\mathrm{PBR} = \frac{V_{\mathrm{oxide}}}{V_{\mathrm{metal}}}
$$

For a reaction $a\mathrm{M} + \frac{b}{2}\mathrm{O}_2 \rightarrow \mathrm{M_aO_b}$, the PBR can be expressed in terms of molar masses ($M$) and densities ($\rho$):

$$
\mathrm{PBR} = \frac{M_{\mathrm{M}_a\mathrm{O}_b} \cdot \rho_{\mathrm{M}}}{a \cdot M_{\mathrm{M}} \cdot \rho_{\mathrm{M}_a\mathrm{O}_b}}
$$

The magnitude of the PBR predicts the stress state and morphology of the scale :
-   **$PBR  1$**: The oxide volume is insufficient to cover the metal surface. This induces tensile stresses in the scale, leading to cracking and porosity, rendering it non-protective.
-   **$1  PBR  2.5$**: The oxide volume is larger than the consumed metal, inducing compressive stresses. For moderate values, these stresses can be accommodated, leading to a dense, adherent, and protective scale. This is the ideal range for protective oxides like $\mathrm{Al_2O_3}$ ($PBR \approx 1.28$) and $\mathrm{Cr_2O_3}$ ($PBR \approx 2.02$) .
-   **$PBR > 2.5$**: The compressive stresses become excessive, often leading to [buckling](@entry_id:162815), cracking, and spallation (flaking off) of the scale, which compromises its protective function.

#### Kinetic Mechanisms of Scale Growth: Transport Through Oxides

Once a continuous scale has formed, its growth rate is typically controlled by the diffusion of ions (cations outward, [anions](@entry_id:166728) inward) and electrons through the oxide layer. This transport is mediated by **point defects** in the oxide's crystal lattice. The standard language for describing these defects is **Kröger-Vink notation**, written as $X_Y^q$, where $X$ is the species (an atom or a vacancy $V$), $Y$ is the lattice site it occupies, and $q$ is its [effective charge](@entry_id:190611) relative to the perfect lattice. A positive [effective charge](@entry_id:190611) is denoted by a dot ($\bullet$), a negative charge by a prime ($'$), and neutrality by a cross ($\times$).

For example, in oxides like $\mathrm{Al_2O_3}$ and $\mathrm{Cr_2O_3}$, which are common protective scales on HEAs, several key defects can exist :
-   An **oxygen vacancy**, $V_{\mathrm{O}}$, has an [effective charge](@entry_id:190611) of $+2$ because it occupies a site that would normally hold an $\mathrm{O}^{2-}$ ion. Its notation is $V_{\mathrm{O}}^{\bullet\bullet}$.
-   A **cation vacancy** on an aluminum site, $V_{\mathrm{Al}}$, has an effective charge of $-3$ and is written $V_{\mathrm{Al}}^{'''}$.
-   Defect formation must conserve charge. For example, under reducing conditions, oxygen can leave the lattice, forming a vacancy. The positive charge can be compensated by free electrons, $e'$:
    $$ O_{\mathrm{O}}^{\times} \rightleftharpoons \frac{1}{2} \mathrm{O}_2(\mathrm{g}) + V_{\mathrm{O}}^{\bullet\bullet} + 2 e' $$
-   Stoichiometric clusters of vacancies, known as **Schottky defects**, can also form while maintaining charge neutrality, for instance:
    $$ \mathrm{nil} \rightleftharpoons 2 V_{\mathrm{Al}}^{'''} + 3 V_{\mathrm{O}}^{\bullet\bullet} $$

The concentration of these defects, which is a function of temperature and [oxygen partial pressure](@entry_id:171160), directly controls the kinetics of scale growth. Consider the case where [oxygen transport](@entry_id:138803) occurs via vacancies. The effective diffusivity of oxygen, $D_{\mathrm{eff}}$, is the product of the vacancy diffusivity, $D_V$, and the vacancy site fraction, $[V_{\mathrm{O}}^{\bullet\bullet}]$. By applying the law of [mass action](@entry_id:194892) to the defect [formation reaction](@entry_id:147837) and imposing charge neutrality, we can derive the dependence of the [vacancy concentration](@entry_id:1133675) on $p_{\mathrm{O}_2}$. For the reaction above, where electrons are the main compensating species ($2[V_O^{\bullet\bullet}] = [e']$), the [vacancy concentration](@entry_id:1133675) scales as $[V_O^{\bullet\bullet}] \propto (p_{\mathrm{O_{2}}})^{-1/6}$. Combining this with a random-walk model for [vacancy diffusion](@entry_id:144259), the effective oxygen diffusivity can be expressed as a function of fundamental energetic parameters, temperature, and oxygen pressure . This linkage between [defect thermodynamics](@entry_id:184020) and [transport kinetics](@entry_id:173334) is central to modeling and predicting oxidation rates.

#### Microstructural Influences: Grain Boundary Oxidation

The idealized models above assume a perfect single crystal. Real engineering alloys are polycrystalline, and their **grain boundaries** represent a critical microstructural feature. Grain boundaries are structurally disordered regions with higher free energy and excess free volume compared to the crystalline bulk. This disorder lowers the activation energy for atomic motion, turning grain boundaries into **fast diffusion paths**, or "short-circuits," for both metal and oxygen atoms .

This enhanced transport leads to **grain boundary oxidation**, where oxide penetration is much faster along boundaries than through the bulk grains. We can model this by considering [one-dimensional diffusion](@entry_id:181320) along a [grain boundary](@entry_id:196965) normal to the surface, governed by Fick's second law with a high grain boundary diffusivity, $D_{\mathrm{gb}}$. For a semi-infinite medium with a constant surface concentration $c_s$, the oxygen concentration profile along the boundary is given by the [complementary error function](@entry_id:165575):

$$
c(x,t) = c_{s} \operatorname{erfc}\left( \frac{x}{2 \sqrt{D_{\mathrm{gb}} t}} \right)
$$

From this, one can define an oxidation front as the position where the oxygen concentration reaches a critical threshold $c^*$ for oxide nucleation. The [instantaneous velocity](@entry_id:167797) of this front, $v(t) = \frac{dx_f}{dt}$, can be derived and shows a $t^{-1/2}$ dependence, characteristic of diffusion-controlled processes. This preferential oxidation along grain boundaries can compromise the mechanical integrity of the material, even if the bulk grains are well-protected .

### Aqueous Corrosion and Passivation

In aqueous environments, corrosion is an electrochemical process involving anodic (metal dissolution) and cathodic (e.g., oxygen or hydrogen reduction) reactions.

#### Electrochemical Principles

The thermodynamic tendency of a metal to corrode in an electrolyte is measured by its **electrode potential**, $E$. For a metal dissolution [half-reaction](@entry_id:176405) $\mathrm{M}^{z+} + z\mathrm{e}^{-} \rightleftharpoons \mathrm{M}(\mathrm{s})$, the equilibrium potential under non-standard conditions is given by the **Nernst equation**:

$$
E = E^{\circ} - \frac{RT}{zF} \ln \left( \frac{a_{\mathrm{M}}}{a_{\mathrm{M}^{z+}}} \right) = E^{\circ} + \frac{RT}{zF} \ln a_{\mathrm{M}^{z+}}
$$

where $E^{\circ}$ is the [standard reduction potential](@entry_id:144699), $F$ is the Faraday constant, and $a_{\mathrm{M}^{z+}}$ is the activity of the metal ion in solution (activity of the pure solid metal $a_{\mathrm{M}}$ is unity). By calculating the Nernst potentials for the constituent elements of an HEA under specific conditions (e.g., neutral, aerated water with very low dissolved ion concentration, $a_{\mathrm{M}^{z+}} \approx 10^{-6}$), we can rank their thermodynamic susceptibility to corrosion. Elements with more negative potentials (e.g., Al, Cr, Fe) are more active and have a stronger thermodynamic driving force to dissolve compared to more noble elements (e.g., Ni) . Corrosion occurs when the potential of the alloy is lower than the potential of the cathodic reaction, such as the reduction of dissolved oxygen.

#### Passivity: The Key to Corrosion Resistance

Despite a strong thermodynamic driving force for dissolution, many alloys, including HEAs containing Cr and Al, exhibit excellent [corrosion resistance](@entry_id:183133) due to **passivity**. Passivity is an electrochemical state in which the rate of anodic dissolution is suppressed to a very low value, typically over a wide range of potentials. This is caused by the formation of a very thin (a few nanometers), tenacious, and electronically insulating surface layer, known as a **[passive film](@entry_id:273228)** .

An effective [passive film](@entry_id:273228) is a compact, dense, and low-porosity oxide or hydroxide layer that acts as a robust barrier to both ionic and electronic transport, thereby kinetically hindering the corrosion process. It is vital to distinguish between two types of passivity:
-   **Thermodynamic Passivity**: This refers to potential-pH conditions (as depicted on a Pourbaix diagram) where a solid oxide/hydroxide is the thermodynamically most stable phase. The system is in its lowest free energy state.
-   **Kinetic Passivity**: This is the more common and practically important form. It describes the state where an alloy exhibits a low [corrosion rate](@entry_id:274545) due to the formation of a metastable [passive film](@entry_id:273228), even under conditions where thermodynamics favors active dissolution (i.e., the dissolved ion is the most stable species). The protectiveness of this film is purely a matter of slow reaction and [transport kinetics](@entry_id:173334) .

The ability of HEAs to form complex, often amorphous or nanocrystalline, single-phase oxide films can enhance the quality of this kinetic barrier, contributing to their notable corrosion resistance.

### Advanced Topics: Coupling of Mechanics and Environment

The interaction between an HEA and its environment can be strongly coupled with its mechanical state, leading to complex failure modes.

#### Stress Corrosion Cracking (SCC)

**Stress Corrosion Cracking (SCC)** is a form of environmentally assisted cracking that results from the synergistic action of three factors: a susceptible material, a specific corrosive environment, and a sustained tensile stress. It is a pernicious failure mode because it can lead to fracture at stress levels far below the material's nominal [yield strength](@entry_id:162154). It is important to distinguish SCC, which is often driven by anodic dissolution at the crack tip, from **[hydrogen embrittlement](@entry_id:197612) (HE)**, a separate mechanism where absorbed atomic hydrogen degrades the material's cohesion or plasticity .

In passive alloys like Cr-containing HEAs, SCC initiation is intimately linked to the breakdown of the [passive film](@entry_id:273228). The mechanism involves a potent chemo-mechanical feedback loop:
1.  **Local Film Breakdown**: The protective [passive film](@entry_id:273228) is breached at a local site, such as a surface defect, inclusion, or slip step. This can be aggravated by aggressive species like chloride ions.
2.  **Stress Concentration**: The applied tensile stress is concentrated at the tip of the resulting micro-notch.
3.  **Stress-Enhanced Dissolution**: The high hydrostatic tensile stress, $\sigma_h$, at the crack tip increases the chemical potential of the metal atoms according to $\mu_i = \mu_i^0 + \Omega_i \sigma_h$, where $\Omega_i$ is the [partial molar volume](@entry_id:143502). This provides an additional thermodynamic driving force for atoms to leave the lattice and dissolve, accelerating anodic dissolution precisely at the crack tip.
4.  **Crack Sharpening and Advance**: This localized dissolution sharpens the crack, which in turn increases the mechanical [stress intensity factor](@entry_id:157604), $K_I$. The crack advances through a repeating cycle of film rupture at the straining tip, followed by dissolution and repassivation. Once $K_I$ exceeds the threshold for [stress corrosion cracking](@entry_id:154970), $K_{\mathrm{ISCC}}$, sustained [crack propagation](@entry_id:160116) occurs .

#### Atomistic Origins: The Role of Short-Range Order (SRO)

On an even more fundamental level, the local atomic arrangements within an HEA can influence surface phenomena that precede oxidation. While often modeled as random solid solutions, many HEAs exhibit **[chemical short-range order](@entry_id:1122353) (SRO)**—a non-random preference for certain types of neighboring atoms. This can be quantified by the Warren-Cowley SRO parameter, $\alpha_{ij}$, where a negative value implies a preference for $i-j$ pairs and a positive value implies avoidance.

SRO directly impacts the **surface segregation** of elements. The enthalpy of segregation for an element depends on its intrinsic surface energy and the energy of the chemical bonds that are broken when it moves from the bulk to the surface. A strong attractive interaction with neighboring atoms in the bulk (negative $\alpha_{ij}$ and favorable interaction energy) will anchor an element, opposing its segregation. Conversely, repulsive interactions can promote segregation. For example, in an Al-containing HEA, Al has a low intrinsic surface energy, which favors its segregation. This tendency can be enhanced or diminished by its SRO with other elements in the alloy .

This surface composition, in turn, dictates the initial stages of oxide nucleation. The [nucleation barrier](@entry_id:141478) for a new phase depends on both the chemical driving force (the Gibbs free energy of oxide formation) and the interfacial energy cost. Surface enrichment of a strong oxide-former like aluminum can be doubly beneficial: not only is the thermodynamic driving force for $\mathrm{Al_2O_3}$ formation very large, but the presence of an Al-rich substrate can also lower the metal-oxide [interfacial energy](@entry_id:198323), $\gamma_{\mathrm{M/Al_2O_3}}$. Both factors work to reduce the nucleation barrier, promoting the rapid formation of a protective alumina layer over competing, less-protective oxides . Understanding these atomistic mechanisms is at the forefront of designing next-generation corrosion-resistant alloys.