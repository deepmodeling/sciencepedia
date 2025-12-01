## Introduction
The analysis of cancer genomes from bulk tumor sequencing presents a fundamental challenge: the data is an aggregate signal from a mixture of malignant and healthy cells. To extract meaningful biological and clinical insights, we must first mathematically deconvolve this mixture. This process, centered on estimating tumor purity (the fraction of tumor-derived DNA) and [ploidy](@entry_id:140594) (the average genomic copy number of tumor cells), is the cornerstone of modern quantitative cancer genomics. It transforms noisy, relative measurements into absolute, interpretable quantities, addressing the critical knowledge gap between raw sequencing output and the true state of the cancer genome.

This article provides a comprehensive guide to the theory and practice of tumor purity and [ploidy](@entry_id:140594) estimation. In **Principles and Mechanisms**, we will dissect the core mathematical models that relate observed data, such as read depth and allele frequencies, to the underlying parameters of the tumor-normal mixture. Next, **Applications and Interdisciplinary Connections** will demonstrate how these robust estimates are indispensable for a range of downstream analyses, from accurate biomarker calculation in precision oncology to integration with histopathology and single-cell data. Finally, **Hands-On Practices** will solidify your understanding through guided problems that apply these theoretical concepts to practical scenarios encountered in genomic research.

## Principles and Mechanisms

The analysis of bulk tumor sequencing data is fundamentally a problem of deconvolution. The observed data—whether from whole-genome, whole-exome, or targeted sequencing—represent an aggregate signal from a heterogeneous population of cells. This population typically includes not only malignant tumor cells but also various non-malignant cell types, such as immune cells and stromal cells, collectively referred to as the normal cell contaminant. To extract biologically and clinically meaningful information about the tumor, we must first establish a rigorous mathematical framework that models this mixture. This chapter delineates the core principles and quantitative mechanisms that underpin the estimation of tumor purity and ploidy.

### Foundational Quantities and Mixture Models

The quantitative analysis of tumor genomes requires a precise vocabulary. Several key parameters describe the composition of the sample and the state of the tumor genome. Understanding their definitions and interrelationships is the first step toward building a coherent model.

**Tumor Cellularity and Purity**: The most fundamental descriptor of a bulk tumor sample is its composition. **Tumor [cellularity](@entry_id:153341)**, denoted by $c$, is defined as the fraction of cells in the sample that are malignant. For instance, in a sample with 70 tumor cells and 30 normal cells, the cellularity is $c=0.7$. However, high-throughput sequencing assays measure DNA, not cells. If tumor cells and normal cells have different DNA content, the proportion of sequencing reads derived from the tumor may not equal the [cellularity](@entry_id:153341). This DNA-based proportion is called **tumor purity**, denoted by $p$.

Normal somatic cells are diploid and contain a baseline amount of DNA, which we can normalize to 2 units per cell. Tumor cells, due to widespread aneuploidy, often have a different average DNA content. We define the **average tumor [ploidy](@entry_id:140594)**, $\pi$, as the average total copy number of the tumor genome, relative to a [haploid](@entry_id:261075) genome. A diploid normal cell has a [ploidy](@entry_id:140594) of 2. If a tumor genome has, on average, 3 copies of each chromosome, its ploidy is $\pi=3$.

The relationship between [cellularity](@entry_id:153341) $c$ and purity $p$ arises from a simple mass-balance argument. The total DNA content in a sample is proportional to the sum of DNA from each cell population. The contribution from tumor cells is proportional to $c \cdot \pi$, and the contribution from normal cells is proportional to $(1-c) \cdot 2$. Tumor purity $p$, being the fraction of DNA from tumor cells, is therefore given by:
$$
p = \frac{c \cdot \pi}{c \cdot \pi + (1-c) \cdot 2}
$$
From this equation [@problem_id:4616081], it is evident that tumor purity $p$ is equal to tumor [cellularity](@entry_id:153341) $c$ if and only if the average tumor ploidy $\pi$ is 2. If the tumor is aneuploid ($\pi \neq 2$), $p$ and $c$ will diverge. For example, in a sample with $c=0.5$ where the tumor is triploid ($\pi=3$), the purity is $p = \frac{0.5 \cdot 3}{0.5 \cdot 3 + 0.5 \cdot 2} = \frac{1.5}{2.5} = 0.6$. Despite making up half the cells, the tumor cells contribute 60% of the DNA.

**Genome-wide vs. Locus-Specific Copy Number**: The average tumor ploidy $\pi$ is a genome-wide summary statistic. It is formally defined as the length-weighted average of the local, segment-specific total copy numbers across the entire tumor genome. If the genome is partitioned into $n$ segments, where segment $i$ has length $L_i$ and a clonal integer total copy number $C_i$ in tumor cells, the average ploidy is:
$$
\pi = \frac{\sum_{i=1}^{n} L_i C_i}{\sum_{i=1}^{n} L_i}
$$
Because it is a weighted average of integers, $\pi$ is not necessarily an integer itself; it is generally a rational number [@problem_id:4616130]. This average [ploidy](@entry_id:140594) $\pi$ is distinct from the **locus-specific total copy number** $C$, which describes the integer number of copies of a particular genomic region within a tumor cell. This can be further broken down into **allele-specific copy numbers** $(a,b)$, where $a$ and $b$ are the integer copy counts of the two parental alleles (e.g., maternal and paternal), such that $C = a+b$.

**Variant-Specific Quantities**: When analyzing somatic mutations, such as single-nucleotide variants (SNVs), we need additional parameters. The **cancer cell fraction** (CCF), denoted by $f$, is the fraction of *tumor cells* that carry a specific mutation. A mutation present in all tumor cells is clonal ($f=1$), while one present in only a subset is subclonal ($0 \lt f \lt 1$). Within a tumor cell that harbors a mutation, the **mutation multiplicity**, $m$, is the number of chromosomal copies that carry the variant allele. For an SNV at a locus with total tumor copy number $C$, the multiplicity must satisfy $0 \le m \le C$. These distinctions are critical; tumor purity $p$ is a global property of the sample, whereas CCF $f$ is a property of a specific variant within the tumor population [@problem_id:4616143].

### The Two Pillars of Copy Number Analysis

The inference of tumor purity, ploidy, and copy number alterations rests on two main types of signals derived from sequencing or microarray data: a measure of total copy number and a measure of allele-specific balance.

#### Modeling Total Copy Number: The Log R Ratio

The total read depth in a genomic segment is, on average, proportional to the total number of DNA copies of that segment present in the sample. We can use this principle to quantify copy number. The observed signal is first normalized to account for library size and other global effects. A common resulting metric is the **Log R Ratio** (LRR or L), which is the base-2 logarithm of the ratio of the observed signal in a segment to the expected signal for a normal, diploid region.

The expected total copy number in the bulk sample, $\langle CN \rangle$, is the purity-weighted average of the copy numbers in the tumor ($C$) and normal ($2$) populations:
$$
\langle CN \rangle = p \cdot C + (1-p) \cdot 2
$$
The copy ratio $R$ is this average copy number normalized to the diploid baseline of 2. The LRR, $L$, is the log-2 transform of $R$:
$$
L = \log_2(R) = \log_2\left(\frac{\langle CN \rangle}{2}\right) = \log_2\left(\frac{pC + (1-p)2}{2}\right)
$$
This can be rearranged to a more intuitive form:
$$
L = \log_2\left(\frac{p(C-2) + 2}{2}\right)
$$
This fundamental equation [@problem_id:4616085] shows that the LRR signal depends on both the underlying biological reality (the tumor copy number $C$) and the sample composition (the purity $p$).

#### Modeling Allele-Specific Copy Number: The B-Allele Frequency

At genomic loci where an individual is heterozygous in their germline (e.g., at many single-nucleotide polymorphisms, or SNPs), the two parental alleles (A and B) are present in a 1:1 ratio in normal cells. Somatic copy number alterations in tumor cells can disrupt this balance. This is quantified using the **B-Allele Frequency** (BAF), defined as the fraction of sequencing reads at a heterozygous locus that support one of the alleles (conventionally, the 'B' allele).

In a mixed sample, the expected BAF is the ratio of the total number of B-allele copies to the total number of all copies (A and B). Let the allele-specific copy numbers in the tumor be $(a,b)$. Normal cells are $(1,1)$. The expected BAF is then:
$$
\mathrm{BAF} = \frac{\text{Total B-allele copies}}{\text{Total A+B copies}} = \frac{p \cdot b + (1-p) \cdot 1}{p \cdot (a+b) + (1-p) \cdot (1+1)} = \frac{p(b-1)+1}{p(a+b-2)+2}
$$
This signal is exquisitely sensitive to allele-specific changes. A particularly informative event is **Loss of Heterozygosity (LOH)**, where one of the two parental alleles is lost in the tumor cells. By convention, we can analyze the **minor-allele BAF** (mBAF), which is always $\le 0.5$. Consider a germline heterozygous locus where the tumor undergoes LOH, resulting in the loss of the B-allele, so the tumor state is $(a_t, 0)$. The expected mBAF becomes:
$$
\mathrm{E}[\mathrm{mBAF}] = \frac{p(0-1)+1}{p(a_t+0-2)+2} = \frac{1-p}{p(a_t-2)+2}
$$
The position of the mBAF cluster depends directly on the purity $p$ and the copy number of the remaining allele, $a_t$. This provides a powerful tool for both identifying specific CNA events and constraining purity [@problem_id:4616090]. For example:
-   **Deletion-mediated LOH (1,0):** $a_t=1$. The mBAF is $\frac{1-p}{2-p}$.
-   **Copy-neutral LOH (2,0):** $a_t=2$. The mBAF is $\frac{1-p}{2}$.
-   **Amplification-mediated LOH (3,0):** $a_t=3$. The mBAF is $\frac{1-p}{2+p}$.

For a sample with purity $p=0.6$, these three distinct LOH events would produce mBAF clusters at approximately 0.286, 0.200, and 0.154, respectively. The observation of such clusters in the data provides strong evidence for both the LOH event and the sample's purity.

### Integrating Signals for Inference

The models for LRR, BAF, and VAF provide a complete framework for interpreting sequencing data. By combining these signals, we can infer the underlying parameters of the tumor.

#### The Unified VAF Model and Its Implications

The expected Variant Allele Fraction (VAF) for a somatic SNV can be modeled using the same mixture principles. The numerator is the contribution of mutant alleles, and the denominator is the total contribution of all alleles at that locus. The mutant alleles come only from the fraction of tumor cells harboring the mutation ($p \cdot f$), each contributing $m$ copies. The total alleles come from all tumor cells ($p \cdot C$) and all normal cells ($(1-p) \cdot 2$).
Thus, the expected VAF, $V$, is given by [@problem_id:4616081]:
$$
V = \frac{p \cdot f \cdot m}{p \cdot C + (1-p) \cdot 2}
$$
This equation integrates all the key parameters. It highlights that the observed VAF is modulated not only by the fraction of cells carrying the mutation ($f$) and the purity ($p$), but also by the local copy number context ($C$) and the mutation multiplicity ($m$).

This model allows us to disentangle purity ($p$) from cancer cell fraction ($f$). For instance [@problem_id:4616143], consider a sample with purity $p=0.7$. At a locus with a clonal single-copy gain, the tumor copy number is $C=3$. A subclonal SNV on a single copy ($m=1$) is observed with a VAF of $V=0.12$. To find the fraction of tumor cells with this SNV, we can invert the VAF equation:
$$
f = \frac{V (pC + (1-p)2)}{pm} = \frac{0.12 (0.7 \cdot 3 + (1-0.7) \cdot 2)}{0.7 \cdot 1} = \frac{0.12 (2.1 + 0.6)}{0.7} = \frac{0.324}{0.7} \approx 0.46
$$
This calculation reveals that while 70% of the cells in the sample are cancerous, only 46% of those cancer cells carry this particular SNV. This demonstrates the critical distinction between the global sample property of purity and the variant-specific property of cancer cell fraction.

#### Statistical Inference Framework

These deterministic models form the basis for [statistical inference](@entry_id:172747). Given observed read counts for a set of variants, we can construct a [likelihood function](@entry_id:141927) for the unknown parameters like $p$ and $f$. Assuming the number of variant-supporting reads $k_i$ out of a total depth $n_i$ at locus $i$ follows a [binomial distribution](@entry_id:141181), the likelihood for parameters $p$ and $f$ is:
$$
\mathcal{L}(p, f \mid \{(k_i, n_i)\}) = \prod_i \binom{n_i}{k_i} V^{k_i} (1-V)^{n_i-k_i}
$$
where $V$ is the expected VAF, which is a function of $p$, $f$, and other parameters like $C$ and $m$. By finding the parameter values that maximize this likelihood (Maximum Likelihood Estimation, or MLE), we can obtain estimates for purity and [ploidy](@entry_id:140594).

In a simplified case with multiple clonal ($f=1$) SNVs in a region of known tumor copy number $C=m$ and multiplicity $c=1$, the MLE for purity $p$ can be derived analytically [@problem_id:4616082]. The expected VAF simplifies to $V = \frac{p}{p(m-2)+2}$. The MLE for $p$ that maximizes the [joint likelihood](@entry_id:750952) across all SNVs is:
$$
\hat{p} = \frac{2 \sum k_i}{\sum n_i + (2-m) \sum k_i}
$$
This demonstrates how, under a specified model, observed read counts can be directly translated into an estimate of a core biological parameter.

### The Challenge of Identifiability and Its Resolution

A central challenge in this field is **[identifiability](@entry_id:194150)**: can we find a unique solution for purity and [ploidy](@entry_id:140594) given the data? Often, multiple combinations of these parameters can explain the observed data almost equally well, leading to ambiguity.

#### The Purity-Ploidy Trade-off

If we only consider total copy number data (the LRR), a fundamental ambiguity arises. A solution with low purity and a highly aneuploid genome (high ploidy) can produce nearly the same LRR profile as a solution with high purity and a less aneuploid genome (low [ploidy](@entry_id:140594)) [@problem_id:4616145]. This can be seen from the LRR model: the signal is driven by the term $p(C-2)$. An increase in $C$ can be offset by a decrease in $p$ to keep the product, and thus the LRR, roughly constant. This trade-off is most pronounced in tumors that lack significant clonal allelic imbalance, as the BAF data remains centered at 0.5 and offers no additional constraint. This is common in genomes that have undergone whole-genome doubling, resulting in many regions with balanced even-integer copy numbers (e.g., 4 copies, with 2 of each allele).

#### Breaking the Ambiguity with Allele-Specific Data

The key to resolving this ambiguity lies in the BAF signal. Unlike the LRR, the BAF's response to changes in allele-specific copy number is non-linear and provides an independent source of constraint.

Consider two possible tumor states for a segment: a balanced state $(2,2)$ and an imbalanced state $(3,1)$. Both have the same total tumor copy number $C=4$. Let's examine the expected LRR and BAF for these two states [@problem_id:4616107]:
-   **State (2,2):** $L = \log_2(\frac{p(4-2)+2}{2}) = \log_2(p+1)$. The BAF is $\frac{p(2-1)+1}{p(4-2)+2} = \frac{p+1}{2(p+1)} = 0.5$.
-   **State (3,1):** $L = \log_2(\frac{p(4-2)+2}{2}) = \log_2(p+1)$. The BAF is $\frac{p(1-1)+1}{p(4-2)+2} = \frac{1}{2(p+1)}$.

The LRR signal is identical for both states. An analysis based on LRR alone could never distinguish them. However, their BAF signatures are distinct for any purity $p>0$. The balanced state produces a BAF of 0.5, while the imbalanced state produces a BAF strictly less than 0.5. The observation of a BAF cluster away from 0.5 definitively rules out the balanced state and simultaneously constrains the value of $p$. The presence of multiple segments with different types of clonal allelic imbalance (e.g., LOH, odd copy numbers like $C=3$ or $C=5$) provides powerful, interlocking constraints that can often pinpoint a unique purity-ploidy solution [@problem_id:4616145].

This process can be formalized by using the observed LRR and BAF values to define a [feasible region](@entry_id:136622) for the unknown integer copy numbers $(a,b)$. Given a fixed purity $p$ and measured intervals for $L$ and BAF, we can derive inequalities that any valid integer pair $(a,b)$ must satisfy, effectively using the data to search for the correct solution [@problem_id:4616105].

### Advanced Topics and Practical Considerations

Real-world genomic data present additional complexities that can confound analysis if not properly handled.

#### Confounding Effect of Genome Mappability

Large portions of the human genome consist of repetitive sequences. During [sequence alignment](@entry_id:145635), reads originating from these regions may not be uniquely mapped to a single location. This leads to a systematic suppression of read counts in low-mappability regions. This effect is captured by a **mappability factor** $\mu_j \in (0,1]$ for each segment $j$. A simple tumor-only LRR calculation is biased by this factor, as the expected LRR becomes $\log_2(\mu_j) + \log_2(\frac{F_j}{2})$, where $F_j$ is the average copy number in the mixture [@problem_id:4616125].

This confounding effect can be corrected by using a matched normal sample. The read depth in the same segment of the normal sample is also affected by the same mappability factor $\mu_j$. By constructing a ratio of normalized tumor depth to normalized [normal depth](@entry_id:265980), the $\mu_j$ term cancels out, yielding a corrected log-ratio statistic $L^{*}_{j}$ that accurately reflects the true copy number change:
$$
L^{*}_{j} = \log_{2}\left(\frac{(T_{j}/s_{j})/\bar{d}^{S}_{t}}{(N_{j}/s_{j})/\bar{d}^{S}_{n}}\right)
$$
Here, $T_j$ and $N_j$ are the tumor and normal read counts in segment $j$ of length $s_j$, and $\bar{d}^{S}_{t}$ and $\bar{d}^{S}_{n}$ are the baseline read densities for the tumor and normal samples, respectively. This highlights the critical value of a high-quality matched normal control in copy number analysis.

#### Confounding Effect of Sample Contamination

Another practical challenge is **tumor-in-normal (TiN) contamination**, where the matched normal sample itself is contaminated with a fraction $\eta$ of tumor cells. This can occur due to field cancerization or inadvertent sampling of tumor-adjacent tissue. This contamination biases the baseline, particularly for BAF analysis. The BAF of the contaminated normal, $b_N$, will be shifted from the expected 0.5 towards the tumor's BAF at that locus.

If one has estimates of the tumor sample purity $p$ and the TiN contamination fraction $\eta$, it is possible to correct for this effect. By modeling the BAF of the tumor sample ($b_T$) and the contaminated normal sample ($b_N$) as two independent mixture equations, one can solve for the true, underlying tumor B-allele fraction $p_B = c_B/c$ [@problem_id:4616124]. The resulting expression eliminates the confounding effect of the unknown germline allelic bias and corrects for the contamination:
$$
p_{B} = \frac{b_{N}(1-p)(c\eta + 2(1-\eta)) - b_{T}(1-\eta)(cp + 2(1-p))}{c(\eta - p)}
$$
This illustrates the sophistication required to handle imperfections in clinical samples and underscores the importance of modeling all components of the system accurately.

In summary, the estimation of tumor purity and [ploidy](@entry_id:140594) is a model-based deconvolution problem. By establishing rigorous mathematical models for the signals generated by tumor-normal mixtures and leveraging the complementary information from total and allele-specific copy number data, it is possible to overcome significant identifiability challenges and correct for practical confounders, ultimately yielding a robust characterization of the cancer genome.