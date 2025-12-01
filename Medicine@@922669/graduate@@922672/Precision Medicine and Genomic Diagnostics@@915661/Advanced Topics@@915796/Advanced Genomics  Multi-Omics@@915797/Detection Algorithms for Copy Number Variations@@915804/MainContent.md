## Introduction
Copy Number Variations (CNVs)—deletions or duplications of DNA segments—are a fundamental source of genomic diversity and a major driver of human disease, from congenital disorders to cancer. The ability to accurately identify these structural changes is therefore a cornerstone of modern genomic diagnostics and precision medicine. However, detecting CNVs presents a significant challenge: the raw data from high-throughput sequencing and [microarray](@entry_id:270888) technologies are inherently noisy, replete with technical biases that can obscure the true biological signal. The central problem, which this article addresses, is how to robustly process this data to distinguish genuine gains and losses from experimental artifacts.

This article provides a comprehensive guide to the algorithms and principles that power modern CNV detection. The journey begins in the **Principles and Mechanisms** chapter, where we will deconstruct the process of transforming raw DNA into a clean, quantifiable signal. You will learn the statistical models that describe genomic data, the critical steps for correcting systematic biases, and the core algorithms used to segment the genome into regions of distinct copy number. Building on this foundation, the **Applications and Interdisciplinary Connections** chapter will explore the real-world impact of these methods in clinical diagnostics, oncology, and pharmacogenomics, demonstrating how CNV analysis informs patient care. Finally, the **Hands-On Practices** section provides an opportunity to apply these concepts through targeted computational exercises, bridging the gap between theory and practical implementation.

## Principles and Mechanisms

The detection of copy number variations (CNVs) from high-throughput sequencing or [microarray](@entry_id:270888) data is a quintessential problem in statistical signal processing, grounded in the molecular biology of the genome. Successful detection relies on a deep understanding of how biological reality—the integer number of copies of a DNA segment—is transformed into quantitative, but noisy, experimental data. This chapter elucidates the core principles and mechanisms that underpin modern CNV detection algorithms, from the generation of primary signals to their statistical interpretation. We will deconstruct the process into three main stages: understanding the primary data signals, correcting for inherent technical biases, and finally, identifying significant changes that correspond to true biological variation.

### From DNA to Data: Modeling Genomic Signals

At the heart of many CNV detection methods is a simple yet powerful premise: the quantity of sequencing data generated from a specific genomic region is, all else being equal, proportional to the number of copies of that region present in the original biological sample. This principle applies to both whole-genome sequencing (WGS) and targeted sequencing approaches like [whole-exome sequencing](@entry_id:141959) (WES), as well as to the signal intensities derived from microarray-based technologies.

#### The Read-Depth Signal and its Statistical Formulation

For sequencing-based methods, the genome is conceptually partitioned into a series of non-overlapping windows, or **bins**. The primary observable is the number of sequencing reads, $X_i$, that map to each bin $i$. Under an idealized model of random [shotgun sequencing](@entry_id:138531), where DNA fragments are sampled uniformly from across the genome, the count $X_i$ can be modeled as a **Poisson random variable**. The Poisson distribution is appropriate because it describes the number of events (read starts) occurring in a fixed interval (the bin) when these events happen with a known constant mean rate and independently of the time since the last event. Thus, we write:

$X_i \sim \text{Poisson}(\lambda_i)$

Here, $\lambda_i$ is the rate parameter, representing the expected number of reads in bin $i$. This parameter is not a single value but a composite that captures both the biological signal of interest and several layers of technical nuisance factors. A comprehensive model for this rate parameter can be expressed as a product of these effects [@problem_id:4331598]:

$\lambda_i = S \cdot c_i \cdot w_i \cdot m_i \cdot h(g_i)$

Let us dissect each component of this model:
-   $c_i$ is the **relative copy number factor** of the DNA in bin $i$. This is the biological signal we aim to measure. For a normal diploid region, $c_i$ is defined as $1$. A [hemizygous](@entry_id:138359) deletion would have $c_i = 0.5$, a duplication to three copies would have $c_i=1.5$, and so on. The absolute copy number is $c_i \cdot 2$.
-   $S$ is a **sample-specific normalization constant** that accounts for the overall [sequencing depth](@entry_id:178191) or library size. It scales the rates across all bins so that their sum reflects the total number of reads in the experiment.
-   $w_i$ is the **width of the bin** in base pairs. A wider bin naturally accumulates more reads, and this term accounts for that linear scaling.
-   $m_i$ is the **mappability** of the bin, a value between $0$ and $1$. It represents the fraction of the bin where a read can be uniquely and confidently mapped. Regions rich in repetitive elements have low mappability, which systematically suppresses the number of uniquely mapped reads, independent of true copy number.
-   $h(g_i)$ is a function representing the **sequence-context bias**, most notably **GC content bias**. The efficiency of PCR amplification and sequencing chemistries can be sensitive to the local guanine-cytosine (GC) content of DNA fragments. This creates a systematic, [non-linear distortion](@entry_id:260858) where regions with very high or very low GC content are often under-represented in the final sequencing data.

This model clarifies the central challenge: to estimate $c_i$, we must first account for and remove the confounding effects of $S$, $m_i$, and $h(g_i)$.

### Integrating Multi-modal Genomic Evidence

While read depth is the foundational signal, its interpretation can be ambiguous. True biological CNVs leave a coordinated footprint across multiple types of genomic data. State-of-the-art algorithms leverage this multi-modal evidence to increase both the sensitivity and specificity of their calls, reliably distinguishing genuine biological events from technical artifacts.

#### Log R Ratio (LRR) and B-Allele Frequency (BAF)

To facilitate comparison across samples and genomic regions, raw read counts are typically transformed into a **log ratio**. This is calculated as the logarithm (usually base 2) of the observed, normalized read count divided by the expected read count in a diploid region. A positive log ratio indicates a gain in copy number, while a negative log ratio indicates a loss.

This concept is directly analogous to the signals produced by Single Nucleotide Polymorphism (SNP) arrays. These arrays provide two key data streams for each SNP locus $l$:

1.  **Log R Ratio (LRR)**: This measures the total signal intensity from both alleles at locus $l$, normalized against a reference. It is conceptually identical to the [read-depth](@entry_id:178601) log ratio, and its expectation is directly related to the absolute copy number $c_l$: $\mathbb{E}[\mathrm{LRR}_l] \approx \log_2(c_l/2)$. For a diploid region ($c_l=2$), LRR fluctuates around $0$. For a deletion ($c_l=1$), it shifts to $\log_2(1/2) = -1$, and for a single-copy gain ($c_l=3$), it shifts to $\log_2(3/2) \approx 0.58$. [@problem_id:4331610]

2.  **B-Allele Frequency (BAF)**: This quantifies the allelic imbalance at a heterozygous locus. It is the fraction of the total signal contributed by the 'B' allele (where 'A' and 'B' are the two alleles for the SNP). In sequencing data, this corresponds to the fraction of reads covering a heterozygous SNP that support the non-reference allele. The BAF provides powerful, independent information about the integer copy number and allelic composition [@problem_id:4331531]:
    -   **Diploid (CN=2)**: At a heterozygous locus (genotype AB), the BAF is expected to be $0.5$.
    -   **Hemizygous Deletion (CN=1)**: The heterozygous locus is lost, leaving only a single allele (genotype A or B). This results in a **[loss of heterozygosity](@entry_id:184588) (LOH)**, and the BAF collapses to $0$ or $1$.
    -   **Single-Copy Gain (CN=3)**: A heterozygous locus AB is duplicated to AAB or ABB. The corresponding BAF values are $1/3$ and $2/3$, respectively.
    -   **Copy-Neutral LOH (CN=2)**: This occurs when a region becomes [homozygous](@entry_id:265358) (e.g., genotype AA or BB) without a change in total copy number. The LRR remains near $0$, but the BAF at formerly heterozygous sites collapses to $0$ or $1$.

The joint analysis of LRR and BAF is extremely powerful. For example, a region with BAF values of $0$ and $1$ could represent either a [hemizygous](@entry_id:138359) deletion (CN=1) or a copy-neutral LOH (CN=2). LRR resolves this ambiguity: a negative LRR value confirms the deletion, while an LRR near zero confirms copy-neutral LOH. [@problem_id:4331610]

#### Read-Pair and Split-Read Evidence

In [paired-end sequencing](@entry_id:272784), fragments of a known approximate size are sequenced from both ends. The resulting read pairs are expected to map to the [reference genome](@entry_id:269221) in a specific orientation (e.g., forward-reverse) and at a predictable distance from each other. Structural variations, including CNVs and balanced rearrangements, can disrupt this expected configuration.

-   **Discordant Read Pairs**: Pairs that map in an incorrect orientation (e.g., reverse-forward, suggesting an inversion) or at an anomalous distance (too large, suggesting a deletion of the intervening sequence; too small, suggesting an insertion) are called discordant.
-   **Split Reads**: A single long read may span a [structural variant](@entry_id:164220)'s breakpoint. When aligned to the [reference genome](@entry_id:269221), this read will be "split" into two separate alignments, precisely pinpointing the junction of the rearrangement.

This evidence is invaluable for identifying the exact breakpoints of CNVs and for detecting **balanced [structural variants](@entry_id:270335)**, such as inversions or translocations. These variants are copy-neutral—they rearrange DNA without changing its quantity—and are therefore invisible to [read-depth](@entry_id:178601) or LRR analysis. However, they generate strong discordant-pair and split-read signals, allowing them to be distinguished from true CNVs. [@problem_id:4331531]

The power of integrated analysis is evident when distinguishing a copy number gain from an artifact. A true biological duplication will present concordant evidence: a positive log ratio, BAF values clustering near $1/3$ and $2/3$, and often split-read or discordant-pair evidence at its boundaries. In contrast, a technical artifact that spuriously increases read depth in a region will show a positive log ratio but will lack the corresponding BAF shifts and breakpoint evidence. [@problem_id:4331512]

### Normalization and Bias Correction

Raw genomic data are replete with technical biases that must be corrected before any meaningful biological interpretation is possible. The goal of normalization is to remove these systematic, non-biological sources of variation, producing a clean signal where the remaining variance is primarily driven by true copy number differences.

#### A Principled Preprocessing Pipeline

A robust pipeline for preparing [read-depth](@entry_id:178601) data for CNV analysis involves several critical steps, each designed to mitigate a specific form of bias [@problem_id:4331543]:

1.  **Alignment and Quality Filtering**: Reads are first aligned to a reference genome. High-quality aligners provide a **[mapping quality](@entry_id:170584) (MAPQ)** score for each read, which is a Phred-scaled probability of mapping error. Reads with low MAPQ scores (e.g., below 20) are typically filtered out, as their placement is ambiguous and they contribute more noise than signal. This is especially important in regions with low mappability.

2.  **PCR Duplicate Removal**: During library preparation, PCR is used to amplify the DNA. This process can create multiple identical copies of a single original fragment. Counting these **PCR duplicates** as independent observations would falsely inflate the read count and introduce significant variance. These duplicates are identified as read pairs mapping to the exact same start and end coordinates and are collapsed to a single count.

3.  **Correction for Systematic Biases**: After initial filtering, the counts in each genomic bin are corrected for the major known biases identified in our earlier model:
    -   **Mappability Correction**: Regions of the genome with low [sequence complexity](@entry_id:175320) or high repeat content have low mappability ($m_i < 1$). This systematically reduces their observed read count. Failure to correct for this bias is a major source of false-positive deletion calls. The correction involves up-weighting the observed count in a bin by a factor related to its mappability, often the inverse of the mappability fraction. For instance, a bin with 50% mappability ($m_i=0.5$) that is truly diploid would be expected to have only half the reads of a fully mappable diploid bin. Observing 55 reads against an uncorrected baseline expectation of 100 would falsely suggest a deletion, whereas comparing it to the correct baseline of $100 \times 0.5 = 50$ reveals no significant deviation. [@problem_id:4331539]
    -   **GC Content Correction**: The relationship between GC content and read depth is often non-linear and sample-specific. This bias is typically corrected by fitting a [regression model](@entry_id:163386) (e.g., using LOESS) to the relationship between read depth and GC content across the genome, and then using this model to adjust the read count in each bin to what it would have been at a neutral GC content. A consistent dip in coverage across high-GC regions in many samples is the hallmark of this technical artifact, not a shared biological deletion. [@problem_id:4331512]

#### Advanced Normalization for Targeted Sequencing

For WES data, an additional, powerful source of noise arises from the variable efficiency of the "bait" probes used to capture exons. This results in massive, systematic differences in coverage between exons that are consistent across samples. **Cohort-based normalization** is a highly effective strategy to address this [@problem_id:4331523]. This method uses a reference panel of "normal" samples, processed with the same protocol, to build a statistical model of the expected technical profile. By fitting a Generalized Linear Model (e.g., using a Negative Binomial distribution to account for [overdispersion](@entry_id:263748)) on the reference panel, one can estimate the expected mean count and variance for every exon. The observed count in a new test sample can then be compared to this robust, empirically derived expectation, often by calculating a standardized Z-score. This approach not only corrects for exon-specific biases but also inherently mitigates [batch effects](@entry_id:265859) when the reference panel is well-matched to the test samples, dramatically improving the signal-to-noise ratio.

### From Cleaned Signal to Biological Segments

After normalization, the data (e.g., a series of log-ratio values along a chromosome) represent a noisy, one-dimensional signal. The final step in detection is to partition this signal into piecewise-constant segments, where each segment corresponds to a region of uniform copy number and the boundaries between segments represent CNV breakpoints. This is a classic **[change-point detection](@entry_id:172061)** problem.

#### Circular Binary Segmentation (CBS)

One of the most influential and widely used algorithms for this task is **Circular Binary Segmentation (CBS)** [@problem_id:4331586]. CBS operates through a recursive process to identify locations where the mean of the signal changes significantly.

The core mechanism of CBS is as follows:
1.  For a given chromosomal segment (initially, the entire chromosome), the algorithm considers all possible sub-intervals.
2.  For each sub-interval, it calculates a statistic, analogous to a t-statistic, that measures how different the mean of the signal within that sub-interval is compared to the mean of the signal in the rest of the segment.
3.  It identifies the sub-interval that yields the maximum value for this statistic.
4.  To determine if this maximum difference is statistically significant or simply due to random noise, CBS employs a [permutation test](@entry_id:163935). It repeatedly shuffles the data points within the segment and re-computes the maximal statistic to generate a null distribution. The observed maximal statistic is then compared to this null distribution to obtain a p-value.
5.  If the change is deemed significant, the algorithm declares the start and end points of the identified sub-interval as change-points. The original segment is split into three new ones, and the entire procedure is applied recursively to these smaller segments.
6.  The [recursion](@entry_id:264696) stops when no more significant change-points can be found.

The "circular" aspect of CBS is a technical device to handle [edge effects](@entry_id:183162), effectively treating the chromosome as if its ends were joined to ensure that potential CNVs at the very beginning or end of a chromosome are not missed. The result of this process is a partition of the chromosome into a set of segments, each with an assigned mean log ratio, which can then be interpreted as a specific copy [number state](@entry_id:180241).

### The Challenge of Cellular Heterogeneity

A final, critical principle is that biological samples are often not homogeneous. They can be mixtures of different cell populations, a phenomenon known as **mosaicism**. This is particularly prominent in cancer, where a tumor biopsy contains a mixture of malignant cells and contaminating normal, non-cancerous cells. This [cellular heterogeneity](@entry_id:262569) systematically affects the observed signal.

#### Signal Dilution in Mosaic and Tumor Samples

Consider a sample where a CNV is present in only a fraction, $f$, of the cells (the mosaic fraction). The remaining fraction, $1-f$, is diploid. Because the sequencing signal is an average across all cells in the sample, the expected average copy number, $\bar{C}$, is a linear mixture of the copy numbers of the two populations [@problem_id:4331546]:

$\bar{C} = f \cdot C_{\text{variant}} + (1-f) \cdot C_{\text{diploid}}$

where $C_{\text{diploid}} = 2$. The resulting log-ratio signal is $L = \log_2(\bar{C}/2)$. Because the average copy number $\bar{C}$ is pulled from the integer state of the variant cells towards the diploid state of the normal cells, the magnitude of the log ratio is attenuated. For example, a clonal ($f=1$) heterozygous deletion ($C_{\text{variant}}=1$) gives an expected log ratio of $\log_2(1/2) = -1$. If the same deletion is present in only 50% of cells ($f=0.5$), the average copy number is $\bar{C} = 0.5 \cdot 1 + 0.5 \cdot 2 = 1.5$, and the log ratio is $\log_2(1.5/2) = \log_2(0.75) \approx -0.415$. The signal amplitude is reduced, making subclonal events more difficult to detect.

This principle is fundamental to [cancer genomics](@entry_id:143632), where the mosaic fraction is known as **tumor purity** ($p$) [@problem_id:4331540]. The observed copy number signal, $C_{\text{obs}}$, is a mixture of the tumor's copy number, $C_{\text{tumor}}$, and the contaminating normal cells:

$C_{\text{obs}} = p \cdot C_{\text{tumor}} + (1-p) \cdot 2$

This relationship introduces a profound ambiguity. A single observed signal amplitude, $C_{\text{obs}}$, can be produced by multiple different combinations of purity and true tumor copy number. For instance, an observed copy number of $2.5$ could correspond to a tumor with $C_{\text{tumor}}=3$ in a sample with 50% purity ($0.5 \cdot 3 + 0.5 \cdot 2 = 2.5$) or a tumor with $C_{\text{tumor}}=4$ in a sample with 25% purity ($0.25 \cdot 4 + 0.75 \cdot 2 = 2.5$). This ambiguity is a central challenge that specialized cancer CNV algorithms must address, often by leveraging allele-specific BAF data to simultaneously co-estimate purity, [ploidy](@entry_id:140594) (the average copy number of the tumor genome), and segment-specific copy numbers.