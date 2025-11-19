## Introduction
In the study of genetics, we learn that genes on the same chromosome tend to be inherited together—a principle known as [genetic linkage](@entry_id:138135). However, this is only part of the story. Within a population, alleles at different genetic loci often show associations that are not random, creating patterns that hold profound clues about our evolutionary past and our susceptibility to disease. This phenomenon, known as **[linkage disequilibrium](@entry_id:146203) (LD)**, and the specific combination of alleles on a chromosome, the **[haplotype](@entry_id:268358)**, are central concepts in modern genomics. The challenge lies in quantifying these non-random associations and understanding the [evolutionary forces](@entry_id:273961) that shape them. This article provides a foundational guide to these powerful ideas. The first chapter, "Principles and Mechanisms," will unpack the definition of haplotypes and LD, introducing the quantitative tools used to measure them and exploring the evolutionary processes that create and erode these patterns. Next, "Applications and Interdisciplinary Connections" will showcase how analyzing LD and haplotypes fuels discoveries in human medicine, evolutionary biology, and even fields beyond genetics. Finally, "Hands-On Practices" will solidify your understanding with practical exercises in calculating and interpreting genetic data.

## Principles and Mechanisms

The previous chapter introduced the concept of [genetic linkage](@entry_id:138135)—the tendency of genes located on the same chromosome to be inherited together. However, the story of how alleles at different loci are associated within a population is more complex than simple physical linkage. This chapter delves into the principles of **[haplotypes](@entry_id:177949)** and **linkage disequilibrium**, the quantitative framework used to describe non-random associations between alleles, and the [evolutionary mechanisms](@entry_id:196221) that create, maintain, and erode these associations.

### Haplotypes and Genetic Phase

In a [diploid](@entry_id:268054) organism, the genotype describes the pair of alleles present at one or more loci. For example, an individual with genotype $A/a$ is [heterozygous](@entry_id:276964) at a single locus. When we consider two loci simultaneously, say with alleles $R$ and $r$ at the first locus and $T$ and $t$ at the second, an individual [heterozygous](@entry_id:276964) at both loci has the genotype $R/r; T/t$. While this notation tells us which alleles are present, it does not specify how they are arranged on the pair of [homologous chromosomes](@entry_id:145316).

The specific combination of alleles located on a single chromosome is known as a **haplotype** (a portmanteau of "[haploid](@entry_id:261075) genotype"). For the doubly heterozygous individual $R/r; T/t$, there are two distinct possibilities for the arrangement of its alleles, a property known as the **genetic phase**.

1.  **Coupling or Cis Configuration**: The dominant (or parental) alleles $R$ and $T$ are on one chromosome, and the recessive (or other parental) alleles $r$ and $t$ are on the homologous chromosome. The individual's two haplotypes are thus $RT$ and $rt$. This is often written as $RT/rt$.

2.  **Repulsion or Trans Configuration**: The allele $R$ is on the same chromosome as $t$, while $r$ is paired with $T$ on the other chromosome. This gives the haplotypes $Rt$ and $rT$, written as $Rt/rT$.

Therefore, a simple genotypic description like $R/r; T/t$ is ambiguous; it could represent either of two fundamentally different chromosomal arrangements [@problem_id:1501150].

This ambiguity has significant practical consequences. Standard genotyping methods often produce "unphased" data, meaning we know an individual's genotype at multiple sites (e.g., they are $A/a$ at locus 1 and $B/b$ at locus 2), but we do not know the phase. For homozygous individuals ($AABB$, $aabb$, $AAbb$, etc.), the [haplotypes](@entry_id:177949) are unambiguous. For instance, an $AAbb$ individual must carry two $Ab$ haplotypes. However, for a double heterozygote ($AaBb$), we cannot know without further information whether their haplotypes are $AB/ab$ (cis) or $Ab/aB$ (trans).

Consider a study where a population of 1000 plants is genotyped at two loci, A and B. Among them, 300 are found to be double heterozygotes ($AaBb$), 20 are $AAbb$, 80 are $AABb$, and 50 are $Aabb$. If we wish to count the total number of $Ab$ haplotypes in this sample, we face an uncertainty. The $AAbb$ individuals contribute $2 \times 20 = 40$ copies of the $Ab$ [haplotype](@entry_id:268358). The $AABb$ individuals (genotype $AB/Ab$) contribute 80 copies. The $Aabb$ individuals ($Ab/ab$) contribute 50 copies. The baseline count from these unambiguous genotypes is $40 + 80 + 50 = 170$. Now consider the 300 $AaBb$ individuals. If all of them are in the cis phase ($AB/ab$), they contribute zero $Ab$ [haplotypes](@entry_id:177949). If all are in the trans phase ($Ab/aB$), they contribute 300 $Ab$ haplotypes. Consequently, the true total count of the $Ab$ [haplotype](@entry_id:268358) in the sample lies within a range—from a minimum of 170 to a maximum of $170 + 300 = 470$ [@problem_id:1501136]. Resolving this phase ambiguity requires either pedigree information or specialized molecular or statistical phasing techniques.

### Quantifying Allelic Association: Linkage Disequilibrium

In a population, alleles at different loci may be associated randomly or non-randomly. The state in which alleles at one locus are randomly associated with alleles at a second locus is called **linkage equilibrium (LE)**. Under LE, the frequency of any given [haplotype](@entry_id:268358) is simply the product of the frequencies of its constituent alleles. For example, if the frequency of allele $A$ is $p_A$ and the frequency of allele $B$ is $p_B$, the expected frequency of the $AB$ haplotype at equilibrium is $P_{AB} = p_A p_B$.

When this condition is not met, the loci are said to be in **linkage disequilibrium (LD)**. LD is the non-random association of alleles at different loci. The deviation from linkage equilibrium is quantified by the **coefficient of linkage disequilibrium, $D$**. For two loci with alleles A/a and B/b, it is defined as:

$D = P_{AB} - p_A p_B$

where $P_{AB}$ is the observed frequency of the $AB$ [haplotype](@entry_id:268358), and $p_A$ and $p_B$ are the population frequencies of the $A$ and $B$ alleles, respectively.

*   If $D = 0$, the loci are in linkage equilibrium.
*   If $D > 0$, the $AB$ [haplotype](@entry_id:268358) is more frequent than expected by chance. This implies an overrepresentation of the coupling [haplotypes](@entry_id:177949) ($AB$ and $ab$).
*   If $D  0$, the $AB$ [haplotype](@entry_id:268358) is less frequent than expected. This implies an overrepresentation of the repulsion [haplotypes](@entry_id:177949) ($Ab$ and $aB$).

A useful property of $D$ is that the deviation from expectation is equal in magnitude but opposite in sign for all four haplotypes. Let's denote the frequencies of alleles $a$ and $b$ as $p_a$ and $p_b$. The frequencies of the four possible haplotypes can be expressed in terms of the [allele frequencies](@entry_id:165920) and the single parameter $D$:

$P_{AB} = p_A p_B + D$
$P_{Ab} = p_A p_b - D$
$P_{aB} = p_a p_B - D$
$P_{ab} = p_a p_b + D$

These relationships allow us to calculate any haplotype frequency if we know the [allele frequencies](@entry_id:165920) and $D$. For instance, imagine a population where for two loci, the frequency of allele $C$ is $p_C = 0.65$ and the frequency of allele $H$ is $p_H = 0.32$. This means $p_T = 1 - 0.65 = 0.35$ and $p_L = 1 - 0.32 = 0.68$. If the linkage disequilibrium is measured to be $D = -0.035$, we can find the frequency of the $TL$ [haplotype](@entry_id:268358). Using the formula $P_{TL} = p_T p_L + D$, we get:

$P_{TL} = (0.35)(0.68) + (-0.035) = 0.238 - 0.035 = 0.203$ [@problem_id:1501138].

Similarly, we can use this framework to calculate other haplotype frequencies, such as the $lg$ [haplotype](@entry_id:268358) in a grasshopper population where $p_L=0.55$, $p_G=0.25$, and $D=-0.090$. We find $p_l = 1 - 0.55 = 0.45$ and $p_g = 1 - 0.25 = 0.75$. The frequency of the $lg$ haplotype is then $P_{lg} = p_l p_g + D = (0.45)(0.75) - 0.090 = 0.3375 - 0.090 = 0.2475$ [@problem_id:1944771].

Conversely, if we have empirical data on [haplotype](@entry_id:268358) counts, we can directly calculate $D$. For example, if a sample of 1000 chromosomes reveals 600 CG, 50 CA, 150 TG, and 200 TA [haplotypes](@entry_id:177949), we first calculate the frequencies: $P_{CG} = 0.60$, $p_C = (600+50)/1000 = 0.65$, and $p_G = (600+150)/1000 = 0.75$. Then, $D$ is calculated as $D = 0.60 - (0.65)(0.75) = 0.60 - 0.4875 = 0.1125$ [@problem_id:1944761]. Such regions of high LD are often referred to as **[haplotype blocks](@entry_id:166800)**, contiguous segments of the genome where a set of alleles are strongly associated and tend to be inherited as a unit.

### The Generation and Decay of Linkage Disequilibrium

Linkage disequilibrium is not a static feature of a population; it is a dynamic quantity shaped by various evolutionary forces.

#### Mechanisms that Generate Linkage Disequilibrium

LD is not merely a consequence of physical linkage. Several key evolutionary processes can create non-random associations between alleles, even those at unlinked loci.

1.  **Mutation**: When a new mutation arises, it does so on a single chromosome, which carries a specific set of alleles at other loci. In that instant, the new mutant allele is perfectly associated with that specific haplotype background. Consider a population where a locus is initially fixed for allele $M$. A new mutation creates allele $m$ on a chromosome that happens to carry allele $Q$ at a nearby locus. Immediately after this event in a population of size $N$, the frequency of the new allele is $f(m) = 1/(2N)$. Since this new allele exists only on a $Q$-carrying chromosome, the frequency of the $Qm$ [haplotype](@entry_id:268358) is also $f(Qm) = 1/(2N)$. If the frequency of allele $Q$ in the population is $p_Q$, the initial LD is $D = f(Qm) - p_Q f(m) = \frac{1}{2N} - p_Q \frac{1}{2N} = \frac{1 - p_Q}{2N} = \frac{p_q}{2N}$ [@problem_id:1501164]. Thus, every new mutation is a source of linkage disequilibrium.

2.  **Genetic Drift**: In finite populations, random fluctuations in allele and haplotype frequencies from one generation to the next can create LD by chance. This effect is particularly pronounced during population bottlenecks or **founder events**. Imagine a small group of five individuals colonizing an island. Even if the large mainland source population was in linkage equilibrium, this small, random sample of haplotypes is unlikely to be. For example, if the 10 chromosomes of the founders include 3 $AB$, 2 $Ab$, 2 $aB$, and 3 $ab$ [haplotypes](@entry_id:177949), the [allele frequencies](@entry_id:165920) are $p_A = (3+2)/10 = 0.5$ and $p_B = (3+2)/10 = 0.5$. The expected frequency of the $AB$ [haplotype](@entry_id:268358) would be $0.5 \times 0.5 = 0.25$. However, its observed frequency is $P_{AB} = 3/10 = 0.3$. This results in a non-zero LD: $D = 0.3 - 0.25 = 0.05$ [@problem_id:1501157]. Thus, [genetic drift](@entry_id:145594), simply by stochastic sampling, can generate significant LD.

3.  **Population Admixture**: When two or more populations, which have been evolving independently and have developed different allele frequencies, merge, LD can be generated in the resulting admixed population. This occurs even if both source populations were themselves in linkage equilibrium. Consider an "Upland" population with $p_A=0.8, p_B=0.3$ and a "Lowland" population with $p_A=0.1, p_B=0.6$. In the Upland population at LE, $P_{AB}^{(1)} = 0.8 \times 0.3 = 0.24$. In the Lowland population at LE, $P_{AB}^{(2)} = 0.1 \times 0.6 = 0.06$. If we create a new population by mixing equal numbers from both, the new frequencies will be the average: $p_A^{(M)} = 0.5(0.8+0.1) = 0.45$, $p_B^{(M)} = 0.5(0.3+0.6) = 0.45$, and $P_{AB}^{(M)} = 0.5(0.24+0.06) = 0.15$. The LD in this new admixed population is $D = P_{AB}^{(M)} - p_A^{(M)} p_B^{(M)} = 0.15 - (0.45 \times 0.45) = 0.15 - 0.2025 = -0.0525$ [@problem_id:1501182]. The admixture has instantly created LD.

4.  **Natural Selection**: If selection favors certain combinations of alleles (a phenomenon known as **epistasis**), it can create and maintain LD. For instance, if the haplotype $AB$ confers a higher fitness than any other combination, its frequency will increase beyond the product of the individual allele frequencies, resulting in $D > 0$.

#### The Decay of Linkage Disequilibrium by Recombination

The primary force that breaks down linkage disequilibrium is **recombination**. During meiosis, [crossing over](@entry_id:136998) between homologous chromosomes can shuffle alleles, creating new haplotype combinations from parental ones. For example, a parent with genotype $AB/ab$ can produce [recombinant gametes](@entry_id:261332) $Ab$ and $aB$. This process gradually randomizes the associations between alleles, driving the population towards linkage equilibrium ($D=0$).

The rate at which LD decays is directly related to the **[recombination rate](@entry_id:203271) ($r$)** between the two loci. In each generation, the amount of LD is reduced by a factor of $(1-r)$. This leads to an [exponential decay](@entry_id:136762) of LD over time:

$D_t = D_0 (1-r)^t$

where $D_t$ is the LD at generation $t$, $D_0$ is the initial LD, and $r$ is the [recombination rate](@entry_id:203271).

This equation has a profound implication: the strength of LD between two loci is inversely related to the recombination frequency between them.
*   For **unlinked loci** (on different chromosomes or very far apart on the same chromosome), $r=0.5$. LD decays rapidly, halving each generation.
*   For **tightly linked loci**, $r$ is very small. LD will decay very slowly over many generations.

This principle explains why we observe [haplotype blocks](@entry_id:166800). These are genomic regions with very low internal recombination rates, allowing LD to persist for long periods. A comparison illustrates this point clearly. Suppose we have two pairs of loci, A-B and A-C, which by chance have the same initial LD ($D_{AB,0} = D_{AC,0} = 0.15$). However, the A-B pair is tightly linked with $r_{AB}=0.02$, while the A-C pair is more loosely linked with $r_{AC}=0.20$. After 5 generations, the ratio of their LD values will be:

$\frac{D_{AC,5}}{D_{AB,5}} = \frac{D_0(1-0.20)^5}{D_0(1-0.02)^5} = \left(\frac{0.80}{0.98}\right)^5 \approx 0.3625$

This shows that the LD between the more distant A-C loci has decayed far more significantly than the LD between the nearby A-B loci [@problem_id:1944727]. LD is therefore a powerful signal of the physical proximity of genes on a chromosome and the local recombination landscape.

### Normalized Measures of Linkage Disequilibrium: $D'$ and $r^2$

The raw value of $D$ can be difficult to interpret because its maximum and minimum possible values are constrained by the [allele frequencies](@entry_id:165920) of the loci in question. For example, if allele $A$ is rare, the frequency of the $AB$ [haplotype](@entry_id:268358) is necessarily low, limiting the potential magnitude of $D$. To facilitate comparisons of LD across different pairs of loci or different populations, we use normalized measures.

#### The Normalized Disequilibrium Coefficient, $D'$

The **normalized [linkage disequilibrium](@entry_id:146203) coefficient, $D'$** (pronounced "D prime"), scales $D$ by its theoretical maximum possible value given the observed allele frequencies.

If $D > 0$, then $D' = \frac{D}{D_{\text{max}}}$, where $D_{\text{max}} = \min(p_A p_b, p_a p_B)$.
If $D  0$, then $D' = \frac{D}{D_{\text{min}}}$, where $D_{\text{min}} = \max(-p_A p_B, -p_a p_b)$.

The value of $D'$ ranges from -1 to 1. A value of $|D'|=1$ has a specific biological interpretation: it indicates that at least one of the four possible haplotypes is absent in the population. This suggests a lack of historical recombination between the two sites since the mutations that defined the alleles arose.

#### The Squared Correlation Coefficient, $r^2$

Another crucial measure is the **squared correlation coefficient, $r^2$**. It is defined as:

$r^2 = \frac{D^2}{p_A p_a p_B p_b}$

This metric, ranging from 0 to 1, measures the [statistical correlation](@entry_id:200201) between the alleles at two loci. An $r^2=1$ indicates a perfect correlation: knowing the allele at one locus allows you to predict the allele at the second locus with certainty. An $r^2=0$ indicates no correlation (linkage equilibrium). The $r^2$ statistic is particularly important in the context of [genome-wide association studies](@entry_id:172285) (GWAS), as it quantifies how well one genetic marker (a "tag SNP") can serve as a proxy for another, ungenotyped variant.

#### Comparing $D'$ and $r^2$

While both are useful, $D'$ and $r^2$ measure different aspects of LD and are not interchangeable. $D'$ is more a measure of recombination history, while $r^2$ is a measure of predictability. A pair of loci can have a maximal $D'$ value but a very low $r^2$ value.

This occurs when there is a large disparity in [allele frequencies](@entry_id:165920). Consider a scenario where a survey finds haplotype counts of $AB$: 450, $Ab$: 0, $aB$: 29,550, and $ab$: 4,500. The absence of the $Ab$ [haplotype](@entry_id:268358) immediately tells us that $|D'|=1$. Indeed, calculation confirms $D' = 1$. However, allele $A$ is very rare ($p_A \approx 0.013$) while allele $B$ is very common ($p_B \approx 0.87$). Because $A$ is so rare, knowing that a chromosome does not have allele $B$ is not very informative about whether it has allele $A$. The low predictive power is reflected in a very low $r^2$ value, which calculates to approximately $0.00198$ for this dataset [@problem_id:1944765]. This example powerfully illustrates that while $D'=1$ indicates a complete association in a historical sense (no recombination has created the missing [haplotype](@entry_id:268358)), the association may have little predictive power if one of the alleles is rare, a nuance captured by $r^2$. Understanding the distinction between these two measures is critical for the proper interpretation of genetic data in population and [medical genetics](@entry_id:262833).