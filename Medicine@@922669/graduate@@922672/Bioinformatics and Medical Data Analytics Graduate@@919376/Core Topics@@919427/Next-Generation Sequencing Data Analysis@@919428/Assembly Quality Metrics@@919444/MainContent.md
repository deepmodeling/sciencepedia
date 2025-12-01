## Introduction
The reconstruction of a complete genome from fragmented sequencing data is a cornerstone of modern biology, yet the output of a [de novo assembly](@entry_id:172264) is merely a draft. The true value of this draft—its utility for gene discovery, evolutionary analysis, or clinical diagnostics—hinges on its quality. However, 'quality' is not a single, simple attribute; it is a complex tapestry of contiguity, completeness, and correctness. This article provides a comprehensive guide to the essential metrics used to quantify assembly quality, addressing the critical knowledge gap between generating an assembly and confidently interpreting it. In the following chapters, you will first delve into the "Principles and Mechanisms" behind core metrics like N50, L50, and NG50, understanding their mathematical foundations and inherent limitations. Next, "Applications and Interdisciplinary Connections" will demonstrate how these metrics are applied and interpreted in diverse fields, from [metagenomics](@entry_id:146980) to human health, highlighting that the 'best' assembly is always context-dependent. Finally, "Hands-On Practices" will challenge you to apply these concepts, solidifying your ability to critically evaluate and compare genome assemblies in your own research.

## Principles and Mechanisms

In the evaluation of a de novo [genome assembly](@entry_id:146218), a primary objective is to quantify its **contiguity**—the extent to which the genome has been reconstructed into long, unbroken sequences. A highly contiguous assembly, characterized by a small number of large sequences, is generally more useful for downstream analyses such as [gene annotation](@entry_id:164186), [variant calling](@entry_id:177461), and [comparative genomics](@entry_id:148244) than a fragmented assembly composed of many small pieces. This chapter delineates the principles and mechanisms of the fundamental metrics used to measure assembly contiguity.

### The N50 and L50 Statistics: Core Measures of Contiguity

The most widely used metrics for assembly contiguity are the **N50** and **L50** statistics. These metrics provide a summary of the contig length distribution that is weighted by length, reflecting the fact that long [contigs](@entry_id:177271) contribute disproportionately more to the overall assembly. To understand these metrics, we must first establish a formal procedure.

Consider an assembly as a set of $n$ [contigs](@entry_id:177271) (or scaffolds), each with a specific length. The calculation of N50 and L50 follows these steps:
1.  Sum the lengths of all contigs to determine the total assembly size.
2.  Sort the contigs by length in descending order.
3.  Iteratively sum the lengths of the sorted contigs, starting from the longest, to create a cumulative length total.
4.  Identify the smallest set of the longest contigs whose cumulative length is at least 50% of the total assembly size.

From this minimal set, two key statistics are derived [@problem_id:4540076]:
-   The **L50** is the *count* of contigs in this set. It is a dimensionless integer that answers the question: "How many of the longest contigs are needed to cover half of the assembly?" A smaller L50 value indicates higher contiguity.
-   The **N50** is the *length* of the shortest contig within this same set. It is reported in base pairs (bp) and answers the question: "What is the minimum length of [contigs](@entry_id:177271) that make up the 'better' half of the assembly?" A larger N50 value indicates higher contiguity.

Let us consider a practical example to solidify these definitions. Suppose a draft genome assembly consists of the following contig lengths in base pairs (bp): $\{12000, 9000, 9000, 7500, 6000, 5000, 3000, 3000, 2000, 1500, 1000\}$ [@problem_id:4540073].

First, we calculate the total assembly size:
$G = 12000 + 9000 + 9000 + 7500 + 6000 + 5000 + 3000 + 3000 + 2000 + 1500 + 1000 = 59000 \text{ bp}$

The 50% threshold is $0.5 \times 59000 = 29500 \text{ bp}$.

Next, we sort the [contigs](@entry_id:177271) (they are already sorted) and compute the cumulative length:
-   Contig 1 (12,000 bp): Cumulative length = 12,000 bp
-   Contig 2 (9,000 bp): Cumulative length = $12000 + 9000 = 21000 \text{ bp}$
-   Contig 3 (9,000 bp): Cumulative length = $21000 + 9000 = 30000 \text{ bp}$

The cumulative length first meets or exceeds the $29500 \text{ bp}$ threshold after including the third contig. The minimal set of contigs required is $\{12000, 9000, 9000\}$.

-   The **L50** is the count of contigs in this set, which is $3$.
-   The **N50** is the length of the shortest contig in this set, which is $9000 \text{ bp}$.

This family of metrics can be generalized. For any percentage $x$, the **Nx** is the length of the contig that crosses the $x$% cumulative length threshold, and the **Lx** is the number of contigs required to do so. For example, **N90** and **L90** are defined analogously using a 90% threshold, providing insight into the more fragmented parts of the assembly [@problem_id:4540114].

### Reference-Based vs. Assembly-Based Metrics: The NG50 Statistic

A significant limitation of the N50 statistic is its dependence on the total assembly size. Since N50's threshold is defined as 50% of the *assembled* length, it is an internal, relative measure. This can be problematic when comparing assemblies of the same organism that have different total lengths, perhaps due to varying levels of completeness or the inclusion of contaminant sequences.

To illustrate, consider two assemblies, A and B. Assembly A has a total length of $95 \text{ Mb}$ and an N50 of $15 \text{ Mb}$. Assembly B is identical to A but includes an additional $20 \text{ Mb}$ of very small, fragmented contigs, bringing its total length to $115 \text{ Mb}$. The N50 threshold for B ($0.5 \times 115 = 57.5 \text{ Mb}$) is higher than for A ($0.5 \times 95 = 47.5 \text{ Mb}$). To reach this higher threshold, an additional large contig must be included in the cumulative sum, which lowers the N50 value (e.g., to $12 \text{ Mb}$). Thus, simply by adding fragmented sequences, the N50 value has decreased, giving a misleading impression of lower contiguity [@problem_id:4540050].

To address this, the **NG50** statistic was introduced. The NG50 calculation is identical to that of N50, but instead of using the total assembly size as the reference, it uses a pre-specified, estimated size of the genome, $G$ [@problem_id:4540053]. The threshold is fixed at $0.5 \times G$. This provides a stable, external frame of reference, making NG50 a more robust metric for comparing assemblies of differing completeness. In the example above, if the true [genome size](@entry_id:274129) is $G=100 \text{ Mb}$, the NG50 threshold is $50 \text{ Mb}$ for both assemblies. Consequently, both assemblies would report the same NG50 value ($15 \text{ Mb}$), correctly reflecting that their underlying contiguity for the well-assembled portions is identical [@problem_id:4540050].

It is important to note the relationship between N50 and NG50. If an assembly is incomplete such that its total length $L_{\text{asm}}$ is less than the estimated genome size $G$, then the threshold for NG50 ($0.5 \times G$) will be higher than the threshold for N50 ($0.5 \times L_{\text{asm}}$). Reaching a higher cumulative length threshold requires including more contigs from the sorted list, which means the index of the contig that crosses the threshold will be larger. Since [contigs](@entry_id:177271) are sorted by decreasing length, a larger index corresponds to a shorter contig length. Therefore, if $L_{\text{asm}} \lt G$, it follows that $NG_{50} \le N_{50}$ [@problem_id:4540053]. If the total assembly length is less than half the estimated genome size ($L_{\text{asm}} \lt 0.5 \times G$), the NG50 is undefined.

### A Broader View: Complementary Contiguity Metrics

While N50 is a powerful indicator of contiguity, it primarily reflects the "head" of the contig length distribution—the few large contigs that comprise the first half of the assembly. It is completely insensitive to the distribution of the remaining smaller contigs. An assembly could have an excellent N50 but be highly fragmented in its other half.

To gain a more complete picture, it is essential to use a suite of complementary metrics.

#### The L90 Statistic: Quantifying Tail Fragmentation

The **L90** statistic, which measures the number of contigs required to cover $90\%$ of the assembly, is an excellent complement to N50. Because it uses a high threshold, its value is strongly influenced by the "tail" of the distribution—the numerous smaller contigs. A high L90 value signals a highly fragmented tail, a fact that N50 would miss.

Consider two assemblies, X and Y, with the same total size ($1000 \text{ kb}$) and the same N50 value ($200 \text{ kb}$). The head of their contig distributions is identical. However, assembly X has a long tail of many small [contigs](@entry_id:177271), while assembly Y consists of only a few more moderately sized contigs. When we calculate L90, we find that $L90_{X} = 8$ while $L90_{Y} = 5$. The higher L90 for assembly X correctly identifies its greater fragmentation, even though its N50 was identical to Y's [@problem_id:4540064]. An ideal assembly exhibits both a high N50 and a low L90.

#### The E-size: Expected Contig Size

Another informative metric is the **E-size**, or expected contig size. It is defined from a simple thought experiment: if you were to pick a single base uniformly at random from the entire assembly, what is the expected length of the contig that base belongs to?

The probability of picking a base from a specific contig $i$ with length $L_i$ is proportional to its length: $P(\text{base in contig } i) = \frac{L_i}{\sum_j L_j}$. The expected contig length, $E$, is the sum of each contig's length multiplied by the probability of landing in it:
$E = \sum_i L_i \cdot P(\text{base in contig } i) = \sum_i L_i \cdot \frac{L_i}{\sum_j L_j} = \frac{\sum_i L_i^2}{\sum_j L_j}$

The E-size is particularly sensitive to the presence of very long [contigs](@entry_id:177271) because their lengths are squared in the numerator. This makes it a powerful detector of changes in the extreme tail of the distribution. It is possible to construct scenarios where two assemblies have an identical N50, but the addition of one very large contig to one of them causes its E-size to increase dramatically, while the N50 remains unchanged [@problem_id:4540098]. This highlights the different sensitivities of N50 and E-size, reinforcing the need to report multiple metrics.

### Practical Complexities: Scaffolds, Gaps, and Misassemblies

Real-world genome assemblies present complexities that require careful interpretation of these metrics.

#### Contig-level versus Scaffold-level Metrics

Most assembly pipelines produce not only contigs (continuous, gap-free sequences) but also **scaffolds**. A scaffold consists of one or more [contigs](@entry_id:177271) that are ordered and oriented relative to each other, with the intervening regions of unknown sequence represented by gaps (typically runs of 'N' characters). When calculating scaffold-level metrics, the lengths of these gaps are included in the total length of the scaffold and the total assembly size.

This distinction is critical [@problem_id:4540063].
-   **Scaffold-level N50** reflects long-range continuity. A high scaffold N50 is desirable for applications like [synteny](@entry_id:270224) analysis or anchoring an assembly to a [physical map](@entry_id:262378), where the overall arrangement of genomic regions is more important than the small, unresolved gaps between them.
-   **Contig-level N50** reflects true, unbroken sequence continuity. It is the more informative metric for base-level analyses like [gene finding](@entry_id:165318) or SNP calling, as a gene or variant call cannot span a gap. A high scaffold N50 can be misleading if it is achieved by scaffolding many small contigs together with large gaps.

Furthermore, the presence of **unresolved gaps** (gaps of unknown size) introduces ambiguity into scaffold-level metrics. Since the length of some scaffolds and the total assembly size become ill-defined, a single, definitive scaffold N50 cannot be calculated. A conservative and transparent reporting strategy is to:
1.  Report contig-level metrics as the primary, unambiguous measure of sequence contiguity.
2.  Provide clearly labeled scaffold-level metrics calculated under different conservative assumptions, such as a "sequence-only" metric where all gaps are treated as zero-length, and a "known-gap" metric where only estimated gap sizes are included [@problem_id:4540066].

#### The Ultimate Caveat: Misassemblies

Perhaps the greatest limitation of all the metrics discussed so far is that they operate on the assumption that the assembly is structurally correct. However, assemblers can erroneously join sequences from non-adjacent parts of the genome, creating **chimeric contigs**. Such misassemblies can artificially and dramatically inflate contiguity statistics.

For example, an assembly with a true N50 of $20 \text{ Mb}$ could, due to a single misassembly event, appear to have a chimeric contig of $55 \text{ Mb}$, which would inflate its reported N50 to $55 \text{ Mb}$. This gives a false impression of a massive improvement in contiguity, when in fact the assembly's structure has been compromised [@problem_id:4540122].

To detect such issues, contiguity metrics must be paired with **validation-aware metrics**. This typically involves aligning the assembly to a high-quality [reference genome](@entry_id:269221) or a long-range [physical map](@entry_id:262378) (e.g., optical maps) to identify breakpoints corresponding to misassemblies. From this alignment, one can calculate:
-   **Breakpoint Count**: The total number of structural errors.
-   **NGA50 (or equivalent)**: The N50 statistic calculated on the set of *validated alignment blocks* created by clipping the original contigs at each breakpoint.

A truly high-quality, contiguous assembly will show a high N50 that is matched by a similarly high NGA50 and a very low breakpoint count. A large discrepancy between N50 and NGA50 is a red flag for an assembly whose contiguity is artificially inflated by misassemblies [@problem_id:4540122].

### Mathematical Foundations of N50

For the theoretically inclined reader, the N50 statistic can be formalized within the framework of robust statistics. If we model contig lengths as a random variable with a [cumulative distribution function](@entry_id:143135) (CDF) $F(x)$, the N50 is not the median of this distribution. Rather, it is the median of the **size-biased distribution**, whose CDF is given by $\mathcal{S}[F](x) = \frac{1}{\mu} \int_0^x t \,dF(t)$, where $\mu$ is the mean contig length. This formulation directly corresponds to the principle of sampling a random base and observing its host contig's length [@problem_id:4540100].

The sensitivity of a statistic to contamination can be measured by its **Influence Function (IF)**. A bounded IF indicates robustness against outliers. A detailed derivation shows that the [influence function](@entry_id:168646) for the N50 functional is unbounded; its effect grows linearly with the size of a contaminating long contig [@problem_id:4540100]. This confirms mathematically what was observed intuitively: the N50 statistic, while powerful, is not robust to extreme outliers in the form of very long (and potentially chimeric) [contigs](@entry_id:177271), further underscoring the need for careful validation and the use of complementary metrics.