## Introduction
In a world where decisions made in transportation, housing, and economic development profoundly affect public health, a systematic method for evaluating these impacts is essential. Health Impact Assessment (HIA) emerges as this critical tool, providing a structured framework to predict the health consequences of policies, particularly those outside the traditional health sector. The central challenge HIA addresses is the frequent disconnect between policymaking and health outcomes, often leading to unintended negative consequences and widening health inequities. This article provides a comprehensive guide to the HIA methodology, designed to bridge this gap by embedding health evidence and equity considerations directly into the decision-making process.

Over the next three chapters, you will gain a deep understanding of this vital methodology. The first chapter, **Principles and Mechanisms**, dissects the core components of the HIA process, from establishing causal pathways to quantifying health effects and analyzing uncertainty. Next, **Applications and Interdisciplinary Connections** demonstrates how HIA is applied in real-world scenarios, such as urban planning and climate policy, showcasing its role in advancing health equity and informing complex decisions. Finally, **Hands-On Practices** will allow you to apply key quantitative techniques, solidifying your ability to translate theory into practice. By navigating these sections, you will be equipped with the knowledge to use HIA as a powerful tool for promoting and protecting population health.

## Principles and Mechanisms

This chapter delves into the core principles and methodological mechanisms that underpin a rigorous Health Impact Assessment (HIA). Moving beyond the introductory concepts, we will dissect the structured process of an HIA, from its initial framing to the quantitative estimation of health effects and the critical analysis of equity. Our focus will be on the "how" and "why" of HIA, providing the conceptual tools necessary for its competent application.

### Situating HIA: A Framework for Health in All Policies

While the goal of protecting and improving health is shared across many disciplines, the methods used are tailored to specific objects of inquiry. Health Impact Assessment distinguishes itself from other related assessment frameworks, such as Environmental Impact Assessment (EIA), Risk Assessment (RA), and Health Technology Assessment (HTA), through its unique scope, perspective, and position in the decision-making cycle. Understanding these distinctions is fundamental to grasping the purpose of HIA.

-   **Object of Assessment**: The primary object of an **HIA** is a proposed policy, plan, program, or project, often originating *outside* the traditional health sector. Classic examples include urban planning decisions, transportation infrastructure, or economic policies. In contrast, **EIA** focuses on projects with significant effects on environmental media (air, water, soil); **RA** targets specific hazards (e.g., a chemical substance); and **HTA** evaluates a particular health technology (e.g., a drug, device, or procedure).

-   **Health Outcomes Considered**: HIA adopts a broad, holistic definition of health consistent with the World Health Organization, encompassing physical, mental, and social well-being. A defining feature is its explicit focus on **health equity**, examining the differential distribution of impacts across population subgroups. EIA, while considering health, primarily focuses on effects mediated by environmental pathways (e.g., respiratory illness from air pollution), rather than the broader social determinants of health. RA quantifies the probability and severity of specific, predefined adverse effects related to a hazard. HTA centers on clinical effectiveness, safety, and cost-effectiveness.

-   **Position in Decision Cycle**: HIA is fundamentally a tool for *ex-ante* appraisal, designed to inform and shape decisions *before* they are finalized. It is embedded within the policy cycle, providing recommendations to maximize health benefits and mitigate harms. EIA serves a similar ex-ante function, typically as a regulatory prerequisite for project approval. RA provides quantified risk characterizations to inform risk management decisions, while HTA informs coverage, reimbursement, and adoption decisions for specific technologies. [@problem_id:4533232]

By focusing on the upstream determinants of health embedded in public policy across all sectors, HIA serves as the principal methodological tool for the "Health in All Policies" (HiAP) strategy.

### The HIA Process: From Concept to Conclusion

An HIA follows a structured sequence of stages, including Screening, Scoping, Appraisal, Reporting, and Monitoring. The intensity and depth of this process are governed by a crucial meta-principle: proportionality.

#### The Principle of Proportionality

The resources invested in an HIA—time, funding, and analytical effort—should be proportional to the decision's potential significance. The appropriate level of HIA intensity, often categorized as **rapid**, **intermediate**, or **comprehensive**, is determined by balancing several factors:

-   **Magnitude of Potential Impact**: Policies expected to have large-scale health consequences warrant a more thorough investigation.
-   **Uncertainty**: Significant uncertainty about potentially large impacts calls for a more in-depth assessment to clarify risks before a decision is made.
-   **Reversibility**: Impacts that are difficult or costly to reverse (i.e., have high [irreversibility](@entry_id:140985)) demand greater scrutiny beforehand.
-   **Decision Timeline**: A practical constraint that dictates feasibility. A short deadline may preclude a comprehensive assessment, forcing a focus on the most critical questions.

For instance, consider a zoning change with a potentially moderate but highly uncertain and irreversible impact on respiratory health (e.g., an expected increase of $\Delta H = +15$ hospitalizations per $100{,}000$ person-years, with a wide $95\%$ confidence interval of $[+3, +40]$ and an irreversibility index of $0.8$). If the decision timeline is very short, say $t_d=6$ weeks, a full comprehensive HIA is impossible. The principle of proportionality directs us not to default to the most minimal option, but to conduct the most intensive assessment feasible within the given timeframe—in this case, likely a focused intermediate HIA—to adequately inform a high-stakes decision. [@problem_id:4533214]

#### Screening: The "Go/No-Go" Decision

**Screening** is the first step, a rapid process to determine whether a full HIA is warranted. The central question is: *Is the proposed policy likely to have significant health effects?* A decision to proceed is typically based on criteria such as:
- The potential magnitude and severity of health impacts.
- The size and vulnerability of the affected populations.
- The degree of stakeholder or community concern.
- The potential to affect health equity.

In some contexts, screening can be supported by a preliminary quantitative analysis. For example, if a proposed freight terminal is expected to affect $N=40{,}000$ residents with an annual increased risk of $\Delta r = 0.005$ for a health outcome with severity $s=3$ Quality-Adjusted Life Years (QALYs), and the probability of this scenario is $p=0.6$, the expected annual health loss is $E(L) = N \times \Delta r \times p \times s = 360$ QALYs. If this value exceeds a predefined significance threshold (e.g., $I_{\min}=100$ QALYs), it provides a strong justification to proceed with a more detailed assessment. This decision can be further bolstered by a value-of-information argument: if the monetized value of the expected health loss far exceeds the cost of the HIA, the assessment is a worthwhile investment. [@problem_id:4533260]

#### Scoping: Charting the Course

Once the decision to conduct an HIA is made, **scoping** sets its boundaries and creates a project plan. It determines *what* the HIA will cover and *how* it will be conducted. This involves identifying plausible causal pathways, defining the geographic and temporal boundaries, specifying the population subgroups of interest, and outlining the analytical methods.

The output of this stage is a formal **Terms of Reference (ToR)**, an agreed-upon document detailing the scope, objectives, methods, and deliverables. The ToR is a critical project management tool that provides clarity and focus. It is the primary defense against **scope creep**, which is the uncontrolled expansion of topics or tasks beyond the agreed-upon plan without formal justification and resource allocation.

A key task in scoping is to prioritize which health endpoints and causal pathways to analyze. Not every conceivable effect can be studied. Inclusion criteria should be scientifically sound and decision-relevant, requiring:
1.  A plausible causal pathway linking the policy to the health outcome.
2.  Potential for a significant impact in terms of magnitude, severity, or distribution.
3.  Relevance to the decision at hand (i.e., the analysis can influence policy design).
4.  Feasibility, given available data, time, and resources.

Pathways that are implausible, negligible, or cannot be analyzed in a way that would materially inform the decision should be excluded. [@problem_id:4533239]

### The Causal Core of HIA

At its heart, HIA is an exercise in applied causal inference. It seeks to answer the question: "What will be the health effect *caused by* this policy?" This requires moving beyond mere statistical association to build a plausible model of causation.

#### Causal Pathways

A **causal pathway** is a sequence of mechanisms linking an intervention to a subsequent change in a health outcome. For example, a policy to build protected bike lanes (intervention $E$) may lead to increased physical activity (mediator $M$), which in turn leads to a reduction in cardiovascular disease (outcome $O$). For a pathway to be considered causal, an intervention that sets the exposure to a certain level, denoted formally as $do(E=e)$, must result in a change in the distribution of the outcome.

To distinguish a causal relationship from a simple correlation, two conditions are paramount:
1.  **Temporality**: The cause must precede the effect. The policy implementation must happen before the change in health outcome is observed.
2.  **Control of Confounding**: A **confounder** is a common cause of both the exposure and the outcome. For instance, if residents in a high-income neighborhood both advocate for bike lanes and have better baseline health for other reasons (e.g., nutrition), income becomes a confounder that can create a spurious association between bike lanes and health. A rigorous HIA must identify and statistically control for such confounders to isolate the true causal effect of the policy itself. [@problem_id:4533254]

#### The Counterfactual

The causal effect of a policy is fundamentally a comparison between two potential worlds: the world *with* the policy and the world *without* it. In the potential outcomes framework, we estimate the health outcome if the policy is implemented, $Y(1)$, and compare it to the **counterfactual** outcome—the health outcome for the same population over the same period had the policy *not* been implemented, $Y(0)$. The average causal effect is the difference, $E[Y(1) - Y(0)]$.

Estimating the counterfactual $Y(0)$ requires defining a realistic **baseline scenario**. This is not simply a snapshot of the world today. For a prospective HIA looking into the future, the appropriate baseline is typically a **business-as-usual (BAU)** scenario. The BAU baseline projects how the future would unfold in the absence of the specific policy being assessed, but *inclusive* of all other known and committed changes. For example, when assessing a new Low-Emission Zone (LEZ), the BAU baseline should include the effects of any separate national emission standards or planned public transit projects that will happen anyway. Using a BAU baseline ensures that the HIA isolates the true *incremental* impact of the decision under consideration, providing the most relevant information to policymakers. [@problem_id:4533251]

### The Quantitative Engine: From Exposure to Impact

Quantitative HIA translates the logic of causal pathways and counterfactuals into numerical estimates of health impacts. This process can be broken down into several key components.

#### Defining and Measuring Exposure

**Exposure** is the contact between an environmental agent and the outer boundary of an organism, such as the breathing zone. The most biologically relevant measure is **personal exposure**, which integrates the concentration of an agent across all the different microenvironments an individual moves through over time. However, measuring personal exposure for a large population is often infeasible.

Therefore, HIAs typically rely on proxies. A common proxy is the **ambient concentration** measured at a fixed monitoring site, which is assigned to all individuals in a geographic area. This approach introduces a specific type of measurement error known as **Berkson error**. Because the assigned value is an average around which true personal exposures vary, this error structure, in linear models, does not typically bias the estimated [effect size](@entry_id:177181) but does reduce statistical power. Another common proxy is a categorical indicator, such as **proximity to a major road**. Using such a crude proxy introduces **nondifferential misclassification** of exposure, which generally biases the estimated health effect towards the null (i.e., it makes the effect appear weaker than it truly is). Understanding the type of exposure data being used and its associated biases is critical for interpreting HIA results. [@problem_id:4533234]

#### The Baseline Health Profile

To estimate the change in health, we must first know the starting point. A **baseline health profile** is a stratified, pre-intervention description of the health status and determinants of the population. It quantifies baseline rates of disease or death (e.g., annual incidence of asthma emergency department visits) for the total population and for specific subgroups defined by age, sex, income, or neighborhood. This profile serves two purposes: it provides the baseline risk to which changes will be applied, and its stratification is the essential foundation for analyzing health equity. [@problem_id:4533262]

#### The Exposure-Response Function (ERF)

The critical link between a change in exposure and a change in health risk is the **exposure-[response function](@entry_id:138845) (ERF)**, also known as a concentration-response function (CRF). Derived from epidemiological studies, an ERF is a mathematical mapping from exposure to a health risk metric. There are several common forms:

-   **Relative Risk (Multiplicative) Model**: The ERF provides a **relative risk** ($RR$), which is a dimensionless factor that scales the baseline risk. The new risk is calculated as $R(X) = R_0 \cdot RR(\Delta X)$, where $R_0$ is the baseline risk and $\Delta X$ is the change in exposure. To use this model, the baseline risk $R_0$ for the specific population under study is a required input.

-   **Excess Risk (Additive) Model**: The ERF provides an **excess risk** ($ER$), which is an absolute change in risk. The new risk is calculated as $R(X) = R_0 + ER(\Delta X)$. This model also requires the baseline risk $R_0$ as an input.

-   **Absolute Risk Model**: The ERF directly provides the absolute risk $R(X)$ for any given exposure level $X$. In this case, the baseline risk $R_0$ is not an independent input, but simply the value of the function at the baseline exposure level, $R(X_0)$.

The final estimate of the change in the number of health events is calculated by applying the change in risk to the population size for each relevant subgroup. [@problem_id:4533222]

### Health Equity: A Central Principle of HIA

A core mandate of HIA is to evaluate the distribution of health impacts and identify potential inequities. This goes beyond simply calculating an average effect for the entire population.

#### The Role of Social Determinants of Health

HIAs must explicitly include **social determinants of health (SDH)** because they play a dual role in shaping policy impacts. First, they can act as **confounders**, as social and economic position often influences both the level of exposure to environmental hazards and baseline health status. Second, and crucially, they can act as **effect modifiers**, meaning that they modify the relationship between exposure and outcome. For example, a low-income individual ($S=1$) might be more vulnerable to a given level of air pollution ($E$) than a high-income individual ($S=0$) due to factors like poorer nutrition, co-existing health conditions, or higher stress levels. This can be represented in a risk model with an interaction term, such as $r(E,S) = \beta_0 + \beta_E E + \beta_S S + \beta_{ES} E S$. The positive [interaction term](@entry_id:166280) $\beta_{ES}$ captures this added vulnerability. Excluding SDH from an HIA would not only fail to address equity but would also lead to an inaccurate estimate of the total population impact, as the overall effect is a weighted average of the different effects across subgroups. [@problem_id:4533276]

#### Systematic Equity Analysis: PROGRESS-Plus

To ensure a systematic and comprehensive equity analysis, practitioners often use frameworks like **PROGRESS-Plus**. This acronym stands for **P**lace of residence, **R**ace/ethnicity/culture/language, **O**ccupation, **G**ender/sex, **R**eligion, **E**ducation, **S**ocioeconomic status, and **S**ocial capital. The "Plus" acknowledges other important axes of social stratification, such as age, disability, or sexual orientation.

In an HIA, variables are selected from this framework based on theories of **structural determinants of health**—the social and economic mechanisms that stratify populations—and an analysis of how the specific policy's mechanisms might create **policy-mediated inequities**. For a policy like a congestion charge, relevant stratifiers would include place of residence (transit access), socioeconomic status (affordability), occupation (shift workers), age, and disability (ability to switch travel modes), and digital/banking access (ability to pay). By identifying these pre-exposure social positions, an HIA can assess differential impacts and recommend targeted mitigation measures (e.g., discounts, exemptions, service enhancements) to ensure the policy's benefits are shared fairly and its burdens do not fall disproportionately on already disadvantaged groups. [@problem_id:4533271]

### Characterizing and Communicating Uncertainty

HIA findings are estimates, not certainties. A credible assessment must transparently characterize the different sources of uncertainty in its analysis. It is useful to distinguish between three main types:

-   **Parameter Uncertainty**: Uncertainty in the specific values of model inputs, such as the ERF coefficient $\beta$ or the baseline incidence rate $I_0$. This arises from finite-sample [estimation error](@entry_id:263890) and is typically addressed using probabilistic [sensitivity analysis](@entry_id:147555) (e.g., Monte Carlo methods).

-   **Model Uncertainty**: Uncertainty about the correct mathematical structure of the model itself. For example, is the true ERF log-linear, linear, or does it have a threshold? This is addressed by conducting structural sensitivity analyses using alternative plausible models.

-   **Scenario Uncertainty**: Uncertainty about the future context in which the policy will be implemented. This includes factors like the degree of policy enforcement, rates of technological adoption, or future demographic trends. This is addressed by developing and comparing a set of discrete, plausible scenarios (e.g., an optimistic vs. a pessimistic scenario).

These types of uncertainty can also be classified into two fundamental categories. **Aleatory uncertainty** refers to inherent randomness or variability in a system that cannot be reduced by more knowledge (e.g., which specific individual gets sick). **Epistemic uncertainty** refers to a lack of knowledge that is, in principle, reducible with more data or better science (e.g., uncertainty about the true value of $\beta$). Parameter and [model uncertainty](@entry_id:265539) are primarily epistemic. By systematically identifying, quantifying, and discussing these uncertainties, an HIA provides decision-makers with a complete and honest picture of what is known, what is unknown, and the level of confidence in its conclusions. [@problem_id:4533249]