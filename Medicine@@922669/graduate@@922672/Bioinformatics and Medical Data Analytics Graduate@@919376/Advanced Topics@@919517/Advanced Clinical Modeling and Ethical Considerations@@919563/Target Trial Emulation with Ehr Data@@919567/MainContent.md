## Introduction
Electronic Health Records (EHR) represent a vast repository of real-world data, offering unprecedented opportunities to answer critical questions about the effectiveness and safety of medical treatments. However, using this observational data for causal inference is fraught with challenges, as inherent biases like confounding by indication and immortal time bias can lead to misleading conclusions. The central problem is how to move from simple correlation to credible causal claims within data that was not collected for research.

Target trial emulation (TTE) emerges as a powerful solution, providing a structured conceptual framework to address these challenges. By explicitly specifying the protocol of a hypothetical randomized controlled trial (the "target trial") that one would ideally conduct, researchers can create a rigorous blueprint for analyzing observational data. This approach forces clarity and helps proactively identify and mitigate sources of bias, making causal estimates more transparent and interpretable.

This article will guide you through the theory and practice of emulating target trials with EHR data. In the **Principles and Mechanisms** chapter, we will dissect the core components of the target trial framework, the fundamental assumptions required for causal claims, and the key biases that must be addressed. The **Applications and Interdisciplinary Connections** chapter will then demonstrate the framework's versatility, exploring its use in pharmacoepidemiology, regulatory science, and its integration with advanced methods from biostatistics and econometrics. Finally, the **Hands-On Practices** section will challenge you to apply these concepts to practical problems, from designing phenotypes to assessing the impact of unmeasured confounding. Let us begin by exploring the foundational principles that make rigorous causal inference from EHR data possible.

## Principles and Mechanisms

The emulation of a target trial using observational data, such as that found in Electronic Health Records (EHR), is a structured process for posing and answering causal questions. It moves beyond simple association mining by providing a rigorous framework to mitigate the biases inherent in non-randomized data. This chapter elucidates the core principles and mechanisms that underpin this framework, detailing the components of a target trial, the fundamental assumptions required for causal identification, common sources of bias and their remedies, and the critical distinction between different types of causal effects.

### The Target Trial Framework: A Blueprint for Causal Inquiry

The guiding principle of target trial emulation is to explicitly specify the protocol of a hypothetical randomized controlled trial (RCT) that, if it were feasible and ethical to conduct, would answer the causal question of interest. This "target trial" then serves as a precise blueprint for the analysis of the observational data. A complete specification of the target trial protocol consists of seven key components, which we will illustrate using the example of a study designed to assess the effect of initiating statin therapy on cardiovascular events [@problem_id:4612490].

1.  **Eligibility Criteria**: These are the criteria that define the population of interest. In an RCT, these are the inclusion and exclusion criteria for enrollment. In an emulation, these criteria must be applied to the observational data to construct the study cohort. For a trial of statin initiation for primary prevention, eligibility criteria might include an age range (e.g., 40-75 years), a clinical indication (e.g., a laboratory result showing low-density [lipoprotein](@entry_id:167520) cholesterol (LDL-C) above a certain threshold, such as $130$ mg/dL), and the absence of prior events that would change the clinical context (e.g., no prior diagnosis of atherosclerotic cardiovascular disease). Crucially, to study the effect of *initiating* therapy, a **new-user design** is often employed, which excludes patients with prior use of the treatment (e.g., no statin prescription in the previous 365 days) [@problem_id:4612490] [@problem_id:4612494].

2.  **Treatment Strategies**: These are the interventions to be compared. A well-specified strategy details the treatment, dose, timing, and duration. For a pragmatic trial of statin initiation, the strategies might be defined as: (1) initiate any statin within a short grace period (e.g., 7 days) of eligibility versus (2) do not initiate a statin within that same grace period [@problem_id:4612490]. The comparator strategy must be an active, well-defined choice, not simply the absence of the intervention over an indefinite period.

3.  **Treatment Assignment**: In an ideal RCT, assignment is random. In an observational emulation, we observe the treatment choices made by clinicians and patients. The goal is to emulate randomization by adjusting for the baseline factors that influenced the treatment decision. This requires measuring a rich set of baseline covariates and using statistical methods, such as [inverse probability](@entry_id:196307) of treatment weighting (IPTW) or [propensity score matching](@entry_id:166096), to achieve balance in these covariates across the treatment groups.

4.  **Time Zero**: This is arguably the most critical component for avoiding temporal biases. **Time zero** is the single, unambiguous point in time at which eligibility is assessed, treatment strategies are assigned, and follow-up for the outcome begins for every individual in the trial. A common and robust choice for time zero is the date of the event that makes the patient eligible, such as the date of the qualifying laboratory test [@problem_id:4612490]. Misalignment of time zero across treatment groups is a primary source of **immortal time bias**, a topic we will explore in detail later in this chapter.

5.  **Follow-up**: This defines the period during which outcomes are ascertained. Follow-up begins for everyone at time zero and ends at the first of several events: the occurrence of the outcome, the end of the pre-specified follow-up period (e.g., 3 years), loss to follow-up (e.g., disenrollment from the health plan), or a major deviation from the assigned protocol if a per-protocol analysis is intended [@problem_id:4612490].

6.  **Outcomes**: The outcome must be precisely defined and ascertainable in the data. For our statin example, this could be the first occurrence of a major adverse cardiovascular event (MACE), identified using validated algorithms based on diagnosis and procedure codes.

7.  **Causal Estimand**: This is the specific causal quantity to be estimated. It could be a risk difference, risk ratio, or hazard ratio. It also specifies the causal contrast of interest, such as the **intention-to-treat effect** (the effect of the baseline treatment assignment) or the **per-protocol effect** (the effect of adhering to the assigned treatment strategy). For example, the target estimand could be the 3-year per-protocol risk difference, $\mathbb{E}[Y^{1}(3)] - \mathbb{E}[Y^{0}(3)]$, where $Y^{a}(t)$ is the potential outcome by time $t$ under strategy $a$ [@problem_id:4612490].

By meticulously specifying each of these components *before* analyzing the data, researchers can impose a structure that minimizes bias and produces a well-defined, interpretable causal estimate.

### Core Identification Assumptions: The Foundation of Causal Claims

To bridge the gap between the observed data and the causal estimand of the target trial, we must rely on a set of fundamental assumptions. These assumptions, which are untestable from the data alone, form the logical foundation upon which a causal interpretation rests.

#### Consistency and SUTVA: Ensuring a Well-Defined Intervention

The **consistency** assumption links the potential outcomes (counterfactuals) to the observed outcomes. It states that an individual's observed outcome is equal to their potential outcome under the treatment they actually received. If an individual received treatment $a$ (i.e., $A=a$), then their observed outcome $Y$ is equal to $Y^a$.

This seemingly simple assumption can be violated if the treatment is not well-defined. This is addressed by the **Stable Unit Treatment Value Assumption (SUTVA)**, which has two components: no interference between individuals, and no "hidden versions" of treatment. In EHR data, the latter is a common challenge. For example, "statin initiation" ($A=1$) is not a single intervention; it encompasses different molecules (e.g., atorvastatin, rosuvastatin), doses, and intensities [@problem_id:4612526]. If these different versions have different effects on the outcome, then a single potential outcome $Y^1$ is ill-defined. The observed outcome for a patient starting atorvastatin is $Y^{\text{atorvastatin}}$, while for another it is $Y^{\text{rosuvastatin}}$. If these are not equal, consistency for the vague intervention "statin" fails.

To address this, we must refine the treatment strategies in our target trial protocol. Sound strategies include:
*   **Restricting the analysis** to a single, well-defined version of the treatment (e.g., comparing initiation of high-intensity atorvastatin to no initiation).
*   **Defining and estimating version-specific effects** by stratifying the analysis by treatment version.
*   **Defining a stochastic intervention** where the target estimand is the effect of initiating a statin according to a pre-specified distribution of versions [@problem_id:4612526].

#### Exchangeability: Achieving Comparability through Adjustment

In an ideal RCT, randomization ensures that the treatment groups are, on average, identical with respect to all baseline characteristics, both measured and unmeasured. This property is called **exchangeability**. Formally, the potential outcomes are independent of the treatment assigned: $Y^a \perp\!\!\!\perp A$.

In observational studies, this is not true. Clinicians use their knowledge of a patient's prognosis to make treatment decisions, a phenomenon known as **confounding by indication**. For example, a patient with a higher baseline cardiovascular risk (e.g., higher LDL-C, more comorbidities) is more likely to be prescribed a statin and is also inherently at higher risk of MACE, regardless of treatment [@problem_id:4512511]. This violates exchangeability.

The goal in target trial emulation is to achieve **conditional exchangeability**. This assumption states that, conditional on a sufficiently rich set of pre-treatment covariates $L$, the potential outcomes are independent of the treatment assigned: $Y^a \perp\!\!\!\perp A \mid L$ [@problem_id:4612585]. In essence, we assume that within any stratum defined by the covariates in $L$, the decision to treat was "as-if" random. This is also known as the "no unmeasured confounding" assumption. The plausibility of this assumption hinges on two key design choices:
1.  A **new-user design**, which compares patients at the inception of therapy, ensures a more comparable starting point than comparing new users to prevalent users, who may have different underlying disease severity or tolerance to treatment [@problem_id:4612494].
2.  Measuring and adjusting for a **comprehensive set of baseline covariates** $L$ that capture the major determinants of treatment. Modern approaches may use **high-dimensional propensity scores** to algorithmically select thousands of variables from EHR data (e.g., diagnosis codes, procedures, lab results) to serve as proxies for clinical judgment and disease severity [@problem_id:4512511].

#### Positivity: Ensuring a Basis for Comparison

The **positivity** assumption requires that for every stratum of covariates $L=l$ present in the study population, there is a non-zero probability of receiving each treatment level. Formally, if $\mathbb{P}(L=l) > 0$, then $\mathbb{P}(A=a \mid L=l) > 0$ for all treatment strategies $a$.

Intuitively, this means that for any type of patient defined by their baseline characteristics, it must have been possible for them to have received or not received the treatment. If this condition fails, it is impossible to estimate the causal effect in that stratum. For example, if a treatment is known to be contraindicated for patients with severe hepatic failure ($L=1$), then no such patients will ever receive the treatment in the observational data, meaning $\mathbb{P}(A=1 \mid L=1) = 0$ [@problem_id:4612445]. This is a **structural positivity violation**.

In this scenario, we cannot estimate the causal effect of treatment for patients with severe hepatic failure, as we have no data on what would happen to them under treatment. Consequently, the average causal effect for the *entire* population is not identifiable from the data. The principled solution is to acknowledge this limitation and redefine the target trial's eligibility criteria to exclude the subgroup for which positivity fails. This changes the causal question to one that can be answered, such as "What is the causal effect of treatment among patients *without* severe hepatic failure?" [@problem_id:4612445].

### Key Biases in EHR-Based Emulation and Their Mitigation

Even with a clear understanding of the core assumptions, several common methodological pitfalls can invalidate the results of an EHR-based study. The target trial framework is designed to proactively avoid these biases.

#### Immortal Time Bias: The Peril of Misaligned Time Zero

**Immortal time bias** is a form of selection bias that arises from the incorrect definition of the start of follow-up, typically when treatment assignment is based on information that would only be available in the future. It creates a period of "immortal" person-time during which an individual is guaranteed to survive without the outcome.

Consider an analysis that defines the "exposed" group as anyone who *ever* initiates a statin during a 12-month follow-up period. Suppose a patient initiates a statin at month 4. To be classified as an "initiator," this patient must have survived for the first 4 months. If the analyst incorrectly classifies this 4-month period as "exposed" person-time, they are adding person-time to the exposed group's denominator during which, by definition, death could not have occurred for that group. This artificially deflates the mortality rate in the exposed group, biasing the effect estimate in favor of the treatment [@problem_id:4612475].

Let's illustrate with the example from problem [@problem_id:4612475]. In a cohort of 1000 patients, 400 initiate a statin at an average of 4 months into a 12-month follow-up. There are 30 deaths in this group after initiation.
*   **A naive, biased analysis** might misclassify all 12 months for each initiator as exposed time. The calculated mortality rate would be $\frac{30}{400 \times 12} = \frac{30}{4800}$ deaths per person-month.
*   **A correct analysis** would only count the time after initiation as exposed. The exposed person-time would be approximately $400 \times (12 - 4) = 3200$ person-months. The correctly classified rate is $\frac{30}{3200}$ deaths per person-month.
The naive rate is substantially lower than the correct rate, demonstrating the downward bias.

The solution is the strict definition of **time zero**: a single point in time that aligns eligibility, assignment, and the start of follow-up for all individuals, before the treatment strategy is executed. For time-varying initiation, advanced methods such as cloning or risk-set matching are required to ensure that at every potential initiation time, initiators are compared only to those who are still eligible and unexposed at that exact moment [@problem_id:4612439].

#### Confounding by Indication and the New-User Design

As previously mentioned, confounding by indication is perhaps the most significant threat to validity in pharmacoepidemiology. It arises because the reasons for prescribing a drug (the "indication") are themselves risk factors for the outcome. A powerful structural approach to mitigate this is the **new-user design** [@problem_id:4612494].

This design restricts the study cohort to individuals who are newly initiating the therapy of interest. It avoids **prevalent user bias**, which occurs when current users are compared to non-users. Prevalent users are a selected group: they have necessarily survived on the drug for some period and tolerated its initial effects. They are therefore systematically different from those just starting the drug, and comparing them to non-users or new users can lead to profound bias.

By focusing on the moment of initiation (time zero) in new users, we create a more comparable inception cohort. The choice of a comparator group is also critical. One can compare new users to non-users who are also eligible at time zero. An often superior approach is the **active-comparator, new-user design**, which compares new users of one drug to new users of another drug prescribed for the same indication (e.g., comparing a new PPI user to a new H2-receptor antagonist user for GERD) [@problem_id:4612494]. This can make the groups even more comparable, as both have received a diagnosis and a clinical decision to treat has been made, strengthening the plausibility of the exchangeability assumption.

### Defining the Causal Question: Intention-to-Treat vs. Per-Protocol Effects

Finally, it is essential to be precise about the causal question being asked. In trials where adherence to the initial treatment strategy is imperfect—as is almost always the case in EHR data—we must distinguish between two different causal effects.

#### The Intention-to-Treat (ITT) Effect

The **intention-to-treat (ITT) effect** is the effect of the *initial assignment* to a treatment strategy at time zero. The analysis follows the principle of "once assigned, always analyzed." Patients are analyzed in the group they were assigned to at baseline, regardless of whether they later discontinued the therapy or (if in the control group) crossed over to the active therapy [@problem_id:4612545].

The ITT effect answers a pragmatic question: "What is the effect of a clinical strategy of initiating treatment versus not initiating it, accounting for the typical patterns of adherence and non-adherence that follow?" To estimate this, one must only adjust for confounding at baseline ($L_0$), as all post-baseline events are considered part of the outcome under the assigned strategy.

#### The Per-Protocol (PP) Effect

The **per-protocol (PP) effect** is the effect of *adhering* to the assigned treatment strategy throughout the follow-up period. For example, what is the effect of taking a statin every day for three years versus never taking a statin for three years? This effect may be of greater biological or clinical interest than the ITT effect.

However, estimating the PP effect from observational data is significantly more complex. Adherence is not random. The decision to continue, stop, or start a therapy during follow-up is often influenced by time-varying patient characteristics (e.g., side effects, evolving disease severity) that are also risk factors for the outcome. This creates **time-varying confounding affected by prior treatment** [@problem_id:4612512]. For instance, a patient's blood pressure at month 6 ($L_6$) may be influenced by antihypertensive treatment in months 0-5 ($A_0, ..., A_5$), and $L_6$ will in turn influence the decision to intensify treatment at month 6 ($A_6$) and also predict the ultimate cardiovascular outcome ($Y$).

In this scenario, $L_6$ is both a confounder for the $A_6 \to Y$ relationship and a mediator on the causal pathway from $A_0, ..., A_5$ to $Y$. Standard regression models, which would adjust for $L_6$, fail because they cannot simultaneously adjust for confounding while avoiding blocking the mediating effect of past treatments. This structural feedback requires specialized **g-methods** for unbiased estimation [@problem_id:4612512]. These include:
*   **Marginal Structural Models (MSMs)** with Inverse Probability of Treatment and Censoring Weights (IPTW/IPCW), which create a pseudo-population where adherence is independent of the measured time-varying confounders.
*   The **Parametric g-Formula** (or g-computation), which models the joint distribution of the data over time and simulates the outcome under the hypothetical scenario where everyone adheres to the specified protocol.

These methods, when applied correctly under the assumptions of sequential exchangeability and positivity, allow for the identification of per-protocol effects even in the complex longitudinal settings typical of EHR data [@problem_id:4612545] [@problem_id:4612512].