## Introduction
The burden of neurological disease is not distributed equally across the globe. From stroke and epilepsy to dementia and Parkinson's disease, vast disparities exist in incidence, prevalence, and access to care, creating profound inequities in health outcomes. Addressing this challenge requires more than clinical expertise; it demands a rigorous, systematic framework for measuring the problem, understanding its root causes, and designing equitable solutions. This article provides such a framework, moving from foundational principles to real-world application.

To equip you with the necessary tools, this exploration is structured across three key chapters. The first chapter, **Principles and Mechanisms**, lays the theoretical groundwork, introducing the essential metrics for quantifying disease burden and unpacking the complex social, genetic, and systemic factors that produce health disparities. The second chapter, **Applications and Interdisciplinary Connections**, bridges theory and practice, demonstrating how these principles are applied to design and evaluate interventions through connections with fields like health economics, genetics, and public policy. Finally, the **Hands-On Practices** chapter allows you to apply these concepts to solve practical problems in global health. We begin by establishing the quantitative language needed to describe and compare the burden of neurological disease across diverse populations.

## Principles and Mechanisms

### Quantifying the Burden of Neurological Disease

To understand and address global neurological health disparities, we must first possess a rigorous and standardized toolkit for measurement. Comparing the burden of disease across different populations is not a trivial task; it requires a set of well-defined metrics that can capture the multifaceted impact of illness on human life. These metrics form the quantitative foundation of global health policy and research.

#### Core Metrics of Disease Burden

The most fundamental measures in population health are **incidence**, **prevalence**, and **mortality**. **Incidence** quantifies the rate at which new cases of a disease emerge in a population over a specified time period. It is a measure of risk. **Prevalence** measures the proportion of a population that has a disease at a single point in time (point prevalence) or over a period (period prevalence). It reflects the existing burden of a condition. **Mortality** measures the rate at which deaths attributable to the disease occur.

While indispensable, these three metrics do not tell the whole story. Consider a hypothetical comparison of a neurological disorder between two countries, Country H and Country L, each with a population of $8{,}000{,}000$ [@problem_id:4482913]. Country H reports $4{,}000$ new cases, $32{,}000$ existing cases, and $160$ deaths in a year. Country L reports $3{,}200$ new cases, $20{,}000$ existing cases, and $300$ deaths. The corresponding rates per $100{,}000$ population are:

- Country H: Incidence $50$, Prevalence $400$, Mortality $2$.
- Country L: Incidence $40$, Prevalence $250$, Mortality $3.75$.

From these crude rates, we see that Country H has a higher incidence and prevalence, suggesting a larger number of people are becoming sick and living with the disease. However, Country L has a nearly twofold higher mortality rate. This simple comparison already reveals a complex picture: is the burden greater where more people get sick, or where more people die? To resolve this, we need more sophisticated, summary measures of population health.

The **Disability-Adjusted Life Year (DALY)** is the principal metric used in global burden of disease studies to provide such a summary. The DALY conceives of disease burden as the total number of healthy life years lost by a population, combining years lost to premature death with years lived in states of less-than-full health. It is the sum of two components: Years of Life Lost (YLL) and Years Lived with Disability (YLD).

$DALY = YLL + YLD$

**Years of Life Lost (YLL)** quantifies the burden from premature mortality. It is calculated for each death as the difference between the age at death and a standard life expectancy at that age. Returning to our example, suppose the median age at death from the disorder in Country H is $75$ years, where the standard remaining life expectancy is $12$ years. In Country L, the median age at death is much younger, $50$ years, with a standard remaining life expectancy of $30$ years [@problem_id:4482913]. The total YLL for each country is the number of deaths multiplied by the years lost per death.

- Country H: $YLL = 160 \text{ deaths} \times 12 \text{ years/death} = 1{,}920 \text{ years}$.
- Country L: $YLL = 300 \text{ deaths} \times 30 \text{ years/death} = 9{,}000 \text{ years}$.

Expressed as a rate per $100{,}000$ population, Country H has a YLL rate of $24$, while Country L has a rate of $112.5$. This illustrates a critical principle: YLL is highly sensitive to the age at which death occurs. Country L suffers a much greater burden from premature mortality, not just because it has more deaths, but because those deaths occur at a much younger age, representing a greater loss of potential life.

**Years Lived with Disability (YLD)** quantifies the burden from non-fatal health outcomes (morbidity). It is calculated by multiplying the number of prevalent cases of a condition by a **disability weight (DW)** that reflects the severity of the health state.

$YLD = \text{Prevalent Cases} \times \text{Disability Weight}$

A **disability weight** is a scalar value on a scale from $0$ to $1$, where $0$ signifies a state of full health and $1$ signifies a state equivalent to death. It represents the proportion of health lost due to a specific condition. These weights are a critical component of the Global Burden of Disease (GBD) methodology and are derived from large-scale surveys of the general population about their preferences for different health states. It is crucial to distinguish a disability weight from three related concepts [@problem_id:4482887]:
1.  **Clinical Severity Classification**: These are categorical labels used by clinicians (e.g., "mild," "moderate," "severe"). A disability weight is a quantitative value assigned to a health state, which may be informed by but is not identical to a clinical category.
2.  **Health State Utility**: This metric is used in the calculation of **Quality-Adjusted Life Years (QALYs)**, a measure common in cost-effectiveness analysis. A utility weight scale is inverted relative to a disability weight: $1$ represents full health and $0$ represents death. Conceptually, for a given health state, the two are related by the formula $DW \approx 1 - \text{Utility}$.
3.  **Context-Specific Valuation**: A core principle of the GBD framework is that disability weights are universal. They are intended to represent the intrinsic severity of a health state, independent of an individual's geographic location or socioeconomic status. Disparities are captured by differences in incidence, prevalence, and mortality, not by adjusting the weights themselves.

In our example, suppose the neurological disorder in Country H is associated with a lower disability weight ($DW_H = 0.25$) than in Country L ($DW_L = 0.35$), perhaps reflecting differences in typical disease severity or access to mitigating treatments. The YLD per $100{,}000$ population can then be calculated [@problem_id:4482913]:

- Country H: $YLD = \frac{32{,}000 \text{ cases} \times 0.25}{8{,}000{,}000} \times 100{,}000 = 100$.
- Country L: $YLD = \frac{20{,}000 \text{ cases} \times 0.35}{8{,}000{,}000} \times 100{,}000 = 87.5$.

Here we see that Country H, despite its lower mortality burden, has a higher non-fatal burden, driven by its much higher prevalence of the condition.

By summing the YLL and YLD rates, we can finally compute the total DALY rate for each country:

- Country H: $DALY = 24 (YLL) + 100 (YLD) = 124$ per $100{,}000$.
- Country L: $DALY = 112.5 (YLL) + 87.5 (YLD) = 200$ per $100{,}000$.

The DALY provides a single, comprehensive measure that allows for a summary comparison. It reveals that the total health loss from this neurological disorder is substantially greater in Country L. This is driven by its high burden of premature mortality (high YLL), which outweighs its lower non-fatal burden (lower YLD). The DALY framework thus enables a nuanced comparison that integrates the distinct impacts of incidence, prevalence, mortality, age at death, and disability severity.

#### Methodological Refinements for Fair Comparison

Calculating these core metrics is only the first step. To ensure that comparisons of disease burden between populations are fair and meaningful, we must address potential methodological biases. Two crucial refinements are age-standardization and comorbidity correction.

A common challenge in comparing disease rates across countries is that populations can have vastly different age structures. This is a significant problem for conditions like stroke, where the risk increases steeply with age. A country with an older population will naturally have a higher crude incidence of stroke, even if the underlying, age-specific risk is identical to that of a younger country. This phenomenon, where a third variable (age) is associated with both the population of interest (country) and the outcome (stroke), is a classic example of **confounding**.

To overcome this, epidemiologists use **age-standardization**, a technique that creates a counterfactual comparison by controlling for differences in age structure. The most common approach is the **direct method**, where the age-specific rates from each study population are applied to a single, common **standard population**. This yields an age-standardized rate, which is a weighted average of the age-specific rates, but where the weights are derived from the standard population's age distribution. This allows for a comparison of what the rates *would be* if the populations had the same age structure. The **indirect method** is an alternative used when stable age-specific rates are not available for a study population; it involves applying a standard set of rates to the study population's age structure to compute an expected number of cases.

Consider a comparison of stroke incidence between Country L, with a young population, and Country H, with an older population [@problem_id:4482917]. Let's say the crude incidence rate in Country L is $215$ per $100{,}000$ and in Country H is $387$ per $100{,}000$. A naive comparison would suggest that stroke risk is much higher in Country H. However, we know Country H has a much larger proportion of its population in older age groups where stroke is more common. If we apply the direct standardization method, using the age-specific rates from each country but weighting them by the structure of a common standard population, the conclusion may be dramatically different. In the scenario presented in the problem, the age-standardized rate for Country L becomes $342.5$ and for Country H becomes $279.0$. After controlling for the confounding effect of age, Country L actually has a higher underlying risk of stroke. This reversal underscores that comparing crude rates for age-dependent diseases across populations with different demographic profiles is misleading and that age-standardization is an essential tool for valid cross-national comparisons.

A second major challenge is accounting for **comorbidity**, the co-occurrence of multiple health conditions in the same individual. Neurological disorders frequently co-occur, for instance, post-stroke cognitive impairment and epilepsy. A simple approach to calculating the total YLD burden would be to sum the YLDs attributable to each condition separately. However, this would effectively double-count the time lived with disability for individuals suffering from both conditions.

The GBD framework addresses this with **comorbidity correction** [@problem_id:4482930]. The standard method assumes that the disabling effects of different conditions are independent and uses a multiplicative model on the *residual health* (the proportion of health an individual retains). If an individual has two conditions with disability weights $w_1$ and $w_2$, the combined disability weight, $w_{1,2}$, is not the simple additive sum $w_1 + w_2$. Instead, it is calculated as:
$$w_{1,2} = 1 - (1 - w_1)(1 - w_2)$$

This formula ensures that the total disability weight cannot exceed $1$. For example, if a person has post-stroke impairment ($w_S = 0.35$) and epilepsy ($w_E = 0.20$), the combined weight is $w_{S,E} = 1 - (1-0.35)(1-0.20) = 1 - (0.65)(0.80) = 0.48$. This is less than the simple additive sum of $0.35 + 0.20 = 0.55$. The difference, $w_S w_E = 0.07$, represents the overlap in disability that would be double-counted by the additive approach.

Failing to apply this correction inflates the total YLD estimate. The magnitude of this inflation is proportional to the prevalence of comorbidity in the population. Therefore, in a population with a higher rate of multimorbidity, the uncorrected YLD estimate will be more exaggerated. This can artificially inflate estimates of health disparities between high- and low-comorbidity populations [@problem_id:4482930]. Comorbidity correction is thus a vital methodological principle for obtaining accurate and comparable estimates of disease burden.

### Unpacking the Mechanisms of Disparity

Having established how to measure neurological health disparities, we now turn to the mechanisms that produce them. Disparities do not arise in a vacuum; they are the result of a complex interplay of social, economic, environmental, and biological factors.

#### The Social and Structural Determinants of Neurological Health

The dominant framework for understanding the root causes of health inequities is that of the **social determinants of health (SDH)**. As defined by the World Health Organization (WHO) Commission on Social Determinants of Health (CSDH), these are "the conditions in which people are born, grow, live, work, and age." Crucially, these conditions are themselves shaped by the distribution of money, power, and resources at global, national, and local levels [@problem_id:4482953].

The CSDH framework distinguishes between two broad categories of determinants, which can be conceptualized in a causal pathway: $X_s \rightarrow X_i \rightarrow \text{Health Outcome}$.

1.  **Structural Determinants ($X_s$)**: These are the "upstream" socioeconomic and political contexts that create social stratification and assign individuals to different socioeconomic positions. They include macro-level factors like governance, fiscal and trade policies, educational systems, labor market structures, and societal norms around gender and ethnicity. For example, a national policy on salt taxation or tobacco marketing is a structural determinant that shapes the environment in which health-related choices are made.

2.  **Intermediary Determinants ($X_i$)**: These are the "downstream" factors that flow from the structural determinants and more directly influence health outcomes. They include material circumstances (e.g., quality of housing, food availability, exposure to air pollution), psychosocial factors (e.g., stress, social support), behavioral and biological factors (e.g., diet, smoking, hypertension), and the health system itself (e.g., access to and quality of care).

For instance, in the context of stroke risk in a low-resource setting, structural determinants like weak regulation of the food industry ($X_s$) can lead to intermediary determinants like widespread household food insecurity and the availability of cheap, high-sodium processed foods ($X_i$). This, in turn, contributes to a high prevalence of hypertension ($X_i$), a primary biological risk factor that directly increases the hazard of stroke [@problem_id:4482953]. This framework moves the focus of explanation and intervention from individual "lifestyle choices" to the societal structures that shape those choices.

The impact of these determinants is often visible in the performance of health systems. The concept of a **cascade of care** is a useful tool for tracking patients through the health system and quantifying points of failure. For a chronic condition like [epilepsy](@entry_id:173650), this cascade includes being diagnosed, being initiated on appropriate treatment, and adhering to that treatment. Failures at each step can be measured as "gaps." Based on the principle that a gap is the proportion of a population in need that is not receiving a service, we can define several key metrics [@problem_id:4482920]:

-   **Diagnostic Gap**: The proportion of people with active [epilepsy](@entry_id:173650) who do not have a diagnosis.
    $$\text{Diagnostic Gap} = \frac{N_{\text{active}} - N_{\text{diagnosed}}}{N_{\text{active}}}$$

-   **Treatment Gap**: The proportion of people with active [epilepsy](@entry_id:173650) who are not receiving appropriate anti-seizure medication (ASM). This is a widely cited metric in global neurology.
    $$\text{Epilepsy Treatment Gap} = \frac{N_{\text{active}} - N_{\text{ASM}}}{N_{\text{active}}}$$

-   **Adherence Gap**: The proportion of people *on treatment* who are not sufficiently adherent. The denominator here is crucial: it is the population receiving ASM, as one cannot be non-adherent to a treatment one is not taking.
    $$\text{Adherence Gap} = \frac{N_{\text{ASM}} - N_{\text{adherent}}}{N_{\text{ASM}}}$$

These gaps are quantitative manifestations of barriers within the intermediary determinants—specifically, the health system. A large treatment gap, for example, may reflect poor access to trained health personnel, stockouts of essential medicines, or high out-of-pocket costs, all of which are shaped by higher-level structural determinants related to health system financing and policy.

#### Genetic Ancestry and Population History

While social determinants are paramount, population history and genetic ancestry can also contribute to disparities in the burden of certain neurological diseases. The distribution of genetic variants is not uniform across the globe; it has been shaped by migration, selection, and random genetic drift. Three key concepts from population genetics are essential for interpreting these patterns: population stratification, founder effects, and admixture.

**Population stratification** refers to systematic differences in allele frequencies between subpopulations. This is a pattern, not a process. When this pattern is not accounted for in [genetic association](@entry_id:195051) studies, it can lead to spurious associations. For example, if a variant is more common in a subpopulation that also has a higher risk of disease for non-genetic reasons (e.g., due to shared environmental or social exposures), the variant may appear to be associated with the disease even if it has no causal role.

A **[founder effect](@entry_id:146976)** is a powerful [evolutionary process](@entry_id:175749) that can create significant [population stratification](@entry_id:175542). It occurs when a new population is established by a small number of individuals ("founders") whose [gene pool](@entry_id:267957) may differ by chance from the source population. A rare allele present in one of the founders can, through this sampling event and subsequent genetic drift in the small, isolated population, rise to a much higher frequency than in the ancestral population. The genomic signature of a classic [founder effect](@entry_id:146976) is distinctive: a large proportion of carriers of the allele will share a long, identical chromosomal segment, or **haplotype**, surrounding the allele, inherited from the common founder ancestor. Carriers will also exhibit excess genome-wide relatedness (**Identity-By-Descent**, or IBD) compared to non-carriers from the same population. The expected length of this shared haplotype decays over time, providing a [molecular clock](@entry_id:141071) to date the founding event [@problem_id:4482936]. For a founder event occurring $t$ generations ago, the expected length of an IBD tract shared between two descendants is approximately $1/(2t)$ Morgans.

**Admixture** is the process of interbreeding between two or more previously distinct populations. This results in the formation of a new, admixed population whose members have ancestry from the multiple source populations. Admixture can serve as a mechanism to introduce alleles—including founder alleles—from one population into another. In a recently admixed population, the allele frequency of a variant is expected to be the weighted average of the frequencies in the source populations, with weights given by the ancestry proportions. The chromosomes of admixed individuals are mosaics of "local [ancestry tracts](@entry_id:166625)" from the source populations, and the average length of these tracts, which is approximately $1/t$ Morgans for an admixture event $t$ generations ago, can be used to estimate its timing [@problem_id:4482936].

These concepts are powerfully illustrated in a study of a movement disorder across three populations: an isolated highland population (X), a neighboring lowland population (Y), and a recently urbanized, admixed population (U). If population X experienced a founder event $\approx 16$ generations ago, we would expect a pathogenic allele to be at high frequency, and for carriers to share, on average, an IBD segment of approximately $1/(2 \times 16) = 1/32$ Morgans (or $\approx 3.13$ centiMorgans) in length. If population U was formed by admixture between X and Y $\approx 9$ generations ago, we would expect the allele to be present at an intermediate frequency, primarily on chromosome segments of X-ancestry with an average length of around $1/9$ Morgans ($\approx 11.1$ cM). These quantitative predictions allow geneticists to piece together population history and understand the origins of elevated disease risk in certain communities [@problem_id:4482936].

#### Threats to Validity in Disparities Research

Identifying the mechanisms driving disparities, whether social or genetic, depends on rigorous observational research. However, such research is fraught with potential biases that can lead to incorrect conclusions. A critical skill for researchers in global neurology is the ability to identify and mitigate these threats to validity. Three of the most important are confounding, selection bias, and measurement error. These are best understood using the language of causal diagrams (Directed Acyclic Graphs, or DAGs) [@problem_id:4482922].

**Confounding** occurs when a pre-exposure variable, $C$, is a common cause of both the exposure, $A$, and the outcome, $Y$. This creates a non-causal "backdoor" path between $A$ and $Y$ ($A \leftarrow C \rightarrow Y$). For example, in an [observational study](@entry_id:174507) of thrombolysis ($A$) for acute stroke, baseline stroke severity ($C$) is a powerful confounder. Patients with milder strokes may be more likely to receive treatment and are also independently more likely to have a good outcome ($Y$). Failing to adjust for severity will spuriously attribute the good outcomes of the mildly affected patients to the treatment, biasing the estimated effect upwards and overstating the treatment's benefit.

**Selection bias** arises when the study population is selected in a way that is dependent on both the exposure and the outcome. A particularly insidious form is **collider-stratification bias**. A "[collider](@entry_id:192770)" is a variable that is caused by two other variables (e.g., $A \rightarrow S \leftarrow Y$). Conditioning on a [collider](@entry_id:192770) (e.g., by restricting the analysis to a specific level of $S$) can open a non-causal path between its causes, $A$ and $Y$. In a multi-country stroke registry, for example, if data completeness ($S=1$) is higher for treated patients ($A=1$) and for those who have good outcomes ($Y=1$), then restricting the analysis to only those with complete records is conditioning on a collider. Within the group of patients with complete data, an untreated patient may be more likely to have had a good outcome (as the good outcome "explains" their inclusion), creating a spurious association that distorts the true treatment effect. Unlike confounding, this bias cannot be fixed by adjusting for pre-exposure variables.

**Measurement error** refers to inaccuracies in measuring exposures, outcomes, or covariates. The effect of measurement error depends on its nature. **Nondifferential misclassification** occurs when the probability of measurement error is the same across the groups being compared. For example, if the outcome (e.g., favorable functional status on the Modified Rankin Scale, mRS) is misclassified with the same error rate in both the treated and untreated groups, this is nondifferential outcome misclassification. For a dichotomous outcome, this type of error generally biases the estimated effect (e.g., the risk difference or odds ratio) towards the null value of no effect. This is called **attenuation** and can lead researchers to incorrectly conclude that an effective intervention is useless.

### Ethical Frameworks for Research and Intervention

The ultimate goal of studying health disparities is to reduce them. This requires not only scientific understanding but also a firm ethical foundation for both the research we conduct and the interventions we implement.

#### Principles of Neuroethics in Global Health

Research in low-resource settings, particularly among vulnerable populations, demands scrupulous attention to ethics. Four principles, derived from foundational [bioethics](@entry_id:274792), are paramount in the context of global neurology [@problem_id:4482911].

1.  **Respect for Persons**: This principle asserts that individuals have intrinsic moral worth and the right to self-determination. In research, this translates to the requirement for voluntary, informed consent. In settings with low literacy or fluctuating capacity (as can occur in [epilepsy](@entry_id:173650)), this principle demands more than a signature on a form. It requires robust processes like interpreter-supported discussions, "teach-back" methods to ensure comprehension, and the involvement of independent bodies like a Community Advisory Board (CAB) to ensure cultural appropriateness.

2.  **Beneficence**: This principle entails an obligation to maximize potential benefits and minimize potential harms. For a clinical study, this requires a rigorous risk-benefit assessment. In the context of resource scarcity, it also implies a duty to use those resources to achieve the greatest good. For example, allocating scarce resources like an investigational drug or EEG access should be guided by transparent clinical criteria aimed at identifying patients with the greatest need or capacity to benefit, rather than by arbitrary methods like a lottery or first-come-first-served.

3.  **Justice**: This principle demands the fair distribution of the burdens and benefits of research and intervention. It requires equitable selection of participants, avoiding the exploitation of vulnerable groups. In a resource-scarce setting, tying access to essential clinical care (e.g., compassionate use medication) to participation in a research trial constitutes undue inducement and is unjust. Justice may also require proactive measures, such as applying equity weights in allocation decisions, to ensure that existing social disadvantages are not exacerbated.

4.  **Reciprocity**: This principle recognizes that research is a partnership between researchers and communities. It creates a mutual obligation to ensure that the host community, which bears the risks and burdens of research, also shares fairly in its benefits. This goes beyond individual compensation. It includes commitments to **capacity-building** (e.g., training local staff), ensuring **reasonable post-trial access** to interventions found to be effective, and sharing data and governance with local health authorities to strengthen the health system.

These four principles are not abstract ideals; they are practical guides to action. An ethically sound study in a global health context will demonstrate concrete strategies to realize each one, navigating the complex interplay between research goals and moral duties in a landscape of disparity [@problem_id:4482911].

#### Economic Evaluation and Equity

When moving from research to policy, decisions must be made about how to allocate finite resources. Health economics provides tools to guide these decisions, but they must be used in a way that is sensitive to the ethical imperative of reducing disparities.

Standard **Cost-Effectiveness Analysis (CEA)** evaluates interventions based on their efficiency in producing health. Two key metrics are the **Incremental Cost-Effectiveness Ratio (ICER)** and the **Net Monetary Benefit (NMB)** [@problem_id:4482893].

The **ICER** is the additional cost of an intervention divided by the additional health gain it produces (typically measured in QALYs).
$$ICER = \frac{\Delta C}{\Delta E}$$
A decision rule is to accept an intervention if its ICER is below a societal **willingness-to-pay (WTP)** threshold, $\lambda$, representing the maximum amount society is willing to pay for one QALY.

The **NMB** framework monetizes the health gains and compares them directly to the costs.
$$NMB = (\lambda \times \Delta E) - \Delta C$$
The decision rule is to accept an intervention if its NMB is greater than zero, which is algebraically equivalent to the ICER rule ($ICER  \lambda$).

While powerful, standard CEA is "equity-blind." It values a QALY gained by a wealthy person the same as a QALY gained by a poor person. An intervention that is highly effective for a disadvantaged group but only moderately effective for a larger, more advantaged group might be rejected on aggregate cost-effectiveness grounds, even if it would reduce health inequity.

Consider a community [epilepsy](@entry_id:173650) program that produces a larger health gain per person for a low-socioeconomic status (SES) group than for a high-SES group, but is also more costly for the high-SES group. A standard CEA might find that the overall program has an ICER of \$556/QALY. If the WTP threshold is \$500/QALY, the program would be rejected as not cost-effective [@problem_id:4482893].

**Distributional Cost-Effectiveness Analysis (DCEA)** is an extension of CEA that explicitly incorporates equity concerns. One approach is to apply **equity weights** to the health gains of different population subgroups. For example, a planner might assign a higher weight ($w_{\text{low}} > 1$) to QALYs gained by the low-SES group and a baseline weight ($w_{\text{high}} = 1$) to the high-SES group. The decision can then be based on an equity-weighted NMB:
$$NMB^{W} = (\lambda \times \sum_i w_i \Delta E_i) - \sum_i \Delta C_i$$

In our [epilepsy](@entry_id:173650) program example, applying an equity weight of $w_{\text{low}}=2$ for the low-SES group could reverse the decision. The equity-weighted health gains, when monetized, might now exceed the total costs, yielding a positive $NMB^{W}$. This would lead to a recommendation to adopt the program, a conclusion that aligns with the goal of improving health and promoting equity simultaneously. DCEA thus provides a formal analytical bridge between the economic logic of efficiency and the ethical principle of justice.