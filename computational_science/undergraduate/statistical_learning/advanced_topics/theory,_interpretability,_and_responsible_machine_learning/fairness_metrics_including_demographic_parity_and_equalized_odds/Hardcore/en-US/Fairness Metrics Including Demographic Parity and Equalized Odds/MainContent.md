## Introduction
As algorithms increasingly make high-stakes decisions about our lives, from loan approvals to medical diagnoses, ensuring their fairness has become as critical as maximizing their accuracy. But how can we mathematically define and measure fairness in a complex world? Simply ignoring sensitive attributes like race or gender is often not enough and can even perpetuate bias. This raises the need for explicit, quantifiable metrics to audit and correct algorithmic systems.

This article provides a comprehensive guide to two of the most fundamental concepts in [algorithmic fairness](@entry_id:143652). In the first chapter, "Principles and Mechanisms," we will dissect the mathematical foundations of Demographic Parity and Equalized Odds, exploring how they work and the inherent tensions between them. The second chapter, "Applications and Interdisciplinary Connections," will bridge theory and practice, demonstrating how these metrics are applied in fields like finance, healthcare, and even [environmental science](@entry_id:187998), revealing the complex trade-offs involved. Finally, the "Hands-On Practices" section will allow you to apply these concepts directly, building your skills in auditing and enforcing fairness in realistic scenarios. Let's begin by establishing the core principles and mechanisms that underpin the quest for fair algorithms.

## Principles and Mechanisms

In the evaluation of algorithmic systems, ensuring fairness is as critical as achieving high predictive accuracy. This chapter delves into the principles and mechanisms of two foundational statistical [fairness metrics](@entry_id:634499): **Demographic Parity** and **Equalized Odds**. We will explore their mathematical definitions, the methods used to enforce them, and the inherent trade-offs that arise when applying them in practice. We begin by formalizing the problem setting. Consider a classification task where for each individual, we have a sensitive attribute $A$ (e.g., race, gender), a set of other features $X$, a true outcome or label $Y$ (e.g., loan default, disease presence), and a model's prediction $\hat{Y}$. Both $Y$ and $\hat{Y}$ are typically binary, taking values in $\{0, 1\}$, where $1$ represents the positive or advantageous outcome.

### Demographic Parity: Equality of Selection Rates

The most straightforward notion of group fairness is [demographic parity](@entry_id:635293). This principle demands that the probability of receiving the positive outcome is independent of the sensitive attribute.

Formally, a classifier satisfies **Demographic Parity** (DP), also known as statistical parity, if the selection rate is equal across all groups defined by the sensitive attribute $A$. For two groups, $A=a$ and $A=b$, this is expressed as:

$$ P(\hat{Y}=1 \mid A=a) = P(\hat{Y}=1 \mid A=b) $$

This definition is appealing in its simplicity. It asserts that the model's impact, as measured by the proportion of positive predictions, should be identical for all demographic groups. It is "blind" to the true outcome $Y$, focusing solely on the distribution of the predictions $\hat{Y}$ with respect to $A$.

To understand the operational implications of this principle, consider a practical scenario of fair resource allocation . Imagine a decision-maker must distribute a scarce resource (e.g., a scholarship, a business loan) to a population of individuals. The decision to allocate the resource is represented by $\hat{Y}=1$, and not to allocate by $\hat{Y}=0$. The population is divided into two groups, $A=0$ and $A=1$, with sizes $n_0$ and $n_1$ respectively. Let $k_0$ and $k_1$ be the number of individuals from each group who receive the resource. In this finite sample context, the probabilities in the DP definition are estimated by the allocation rates:

$$ P(\hat{Y}=1 \mid A=0) \approx \frac{k_0}{n_0} \quad \text{and} \quad P(\hat{Y}=1 \mid A=1) \approx \frac{k_1}{n_1} $$

The [demographic parity](@entry_id:635293) constraint thus becomes $\frac{k_0}{n_0} = \frac{k_1}{n_1}$. This simple equation reveals the core mechanism of DP: it forces the proportion of positive outcomes to be equal, directly linking the number of allocations in one group to the number in another. If a decision-maker aims to maximize the total utility (e.g., societal benefit) from the allocation, subject to a capacity limit $K$ (i.e., $k_0 + k_1 \le K$), the problem becomes a constrained optimization task. This is a variant of the classic [knapsack problem](@entry_id:272416), where the fairness constraint adds a crucial dimension to the decision-making process. For example, if group sizes are $n_0=4$ and $n_1=6$, the DP constraint $\frac{k_0}{4} = \frac{k_1}{6}$ simplifies to $3k_0 = 2k_1$. To satisfy this with integers, the number of allocated individuals $(k_0, k_1)$ must be a multiple of $(2, 3)$. If the total capacity is $K=5$, the only non-trivial solution is to allocate to $k_0=2$ individuals from group $0$ and $k_1=3$ from group $1$, ensuring the allocation rate is exactly $0.5$ for both groups.

While [demographic parity](@entry_id:635293) is intuitive, its disregard for the true outcome $Y$ can be problematic. It may require granting a positive outcome to less qualified individuals in one group or denying it to more qualified individuals in another, simply to balance the selection rates. This can lead to suboptimal and potentially unfair decisions at the individual level, motivating the need for criteria that account for the true labels.

### Equalized Odds: Equality of Error Rates

To address the limitations of [demographic parity](@entry_id:635293), we can incorporate the true outcome $Y$ into our fairness definition. The principle of **Equalized Odds** (EO) requires that the model's predictions be independent of the sensitive attribute, conditional on the true outcome. This means the classifier should perform equally well for all groups, both for individuals who are genuinely positive ($Y=1$) and for those who are genuinely negative ($Y=0$).

This principle is formalized by requiring equality of both the **True Positive Rate (TPR)** and the **False Positive Rate (FPR)** across groups. The TPR, also known as sensitivity or recall, is the probability of a correct positive prediction among the true positives. The FPR is the probability of an incorrect positive prediction among the true negatives.

$$ \text{TPR}_a = P(\hat{Y}=1 \mid Y=1, A=a) $$
$$ \text{FPR}_a = P(\hat{Y}=1 \mid Y=0, A=a) $$

A classifier satisfies [equalized odds](@entry_id:637744) if for any two groups $a$ and $b$:

$$ \text{TPR}_a = \text{TPR}_b \quad \text{and} \quad \text{FPR}_a = \text{FPR}_b $$

Enforcing [equalized odds](@entry_id:637744) ensures that, for instance, a qualified applicant from group $a$ has the same chance of being correctly identified as a qualified applicant from group $b$. Likewise, it ensures that an unqualified applicant from either group has the same chance of being incorrectly flagged.

#### Mechanisms for Achieving Equalized Odds

Achieving [equalized odds](@entry_id:637744) often involves post-processing the output of a standard classifier. Two common mechanisms are group-specific thresholding and randomized post-processing.

**1. Group-Specific Thresholding**

Most classifiers produce a continuous score $s(x)$, which is then thresholded to make a binary prediction (e.g., $\hat{Y}=1$ if $s(x) \ge t$). A single, universal threshold $t$ applied to all individuals will generally not satisfy [equalized odds](@entry_id:637744) if the score distributions differ across groups. A more flexible approach is to use group-specific thresholds, $t_a$ and $t_b$.

The relationship between the threshold and the (TPR, FPR) pair for a given group defines its **Receiver Operating Characteristic (ROC) curve**. By choosing different thresholds for each group, we can select different points on their respective ROC curves. To satisfy [equalized odds](@entry_id:637744), we must find thresholds $t_a$ and $t_b$ such that the resulting $(\text{FPR}_a, \text{TPR}_a)$ and $(\text{FPR}_b, \text{TPR}_b)$ are identical. This is possible if the ROC curves for the groups intersect at some non-trivial point.

For instance, consider a model that produces a calibrated score $s(x)$, meaning $P(Y=1 \mid s(x)=s) = s$. With discrete scores, we can calculate the exact (TPR, FPR) pairs achievable at different thresholds for each group. By finding a common (TPR, FPR) pair in the sets of achievable points for all groups, we can enforce [equalized odds](@entry_id:637744) . A more advanced analysis with continuous score distributions allows for the derivation of TPR and FPR as continuous functions of the threshold, e.g., $\text{TPR}_a(t_a)$ and $\text{FPR}_a(t_a)$. The [equalized odds](@entry_id:637744) constraint then creates a system of two equations, $\text{TPR}_a(t_a) = \text{TPR}_b(t_b)$ and $\text{FPR}_a(t_a) = \text{FPR}_b(t_b)$, which can be solved for the thresholds $t_a$ and $t_b$ . This can also be achieved by training separate models for each group (stratified training) and then applying group-specific thresholds to align their performance metrics .

**2. Randomized Post-Processing**

In some cases, especially with a small number of discrete score values, pure thresholding may not be flexible enough to achieve a desired (TPR, FPR) target. A more general technique is to introduce [randomization](@entry_id:198186) into the decision-making process. For each group $a$ and each possible score value $s$, we can define a probability $p_{a,s}$ of assigning a positive prediction $\hat{Y}=1$.

$$ p_{a,s} = P(\hat{Y}=1 \mid A=a, s(x)=s) $$

The group's overall TPR and FPR can then be expressed as [linear combinations](@entry_id:154743) of these [randomization](@entry_id:198186) probabilities. This results in a system of linear equations that can be solved to find the values of $p_{a,s}$ that achieve the target TPR and FPR for each group, thereby satisfying [equalized odds](@entry_id:637744) . This method offers greater control but comes at the cost of making the classifier's decisions non-deterministic for a given individual.

### The Inherent Tensions Between Fairness Metrics

A central challenge in [algorithmic fairness](@entry_id:143652) is that satisfying one fairness criterion often means violating another. This is not a flaw in the definitions themselves but a fundamental property of the world, particularly when the underlying **base rates** ($P(Y=1 \mid A=a)$) differ across groups.

#### Equalized Odds vs. Demographic Parity

The relationship between the selection rate and the error rates is given by the law of total probability:
$$ P(\hat{Y}=1 \mid A=a) = \mathrm{TPR}_a \cdot P(Y=1 \mid A=a) + \mathrm{FPR}_a \cdot (1 - P(Y=1 \mid A=a)) $$

Let's assume a classifier satisfies [equalized odds](@entry_id:637744), so $\mathrm{TPR}_a = \mathrm{TPR}_b = \text{TPR}$ and $\mathrm{FPR}_a = \mathrm{FPR}_b = \text{FPR}$. For [demographic parity](@entry_id:635293) to hold, we need $P(\hat{Y}=1 \mid A=a) = P(\hat{Y}=1 \mid A=b)$. Substituting the equation above gives:

$$ \text{TPR} \cdot \pi_a + \text{FPR} \cdot (1 - \pi_a) = \text{TPR} \cdot \pi_b + \text{FPR} \cdot (1 - \pi_b) $$
where $\pi_a = P(Y=1 \mid A=a)$ is the base rate for group $a$. Rearranging this equation yields:
$$ (\text{TPR} - \text{FPR})(\pi_a - \pi_b) = 0 $$

This remarkable result shows that if a classifier is informative (i.e., $\text{TPR} > \text{FPR}$), then [equalized odds](@entry_id:637744) and [demographic parity](@entry_id:635293) can hold simultaneously *only if* the base rates are equal ($\pi_a = \pi_b$). In many real-world settings, base rates differ between groups. For example, the prevalence of a disease may be different across different populations. In such cases, it is mathematically impossible to satisfy both [equalized odds](@entry_id:637744) and [demographic parity](@entry_id:635293) with a useful classifier . In fact, enforcing [equalized odds](@entry_id:637744) when base rates are different can sometimes *increase* the [demographic parity](@entry_id:635293) gap compared to a standard, unconstrained classifier.

#### Equalized Odds vs. Predictive Parity

Another important fairness criterion is **Predictive Parity**, which requires that the **Positive Predictive Value (PPV)** be equal across groups. PPV, or precision, is the probability that an individual who received a positive prediction truly belongs to the positive class.

$$ \text{PPV}_a = P(Y=1 \mid \hat{Y}=1, A=a) $$

Predictive parity ensures that a positive prediction from the model carries the same meaning regardless of an individual's group membership. Using Bayes' theorem, we can express PPV in terms of TPR, FPR, and the base rate $\pi_a$ :

$$ \text{PPV}_a = \frac{P(\hat{Y}=1 \mid Y=1, A=a)P(Y=1 \mid A=a)}{P(\hat{Y}=1 \mid A=a)} = \frac{\text{TPR} \cdot \pi_a}{\text{TPR} \cdot \pi_a + \text{FPR} \cdot (1 - \pi_a)} $$

From this equation, it is clear that even if a classifier satisfies [equalized odds](@entry_id:637744) (equal TPR and FPR), the PPV will still depend on the group-specific base rate $\pi_a$. If the base rates $\pi_a$ and $\pi_b$ are different, then $\text{PPV}_a$ and $\text{PPV}_b$ will also be different. For example, if a disease is much rarer in group $A$ ($\pi_A$ is low) than in group $B$ ($\pi_B$ is high), then even with an EO-compliant test, a positive result for someone in group $A$ is much more likely to be a false alarm than a positive result for someone in group $B$. This illustrates a three-way conflict: one generally cannot satisfy [demographic parity](@entry_id:635293), [equalized odds](@entry_id:637744), and predictive parity all at once if base rates differ.

#### Equalized Odds vs. Calibration

**Calibration** is a desirable property of a probabilistic classifier, where the predicted score $\hat{p}$ accurately reflects the true probability of the positive outcome. A model is calibrated if, for any score value $s$, the subset of individuals who receive that score have a [true positive rate](@entry_id:637442) of $s$, i.e., $P(Y=1 \mid \hat{p}=s) = s$. Interventions to enforce fairness, such as the post-processing methods for [equalized odds](@entry_id:637744), can disrupt a model's calibration.

Consider a model that is initially well-calibrated for each group. If we then apply post-processing [randomization](@entry_id:198186) to achieve [equalized odds](@entry_id:637744), the new prediction probabilities $\tilde{p}$ will generally no longer be calibrated. For instance, a simple intervention might collapse all predictions to a single probability (e.g., $\tilde{p}=0.5$ for everyone), which would satisfy EO with TPR=FPR=0.5 but would be severely miscalibrated unless the true base rate in every subgroup happened to be exactly $0.5$. This miscalibration can be quantified by measuring the deviation $\mathbb{E}[Y \mid \tilde{p}, A=a] - \tilde{p}$ and is reflected in an increase in metrics like the **Brier score**, which measures the [mean squared error](@entry_id:276542) between predicted probabilities and true outcomes .

### A Glimpse into Causal Fairness

The statistical [fairness metrics](@entry_id:634499) discussed so far are observational. They describe disparities in outcomes between groups but do not address the causal pathways that produce these disparities. Causal fairness provides a deeper, alternative perspective.

One key concept is **Counterfactual Fairness**. A decision is counterfactually fair if it would have been the same for an individual had their sensitive attribute been different, holding all else constant (i.e., fixing the background factors unique to that individual). Consider a causal model where the sensitive attribute $A$ can influence both a feature $X$ and the outcome $Y$ directly ($A \to X \to Y$ and $A \to Y$). A classifier that uses $X$ to make a prediction, $\hat{Y} = f(X)$, is not counterfactually fair. This is because intervening to change an individual's attribute from $A=a$ to $A=b$ would change the value of $X$, and thus potentially change the prediction $\hat{Y}$. This holds true even if $X$ does not explicitly encode $A$ .

This reveals a fundamental disconnect between statistical and causal notions of fairness. A classifier can satisfy a statistical criterion like [equalized odds](@entry_id:637744) yet fail to be counterfactually fair. Causal fairness forces us to grapple with the data-generating process itself, asking not just whether outcomes are correlated with sensitive attributes, but *why* they are. While computationally more demanding, the causal perspective offers a powerful lens for reasoning about the underlying sources of bias and designing more robustly fair systems.