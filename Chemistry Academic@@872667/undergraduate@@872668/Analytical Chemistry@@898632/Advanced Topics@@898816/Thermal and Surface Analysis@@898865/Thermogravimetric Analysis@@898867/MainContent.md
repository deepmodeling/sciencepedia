## Introduction
Thermogravimetric Analysis (TGA) is a cornerstone technique in [thermal analysis](@entry_id:150264), offering powerful insights into how a material's composition and stability change under thermal stress. Its ability to precisely measure mass as a function of temperature makes it an indispensable tool in fields from polymer chemistry to pharmaceuticals for characterizing, comparing, and ensuring the quality of materials. A fundamental challenge in materials science is understanding and predicting material behavior at elevated temperatures, whether it's the degradation of a polymer, the dehydration of a drug, or the oxidation of a metal. TGA directly addresses this by providing quantitative data on the thermal events that involve a change in mass. This article serves as a comprehensive guide to this technique, structured to build knowledge progressively. The first chapter, "Principles and Mechanisms," lays the groundwork by exploring the fundamental theory behind TGA, including how to interpret mass changes and the critical role of experimental parameters. The second chapter, "Applications and Interdisciplinary Connections," demonstrates the versatility of TGA by showcasing its use in compositional analysis, stability testing, and mechanistic studies across various scientific disciplines. Finally, the "Hands-On Practices" section provides practical problems that allow you to apply stoichiometric principles to real-world TGA data, solidifying your understanding of this essential analytical method.

## Principles and Mechanisms

Thermogravimetric Analysis (TGA) is a powerful [thermal analysis](@entry_id:150264) technique that provides quantitative information about the physical and chemical changes a material undergoes upon heating. The core principle of TGA is the continuous measurement of a sample's mass as a function of temperature or time in a controlled atmosphere. The resulting data, typically plotted as a [thermogram](@entry_id:157820) of mass versus temperature, offers profound insights into a material's composition, thermal stability, and [reaction kinetics](@entry_id:150220). This chapter will elucidate the fundamental principles governing mass changes, the critical influence of the experimental environment, methods for interpreting thermograms, and important instrumental considerations.

### The Fundamental Measurement: Mass Change Events

The central measurement in TGA is mass, a fundamental property of matter. For the mass of a sample in the TGA pan to change, matter must either be lost from the sample to its surroundings or gained from the surroundings. A TGA experiment, therefore, is an open-system measurement that tracks the flux of matter across the sample-gas boundary. The events observed in a [thermogram](@entry_id:157820) can be categorized into three types: mass loss, mass gain, and mass stability.

**Mass Loss (Decomposition, Desorption, Volatilization)**

A decrease in sample mass is the most common event observed in TGA. This indicates that a portion of the sample has transformed into volatile products that are swept away by the purge gas. Common processes include:
*   **Desorption:** The release of physically adsorbed volatiles, such as surface moisture, which typically occurs at relatively low temperatures.
*   **Volatilization:** The [evaporation](@entry_id:137264) or sublimation of the sample itself.
*   **Decomposition:** The chemical breakdown of the material into one or more volatile products and, potentially, a solid residue.

Quantitative analysis of [mass loss](@entry_id:188886) is a cornerstone of TGA. By relating the measured mass change to the [stoichiometry](@entry_id:140916) of a known reaction, one can determine the composition or purity of a sample. For instance, consider the analysis of a hydrated salt, such as nickel(II) sulfate hexahydrate ($\text{NiSO}_4 \cdot 6\text{H}_2\text{O}$), which is known to be contaminated with a thermally stable, inert substance like sodium chloride ($\text{NaCl}$) [@problem_id:1483904]. Upon heating in an [inert atmosphere](@entry_id:275393), the hydrate undergoes dehydration:

$$ \text{NiSO}_4 \cdot 6\text{H}_2\text{O}_\text{(s)} \rightarrow \text{NiSO}_{4\text{(s)}} + 6\text{H}_2\text{O}_\text{(g)} $$

The TGA [thermogram](@entry_id:157820) will show a distinct [mass loss](@entry_id:188886) step corresponding to the evolution of water vapor. If the initial sample mass is $m_i$ and the final mass of the anhydrous residue (anhydrous $\text{NiSO}_4$ plus the $\text{NaCl}$ impurity) is $m_f$, the mass of water lost is simply $\Delta m = m_i - m_f$. From the stoichiometry, we know that for every mole of $\text{NiSO}_4 \cdot 6\text{H}_2\text{O}$ ([molar mass](@entry_id:146110) $M_{\text{hydrate}}$), 6 moles of water (molar mass $M_{\text{H}_2\text{O}}$) are lost. The initial mass of the pure hydrate, $m_{\text{hydrate}}$, in the sample can therefore be calculated from the mass of water lost:

$$ m_{\text{hydrate}} = (m_i - m_f) \left( \frac{M_{\text{hydrate}}}{6 M_{\text{H}_2\text{O}}} \right) $$

This allows for the direct determination of the original sample's purity.

**Mass Gain (Reaction with Atmosphere)**

Conversely, an increase in sample mass indicates that the material has reacted with the surrounding purge gas to form a new, heavier, non-volatile product. The most common example of this is oxidation. When a metal is heated in a reactive atmosphere such as air or pure oxygen, it can form a metal oxide, resulting in a mass gain.

For example, when finely powdered chromium metal ($\text{Cr}$) is heated in an oxygen atmosphere, it reacts to form chromium(III) oxide ($\text{Cr}_2\text{O}_3$) [@problem_id:1483868]. The [balanced chemical equation](@entry_id:141254) for this reaction is:

$$ 4\text{Cr}_\text{(s)} + 3\text{O}_{2\text{(g)}} \rightarrow 2\text{Cr}_2\text{O}_{3\text{(s)}} $$

For every 4 moles of chromium (atomic mass $A_{\text{Cr}}$) that react, 2 moles of chromium(III) oxide ([molar mass](@entry_id:146110) $M_{\text{Cr}_2\text{O}_3}$) are formed. The final mass, $m_f$, can be stoichiometrically related to the initial mass of chromium, $m_i$:

$$ m_f = m_i \left( \frac{2 M_{\text{Cr}_2\text{O}_3}}{4 A_{\text{Cr}}} \right) = m_i \left( \frac{M_{\text{Cr}_2\text{O}_3}}{2 A_{\text{Cr}}} \right) $$

Since the molar mass of the oxide is greater than twice the atomic mass of the metal due to the addition of oxygen, the final mass will be greater than the initial mass. This ability to monitor mass gain makes TGA an invaluable tool for studying corrosion, [oxidation kinetics](@entry_id:185767), and gas-solid reactions.

**Mass Stability (Inertness)**

A flat, horizontal line on a TGA [thermogram](@entry_id:157820) indicates that the sample's mass is constant over the measured temperature range. This implies that the material is **thermally stable**, meaning it does not decompose or volatilize. Furthermore, it implies that the material is **chemically inert** with respect to the purge gas [@problem_id:1483853]. A sample of pure gold heated to 1000 °C in a nitrogen atmosphere, for example, will show no mass change. This is because gold has extremely low volatility below its [melting point](@entry_id:176987) (1064 °C) and does not react with nitrogen.

It is critical to distinguish thermal events that involve mass change from those that do not. A **phase transition**, such as melting (solid to liquid) or a solid-solid crystal transition, occurs at constant mass. Heating gold through its [melting point](@entry_id:176987) would result in a [phase change](@entry_id:147324), but the TGA curve would remain flat because no matter is lost or gained. Therefore, TGA, when used alone, is insensitive to first-order phase transitions like melting.

### The Critical Role of the Experimental Atmosphere

The gaseous environment surrounding the sample is not a passive background but an active experimental parameter that can fundamentally alter the observed thermal events. The choice of purge gas is critical and is dictated by the analytical goal.

**Inert Atmosphere**

Most TGA experiments are conducted under a continuous flow of an inert gas, such as high-purity nitrogen or argon. The use of a purge gas serves two primary, critical functions [@problem_id:1343625]:
1.  **To Provide a Controlled, Non-Reactive Environment:** The inert gas displaces reactive atmospheric gases, principally oxygen. This prevents unwanted side reactions like oxidation, ensuring that the observed mass loss is attributable to the intrinsic [thermal decomposition](@entry_id:202824) ([pyrolysis](@entry_id:153466)) of the material.
2.  **To Remove Volatile Products:** The constant flow of the purge gas efficiently sweeps gaseous decomposition products away from the sample. This is crucial for preventing the products from re-adsorbing onto the sample or participating in secondary reactions. By maintaining a near-zero [partial pressure](@entry_id:143994) of the product gases above the sample, the purge gas ensures that the decomposition equilibrium is continuously shifted towards product formation, allowing the intrinsic [reaction kinetics](@entry_id:150220) to be studied more accurately.

**Reactive Atmosphere**

Alternatively, a reactive gas (e.g., air, oxygen, hydrogen) can be used as the purge gas to intentionally study the reactivity of a sample. As discussed with the oxidation of chromium, using an oxygen-containing atmosphere is the standard method for investigating the oxidative stability of materials.

The profound impact of the atmosphere can be illustrated by analyzing a material like Polyvinyl Chloride (PVC) under different conditions [@problem_id:1483881]. When a composite of PVC and an inert filler is heated to a high temperature in a nitrogen atmosphere, the PVC pyrolyzes. In this process, volatile components ($\text{HCl}$ and hydrocarbons) are driven off, leaving a residue of solid carbon. The final mass is the sum of the inert filler and this carbon char. However, when the same material is heated in air, the process is entirely different. The PVC undergoes complete [combustion](@entry_id:146700), reacting with oxygen to form exclusively gaseous products ($\text{CO}_2$, $\text{H}_2\text{O}$, $\text{HCl}$). In this case, the PVC component leaves no solid residue. The final mass corresponds only to the inert filler. By comparing the results from these two experiments, one can quantitatively determine the composition of the original composite and even deduce properties of the polymer itself.

### Interpreting the Thermogram: Key Features and Kinetic Insights

A standard TGA [thermogram](@entry_id:157820) plots the percentage of initial mass remaining on the y-axis against the temperature on the x-axis. A more detailed analysis often involves the derivative of this curve.

**The Onset Temperature ($T_{onset}$)**

While the entire curve provides a profile of stability, it is often useful to define a single temperature to characterize the beginning of a decomposition event. The **[onset temperature](@entry_id:197328) ($T_{onset}$)** is a common metric for this purpose. While several definitions exist, a standard instrumental method defines $T_{onset}$ as the temperature at the intersection of the extrapolated pre-decomposition baseline and the tangent drawn to the TGA curve at its point of maximum slope (i.e., maximum rate of [mass loss](@entry_id:188886)) [@problem_id:1483886]. This extrapolated value provides a consistent, albeit somewhat arbitrary, marker for comparing the stability of different materials under identical conditions.

**The Derivative Thermogravimetry (DTG) Curve**

For a more nuanced view of the decomposition process, analysts often compute the first derivative of the TGA curve. The **Derivative Thermogravimetry (DTG) curve** is a plot of the rate of [mass loss](@entry_id:188886) versus temperature. Mathematically, the DTG signal is typically defined as the negative of the first derivative of mass with respect to time, $-\frac{\text{d}m}{\text{d}t}$. Plotting this signal against temperature reveals peaks corresponding to [mass loss](@entry_id:188886) events.

The key feature of a DTG curve is its peak. The temperature at which a DTG peak reaches its maximum, $T_p$, corresponds to the temperature at which the **rate of the [mass loss](@entry_id:188886) reaction is at its maximum** [@problem_id:1483851]. This is an inflection point on the original TGA mass curve. The DTG curve is exceptionally useful for resolving overlapping thermal events that might appear as a single, drawn-out step in the TGA curve, as each distinct process will ideally give rise to its own peak in the derivative plot.

**The Influence of Heating Rate**

Decomposition reactions are kinetically controlled processes, not [thermodynamic equilibrium](@entry_id:141660) events. Consequently, the rate at which the sample is heated ($\beta = \frac{\text{d}T}{\text{d}t}$) has a significant impact on the observed decomposition temperature. As a general rule, **increasing the heating rate shifts the TGA curve and its corresponding DTG peak to higher temperatures**.

This phenomenon can be understood intuitively: a [decomposition reaction](@entry_id:145427) requires a certain amount of time to occur at a given temperature. If the temperature is ramped up more quickly, the system has less time to react at any given temperature. It must therefore reach a higher temperature to achieve the same degree of conversion (i.e., the same percentage of mass loss). This kinetic dependence can be modeled mathematically. Isoconversional methods, such as the Ozawa-Flynn-Wall (OFW) method, provide a relationship between heating rate ($\beta$), activation energy ($E_a$), and the absolute temperature ($T$) at which a specific conversion (fraction of mass loss) is reached [@problem_id:1483872]:

$$ \ln(\beta) = C - \frac{E_a}{R T} $$

Here, $R$ is the ideal gas constant and $C$ is a constant. This equation clearly shows that for a constant activation energy, a higher heating rate $\beta$ requires a higher temperature $T$ to satisfy the equality. By performing experiments at multiple heating rates, one can use this relationship to determine the activation energy of the decomposition process.

### Combining Techniques: Simultaneous Thermal Analysis

While TGA is powerful, its interpretation can be ambiguous. For example, is a mass loss event due to decomposition or simple boiling? To resolve such questions, TGA is often combined with other techniques, most commonly Differential Scanning Calorimetry (DSC), in a single instrument. This is known as **Simultaneous Thermal Analysis (STA)** or TGA-DSC.

In a TGA-DSC experiment, both the mass change and the heat flow to or from the sample are measured simultaneously as a function of temperature [@problem_id:1483874]. This provides two complementary data streams that allow for unambiguous event identification.
*   A **melting** process is a phase transition that is endothermic (absorbs heat) but involves no change in mass. It will therefore appear as a sharp endothermic peak on the DSC signal with a corresponding flat line on the TGA signal.
*   A **decomposition** process typically involves breaking chemical bonds, which is often an [endothermic process](@entry_id:141358), and it inherently involves the generation of volatile products. It will therefore appear as an endothermic feature on the DSC signal that occurs concurrently with a mass loss step on the TGA signal.
*   An **exothermic decomposition** or a **crystallization** event would show an exothermic peak on the DSC signal, with the former also showing a [mass loss](@entry_id:188886) on the TGA trace and the latter showing no mass change.

### Instrumental Considerations: The Buoyancy Artifact

A crucial aspect of performing accurate TGA measurements is understanding and correcting for instrumental artifacts. The most prominent of these is the **buoyancy effect**. The ultra-sensitive microbalance in a TGA instrument measures the *[apparent weight](@entry_id:173983)* of the sample, which is its true weight minus the [buoyant force](@entry_id:144145) exerted by the surrounding purge gas. This buoyant force is equal to the weight of the gas displaced by the volume of the sample and the sample holder.

$$ m_{\text{app}}(T) = m_{\text{true}} - \rho_{\text{gas}}(T) V_{\text{displaced}} $$

The density of the purge gas, $\rho_{\text{gas}}$, is temperature-dependent. Assuming ideal gas behavior, the density of the gas decreases as the temperature increases ($ \rho = \frac{PM}{RT} $). As the gas density $\rho_{\text{gas}}(T)$ decreases, the upward [buoyant force](@entry_id:144145) also decreases. This causes the apparent mass, $m_{\text{app}}$, to increase [@problem_id:1483870].

This effect is present in all TGA experiments but is most pronounced for samples that have a large volume and low density, such as foams and [aerogels](@entry_id:194660). For such a sample, the initial heating phase of a TGA run may show a slight but noticeable apparent mass *gain* before any true [thermal decomposition](@entry_id:202824) begins. To correct for this and other instrumental drift, a baseline measurement is always performed by running an identical temperature program with an empty sample pan. This baseline is then subtracted from the sample data to yield the true mass change of the sample.