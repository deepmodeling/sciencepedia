## Introduction
The vast diversity of life is underpinned by variation in observable traits, or phenotypes. Understanding how this variation arises and is passed across generations is a central goal of evolutionary biology. The field of quantitative genetics provides a powerful statistical framework to dissect the complex interplay between an organism's genetic makeup (genotype) and its environment. Attributing phenotypic differences to specific sources is challenging because genes do not act in isolation; their effects can be non-additive and can change across different environments. This article addresses the fundamental problem of how to partition this total [phenotypic variance](@entry_id:274482) into its distinct causal components.

You will learn the core principles of this decomposition, from the foundational partitioning of genetic and environmental effects to the more nuanced breakdown of [genetic variance](@entry_id:151205) itself. The first chapter, **Principles and Mechanisms**, establishes the theoretical model, defining key concepts like additive variance, dominance deviation, and epistasis. The second chapter, **Applications and Interdisciplinary Connections**, explores how these theoretical components are estimated and applied in diverse fields such as [selective breeding](@entry_id:269785), conservation genetics, and [evolutionary ecology](@entry_id:204543). Finally, **Hands-On Practices** will guide you through the derivation of key [variance components](@entry_id:267561), solidifying your understanding of this essential framework.

## Principles and Mechanisms

The observable characteristics of an organism, its **phenotype**, are the product of a complex interplay between its genetic makeup and the environment it experiences. Quantitative genetics provides a statistical framework for dissecting this complexity by partitioning the [total variation](@entry_id:140383) in a trait observed within a population into components attributable to different sources. This chapter lays out the foundational principles and mechanisms of this partitioning, beginning with the broadest division between genetic and environmental effects and proceeding to the finer-scale components of [genetic variance](@entry_id:151205).

### The Foundational Partition of Phenotypic Variance

The starting point for any quantitative [genetic analysis](@entry_id:167901) is the decomposition of an individual's phenotypic value, $P$, into its constituent parts. In the simplest model, we express the phenotype as the sum of the **genotypic value**, $G$, and the **environmental deviation**, $E$:

$$
P = G + E
$$

The genotypic value, $G$, represents the average phenotype of a given genotype if it could be raised across the entire spectrum of possible environments. The environmental deviation, $E$, is the difference between the phenotype of an individual in its specific environment and the average phenotype for its genotype. By convention, these effects are defined such that their average over the population is zero, i.e., $\mathbb{E}[E] = 0$. If the genotypic values are also centered, then $\mathbb{E}[G] = 0$ and $\mathbb{E}[P] = 0$.

Our primary interest lies not in individual values but in the sources of variation within a population. The total [phenotypic variance](@entry_id:274482), $V_P$, can be expressed in terms of the variances of its components. Using the fundamental statistical identity for the variance of a sum of two variables, we derive the general expression for [phenotypic variance](@entry_id:274482):

$$
V_P = \mathrm{Var}(P) = \mathrm{Var}(G + E) = \mathrm{Var}(G) + \mathrm{Var}(E) + 2\mathrm{Cov}(G, E)
$$

This equation states that the total [phenotypic variance](@entry_id:274482) ($V_P$) is the sum of the [genetic variance](@entry_id:151205) ($V_G$), the environmental variance ($V_E$), and twice the covariance between genotypic values and environmental deviations ($\mathrm{Cov}(G,E)$) [@problem_id:2697779].

The covariance term, $\mathrm{Cov}(G, E)$, is of critical biological importance. It represents the **genotype-environment correlation**, which is the statistical tendency for certain genotypes to be found in particular environments. A positive covariance implies that genotypes associated with higher trait values tend to occur in environments that also promote higher trait values, while a negative covariance implies the opposite. Such correlations arise from various biological phenomena, including:
- **Habitat Choice**: Individuals of a particular genotype may actively select or thrive in specific microhabitats.
- **Parental Effects**: Parents with certain genotypes may provide their offspring with systematically better or worse rearing environments.
- **Artificial Manipulation**: In agricultural or laboratory settings, humans may deliberately place high-performing genotypes in enriched environments.

For many theoretical and practical purposes, it is desirable to simplify the [variance decomposition](@entry_id:272134). This requires the covariance term to be zero. The condition $\mathrm{Cov}(G, E) = 0$ holds when genotypes are distributed randomly and independently with respect to environmental conditions. This can be achieved experimentally through controlled randomization, such as in a **[common garden experiment](@entry_id:171582)** where individuals from different genetic backgrounds are randomly assigned to plots, or through **cross-fostering** where offspring are randomly assigned to different parents for rearing. In nature, this condition is met only if the biological mechanisms causing correlation are absent [@problem_id:2697779].

It is essential to distinguish genotype-environment correlation, $\mathrm{Cov}(G,E)$, from **[genotype-by-environment interaction](@entry_id:155645)**, often denoted as $G \times E$. Correlation refers to a [statistical association](@entry_id:172897) between the causal factors themselves ($G$ and $E$). Interaction refers to the non-additive effect of these factors on the outcome ($P$), where the phenotypic effect of an environment depends on an individual's genotype. We will return to this crucial distinction in a later section.

### Decomposing Genetic Variance: Additive and Dominance Effects

The total [genetic variance](@entry_id:151205), $V_G$, is itself a composite quantity. For a [diploid](@entry_id:268054) organism, the genotypic value is determined by the two alleles present at each locus and the interactions between them. The genius of R.A. Fisher was to recognize that from an evolutionary perspective, the most important part of the genotypic value is the part that is reliably transmitted from parents to offspring. This led to the partitioning of the genotypic value, and consequently the genetic variance, into additive and non-additive components.

#### Breeding Values and Additive Variance

Let's consider a single locus with two alleles, $A$ and $a$. An individual's genotypic value, $G$, can be statistically partitioned into two components: the **[breeding value](@entry_id:196154)** (or **additive genetic value**), $A$, and the **dominance deviation**, $D$.

$$
G = \mu + A + D
$$

where $\mu$ is the [population mean](@entry_id:175446) phenotype. The [breeding value](@entry_id:196154) $A$ represents the heritable portion of the genotypic value. It is defined as the best linear predictor of the genotypic value based on the number of a particular allele an individual carries. This prediction is made using a least-squares linear regression of genotypic value ($G$) on allele count ($X$, e.g., the number of $A$ alleles, which can be 0, 1, or 2). The dominance deviation $D$ is simply the residual error of this regression—the part of the genotypic value that cannot be explained by the simple additive effects of its alleles.

The slope of this regression is a quantity of fundamental importance, known as the **average effect of allele substitution**, denoted by $\alpha$. It represents the expected change in phenotype for a random individual if one of its alleles at a locus were replaced by another allele from the population's [gene pool](@entry_id:267957). For a diallelic locus with alleles $A$ and $a$ at frequencies $p$ and $q$ respectively, and with genotypic values $G_{AA}$, $G_{Aa}$, and $G_{aa}$, the average effect of substituting an $a$ allele with an $A$ allele is given by [@problem_id:2697775]:

$$
\alpha = p(G_{AA} - G_{Aa}) + q(G_{Aa} - G_{aa})
$$

This expression can be rewritten to reveal its dependence on [allele frequencies](@entry_id:165920) and dominance. If we define an additive parameter $a = \frac{G_{AA} - G_{aa}}{2}$ (half the difference between homozygotes) and a dominance parameter $d = G_{Aa} - \frac{G_{AA} + G_{aa}}{2}$ (the heterozygote's deviation from the midpoint of the homozygotes), then the average effect becomes:

$$
\alpha = a + d(q-p)
$$

This powerful result shows that the average effect of an allele, $\alpha$, is not a fixed property of that allele. It is a population-specific parameter that depends on the [allele frequencies](@entry_id:165920) ($p$ and $q$) whenever dominance is present ($d \neq 0$). Only in the case of pure additivity ($d=0$) is the average effect independent of allele frequency [@problem_id:2697775].

With $\alpha$ defined, the [breeding value](@entry_id:196154) for an individual with allele count $X$ is given by $A = \alpha(X - \mathbb{E}[X])$, where $\mathbb{E}[X]=2p$ is the mean allele count in the population. The variance of these breeding values across the population is the **[additive genetic variance](@entry_id:154158)**, $V_A$:

$$
V_A = \mathrm{Var}(A) = \alpha^2 \mathrm{Var}(X)
$$

Under Hardy-Weinberg Equilibrium (HWE), the variance of the allele count is $\mathrm{Var}(X) = 2pq$. Thus, the additive variance is:

$$
V_A = 2pq\alpha^2 = 2pq[a + d(q-p)]^2
$$

**Example Calculation**
Consider a population at HWE with allele frequencies $p=0.25$ for allele $A$ and $q=0.75$ for allele $a$. The genotypic values are $G_{AA}=12$, $G_{Aa}=7$, and $G_{aa}=5$. First, we calculate the average effect of substitution: $\alpha = 0.25(12-7) + 0.75(7-5) = 1.25 + 1.50 = 2.75$. The mean allele count is $\mathbb{E}[X] = 2p = 0.5$. The breeding values for the three genotypes are:
- $A(AA) = 2.75(2 - 0.5) = 4.125$
- $A(Aa) = 2.75(1 - 0.5) = 1.375$
- $A(aa) = 2.75(0 - 0.5) = -1.375$

The [additive genetic variance](@entry_id:154158) is $V_A = 2pq\alpha^2 = 2(0.25)(0.75)(2.75)^2 \approx 2.836$ [@problem_id:2697755].

#### Dominance Deviations and Dominance Variance

The dominance deviation, $\delta_g$ (or $D_g$), is the difference between a genotype's actual value and its [breeding value](@entry_id:196154): $\delta_g = G_g - (\mu + A_g)$. By construction in the least-squares framework, the [population mean](@entry_id:175446) of the dominance deviations is zero, i.e., $\mathbb{E}[D] = 0$. This holds true regardless of the mating system or whether the population is in HWE [@problem_id:2697734] [@problem_id:2697766].

The variance of these deviations is the **[dominance variance](@entry_id:184256)**, $V_D$. Since the mean deviation is zero, the variance is simply the mean of the squared deviations:

$$
V_D = \mathrm{Var}(D) = \mathbb{E}[D^2] = \sum_g f_g \delta_g^2
$$

where $f_g$ is the frequency of genotype $g$. For a population in HWE, this simplifies to the well-known formula:

$$
V_D = (2pqd)^2
$$

#### Variance Components are Properties of Populations

It is crucial to understand that $V_A$ and $V_D$ are not intrinsic properties of a gene. They are statistical parameters of a population, dependent on both the genotypic values ($a$ and $d$) and the allele frequencies ($p$ and $q$).

A striking illustration of this principle involves a specific case of [overdominance](@entry_id:268017), where, for instance, genotypic values are $G_{AA}=0, G_{Aa}=1, G_{aa}=0$. The heterozygote has a unique phenotype. Let's examine two populations with the same gene but different [allele frequencies](@entry_id:165920) [@problem_id:2697705]:
1.  **Population 1:** $p=0.5$. Here, the average effect of substitution $\alpha = q-p = 0$. Consequently, the additive variance $V_A = 2(0.5)(0.5)(0)^2 = 0$. All [genetic variance](@entry_id:151205) is due to dominance: $V_G = V_D = (2(0.5)(0.5))^2 = 0.25$. In this specific context, there is no [additive genetic variance](@entry_id:154158) for selection to act upon, even though there is genetic variation.
2.  **Population 2:** $p=0.9$. Here, $\alpha = q-p = 0.1-0.9 = -0.8$. The additive variance is now substantial: $V_A = 2(0.9)(0.1)(-0.8)^2 = 0.1152$. The [dominance variance](@entry_id:184256) is $V_D = (2(0.9)(0.1))^2 = 0.0324$.

In these two populations, the gene's physiological action is identical, yet the partitioning of its variance into additive and dominance components is drastically different. This underscores that [variance components](@entry_id:267561) are statistical properties of a trait within a specific population at a specific time.

### The Importance of Additive Variance: Resemblance Between Relatives

The partitioning of [genetic variance](@entry_id:151205) into additive and non-additive components is not merely a statistical exercise; it has profound evolutionary implications. The [additive genetic variance](@entry_id:154158), $V_A$, is the primary determinant of the degree of resemblance between relatives and, consequently, the primary cause of a population's [response to selection](@entry_id:267049).

To understand why, consider the covariance between a parent ($P$) and an offspring ($O$) for a quantitative trait, assuming [random mating](@entry_id:149892) and no environmental covariance. The genotypic value of the parent is $G_P = A_P + D_P + I_P$ (where $I_P$ is the epistatic deviation, discussed later). The genotypic value of the offspring is $G_O = A_O + D_O + I_O$. The covariance $\mathrm{Cov}(G_P, G_O)$ measures the extent to which the parent's and offspring's phenotypes tend to vary together.

The key lies in how genes are transmitted. An offspring receives exactly half of its alleles from a given parent, and this sample is random due to Mendelian segregation. The other half comes from a second parent chosen at random from the population.
- The **additive value** ($A$) is a linear function of alleles. Because the offspring receives half of the parent's alleles, its expected [breeding value](@entry_id:196154) is half that of the parent's [breeding value](@entry_id:196154). This leads directly to the covariance contribution: $\mathrm{Cov}(A_P, A_O) = \frac{1}{2}V_A$.
- The **dominance deviation** ($D$) arises from the specific combination of two alleles at a locus. A parent passes on only one of those alleles. The second allele in the offspring comes from the gene pool at random. Thus, the specific diploid combination that created the parent's dominance deviation is broken up. On average, there is no correlation between a parent's dominance deviation and that of its offspring. Therefore, $\mathrm{Cov}(D_P, D_O) = 0$.

Combining these facts (and temporarily ignoring epistasis), we find that the parent-offspring covariance for the genotypic value is:

$$
\mathrm{Cov}(G_P, G_O) = \frac{1}{2}V_A
$$

This result is fundamental. It demonstrates that the resemblance between parents and offspring is determined solely by the additive component of genetic variance. Dominance creates variation within a generation but does not contribute, on average, to the similarity across generations under [random mating](@entry_id:149892) [@problem_id:2697753]. This is why $V_A$ is often called the "heritable variance" and is the central parameter in predicting evolutionary change.

### Expanding the Model: Epistasis and Interaction Variance

The single-locus model is a simplification. Genotypic values are often influenced by **[epistasis](@entry_id:136574)**, the non-additive interaction between alleles at different loci. When we extend our model to include two or more loci, the [genetic variance](@entry_id:151205) must be partitioned further. The total genetic variance is now the sum of additive, dominance, and **[epistatic variance](@entry_id:263723)** ($V_I$):

$$
V_G = V_A + V_D + V_I
$$

The [epistatic variance](@entry_id:263723) itself can be decomposed into components representing different types of interactions. Using an orthogonal statistical framework analogous to Analysis of Variance (ANOVA), we can define these components based on products of single-locus contrasts [@problem_id:2697710]. For a two-locus system, this yields:
- **Additive-by-Additive variance ($V_{AA}$)**: Variance arising from interactions between the additive effects of two loci.
- **Additive-by-Dominance variance ($V_{AD}$)**: Variance from interactions between the additive effect of one locus and the dominance effect of another.
- **Dominance-by-Additive variance ($V_{DA}$)**: The reciprocal of the above.
- **Dominance-by-Dominance variance ($V_{DD}$)**: Variance from interactions between the dominance effects of two loci.

Under linkage equilibrium, these components are orthogonal, and the total [epistatic variance](@entry_id:263723) is their sum: $V_I = V_{AA} + V_{AD} + V_{DA} + V_{DD}$.

The presence of epistasis makes the genetic architecture of a trait more complex. For instance, the additive variance at one locus can become dependent on the [allele frequencies](@entry_id:165920) at an interacting locus. Furthermore, epistatic [variance components](@entry_id:267561), like all [variance components](@entry_id:267561), require polymorphism at the interacting loci; if one locus becomes fixed for an allele, any interaction variance involving that locus disappears [@problem_id:2697782].

Let's consider a specific two-locus system where genotypic values are such that all heterozygous genotypes have a value of 0, while homozygotes have values of +2 or -2 depending on the combination (e.g., $G_{AABB}=+2, G_{AAbb}=-2, G_{aaBB}=-2, G_{aabb}=+2$). In this model of pure [sign epistasis](@entry_id:188310), a detailed analysis reveals that all dominance and mixed-interaction variances ($V_D, V_{AD}, V_{DA}, V_{DD}$) are zero. The only non-additive variance is the additive-by-additive component, $V_{AA}$. The total [genetic variance](@entry_id:151205) is simply $V_G = V_A + V_{AA}$. The additive variance, $V_A$, now comprises contributions from both loci, each of which depends on the [allele frequency](@entry_id:146872) at the *other* locus, a clear signature of epistasis. For example, the additive variance from locus A is $V_{A(A)} = 8p_A q_A (2p_B-1)^2$. This term vanishes if locus B is at a frequency of $p_B=0.5$, demonstrating how the [heritable variation](@entry_id:147069) at one gene can be masked or revealed by the genetic background at another [@problem_id:2697782].

Epistasis also modifies the pattern of resemblance between relatives. While [dominance variance](@entry_id:184256) does not contribute to parent-offspring covariance, some epistatic components do. The covariance becomes a series:

$$
\mathrm{Cov}(G_P, G_O) = \frac{1}{2}V_A + \frac{1}{4}V_{AA} + \frac{1}{8}V_{AAA} + \dots
$$

where $V_{AAA}$ represents additive-by-additive-by-additive variance, and so on. Interactions involving dominance still do not contribute. This shows that while $V_A$ remains the largest and most important contributor to heritability, strong additive-by-additive epistasis can also play a role.

### The Complete Picture: Incorporating Genotype-by-Environment Interaction

We can now synthesize these concepts into a complete model for [phenotypic variance](@entry_id:274482). The phenotype ($P$) is a function not only of genetic [main effects](@entry_id:169824) ($G$) and environmental [main effects](@entry_id:169824) ($E$), but also their interaction ($G \times E$). A **[genotype-by-environment interaction](@entry_id:155645)** exists when the differences among genotypes change across environments. This is often visualized as non-parallel reaction norms, where the lines plotting phenotype against environment for different genotypes are not parallel and may even cross [@problem_id:2697722].

A full linear model for the phenotype includes a main effect for genotype, a main effect for environment, an interaction term, and a residual error ($R$) for micro-environmental or [developmental noise](@entry_id:169534):

$$
P = \mu + G + E + (G \times E) + R
$$

The total [phenotypic variance](@entry_id:274482) is the variance of this sum. In the most general case, this includes multiple covariance terms:

$$
V_P = V_G + V_E + V_{G \times E} + V_R + 2\mathrm{Cov}(G,E) + 2\mathrm{Cov}(G, G \times E) + 2\mathrm{Cov}(E, G \times E)
$$

This formidable expression simplifies under the carefully controlled conditions of a well-designed experiment. If genotypes are randomly assigned to environments, the genotype-environment correlation vanishes ($\mathrm{Cov}(G,E)=0$). If the experiment is balanced (equal replication of each genotype in each environment), then the [main effects](@entry_id:169824) and interactions are statistically orthogonal, causing the remaining covariance terms to also become zero. Under these ideal conditions, the [variance decomposition](@entry_id:272134) becomes purely additive:

$$
V_P = V_G + V_E + V_{G \times E} + V_R
$$

This equation represents the complete partitioning of [phenotypic variance](@entry_id:274482). It separates the variation due to average genetic differences ($V_G$), average environmental differences ($V_E$), the unique effects arising from specific gene-environment combinations ($V_{G \times E}$), and unexplained residual noise ($V_R$). Each of these components, in turn, can be further dissected, with $V_G$ being the sum of its additive, dominance, and epistatic parts. This comprehensive framework allows quantitative geneticists to estimate the relative importance of different sources of variation, understand the [genetic architecture](@entry_id:151576) of [complex traits](@entry_id:265688), and predict their evolution.