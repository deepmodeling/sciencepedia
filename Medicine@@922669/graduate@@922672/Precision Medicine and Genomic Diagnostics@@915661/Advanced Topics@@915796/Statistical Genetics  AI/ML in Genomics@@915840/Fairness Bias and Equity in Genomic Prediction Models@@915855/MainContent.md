## Introduction
Genomic prediction models, such as [polygenic risk scores](@entry_id:164799), hold immense promise for advancing precision medicine by personalizing disease risk assessment and prevention. However, this potential is shadowed by a critical challenge: the risk of perpetuating and even exacerbating existing health disparities. Models trained on data from predominantly European-ancestry populations have consistently shown reduced accuracy and biased performance when applied to individuals from other ancestries, raising urgent questions about fairness and equity. This article directly addresses this knowledge gap by providing a systematic exploration of bias in genomic prediction, from its theoretical foundations to its practical implications.

Over the following chapters, you will gain a comprehensive understanding of this complex field. The first chapter, **Principles and Mechanisms**, will establish a formal vocabulary for fairness, dissecting the key statistical criteria and the specific mechanisms—from data ascertainment to population genetics—that introduce bias into the modeling pipeline. The second chapter, **Applications and Interdisciplinary Connections**, will bridge theory and practice, demonstrating how to build more equitable models, audit them rigorously, and navigate their deployment within clinical, ethical, and legal frameworks. Finally, the **Hands-On Practices** chapter will offer opportunities to apply these concepts through guided computational exercises. We begin by delving into the core principles that allow us to rigorously define, measure, and reason about fairness in genomic prediction.

## Principles and Mechanisms

This chapter delves into the core principles and mechanisms that underpin fairness, bias, and equity in genomic prediction models. We will begin by establishing a formal vocabulary for discussing fairness, defining the key statistical criteria used to measure and audit model performance across different population groups. Subsequently, we will undertake a systematic exploration of the primary sources and mechanisms of bias in the genomic prediction pipeline—from data generation and processing to model training and evaluation. Finally, we will advance our discussion to encompass more sophisticated causal frameworks for defining and enforcing fairness, and conclude by examining the inherent tensions that can arise between different conceptions of what it means for a model to be fair.

### Formalizing Fairness: Key Statistical Criteria

To rigorously analyze and compare the behavior of predictive models across different population groups, we must first define a clear set of mathematical criteria for fairness. These criteria are typically expressed as statistical properties that a model's predictions should satisfy with respect to a protected group attribute, denoted by $G$. Let $Y \in \{0, 1\}$ be the true [binary outcome](@entry_id:191030) of interest (e.g., disease status), $S \in [0, 1]$ be a continuous risk score produced by a model, and $\hat{Y} \in \{0, 1\}$ be the binary prediction derived from thresholding the score $S$ at some value $t$.

The fairness criteria can be broadly categorized based on the information they condition on: independence, separation, and sufficiency [@problem_id:4338555].

#### Independence Criteria

Independence criteria demand that the model's predictions be statistically independent of the protected group attribute $G$. The most common criterion in this class is **[demographic parity](@entry_id:635293)** (or **statistical parity**).

**Demographic Parity** requires that the rate of positive predictions be equal across all groups. Formally, for any two groups $g_1, g_2$ in the population:
$$
P(\hat{Y}=1 \mid G=g_1) = P(\hat{Y}=1 \mid G=g_2)
$$
This criterion focuses solely on the model's outputs, ignoring the true outcome $Y$. It ensures that all groups receive predictions at the same rate, which might be desirable for resource allocation. However, it can conflict with predictive accuracy, especially if the underlying prevalence of the outcome, $P(Y=1 \mid G=g)$, differs across groups. For a model using a score threshold $t$, this condition is equivalent to requiring $P(S \ge t \mid G=g)$ to be constant across groups [@problem_id:4338555].

#### Separation Criteria

Separation criteria condition on the true outcome $Y$, requiring that the model's predictions be independent of the group attribute $G$ for individuals with the same true outcome. These criteria focus on the equality of error rates.

**Equalized Odds** is the primary criterion in this family. It demands that both the **[true positive rate](@entry_id:637442) (TPR)** and the **false positive rate (FPR)** be equal across all groups.
$$
\text{TPR: } P(\hat{Y}=1 \mid Y=1, G=g_1) = P(\hat{Y}=1 \mid Y=1, G=g_2)
$$
$$
\text{FPR: } P(\hat{Y}=1 \mid Y=0, G=g_1) = P(\hat{Y}=1 \mid Y=0, G=g_2)
$$
Equalized odds ensures that the model performs equally well for affected individuals (in terms of TPR) and unaffected individuals (in terms of FPR) regardless of their group membership. It is often considered a strong standard for fairness in applications like medical screening, where the consequences of false negatives and false positives are significant [@problem_id:4338555].

A common relaxation of equalized odds is **Equal Opportunity**. This criterion requires equality only of the true positive rate across groups.
$$
P(\hat{Y}=1 \mid Y=1, G=g_1) = P(\hat{Y}=1 \mid Y=1, G=g_2)
$$
This focuses on ensuring that individuals who are genuinely positive for the outcome have an equal chance of being correctly identified, irrespective of their group. This is particularly relevant in contexts where maximizing benefit for the "positive" class is the primary concern [@problem_id:4338555].

#### Sufficiency Criteria

Sufficiency criteria condition on the model's prediction $\hat{Y}$ or score $S$. They demand that, given the prediction, the true outcome $Y$ is independent of the group attribute $G$.

**Predictive Parity** requires that the **positive predictive value (PPV)** be equal across groups.
$$
P(Y=1 \mid \hat{Y}=1, G=g_1) = P(Y=1 \mid \hat{Y}=1, G=g_2)
$$
This criterion ensures that a positive prediction carries the same meaning and implies the same probability of having the condition, regardless of an individual's group. This is crucial for building trust and ensuring that interventions based on a positive prediction are equitably applied. Using Bayes' rule, achieving predictive parity is closely tied to both the model's error rates (TPR, FPR) and the underlying group-specific disease prevalence, $P(Y=1 \mid G=g)$ [@problem_id:4338555].

A stronger, score-based version of this idea is **Calibration**. A model is said to be **calibrated within groups** if, for any given risk score $s$, the probability of a positive outcome for an individual with that score is equal to $s$, and this holds within each group.
$$
P(Y=1 \mid S=s, G=g) = s \quad \text{for all } s \text{ and } g
$$
Calibration ensures that the risk score has a consistent, probabilistic interpretation across all individuals and groups. If a model is calibrated, it automatically satisfies predictive parity at every score threshold. However, it is a very strong condition that is often difficult to achieve in practice [@problem_id:4338555]. It is also important to note that these various fairness criteria are often mutually exclusive; except in trivial cases, it is mathematically impossible for a model to satisfy [demographic parity](@entry_id:635293), [equalized odds](@entry_id:637744), and predictive parity simultaneously if the base rates of the outcome differ between groups.

### Mechanisms of Bias and Inequity in Genomic Prediction

Disparities in the performance of genomic prediction models do not arise from a vacuum. They are the result of specific, identifiable mechanisms that introduce bias at various stages of the model development lifecycle. Understanding these mechanisms is essential for diagnosing, mitigating, and ultimately preventing inequitable outcomes.

#### Bias from Data Generation and Composition

The first point at which bias can be introduced is during the very creation of the datasets used for training and validation.

**Ascertainment Bias** in biobank recruitment is a primary concern. Most large-scale genomic datasets are not random samples of the population but are assembled through specific recruitment strategies. Retrospective case-control studies, for example, intentionally oversample individuals with the disease. If the probabilities of being included in the study differ for cases and controls across different ancestral groups, this introduces **ascertainment bias**. As demonstrated in [@problem_id:4338531], such group-specific sampling imbalances can systematically distort the calibration of a risk model. If the selection probabilities for cases ($s_{1g} = P(\text{Sampled} \mid Y=1, G=g)$) and controls ($s_{0g} = P(\text{Sampled} \mid Y=0, G=g)$) differ by group $g$, the relationship between the log-odds of disease in the sample and the [log-odds](@entry_id:141427) in the target population is shifted by a group-specific offset, $\delta_g = \ln(s_{1g}/s_{0g})$. A model trained on such a biobank may be well-calibrated to the biased sample but will be miscalibrated when applied to the general population, with the degree of miscalibration varying by group. This necessitates group-specific correction to recover true population risk estimates.

**Confounding by Ancestry**, also known as **[population stratification](@entry_id:175542)**, is another fundamental source of bias originating from data generation [@problem_id:4338590]. In human populations, ancestry is correlated with both genetic variation and environmental or social exposures. A Directed Acyclic Graph (DAG) can illustrate this: ancestry ($A$) can be a common cause of both genotype ($G$) and a relevant environmental factor ($E$), with both $G$ and $E$ in turn causing the disease outcome ($Y$). This creates a non-causal "backdoor path" between genotype and disease: $G \leftarrow A \rightarrow E \rightarrow Y$. If a genomic predictor is trained by regressing $Y$ on $G$ alone, it will mistakenly attribute the effect of the environmental confounder $E$ to the genotype $G$. The estimated effect of the genotype, $\hat{\beta}_G$, will be biased by a term proportional to the covariance between $G$ and $E$, which is non-zero due to their shared cause, $A$. This can lead to spurious associations and a predictor that performs poorly and inequitably, as its predictions are entangled with environmental and social factors that are unfairly distributed across ancestral groups.

#### Bias from Population-Specific Genetic Architecture

Even with perfectly representative data, differences in the genetic architecture between populations can lead to performance disparities. A crucial mechanism is the variation in **Linkage Disequilibrium (LD)** patterns across ancestries [@problem_id:4338578]. Genome-wide association studies (GWAS) often identify "tag" SNPs that are statistically associated with a trait but may not be the true causal variants. These tag SNPs are useful because they are in high LD (i.e., strongly correlated) with the causal variants. A [polygenic risk score](@entry_id:136680) (PRS) is built using the effects of these tag SNPs.

The problem arises when such a predictor is applied to a new population with different LD patterns. For instance, a PRS developed in a European-ancestry cohort may be applied to an African-ancestry cohort. Due to the greater genetic diversity and older evolutionary history of African populations, LD blocks are generally smaller. A tag SNP that is an excellent proxy for a causal variant in European populations (e.g., correlation $r_A$) may be a much poorer proxy in African populations (correlation $r_B  r_A$). As derived in [@problem_id:4338578], the predictive accuracy of the tag SNP, measured by the [coefficient of determination](@entry_id:168150) ($R^2$), is proportional to the square of this correlation. When transferred from population A to B, the predictor's performance is expected to drop by a factor of $(r_B/r_A)^2$. This decay in predictive power due to LD mismatch is a primary driver of the observed portability gap for many PRS across different ancestries.

#### Bias from Data Processing and Modeling

Bias can also be introduced or amplified during the data processing and modeling stages.

**Differential Imputation Quality** is a key example [@problem_id:4338586]. Genotype [imputation](@entry_id:270805)—the [statistical inference](@entry_id:172747) of unobserved genotypes from a smaller set of typed markers—is a standard procedure. The accuracy of [imputation](@entry_id:270805) depends heavily on the quality and diversity of the reference panel of [haplotypes](@entry_id:177949) used. If a reference panel is predominantly composed of haplotypes from one ancestral group (e.g., European), the imputation quality for individuals from underrepresented groups will be lower. This can be modeled as a group-specific [imputation](@entry_id:270805) error. Lower imputation quality introduces more noise into the imputed genotypes for the underrepresented group. When a PRS is calculated from these noisier imputed genotypes, its variance is inflated, and its correlation with the true PRS is attenuated. This leads to a group-specific miscalibration, where the observed PRS for the underrepresented group will appear to have a weaker effect on the outcome than it truly does. The calibration slope of the true PRS on the imputed PRS, which should ideally be 1, becomes a value less than 1 that is smaller for groups with poorer [imputation](@entry_id:270805) quality, systematically underestimating risk for those groups.

**Regularization and Sample Size Imbalance** can also create disparities [@problem_id:4338587]. Penalized regression methods like [ridge regression](@entry_id:140984) are commonly used to build stable predictors by shrinking effect size estimates towards zero, which helps prevent overfitting. The degree of shrinkage is controlled by a [penalty parameter](@entry_id:753318), $\lambda$. A critical issue arises when a single, fixed $\lambda$ is used to train models in the context of vastly different sample sizes for different groups. The effective shrinkage applied to an effect estimate depends on the ratio of the penalty $\lambda$ to the amount of data available (proportional to sample size $n$). For an underrepresented group with a small $n$, a fixed $\lambda$ results in much stronger shrinkage compared to a well-represented group with a large $n$. This can lead to excessive bias for the smaller group, where true genetic effects are aggressively and inappropriately shrunk towards zero. Consequently, the predictor for the underrepresented group suffers from a large bias component in its prediction error, leading to systematically poorer performance compared to the majority group, even when the underlying biology is identical.

#### Bias in Model Evaluation

Finally, bias can emerge in the very process of evaluating a model's fairness.

**Differential Misclassification of Labels** occurs when the "ground truth" clinical labels used to train and audit a model are themselves subject to group-specific error rates [@problem_id:4338606]. For example, if access to high-quality diagnostics or the clinical criteria for diagnosis differ between groups, the observed diagnosis $D$ may be a noisy proxy for the true biological status $Y$, with the error rate $e_g = P(D \neq Y \mid G=g)$ varying by group. In this scenario, [fairness metrics](@entry_id:634499) computed using the noisy labels, such as the observed TPR ($P(\hat{Y}=1 \mid D=1, g)$) and FPR ($P(\hat{Y}=1 \mid D=0, g)$), will not reflect the true model performance. The observed rates become complex mixtures of the true TPR and FPR, with weights that depend on both the group-specific error rate $e_g$ and the group-specific disease prevalence $\pi_g$. A naive fairness audit based on these observed rates could be highly misleading, potentially masking true disparities or creating the illusion of disparities where none exist. Correcting for this measurement error by solving for the true rates is necessary for a valid fairness assessment.

### Advanced Causal and Individual-Level Perspectives

While statistical fairness criteria are essential for auditing models, they are fundamentally observational and can sometimes fall short of capturing our ethical intuitions about fairness, which are often causal in nature.

#### Counterfactual Fairness

Causal inference provides a more powerful language for defining fairness through the **Structural Causal Model (SCM)** framework [@problem_id:4338576]. In an SCM, we model the data-generating process with a set of [structural equations](@entry_id:274644), where each variable is a deterministic function of its direct causes and an exogenous (unexplained) error term. The set of all exogenous variables for an individual, $U$, can be thought of as representing their unique, immutable characteristics—everything about them that is not caused by other variables in the model.

**Counterfactual Fairness** is defined based on this framework. A predictor $\hat{Y}$ is counterfactually fair with respect to a protected attribute $A$ if, for any individual (i.e., for any fixed $U=u$), their predicted outcome would be the same even if we had hypothetically intervened to change their protected attribute. Formally:
$$
\hat{Y}_{A \leftarrow a}(U) = \hat{Y}_{A \leftarrow a'}(U) \quad \text{for all } a, a'
$$
This criterion captures the intuitive idea that a decision should not change "but for" an individual's protected attribute. In genomics, the exogenous variables $U$ represent the collection of latent factors like an individual's complete genetic blueprint (of which the measured genotype $G$ is a partial and noisy observation), unmeasured environmental exposures, and stochastic [biological noise](@entry_id:269503). It is crucial to distinguish these truly exogenous factors from endogenous variables like principal components of the genotype matrix, which are functions of the measured data and thus cannot be part of $U$ [@problem_id:4338576].

#### Path-Specific Fairness

In some cases, we may not wish to block all causal pathways from a protected attribute to an outcome. For instance, we might deem a pathway reflecting systemic bias to be unfair, while another pathway reflecting a biological reality to be acceptable. **Path-Specific Counterfactual Fairness** allows for this nuance [@problem_id:4338539].

Consider an SCM where ancestry $A$ influences environment $E$, a clinical mediator $M$, and the outcome $Y$. Genotype $G$ also influences $M$ and $Y$. An ethical stance might hold that causal pathways from $A$ to $Y$ that pass through societal factors like $E$ or potentially biased mediators like $M$ are unfair, while the influence of an individual's own genotype $G$ is permissible. To formalize this, one can define a "fair" prediction as the counterfactual outcome that would be realized if all unfair pathways were disabled. This is achieved by constructing a prediction using nested counterfactuals: we feed the model an individual's factual genotype $G$, but for all other inputs that are descendants of $A$, we use the values they would have taken had the individual's ancestry been set to some baseline reference value, $a_0$. This surgically blocks the unfair influences while preserving the permitted ones, providing a flexible and powerful tool for aligning models with specific ethical principles.

#### The Conflict Between Individual and Group Fairness

Finally, it is important to recognize that different formalisms of fairness can be in direct conflict. A prominent example is the tension between **Individual Fairness (IF)** and **Group Fairness** criteria like statistical parity or equalized odds [@problem_id:4338580].

Individual Fairness is often defined as a Lipschitz condition: for any two individuals $x$ and $x'$, their predictions should be close if their features are similar, i.e., $|\hat{f}(x) - \hat{f}(x')| \le L \cdot d(x, x')$, where $d(\cdot, \cdot)$ is a task-specific distance metric. This captures the principle that "similar individuals should be treated similarly."

The conflict arises when the chosen distance metric $d$ is itself correlated with the protected group attribute. In genomics, a natural distance metric is the Euclidean distance between genotype vectors. Due to population structure, the average genetic distance between two individuals from different continental ancestries is systematically larger than the average distance between two individuals from the same ancestry. This is because allele frequencies differ at many loci, adding a component to the inter-group distance that reflects the divergence between population means.

When this is the case, the IF constraint becomes systematically more permissive for inter-group comparisons than for intra-group comparisons. An accuracy-maximizing model can exploit this leeway. It is "allowed" by the IF constraint to make substantially different predictions for an individual from group A versus group B, because their genetic distance is large. If true risk differs between the groups, the model will learn to separate their predictions, leading to different group-average scores and error rates. This directly violates group fairness criteria like statistical parity or equalized odds. This demonstrates a deep-seated conflict: a fairness criterion designed to protect individuals based on similarity can inadvertently sanction group-level disparities when the very notion of "similarity" is entangled with group identity.