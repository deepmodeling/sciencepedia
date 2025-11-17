## Introduction
In the study of evolutionary biology, a central challenge is understanding the inheritance of [complex traits](@entry_id:265688)—like height, behavior, or disease susceptibility—that vary continuously among individuals. These traits are shaped by a combination of genetic and environmental factors, but how can we disentangle these influences to predict how a trait will evolve? This question lies at the heart of quantitative genetics, and the concept of heritability provides the key. The fundamental problem is to partition the observable [phenotypic variation](@entry_id:163153) within a population into its genetic and environmental components. Heritability quantifies the proportion of this variation that is attributable to genes. However, not all genetic influence is passed down predictably. This leads to a crucial distinction between [broad-sense heritability](@entry_id:267885), which captures all genetic effects, and [narrow-sense heritability](@entry_id:262760), which isolates the component that reliably determines resemblance between relatives and fuels evolutionary change. This article will guide you through this foundational concept in three parts. First, **Principles and Mechanisms** will decompose [phenotypic variance](@entry_id:274482), define broad- and [narrow-sense heritability](@entry_id:262760), and explain why [narrow-sense heritability](@entry_id:262760) is the key to predicting evolution. Next, **Applications and Interdisciplinary Connections** will demonstrate how [heritability](@entry_id:151095) is estimated and used in fields from agriculture to human genomics, and how it helps test evolutionary hypotheses. Finally, **Hands-On Practices** will provide practical exercises to solidify your understanding of these critical quantitative tools.

## Principles and Mechanisms

The study of [quantitative traits](@entry_id:144946)—those that vary continuously, such as height, weight, or yield—rests on a foundational principle: the partitioning of observable [phenotypic variation](@entry_id:163153) into its underlying genetic and environmental causes. This chapter delves into the principles and mechanisms of this partitioning, defining the key concepts of broad-sense and [narrow-sense heritability](@entry_id:262760). We will explore how these measures are derived, what they signify about the [genetic architecture](@entry_id:151576) of a trait, and how they are used to predict evolutionary change. Furthermore, we will address their limitations and common misinterpretations, providing a rigorous framework for their application in evolutionary biology.

### The Fundamental Partition of Phenotypic Variance

The starting point for any quantitative [genetic analysis](@entry_id:167901) is a simple, yet powerful, model that conceptualizes an individual's phenotype ($P$) as the sum of a contribution from its genotype ($G$) and a deviation caused by its environment ($E$):

$P = G + E$

This model allows us to decompose the total [phenotypic variance](@entry_id:274482) ($V_P$) in a population. The variance of a sum of two variables is the sum of their variances plus twice their covariance. Therefore, the [phenotypic variance](@entry_id:274482) is:

$V_P = V_G + V_E + 2\text{Cov}(G,E)$

where $V_G$ is the genetic variance, $V_E$ is the environmental variance, and $\text{Cov}(G,E)$ is the genotype-environment covariance. A non-zero $\text{Cov}(G,E)$ implies that genotypes are not randomly distributed across environments; for example, if individuals with genotypes for high yield are systematically placed in resource-rich environments. In well-designed experiments, this covariance can be eliminated by randomly assigning individuals to different environmental conditions, ensuring that $\text{Cov}(G,E) = 0$.

However, this model can be incomplete. The effect of a genotype may itself depend on the environment. This phenomenon, known as **[genotype-by-environment interaction](@entry_id:155645)** (G×E), requires adding an interaction term ($I_{GE}$) to our model:

$P = G + E + I_{GE}$

To achieve a clean partition of variance, this interaction term is statistically defined to be orthogonal to the [main effects](@entry_id:169824) of genotype and environment. This means that the average interaction effect for any given genotype across all environments is zero, and the average interaction effect for any given environment across all genotypes is zero. These orthogonality conditions, practically achieved through balanced experimental designs, ensure that the covariance between the [interaction term](@entry_id:166280) and the [main effects](@entry_id:169824) is zero [@problem_id:2695414].

Under these conditions—no genotype-environment covariance and an orthogonal [interaction term](@entry_id:166280)—the [phenotypic variance](@entry_id:274482) neatly decomposes into a sum of three components:

$V_P = V_G + V_E + V_{GE}$

Here, $V_G = \text{Var}(G)$ represents the variance due to genetic differences among individuals, $V_E = \text{Var}(E)$ represents variance due to environmental differences (including [developmental noise](@entry_id:169534) and [measurement error](@entry_id:270998)), and $V_{GE} = \text{Var}(I_{GE})$ is the variance due to genotype-by-environment interactions. This partitioning is the fundamental equation upon which the concept of heritability is built.

### Decomposing Genetic Variance: Additive, Dominance, and Epistatic Effects

The total genetic variance, $V_G$, is itself a composite term. It can be partitioned into components that reflect different types of gene action. The three primary components are:

1.  **Additive Genetic Variance ($V_A$)**: This component arises from the average effects of alleles. It represents the part of the [genetic variation](@entry_id:141964) that is transmitted predictably from parents to offspring. The sum of these average effects for an individual is known as their **[breeding value](@entry_id:196154)**.

2.  **Dominance Variance ($V_D$)**: This component arises from interactions between alleles at the same locus. The phenotype of a heterozygote is not simply the average of the two corresponding homozygotes, and this deviation from additivity contributes to $V_D$.

3.  **Epistatic (or Interaction) Variance ($V_I$)**: This component arises from interactions between alleles at different loci. The effect of an allele at one locus depends on which alleles are present at other loci.

Thus, the total [genetic variance](@entry_id:151205) is decomposed as:

$V_G = V_A + V_D + V_I$

It is crucial to understand that these components are statistical abstractions, not direct measures of underlying biochemical mechanisms [@problem_id:2695438]. They are defined based on a statistical model, typically a [least-squares regression](@entry_id:262382), applied to a specific population with its unique [allele frequencies](@entry_id:165920). The **additive genetic value** (or [breeding value](@entry_id:196154), $A$) of an individual is formally defined as the best linear predictor of its genotypic value ($G$) based on its allele counts. The **dominance deviation** ($D$) and **epistatic deviation** ($I$) are the residuals—the parts of the genotypic value that are not explained by this simple additive model. Because they are defined as statistical partitions within a specific population, their magnitudes ($V_A$, $V_D$, $V_I$) will change if allele frequencies change. They are properties of a population, not immutable properties of the genes themselves.

### Defining Heritability: Broad-Sense ($H^2$) and Narrow-Sense ($h^2$)

With the full [variance decomposition](@entry_id:272134) in place, we can define the two main types of heritability.

**Broad-sense [heritability](@entry_id:151095) ($H^2$)** is the proportion of the total [phenotypic variance](@entry_id:274482) that is due to [genetic variance](@entry_id:151205) of any kind. It quantifies the overall extent to which genetic differences among individuals contribute to phenotypic differences among them.

$H^2 = \frac{V_G}{V_P} = \frac{V_A + V_D + V_I}{V_P}$

**Narrow-sense heritability ($h^2$)** is the proportion of the total [phenotypic variance](@entry_id:274482) that is due to [additive genetic variance](@entry_id:154158) only.

$h^2 = \frac{V_A}{V_P}$

From these definitions, it is evident that $H^2 \ge h^2$. The two are equal only when all non-[additive genetic variance](@entry_id:154158) is zero ($V_D = 0$ and $V_I = 0$). This can occur if gene action is purely additive, or if there is no [heterozygosity](@entry_id:166208) (e.g., in a population of haploids or fully inbred lines), which means dominance cannot be expressed [@problem_id:2695405].

Consider a hypothetical plant population in Hardy-Weinberg equilibrium where analysis yields $V_A = 36$, $V_D = 24$, $V_I \approx 0$, and $V_E = 40$ units squared [@problem_id:2695405]. The total [phenotypic variance](@entry_id:274482) is $V_P = 36 + 24 + 40 = 100$.
For this population:
$H^2 = \frac{36 + 24}{100} = 0.60$
$h^2 = \frac{36}{100} = 0.36$
Here, $60\%$ of the [phenotypic variation](@entry_id:163153) is due to genetic differences, but only $36\%$ is due to the additive effects of genes. The difference is due to dominance.

Now, imagine we use this population to create a set of fully inbred lines. Within these lines, all individuals are [homozygous](@entry_id:265358). Consequently, dominance effects cannot be expressed, and the [dominance variance](@entry_id:184256) among lines, $V_D$, becomes zero. The total genetic variance among the lines is now entirely additive. In this new population structure, $H^2$ and $h^2$ become equal, illustrating the population-dependent nature of these parameters [@problem_id:2695405].

### The Predictive Power of Narrow-Sense Heritability

While $H^2$ provides a general sense of the importance of genetics for a trait, it is **[narrow-sense heritability](@entry_id:262760) ($h^2$) that is of paramount importance in evolutionary biology and breeding**. This is because $h^2$ quantifies the extent to which phenotypes are predictably passed from parents to offspring, and thus determines the potential for a trait to respond to selection.

The key reason lies in the mechanics of [sexual reproduction](@entry_id:143318). Parents do not pass on their full genotypes to their offspring. Instead, they pass on their alleles, which are reshuffled by segregation and recombination. The additive effects of these alleles, captured by the [breeding value](@entry_id:196154) ($A$), are transmitted predictably. In contrast, dominance and epistatic effects, which depend on specific combinations of alleles, are broken apart during meiosis and are not reliably passed on.

This principle has two direct consequences:

1.  **Parent-Offspring Resemblance**: The degree to which offspring resemble their parents is determined by $h^2$. More formally, the slope of a [linear regression](@entry_id:142318) of offspring phenotypic values on the average phenotypic value of their two parents (the mid-parent value) is equal to the [narrow-sense heritability](@entry_id:262760), assuming no shared environmental effects between generations.
    $$b_{Offspring, Midparent} = \frac{\text{Cov}(P_O, P_{MP})}{\text{Var}(P_{MP})} = \frac{\frac{1}{2}V_A}{\frac{1}{2}V_P} = \frac{V_A}{V_P} = h^2$$
    This relationship provides a classic method for estimating $h^2$ and demonstrates its role as the primary measure of heritable resemblance [@problem_id:2846028].

2.  **Response to Selection**: The predictable, one-generation [response to selection](@entry_id:267049) ($R$) is directly proportional to the [narrow-sense heritability](@entry_id:262760) and the strength of selection ($S$). This relationship is captured by the famous **Breeder's Equation**:
    $R = h^2 S$
    Here, $S$ (the **[selection differential](@entry_id:276336)**) is the difference between the mean phenotype of the selected parents and the mean phenotype of the entire parental generation. The response, $R$, is the change in the mean phenotype of the offspring generation. The equation shows that the evolutionary response is a [direct product](@entry_id:143046) of the opportunity for selection ($S$) and the ability to inherit the selected traits ($h^2$) [@problem_id:2695439]. Dominance and epistasis do not contribute to the predictable response in a large, randomly mating population because the genotypic combinations they rely on are not passed on intact.

It is instructive to contrast this with clonal, or asexual, reproduction. In a clonal population, the parent's entire genotype is passed on to its offspring. Therefore, all genetic variance—additive, dominance, and epistatic—contributes to the resemblance between generations. In this case, the [response to selection](@entry_id:267049) among clonal lines is predicted by the [broad-sense heritability](@entry_id:267885): $R = H^2 S$. This highlights that the unique importance of $h^2$ is intrinsically linked to the genetic shuffling that occurs during [sexual reproduction](@entry_id:143318) [@problem_id:2695439].

### Heritability, Repeatability, and Complex Variance Structures

The basic variance partitioning can be extended to accommodate more complex experimental designs, such as when traits are measured repeatedly on the same individuals over time. This allows for a more nuanced understanding of the sources of variation [@problem_id:2695433]. In such cases, the environmental variance $V_E$ can be split into:

*   **Permanent Environmental Variance ($V_{PE}$)**: Consistent, non-genetic differences among individuals that persist through time (e.g., effects of a stable microhabitat or early life nutrition).
*   **Transient Environmental Variance ($V_{TE}$)**: Temporary, time-specific influences and [measurement error](@entry_id:270998) that cause an individual's phenotype to fluctuate from one measurement to the next.

In this context, we can define a third important measure: **Repeatability ($R_{ep}$)**. Repeatability is the proportion of total [phenotypic variance](@entry_id:274482) attributable to all permanent differences among individuals, both genetic and environmental. It sets the upper limit for [broad-sense heritability](@entry_id:267885).
$$R_{ep} = \frac{V_G + V_{PE}}{V_P} = \frac{V_A + V_D + V_I + V_{PE}}{V_P}$$
The repeatability tells us how consistent an individual's phenotype is over time. If we measure an individual once, repeatability quantifies how much of that measurement is predictive of its future measurements. In contrast, $H^2$ isolates the fraction of permanent differences that are genetic, and $h^2$ isolates the fraction that is both genetic and additive.

### The Interpretation and Misinterpretation of Heritability

Despite their utility, heritability estimates are among the most misunderstood and misused concepts in biology. A correct interpretation requires acknowledging their inherent limitations.

#### Heritability is Not a Constant

A common fallacy is to view [heritability](@entry_id:151095) as an intrinsic, fixed property of a trait. In reality, heritability is a population-level statistic that is specific to the population and the environment in which it was measured.

*   **It is population-specific** because the genetic [variance components](@entry_id:267561) ($V_A, V_D, V_I$) depend on the [allele frequencies](@entry_id:165920) within that population.
*   **It is environment-specific** because the environmental variance ($V_E$) depends on the range and distribution of environments experienced by the population.

Consider a set of plant genotypes for which the [additive genetic variance](@entry_id:154158) ($V_A$) is 20 units. If these plants are grown in a highly controlled growth chamber, the environmental variance might be low, say $V_E = 5$. The [heritability](@entry_id:151095) would be high: $h^2 = \frac{20}{20+5} = 0.8$. If the same genotypes are grown in a heterogeneous field, the environmental variance would be much larger, say $V_E = 45$. Now, the [heritability](@entry_id:151095) is much lower: $h^2 = \frac{20}{20+45} \approx 0.31$ [@problem_id:2695403]. The underlying genetic potential has not changed, but its contribution to the *proportion* of total variation has.

#### High Heritability Does Not Imply Immutability

Perhaps the most dangerous misinterpretation is the belief that a high [heritability](@entry_id:151095) implies a trait is genetically determined and cannot be changed by the environment—that it is immutable. This is fundamentally incorrect [@problem_id:2695426]. Heritability describes the sources of *variation within a population*, not the causes of the *absolute value* of a trait for an individual or the [population mean](@entry_id:175446).

A trait can have a heritability of nearly 1.0, yet be dramatically altered by a uniform environmental change. For example, a high heritability for plant height measured in a nutrient-poor field tells us that the differences between plants *in that field* are mostly due to their genes. However, applying fertilizer to the entire field (a uniform environmental change) could cause all plants to grow much taller, demonstrating that the trait is highly mutable. The [heritability](@entry_id:151095) analysis within a single environmental context provides no information about the potential response to a different environment. This distinction between the [analysis of variance](@entry_id:178748) and the analysis of causes is critical [@problem_id:2695426]. Furthermore, moving a population to a novel environment can reveal previously unseen genotype-by-environment interactions ($V_{GE}$), further demonstrating that a trait's expression is not fixed by its genes.

#### Heritability of Fitness

An important application of these principles is in understanding the evolution of fitness itself. Fisher's Fundamental Theorem of Natural Selection states that the rate of increase in mean fitness is equal to the [additive genetic variance](@entry_id:154158) in fitness, $V_A(w)$. A direct consequence is that persistent [directional selection](@entry_id:136267) on fitness will tend to deplete its own fuel—it will drive beneficial alleles to fixation, eroding $V_A(w)$. Therefore, at evolutionary equilibrium in a constant environment, traits closely correlated with fitness are expected to have very low [narrow-sense heritability](@entry_id:262760) [@problem_id:2695421]. Most of the standing [genetic variance](@entry_id:151205) for fitness is expected to be non-additive ($V_D$ and $V_I$), which is not readily acted upon by selection.

### Assumptions and Complications in Estimating Heritability

The simple relationship between [parent-offspring regression](@entry_id:192145) and $h^2$ holds only under a set of idealized assumptions. Violations of these assumptions, which are common in natural populations, can bias heritability estimates [@problem_id:2695412].

*   **Assortative Mating**: If individuals mate with others that are phenotypically similar (positive [assortative mating](@entry_id:270038)), it increases the genetic similarity between parents and offspring beyond what is expected under [random mating](@entry_id:149892). This inflates the [parent-offspring regression](@entry_id:192145) slope, leading to an **overestimation** of $h^2$.

*   **Genotype-Environment Correlation ($\text{Cov}(G,E)$)**: If "better" genotypes tend to be found in "better" environments, this positive correlation can be transmitted across generations. The environmental advantages of the parents become confounded with their genetic advantages, also leading to an **overestimation** of $h^2$. A [negative correlation](@entry_id:637494) would cause an underestimation.

*   **Genotype-by-Environment Interaction ($V_{GE}$)**: As discussed, G×E variance inflates the total [phenotypic variance](@entry_id:274482) ($V_P$) without contributing to [parent-offspring resemblance](@entry_id:180502) (assuming environments are not shared). This increases the denominator of the heritability ratio, leading to an **underestimation** of the heritability that would be observed in the absence of such interactions.

*   **Inbreeding**: Inbreeding does not bias the estimate of [heritability](@entry_id:151095) *for the inbred population itself*, but it does change the genetic architecture. It increases [homozygosity](@entry_id:174206), converting some [dominance variance](@entry_id:184256) into additive variance, thereby altering the true value of $V_A$ and $h^2$ relative to a non-inbred base population.

A rigorous estimation of [heritability](@entry_id:151095) requires sophisticated statistical methods, such as animal models using full pedigree information or genomic methods, that can simultaneously account for these and other [confounding](@entry_id:260626) factors. Understanding the foundational principles laid out in this chapter is the essential first step toward appreciating both the power and the peril of using heritability to understand the evolution of [complex traits](@entry_id:265688).