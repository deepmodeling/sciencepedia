## Introduction
Feature engineering is the critical and often most time-consuming process in transforming raw clinical data into a format suitable for machine learning. Electronic Health Records (EHRs) and the clinical narratives they contain represent a vast, yet complex, source of patient information. Unlocking the potential of this data for predictive modeling, causal inference, and clinical decision support hinges on the ability to thoughtfully construct meaningful, robust, and reliable features. This article addresses the significant challenge that raw EHR data—with its heterogeneity, temporal complexity, and mix of structured codes and unstructured text—is not directly amenable to analysis. It provides a comprehensive guide to the principles, techniques, and applications of [feature engineering](@entry_id:174925) in the clinical domain.

Over the next three chapters, you will gain a deep understanding of this essential discipline. The first chapter, **Principles and Mechanisms**, establishes the foundational techniques for processing both structured data, like lab results and diagnoses, and unstructured clinical narratives. You will learn how to create a unified data model, normalize concepts, and handle the temporal dimension. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates how these features are applied in real-world scenarios, from building predictive models and calculating clinical indices to enabling causal inference and survival analysis. Finally, the **Hands-On Practices** chapter provides practical exercises to solidify your skills in normalizing text, [resampling](@entry_id:142583) [time-series data](@entry_id:262935), and building methodologically sound survival models. By navigating this material, you will be equipped to turn messy clinical data into powerful, actionable insights.

## Principles and Mechanisms

This chapter delves into the core principles and mechanisms of [feature engineering](@entry_id:174925) for Electronic Health Records (EHRs), covering the transformation of both structured data and unstructured clinical narratives into formats suitable for analytical modeling. We will begin by establishing a foundational data model, proceed to specific techniques for structured and unstructured data, and conclude with advanced considerations essential for robust and valid clinical data science, including temporal dynamics, missing data, and evaluation strategies.

### Foundations of EHR Data Representation

A fundamental challenge in EHR analytics is the heterogeneity of the data. To build reproducible and meaningful features, we must first impose a consistent structure on the raw data streams.

#### The Duality of EHR Data: Structured vs. Unstructured

EHR data can be broadly categorized into two forms: structured and unstructured. **Structured data** are discrete, atomic records that conform to a predefined schema and are often coded using standardized vocabularies. Examples include laboratory results, which are identified by codes from vocabularies like Logical Observation Identifiers Names and Codes (LOINC), medication orders coded in systems like RxNorm, and diagnoses coded using the International Classification of Diseases (ICD). These data are recorded in specific fields with expected data types (e.g., a numeric value and a unit for a lab test).

In contrast, **unstructured data** consists of free-form text, most notably the clinical narratives found in progress notes, discharge summaries, and radiology reports. This text does not adhere to a rigid field structure and captures a rich, nuanced view of clinical reasoning, patient history, and physical examinations. While it contains a wealth of information, its lack of standardization makes it challenging to use directly for computation.

#### A Unified Event Model for Reproducibility

To analyze these disparate data sources in an integrated fashion, it is essential to represent them within a common data model. A robust and reproducible feature engineering pipeline requires that the transformation from raw data to features is a deterministic function. Any feature should be able to be recomputed from the source data with no loss of critical information. This necessitates a minimal, yet comprehensive, schema for representing any clinical event, whether from a structured or unstructured source [@problem_id:4563144].

A standard and effective approach is to model the patient journey as a sequence of time-stamped events, where each event is represented by a tuple containing sufficient information to preserve its full context. A minimal schema to guarantee reproducibility includes the following attributes:

*   `patient_id`: A unique identifier for the individual, enabling the aggregation of all data for a single patient.
*   `visit_id`: A unique identifier for the clinical encounter (e.g., a specific hospitalization or outpatient visit). This is crucial for contextualizing events and distinguishing between different care episodes.
*   `timestamp`: The time at which the event occurred. The temporal ordering of events is paramount in clinical data.
*   `source_type`: An indicator of the event's origin (e.g., 'lab', 'diagnosis', 'note'). This provides essential provenance, allowing for differential handling of data from various systems.
*   `code`: A standardized concept code (e.g., a LOINC or ICD code) that provides the semantic meaning of the event.
*   `value`: The recorded quantitative or categorical value of the event (e.g., '140' for a lab result, 'positive' for a test).
*   `unit`: The unit of measurement for the `value` (e.g., 'mg/dL', 'beats/min'). A value is meaningless without its unit.
*   `note_text`: The full content of a clinical narrative, if the event is from an unstructured source.

This unified schema can accommodate both data types. For a structured lab result, the `code`, `value`, and `unit` fields would be populated, while `note_text` might be empty. For an unstructured clinical note, the `note_text` field would contain the narrative, while `value` and `unit` might be empty, and a `code` might only be assigned later through a Natural Language Processing (NLP) pipeline [@problem_id:4563144]. Adopting such an event model is the first step toward building a [feature engineering](@entry_id:174925) pipeline that is transparent, auditable, and scientifically valid.

### Feature Engineering from Structured Data

Once data is organized into a consistent event model, we can begin creating features. For structured data, this involves semantic normalization, aggregation, and strategic [dimensionality reduction](@entry_id:142982).

#### Semantic Normalization with Standard Terminologies

Raw clinical data often uses local or institution-specific codes. To ensure that features are comparable across different sites and are clinically meaningful, events must be mapped to standard terminologies. Each terminology is designed for a specific semantic domain, and choosing the correct one is vital for interoperability [@problem_id:4563189]. The primary terminologies include:

*   **International Classification of Diseases (ICD)**: Maintained by the World Health Organization, ICD is the standard for encoding diagnoses for billing, epidemiology, and health management. Discharge diagnoses are typically mapped to ICD codes.
*   **Current Procedural Terminology (CPT)**: Maintained by the American Medical Association, CPT is used to document medical, surgical, and diagnostic procedures and services, primarily for billing in the United States.
*   **Logical Observation Identifiers Names and Codes (LOINC)**: This is the standard for identifying laboratory tests, clinical measurements, and observations. It provides a unique code for each test-analyte-timing-system combination.
*   **RxNorm**: Developed by the U.S. National Library of Medicine, RxNorm provides normalized names and unique identifiers for clinical drugs, linking various drug vocabularies and supporting interoperability in medication-related data.
*   **Systematized Nomenclature of Medicine—Clinical Terms (SNOMED CT)**: This is a comprehensive, multilingual clinical ontology that covers a vast range of clinical concepts, including findings, diseases, procedures, body structures, and substances. Its hierarchical structure enables powerful reasoning. Clinical findings extracted from notes are often mapped to SNOMED CT.

Correctly mapping raw events to these standards—for instance, mapping lab tests to LOINC and medications to RxNorm—is a foundational step that transforms institution-specific data into a universal, analyzable format.

#### Constructing Features from Coded Events

With normalized codes, we can construct patient-level or visit-level feature vectors. Three common types of features are derived from coded event data [@problem_id:4563111]:

*   **Occurrence Features**: These are binary indicators that capture the presence or absence of a specific code within an aggregation unit (e.g., a patient's entire history or a single visit). For a given code $c$, the feature value is $1$ if the code appears at least once and $0$ otherwise.
*   **Frequency Features**: These are counts of how often a code occurs within the aggregation unit. This can be the total number of times a diagnosis was recorded for a patient or the number of times a procedure was performed during a visit.
*   **Burden Features**: These are weighted counts that aim to capture the clinical or economic significance of events. Each code $c$ is assigned a weight $w_c$, which could represent disease severity, resource utilization, or predictive risk. The burden feature is then the sum of weights for all occurrences of the code. For example, if a patient has two instances of a code $c$ with weight $w_c=1.5$, the frequency feature would be $2$ and the burden feature would be $2 \times 1.5 = 3.0$.

The choice between **per-visit** and **per-patient** aggregation depends on the analytical goal. Per-visit features describe the state of a single encounter, while per-patient features summarize an individual's entire history up to a point in time. For example, a per-patient frequency feature for a code is the sum of its frequencies across all of that patient's visits [@problem_id:4563111].

#### Dimensionality Reduction through Ontological Grouping

The space of all possible clinical codes is vast (e.g., over 70,000 codes in ICD-10-CM), leading to extremely high-dimensional and sparse feature vectors. This "[curse of dimensionality](@entry_id:143920)" can impair model performance and generalization. A powerful technique to mitigate this is **ontology-based code grouping**, where fine-grained codes are collapsed into a smaller number of clinically coherent parent categories [@problem_id:4563188]. For example, the Clinical Classifications Software (CCS) groups thousands of ICD codes into a few hundred categories.

This grouping, which maps a high-dimensional code variable $X$ to a lower-dimensional group variable $Z = \pi(X)$, is a form of [dimensionality reduction](@entry_id:142982). However, it comes with a trade-off: potential loss of information. The Data Processing Inequality from information theory states that for a Markov chain $Y \to X \to Z$, where $Y$ is the prediction target, the mutual information can only decrease or stay the same: $I(Y;X) \ge I(Y;Z)$. This means that collapsing features can never increase their predictive [information content](@entry_id:272315).

The critical question is: when is this [information loss](@entry_id:271961) minimal? The loss of information, $I(Y;X) - I(Y;Z)$, is precisely equal to the expected Kullback-Leibler (KL) divergence between the true posterior distribution given the fine-grained code, $\mathbb{P}(Y|X)$, and the posterior given the group, $\mathbb{P}(Y|Z)$:
$$ I(Y;X) - I(Y;Z) = \mathbb{E}_{X}\! \left[ \mathrm{KL}\! \left( \mathbb{P}(Y \mid X) \,\|\, \mathbb{P}(Y \mid Z) \right) \right] $$
This quantity is zero—meaning no information is lost—if and only if the posterior probability $\mathbb{P}(Y|X=x)$ is identical for all codes $x$ that are mapped to the same group $z$ [@problem_id:4563188]. In practice, this means that an effective grouping strategy should combine codes that have a similar relationship with the outcome of interest. For the simpler task of [binary classification](@entry_id:142257), the Bayes error rate is preserved if, within each group, all constituent codes lead to the same optimal prediction (e.g., all codes in a "high-risk" group are individually associated with a risk greater than $0.5$) [@problem_id:4563188].

### Feature Engineering from Clinical Narratives

Clinical narratives are a rich but challenging source of information. Feature engineering here focuses on extracting, normalizing, and numerically representing the concepts embedded in free text.

#### From Text to Concepts: The Role of Concept Normalization

A major challenge in processing clinical text is lexical variation: the same clinical concept can be expressed using different words or phrases. For example, one clinician might write "myocardial infarction," while another writes "heart attack." Without a way to reconcile these synonyms, NLP systems would treat them as entirely different features, failing to capture the underlying [semantic equivalence](@entry_id:754673).

The **Unified Medical Language System (UMLS)** provides a solution. The UMLS Metathesaurus groups synonymous terms from various source vocabularies into a single **Concept Unique Identifier (CUI)**. By mapping textual mentions to their corresponding CUIs, we perform **concept normalization**. This process collapses semantically equivalent but lexically different surface forms into a single, standardized feature.

This normalization is crucial for enabling cross-document and cross-institution comparability. Consider two documents, one mentioning "heart attack" and the other "myocardial infarction." In a simple token-based feature space, their vector representations would be orthogonal, with a [cosine similarity](@entry_id:634957) of $0$. After mapping both terms to the same CUI, their vector representations in the CUI space become identical, yielding a [cosine similarity](@entry_id:634957) of $1$. This process effectively removes variability due to synonym choice and ensures that similarity is measured at the conceptual level [@problem_id:4563183].

#### Representing Text Numerically: From Words to Vectors

Once concepts are identified, the text must be converted into a numerical format.

A foundational approach is the **Bag-of-Words (BoW)** model, where a document is represented as a vector of term frequencies, ignoring grammar and word order. To capture local context, such as negation, we can extend this to **n-grams**, which are contiguous sequences of $n$ words. For instance, the bigram (2-gram) "no fever" is treated as a single feature distinct from the unigram "fever". This allows a model to learn that "no fever" is a strong indicator of the *absence* of the fever phenotype, which is crucial for accurate phenotyping from clinical text [@problem_id:4563206].

Simple counts can be misleading, as common words like "patient" might dominate. **Term Frequency-Inverse Document Frequency (TF-IDF)** is a weighting scheme that addresses this by assessing a term's importance in a document relative to its frequency across the entire corpus. It is calculated as:
$$ \text{TF-IDF}(t, d) = \text{TF}(t, d) \times \text{IDF}(t) $$
where $\text{TF}(t, d)$ is the frequency of term $t$ in document $d$, and $\text{IDF}(t) = \log\left(\frac{N}{DF(t)}\right)$ is the inverse document frequency, with $N$ being the total number of documents and $DF(t)$ the number of documents containing term $t$. TF-IDF gives higher weight to terms that are frequent in a specific document but rare across the corpus, effectively highlighting informative keywords. For example, in a corpus of clinical notes, the word "sepsis" would have a much higher IDF (and thus a higher TF-IDF score in a relevant note) than the ubiquitous word "patient" [@problem_id:4563206].

Other techniques, such as **character n-grams**, can further improve robustness by breaking words into sub-word units. This allows the model to handle morphological variations (e.g., "diabetes," "diabetic") and out-of-vocabulary words by representing them through their shared character sequences [@problem_id:4563206].

#### Understanding Context: Assertion Status Modification

Extracting a concept is only the first step; we must also determine its **assertion status**. A patient note mentioning "pneumonia" could be affirming its presence, denying it, speculating about it, or referring to a past episode. These contextual nuances are captured by analyzing linguistic cues in the text. Key assertion categories and their corresponding cues include [@problem_id:4563161]:

*   **Present**: The concept holds at the time of documentation. This is often the default status in the absence of modifying cues.
*   **Absent**: The concept is explicitly denied. **Negation cues** like "denies," "no signs of," or "ruled out" place a concept in this category. For example, in "patient denies chest pain," the concept "chest pain" is `absent`.
*   **Possible**: The concept is uncertain. **Uncertainty cues** like "suggests," "possible," or "concern for" indicate that the concept is being considered but is not confirmed. For instance, "radiograph suggests possible pneumonia" classifies "pneumonia" as `possible`.
*   **Historical**: The concept was true in the past but is not active at present. **Temporality cues** like "history of" or specific past dates place a concept in this category. A sentence like "History of ischemic stroke in 2012" marks "[ischemic stroke](@entry_id:183348)" as `historical`.
*   **Planned**: The concept is intended to occur in the future. Future-oriented temporality cues like "plan to start" or "schedule for" signal this status. For example, "Plan to start insulin tomorrow" asserts "insulin" as `planned`.

A robust NLP pipeline must not only extract concepts but also classify their assertion status to avoid generating misleading features, such as flagging a patient as having a condition they were explicitly noted not to have.

### Advanced Considerations in Feature Engineering

Building effective and reliable models from EHR data requires mastering several advanced concepts that go beyond basic feature creation.

#### Handling the Temporal Dimension

EHR data is inherently longitudinal. When building predictive models, it is crucial to handle the time axis correctly to prevent [information leakage](@entry_id:155485), where the model is inadvertently trained on information that would not be available at prediction time. This is managed through a formal windowing framework [@problem_id:4563180]:

*   **Index Time ($\tau$)**: The specific point in time at which a prediction is made.
*   **Observation Window ($w_o$)**: The period of time *before* the index time from which features are extracted. For example, a 1-year look-back window.
*   **Prediction Window ($w_p$)**: The period of time *after* the index time during which the outcome is monitored. For example, a 30-day window to check for readmission.
*   **Gap Time ($g$)**: A buffer period immediately preceding the index time. Features are constructed using data only from before this gap (i.e., from the interval $(\tau - g - w_o, \tau - g]$). This is critical for mitigating leakage due to documentation delays, where information about an event at time $\tau$ might only appear in the EHR at time $\tau + \delta$.

Two common strategies for selecting index times are **landmarking**, which uses a few clinically meaningful time points (e.g., hospital discharge), and the **rolling window** approach, which generates a dense grid of index times along a patient's trajectory. Both methods require careful construction of the at-risk set (i.e., only making predictions for patients who have not yet had the event) to ensure a valid analysis [@problem_id:4563180, @problem_id:4563180].

#### The Challenge of Missing Data

EHR data is characterized by pervasive missingness. A lab test may not be ordered, or a patient may not report a specific symptom. The reason for this missingness is critical. There are three primary mechanisms [@problem_id:4563199]:

*   **Missing Completely At Random (MCAR)**: The probability of a value being missing is independent of both the observed and unobserved data. Formally, $P(R=1 | Y, X) = P(R=1)$, where $R$ is the missingness indicator, $Y$ is the variable of interest, and $X$ are covariates. An example is a lab sample being accidentally destroyed.
*   **Missing At Random (MAR)**: The probability of a value being missing depends only on the *observed* data, not on the unobserved value itself. Formally, $P(R=1 | Y, X) = P(R=1 | X)$. For example, if physicians are more likely to order a potassium test for older patients, but this decision is not related to the patient's true (but unknown) potassium level, the data are MAR.
*   **Missing Not At Random (MNAR)**: The probability of a value being missing depends on the unobserved value itself. Formally, $P(R=1 | Y, X)$ depends on $Y$. This is often called "informative missingness." For example, if a clinician forgoes a test because they have an unrecorded intuition that the result will be normal, the missingness is MNAR.

It is also vital to distinguish missingness from **censoring**. Censoring occurs when a measurement is obtained but is imprecise. For example, a lab assay with a lower [limit of detection](@entry_id:182454) $L$ might report a value as " L", which is an instance of [left-censoring](@entry_id:169731), not a missing value.