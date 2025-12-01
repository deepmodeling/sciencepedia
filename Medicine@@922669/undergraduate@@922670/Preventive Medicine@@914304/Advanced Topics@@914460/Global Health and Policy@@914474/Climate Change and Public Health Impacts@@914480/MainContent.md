## Introduction
Climate change is not just an environmental issue; it is one of the most significant public health challenges of the 21st century. From intensifying heatwaves and worsening air pollution to the expanding reach of infectious diseases, the consequences of a warming planet directly threaten human well-being. To effectively protect communities, public health professionals must move beyond simple awareness and develop a deep, mechanistic understanding of these threats. This article bridges the gap between climate science and public health practice, equipping readers with the knowledge and tools to analyze risks and formulate evidence-based solutions.

This article is structured to build your expertise progressively. In the first chapter, **Principles and Mechanisms**, we will dissect the foundational science, exploring how shifts in the climate system translate into specific health hazards and introducing core frameworks for quantifying risk. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate how these principles are applied in real-world scenarios, from designing heat-health warning systems to evaluating the health co-benefits of climate policy. Finally, the **Hands-On Practices** section will provide practical exercises to solidify your understanding of risk assessment and intervention evaluation, empowering you to translate theory into action.

## Principles and Mechanisms

The intersection of climate change and public health is governed by a series of cascading physical, ecological, and social mechanisms. Understanding these principles is fundamental to assessing current burdens, projecting future risks, and designing effective interventions. This chapter elucidates the core frameworks and pathways that connect a changing climate to human health outcomes.

### The Climate System as a Driver of Health Risk

The primary link between climate change and health begins with fundamental shifts in the Earth's energy balance and the resulting statistical changes in our weather and climate.

#### Radiative Forcing and the Shift in Climate Distributions

The principal driver of anthropogenic [climate change](@entry_id:138893) is **[radiative forcing](@entry_id:155289)**, a concept central to [climate science](@entry_id:161057). The Intergovernmental Panel on Climate Change (IPCC) defines effective [radiative forcing](@entry_id:155289) ($\Delta F$) as the change in the net downward radiative energy flux at the top of the atmosphere, or tropopause, caused by a change in a climate driver (such as an increase in greenhouse gas concentrations), after allowing for rapid atmospheric adjustments. It is a measure of how a given factor perturbs the planet's energy balance, expressed in watts per square meter ($W/m^2$) [@problem_id:4510859].

A sustained positive [radiative forcing](@entry_id:155289) creates an energy imbalance where the Earth absorbs more energy than it radiates to space. The climate system responds by warming until it can radiate enough additional energy to restore equilibrium. This relationship can be approximated at equilibrium by the equation:

$$ \Delta T \approx \frac{\Delta F}{\lambda} $$

Here, $\Delta T$ is the change in global mean surface temperature (in K or $^\circ\mathrm{C}$), and $\lambda$ is the **climate feedback parameter**, which represents how much outgoing radiation increases for each degree of surface warming. For instance, a sustained positive forcing of $\Delta F = +3 \, \mathrm{W/m^2}$, a level expected under many intermediate to high emissions scenarios this century, combined with a typical climate feedback parameter of $\lambda = 1.23 \, \mathrm{W/m^2/K}$, would lead to an equilibrium global mean warming of approximately $\Delta T \approx 2.4^\circ\mathrm{C}$ [@problem_id:4510859].

Crucially for public health, this global average warming manifests as a fundamental shift in the statistical distribution of local weather variables. A modest shift in the mean of a temperature distribution can lead to a dramatic, non-linear increase in the frequency and intensity of extreme events.

Consider a region where summertime daily maximum temperature, $T_{\max}$, is normally distributed with a historical mean $\mu_0 = 35^\circ\mathrm{C}$ and standard deviation $\sigma = 2^\circ\mathrm{C}$. Suppose a temperature of $40^\circ\mathrm{C}$ is a critical threshold for a sharp rise in heat-related illnesses. The baseline probability of exceeding this threshold is the area in the tail of the distribution, which can be calculated using the standard normal [cumulative distribution function](@entry_id:143135), $\Phi(z)$:

$$ P(T_{\max} > 40^\circ\mathrm{C}) = 1 - \Phi\left(\frac{40 - 35}{2}\right) = 1 - \Phi(2.5) \approx 0.0062 $$

This means that historically, such a day occurred about $0.62\%$ of the time. Now, if [climate change](@entry_id:138893) shifts the mean temperature by $\Delta T = +2.4^\circ\mathrm{C}$ to a new mean of $\mu_1 = 37.4^\circ\mathrm{C}$, while the standard deviation remains unchanged, the new probability becomes:

$$ P(T_{\max} > 40^\circ\mathrm{C}) = 1 - \Phi\left(\frac{40 - 37.4}{2}\right) = 1 - \Phi(1.3) \approx 0.0968 $$

The frequency of these dangerous days has increased from about $0.6\%$ to nearly $10\%$, a relative increase of over 15 times [@problem_id:4510859]. This simple example illustrates a foundational principle: even seemingly small changes in average climate can lead to massive increases in the extreme weather events that most directly threaten public health.

#### Understanding Timescales: Weather, Climate Variability, and Climate Change

To design effective health interventions, it is essential to distinguish between the different temporal scales at which climate phenomena operate. Public health strategies must be aligned with the timescale of the threat they aim to address [@problem_id:4510891].

**Weather variability** refers to short-term, day-to-day deviations in atmospheric conditions. A forecast of a $+5^\circ\mathrm{C}$ temperature anomaly for the upcoming week is an example of weather variability. Public health responses to weather operate on a tactical, short-term basis. These include implementing heat-health warning systems that trigger emergency actions like opening cooling centers, conducting wellness checks on vulnerable individuals, and disseminating public risk messages.

**Climate variability** describes medium-term fluctuations around a long-term average, occurring on interannual to decadal timescales. The El Niño-Southern Oscillation (ENSO), which can cause a region's summer to be significantly hotter or cooler than average, is a prime example of climate variability. Public health planning for climate variability is strategic and seasonal. For instance, a seasonal forecast for a hotter-than-average summer due to ENSO would prompt health departments to pre-allocate budgets, increase summer staffing, and prepare large-scale public outreach campaigns on hydration and heat safety.

**Climate change** refers to persistent, long-term shifts in the statistical properties of the climate system, such as a multi-decadal warming trend of $+0.3^\circ\mathrm{C}$ per decade. This persistent change alters the baseline risk permanently. Responses to climate change must therefore be long-term and structural, focusing on adaptation to reduce underlying vulnerability. These interventions include investments in long-lived infrastructure such as increasing urban tree canopy, implementing "cool roof" and pavement programs, and updating building codes for [thermal efficiency](@entry_id:142875). A coherent public health strategy integrates actions across all three timescales, from daily warnings to seasonal preparedness and long-term urban planning [@problem_id:4510891].

### Core Frameworks for Assessing Health Impacts

To systematically analyze and quantify the health effects of climate change, the field relies on established conceptual and quantitative frameworks.

#### The Vulnerability and Risk Framework

The translation of a climatic phenomenon into a health impact is not automatic; it is mediated by the characteristics of the affected population and system. The IPCC provides a widely used framework that defines these relationships [@problem_id:4510851].

A **hazard** ($H$) is the potentially damaging climate event, trend, or impact itself, such as a heatwave, flood, or shift in a disease vector's range.

**Vulnerability** ($V$) is the propensity or predisposition of a system to be adversely affected. It is an internal characteristic of the population or system and is not a property of the hazard itself. Vulnerability is itself a composite of three components:

1.  **Exposure** ($E$): The presence of people, livelihoods, ecosystems, assets, and infrastructure in places and settings that could be adversely affected by a hazard.
2.  **Sensitivity** ($S$): The degree to which a system or species is affected, either adversely or beneficially, by climate variability or change. For health, this includes physiological susceptibility, such as the prevalence of pre-existing chronic conditions, age distribution (e.g., high proportions of elderly or very young), and occupational exposure.
3.  **Adaptive Capacity** ($A$): The ability of systems, institutions, humans, and other organisms to adjust to potential damage, to take advantage of opportunities, or to respond to consequences. This includes access to healthcare, effectiveness of public health infrastructure, level of income and education, and access to technologies like air conditioning.

The relationship between these components is intuitive: vulnerability increases with greater exposure and higher sensitivity, but decreases with greater [adaptive capacity](@entry_id:194789).

Finally, **risk** ($R$) is the potential for adverse consequences where something of value is at stake and the outcome is uncertain. In the context of [climate change](@entry_id:138893), risk results from the interaction of a climate hazard ($H$) with the vulnerability ($V$) of the exposed system. A common conceptual formulation is $R = f(H, V)$. This clarifies that a hazard poses no risk if there is nothing vulnerable to its effects (e.g., a powerful hurricane over an empty stretch of ocean), and a highly vulnerable population faces no risk if the hazard never occurs. Public health interventions can reduce risk by reducing exposure (e.g., evacuation), reducing sensitivity (e.g., managing chronic diseases), or increasing [adaptive capacity](@entry_id:194789) (e.g., implementing early warning systems).

#### Quantifying the Burden of Disease: Disability-Adjusted Life Years (DALYs)

To evaluate the magnitude of health impacts and prioritize interventions, a standardized metric is needed to quantify the total health loss from both mortality and morbidity. The **Disability-Adjusted Life Year (DALY)**, a cornerstone of the Global Burden of Disease (GBD) study, serves this purpose [@problem_id:4510852]. One DALY represents the loss of one year of full health.

The DALY is calculated as the sum of two components:

$$ DALY = YLL + YLD $$

**Years of Life Lost (YLL)** quantifies the burden from premature mortality. It is calculated by multiplying the number of deaths in each age group by a standard life expectancy at the age of death. For example, if a heatwave causes 5 deaths at age 60, where the standard remaining life expectancy is 22 years, and 7 deaths at age 75, where the remaining life expectancy is 12 years, the total YLL would be:

$$ YLL = (5 \text{ deaths} \times 22 \text{ years/death}) + (7 \text{ deaths} \times 12 \text{ years/death}) = 110 + 84 = 194 \text{ years} $$

**Years Lived with Disability (YLD)** quantifies the burden from non-fatal health conditions (morbidity). For a given condition, it is calculated using the formula:

$$ YLD = I \times DW \times L $$

where $I$ is the number of incident cases, $DW$ is the **disability weight**, and $L$ is the average duration of the disability. The disability weight is a value between 0 (perfect health) and 1 (equivalent to death) that reflects the severity of the health state. To illustrate, consider a cohort of individuals who develop heat-related kidney disease. If 300 people develop moderate Chronic Kidney Disease ($DW = 0.104$) with an average duration of 10 years, and 120 people develop a severe form ($DW = 0.163$) lasting 6 years, the total YLD would be the sum of the burden from each group:

$$ YLD = (300 \times 0.104 \times 10) + (120 \times 0.163 \times 6) = 312 + 117.36 = 429.36 \text{ years} $$

The total disease burden from heat-related kidney disease in this example would be $DALY = 194 + 429.36 = 623.36$ years of healthy life lost [@problem_id:4510852]. The DALY framework allows for a comprehensive assessment of health impacts and enables comparison of the burden across different diseases and risk factors.

### Key Mechanistic Pathways of Climate-Health Impacts

Climate change impacts health through a diverse set of [direct and indirect pathways](@entry_id:149318). The following sections explore the mechanisms for several key climate-sensitive health outcomes.

#### Air Quality: Ground-Level Ozone Photochemistry

Climate change can exacerbate air pollution, with significant consequences for respiratory and cardiovascular health. A prime example is the formation of ground-level ozone ($O_3$), a harmful secondary pollutant. Ozone is not directly emitted but is formed in the atmosphere through photochemical reactions involving precursor pollutants, primarily [nitrogen oxides](@entry_id:150764) ($NO_x$) and volatile organic compounds (VOCs). The formation of ozone is highly sensitive to both temperature and solar radiation, two factors directly affected by climate change [@problem_id:4510863].

In a simplified urban atmosphere, the concentration of ozone is governed by a rapid cycle of reactions known as the **Leighton relationship**. The core reactions are:
1.  Photolysis of [nitrogen dioxide](@entry_id:149973): $NO_2 + h\nu \rightarrow NO + O$
2.  Ozone formation: $O + O_2 \rightarrow O_3$
3.  Ozone titration (destruction): $NO + O_3 \rightarrow NO_2 + O_2$

Under photostationary steady-state (PSS) conditions, the rate of ozone production from $NO_2$ [photolysis](@entry_id:164141) equals its rate of destruction by $NO$. This leads to the relationship:

$$ [{\rm O_3}]_{\text{PSS}} = \frac{J_{{\rm NO_2}} [{\rm NO_2}]}{k_{{\rm NO}+{\rm O_3}} [{\rm NO}]} $$

Here, $[{\rm O_3}]$, $[{\rm NO}]$, and $[{\rm NO_2}]$ are the concentrations of the respective molecules, $J_{{\rm NO_2}}$ is the [photolysis](@entry_id:164141) frequency of $NO_2$, and $k_{{\rm NO}+{\rm O_3}}$ is the temperature-dependent rate constant for the ozone titration reaction.

Climate change intensifies ozone formation through two [main effects](@entry_id:169824):
*   **Increased Solar Radiation**: Clearer skies or changes in cloud patterns associated with certain climate shifts can increase solar radiation, which in turn increases the [photolysis](@entry_id:164141) rate $J_{{\rm NO_2}}$, boosting the ozone production term in the numerator.
*   **Increased Temperature**: Most chemical reaction rates increase with temperature, as described by the Arrhenius equation. This affects the ozone titration rate constant $k_{{\rm NO}+{\rm O_3}}$ in the denominator.

The net effect on ozone depends on the relative sensitivity of $J_{{\rm NO_2}}$ and $k_{{\rm NO}+{\rm O_3}}$ to these changes. A quantitative analysis reveals that the increase in ozone production from higher radiation typically outweighs the increase in its destruction from higher temperatures. For example, on a day that is hotter ($308$ K vs. $298$ K) and sunnier ($800 \, W/m^{-2}$ vs. $600 \, W/m^{-2}$), the [photolysis](@entry_id:164141) rate $J_{{\rm NO_2}}$ might increase by about $33\%$, while the destruction rate constant $k_{{\rm NO}+{\rm O_3}}$ might increase by only about $18\%$. The resulting steady-state ozone concentration, being proportional to the ratio $J/k$, would increase by approximately $13\%$ [@problem_id:4510863]. This "climate penalty" on air quality means that even if precursor emissions remain constant, warming temperatures and changing solar radiation patterns can lead to higher concentrations of ground-level ozone, elevating the risk of cardiopulmonary events by provoking airway inflammation and other physiological stresses.

#### Water-Borne Infectious Diseases: Proliferation of Pathogens

Warming of the world's oceans, lakes, and rivers can alter the ecology of waterborne pathogens, creating more favorable conditions for their growth and survival. A critical example is the proliferation of bacteria from the genus *Vibrio* (e.g., *Vibrio vulnificus*), which are naturally found in warm coastal and estuarine waters and can cause severe wound infections, gastroenteritis, and septicemia [@problem_id:4510870].

The replication rate of many bacteria, including *Vibrio*, is strongly dependent on temperature. Within their viable range, warmer temperatures increase metabolic and enzymatic activity, leading to faster growth. This relationship is often quantified using the **$Q_{10}$ [temperature coefficient](@entry_id:262493)**, which describes the factor by which the rate of a biological process increases for every $10^\circ\mathrm{C}$ rise in temperature. A typical $Q_{10}$ value for [bacterial growth](@entry_id:142215) is 2. The change in growth rate ($r$) can be modeled as:

$$ \frac{r(T_2)}{r(T_1)} = Q_{10}^{\frac{T_2 - T_1}{10}} $$

If the steady-state concentration of bacteria in the water is proportional to their growth rate, a $4^\circ\mathrm{C}$ increase in sea surface temperature (SST) from $22^\circ\mathrm{C}$ to $26^\circ\mathrm{C}$, with $Q_{10} = 2$, would increase *Vibrio* concentrations by a factor of $2^{(26-22)/10} = 2^{0.4} \approx 1.32$.

This environmental change can be translated into a human health risk using a **Quantitative Microbial Risk Assessment (QMRA)** framework. The increased concentration leads to a higher dose of pathogens entering an open wound during recreational water activities. This dose ($D$) can then be used in a dose-response model to estimate the probability of infection ($P_{\text{inf}}$). A common model is the exponential dose-response function:

$$ P_{\text{inf}} = 1 - e^{-\beta D} $$

where $\beta$ is a parameter describing the infectivity of the pathogen. Following our example, the $\sim32\%$ increase in *Vibrio* concentration leads to a $\sim32\%$ increase in the ingested dose, which in turn elevates the probability of a wound infection from approximately $1.0\%$ to $1.3\%$ [@problem_id:4510870]. This demonstrates a clear mechanistic chain from warming waters to increased risk of marine infections.

#### Vector-Borne Infectious Diseases: Modifying Transmission Dynamics

Climate change is a potent driver of the geographic range and transmission intensity of many vector-borne diseases, such as malaria, dengue, and Lyme disease. Temperature, precipitation, and humidity directly influence the survival, reproduction, and behavior of vectors like mosquitoes and ticks, as well as the development rate of the pathogens they carry.

The transmission potential of a [vector-borne disease](@entry_id:201045) in a susceptible population is encapsulated by the **basic reproduction number, $R_0$**, defined as the expected number of secondary human infections generated by a single primary infectious human. If $R_0 > 1$, the disease can spread; if $R_0  1$, it will die out. A foundational model for $R_0$ in a mosquito-borne disease system is [@problem_id:4510895]:

$$ R_0 = \frac{m a^2 b c p^n}{r(-\ln p)} $$

Each parameter in this equation is influenced by climate:
*   $m$: The density of mosquitoes relative to humans.
*   $a$: The mosquito-to-human biting rate. Warmer temperatures can increase mosquito metabolic activity and biting frequency. Note its presence as $a^2$, reflecting two transmission steps (human-to-mosquito and mosquito-to-human), which makes $R_0$ highly sensitive to this parameter.
*   $b, c$: The probabilities of transmission per bite from mosquito to human ($b$) and human to mosquito ($c$).
*   $r$: The rate at which humans recover from infection.
*   $p$: The daily [survival probability](@entry_id:137919) of the mosquito vector. The denominator term $(-\ln p)$ is the daily mortality rate, $\mu$, so its inverse, $1/(-\ln p)$, represents the expected lifespan of the mosquito. Survival is temperature-dependent, often peaking at an optimal temperature and declining at colder or hotter extremes.
*   $n$: The duration of the **Extrinsic Incubation Period (EIP)**, the time required for a pathogen to develop inside the vector to the point where it can be transmitted. This process is highly temperature-dependent, with warming generally shortening the EIP.

The term $p^n$ is particularly critical: it represents the probability that a mosquito will survive long enough to complete the EIP and become infectious. Because $n$ is in the exponent, even a small decrease in the EIP due to warming can dramatically increase this probability, and thus substantially increase $R_0$. For example, a warming trend that shortens the EIP while increasing the biting rate could significantly increase transmission potential, even if it also causes some heat stress that slightly reduces mosquito survival ($p$) [@problem_id:4510895]. The ultimate impact of climate change on [vector-borne disease](@entry_id:201045) risk depends on the complex interplay of these competing effects on different parameters.

### Advanced Topics in Assessment and Policy

Building on these foundational principles, the field employs sophisticated methods to project future risks, attribute observed impacts to [climate change](@entry_id:138893), and evaluate the health benefits of climate policy.

#### Projecting Future Impacts: The RCP-SSP Framework

To project future health burdens, researchers must make assumptions about both the future climate and the future state of society. The IPCC has developed a scenario framework for this purpose, based on **Representative Concentration Pathways (RCPs)** and **Shared Socioeconomic Pathways (SSPs)** [@problem_id:4510858].

**Representative Concentration Pathways (RCPs)** describe different trajectories of greenhouse gas concentrations over the 21st century, leading to specific levels of [radiative forcing](@entry_id:155289) by the year 2100. They range from the low-emission RCP 2.6 (forcing of $2.6 \, W/m^2$) to the high-emission RCP 8.5 (forcing of $8.5 \, W/m^2$). RCPs are used as inputs for Earth System Models (ESMs) to project future climate conditions (e.g., temperature, precipitation).

**Shared Socioeconomic Pathways (SSPs)** are narratives that describe plausible alternative futures for socioeconomic development, independent of [climate change](@entry_id:138893). They project variables like [population growth](@entry_id:139111), age structure, urbanization, education, and economic development. The five core SSPs span a range of futures from SSP1 (Sustainability) to SSP3 (Regional Rivalry) and SSP5 (Fossil-fueled Development). These pathways determine a population's future vulnerability by defining its exposure, sensitivity, and [adaptive capacity](@entry_id:194789).

A coherent health impact projection requires pairing plausible RCPs and SSPs. For example, a high-mitigation world leading to RCP 2.6 is more plausible under the socioeconomic conditions of SSP1 than under SSP5. The state-of-the-art workflow involves selecting these plausible scenarios, using ensembles of multiple climate models to capture climate uncertainty, downscaling the climate projections to a local scale, and feeding the climate and socioeconomic projections into a health impact function. This allows for estimation of a range of future health burdens, complete with uncertainty bounds reflecting both climate model and socioeconomic scenario uncertainty [@problem_id:4510858].

#### Causal Attribution: Linking Health Outcomes to Climate Change

A rapidly advancing area of climate and health science is **causal attribution**, which seeks to answer questions like, "To what extent did anthropogenic [climate change](@entry_id:138893) contribute to the mortality observed during a specific heatwave?" This is accomplished using a **counterfactual framework**, which compares outcomes in the real, observed world with outcomes in a hypothetical world that might have been without anthropogenic climate change [@problem_id:4510872].

There are two main types of attribution:
1.  **Event Attribution**: This focuses on the role of climate change in a specific, extreme weather event. To quantify the mortality attributable to climate change during a heatwave, one compares the deaths that occurred at the observed temperatures ($T_{\text{obs}}$) with the deaths that would have occurred under the counterfactual temperatures for that same event had it unfolded in a pre-industrial climate ($T_{\text{cf}}$). Climate models are used to estimate this temperature difference (e.g., finding that the heatwave was $1.5^\circ\mathrm{C}$ hotter due to climate change). The attributable mortality is then the sum of the difference in daily deaths:
    
    $$ \text{Attributable Deaths (Event)} = \sum_{\text{event days}} m_0 \cdot [RR(T_{\text{obs}}(d)) - RR(T_{\text{cf}}(d))] $$
    
    where $m_0$ is baseline mortality and $RR(T)$ is the exposure-[response function](@entry_id:138845). This isolates the portion of the death toll caused specifically by the anthropogenic warming component of the event.

2.  **Trend Attribution**: This assesses the long-term impact of [climate change](@entry_id:138893) on seasonal or annual health burdens. It compares the total expected mortality under the current, anthropogenically-altered distribution of temperatures ($f_{\text{obs}}(T)$) with the mortality that would be expected under the counterfactual distribution without climate change ($f_{\text{cf}}(T)$). The attributable mortality over a season of $N$ days is:

    $$ \text{Attributable Deaths (Trend)} = N \cdot [\mathbb{E}_{T \sim f_{\text{obs}}}[m_0 \cdot RR(T)] - \mathbb{E}_{T \sim f_{\text{cf}}}[m_0 \cdot RR(T)]] $$

    This approach quantifies the total burden from the persistent, [climate change](@entry_id:138893)-driven shift in the entire temperature distribution, not just its effect on a single event [@problem_id:4510872].

#### Climate Action and Health: The Concept of Co-Benefits

While [climate change](@entry_id:138893) poses immense threats to public health, actions taken to mitigate climate change—that is, to reduce greenhouse gas emissions—can yield substantial and immediate health improvements. These ancillary health gains are known as **health co-benefits** [@problem_id:4510853]. Framing climate action in terms of these immediate, local health gains can be a powerful motivator for policy.

Health co-benefits arise through two main pathways:
1.  **Direct Pathways**: Many sources of [greenhouse gases](@entry_id:201380), particularly the burning of fossil fuels, also release hazardous air pollutants like fine particulate matter ($PM_{2.5}$) and [sulfur dioxide](@entry_id:149582) ($SO_2$). Climate policies that transition energy systems to clean sources like wind and solar directly reduce these co-pollutants, leading to immediate improvements in air quality and reductions in cardiovascular and respiratory diseases.
2.  **Indirect Pathways**: Some mitigation policies promote behavioral changes that also improve health. For example, policies that invest in public transit and active transport infrastructure (e.g., bike lanes, pedestrian-friendly streets) aim to reduce vehicle emissions. A major co-benefit of these policies is an increase in physical activity, which independently reduces the risk of numerous chronic diseases, including heart disease, diabetes, and some cancers.

The magnitude of these co-benefits can be substantial. For example, a quantitative assessment might find that a city's policy to retrofit its energy sector, which reduces annual average $PM_{2.5}$ by $3\,\mu\text{g/m}^3$, could avoid approximately 180 deaths per year. Simultaneously, a transportation policy that encourages 200,000 previously inactive adults to become physically active could avoid approximately 360 deaths per year [@problem_id:4510853]. By quantifying these health co-benefits, public health professionals can make a strong case that climate mitigation is not just a long-term environmental strategy, but an immediate public health imperative.