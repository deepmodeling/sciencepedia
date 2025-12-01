## Introduction
In the field of public health, case definitions and epidemic curves are the foundational instruments used to see, measure, and respond to disease outbreaks. They transform chaotic streams of raw data—symptoms, lab tests, and patient reports—into a coherent picture of an epidemic's progression, providing the actionable intelligence needed to guide interventions and save lives. However, these tools are not simple photographs of reality. Their creation is a complex process, and their interpretation requires a deep understanding of their inherent limitations. Without a rigorous grasp of how a case is defined and how an [epidemic curve](@entry_id:172741) is constructed, our perception of an outbreak can be dangerously distorted, leading to flawed conclusions and ineffective responses.

This article provides a comprehensive guide to the theory and practice of developing case definitions and using epidemic curves. It bridges the gap between raw data and epidemiological insight, equipping you with the critical knowledge to understand and analyze outbreak data effectively.

*   In the first chapter, **Principles and Mechanisms**, we will explore the core concepts that govern these tools. You will learn how case definitions are formulated, how their performance is measured using sensitivity and specificity, and how these metrics create systematic biases in the epidemic curves we observe.

*   The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate how these theoretical principles are operationalized in real-world public health. We will examine their use in outbreak investigations, risk assessment, [policy evaluation](@entry_id:136637), and their connections to fields like health economics and statistics.

*   Finally, the **Hands-On Practices** section will offer an opportunity to apply this knowledge directly, reinforcing your understanding by working through practical problems that mirror the challenges faced by epidemiologists in the field.

## Principles and Mechanisms

### The Case Definition: Bridging Latent Disease and Observable Data

In [public health surveillance](@entry_id:170581) and outbreak investigation, a central challenge is that the true infection status of an individual is a **latent state**—it cannot be directly observed. An individual is either truly infected or not, but this reality is hidden from us. To take action, we must rely on observable phenomena: clinical symptoms, laboratory test results, and known epidemiologic links to other cases. The bridge between the unobservable truth and the observable data is the **case definition**.

A case definition is a standardized, operational rule that maps a set of observable variables to a [binary classification](@entry_id:142257): "case" or "non-case." It is the instrument through which we "measure" the presence of an epidemic. For instance, in an investigation of a new disease, which we might call NovaPox, the observable data for an individual $i$ at time $t$ could include a clinical syndrome indicator $S_i(t)$, a rapid test result $T_i(t)$, and an epidemiologic link indicator $E_i(t)$. A case definition might classify an individual as a case if they have both symptoms and a positive test, or if they have symptoms and a known link to a confirmed case [@problem_id:4507868].

The performance of any case definition, like any measurement tool, is characterized by its accuracy. The two most fundamental metrics of this accuracy are its **sensitivity** and **specificity**. Let $D=1$ represent the latent state of being truly diseased and $D=0$ represent being non-diseased. Let $Y=1$ indicate that an individual meets the case definition (is classified as a case) and $Y=0$ indicate they do not.

**Sensitivity ($Se$)** is the probability that a truly diseased individual is correctly classified as a case.
$Se = P(Y=1 | D=1)$

**Specificity ($Sp$)** is the probability that a truly non-diseased individual is correctly classified as a non-case.
$Sp = P(Y=0 | D=0)$

These are intrinsic properties of the case definition under specific operational conditions. Consider a scenario where a symptom-based case definition is evaluated against a "gold standard" laboratory test like PCR. In a sample of 500 people, 280 are found to be truly infected ($D=1$) and 220 are truly non-infected ($D=0$). The case definition classifies 231 of the infected individuals as cases ($Y=1$) and classifies 162 of the non-infected individuals as non-cases ($Y=0$). This information can be organized in a standard $2 \times 2$ table, or confusion matrix:

| | **True Disease ($D=1$)** | **No Disease ($D=0$)** |
| :--- | :---: | :---: |
| **Case ($Y=1$)** | True Positives (TP) = 231 | False Positives (FP) = 58 |
| **Non-Case ($Y=0$)** | False Negatives (FN) = 49 | True Negatives (TN) = 162 |
| **Total** | 280 | 220 |

From this data, we can estimate the sensitivity and specificity:

$Se = \frac{\text{TP}}{\text{TP} + \text{FN}} = \frac{231}{280} = 0.825$

$Sp = \frac{\text{TN}}{\text{TN} + \text{FP}} = \frac{162}{220} \approx 0.7364$

These values quantify the performance of the case definition. A sensitivity of $0.825$ means it successfully identifies $82.5\%$ of true cases, while a specificity of $0.7364$ means it correctly rules out $73.64\%$ of those who are not cases. The remaining individuals are misclassified: **false negatives** ($1 - Se = 0.175$) are true cases that are missed, and **false positives** ($1 - Sp \approx 0.2636$) are non-cases that are incorrectly labeled as cases [@problem_id:4507918].

### The Epidemic Curve: A Biased Portrait of an Outbreak

The primary tool for visualizing the temporality of an outbreak is the **[epidemic curve](@entry_id:172741)**, a histogram that plots the number of new cases over successive time intervals. While it may seem like a direct photograph of the epidemic's progression, it is crucial to understand that the observed epidemic curve, let's call its value on day $t$ as $C_t$, is a systematically biased and noisy representation of the true, latent incidence of infection, $I_t$.

The observed case count $C_t$ is the sum of true positives and false positives identified on day $t$. To understand the relationship between $C_t$ and $I_t$, we can derive the expected value of the observed count, $\mathbb{E}[C_t]$. Assume on day $t$ a total of $N_t$ individuals are evaluated, of whom $I_t$ are truly incident cases and $N_t - I_t$ are not.

The expected number of true positives is the number of true cases, $I_t$, multiplied by the probability of correctly identifying them (sensitivity):
$\mathbb{E}[\text{True Positives}] = I_t \cdot Se$

The expected number of false positives is the number of non-cases, $N_t - I_t$, multiplied by the probability of incorrectly identifying them (1 minus specificity):
$\mathbb{E}[\text{False Positives}] = (N_t - I_t)(1 - Sp)$

The total expected observed case count is the sum of these two components:
$$\mathbb{E}[C_t] = I_t \cdot Se + (N_t - I_t)(1 - Sp)$$

This equation is fundamental. It reveals that the observed curve is a linear transformation of the true incidence curve. The **bias** in the measurement, defined as $B_t = \mathbb{E}[C_t] - I_t$, can be expressed in a simplified form by rearranging the terms [@problem_id:4507900]:

$B_t = [I_t \cdot Se + (N_t - I_t)(1 - Sp)] - I_t$
$B_t = I_t (Se - 1) + (N_t - I_t)(1 - Sp)$
$$B_t = I_t(Se + Sp - 2) + N_t(1 - Sp)$$

This expression formalizes the two sources of error. The term $I_t(Se - 1)$ is simply the negative of the number of false negatives, representing the downward bias from missed cases. The term $(N_t - I_t)(1 - Sp)$ is the number of false positives, representing the upward bias from incorrect classifications. The total bias on any given day depends on the test characteristics ($Se, Sp$) and the true number of infections ($I_t$) relative to the number of people evaluated ($N_t$). The epidemic curve is therefore not a pure signal of incidence, but a composite signal shaped by both biology and measurement error.

### The Role of Prevalence: The Dynamic Nature of a Case Definition's Meaning

While sensitivity and specificity are intrinsic properties of a case definition, their practical implications depend entirely on the context in which they are used—specifically, the underlying prevalence of the disease in the population being assessed. This leads to two other critical metrics: Positive Predictive Value (PPV) and Negative Predictive Value (NPV).

**Positive Predictive Value ($PPV$)** is the probability that an individual who meets the case definition is truly diseased.
$PPV = P(D=1 | Y=1)$

**Negative Predictive Value ($NPV$)** is the probability that an individual who does not meet the case definition is truly non-diseased.
$NPV = P(D=0 | Y=0)$

Unlike $Se$ and $Sp$, which are conditioned on the true disease state, $PPV$ and $NPV$ are conditioned on the observable classification. They answer the practical questions: "Given this positive result, what is the chance this person is actually a case?" and "Given this negative result, what is the chance this person is truly healthy?"

Using Bayes' theorem, we can show that these values are critically dependent on the prevalence of the disease at time $t$, denoted $\pi_t = P(D=1 \text{ at time } t)$. The derived formulas are [@problem_id:4507842]:

$$PPV_t = \frac{Se \cdot \pi_t}{Se \cdot \pi_t + (1 - Sp)(1 - \pi_t)}$$

$$NPV_t = \frac{Sp \cdot (1 - \pi_t)}{Sp \cdot (1 - \pi_t) + (1 - Se) \pi_t}$$

The epidemiological implication is profound: the meaning of a "case" classification changes over the course of an epidemic.
*   **Early in an outbreak**, when prevalence $\pi_t$ is very low, the $PPV_t$ will also be very low. A large proportion of individuals meeting the case definition will be false positives. The case definition is weak for "ruling in" disease.
*   **At the peak of an outbreak**, when prevalence $\pi_t$ is high, the $PPV_t$ will be very high. A positive classification is now a strong indicator of true infection. Conversely, the $NPV_t$ will be lower, meaning a negative classification is less reassuring.

We can even calculate the prevalence $\pi^{\star}$ at which the test's ability to rule in and rule out are balanced, i.e., $PPV_t = NPV_t$. This "stability moment" occurs at a specific prevalence that depends only on the test's characteristics [@problem_id:4507842]:

$$\pi^{\star} = \frac{\sqrt{Sp(1 - Sp)}}{\sqrt{Se(1 - Se)} + \sqrt{Sp(1 - Sp)}}$$

For a hypothetical epidemic following a [logistic growth](@entry_id:140768) curve, one could calculate the exact day $t^{\star}$ when this prevalence is reached. This point marks a functional transition in the utility of the case definition during the epidemic's trajectory [@problem_id:4507842].

### Constructing the Epidemic Curve: From Raw Data to Insight

Moving from theory to practice, the construction of an [epidemic curve](@entry_id:172741) from raw surveillance data—typically a **line list** containing one row per reported event—is a systematic, multi-step process [@problem_id:4507851].

1.  **Define the Analytic Case Set**: The first step is to apply the formal case definition to the raw records. This involves filtering the line list to include only records that meet the criteria for a confirmed or probable case, and excluding those that are ruled out (e.g., negative lab results).

2.  **Deduplicate Records**: Surveillance systems often receive multiple reports for the same person's single illness episode. It is essential to count unique illness episodes, not records. This **deduplication** process involves matching records based on stable identifiers (like name and date of birth) and collapsing them into a single, master record for each case. This must be done *before* counting.

3.  **Assign a Time Reference**: Every case must be placed at a single point on the time axis. The choice of which date to use is critical. Common date variables on a line list include:
    *   Date of symptom onset
    *   Date of specimen collection
    *   Date of laboratory result
    *   Date of report to the health department

    These dates represent a temporal sequence of events. The date of symptom onset is biologically closest to the time of infection and is therefore the most epidemiologically relevant for understanding transmission dynamics. However, it is often missing or subject to recall bias. Therefore, a standard **date hierarchy** is used: use symptom onset date if available; if not, use specimen collection date; if not, use report date [@problem_id:4507851].

    The choice of date profoundly affects the epidemic curve's shape and timing. An [epidemic curve](@entry_id:172741) plotted by a later reference date (e.g., report date) can be thought of as a **time-shifted and smoothed** version of the curve plotted by an earlier date (e.g., onset date). This is because the delays between events (onset-to-specimen, specimen-to-report) are not constant but are random variables drawn from a distribution. The mathematical operation that describes this process is convolution. The resulting curve will have its peak shifted later in time and will be broader and flatter due to the added variance from the delay distributions [@problem_id:4507894]. This distortion is particularly problematic when using surveillance data to estimate [transmissibility](@entry_id:756124), such as the [effective reproduction number](@entry_id:164900) ($R_t$). For this reason, onset date is strongly preferred. If report date must be used due to data completeness, sophisticated statistical methods are required to adjust for time-varying reporting delays, day-of-week reporting artifacts, and the fact that recent cases have not yet been reported (**right truncation**) [@problem_id:4507848].

4.  **Binning and Visualization**: Once each unique case has a single date assigned, the final step is to group the data into time bins. The bin width (e.g., 1 day, 3 days, 1 week) should be chosen based on the pathogen's incubation period and the desired resolution. The bins must be contiguous and non-overlapping. The final [histogram](@entry_id:178776), with time on the x-axis and case counts on the y-axis, is the epidemic curve.

### Interpreting the Epidemic Curve: Uncovering Transmission Patterns

Once constructed, the shape of the [epidemic curve](@entry_id:172741) provides powerful clues about the nature of the outbreak's transmission source [@problem_id:4507852]. There are three classic patterns:

*   **Point-Source Outbreak**: This occurs when a group of people is exposed to a common infectious source over a short period (e.g., contaminated food at a single event). The [epidemic curve](@entry_id:172741) shows a single, sharp peak of cases. The cases begin to appear after a minimum incubation period, the peak occurs, and the outbreak wanes after the source is removed. The width of the peak reflects the variation in the incubation period among those exposed.

*   **Continuous Common-Source Outbreak**: This occurs when exposure to a common source persists over a longer period (e.g., a contaminated municipal water supply). The curve rises and then plateaus, remaining elevated for as long as the exposure continues.

*   **Propagated (Person-to-Person) Outbreak**: This pattern occurs when the disease is transmitted from one person to another. The curve shows a series of progressively taller peaks, each representing a new "generation" of cases. The time interval between successive peaks approximates the pathogen's **serial interval**, which is the time between symptom onset in a primary case and symptom onset in the secondary cases they infect.

For example, if an epidemic curve shows distinct peaks in case onsets on Day 3, Day 7, and Day 11, the interval between peaks is 4 days. If the suspected pathogen is known to have a median [serial interval](@entry_id:191568) of 4 days, this provides strong evidence that the outbreak is being driven by person-to-person transmission [@problem_id:4507852].

### Advanced Topics and Practical Realities

#### The Surveillance Landscape and Its Biases

In reality, public health officials rarely have a single, perfect data stream. They typically synthesize information from multiple surveillance systems, each with its own sampling frame and inherent biases [@problem_id:4507906].
*   **Laboratory Reports**: The sampling frame is restricted to those who are tested. The resulting curve is heavily influenced by testing availability, eligibility criteria, and healthcare-seeking behavior. A sudden increase in testing capacity can create a spike in the curve that is unrelated to true incidence.
*   **Electronic Health Records (EHR)**: The sampling frame is individuals who seek care. The curve is modulated by public awareness and disease severity, which affect care-seeking behavior.
*   **Syndromic Surveillance (e.g., from Emergency Departments)**: Uses broad, non-specific case definitions (e.g., "fever and cough"). The curve is an additive mixture of cases from the epidemic of interest and cases from background co-circulating illnesses, which can distort its shape and peak timing.
*   **Sentinel Networks**: Samples a fixed fraction of providers. If well-designed, its curve can be a stable, scaled-down version of a more comprehensive system like EHR, but it is susceptible to changes in membership or reporting completeness.

Because each system's observed curve is distorted by different, often time-varying, factors (e.g., testing rates $r(t)$, care-seeking propensity $q(t)$), their raw shapes are not directly comparable. Valid interpretation requires understanding and often statistically adjusting for these biases.

#### Standardization versus Context-Sensitivity

This leads to a fundamental dilemma in designing case definitions.
*   **Within a jurisdiction**, it is imperative that a single, standardized case definition is used over time. This ensures that the measurement properties ($Se, Sp$) are held constant, so that changes in the observed epidemic curve $C(t)$ faithfully reflect changes in the true underlying prevalence $\pi(t)$ [@problem_id:4507864]. Changing the definition mid-outbreak confounds real trends with measurement artifacts.
*   **Across heterogeneous settings** (e.g., comparing a high-resource region with a low-resource one), a rigidly identical case definition may not be appropriate. Differences in laboratory capacity, population behavior, and healthcare access can cause the *operational* sensitivity and specificity of the same nominal definition to differ dramatically. This undermines the external validity of comparisons. To preserve [interpretability](@entry_id:637759), it may be necessary to use context-sensitive definitions that are tailored to achieve a more comparable measurement performance across settings [@problem_id:4507864].

#### The Ethical Dimensions of Case Definition

Finally, the choice of where to set the threshold for a case definition—trading off sensitivity for specificity—is not merely a statistical decision, but an ethical one. The costs of a false positive and a false negative are asymmetric and depend on the public health context [@problem_id:4507857].

*   **Cost of a False Positive ($w_{FP}$)**: An uninfected person is misclassified as a case. The harm includes unnecessary isolation, potential loss of income, psychological stress, and social stigma. This harm is primarily borne by the individual.

*   **Cost of a False Negative ($w_{FN}$)**: An infected person is missed. The harm is twofold. First, there is harm to the individual from delayed diagnosis and care. Second, and often more significant from a public health standpoint, is the harm to the community from continued, unmitigated transmission.

During the exponential growth phase of an epidemic, the cost of a false negative can be quantified by considering the chain of transmission it enables. If the effective reproduction number is $R_e$, a single missed case will lead to an expected $R_e$ new infections in the next generation, $R_e^2$ in the generation after that, and so on. By assigning a cost (e.g., in Quality-Adjusted Life Years, QALYs) to each new infection, the total downstream harm of a single false negative can be calculated. In a growing epidemic, this harm from onward transmission often vastly outweighs the direct harm to the individual and the harm of a false positive. This provides a strong ethical rationale for prioritizing high sensitivity in a case definition during the early, uncontrolled phase of an outbreak, even at the cost of lower specificity [@problem_id:4507857].