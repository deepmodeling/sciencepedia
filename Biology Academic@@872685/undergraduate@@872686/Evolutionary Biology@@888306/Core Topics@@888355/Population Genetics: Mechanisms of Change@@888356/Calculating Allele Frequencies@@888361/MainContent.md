## Introduction
The genetic composition of a population is the raw material for evolution. To decipher how populations change over time, we must first learn to quantify this composition. The most fundamental metric for this is the **allele frequency**—the relative proportion of a specific gene variant in the [gene pool](@entry_id:267957). But how are these frequencies measured, and what causes them to shift from one generation to the next? This article demystifies the core concepts of population genetics by providing a comprehensive guide to calculating and interpreting allele frequencies.

First, in **Principles and Mechanisms**, we will delve into the foundational methods for determining [allele frequencies](@entry_id:165920), from direct gene counting to the elegant inferences made possible by the Hardy-Weinberg equilibrium. We will also explore the primary forces—natural selection, genetic drift, and [gene flow](@entry_id:140922)—that drive [microevolution](@entry_id:140463) by altering these frequencies. Next, in **Applications and Interdisciplinary Connections**, we will bridge theory and practice by showcasing how these calculations are applied to solve critical problems in fields as diverse as [medical genetics](@entry_id:262833), [conservation biology](@entry_id:139331), and [paleogenomics](@entry_id:165899). Finally, you will have the opportunity to solidify your knowledge in **Hands-On Practices** through guided problems that challenge you to apply these principles to realistic scenarios.

## Principles and Mechanisms

The genetic composition of a population is the foundation upon which evolutionary forces act. To understand evolution, we must first be able to quantify this composition. The most fundamental measure of [genetic variation](@entry_id:141964) within a population is the **allele frequency**, which represents the proportion of a specific allele within the population's gene pool. This section will delineate the principles for calculating allele frequencies from different types of data and explore the primary mechanisms that cause these frequencies to change over time.

### Direct Calculation of Allele Frequencies from Genotype Data

The most direct method for determining [allele frequencies](@entry_id:165920) is to count them from known genotype data. In a diploid population of $N$ individuals, there are $2N$ total alleles for any given autosomal [gene locus](@entry_id:177958). The collection of all these alleles is referred to as the **[gene pool](@entry_id:267957)**.

Consider a simple locus with two alleles, which we can denote as $A$ and $a$. An individual's genotype will be either [homozygous](@entry_id:265358) ($AA$ or $aa$) or [heterozygous](@entry_id:276964) ($Aa$). If we can survey the population and count the number of individuals with each genotype ($n_{AA}$, $n_{Aa}$, and $n_{aa}$), we can calculate the frequency of allele $A$, denoted as $p$, and the frequency of allele $a$, denoted as $q$.

Each $AA$ individual carries two copies of the $A$ allele, and each $Aa$ individual carries one copy. Therefore, the total number of $A$ alleles in the population is $(2 \times n_{AA}) + n_{Aa}$. The frequency of allele $A$ is this count divided by the total number of alleles in the gene pool ($2N$):

$p = f(A) = \frac{2 n_{AA} + n_{Aa}}{2N}$

Similarly, the frequency of allele $a$ is:

$q = f(a) = \frac{2 n_{aa} + n_{Aa}}{2N}$

Since there are only two alleles at this locus, the sum of their frequencies must be unity: $p + q = 1$.

For instance, consider a population survey of 1850 orchids where [genetic analysis](@entry_id:167901) provides exact genotype counts: 759 plants with genotype $C^A C^A$, 872 with $C^A C^B$, and 219 with $C^B C^B$ [@problem_id:1912317]. The total number of alleles in this sample is $2 \times 1850 = 3700$. The number of $C^A$ alleles is derived from the $C^A C^A$ homozygotes, which contribute $2 \times 759 = 1518$ alleles, and the $C^A C^B$ heterozygotes, which contribute 872 alleles. The frequency of the $C^A$ allele, $p$, is therefore:

$p = f(C^A) = \frac{(2 \times 759) + 872}{2 \times 1850} = \frac{1518 + 872}{3700} = \frac{2390}{3700} \approx 0.646$

This direct counting method is robust and does not rely on any assumptions about the population's mating structure. It is the gold standard for measuring allele frequencies when genotype data is available, as is often the case in studies involving agricultural pests like the cotton bollworm [@problem_id:1912305].

The same principle extends straightforwardly to loci with more than two alleles. For a gene with three alleles ($L^R$, $L^Y$, and $L^B$), the frequency of any given allele is found by summing twice the count of its homozygote with the counts of all heterozygotes containing that allele, and dividing by the total number of alleles in the sample ($2N$). In a study of 700 fireflies, genotype counts allowed for the precise calculation of the frequencies of all three alleles controlling glow color, demonstrating the general applicability of this counting method [@problem_id:1912287]. The sum of the frequencies of all alleles at the locus, $f(L^R) + f(L^Y) + f(L^B)$, must equal 1.

### Inferring Allele Frequencies with the Hardy-Weinberg Principle

Often, it is not possible to determine the exact genotype of all individuals. This is particularly true in cases of complete dominance, where homozygous dominant ($AA$) and heterozygous ($Aa$) individuals are phenotypically indistinguishable. In such situations, we can infer [allele frequencies](@entry_id:165920) if we can reasonably assume the population meets the conditions of the **Hardy-Weinberg Equilibrium (HWE)**.

The Hardy-Weinberg principle serves as a [null model](@entry_id:181842) in [population genetics](@entry_id:146344). It describes a population that is not evolving. For a population to be in HWE for a specific locus, it must satisfy several key assumptions: a large (effectively infinite) population size, [random mating](@entry_id:149892), and the absence of evolutionary pressures such as mutation, migration ([gene flow](@entry_id:140922)), and natural selection.

For a locus with two alleles, $A$ and $a$, with frequencies $p$ and $q$ respectively, the HWE principle predicts that after one generation of [random mating](@entry_id:149892), the genotype frequencies will be:

-   Frequency of $AA = p^2$
-   Frequency of $Aa = 2pq$
-   Frequency of $aa = q^2$

These genotype frequencies sum to 1: $p^2 + 2pq + q^2 = 1$. This mathematical relationship provides a powerful tool. If we observe a population where a trait is determined by complete dominance, the only genotype that can be directly identified from its phenotype is the [homozygous recessive](@entry_id:273509) ($aa$). The observed frequency of this recessive phenotype in the population is a direct estimate of $q^2$.

From this starting point, we can deduce the [allele frequencies](@entry_id:165920). For example, if a survey of 4800 moths finds that 432 have light-colored wings, a known recessive trait ($ww$), we can estimate the frequency of the $ww$ genotype as $\frac{432}{4800} = 0.09$ [@problem_id:1912347]. Assuming HWE, this frequency is equal to $q^2$:

$q^2 = 0.09$

The frequency of the recessive allele, $q$, is the square root of this value:

$q = \sqrt{0.09} = 0.3$

Since $p + q = 1$, the frequency of the dominant allele, $p$, is:

$p = 1 - q = 1 - 0.3 = 0.7$

Once we have estimated $p$ and $q$, we can also calculate the expected frequencies of the other genotypes. The frequency of [heterozygous](@entry_id:276964) individuals, for example, is predicted to be $2pq$. This is a common application in [ecological genetics](@entry_id:263765), such as estimating the proportion of carriers for a recessive trait in a wild population [@problem_id:1912331] [@problem_id:1912322]. For a population of flowering plants where the frequency of the white-flowered recessive homozygote ($cc$) was found to be $\frac{49}{2500}$, the frequency of the recessive allele $c$ is $q = \sqrt{49/2500} = 7/50 = 0.14$. Consequently, the frequency of the dominant allele $C$ is $p = 1 - 0.14 = 0.86$. The expected frequency of heterozygotes ($Cc$) in this population is therefore $2pq = 2(0.86)(0.14) \approx 0.241$ [@problem_id:1912322].

### Mechanisms of Allele Frequency Change

The Hardy-Weinberg principle provides a static baseline. The true focus of evolutionary biology is understanding change. When the assumptions of HWE are violated, allele frequencies can and do change from one generation to the next. This change is the very definition of [microevolution](@entry_id:140463).

#### Natural Selection

**Natural selection** is the process whereby individuals with certain heritable traits survive and reproduce at higher rates than other individuals. Selection acts on the phenotype, but its evolutionary consequence is a change in the frequencies of the underlying alleles. We can quantify this by assigning a **[relative fitness](@entry_id:153028) ($w$)** to each genotype, which measures its comparative [reproductive success](@entry_id:166712). A common convention is to set the fitness of the most successful genotype to $w=1$.

Consider a population initially in HWE with allele frequencies $p_0$ and $q_0$. The genotype frequencies at the [zygote](@entry_id:146894) stage are $p_0^2$, $2p_0 q_0$, and $q_0^2$. If these genotypes have different survival rates to adulthood, defined by their relative fitnesses ($w_{SS}, w_{SR}, w_{RR}$), the frequencies of the genotypes among the surviving adults will be proportional to $p_0^2 w_{SS}$, $2p_0 q_0 w_{SR}$, and $q_0^2 w_{RR}$.

To find the normalized frequencies, we divide by the **mean fitness of the population ($\overline{w}$)**, which is the weighted average of the fitnesses of the genotypes:

$\overline{w} = p_0^2 w_{SS} + 2p_0 q_0 w_{SR} + q_0^2 w_{RR}$

The frequency of the $S$ allele in the next generation ($p_1$) is the frequency of that allele among the survivors. It is calculated by summing the frequencies of genotypes carrying the allele, weighted by the number of $S$ alleles they carry (2 for $SS$, 1 for $SR$), after selection:

$p_1 = \frac{p_0^2 w_{SS} + p_0 q_0 w_{SR}}{\overline{w}}$

This model can be applied to practical scenarios, such as the evolution of pesticide resistance [@problem_id:1912313]. If an insect population with an initial susceptible allele frequency of $p_0 = 0.8$ is subjected to a pesticide that results in fitness values of $w_{SS}=0.30$, $w_{SR}=0.65$, and $w_{RR}=1.0$, the frequency of the susceptible allele will decrease dramatically in a single generation. The calculation reveals a new frequency of $p_1 \approx 0.6727$, demonstrating the rapid efficacy of strong [directional selection](@entry_id:136267).

#### Gene Flow

**Gene flow**, or migration, is the transfer of alleles from one population to another. It acts as a homogenizing force, reducing genetic differences between populations. The effect of a migration event on allele frequency can be calculated with a simple mixing model.

If a recipient population of size $N_{rec}$ and allele frequency $p_{rec}$ receives $N_{mig}$ migrants from a source population with [allele frequency](@entry_id:146872) $p_{src}$, the new allele frequency in the admixed population ($p'$) is the weighted average of the original frequencies, where the weights are the proportional contributions of each group to the new total population.

$p' = \frac{(p_{rec} \times N_{rec}) + (p_{src} \times N_{mig})}{N_{rec} + N_{mig}}$

This equation represents the total number of the allele of interest in the new population, divided by the total number of gene copies. This principle is scalable from birds migrating between islands to bacteria being transferred between cultures [@problem_id:1912329]. For example, if a flask of $3.5 \times 10^8$ bacteria with a resistance gene frequency of $0.12$ receives $5.0 \times 10^7$ cells from a source where the frequency is $0.88$, the new frequency in the flask is not a simple average. It is a weighted average reflecting the relative sizes of the populations being mixed, resulting in a new frequency of $0.215$.

#### Genetic Drift and Fixation Probability

**Genetic drift** refers to random fluctuations in allele frequencies that occur in finite populations due to chance events in survival and reproduction ([sampling error](@entry_id:182646)). Its effects are most pronounced in small populations. Over time, drift leads to the loss of alleles and the eventual **fixation** of a single allele at a locus (i.e., its frequency becomes 1.0).

A cornerstone of neutral theory, developed by Motoo Kimura and others, concerns the ultimate fate of a new, neutral allele—one that has no effect on fitness. For such an allele, its probability of eventually becoming fixed in the population is simply equal to its initial frequency, $p_0$.

$P_{fixation} = p_0$

This remarkably simple and powerful result means that a new mutation arising in a single [diploid](@entry_id:268054) individual (initial frequency $p_0 = \frac{1}{2N}$) has a very small chance of fixation, whereas an allele that is already common has a high probability of eventually becoming the only allele. This principle is crucial in conservation biology, for instance, when assessing the genetic future of a newly founded population [@problem_id:1912293]. If a new population of birds is founded by mixing 35 individuals from a source with $p_1 = 0.75$ and 15 individuals from another source with $p_2 = 0.20$, the initial [allele frequency](@entry_id:146872) in the founder group is a weighted average: $p_0 = \frac{(35 \times 0.75) + (15 \times 0.20)}{35+15} = 0.585$. The probability that this neutral marker allele will eventually drift to fixation in the island population is therefore precisely $0.585$. The long-term [effective population size](@entry_id:146802) ($N_e$) influences how *fast* this process of drift occurs, but for a neutral allele, it does not alter the ultimate probability of fixation.

#### Population Structure and F-Statistics

In reality, few species exist as single, panmictic units. Most are subdivided into smaller, semi-isolated subpopulations. Gene flow among them may be limited, allowing their allele frequencies to diverge due to drift or localized selection. **F-statistics**, developed by Sewall Wright, provide a framework for quantifying this genetic structure.

The most common of these is the **[fixation index](@entry_id:174999), $F_{ST}$**. It measures the degree of [genetic differentiation](@entry_id:163113) among subpopulations. Conceptually, $F_{ST}$ quantifies the proportion of the total [genetic variance](@entry_id:151205) that is found *between* subpopulations. It ranges from 0 (no differentiation; all subpopulations have the same allele frequencies) to 1 (complete differentiation; subpopulations are fixed for different alleles).

For a locus with two alleles, $F_{ST}$ can be calculated from the variance in allele frequency among subpopulations, $\operatorname{Var}(p)$, and the [allele frequency](@entry_id:146872) in the total metapopulation, $p_T$:

$F_{ST} = \frac{\operatorname{Var}(p)}{p_T (1 - p_T)}$

This relationship allows us to connect the observable pattern of differentiation ($F_{ST}$) to the underlying allele frequencies in the constituent populations. For example, if two isolated and equally sized plant subpopulations have a total metapopulation [allele frequency](@entry_id:146872) of $p_T = 0.5$ and a high [fixation index](@entry_id:174999) of $F_{ST} = 0.36$, this indicates significant divergence [@problem_id:1912346]. Using the formula, we can solve for the unknown subpopulation frequencies. An $F_{ST}$ of $0.36$ in this scenario implies that the [allele frequencies](@entry_id:165920) in the two subpopulations have diverged to $0.2$ and $0.8$, a clear quantitative picture of the genetic consequences of isolation.