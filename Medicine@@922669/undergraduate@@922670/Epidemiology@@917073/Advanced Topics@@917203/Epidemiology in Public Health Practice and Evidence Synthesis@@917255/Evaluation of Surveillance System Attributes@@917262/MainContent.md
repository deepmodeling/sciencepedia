## Introduction
Public health surveillance forms the cornerstone of disease prevention and control, providing the critical information needed to detect threats and guide interventions. However, the value of a surveillance system is not inherent; it depends entirely on its performance and utility. Raw data streams can be incomplete, delayed, or unrepresentative, potentially painting a distorted picture of reality that can lead to misguided public health decisions. To ensure these systems effectively protect populations, they must be subjected to rigorous, systematic evaluation. This article provides a comprehensive guide to this essential process. It addresses the critical need for a standardized framework to measure, interpret, and improve the performance of public health surveillance systems.

Across the following chapters, you will gain a deep understanding of surveillance evaluation. The first chapter, **"Principles and Mechanisms,"** establishes the theoretical foundation by defining and operationalizing the core attributes of a system, from data quality and timeliness to flexibility and actionability. Next, **"Applications and Interdisciplinary Connections"** bridges theory and practice, demonstrating how these principles are applied using advanced statistical methods and how they connect to fields like health economics and decision science. Finally, **"Hands-On Practices"** offers the opportunity to apply these concepts to solve realistic problems, cementing your analytical skills. We begin by exploring the fundamental principles that govern every aspect of surveillance system performance.

## Principles and Mechanisms

The evaluation of a public health surveillance system is a critical endeavor that ensures the system meets its public health objectives efficiently and effectively. This process involves a systematic assessment of the system's core attributes. These attributes provide a standardized framework for understanding a system's performance, identifying its strengths and weaknesses, and guiding future improvements. This chapter delineates the principles and mechanisms underlying the key attributes used in surveillance system evaluation.

### Data Quality and Accuracy

The foundation of any surveillance system is the quality and accuracy of the data it collects. Without trustworthy data, subsequent analyses and public health actions are built on uncertain ground. Several attributes speak directly to this foundation.

#### Completeness: Capturing Cases and Their Details

**Completeness** refers to the extent to which all required information is captured by the surveillance system. This concept is twofold, encompassing both the capture of entire health events and the completeness of the data within each captured record.

First, **unit completeness**, often called **case completeness**, measures the proportion of true cases of a health event in the population that are successfully captured by the surveillance system. It is a measure of the system's overall reach. To calculate unit completeness, one needs an independent, "gold standard" estimate of the true number of cases, $N_{true}$, in the population over a specific period. The number of valid, unique cases captured by the surveillance system, $N_{valid}$, is then compared to this benchmark.

$$C_{unit} = \frac{N_{valid}}{N_{true}}$$

It is crucial that the numerator, $N_{valid}$, represents only the true, unique cases captured. Raw report counts are often inflated by errors such as false positives (reports that do not meet the case definition) and duplicate entries, which must be removed during data cleaning before the calculation. For instance, if a surveillance system receives $110$ case reports for acute hepatitis A in a month, but after adjudication $4$ are found to be false positives and $3$ are duplicates, the number of valid, unique reports is $N_{valid} = 110 - 4 - 3 = 103$. If an independent laboratory information system identified $120$ true cases ($N_{true} = 120$) in the same period, the unit completeness would be $\frac{103}{120}$ [@problem_id:4592269]. The $17$ cases not captured represent unit-level nonresponse.

Second, **item completeness** assesses the proportion of captured case records for which specific data fields (items) are complete and informative. This measures the quality of the data for the cases that were actually captured. For a given data field, item completeness is calculated as:

$$C_{item} = \frac{\text{Number of valid reports with complete data for the item}}{\text{Total number of valid reports}}$$

The denominator for item completeness is always the number of valid reports captured by the system ($N_{valid}$), not the total true cases in the population ($N_{true}$). Each required data field will have its own item completeness measure. Furthermore, system protocols may define certain entries, such as "Unknown," as non-informative and thus treat them as missing. Continuing the hepatitis A example, if among the $103$ valid reports, the "patient name" field is blank in $5$ records, its item completeness is $\frac{103 - 5}{103} = \frac{98}{103}$. If "vaccination status" is coded as "Unknown" in $22$ records and this is considered a missing value, its item completeness is $\frac{103 - 22}{103} = \frac{81}{103}$ [@problem_id:4592269].

#### Validity: The Accuracy of Case Classification

A surveillance system's ability to correctly classify individuals as cases or non-cases is fundamental. This is governed by the **surveillance case definition**, which may diverge from a **clinical gold standard**. This divergence is a primary source of systematic misclassification.

Consider an acute respiratory infection where the clinical gold standard for diagnosis is a Polymerase Chain Reaction (PCR) test, treated as having perfect accuracy. However, for routine surveillance, the system uses a more accessible but less accurate Rapid Antigen Test (RAT), defining a case as any person with a positive RAT [@problem_id:4592178]. The performance of such a definition is characterized by its **sensitivity ($Se$)**—the probability that a truly infected person tests positive—and its **specificity ($Sp$)**—the probability that a truly uninfected person tests negative.

The number of cases reported by the surveillance system will be the sum of true positives (TP) and false positives (FP). The number of missed cases will be the false negatives (FN). Let's examine a population of $N=10,000$ where the true disease prevalence is $p=0.05$.
- True number of cases: $N_{true} = N \times p = 10,000 \times 0.05 = 500$.
- Number of non-cases: $N_{non} = N \times (1-p) = 10,000 \times 0.95 = 9,500$.

If the RAT has $Se = 0.70$ and $Sp = 0.98$:
- True Positives (correctly identified cases): $TP = Se \times N_{true} = 0.70 \times 500 = 350$.
- False Negatives (missed cases): $FN = (1 - Se) \times N_{true} = 0.30 \times 500 = 150$.
- False Positives (incorrectly identified cases): $FP = (1 - Sp) \times N_{non} = 0.02 \times 9,500 = 190$.

The total number of cases reported by the surveillance system is $N_{surv} = TP + FP = 350 + 190 = 540$. In this scenario, despite an imperfect sensitivity that misses $150$ true cases, the system overestimates the total case count by $40$ (an $8\%$ overestimation). This occurs because even a high specificity ($98\%$) applied to a very large pool of uninfected individuals can generate a substantial number of false positives, which can outweigh the number of false negatives. This demonstrates a critical principle: the overall accuracy of surveillance counts depends on the interplay between test characteristics ($Se$, $Sp$) and population prevalence ($p$).

This misclassification also impacts the **Positive Predictive Value (PPV)**, defined as the probability that a person reported as a case is truly a case ($PPV = \frac{TP}{TP + FP}$). In our example, the PPV is $\frac{350}{540} \approx 0.648$, meaning over a third of the alerts are for individuals who are not truly infected.

#### Evaluating Continuous Scores: ROC and PR Curves

Many modern surveillance systems use continuous scores (e.g., from a statistical model) to flag potential cases, where a case is flagged if the score $S$ exceeds a certain threshold $\tau$. Evaluating such a system requires understanding its performance across all possible thresholds. Two graphical tools are essential for this: the Receiver Operating Characteristic (ROC) curve and the Precision-Recall (PR) curve [@problem_id:4592228].

A **Receiver Operating Characteristic (ROC) curve** plots the True Positive Rate ($TPR$, or Sensitivity) on the y-axis against the False Positive Rate ($FPR$, or $1 - Sp$) on the x-axis. Each point on the curve represents the $(FPR, TPR)$ pair for a specific threshold $\tau$. The ROC curve visualizes the trade-off between correctly identifying cases and incorrectly flagging non-cases. A key property of the ROC curve is that it is **prevalence-independent**. Since both sensitivity and specificity are conditional probabilities based on true disease status, they do not depend on the proportion of diseased individuals in the population. Therefore, a scoring system will have the same ROC curve in a high-prevalence population as in a low-prevalence one.

In contrast, a **Precision-Recall (PR) curve** plots Precision (or PPV) on the y-axis against Recall (or Sensitivity) on the x-axis. This curve is highly **prevalence-dependent**. As established previously, PPV is a function of sensitivity, specificity, and prevalence. At a fixed sensitivity and specificity, a lower prevalence will drastically decrease the PPV. For example, for a test with $Se=0.8$ and $Sp=0.8$, reducing prevalence from $0.10$ to $0.01$ would decrease the precision from approximately $0.31$ to just $0.04$ [@problem_id:4592228]. This means the PR curve for the low-prevalence population would be shifted substantially downward compared to the high-prevalence population. Consequently, PR curves are often more informative than ROC curves in typical surveillance settings where the prevalence of disease is low, as they more clearly reveal the large impact of false positives on the system's performance.

#### Handling Imperfections: Missing Data

Real-world surveillance data is invariably incomplete. Understanding the nature of the [missing data](@entry_id:271026) is crucial for accurate evaluation, as different types of missingness have different implications for analysis. Missing data mechanisms are typically classified into three categories [@problem_id:4592221].

- **Missing Completely At Random (MCAR)**: Missingness is independent of both the missing value itself and any other variables in the dataset. For example, if a random technical glitch causes $20\%$ of timeliness records to be lost, this is MCAR. In this case, the remaining observed data is a simple random subsample of the full data. A **complete-case analysis** (an analysis restricted to records with no missing data) will produce unbiased estimates of parameters like the mean timeliness, though with reduced statistical power.

- **Missing At Random (MAR)**: Missingness depends on other observed variables, but not on the missing value itself after accounting for those other variables. For instance, if laboratory confirmation results are more likely to be missing for patients in rural clinics or for older adults, but within a specific age-region group, the probability of missingness is not related to the actual lab result. This is MAR. A naive complete-case analysis that ignores region and age would be biased if those factors are also related to the outcome (e.g., if PPV differs by region). However, statistical methods that properly account for these covariates, such as **[inverse probability](@entry_id:196307) weighting** or **[multiple imputation](@entry_id:177416)**, can produce unbiased estimates.

- **Missing Not At Random (MNAR)**: The probability of missingness depends on the unobserved value itself, even after accounting for all observed variables. For example, in an audit to estimate surveillance sensitivity, if the data validation process is more likely to be completed for severe cases, and severity (which is unrecorded) also makes a case more likely to be captured by surveillance in the first place, then the missingness of the "capture status" variable is MNAR. A complete-case analysis would be biased, as the observed sample is no longer representative. In this specific scenario, the analysis would be restricted to a group enriched with severe (and thus more likely to be captured) cases, leading to an upwardly biased estimate of sensitivity.

### System Performance and Structure

Beyond data accuracy, a surveillance system's performance is judged by its operational characteristics, such as its speed, its ability to reflect the true population, and its technical dependability.

#### Timeliness: The Speed of Information

**Timeliness** measures the speed with which information moves through the surveillance system, from the occurrence of a health event to the point where the data are available to inform public health action. It is best characterized not as a single average value but as a distribution of delays across cases.

The total delay can be decomposed into a pipeline of consecutive intervals. For an infectious disease, this might be [@problem_id:4592270]:
1.  **Onset-to-Diagnosis Delay ($T_{od}$)**: The time from symptom onset ($t_0$) to clinical diagnosis ($t_1$).
2.  **Diagnosis-to-Report Delay ($T_{dr}$)**: The time from diagnosis ($t_1$) to notification of public health authorities ($t_2$).
3.  **Report-to-Aggregation Delay ($T_{ra}$)**: The time from notification ($t_2$) to the inclusion of the case in a dataset ready for analysis and action ($t_3$).

The total timeliness for a case is the sum of these delays: $T = T_{od} + T_{dr} + T_{ra}$. When evaluating timeliness, it is common for some cases not to have completed the entire sequence by the evaluation cutoff date ($t^*$). For such a case, the total delay is unknown. To avoid the bias that would result from simply excluding these cases, they should be treated as **right-censored** data. For a case with an unobserved aggregation time $t_3$, its observed delay is at least $t^* - t_0$, and this information is incorporated into survival analysis techniques to produce an unbiased estimate of the timeliness distribution.

#### Representativeness: Reflecting the Population

A surveillance system is **representative** if the cases it captures accurately reflect the occurrence and distribution of the health event in the target population with respect to person, place, and time. Lack of representativeness occurs when the **capture probability**—the probability that a true case is included in the surveillance system—systematically varies across different population subgroups.

For example, a system may have a high capture probability for urban cases ($90\%$) but a very low one for rural cases ($30\%$) due to reliance on hospital-based reporting. Similarly, it might capture senior cases more effectively ($90\%$) than pediatric cases ($50\%$), or have reduced capacity during peak seasons, leading to lower capture rates in winter ($60\%$) than in other seasons ($90\%$) [@problem_id:4592242].

Such disparities mean that the raw surveillance data present a distorted picture of the epidemic. The disease burden in rural populations and children would be severely underestimated. An evaluation of representativeness involves comparing the distribution of cases in the surveillance system to the known distribution in the population. Interventions to improve representativeness must directly target the sources of these disparities, for instance, by implementing active case-finding in under-represented groups like rural clinics and pediatric practices to equalize the capture probabilities across strata. Improving timeliness or changing case definitions does not, by itself, fix underlying problems of representativeness.

#### Stability and Reliability: System Dependability

**Stability** and **reliability** refer to the capacity of the surveillance system to collect, manage, and provide data without failure. A system that is frequently offline cannot function effectively. These attributes are typically operationalized using metrics from [reliability engineering](@entry_id:271311) [@problem_id:4592255].

The first key metric is the **Uptime Proportion**, which is the proportion of scheduled time that the system is fully operational. It is crucial to properly define the denominator. Total calendar time ($H_{cal}$) is not the correct basis if there are periods of planned maintenance ($H_{plan}$) during which the system is not expected to operate. The scheduled operating time is $H_{sched} = H_{cal} - H_{plan}$. If the system experiences unplanned downtime ($D$) due to failures, the actual operational time is $H_{op} = H_{sched} - D$. The uptime proportion is then:

$$U = \frac{H_{op}}{H_{sched}}$$

The second key metric is the **Mean Time Between Failures (MTBF)**, which measures the average duration of operational time between consecutive failures. It is calculated by dividing the total operational time by the number of failures ($N_f$):

$$\text{MTBF} = \frac{H_{op}}{N_f}$$

For a system evaluated over a $90$-day period ($2160$ hours) with $24$ hours of planned maintenance and $5$ failures totaling $36$ hours of downtime, the scheduled time is $2160 - 24 = 2136$ hours. The operational time is $2136 - 36 = 2100$ hours. The uptime proportion would be $\frac{2100}{2136} \approx 0.983$, and the MTBF would be $\frac{2100}{5} = 420$ hours.

### System Usability and Adaptability

Even a technically robust system will fail if it is too difficult for people to use or too rigid to adapt to changing needs.

#### Flexibility: Adapting to New Challenges

**Flexibility** is the ability of a surveillance system to adapt to changing requirements with minimal cost and disruption. These changes can include adding a new disease to monitor, updating a case definition for an existing disease, or integrating a new data source (e.g., electronic laboratory reports).

Flexibility is not an abstract quality but can be operationalized by measuring the resources consumed during an adaptation task. Key quantitative metrics include [@problem_id:4592232]:
- **Effort**: Total staff hours required for analysis, programming, and testing the change.
- **Time**: The calendar time from the change request to its deployment in the production system.
- **Scope**: The number of distinct system components or lines of code that needed modification.
- **Disruption**: Total system downtime attributable to implementing the change.
- **Training Burden**: The time required to train end-users on any new workflows or interfaces.

A system that requires fewer hours, less time, and smaller-scale modifications to accommodate a new disease is, by definition, more flexible.

#### Acceptability: Willingness to Participate

**Acceptability** reflects the willingness of individuals and organizations (stakeholders) to participate in the surveillance system. Stakeholders can include healthcare providers who report cases, laboratory staff who submit results, and patients who provide information. Low acceptability can cripple a system, leading to low completeness and poor representativeness.

Acceptability can be quantified by measuring participation at key stages of the surveillance process. For a school-based surveillance system, for instance, we can measure [@problem_id:4592290]:
- **Enrollment Proportion**: Of the schools that are invited to participate, what proportion agrees to enroll? If $200$ schools are approached and $150$ enroll, the enrollment proportion is $\frac{150}{200} = 0.75$. The denominator should be those given the opportunity, not the total number of schools in the district.
- **Reporting Adherence**: Of the reports that are expected from enrolled participants, what proportion are actually submitted? If $150$ schools are expected to submit one report per week for $8$ weeks (totaling $150 \times 8 = 1200$ expected reports) and they submit $920$ reports, the reporting adherence is $\frac{920}{1200} \approx 0.767$.

These metrics directly measure stakeholders' willingness to join and to continue participating, which is the essence of acceptability. It should not be confused with other attributes; for example, whether reports are submitted on time is a measure of timeliness, not acceptability.

### The Ultimate Goal: Public Health Action

While the previously discussed attributes are essential, they are ultimately means to an end. The final and most important measure of a surveillance system is its utility—its ability to drive actions that protect public health.

#### Actionability: From Data to Impact

**Actionability** is the degree to which the outputs of a surveillance system (e.g., weekly reports, automated alerts) trigger effective public health actions that lead to measurable outcomes. This attribute sits at the pinnacle of the evaluation hierarchy, as it links the entire surveillance process to its ultimate purpose.

To operationalize actionability, a metric must capture three components: the triggering of an action, the effectiveness of that action, and the magnitude of the resulting outcome. Simpler metrics are insufficient. For example, "the proportion of alerts that trigger an action" measures responsiveness but not effectiveness. "The proportion of alerts leading to an effective action" is better, but it treats an action that averts one case as equivalent to an action that averts one hundred cases.

The most comprehensive metric captures the average magnitude of the outcome per surveillance output. Consider a system that generates alerts for enteric disease outbreaks. We can define a metric as [@problem_id:4592210]:

$$\text{Actionability} = \frac{\sum_{i=1}^{N_{alerts}} \Delta Y_i}{N_{alerts}}$$

Here, $N_{alerts}$ is the total number of alerts the system generated. For each alert $i$, $\Delta Y_i$ is the measured outcome improvement (e.g., cases averted) attributable to the public health action that followed. If no action was taken or the action had no measurable effect, $\Delta Y_i = 0$. This metric elegantly integrates the entire causal chain. If a system generated $24$ alerts over a period, and the resulting actions led to a total of $96$ estimated cases averted, the actionability would be $\frac{96}{24} = 4$ cases averted per alert. This single, powerful figure quantifies the system's tangible contribution to public health, providing the ultimate assessment of its value.