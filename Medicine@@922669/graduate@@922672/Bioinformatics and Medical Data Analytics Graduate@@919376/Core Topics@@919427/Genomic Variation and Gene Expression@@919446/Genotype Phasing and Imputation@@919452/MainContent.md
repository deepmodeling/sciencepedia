## Introduction
Genomic data obtained from standard genotyping technologies is inherently ambiguous; while it tells us which genetic variants an individual possesses, it does not reveal their parental origin. This unresolved assignment of alleles to their respective chromosomes, known as the genetic phase, represents a significant knowledge gap. Genotype phasing and imputation are powerful computational methods designed to solve this problem, allowing us to reconstruct complete [haplotypes](@entry_id:177949) and infer genotypes at millions of unmeasured sites. The ability to perform these inferences has become foundational in modern genomics, enabling deeper insights into disease association, [drug response](@entry_id:182654), and the intricacies of human history.

This article provides a thorough exploration of these essential techniques. In the "Principles and Mechanisms" chapter, we will dissect the statistical foundation that makes inference possible, from the concept of Linkage Disequilibrium to the Hidden Markov Models that serve as the engine for modern algorithms. Following this, the "Applications and Interdisciplinary Connections" chapter will demonstrate the transformative impact of these methods across diverse scientific domains, from powering large-scale [genome-wide association studies](@entry_id:172285) and enabling precision in clinical diagnostics to reconstructing ancient genomes. Finally, the "Hands-On Practices" section offers conceptual exercises to solidify your understanding of key calculations and quality control measures. We begin by establishing the fundamental concepts that distinguish genotypes from haplotypes and create the challenge that phasing aims to solve.

## Principles and Mechanisms

### Fundamental Concepts: Genotypes, Haplotypes, and Phase

In diploid organisms, the genetic information at any autosomal locus is carried on two [homologous chromosomes](@entry_id:145316). The specific variant of a gene or marker at a locus is termed an **allele**. For a biallelic Single Nucleotide Polymorphism (SNP), there are typically two alleles in the population, which can be encoded as $0$ (reference) and $1$ (alternate). The pair of alleles an individual possesses at a given locus constitutes their **genotype**. Standard genotyping technologies measure these alleles without distinguishing their parental origin. Consequently, a genotype is formally the unordered multiset of two alleles. For a biallelic locus, the possible genotypes are homozygous, $\{0,0\}$ or $\{1,1\}$, or heterozygous, $\{0,1\}$.

In contrast, a **haplotype** is the sequence of alleles situated along a single homologous chromosome. Across $L$ loci, a haplotype is an ordered vector of alleles, $\mathbf{h} = (h_1, h_2, \dots, h_L)$. An individual's complete diploid genetic makeup at these loci is therefore described by an [ordered pair](@entry_id:148349) of [haplotypes](@entry_id:177949), $(\mathbf{h}^{(1)}, \mathbf{h}^{(2)})$, one inherited from each parent. The assignment of alleles to their respective homologous chromosomes is known as the **genetic phase**.

The fundamental challenge of phasing arises from the nature of genotype data. While a homozygous genotype like $\{0,0\}$ unambiguously implies that both haplotypes carry the $0$ allele at that locus, a heterozygous genotype $\{0,1\}$ introduces uncertainty. The true phased state could be either $(0,1)$—with allele $0$ on the first haplotype and $1$ on the second—or $(1,0)$. These two possibilities are observationally equivalent from the unphased genotype data alone [@problem_id:4569495].

This ambiguity compounds across multiple loci. For an individual with $k$ heterozygous loci, there are two choices for assigning the alleles to the two [haplotypes](@entry_id:177949) at each of these $k$ sites. This results in $2^k$ possible ordered pairs of phased haplotypes. Since swapping the two entire [haplotypes](@entry_id:177949) $(\mathbf{h}^{(1)}, \mathbf{h}^{(2)}) \to (\mathbf{h}^{(2)}, \mathbf{h}^{(1)})$ does not change the biological state, there are $2^{k-1}$ distinct (unordered) haplotype pairs for $k \ge 1$. Resolving this exponential ambiguity is the primary goal of genotype phasing.

### The Basis of Statistical Phasing: Linkage Disequilibrium

While the phase of an individual's heterozygous sites is not directly observable from unphased genotypes, it can be inferred statistically using information from the broader population. The statistical foundation for this inference is **Linkage Disequilibrium (LD)**, the non-random association of alleles at different loci on the same chromosome.

In a population, if alleles at two loci were assorted independently, the frequency of a haplotype would simply be the product of the corresponding allele frequencies. For two loci with alleles $A/a$ and $B/b$, under linkage equilibrium, the frequency of the $AB$ haplotype would be $P_{AB} = p_A p_B$, where $p_A$ and $p_B$ are the frequencies of alleles $A$ and $B$, respectively. LD measures the deviation from this expectation. The most common measure is the disequilibrium coefficient, $D$:

$$ D = P_{AB} - p_A p_B $$

A non-zero $D$ indicates that alleles at the two loci are correlated. A positive $D$ means the $AB$ and $ab$ [haplotypes](@entry_id:177949) are more common than expected, while a negative $D$ implies the $Ab$ and $aB$ [haplotypes](@entry_id:177949) are overrepresented. The strength of this correlation, normalized for allele frequencies, is captured by the squared correlation coefficient, $r^2$:

$$ r^2 = \frac{D^2}{p_A(1-p_A)p_B(1-p_B)} $$

The value of $r^2$ ranges from $0$ (perfect linkage equilibrium) to $1$ (perfect LD, where only two of the four possible [haplotypes](@entry_id:177949) exist).

LD is the key that unlocks population-based phasing. Consider an individual who is a double heterozygote ($A/a$ at the first locus, $B/b$ at the second). Their true phase is either "coupling" ($AB$ on one chromosome, $ab$ on the other) or "repulsion" ($Ab$ and $aB$). If $D \ne 0$ in the population, these two configurations are not equally probable. For instance, if a population has $p_A = 0.3$, $p_B = 0.4$, and the observed haplotype frequency $P_{AB} = 0.18$, then $D = 0.18 - (0.3)(0.4) = 0.06$. The associated $r^2$ is approximately $0.071$. This positive value of $D$ signifies that the coupling haplotypes ($AB$ and $ab$) are more frequent than their repulsion counterparts. Consequently, a randomly chosen double heterozygote from this population is more likely to have the coupling phase $AB \parallel ab$. The conditional probability of this phase can be shown to be approximately $0.766$, significantly greater than the $0.5$ expected under linkage equilibrium. The magnitude of $r^2$ dictates the strength of this inference; as $r^2$ approaches $1$, the phasing of the double heterozygote becomes nearly certain [@problem_id:4569503].

### Population-Specific Nature of LD and Its Implications

Linkage disequilibrium patterns are not universal; they are a distinctive feature of a population's unique demographic history. The level of LD is shaped by a dynamic interplay between processes that create it and those that break it down.

Genetic drift, the random fluctuation of allele frequencies due to chance sampling in finite populations, is a primary force creating LD. The effect of drift is stronger in populations with a smaller **effective population size ($N_e$)**. Recombination, which shuffles alleles between [homologous chromosomes](@entry_id:145316) during meiosis, is the main force that erodes LD. For neutral loci separated by a recombination fraction $c$, the expected equilibrium level of LD is approximated by:

$$ E[r^2] \approx \frac{1}{1 + 4N_e c} $$

This relationship shows that populations with a smaller $N_e$ (e.g., historically isolated groups) will exhibit higher levels of LD and longer blocks of associated alleles for a given genetic distance. Conversely, large, historically diverse populations (large $N_e$) tend to have lower LD and shorter [haplotype blocks](@entry_id:166800) [@problem_id:4569498].

Furthermore, specific demographic events like recent population bottlenecks, founder events, or admixture (mixing of genetically distinct populations) can generate unique, long-range LD patterns that are [far from equilibrium](@entry_id:195475). For example, admixture can create statistical associations between loci that are physically very far apart, even on different chromosomes [@problem_id:4569498].

This population-specificity of LD has a critical practical implication: for population-based phasing and [imputation](@entry_id:270805) to be accurate, the **ancestry of the reference panel must be well-matched to the ancestry of the target samples**. Phasing algorithms model an individual's chromosomes as a mosaic of haplotypes from the reference panel. If the panel lacks the specific haplotype structures present in the target individual's population, the model will be forced to stitch together a poor-fitting mosaic, leading to a high rate of phasing errors [@problem_id:4569498] [@problem_id:4569453].

### Mechanisms of Population-Based Phasing and Imputation

The core principle of population-based methods is to leverage the LD structure, as captured in a large reference panel of known [haplotypes](@entry_id:177949), to infer phase and unobserved genotypes in a target sample.

**Genotype imputation** is the process of statistically inferring genotypes at loci that were not directly assayed in a study. The formal goal is to compute the posterior probability distribution of the unobserved genotypes, $G_u$, given the observed genotypes, $G_o$, and the reference panel of haplotypes, $H$. This is expressed as $p(G_u \mid G_o, H)$ [@problem_id:4569509]. By borrowing information from the densely genotyped reference panel, [imputation](@entry_id:270805) can dramatically increase the number of variants available for analysis, such as in a [genome-wide association study](@entry_id:176222) (GWAS).

#### The Hidden Markov Model (HMM) Engine

The workhorse for modern phasing and [imputation](@entry_id:270805) is a type of **Hidden Markov Model (HMM)**, most famously the Li-Stephens model. This model formalizes the idea that an individual's haplotype is a "mosaic" of segments copied from the haplotypes in the reference panel.

The components of this HMM are defined as follows [@problem_id:4569523] [@problem_id:4569456]:

*   **Hidden States**: The [hidden state](@entry_id:634361) at a marker locus $i$, denoted $Z_i$, is the index of the reference haplotype from the panel of size $K$ that is being "copied" by the target haplotype at that position. Thus, $Z_i \in \{1, \dots, K\}$.

*   **Transitions**: Transitions between hidden states from one marker to the next, $P(Z_i \mid Z_{i-1})$, model recombination events in the ancestral history of the target haplotype. The probability of a switch to a new template haplotype depends on the **genetic distance** between the markers. A **[genetic map](@entry_id:142019)**, $g(x)$, relates the physical position on a chromosome (in base pairs) to genetic distance (in **Morgans**), where one Morgan corresponds to an expected one crossover per meiosis. The transition probability is a function of this distance. For adjacent markers separated by genetic distance $r_i$, the probability of *staying* on the same reference haplotype template decays exponentially:
    $$ P(Z_i = \ell \mid Z_{i-1} = \ell) = \exp(-\rho r_i) $$
    Here, $\rho$ is an effective population [recombination rate](@entry_id:203271) parameter that scales the genetic distance. The complementary probability of *switching* to a new template, $1 - \exp(-\rho r_i)$, is distributed among the other $K-1$ haplotypes [@problem_id:4569523]. This exponential form arises from modeling ancestral recombination events as a Poisson process along the chromosome [@problem_id:4569493] [@problem_id:4569456].

*   **Emissions**: Emission probabilities, $P(\text{Observed Allele} \mid Z_i = k)$, model the relationship between the observed allele on the target haplotype and the allele on the chosen template haplotype $k$. To account for historical mutations or modern genotyping errors that can cause a mismatch, the model uses a small error probability $\varepsilon$. If the allele on the template haplotype $h_k(i)$ matches the observed allele, the emission probability is high ($1-\varepsilon$); if they differ, it is low ($\varepsilon$) [@problem_id:4569523]. The theoretical value of this parameter is related to the mutation rate and effective population size [@problem_id:4569456].

#### Methodological Approaches: Joint Imputation vs. Pre-phasing

In practice, since both the phase of the observed genotypes and the identity of the missing genotypes are unknown, algorithms must handle both simultaneously. Two main strategies exist [@problem_id:4569509]:

1.  **Joint Imputation**: This is the fully probabilistic approach. It considers all possible phasings ($Z$) of the observed genotypes, weighted by their posterior probabilities. The final imputed genotypes are obtained by marginalizing over this phase uncertainty:
    $$ p(G_u \mid G_o, H) = \sum_Z p(G_u \mid Z, H) p(Z \mid G_o, H) $$
    This method properly propagates uncertainty but can be computationally intensive.

2.  **Pre-phasing**: This is a computationally efficient two-step approximation. First, the most probable [haplotype phasing](@entry_id:274867) for the target sample, $\hat{Z}$, is estimated. Second, this single estimated phase is treated as if it were the true phase, and [imputation](@entry_id:270805) is performed conditioning on $\hat{Z}$. This decouples the problem, but by collapsing the probability distribution over phases to a single [point estimate](@entry_id:176325), it can lead to an underestimation of imputation uncertainty, especially for rare variants where phase is less certain [@problem_id:4569509].

### Read-Backed Phasing: An Orthogonal Approach

An entirely different class of methods, known as **read-backed phasing**, infers phase using direct physical evidence from sequencing reads within a single individual, rather than statistical evidence from a population reference panel. When a single sequencing read or a pair of reads from the same DNA fragment spans two or more heterozygous sites, the alleles are physically linked, providing a direct constraint on the local phase [@problem_id:4569453].

The key distinction lies in the source of information and, consequently, the sources of uncertainty. Read-backed phasing is subject to uncertainties at the molecular level: sequencing errors, read coverage depth, and the physical length of sequenced fragments. In contrast, population-based phasing is subject to uncertainties at the population level: the strength of LD, the representativeness of the reference panel, and the accuracy of the assumed recombination model [@problem_id:4569552].

Various sequencing technologies provide different types of read-based evidence [@problem_id:4569453]:

*   **Paired-end short reads**: The most common data type. They provide high-confidence phase information for variants that fall within the DNA insert size (typically a few hundred base pairs), creating small, accurate "phase blocks". However, they cannot bridge the gaps between these blocks.

*   **Long reads** (e.g., PacBio, Oxford Nanopore): These reads can be tens of thousands of base pairs long, allowing them to span many heterozygous sites and directly resolve phase over long distances.

*   **Proximity-ligation data (Hi-C)**: This method captures physical interactions between distant genomic regions that are close in 3D nuclear space. As regions of the same chromosome are more likely to interact, Hi-C read pairs can provide sparse but very long-range phasing information, linking phase blocks that are megabases apart.

*   **Strand-seq**: This [single-cell sequencing](@entry_id:198847) method preserves the identity of the template DNA strand (Watson or Crick) that was used for replication. Since each homolog is segregated to daughter cells as a set of consistent template strands, reads from a single cell can be partitioned by strand identity, effectively phasing all heterozygous variants across an entire chromosome.

In practice, the most powerful strategies often combine approaches. Population-based methods provide a chromosome-scale scaffold, while read-backed evidence provides high-confidence local phasing and is essential for positioning rare and private variants that are absent from reference panels [@problem_id:4569453].

### Evaluating Phasing and Imputation Accuracy

Robust evaluation metrics are essential for quality control and for comparing different methods.

#### Phasing Accuracy: Switch Error Rate

The primary metric for phasing accuracy is the **switch error rate**. It is defined as the fraction of adjacent heterozygous sites where the inferred relative phase is incorrect with respect to a "gold standard" truth. This metric is independent of the arbitrary labels assigned to the two [haplotypes](@entry_id:177949) (paternal/maternal or 1/2) because it only assesses the correctness of the transitions between loci [@problem_id:4569508].

To calculate the switch error rate, a ground truth phasing is required. This is often obtained from:
*   **Trio data**: In a family trio (two parents and a child), the child's true [haplotypes](@entry_id:177949) can often be determined unambiguously by applying the laws of Mendelian inheritance. For example, if a child is heterozygous ($0/1$) and one parent is homozygous ($0/0$), the child must have inherited the $0$ allele from that parent, determining the parental origin of both alleles.
*   **Long reads**: Spanning reads provide direct physical evidence of phase. The phase supported by the majority of reads is taken as the truth.

For example, given a predicted phasing and a trio-derived truth for a child, one identifies all pairs of adjacent heterozygous SNPs. For each pair, one compares the predicted relative phase (are the alternate alleles on the same or different haplotypes?) with the true relative phase. The switch error rate is the number of incorrectly predicted pairs divided by the total number of such pairs [@problem_id:4569508].

#### Imputation Accuracy: Imputation $R^2$

For [genotype imputation](@entry_id:163993), the most widely used quality metric is the imputation **$R^2$** (or $r^2$). For a given SNP, let the true genotype dosage (minor allele count) be $G \in \{0,1,2\}$ and the imputed dosage, representing the [posterior mean](@entry_id:173826) expectation of $G$, be $\hat{d}$. Assuming the population is in Hardy-Weinberg Equilibrium with minor [allele frequency](@entry_id:146872) $p$, the variance of the true genotype is $\mathrm{Var}(G) = 2p(1-p)$. The [imputation](@entry_id:270805) $R^2$ is defined as:

$$ R^2 = \frac{\mathrm{Var}(\hat{d})}{2p(1-p)} = \frac{\mathrm{Var}(\hat{d})}{\mathrm{Var}(G)} $$

This metric has a powerful and intuitive interpretation. If the imputation algorithm is well-calibrated (i.e., $\hat{d} = \mathbb{E}[G \mid \text{data}]$), then the $R^2$ value is precisely equal to the **squared Pearson correlation coefficient** between the true and imputed dosages, $\mathrm{Corr}(G, \hat{d})^2$ [@problem_id:4569460].

Thus, $R^2$ represents the proportion of the variance in the true genotypes that is explained by the imputed dosages. Its value ranges from $0$ to $1$. An $R^2$ of $1$ signifies perfect imputation, where the imputed dosage perfectly predicts the true genotype, meaning the [conditional variance](@entry_id:183803) of the genotype given the data, $\mathrm{Var}(G \mid \text{data})$, is zero. An $R^2$ near $0$ indicates that the imputation has failed and provides no information beyond the [population mean](@entry_id:175446). In practice, imputed SNPs with a low $R^2$ (e.g., $\lt 0.3$ or $\lt 0.8$, depending on the application) are typically excluded from downstream analyses to ensure data quality [@problem_id:4569460].