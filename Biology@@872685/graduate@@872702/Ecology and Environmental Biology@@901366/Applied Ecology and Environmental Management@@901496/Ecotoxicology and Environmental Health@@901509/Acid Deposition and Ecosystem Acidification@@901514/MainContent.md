## Introduction
Acid deposition, a pervasive consequence of industrial and agricultural emissions, represents a classic example of a cross-boundary environmental problem with far-reaching impacts on natural ecosystems. For decades, the acidification of forests, lakes, and streams has posed a significant threat to [biodiversity](@entry_id:139919) and [ecosystem health](@entry_id:202023), driving a need for a deep, mechanistic understanding of the issue. This article addresses the challenge of connecting atmospheric pollution to tangible ecological harm by providing a holistic scientific framework. In the following chapters, you will embark on a journey from the sky to the soil. "Principles and Mechanisms" will dissect the [atmospheric chemistry](@entry_id:198364) of acid formation and the sequence of biogeochemical buffering reactions within ecosystems that dictate their response. "Applications and Interdisciplinary Connections" will demonstrate how this foundational knowledge is operationalized through monitoring networks, geochemical tracers, ecosystem models, and policy-informing tools like the [critical load](@entry_id:193340) concept. Finally, "Hands-On Practices" will allow you to apply these principles through practical calculations and assessments, solidifying your understanding of this critical environmental issue.

## Principles and Mechanisms

The phenomenon of [ecosystem acidification](@entry_id:192280) is governed by a sequence of interconnected physical, chemical, and biological processes. This chain of events begins with the emission of precursor pollutants, proceeds through atmospheric transformation and transport, and culminates in a suite of biogeochemical and physiological responses within terrestrial and aquatic ecosystems. This chapter systematically dissects these principles and mechanisms, tracing the path of acidifying compounds from their atmospheric origins to their ultimate ecological impacts.

### Atmospheric Formation and Deposition of Acidity

The journey of [acid deposition](@entry_id:202282) begins in the atmosphere, where primary pollutants are transformed into acidic species and then delivered to the Earth's surface. Understanding these atmospheric processes is fundamental to comprehending the patterns and intensity of [ecosystem acidification](@entry_id:192280).

#### Sources and Transformation of Acid Precursors

The principal precursors to [acid deposition](@entry_id:202282) are [sulfur oxides](@entry_id:148614) ($\mathrm{SO_x}$, primarily [sulfur dioxide](@entry_id:149582), $\mathrm{SO_2}$), [nitrogen oxides](@entry_id:150764) ($\mathrm{NO_x}$, a mixture of [nitric oxide](@entry_id:154957), $\mathrm{NO}$, and [nitrogen dioxide](@entry_id:149973), $\mathrm{NO_2}$), and ammonia ($\mathrm{NH_3}$). These compounds are emitted from both natural and anthropogenic sources.

Historically, the dominant anthropogenic source of $\mathrm{SO_2}$ has been the [combustion](@entry_id:146700) of sulfur-containing fossil fuels, especially coal in power plants and industrial facilities. Anthropogenic $\mathrm{NO_x}$ is primarily formed during high-temperature combustion, where atmospheric nitrogen ($\mathrm{N_2}$) is oxidized, with major contributions from vehicle exhaust and [power generation](@entry_id:146388). Agriculture, particularly livestock farming and fertilizer application, is the overwhelming source of anthropogenic $\mathrm{NH_3}$. Natural sources also contribute to the global budget; these include volcanic emissions of $\mathrm{SO_2}$, lightning and soil microbial activity that produce $\mathrm{NO_x}$, and emissions of $\mathrm{NH_3}$ from natural soils and vegetation [@problem_id:2467907]. While natural sources are significant on a global scale, regional "hotspots" of [acid deposition](@entry_id:202282) are typically driven by dense concentrations of anthropogenic sources. In the contemporary era, anthropogenic emissions of $\mathrm{SO_2}$, $\mathrm{NO_x}$, and $\mathrm{NH_3}$ all exceed their natural counterparts, often by a substantial margin.

Once in the atmosphere, these primary pollutants undergo chemical transformation into secondary pollutants, including [sulfuric acid](@entry_id:136594) ($\mathrm{H_2SO_4}$) and [nitric acid](@entry_id:153836) ($\mathrm{HNO_3}$). This conversion can occur through two main types of pathways: gas-phase reactions and aqueous-phase reactions.

**Gas-Phase Oxidation**: During the daytime, the most important oxidant in the troposphere is the highly reactive **[hydroxyl radical](@entry_id:263428)** ($\mathrm{OH}$). It initiates the conversion of $\mathrm{SO_2}$ and $\mathrm{NO_2}$ to acids through the following key reactions:
$$ \mathrm{SO_2} + \mathrm{OH} \cdot \rightarrow \mathrm{HOSO_2} \cdot $$
$$ \mathrm{HOSO_2} \cdot + \mathrm{O_2} \rightarrow \mathrm{SO_3} + \mathrm{HO_2} \cdot $$
$$ \mathrm{SO_3} + \mathrm{H_2O} \rightarrow \mathrm{H_2SO_4} $$
And for [nitrogen dioxide](@entry_id:149973):
$$ \mathrm{NO_2} + \mathrm{OH} \cdot \rightarrow \mathrm{HNO_3} $$
These gas-phase pathways are the primary daytime mechanisms for forming sulfuric and [nitric acid](@entry_id:153836) in clear-air conditions [@problem_id:2467892].

**Aqueous-Phase Oxidation**: Reactions occurring within cloud droplets, fog, or aqueous aerosols are often much faster than gas-phase reactions, making clouds efficient "chemical reactors" for acid formation. Gases must first dissolve in water, a process governed by their solubility, which is described by **Henry's Law** ($C = H \cdot p$, where $C$ is the aqueous concentration, $H$ is the Henry's Law constant, and $p$ is the gas [partial pressure](@entry_id:143994)).

For [sulfur dioxide](@entry_id:149582), dissolution is followed by [acid-base equilibria](@entry_id:145743):
$$ \mathrm{SO_2}(g) + \mathrm{H_2O} \rightleftharpoons \mathrm{SO_2} \cdot \mathrm{H_2O}(aq) $$
$$ \mathrm{SO_2} \cdot \mathrm{H_2O}(aq) \rightleftharpoons \mathrm{H}^+ + \mathrm{HSO_3^-}(aq) \quad (\mathrm{p}K_{a1} \approx 1.9) $$
$$ \mathrm{HSO_3^-}(aq) \rightleftharpoons \mathrm{H}^+ + \mathrm{SO_3^{2-}}(aq) \quad (\mathrm{p}K_{a2} \approx 7.2) $$
The dissolved sulfur(IV) species ($\mathrm{SO_2} \cdot \mathrm{H_2O}$, $\mathrm{HSO_3^-}$, $\mathrm{SO_3^{2-}}$) are then oxidized to sulfur(VI) (sulfate, $\mathrm{SO_4^{2-}}$) by dissolved oxidants. The two most important aqueous-phase oxidants for S(IV) are hydrogen peroxide ($\mathrm{H_2O_2}$) and ozone ($\mathrm{O_3}$).
-   Oxidation by $\mathrm{H_2O_2}$ is rapid and relatively insensitive to pH in the typical cloud pH range of 3 to 6.
-   Oxidation by $\mathrm{O_3}$ is highly pH-dependent; it proceeds much more rapidly with sulfite ($\mathrm{SO_3^{2-}}$) than with bisulfite ($\mathrm{HSO_3^-}$). At the acidic pH values common in polluted clouds (e.g., pH  5), the concentration of $\mathrm{SO_3^{2-}}$ is extremely low, making the $\mathrm{H_2O_2}$ pathway dominant. Consequently, the availability of $\mathrm{H_2O_2}$ can be the limiting factor for in-cloud sulfate production [@problem_id:2467892].

While $\mathrm{NO_x}$ has a lower solubility in water compared to $\mathrm{SO_2}$, some aqueous-phase production of [nitric acid](@entry_id:153836) can occur. However, the most significant pathway for forming nitric acid at night involves the gas-phase oxidation of $\mathrm{NO_2}$ by ozone to form the nitrate radical ($\mathrm{NO_3}$), which then reacts to form dinitrogen pentoxide ($\mathrm{N_2O_5}$). The heterogeneous hydrolysis of $\mathrm{N_2O_5}$ on the surface of aqueous aerosols is a major source of [nitric acid](@entry_id:153836), especially during nighttime hours.
$$ \mathrm{N_2O_5}(g) + \mathrm{H_2O}(l) \rightarrow 2 \mathrm{HNO_3}(aq) $$

#### The Role of Ammonia and Plume Chemistry

Ammonia ($\mathrm{NH_3}$) plays a crucial dual role. As a [weak base](@entry_id:156341), it is the only significant gaseous base in the atmosphere and readily neutralizes sulfuric and nitric acids to form fine particulate matter:
$$ 2 \mathrm{NH_3} + \mathrm{H_2SO_4} \rightarrow (\mathrm{NH_4})_2\mathrm{SO_4}(s, aq) $$
$$ \mathrm{NH_3} + \mathrm{HNO_3} \rightarrow \mathrm{NH_4NO_3}(s, aq) $$
This [neutralization reaction](@entry_id:193771) transforms acidic gases into ammonium salts, which exist as aerosols. In an air mass where ammonia emissions are abundant relative to acid formation rates, virtually all newly formed $\mathrm{H_2SO_4}$ and $\mathrm{HNO_3}$ can be neutralized during transport. This means that the immediate acidity of deposition may be low, with pollutants arriving as ammonium salts rather than free acids [@problem_id:2467907]. However, as we will see, this atmospheric neutralization does not eliminate the potential for [ecosystem acidification](@entry_id:192280).

#### Deposition Mechanisms

The transfer of atmospheric pollutants to ecosystems occurs through three primary mechanisms: wet, dry, and occult deposition.

-   **Wet Deposition** refers to the removal of pollutants by precipitation (rain, snow, sleet, hail). This process includes both **in-cloud scavenging**, where pollutants are incorporated into cloud droplets that then form [precipitation](@entry_id:144409), and **below-cloud scavenging**, where falling hydrometeors collect gases and particles as they descend. Wet deposition is highly efficient for soluble gases like $\mathrm{HNO_3}$ and for aerosol particles like sulfate and nitrate, which act as cloud condensation nuclei.

-   **Dry Deposition** is the direct transfer and uptake of gases and particles onto surfaces (vegetation, soil, water) in the absence of precipitation. This process is governed by a **resistance-in-series** framework, where the overall transfer rate is limited by a combination of aerodynamic resistance ($R_a$, related to turbulence), quasi-[laminar boundary layer](@entry_id:153016) resistance ($R_b$, related to [molecular diffusion](@entry_id:154595) near the surface), and [surface resistance](@entry_id:149810) ($R_c$, related to the chemical and biological reactivity of the surface itself). For a highly reactive and soluble gas like $\mathrm{HNO_3}$, the [surface resistance](@entry_id:149810) is near zero, leading to very rapid dry deposition. For a gas like $\mathrm{SO_2}$, [surface resistance](@entry_id:149810) can be significant and depends on factors like surface wetness and pH. For aerosol particles, dry deposition is strongly dependent on particle size, with intermediate-sized particles (the "accumulation mode," ~0.1-2 µm) having the lowest deposition velocities.

-   **Occult Deposition** involves the direct interception and impaction of cloud or fog droplets onto vegetation. This process is particularly important in high-elevation forests and coastal areas that are frequently immersed in clouds or fog. Because pollutant concentrations in fog and cloud water can be much higher than in rainwater, occult deposition can be a major input of acidity and nutrients to these specific ecosystems.

The relative importance of these deposition pathways varies by compound. For example, the strong acidity and high solubility of $\mathrm{HNO_3}$ make both wet and dry deposition highly efficient removal pathways. For $\mathrm{NH_3}$, its high solubility and reactivity in acidic droplets promote strong wet and occult deposition. Its dry deposition flux can also be large, especially to acidified canopies, though the flux can be bidirectional depending on the [concentration gradient](@entry_id:136633) between the atmosphere and the surface [@problem_id:2467896].

### Ecosystem Impacts: The Biogeochemical Response to Acid Inputs

Once deposited, acidifying compounds initiate a cascade of biogeochemical changes in soils and freshwaters. The ecosystem's response is dictated by its capacity to neutralize the incoming [acidity](@entry_id:137608).

#### Measuring Ecosystem Acidity: pH, Alkalinity, and ANC

To quantify acidification, we use several key metrics, which, while related, are distinct in their definition and measurement.

-   **pH**: Formally, pH is defined as the [negative base](@entry_id:634916)-10 logarithm of the hydrogen ion **activity** ($a_{\mathrm{H}^{+}}$), not its concentration: $pH = -\log_{10}(a_{\mathrm{H}^{+}})$. Potentiometric measurements with a calibrated glass electrode are designed to respond to activity. Accurate pH measurement requires careful [temperature compensation](@entry_id:148868) and calibration with standard [buffers](@entry_id:137243).

-   **Alkalinity**: The theoretical alkalinity of a water sample is a measure of its capacity to neutralize acid. It is rigorously defined based on a proton balance relative to a set of zero-proton-level species (e.g., $\mathrm{H_2O}$, $\mathrm{H_2CO_3^*}$). It represents the net charge excess of proton acceptors (bases) over proton donors (acids). For a typical natural water, it can be expressed as the sum of the concentrations of weak-base [anions](@entry_id:166728):
    $$ \text{Alkalinity} = [\mathrm{HCO_3^-}] + 2[\mathrm{CO_3^{2-}}] + [\mathrm{B(OH)_4^-}] + [\mathrm{HSiO_3^-}] + [\mathrm{A^-}] + [\mathrm{OH^-}] - [\mathrm{H^+}] $$
    where $[\mathrm{A^-}]$ represents the sum of organic acid anions. Alkalinity is operationally measured by an acid titration, typically to an endpoint pH of around 4.5, which corresponds to the conversion of most bicarbonate to [carbonic acid](@entry_id:180409).

-   **Acid Neutralizing Capacity (ANC)**: In the context of acidification, ANC is often defined from a charge balance perspective. Based on the [principle of electroneutrality](@entry_id:139787), the sum of cation charges must equal the sum of anion charges. ANC is defined as the equivalent sum of base cations (non-acidic cations like $\mathrm{Ca^{2+}}$, $\mathrm{Mg^{2+}}$, $\mathrm{Na^+}$, $\mathrm{K^+}$) minus the equivalent sum of strong acid [anions](@entry_id:166728) ($\mathrm{SO_4^{2-}}$, $\mathrm{NO_3^-}$, $\mathrm{Cl^-}$).
    $$ \text{ANC} = \sum [\text{Base Cations}] - \sum [\text{Strong Acid Anions}] $$
    In waters with high concentrations of dissolved organic carbon (DOC), titrated alkalinity can be significantly higher than the ANC calculated from major ions. This difference arises because the [titration](@entry_id:145369) measures the contribution of organic anions, which are not included in the charge balance calculation of ANC [@problem_id:2467872]. Distinguishing between these metrics and understanding the artifacts of different measurement procedures (e.g., open- vs. closed-cell [titration](@entry_id:145369), filtered vs. unfiltered samples) is critical for accurately assessing the acid-base status of an ecosystem [@problem_id:2467872].

#### Soil Acidification and Buffering Mechanisms

Soils possess a natural ability to resist changes in pH, a property known as **[buffering capacity](@entry_id:167128)**. As an ecosystem is subjected to chronic [acid deposition](@entry_id:202282), it consumes its [buffering capacity](@entry_id:167128) in a predictable sequence. This sequence proceeds from the most reactive to the least reactive buffering systems, with each system dominating a specific pH range.

1.  **Carbonate Buffering (pH > 6.2)**: In soils containing free carbonate minerals like [calcite](@entry_id:162944) ($\mathrm{CaCO_3}$), this is the first and most effective line of defense. Added protons are consumed by the dissolution of [calcite](@entry_id:162944):
    $$ \mathrm{CaCO_3}(s) + \mathrm{H}^+ \rightarrow \mathrm{Ca^{2+}} + \mathrm{HCO_3^-} $$
    As long as calcite is present, this reaction will hold the soil pH in the neutral to alkaline range (typically pH 6.2-8.4). Soils derived from limestone or calcareous parent material have immense [buffering capacity](@entry_id:167128) and are largely insensitive to [acid deposition](@entry_id:202282).

2.  **Cation Exchange Buffering (pH ≈ 5.0 - 6.2)**: Once carbonates are depleted, the next buffering mechanism involves the exchange of cations on the surfaces of [clay minerals](@entry_id:182570) and [soil organic matter](@entry_id:186899). These surfaces carry a net negative charge, known as the **Cation Exchange Capacity (CEC)**, which holds onto nutrient cations like $\mathrm{Ca^{2+}}$, $\mathrm{Mg^{2+}}$, and $\mathrm{K^+}$ (collectively, **base cations**). Incoming $\mathrm{H^+}$ ions from [acid deposition](@entry_id:202282) displace these base cations from the exchange sites into the soil solution, from where they can be taken up by plants or leached from the [soil profile](@entry_id:195342).
    $$ \text{Soil-Ca} + 2\mathrm{H}^+ \rightarrow \text{Soil-}(\mathrm{H})_2 + \mathrm{Ca^{2+}} $$
    The fraction of the CEC occupied by base cations is called the **base saturation (BS)**. As this buffering process continues, base saturation declines, leading to nutrient depletion. This process governs buffering in the weakly acidic range.

3.  **Aluminum Buffering (pH ≈ 4.0 - 5.0)**: As the pH drops below 5.0 and base saturation becomes very low, the dissolution of aluminum-bearing minerals ([aluminosilicates](@entry_id:151974) like clays and secondary minerals like gibbsite, $\mathrm{Al(OH)_3}$) becomes the dominant buffering reaction.
    $$ \mathrm{Al(OH)_3}(s) + 3\mathrm{H}^+ \rightarrow \mathrm{Al^{3+}} + 3\mathrm{H_2O} $$
    This process consumes a large amount of acid and can hold the soil pH in a strongly acidic plateau. However, a critical consequence is the release of soluble and toxic forms of aluminum into the soil solution.

4.  **Iron Buffering (pH  4.0)**: In extremely acidified soils, after the more reactive aluminum phases are depleted, the dissolution of iron oxides (e.g., goethite, $\mathrm{FeOOH}$) provides the final buffering mechanism.
    $$ \mathrm{FeOOH}(s) + 3\mathrm{H}^+ \rightarrow \mathrm{Fe^{3+}} + 2\mathrm{H_2O} $$
    This range is associated with severe soil degradation and conditions hostile to most plant life [@problem_id:2467926].

The rate at which a soil progresses through these buffering stages depends on the magnitude of the net acid load and the size of each buffering pool. Simple mass-balance models can be used to estimate the time required for a soil's base saturation to decline to a critical threshold, highlighting the long-term, cumulative nature of soil acidification [@problem_id:2467933].

#### The Acidifying Role of Nitrogen Deposition

The role of nitrogen is complex. As noted, atmospheric ammonia neutralizes acids to form ammonium aerosols. However, once this ammonium ($\mathrm{NH_4^+}$) is deposited in the ecosystem, it can be taken up by plants or undergo microbial **[nitrification](@entry_id:172183)**. Nitrification is an oxidation process that generates significant [acidity](@entry_id:137608):
$$ \mathrm{NH_4^+} + 2\mathrm{O_2} \rightarrow \mathrm{NO_3^-} + 2\mathrm{H^+} + \mathrm{H_2O} $$
For every mole of ammonium that is nitrified, two moles of hydrogen ions are produced. Therefore, the deposition of seemingly neutral ammonium salts can lead to substantial "delayed" acidification of the soil and subsequent leaching of nitrate and acidity to surface waters. In regions with high ammonia emissions, this process can be a dominant driver of [ecosystem acidification](@entry_id:192280), rivaling or exceeding the direct input of sulfuric and nitric acids [@problem_id:2467907].

### Ecotoxicology of Acidification: Mechanisms of Biological Damage

The ecological harm from acidification stems from both the direct effects of increased proton activity (low pH) and, more significantly, the indirect effects of altered soil and [water chemistry](@entry_id:148133), particularly the mobilization of toxic aluminum.

#### Aluminum Speciation and Bioavailability

In soil and water, aluminum exists in various chemical forms, or species, whose distribution is highly dependent on pH and the presence of complexing ligands. A crucial distinction is made between:
-   **Inorganic Monomeric Aluminum**: This category includes the free aluminum ion ($\mathrm{Al^{3+}}$) and its complexes with inorganic ligands like hydroxide (e.g., $\mathrm{AlOH^{2+}}$, $\mathrm{Al(OH)_2^+}$), fluoride (e.g., $\mathrm{AlF^{2+}}$), and sulfate (e.g., $\mathrm{AlSO_4^+}$).
-   **Organically-Complexed Aluminum**: This refers to aluminum bound to dissolved organic matter (DOM).

According to the **Free Ion Activity Model (FIAM)** and related ecotoxicological frameworks, the [bioavailability](@entry_id:149525) and acute toxicity of metals are primarily driven by the activity of the free metal ion and, in some cases, other small, labile [inorganic complexes](@entry_id:155582). Large organic complexes are generally considered to be non-bioavailable and non-toxic.

In acidified waters (e.g., pH  5), aluminum becomes soluble. The presence of strong complexing ligands, particularly fluoride and dissolved organic matter, can drastically reduce the concentration of the free $\mathrm{Al^{3+}}$ ion. For instance, in a high-DOC stream, the vast majority of dissolved aluminum may be bound to organic matter, rendering it largely non-toxic. Understanding the speciation of aluminum is therefore essential for predicting its [ecological risk](@entry_id:199224) [@problem_id:2467898].

#### Mechanisms of Aquatic and Terrestrial Toxicity

**Aquatic Organisms**: For freshwater fish, the primary site of toxic action is the gill epithelium. The combination of low pH and elevated inorganic monomeric aluminum disrupts the fish's ability to maintain its internal [salt balance](@entry_id:154372) (**ionoregulation**). This occurs via two main mechanisms:
1.  **Increased Gill Permeability**: The [tight junctions](@entry_id:143539) between gill epithelial cells, which regulate paracellular "leakiness," are stabilized by calcium ($\mathrm{Ca^{2+}}$). At low pH, protonation of fixed negative charges on the gill surface reduces the local binding of $\mathrm{Ca^{2+}}$. Furthermore, dissolved aluminum ($\mathrm{Al^{3+}}$) directly competes with and displaces $\mathrm{Ca^{2+}}$ from these critical binding sites, disrupting junctional integrity. This leads to a dramatic increase in the passive, outward leakage of essential ions like sodium ($\mathrm{Na^+}$) and chloride ($\mathrm{Cl^-}$) from the fish's blood into the water.
2.  **Inhibition of Active Ion Uptake**: To counteract passive losses, fish actively pump $\mathrm{Na^+}$ and $\mathrm{Cl^-}$ from the dilute freshwater into their blood using specialized transporters on the gill surface. High external $\mathrm{H^+}$ concentrations directly inhibit these transporters (e.g., by competing for binding at $\mathrm{Na^+}$ channels). Aluminum also binds to and damages these [transport proteins](@entry_id:176617).

The combined effect of massively increased ion efflux and inhibited ion influx leads to a rapid net loss of salts, a severe physiological stress known as ionoregulatory failure, which is the primary cause of fish mortality in acidified waters [@problem_id:2467942].

**Terrestrial Plants**: For plants, the primary target of aluminum toxicity is the root system, particularly the sensitive root tips where growth occurs. Calcium is essential for cell wall stability and as a [second messenger](@entry_id:149538) in [plant signaling](@entry_id:266464). The mechanism of Al toxicity is primarily one of **competitive antagonism with calcium**. Soluble $\mathrm{Al^{3+}}$ in the soil solution competes with $\mathrm{Ca^{2+}}$ for binding sites on the root [plasma membrane](@entry_id:145486), including cation channels responsible for calcium uptake. Because $\mathrm{Al^{3+}}$ often binds more strongly than $\mathrm{Ca^{2+}}$, even at low concentrations it can effectively block calcium uptake, leading to calcium deficiency, inhibition of root elongation, and ultimately, reduced plant growth and vigor.

This competitive interaction has led to the development of the soil solution **calcium-to-aluminum (Ca:Al) [molar ratio](@entry_id:193577)** as a key indicator of forest health risk. Below a critical Ca:Al ratio (often found to be near 1.0 in sensitive tree species), the fraction of root membrane sites occupied by calcium falls below the threshold required for normal function, and root damage is expected to occur [@problem_id:2467874]. The leaching of soil calcium and mobilization of aluminum by [acid deposition](@entry_id:202282) directly drives this ratio down, creating stressful conditions for forests.

### Synthesis and Application: The Critical Load Concept

The scientific understanding of the principles and mechanisms described above provides the foundation for a powerful environmental management tool: the **[critical load](@entry_id:193340)**. A critical load is defined as "a quantitative estimate of an exposure to one or more pollutants below which significant harmful effects on specified sensitive elements of the environment do not occur according to present knowledge."

Critical loads can be determined in two ways:
-   **Empirical Critical Loads** are based on direct observations of ecosystem responses along gradients of deposition or in manipulation experiments. For example, the deposition level at which a sensitive lichen species disappears from a region could be defined as an empirical critical load.
-   **Calculated Critical Loads** are derived from process-based models, most commonly **steady-state [mass balance](@entry_id:181721) models**. These models calculate the maximum deposition of sulfur and/or nitrogen an ecosystem can receive without violating a pre-defined chemical criterion (e.g., stream ANC > 20 µeq L⁻¹, soil Ca:Al ratio > 1.0), which is chosen to protect a sensitive biological endpoint.

The general formula for a steady-state [critical load](@entry_id:193340) of acidity is derived from a charge balance of inputs and outputs to a catchment:
$$ CL(S+N) = BC_w + BC_{dep} - Cl_{dep} - BC_u - ANC_{leach} $$
where $CL(S+N)$ is the [critical load](@entry_id:193340) of sulfur and nitrogen [acidity](@entry_id:137608), $BC_w$ is the base cation supply from weathering, $BC_{dep}$ and $Cl_{dep}$ are deposition terms, $BC_u$ is net base cation uptake by vegetation, and $ANC_{leach}$ is the allowable leaching of alkalinity needed to maintain the chemical criterion. By accounting for all major sources of alkalinity (weathering, deposition) and sinks of alkalinity (net ecosystem retention of N and S, leaching), this framework allows scientists to calculate a site-specific threshold for [acid deposition](@entry_id:202282). This concept has been instrumental in informing international agreements to reduce emissions of sulfur and [nitrogen oxides](@entry_id:150764) [@problem_id:2467884].