## Introduction
The non-random association of alleles at different loci, known as [linkage disequilibrium](@entry_id:146203) (LD), is a fundamental concept in [population genetics](@entry_id:146344). It serves as a powerful source of information, encoding the evolutionary history and genomic architecture of a population. However, quantifying the strength and nature of this association is not straightforward. Several different statistical measures exist, most notably the disequilibrium coefficient $D$, the normalized measure $D'$, and the squared correlation $r^2$. Understanding the distinct properties, advantages, and limitations of each is critical for their correct application, a challenge that can lead to confusion and misinterpretation of genetic data.

This article provides a comprehensive guide to the core measures of linkage disequilibrium. Across three chapters, we will build a robust understanding of this essential topic. The first chapter, **Principles and Mechanisms**, will delve into the mathematical definitions of $D$, $D'$, and $r^2$, explore their statistical interpretations, and examine the [evolutionary forces](@entry_id:273961) like recombination and population structure that shape LD patterns. Next, in **Applications and Interdisciplinary Connections**, we will see these measures in action, exploring their central role in [gene mapping](@entry_id:140611), [genome-wide association studies](@entry_id:172285) (GWAS), and in making inferences about natural selection and demographic history. Finally, the **Hands-On Practices** section provides exercises to solidify these theoretical concepts. By navigating these chapters, you will gain the expertise to choose the appropriate LD measure for your research question and interpret the results with confidence.

## Principles and Mechanisms

The study of [linkage disequilibrium](@entry_id:146203) (LD) rests upon a foundation of precise quantitative measures. These measures are not merely descriptive statistics; they are deeply connected to the statistical properties of genetic data and the [evolutionary mechanisms](@entry_id:196221) that shape them. This chapter elucidates the principles underlying the most common measures of LD, explores their interrelationships, and examines the dynamic processes of recombination and population structure that influence them.

### The Coefficient of Linkage Disequilibrium, $D$

The simplest and most fundamental measure of association between two loci is the **[linkage disequilibrium](@entry_id:146203) coefficient**, denoted by $D$. To define it, we consider two biallelic loci with alleles $A/a$ and $B/b$. In a population, there are four possible [haplotypes](@entry_id:177949): $AB$, $Ab$, $aB$, and $ab$. We denote their respective frequencies as $P_{AB}$, $P_{Ab}$, $P_{aB}$, and $P_{ab}$. These frequencies must sum to unity.

The frequencies of the individual alleles, known as **marginal allele frequencies**, can be calculated by summing the frequencies of the haplotypes in which they appear. For instance, the frequency of allele $A$, denoted $p_A$, and allele $B$, denoted $p_B$, are:

$p_A = P_{AB} + P_{Ab}$

$p_B = P_{AB} + P_{aB}$

The complementary [allele frequencies](@entry_id:165920) are $q_A = 1 - p_A$ and $q_B = 1 - p_B$.

The state of **linkage equilibrium** (LE) is defined as the [statistical independence](@entry_id:150300) of alleles at the two loci. If the loci are in LE, the frequency of any given [haplotype](@entry_id:268358) is simply the product of its constituent allele frequencies. For the $AB$ haplotype, this would mean $P_{AB} = p_A p_B$.

Linkage disequilibrium, then, represents any deviation from this state of independence. The coefficient $D$ quantifies this deviation for the $AB$ [haplotype](@entry_id:268358):

$D = P_{AB} - p_A p_B$

A positive value of $D$ indicates an excess of $AB$ [haplotypes](@entry_id:177949) compared to the expectation at equilibrium, while a negative value indicates a deficit. Because the frequencies of all four [haplotypes](@entry_id:177949) are interrelated, this single coefficient is sufficient to describe the entire system. One can show that the deviation is equal in magnitude but opposite in sign for the "repulsion" [haplotypes](@entry_id:177949) ($Ab$ and $aB$) and equal in magnitude and sign for the complementary "coupling" [haplotype](@entry_id:268358) ($ab$). Specifically, all four [haplotype](@entry_id:268358) frequencies can be expressed in terms of the [allele frequencies](@entry_id:165920) and $D$:

$P_{AB} = p_A p_B + D$

$P_{Ab} = p_A q_B - D$

$P_{aB} = q_A p_B - D$

$P_{ab} = q_A q_B + D$

An equivalent and often useful definition of $D$ is based on the frequencies of the coupling ($AB, ab$) versus repulsion ($Ab, aB$) haplotypes:

$D = P_{AB}P_{ab} - P_{Ab}P_{aB}$

This expression highlights that $D$ is a measure of the excess of coupling gametes over repulsion gametes. For example, given observed haplotype counts of $C_{AB} = 46$, $C_{Ab} = 14$, $C_{aB} = 14$, and $C_{ab} = 26$ in a sample of 100 chromosomes, we first find the frequencies: $P_{AB}=0.46, P_{Ab}=0.14, P_{aB}=0.14, P_{ab}=0.26$. The allele frequencies are $p_A = 0.46+0.14 = 0.60$ and $p_B = 0.46+0.14=0.60$. Using the primary definition, $D = 0.46 - (0.60)(0.60) = 0.10$. Using the second definition, $D = (0.46)(0.26) - (0.14)(0.14) = 0.1196 - 0.0196 = 0.10$, yielding the identical result [@problem_id:2732241].

It is crucial to recognize that the sign of $D$ is arbitrary and depends on how alleles are labeled. If we were to relabel the alleles at the first locus ($A \leftrightarrow a$), the new disequilibrium coefficient $D'$ would be equal to $-D$. If we relabeled alleles at both loci, the sign would be preserved ($D''=D$). This demonstrates that the magnitude of $D$, not its sign, reflects the extent of non-random association [@problem_id:2732243].

Statistically, $D$ can be interpreted as the covariance between the allelic states at the two loci. If we define [indicator random variables](@entry_id:260717) $X$ and $Y$ for a randomly sampled gamete, where $X=1$ for allele $A$ and $0$ for allele $a$, and $Y=1$ for allele $B$ and $0$ for allele $b$, then the expected values are $E[X] = p_A$ and $E[Y] = p_B$. The expectation of their product, $E[XY]$, is the probability that both $X=1$ and $Y=1$, which is simply $P_{AB}$. The covariance is then:

$\operatorname{Cov}(X,Y) = E[XY] - E[X]E[Y] = P_{AB} - p_A p_B = D$

This provides a rigorous statistical foundation for our primary measure of [linkage disequilibrium](@entry_id:146203) [@problem_id:2732260].

### The Constraints on $D$ and the Normalized Measure $D'$

A significant limitation of $D$ is that its maximum and minimum possible values depend on the allele frequencies at the loci being compared. This makes it difficult to compare the "strength" of LD across different pairs of loci or different populations. The constraints on $D$ arise from the fundamental requirement that no [haplotype](@entry_id:268358) frequency can be negative. From the equations relating [haplotype](@entry_id:268358) frequencies to $D$, we can derive a set of inequalities:

1.  $P_{AB} = p_A p_B + D \ge 0 \implies D \ge -p_A p_B$
2.  $P_{Ab} = p_A q_B - D \ge 0 \implies D \le p_A q_B$
3.  $P_{aB} = q_A p_B - D \ge 0 \implies D \le q_A p_B$
4.  $P_{ab} = q_A q_B + D \ge 0 \implies D \ge -q_A q_B$

Combining these, the feasible range for $D$ is $[D_{min}, D_{max}]$, where:

$D_{max} = \min(p_A q_B, q_A p_B)$

$D_{min} = \max(-p_A p_B, -q_A q_B) = -\min(p_A p_B, q_A q_B)$

Consider a scenario where [allele frequencies](@entry_id:165920) are highly skewed, for example $p_A=0.1$ and $p_B=0.9$. Then $q_A=0.9$ and $q_B=0.1$. The bounds on $D$ are:

$D_{max} = \min((0.1)(0.1), (0.9)(0.9)) = \min(0.01, 0.81) = 0.01$

$D_{min} = -\min((0.1)(0.9), (0.9)(0.1)) = -\min(0.09, 0.09) = -0.09$

The permissible range for $D$ is $[-0.09, 0.01]$. This range is highly asymmetric. The small maximum value ($D_{max}=0.01$) is because creating an excess of $AB$ [haplotypes](@entry_id:177949) (positive $D$) requires reducing the number of repulsion [haplotypes](@entry_id:177949), particularly $Ab$. Since the expected frequency of this [haplotype](@entry_id:268358) under equilibrium, $p_A q_B$, is already very small ($0.01$), there is little "room" for $D$ to increase before this frequency would become negative [@problem_id:2825921].

To account for this frequency dependence, Richard Lewontin proposed a standardized measure, **$D'$ (D-prime)**. $D'$ normalizes the observed value of $D$ by the maximum possible deviation in the same direction, given the allele frequencies:

$D' = \begin{cases} \frac{D}{D_{max}}  \text{if } D > 0 \\ \frac{D}{|D_{min}|}  \text{if } D  0 \end{cases}$

By this definition, $D'$ ranges from $-1$ to $1$. A value of $D'=1$ or $D'=-1$ signifies "complete" LD, meaning that at least one of the four possible [haplotypes](@entry_id:177949) is absent from the population, indicating that no recombination (or mutation) has occurred to generate it. For example, consider a population with $p_A=0.2$ and $p_B=0.8$. The theoretical maximum for positive $D$ is $D_{max} = \min((0.2)(0.2), (0.8)(0.8)) = 0.04$. If a sample from this population yielded an observed $D$ equal to this maximum of $0.04$, it would imply complete association. In this case, $D'$ would be calculated as $D/D_{max} = 0.04/0.04 = 1$ [@problem_id:2825935].

### Disequilibrium as Correlation: The $r^2$ Measure

While $D'$ is useful for assessing the completeness of LD, another measure, $r^2$, is often more informative, particularly in the context of [gene mapping](@entry_id:140611) and association studies. The measure $r^2$ is the squared **Pearson [correlation coefficient](@entry_id:147037)** between the [indicator variables](@entry_id:266428) $X$ and $Y$ defined previously.

Recalling that $\operatorname{Cov}(X,Y) = D$, and the variances are $\operatorname{Var}(X) = E[X^2] - (E[X])^2 = p_A - p_A^2 = p_A q_A$ and $\operatorname{Var}(Y) = p_B q_B$, the [correlation coefficient](@entry_id:147037) $r$ is:

$r = \operatorname{Corr}(X,Y) = \frac{\operatorname{Cov}(X,Y)}{\sqrt{\operatorname{Var}(X)\operatorname{Var}(Y)}} = \frac{D}{\sqrt{p_A q_A p_B q_B}}$

The squared correlation, $r^2$, is therefore:

$r^2 = \frac{D^2}{p_A q_A p_B q_B}$

Unlike $D'$, whose sign depends on the arbitrary labeling of alleles, $r^2$ is always non-negative and ranges from $0$ (linkage equilibrium) to $1$ (perfect correlation). An $r^2$ of $1$ occurs only when two of the four [haplotypes](@entry_id:177949) are absent, meaning knowledge of the allele at one locus perfectly predicts the allele at the other. In statistical terms, $r^2$ is the **[coefficient of determination](@entry_id:168150)**: it measures the proportion of the variance in the allelic state at one locus that can be explained by the allelic state at the other locus.

An important property of $r$ is that it is the same whether calculated from gametic (haploid) data or from genotypic (diploid) data in a randomly mating population. If we consider allele counts per individual ($X', Y' \in \{0,1,2\}$), under [random mating](@entry_id:149892) the correlation $\operatorname{Corr}(X',Y')$ is exactly equal to the gametic correlation $r$ [@problem_id:2732260].

### Comparing Measures: $D'$ versus $r^2$ in Application

The existence of two normalized measures, $D'$ and $r^2$, raises the question of which to use. The answer depends on the scientific question being asked, as they capture different aspects of disequilibrium. $D'$ measures the extent to which the population is missing specific haplotypes, while $r^2$ measures the statistical predictability between loci.

The two measures are not equivalent and can give very different impressions of the strength of LD, especially when [allele frequencies](@entry_id:165920) are skewed. Consider a scenario where one allele is rare. For example, with [haplotype](@entry_id:268358) frequencies $P_{AB}=0.05, P_{Ab}=0, P_{aB}=0.45, P_{ab}=0.50$, the [allele frequencies](@entry_id:165920) are $p_A=0.05$ and $p_B=0.50$. The disequilibrium is $D = 0.05 - (0.05)(0.5) = 0.025$. The maximum possible positive $D$ is $D_{max} = \min(p_A q_B, q_A p_B) = \min((0.05)(0.5), (0.95)(0.5)) = 0.025$. Therefore, $D' = D/D_{max} = 1$. The value of $D'=1$ reflects the fact that the $Ab$ haplotype is absent—a state of complete disequilibrium. However, the squared correlation is $r^2 = (0.025)^2 / ((0.05)(0.95)(0.5)(0.5)) \approx 0.053$. This low value of $r^2$ reflects the poor predictive power between the loci; knowing the state of the common B/b locus tells us little about the state of the rare A/a locus [@problem_id:2732234].

This distinction is critical in applications like **[genome-wide association studies](@entry_id:172285) (GWAS)**, where a key strategy is to genotype a subset of common variants (**tag SNPs**) to act as proxies for untyped variants. The utility of a tag SNP depends on its ability to predict the allelic state of another SNP. This predictive power is directly quantified by $r^2$. The statistical power to detect an association using a tag SNP is a function of the $r^2$ between the tag and the true causal variant. For this reason, $r^2$ is the standard measure for selecting tag SNPs and for assessing the transferability of association signals between markers [@problem_id:2732231]. A high value of $|D'|$ with a low value of $r^2$ is often uninformative for [association mapping](@entry_id:189453).

The different behaviors of these measures can be seen clearly by considering how they change as a function of [allele frequencies](@entry_id:165920). If we fix the frequency of one allele ($p_B$) and the frequency of one haplotype ($P_{AB}$), and allow the other [allele frequency](@entry_id:146872) ($p_A$) to vary, $D$ changes linearly, while $D'$ and $r^2$ exhibit more complex, non-linear behavior. $D'$ will vary between $-1$ and $1$ across the feasible range of $p_A$, whereas $r^2$ will start at a value less than 1, decrease to a unique minimum of 0 (at linkage equilibrium), and then increase again [@problem_id:2825914].

### The Dynamics of Linkage Disequilibrium

Linkage disequilibrium is not a static property of a population; it is generated and eroded by several [evolutionary forces](@entry_id:273961).

#### Erosion by Recombination

The most fundamental process that breaks down LD is **recombination**. In a large, randomly mating population free from other evolutionary forces, the value of $D$ is expected to decay over generations. Consider the frequency of the $AB$ [haplotype](@entry_id:268358) in the next generation, $P_{AB}(t+1)$. An $AB$ gamete can be produced in two ways: (1) as a non-recombinant gamete from a [diploid](@entry_id:268054) parent, which occurs with probability $(1-r)$, where $r$ is the [recombination fraction](@entry_id:192926); or (2) as a newly formed recombinant gamete, which occurs with probability $r$. Under [random mating](@entry_id:149892), the alleles that recombine are drawn independently from the population's allele frequency pool. This leads to the recurrence relation:

$P_{AB}(t+1) = (1-r)P_{AB}(t) + r p_A p_B$

By substituting $D(t) = P_{AB}(t) - p_A p_B$ (noting that [allele frequencies](@entry_id:165920) $p_A$ and $p_B$ are constant under these assumptions), we can derive the dynamics of $D$ itself:

$D(t+1) = (1-r)D(t)$

This simple but powerful result shows that LD decays geometrically (exponentially) each generation by a factor of $(1-r)$. For unlinked loci on different chromosomes, $r=0.5$, and LD is halved each generation. For very tightly linked loci, $r \approx 0$, and LD decays very slowly. After $t$ generations, the amount of LD remaining is $D(t) = (1-r)^t D(0)$. The difference is stark: after 5 generations, the fraction of initial LD remaining for an unlinked locus is $(0.5)^5 \approx 0.03$, while for a linked locus with $r=0.01$, it is $(0.99)^5 \approx 0.95$ [@problem_id:2825913].

#### Generation by Population Admixture: The Wahlund Effect

While recombination erodes LD, other forces can generate it. These include selection, mutation, genetic drift, and, critically, [population structure](@entry_id:148599). The generation of spurious LD by the pooling of genetically distinct subpopulations is a classic phenomenon known as the **Wahlund effect**.

Imagine two subpopulations that are themselves in linkage equilibrium ($D=0$ within each), but which have different [allele frequencies](@entry_id:165920). For example, suppose in deme 1, $p_A=0.8$ and $p_B=0.2$, while in deme 2, $p_A=0.2$ and $p_B=0.8$. If we were to pool equal numbers of individuals from both demes into a single sample, the pooled allele frequencies would be $p_A=0.5$ and $p_B=0.5$. However, the pooled sample would show significant, non-zero LD. This occurs because the pooled sample has an excess of the haplotypes that were common in the original demes (e.g., $Ab$ and $aB$) and a deficit of the haplotypes that were rare (e.g., $AB$ and $ab$), creating a negative value of $D$. This apparent LD does not reflect physical linkage but is an artifact of the hidden population structure [@problem_id:2732248].

The total disequilibrium in a mixture ($D_{total}$) can be decomposed into the average disequilibrium within subpopulations ($\bar{D}$) and the covariance of [allele frequencies](@entry_id:165920) across those subpopulations ($\operatorname{Cov}(p_A, p_B)$):

$D_{total} = \bar{D} + \operatorname{Cov}(p_A, p_B)$

In the scenario described, $\bar{D}=0$, and the entire observed LD is due to the covariance term. This underscores a critical pitfall in population genetic studies: an observation of LD in a sample is not, by itself, evidence of physical linkage or historical association. One must first rule out the possibility of [population stratification](@entry_id:175542). A standard diagnostic is to stratify the analysis by suspected subpopulations. If the LD disappears or is greatly attenuated within the strata, the Wahlund effect is a likely explanation. Statistical methods like the **Cochran–Mantel–Haenszel (CMH) test** provide a formal framework for testing for association while conditioning on population labels, effectively removing confounding due to admixture [@problem_id:2732248].

### Higher-Order Disequilibrium

The discussion thus far has focused on pairwise, or two-locus, disequilibrium. However, the concept can be extended to three or more loci. **Higher-order LD** describes statistical interactions among multiple loci that cannot be explained by pairwise interactions alone.

Consider three loci, $A/a$, $B/b$, and $C/c$. It is possible to construct a scenario where all three pairwise LD coefficients are zero ($D_{AB}=D_{AC}=D_{BC}=0$), yet the loci are not fully independent. For instance, consider a population consisting of only four [haplotypes](@entry_id:177949), each at a frequency of $0.25$: $ABC$, $Abc$, $aBc$, and $abC$. In this population, the allele frequencies are all $0.5$, and one can verify that all pairwise LDs are exactly zero. However, the frequency of the $ABC$ haplotype, $0.25$, is not equal to the product of the [allele frequencies](@entry_id:165920), $p_A p_B p_C = (0.5)^3 = 0.125$.

This residual deviation is captured by the three-locus disequilibrium coefficient, $D_{ABC}$. In a system with no pairwise LD, it is defined as:

$D_{ABC} = P_{ABC} - p_A p_B p_C$

For our example, $D_{ABC} = 0.25 - 0.125 = 0.125$. This non-zero value reveals a specific three-way interaction: an over-representation of haplotypes with an even number of 'lowercase' alleles. This demonstrates that the genetic architecture of a population can have complexities that are invisible to pairwise analysis, necessitating a more sophisticated view of multi-locus structure [@problem_id:2732262].