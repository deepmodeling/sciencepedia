## Introduction
A central challenge in medical research is ensuring that scientific discoveries translate into tangible benefits for patients in routine clinical settings. Too often, a gap exists between what is shown to work in a highly controlled laboratory or research environment and what actually works in the messy, complex reality of healthcare. This gap highlights a fundamental choice in clinical trial design: should a study focus on whether an intervention *can* work under perfect conditions, or whether it *does* work in everyday practice? This article unpacks the two major paradigms designed to answer these distinct questions: the explanatory trial and the pragmatic trial. By understanding their differences, researchers can design studies that provide the right evidence for the right decisions.

This article is structured to provide a comprehensive understanding of this critical topic. The first chapter, **"Principles and Mechanisms,"** will delve into the core concepts of efficacy versus effectiveness, the inherent trade-off between internal and external validity, and the formal statistical estimands that define the research question. The second chapter, **"Applications and Interdisciplinary Connections,"** will demonstrate how these principles are applied in diverse fields such as implementation science, health economics, and oncology, and will explore advanced pragmatic designs. Finally, the third chapter, **"Hands-On Practices,"** will offer interactive exercises to solidify your grasp of key concepts like cluster randomization and cost-effectiveness analysis. We begin by examining the fundamental distinction that lies at the heart of these two trial paradigms.

## Principles and Mechanisms

### The Core Distinction: Efficacy versus Effectiveness

At the heart of clinical trial design lies a fundamental choice regarding the primary research question. Is the goal to determine if an intervention *can* work under idealized, perfectly controlled circumstances? Or is it to determine if the intervention *does* work when implemented in the complex, variable environment of routine clinical practice? These two questions define the opposing poles of a continuum, with the **explanatory** trial paradigm at one end and the **pragmatic** trial paradigm at the other.

An **explanatory trial** is designed to test a causal hypothesis, often a biological one, with the highest possible degree of scientific rigor. To achieve this, investigators create a highly controlled experimental setting that minimizes all sources of variability other than the intervention itself. The focus is on demonstrating **efficacy**—the effect of an intervention when delivered and received under perfect or optimal conditions. The guiding question is, "Can this intervention work?"

Conversely, a **pragmatic trial** is designed to inform a decision for patients, clinicians, or policymakers. It aims to evaluate the overall utility of an intervention as it would be applied in typical, real-world settings. These trials embrace the natural variability of clinical practice, including heterogeneity in patients, provider behavior, and adherence. The focus is on determining **effectiveness**—the effect of an intervention when deployed as a strategy in routine care. The guiding question is, "Does this intervention work in practice?"

### Foundational Trade-offs: Internal and External Validity

The distinction between explanatory and pragmatic goals maps directly onto two critical concepts of validity in epidemiologic research: internal and external validity.

**Internal validity** refers to the degree of confidence that the observed association between the intervention and the outcome is causal and not due to systematic error (bias) *within the specific sample of participants studied*. A study with high internal validity provides a trustworthy answer to the research question for the population enrolled in that trial. Explanatory trials prioritize internal validity above all else. Design features such as strict eligibility criteria, intensive monitoring, standardized protocols, and aggressive blinding are all employed to minimize confounding, performance bias, and detection bias, thereby producing the cleanest possible estimate of the intervention's effect in the study sample.

**External validity**, also known as generalizability or applicability, refers to the extent to which the results of a study can be confidently applied to a broader target population or setting beyond the confines of the trial. A study with high external validity provides results that are relevant and transportable to the real world of clinical decision-making. Pragmatic trials prioritize external validity. They achieve this by using broad eligibility criteria to enroll a representative patient population, implementing the intervention in typical care settings, and allowing for the natural flexibility of routine practice.

Crucially, there is an inherent **trade-off** between these two forms of validity. The very design choices that maximize internal validity in an explanatory trial—such as enrolling a highly selected, homogeneous group of patients and enforcing perfect adherence—can severely limit the generalizability of the findings. An intervention that proves efficacious in a hand-picked group of young, otherwise healthy, and highly motivated individuals may not be effective in an elderly, multimorbid population with typical levels of adherence. Conversely, the choices that maximize external validity in a pragmatic trial—such as embracing patient heterogeneity and real-world adherence—can introduce variability and potential biases that pose challenges to achieving the pristine internal validity of a classic explanatory trial.

### Formalizing the Research Question: Estimands and Analysis

The potential outcomes framework of causal inference provides a [formal language](@entry_id:153638) to precisely define the different research questions targeted by explanatory and pragmatic trials. Let us consider a randomized controlled trial (RCT) where $Z$ is an indicator for random assignment ($Z=1$ for assignment to the new intervention, $Z=0$ for assignment to the control condition) and $Y$ is the outcome of interest. Each participant has two potential outcomes: $Y(Z=1)$, the outcome they would have if assigned to the intervention, and $Y(Z=0)$, the outcome they would have if assigned to the control.

The primary estimand of a **pragmatic trial** is the average effect of the *assignment* or *policy* of offering the intervention. This is the **Intention-to-Treat (ITT) estimand**, formally defined as the average difference in potential outcomes under assignment:

$$
\text{ITT Effect} = E\left[Y(Z=1) - Y(Z=0)\right]
$$

Because randomization ensures that the assignment $Z$ is independent of the potential outcomes, this causal quantity is directly identified by the observed difference in mean outcomes between the randomized groups. This is a cornerstone of trial analysis:

$$
E\left[Y(Z=1) - Y(Z=0)\right] = E\left[Y \mid Z=1\right] - E\left[Y \mid Z=0\right]
$$

This estimand captures the real-world **effectiveness** of the treatment strategy, including all its downstream consequences such as non-adherence, crossovers, and co-interventions. It answers the pragmatic question, "What is the net effect of adopting a policy of offering this new intervention compared to the alternative?"

The primary estimand of an **explanatory trial**, by contrast, seeks to quantify the biological **efficacy** of the treatment itself, separate from the behavioral complexities of adherence. The conceptual target is the effect of *receiving* the treatment as intended by the protocol. Let $D$ be an indicator for the treatment actually received ($D=1$ for receiving treatment, $D=0$ for not). The "per-protocol biological effect" is the average difference in potential outcomes under actual receipt of treatment:

$$
\text{Per-Protocol Effect} = E\left[Y(D=1) - Y(D=0)\right]
$$

Unlike the ITT estimand, this quantity is generally *not* identified by a simple comparison of observed groups, because the treatment actually received, $D$, is a post-randomization choice that can be confounded. For example, patients who feel sicker might be more likely to adhere to their assigned treatment, creating a spurious association between treatment receipt and outcome. A naive "as-treated" analysis that compares those who took the drug to those who did not, ignoring initial randomization, is therefore highly susceptible to bias. Estimating an efficacy-oriented estimand like the per-protocol effect or the Complier Average Causal Effect (CACE) from a trial with non-adherence requires advanced statistical methods, such as Instrumental Variables analysis or g-methods (e.g., Inverse Probability Weighting), that make additional assumptions to adjust for post-randomization confounding.

### From Theory to Practice: Key Design Choices on the Explanatory-Pragmatic Continuum

The philosophical difference between explanatory and pragmatic paradigms translates into a series of concrete design decisions. The Pragmatic-Explanatory Continuum Indicator Summary version 2 (PRECIS-2) tool provides a useful framework for characterizing these choices across nine key domains. A highly pragmatic trial would score close to "usual care" on each domain, while a highly explanatory trial would score toward "highly controlled."

#### Eligibility Criteria and Heterogeneity

Explanatory trials employ **strict inclusion and exclusion criteria**. For instance, a trial of a new antihypertensive drug might recruit only patients aged 40-65 with a specific range of baseline blood pressure and no comorbidities. This creates a **homogeneous** study population, which reduces the variability of outcomes and treatment effects. This reduction in heterogeneity increases statistical precision (i.e., reduces the variance of the effect estimate) for a given sample size and enhances internal validity by minimizing confounding from other conditions. However, the finding is specific to this narrow, "ideal" subgroup and has low external validity.

Pragmatic trials use **broad eligibility criteria** that mirror the patient population who would receive the intervention in routine practice. The same antihypertensive trial designed pragmatically might include adults of all ages, with comorbidities and concomitant medications. This creates a **heterogeneous** sample, which reflects real-world diversity. While this increases external validity, the greater variability in outcomes may decrease statistical precision, requiring larger sample sizes to achieve adequate power.

#### Intervention Delivery: Protocolization versus Flexibility

An explanatory trial is characterized by high **protocolization**, meaning the intervention is delivered according to a strict, standardized, and inflexible protocol. For example, a trial of a new digital therapy for insomnia might mandate fixed session lengths, standardized scripts, and prohibit any co-interventions for sleep. This uniformity is essential for internal validity, ensuring that any observed effect is attributable to the specific intervention as designed.

A pragmatic trial embraces **flexibility** in delivery. The same insomnia therapy trial, if designed pragmatically, would allow clinicians to adapt session length and content to patient needs, permit common co-interventions like sleep hygiene advice, and integrate the tool into their existing clinical workflows. This flexibility mirrors usual care, thereby enhancing external validity by testing a strategy that is adaptable to individual contexts.

#### Adherence and Fidelity

**Adherence** refers to the extent to which participants follow the prescribed regimen (e.g., taking medication). **Fidelity** refers to the extent to which clinicians or the health system deliver the intervention as intended.

In an explanatory trial, high adherence and fidelity are critical for isolating the biological effect of the intervention. These trials will therefore actively *maximize and monitor* both. This may involve pre-randomization "run-in" periods to exclude non-adherent individuals, frequent pill counts or electronic monitoring, and retraining of staff who deviate from the protocol.

In a pragmatic trial, imperfect adherence and variable fidelity are considered part of the "real-world" effect being measured. Therefore, these trials typically *measure but do not enforce* adherence and fidelity beyond what is routine. Data on adherence might come from pharmacy refill records, and fidelity might be assessed via periodic chart audits. This information is crucial for interpreting the trial's results—an intervention might be ineffective either because it has no biological effect or because it was not used by patients or delivered by clinicians in practice.

#### Choice of Outcomes: Surrogate versus Patient-Centered

Explanatory trials often use **surrogate outcomes**, which are laboratory measures or physical signs intended to be a substitute for a clinically meaningful endpoint. Examples include glycated hemoglobin ($\mathrm{HbA1c}$) in a diabetes trial or tumor size in an oncology trial. Surrogates are often chosen because they can be measured more quickly, easily, and precisely than patient-centered outcomes, allowing for smaller, shorter trials.

Pragmatic trials strongly prioritize **patient-centered outcomes**—endpoints that matter directly to patients' experience, function, and survival. Examples include all-cause hospitalization, quality of life, stroke, or mortality. While these outcomes may take longer to accrue and be subject to more variability, they provide direct evidence of the intervention's real-world benefit or harm.

A critical danger in relying on surrogate endpoints is the potential for **surrogate failure**. An intervention may successfully improve a surrogate marker without translating to a benefit in a patient-centered outcome; in some cases, it may even be harmful. For a surrogate $S$ to be valid for a clinical outcome $Y$, the entire effect of the treatment $T$ on $Y$ must be mediated through $S$ (formally, $Y \perp T \mid S$). This is a strong and often unproven assumption. A trial might show a drug significantly lowers $\mathrm{HbA1c}$, yet a subsequent pragmatic trial reveals it fails to reduce hospitalizations and may even worsen quality of life, demonstrating the discordance.

### Addressing Methodological and Ethical Challenges in Pragmatic Designs

The commitment of pragmatic trials to real-world conditions introduces unique challenges, particularly regarding blinding and informed consent.

#### Blinding and Expectation Bias

In many pragmatic trials, **blinding** (concealing the treatment assignment) is difficult or impossible. Interventions are often complex and visible, such as a new collaborative care program for depression, a surgical procedure, or a digital health tool. Furthermore, the comparator is often "usual care," which is inherently recognizable. The inability to blind participants and clinicians raises concerns about **expectation bias**, where knowledge of the treatment assignment influences behaviors or reporting of outcomes.

While blinding may be infeasible, several strategies can mitigate its absence:
*   **Use of Objective Outcomes**: Prioritizing "hard" outcomes that are less susceptible to subjective influence, such as mortality or hospitalizations obtained from administrative or electronic health record (EHR) data.
*   **Blinded Outcome Adjudication**: Employing an independent committee, unaware of treatment assignments, to review patient data and adjudicate key clinical events.
*   **Neutral Messaging**: Using standardized, neutral language during enrollment to present the compared interventions with equipoise, thereby managing participant expectations.

#### Informed Consent

The ethical conduct of research, guided by principles such as those in the Belmont Report, mandates respect for persons, primarily through informed consent. In an **explanatory trial**, where participants are subjected to protocolized procedures and risks beyond standard care, comprehensive, explicit, individual informed consent is non-negotiable.

For certain **pragmatic trials**, the ethical landscape is more nuanced. When a trial compares two or more treatments that are all considered standard of care, is embedded within routine clinical practice, and poses no more than minimal incremental risk to participants, a full, traditional consent process may be impracticable and could even harm the scientific validity of the study by introducing selection bias. In such cases, and with rigorous oversight from an Institutional Review Board (IRB), ethical frameworks may permit the use of **streamlined consent, opt-out procedures, or a waiver of consent**. This approach is justified when the research could not practicably be carried out otherwise and the rights and welfare of patients are not adversely affected. It represents a careful balancing of the duty to improve care through research (beneficence) with a contextualized application of respect for persons.