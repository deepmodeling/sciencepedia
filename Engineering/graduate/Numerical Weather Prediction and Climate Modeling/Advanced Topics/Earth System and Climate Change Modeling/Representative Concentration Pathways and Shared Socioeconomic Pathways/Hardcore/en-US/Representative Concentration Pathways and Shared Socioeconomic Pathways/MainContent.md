## Introduction
Projecting the Earth's future climate is an endeavor fundamentally linked to envisioning the future of humanity. The complex interplay of [population growth](@entry_id:139111), economic development, technological change, and policy decisions dictates the trajectory of greenhouse gas emissions and, consequently, the planet's energy balance. To navigate this complexity, the climate science community has developed sophisticated frameworks to construct plausible, internally consistent scenarios. The **Representative Concentration Pathways (RCPs)** and **Shared Socioeconomic Pathways (SSPs)** stand as the cornerstones of this effort, providing a structured language to connect societal choices with physical climate outcomes. This article demystifies these critical frameworks, addressing the challenge of how to systematically explore a range of possible climate futures.

Across the following chapters, you will gain a graduate-level understanding of the complete scenario-based modeling process. The first chapter, **Principles and Mechanisms**, deconstructs the causal chain from human activity to climate response, introducing foundational concepts like the Kaya identity and radiative forcing. The second chapter, **Applications and Interdisciplinary Connections**, illustrates how these scenarios are operationalized across diverse fields, from assessing biogeochemical feedbacks to downscaling projections for local impact studies. Finally, the **Hands-On Practices** section provides a look into the quantitative methods used to translate scenarios into concrete metrics like carbon budgets and temperature projections. We begin by examining the core principles that enable us to translate narratives about our future into the language of climate models.

## Principles and Mechanisms

To project the future of the Earth's climate, we must first construct plausible narratives of the future of humanity. The trajectory of our planet's climate over the coming century is inextricably linked to socioeconomic development, technological innovation, and global policy choices. This chapter delves into the principles and mechanisms that form the foundation of modern climate scenarios, specifically the **Representative Concentration Pathways (RCPs)** and **Shared Socioeconomic Pathways (SSPs)**. We will deconstruct the causal chain from human activity to climate response, examine the frameworks used to model these links, and explore the practical implementation of these scenarios in state-of-the-science Earth System Models (ESMs).

### The Causal Chain: From Human Activity to Climate Response

At its core, the challenge of [climate projection](@entry_id:1122479) can be understood as a sequence of cause and effect. This causal chain provides a conceptual roadmap for the components we must model:

1.  **Socioeconomic Drivers:** Human activities, driven by population growth, economic development, and technological choices, are the ultimate source of changes in atmospheric composition.

2.  **Emissions:** These activities result in the emission of greenhouse gases (GHGs) like carbon dioxide ($\text{CO}_2$), methane ($\text{CH}_4$), and nitrous oxide ($\text{N}_2\text{O}$), as well as aerosols and other radiatively active substances.

3.  **Concentrations:** Once emitted, these substances accumulate in the atmosphere. Their atmospheric concentration is determined by a balance between emission rates and their removal by natural sinks (e.g., oceans, land biosphere).

4.  **Radiative Forcing:** The altered atmospheric composition changes the Earth's energy balance. The net change in the energy balance at the tropopause, before the climate system has adjusted, is termed **Radiative Forcing (RF)**. It is the fundamental metric that quantifies the direct warming or cooling influence of a given change.

5.  **Climate Response:** Positive radiative forcing leads to a planetary energy imbalance, causing the global climate system—including the atmosphere, oceans, and cryosphere—to warm until a new equilibrium is reached. This response manifests as changes in global mean temperature, precipitation patterns, sea level, and the frequency of extreme weather events.

The SSP and RCP frameworks are designed to provide a structured way to quantify and explore this entire chain.

### Quantifying the Drivers: The Kaya Identity and Shared Socioeconomic Pathways (SSPs)

To formalize the link between socioeconomic activity and emissions, we can use the **Kaya identity**. This identity decomposes total anthropogenic $\text{CO}_2$ emissions into the product of four key factors:

$$
E_{\mathrm{CO2}}(t) = P(t) \times \frac{\mathrm{GDP}(t)}{P(t)} \times \frac{E(t)}{\mathrm{GDP}(t)} \times \frac{\mathrm{CO2}(t)}{E(t)}
$$

Here, $E_{\mathrm{CO2}}(t)$ is total $\text{CO}_2$ emissions, $P(t)$ is population, $\frac{\mathrm{GDP}(t)}{P(t)}$ is per capita economic output (a measure of affluence), $\frac{E(t)}{\mathrm{GDP}(t)}$ is the **energy intensity** of the economy (energy consumed per unit of GDP), and $\frac{\mathrm{CO2}(t)}{E(t)}$ is the **carbon intensity** of the energy system ($\text{CO}_2$ emitted per unit of energy).

The power of this identity lies in its analytical tractability. The fractional growth rate of emissions, $g_{E_{\mathrm{CO2}}}$, is approximately the sum of the growth rates of its components: $g_{E_{\mathrm{CO2}}} \approx g_P + g_A + g_I + g_C$, where the subscripts denote population, affluence, energy intensity, and carbon intensity, respectively. This allows us to analyze how different societal trends combine to influence the overall emissions trajectory.

For instance, consider a hypothetical scenario where, starting in 2035, population grows at $0.6\%$ per year ($g_P=0.006$) and per capita GDP grows at $1.9\%$ per year ($g_A=0.019$). These upward pressures on emissions could be counteracted by improvements in energy efficiency (a negative $g_I$) and decarbonization of the energy supply (a negative $g_C$). If energy intensity improves at a rate of $-1.6\%$ per year and carbon intensity improves at $-0.8\%$ per year, the net emissions growth rate would be $0.006 + 0.019 - 0.016 - 0.008 = 0.001$, or $0.1\%$. If, a decade later, the rate of decarbonization accelerates to $-1.5\%$ per year while other factors remain similar, the net growth rate could become negative, marking a peak in emissions .

This is precisely the conceptual space that **Shared Socioeconomic Pathways (SSPs)** are designed to explore. An SSP is a narrative, supported by quantitative data, that describes a plausible future evolution of these Kaya factors and other societal elements like land use, education, and governance. The five primary SSPs span a wide range of futures:

*   **SSP1 (Sustainability - Taking the Green Road):** A world shifting towards sustainability, with low [population growth](@entry_id:139111), high education, rapid technological progress in renewables, and high value placed on environmental protection.
*   **SSP2 (Middle of the Road):** A world where historical trends continue, with moderate progress in all areas.
*   **SSP3 (Regional Rivalry - A Rocky Road):** A fragmented world with resurgent nationalism, low international cooperation, slow economic growth, and little investment in education or environmental protection.
*   **SSP4 (Inequality - A Road Divided):** A world with high inequality both between and within countries, where a high-tech elite prospers while a large, low-income population struggles.
*   **SSP5 (Fossil-fueled Development - Taking the Highway):** A world with rapid, fossil-fuel-intensive economic growth, high faith in technological solutions, and high energy demand.

Crucially, SSPs are defined as **policy-neutral** with respect to new, explicit [climate policy](@entry_id:1122477) . They describe the socioeconomic background and the challenges it presents for climate mitigation and adaptation. The same SSP can be paired with different levels of climate policy ambition within an **Integrated Assessment Model (IAM)**, a type of model that links socioeconomic, energy, and climate systems. This allows researchers to explore how a specific climate outcome (e.g., limiting warming to $2^\circ\text{C}$) might be achieved under vastly different world conditions.

### From Emissions to Concentrations: The Role of Biogeochemical Cycles

Once emitted, greenhouse gases do not simply remain in the atmosphere. They are subject to complex biogeochemical cycles that redistribute them between the atmosphere, oceans, and land. The rate of change of a gas's atmospheric concentration, $C(t)$, can be described by a [mass balance equation](@entry_id:178786):

$$
\frac{dC(t)}{dt} = E(t) - S(C(t), t)
$$

Here, $E(t)$ is the anthropogenic emission rate and $S(C(t), t)$ is the net **sink** term, representing the rate of removal by land and ocean processes. This sink term is not constant; it depends on the atmospheric concentration itself and the state of the climate. For example, as the oceans warm, their ability to absorb $\text{CO}_2$ decreases. This **climate-carbon feedback** means that the fraction of emissions that remains in the atmosphere—the **airborne fraction**—is not constant and tends to increase under higher warming scenarios.

To model this complex behavior in a computationally efficient manner, especially for $\text{CO}_2$, a common approach is to use an **[impulse response function](@entry_id:137098) (IRF)**. The concentration increase above a preindustrial baseline is calculated as the convolution of the historical and future emissions path with a function that describes how a single pulse of emissions decays over time through multiple reservoirs (e.g., shallow ocean, deep ocean, terrestrial [biosphere](@entry_id:183762)) . This can be written as:

$$
\Delta C_{\mathrm{CO_2}}(t) = \int_{t_0}^{t} E_{\mathrm{CO_2}}(\tau) R(t-\tau) \, d\tau
$$

where $R(t-\tau)$ is the IRF, often represented as a sum of exponentials with different decay timescales, calibrated to reproduce the behavior of more complex carbon cycle models.

### From Concentrations to Forcing: The Physics of Radiative Transfer

The link between atmospheric concentrations and the Earth's energy balance is quantified by **Radiative Forcing (RF)**. It is defined as the net change in [irradiance](@entry_id:176465) at the tropopause (in $\text{W m}^{-2}$) following a perturbation (e.g., an increase in GHG concentration), after allowing for stratospheric temperatures to readjust to [radiative equilibrium](@entry_id:158473). A positive forcing implies a net energy gain and thus a warming influence.

For $\text{CO}_2$, the relationship between concentration and forcing is not linear. Each additional unit of $\text{CO}_2$ has a smaller warming effect than the one before it. This is due to a phenomenon called **absorption band saturation**. $\text{CO}_2$ absorbs outgoing longwave radiation in specific wavelength bands (notably around $15 \, \mu\text{m}$). At the center of these bands, the atmosphere is already nearly opaque even at preindustrial concentrations. Further increases in $\text{CO}_2$ primarily act to broaden these absorption bands, trapping radiation in the "wings" of the band. This process yields a logarithmic relationship, famously parameterized by Myhre et al. (1998):

$$
\Delta F_{\mathrm{CO_2}} = \alpha \ln\left(\frac{C}{C_0}\right)
$$

where $\alpha \approx 5.35 \, \text{W m}^{-2}$, $C$ is the current concentration, and $C_0$ is a preindustrial reference concentration (e.g., $278 \, \text{ppm}$). According to this formula, a doubling of $\text{CO}_2$ concentration from $278 \, \text{ppm}$ to $556 \, \text{ppm}$ results in a forcing of $5.35 \ln(2) \approx 3.7 \, \text{W m}^{-2}$. To achieve the same incremental forcing again, concentration would need to double again to $1112 \, \text{ppm}$ .

This leads us to the concept of **Representative Concentration Pathways (RCPs)**. An RCP is a trajectory of total radiative forcing over the 21st century and beyond. They are named after their approximate total radiative forcing value in the year 2100 relative to preindustrial times. The four canonical RCPs used in the Coupled Model Intercomparison Project Phase 5 (CMIP5) are:

*   **RCP2.6:** A strong mitigation pathway where forcing peaks at $\approx 3 \, \text{W m}^{-2}$ mid-century and declines to $2.6 \, \text{W m}^{-2}$ by 2100.
*   **RCP4.5:** An intermediate stabilization pathway where forcing stabilizes at $4.5 \, \text{W m}^{-2}$ after 2100.
*   **RCP6.0:** Another stabilization pathway, at a higher level of $6.0 \, \text{W m}^{-2}$.
*   **RCP8.5:** A high-end pathway with continuously rising forcing, reaching $8.5 \, \text{W m}^{-2}$ by 2100.

An RCP is fundamentally a forcing pathway, not an emissions or concentration pathway, though it is defined by a consistent set of concentrations for all major greenhouse gases and aerosols that would produce the target forcing.

### Scenario Frameworks for Climate Modeling

The evolution of climate modeling has seen a shift from prescribing simplified scenarios to using more integrated and consistent frameworks.

#### The CMIP5 Framework: A Focus on Forcing

The CMIP5 experimental design was primarily organized around the four RCPs. For the core experiments, modeling centers were provided with prescribed time series of greenhouse gas concentrations corresponding to each RCP. This **concentration-driven** approach had a major advantage: it allowed for direct comparison of the climate response across different models, regardless of whether they had an interactive carbon cycle. The forcing was effectively standardized. However, this came at the cost of decoupling the climate outcome from its underlying socioeconomic drivers. It answered the question "What is the climate response to a forcing of $X$?", but not "How could a forcing of $X$ come about, and what would be the cost?".

#### The CMIP6 Scenario Matrix: Pairing SSPs and RCPs

The CMIP6 framework introduces a more sophisticated **scenario matrix** that pairs the socioeconomic pathways (SSPs) with the radiative forcing targets (RCPs) . This two-dimensional matrix allows researchers to explore a much richer set of questions. The SSPs form the rows, representing different socioeconomic futures, and the forcing targets (named after the RCPs) form the columns, representing different levels of climate ambition. A scenario is now labeled, for example, **SSP2-4.5**, signifying a future that follows a "middle of the road" socioeconomic path (SSP2) and implements policies sufficient to limit 2100 radiative forcing to $4.5 \, \text{W m}^{-2}$.

This framework allows for the exploration of mitigation and adaptation challenges in a consistent way. For example, one can compare SSP1-2.6 and SSP5-2.6 to understand how much harder it is to achieve a low-forcing target in a fossil-fuel-intensive world (SSP5) versus a sustainability-focused one (SSP1).

However, not all combinations in this matrix are considered equally plausible. Integrated Assessment Models are used to determine which pairings are feasible. Some pairings may be ruled out due to **feasibility constraints** (the required emissions reductions are technologically or economically impossible) or **consistency constraints** (the required emissions trajectory violates the core narrative of the SSP). For example, a stylized analysis might show that for SSP3 (Regional Rivalry), with its limited capacity for mitigation and negative emissions, achieving the stringent RCP2.6 budget is infeasible. Conversely, for SSP1 (Sustainability), with its baseline emissions already low, it is inconsistent with the narrative to imagine a massive expansion of fossil fuel use to reach the high emissions of RCP8.5 .

### Mechanisms of Scenario Implementation in Models

The practical use of these scenarios in global climate models requires a sophisticated technical pipeline and distinct experimental designs.

#### Concentration-Driven vs. Emissions-Driven Simulations

At the heart of scenario implementation are two fundamental types of experiments , :

1.  **Concentration-Driven Simulations:** In this setup, the model is provided with prescribed time series of atmospheric concentrations for GHGs. The model's radiative transfer code uses these concentrations to calculate radiative forcing, which then drives the climate response. This approach bypasses the model's own carbon cycle. The causal chain within the model is simply: Prescribed $C(t) \rightarrow$ Calculated $F(t) \rightarrow$ Calculated $\Delta T(t)$. This is the required mode for models without an interactive carbon cycle (e.g., older Atmosphere-Ocean General Circulation Models, AOGCMs) and is the standard for the main CMIP intercomparison experiments to ensure a common forcing.

2.  **Emissions-Driven Simulations:** Here, the model is provided with prescribed emissions of GHGs and other substances. An Earth System Model (ESM) with an interactive carbon cycle then prognostically calculates the resulting atmospheric concentrations by simulating the exchange of carbon with the land and ocean sinks. The model's radiative code then calculates forcing from these internally generated concentrations. The full causal chain is simulated: Prescribed $E(t) \rightarrow$ Calculated $C(t) \rightarrow$ Calculated $F(t) \rightarrow$ Calculated $\Delta T(t)$. This approach is essential for studying climate-carbon feedbacks, as the efficiency of the carbon sinks can respond to the evolving climate state.

#### The Data Pipeline: From IAMs to Model Forcings

The generation of the standardized forcing datasets used by climate models—housed in repositories like **input4MIPs**—is a complex, multi-step process :

1.  **Harmonization:** Emissions trajectories from IAMs, which start from a stylized base year, must be smoothly blended with official historical emissions inventories. This "stitching" process is critical to avoid unphysical jumps or kinks in the emissions time series that could shock the climate model. Sophisticated mathematical techniques are used to ensure the resulting harmonized path is continuous in both its value and its rate of change ($C^1$ continuity) across the transition window .

2.  **Concentration Conversion:** The harmonized emissions are then fed into a reduced-complexity climate model (like MAGICC) that simulates the translation from emissions to concentrations for each gas. This involves using IRFs for $\text{CO}_2$, modeling complex chemical feedbacks for the lifetime of $\text{CH}_4$ (which depends on the hydroxyl radical, OH), and accounting for the "banks" of halocarbons present in existing equipment.

3.  **Ozone and Aerosol Fields:** For short-lived, spatially heterogeneous constituents like ozone and aerosols, the process is even more complex. For ozone, for example, emulators trained on ensembles of complex chemistry-climate models are used to generate full three-dimensional, monthly-mean ozone fields that are consistent with the scenario's emissions of ozone precursors ($\text{NO}_{\text{x}}$, VOCs) and methane concentrations.

The final product is a comprehensive, internally consistent set of gridded concentration and forcing data that can be used by modeling centers around the world.

### Interpreting and Using Scenario-Based Projections

The SSP-RCP framework does not produce predictions. It produces "projections"—[conditional statements](@entry_id:268820) about the future, contingent on the scenario's assumptions coming to pass. Understanding the sources of uncertainty in these projections is key to their proper use.

#### Decomposing Projection Uncertainty

At any given point in the future, the total uncertainty in a [climate projection](@entry_id:1122479) (e.g., for global mean temperature) can be decomposed into three main sources:

1.  **Internal Variability:** This is the natural, chaotic variability inherent in the climate system (e.g., El Niño-Southern Oscillation). It is often estimated as the spread of different simulations from the same model under the same forcing scenario (a "large ensemble"). Its variance contribution, $V_{\text{int}}$, is largely constant with time.

2.  **Model Uncertainty:** Different climate models, though based on the same physical laws, use different numerical methods, parameterizations, and resolutions. This leads to a spread in their climate response to the same forcing. The variance contribution, $V_{\text{mod}}$, typically grows with the magnitude of the forced signal.

3.  **Scenario Uncertainty:** This is the uncertainty arising from the unknown future path of human development and emissions, as captured by the different SSP-RCP scenarios. Its variance contribution, $V_{\text{scen}}$, is small in the near term (as all scenarios start from the same historical point) but grows substantially over time as the scenarios diverge.

A key finding from analyses of this decomposition is that in the near term (out to ~2040), [internal variability](@entry_id:1126630) and model uncertainty are the dominant sources of uncertainty in global temperature projections. However, by the second half of the 21st century, **scenario uncertainty becomes the single largest source of uncertainty** . This powerfully demonstrates that our long-term climate future is not predetermined; it depends profoundly on the societal choices we make today and in the coming decades.

#### The Epistemology of High-End Scenarios

This leads to a final, critical point about the use of scenarios. What is the epistemic status of a high-end scenario like SSP5-8.5, which involves a massive, century-long expansion of fossil fuel use? Some critics argue that, given recent trends in decarbonization, such a scenario is implausible and its use is misleading.

However, its justification does not lie in its being a likely forecast. Rather, SSP5-8.5 and other high-end scenarios serve an essential role as **plausible worst-case storylines** or **stress tests** . In [risk assessment](@entry_id:170894), it is critical to understand the [upper bounds](@entry_id:274738) of [potential outcomes](@entry_id:753644), even if their probability is low. SSP5-8.5 explores a future where current decarbonization trends falter and are reversed, providing an invaluable tool for impact and adaptation studies that need to plan for high levels of warming.

At the same time, it is scientifically rigorous to test the feasibility of these scenarios against known physical and economic constraints. For example, a proper sensitivity analysis could use an IAM to examine whether the cumulative emissions required for an SSP5-8.5 pathway are achievable given different estimates of ultimately recoverable fossil fuel resources, modeled through dynamic cost-supply curves. Such work helps to refine our understanding of what is not just imaginable, but also attainable, at the high end of the scenario spectrum.