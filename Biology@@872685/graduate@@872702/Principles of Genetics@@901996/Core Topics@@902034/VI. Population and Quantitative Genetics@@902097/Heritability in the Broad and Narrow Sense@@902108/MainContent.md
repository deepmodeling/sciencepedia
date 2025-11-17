## Introduction
Heritability is a cornerstone concept in [quantitative genetics](@entry_id:154685), providing a statistical measure of how much of the variation in a trait within a population is due to genetic differences among individuals. While fundamental to understanding evolution, agriculture, and human health, the concept is often oversimplified, leading to significant misconceptions about the nature of genetic influence. The critical distinction between the total genetic contribution ([broad-sense heritability](@entry_id:267885)) and the portion that reliably predicts evolutionary response ([narrow-sense heritability](@entry_id:262760)) is frequently lost, creating a knowledge gap that this article seeks to address.

This exploration will guide you through a comprehensive understanding of heritability. We will begin by dissecting the fundamental theory in "Principles and Mechanisms," where [phenotypic variance](@entry_id:274482) is partitioned into its genetic and environmental components. Next, in "Applications and Interdisciplinary Connections," we will examine how these theoretical principles are put into practice in diverse fields such as animal breeding, human [medical genetics](@entry_id:262833), and evolutionary biology. Finally, the "Hands-On Practices" section will provide an opportunity to solidify your understanding by working through practical estimation problems. By navigating these chapters, you will gain the expertise to not only define [heritability](@entry_id:151095) but also to correctly apply and interpret it in a scientific context.

## Principles and Mechanisms

The [phenotypic variation](@entry_id:163153) observed in any [biological population](@entry_id:200266) is the substrate for evolution and the target of [selective breeding](@entry_id:269785). A central goal of quantitative genetics is to partition this variation into components attributable to genetic and environmental sources. This chapter elucidates the principles and mechanisms underlying this partitioning, defining the concepts of broad-sense and [narrow-sense heritability](@entry_id:262760) and exploring their estimation, interpretation, and profound implications for biology.

### The Fundamental Partition of Phenotypic Variance

The starting point for any quantitative [genetic analysis](@entry_id:167901) is the recognition that an individual's phenotype is a product of its genotype and the environment it experiences. While this relationship can be complex, its statistical consequences for a population can be rigorously defined. Consider a quantitative trait, represented by a random variable $Y$ with a [population mean](@entry_id:175446) $\mu = \mathbb{E}[Y]$. The total [phenotypic variance](@entry_id:274482) is $V_P = \operatorname{Var}(Y) = \mathbb{E}[(Y-\mu)^2]$. Our goal is to decompose this variance into causally interpretable components.

A complete and general framework for this decomposition can be established using a statistical approach based on least-squares principles, without making restrictive assumptions such as the independence of genetic and environmental factors [@problem_id:2821433]. Let the genotype be represented by a random variable $\Gamma$ and the environment by $\Xi$. We can define a **genetic main effect**, $G$, and an **environmental main effect**, $E$, as the pair of functions of $\Gamma$ and $\Xi$, respectively, that together provide the best additive approximation of the centered phenotype, $Y-\mu$. Formally, $(G, E)$ are defined as the solution that minimizes the [mean squared error](@entry_id:276542) of the residual:

$$ \text{minimize } \mathbb{E}[(Y - \mu - g(\Gamma) - e(\Xi))^2] $$

The solution to this problem defines the [main effects](@entry_id:169824) $G$ and $E$, and the residual is defined as the **[gene-environment interaction](@entry_id:138514)**, $I = Y - \mu - G - E$. A fundamental property of this [least-squares](@entry_id:173916) definition is that the interaction term $I$ is statistically orthogonal to both [main effects](@entry_id:169824), meaning $\mathbb{E}[GI]=0$ and $\mathbb{E}[EI]=0$. Substituting this decomposition into the formula for variance yields:

$$ V_P = \operatorname{Var}(G+E+I) = \mathbb{E}[G^2] + \mathbb{E}[E^2] + \mathbb{E}[I^2] + 2\mathbb{E}[GE] $$

This leads to the most general decomposition of [phenotypic variance](@entry_id:274482):

$$ V_P = V_G + V_E + V_{GE} + 2\operatorname{Cov}(G,E) $$

where:
-   $V_G = \operatorname{Var}(G)$ is the variance of the genetic [main effects](@entry_id:169824).
-   $V_E = \operatorname{Var}(E)$ is the variance of the environmental [main effects](@entry_id:169824).
-   $V_{GE} = \operatorname{Var}(I)$ is the **[gene-environment interaction](@entry_id:138514) variance**, which captures the portion of [phenotypic variance](@entry_id:274482) arising from the non-additive effects of genotypes and environments. It reflects the fact that different genotypes may respond differently to environmental changes.
-   $\operatorname{Cov}(G,E)$ is the **gene-environment covariance**, which is non-zero when specific genotypes tend to be found in specific environments. For example, if genetically superior dairy cows are systematically given better feed, $\operatorname{Cov}(G,E)$ would be positive.

In many controlled experiments and idealized [population models](@entry_id:155092), it is assumed that $\operatorname{Cov}(G,E)=0$, simplifying the model to $V_P = V_G + V_E + V_{GE}$.

### Broad-Sense Heritability and the Composition of Genetic Variance

The term $V_G$ represents the total contribution of genetic differences among individuals to the variance in their phenotypes. The proportion of total [phenotypic variance](@entry_id:274482) that is attributable to this total genetic variance is known as **[broad-sense heritability](@entry_id:267885)**, denoted $H^2$.

$$ H^2 = \frac{V_G}{V_P} = \frac{V_G}{V_G + V_E + V_{GE}} $$

$H^2$ provides an overarching measure of the importance of [genetic variation](@entry_id:141964) in explaining phenotypic differences within a population. To understand its meaning, we must further dissect the total genetic variance, $V_G$. The genotypic value of an individual is not a monolithic quantity; it is the result of the effects of its individual alleles and the interactions between them. Consequently, $V_G$ can be partitioned into three fundamental components [@problem_id:2821448]:

$$ V_G = V_A + V_D + V_I $$

-   $V_A$ is the **[additive genetic variance](@entry_id:154158)**. It arises from the average effects of alleles. When an allele is passed from parent to offspring, its average effect on the phenotype is transmitted as well. This is the primary source of resemblance between relatives.
-   $V_D$ is the **[dominance genetic variance](@entry_id:197376)**. It arises from interactions between alleles at the same locus (e.g., the phenotype of a heterozygote is not exactly intermediate between the two homozygotes). These effects are not simply passed on, as a parent transmits only one allele, not its diploid genotype, at a locus.
-   $V_I$ is the **epistatic (or interaction) genetic variance**. It arises from interactions between alleles at different loci. Like dominance, these specific multi-locus combinations are broken up by segregation and recombination during meiosis.

Broad-sense [heritability](@entry_id:151095), then, accounts for all these sources of [genetic variance](@entry_id:151205). Even a genetic architecture devoid of simple additive effects can generate substantial genetic variance and thus contribute to $H^2$. Consider a simple two-locus model where the phenotype is determined purely by an interaction between the additive codes ($x_A, x_B \in \{-1, 0, 1\}$ for genotypes $aa, Aa, AA$) at two unlinked loci: $Y = \mu + t \cdot x_A x_B + E$ [@problem_id:2821475]. In a randomly mating population with [allele frequencies](@entry_id:165920) of $0.5$ at both loci, this model generates no additive ($V_A=0$) or dominance ($V_D=0$) variance. All the [genetic variance](@entry_id:151205) is of the additive-by-additive epistatic type, $V_{AA}$ (a component of $V_I$), and its magnitude is $V_G = V_{AA} = t^2/4$. This purely [epistatic variance](@entry_id:263723) contributes directly to $V_G$ and therefore to the [broad-sense heritability](@entry_id:267885), $H^2$.

### Narrow-Sense Heritability: The Engine of Selection

While $H^2$ quantifies the total genetic contribution to variance, not all [genetic variance](@entry_id:151205) has the same consequence for evolution. The response of a population to selection depends specifically on the variance that is reliably transmitted from parents to offspring. This is the [additive genetic variance](@entry_id:154158), $V_A$. The proportion of [phenotypic variance](@entry_id:274482) due to [additive genetic variance](@entry_id:154158) is called **[narrow-sense heritability](@entry_id:262760)**, denoted $h^2$.

$$ h^2 = \frac{V_A}{V_P} $$

The unique status of $V_A$ stems from its precise statistical definition. Additive [genetic variance](@entry_id:151205) is the portion of the total genetic variance, $V_G$, that can be explained by a [linear regression](@entry_id:142318) of the genotypic value ($G$) on the count of alleles an individual carries [@problem_id:2821452]. The best linear predictor of $G$ from the vector of allele counts $\mathbf{X}$ is known as the individual's **[breeding value](@entry_id:196154)**, or **additive genetic value**, $A$. By definition, the [additive genetic variance](@entry_id:154158), $V_A$, is the variance of these breeding values: $V_A = \operatorname{Var}(A)$.

The remaining genetic variance, $V_D + V_I$, constitutes the residual from this [linear regression](@entry_id:142318). This non-additive variance arises from gene combinations ([dominance and epistasis](@entry_id:193536)) whose effects are context-dependent and are disrupted by the stochastic processes of segregation and recombination during meiosis. Thus, only the additive component, $V_A$, is passed from parent to offspring in a predictable manner, making $h^2$ the key parameter for predicting short-term evolutionary change.

### Heritability and the Prediction of Resemblance and Selection Response

The central role of [narrow-sense heritability](@entry_id:262760) is most clearly demonstrated by its connection to the resemblance between relatives and the response to artificial or natural selection.

The degree to which relatives resemble each other phenotypically is determined by the [genetic covariance](@entry_id:174971) they share, which is primarily a function of their shared [additive genetic variance](@entry_id:154158). A classic method for estimating $h^2$ is to regress the phenotypes of offspring on the phenotypes of their parents. For the regression of an offspring's phenotype on the average phenotype of its two parents (the **midparent**), the slope is exactly equal to the [narrow-sense heritability](@entry_id:262760), assuming an idealized population ([random mating](@entry_id:149892), no shared environment, etc.) [@problem_id:2821439] [@problem_id:2821461].

$$ \beta_{O,MP} = \frac{\operatorname{Cov}(P_{Offspring}, P_{Midparent})}{\operatorname{Var}(P_{Midparent})} = \frac{\frac{1}{2}V_A}{\frac{1}{2}V_P} = \frac{V_A}{V_P} = h^2 $$

This elegant result arises because the covariance between an offspring and its midparent is $\frac{1}{2}V_A$, while the variance of the midparent value is $\frac{1}{2}V_P$. Critically, non-additive [variance components](@entry_id:267561) like $V_D$ and $V_I$ do not contribute to this covariance because the specific allelic combinations that generate dominance and epistatic effects in the parents are broken apart during meiosis and are not inherited as a unit. For this reason, the resemblance between parent and offspring reflects only the additive, transmissible portion of genetic variance. Similarly, the slope of the regression on a single parent is $\beta_{O,P} = h^2/2$ [@problem_id:2821439].

This direct link between [parent-offspring resemblance](@entry_id:180502) and $h^2$ explains why [narrow-sense heritability](@entry_id:262760) is fundamental to predicting evolutionary change. The [response to selection](@entry_id:267049) ($R$), defined as the change in the [population mean](@entry_id:175446) from one generation to the next, is given by the **Breeder's Equation**:

$$ R = h^2 S $$

where $S$ is the [selection differential](@entry_id:276336), or the difference between the mean of the selected parents and the mean of the overall parental generation. This equation shows that the [response to selection](@entry_id:267049) is directly proportional to the [narrow-sense heritability](@entry_id:262760). If $h^2$ is high, a large fraction of the selected parents' phenotypic superiority is passed to their offspring. If $h^2$ is low, most of the parents' superiority was due to non-additive genetic or environmental effects, and the [response to selection](@entry_id:267049) will be weak.

### Nuances in the Estimation and Interpretation of Heritability

The concepts of heritability are powerful but require careful interpretation. Heritability is not a fixed biological constant but a parameter specific to a particular population in a particular environment. Its estimation is also subject to several [confounding](@entry_id:260626) factors.

#### Heritability is Environment-Dependent

A common misconception is that heritability is an immutable property of a trait. In reality, because [heritability](@entry_id:151095) is a proportion of variances, any change in an environmental variance component will alter it. Consider a scenario where genetically identical clones of a plant are grown in a variable field environment and a uniform laboratory environment [@problem_id:2821458]. Suppose the genetic variance ($V_G$) is the same in both settings, but the environmental variance ($V_E$) is much larger in the field (e.g., $V_E=9.0$) than in the lab ($V_E=1.0$). Even with identical genetic variance ($V_G=3.0$), the [broad-sense heritability](@entry_id:267885) will be dramatically different: $H^2_{field} = 3/(3+9) = 0.25$, while $H^2_{lab} = 3/(3+1) = 0.75$. The reduction of environmental "noise" in the lab makes the existing genetic differences account for a larger proportion of the total [phenotypic variance](@entry_id:274482).

The role of **[genotype-by-environment interaction](@entry_id:155645) variance ($V_{GE}$)** adds another layer of complexity [@problem_id:2821453]. In the standard heritability formula, $V_{GE}$ appears in the denominator ($V_P$) but not the numerator ($V_G$). This treats interaction effects as a source of noise that reduces [heritability](@entry_id:151095). However, for some questions, particularly in plant and animal breeding, the "genetic value" of an individual might be defined relative to a specific environment. In this context, the genetic variance could be conceptualized as $V_G + V_{GE}$, thereby including the interaction term in the numerator of $H^2$. The choice depends on whether one is interested in performance averaged across all environments or in environment-specific performance.

#### Heritability and Immutability

Perhaps the most persistent misconception is that high [heritability](@entry_id:151095) implies a trait is genetically determined and therefore immutable to environmental intervention. This is fundamentally incorrect. Heritability describes the causes of *variation* within a population, not the causes of the population's *average* value.

A powerful illustration involves a highly heritable trait like maize ear mass [@problem_id:2821457]. Imagine a population where the [narrow-sense heritability](@entry_id:262760) for this trait is high, say $h^2 = 0.75$. If a uniform policy of nitrogen supplementation is introduced, this environmental improvement could raise the yield for all genotypes, causing a substantial increase in the [population mean](@entry_id:175446) (e.g., from $50\,\mathrm{g}$ to $65\,\mathrm{g}$). This can occur even while the [variance components](@entry_id:267561) and the high [heritability](@entry_id:151095) within the population remain unchanged. High heritability simply means that the *rank* of individuals within that population is largely determined by their genes; it does not prevent the entire population's phenotype from shifting in response to a global environmental change.

#### Confounding Factors and Estimation Challenges

Estimating heritability from the resemblance of relatives is fraught with potential pitfalls. The simple equation $\beta_{O,P} = h^2/2$ rests on a set of ideal assumptions. If these are violated, estimates can be biased. For example, if parents and offspring share a common rearing environment, this can create an environmental covariance ($\operatorname{Cov}(E_{parent}, E_{offspring}) > 0$). This covariance will inflate the phenotypic covariance, leading to an overestimation of $h^2$ [@problem_id:2821439]. Likewise, positive [assortative mating](@entry_id:270038) inflates [genetic variance](@entry_id:151205) and the covariance between relatives, also biasing heritability estimates.

Advanced experimental designs are required to disentangle different genetic components. The classical twin study, for instance, compares the resemblance of monozygotic (MZ, genetically identical) and dizygotic (DZ, sharing 50% of genes on average) twins. In an idealized Additive-Dominance-Environment (ADE) model, the expected correlations are $r_{MZ} = h^2 + h_D^2$ and $r_{DZ} = 0.5h^2 + 0.25h_D^2$, where $h_D^2 = V_D/V_P$. This system of equations can be solved to estimate both additive and [dominance variance](@entry_id:184256) [@problem_id:2821468]. However, this estimation is sensitive to the strong assumption that there are no shared environmental effects that make twins more similar. If such effects exist but are unmodeled, they can severely bias the estimates of genetic [variance components](@entry_id:267561).

Finally, it is crucial to recognize that [heritability](@entry_id:151095) itself can evolve. The partitioning of variance is not static. As selection acts on a population, it changes [allele frequencies](@entry_id:165920) and can create [linkage disequilibrium](@entry_id:146203) between causal loci. This process can alter the average effects of alleles, effectively "converting" some of the [epistatic variance](@entry_id:263723) ($V_I$) into additive variance ($V_A$) from one generation to the next [@problem_id:2821475]. Therefore, the very parameter that determines the [response to selection](@entry_id:267049), $h^2$, is itself a dynamic feature of a population's evolutionary trajectory.