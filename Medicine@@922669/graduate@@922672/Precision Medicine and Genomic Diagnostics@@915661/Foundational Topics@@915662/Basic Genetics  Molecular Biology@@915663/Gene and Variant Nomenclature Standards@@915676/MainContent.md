## Introduction
In the era of precision medicine, our ability to interpret the human genome hinges on a shared, unambiguous language for describing genetic variation. Historically, the absence of a universal standard led to confusion, database errors, and potentially flawed clinical diagnoses, creating a critical bottleneck in translating genomic discoveries into patient care. The Human Genome Variation Society (HGVS) nomenclature was developed to solve this problem, providing a rigorous and consistent framework for documenting genetic changes.

This article serves as a comprehensive guide to mastering these essential standards. We will begin in "Principles and Mechanisms" by dissecting the core rules of HGVS, from the foundational concept of a versioned reference sequence to the specific coordinate systems for DNA, RNA, and protein. Next, in "Applications and Interdisciplinary Connections," we will explore how this nomenclature is applied in real-world scenarios, including clinical variant curation, pharmacogenomics, and the integration of data across platforms like ClinVar and FHIR. Finally, "Hands-On Practices" will challenge you to apply your knowledge to complex, practical examples. By the end, you will have a robust understanding of how to accurately describe and interpret genetic variants, a cornerstone skill for any professional in genomics or precision medicine.

## Principles and Mechanisms

The accurate and unambiguous description of genetic variation is a cornerstone of genomics, genetics, and precision medicine. In the absence of a universal standard, historical descriptions of variants were often ambiguous, leading to confusion, erroneous database entries, and potentially incorrect clinical interpretations. To solve this problem, the Human Genome Variation Society (HGVS) developed a comprehensive set of rules for variant nomenclature. This chapter elucidates the core principles and mechanisms of the HGVS standard, providing a systematic framework for describing genetic variants at the DNA, RNA, and protein levels.

### The Foundation: The Principle of Unambiguous Reference

The central tenet of HGVS nomenclature is that **every variant description must be inextricably linked to a defined reference sequence**. A variant is a deviation from a "normal" sequence, and its description is meaningless without specifying precisely which version of "normal" is being used as the comparator. Reference sequences, whether for a chromosome, a transcript, or a protein, are not static. They are curated entities stored in databases like the Reference Sequence (RefSeq) database at the National Center for Biotechnology Information (NCBI), and they are periodically updated to correct errors or reflect new biological knowledge.

For this reason, HGVS nomenclature mandates the inclusion of the reference sequence **[accession number](@entry_id:165652) and version**. An [accession number](@entry_id:165652) (e.g., `NM_000546`) is a stable label for a sequence record, while the version number (the integer following the period, e.g., `.6` in `NM_000546.6`) tracks changes to that record over time.

The critical importance of the version number cannot be overstated. Consider a hypothetical clinical report describing a variant in the $TP53$ gene as `NM_000546:c.215C>G`, omitting the version number. Suppose this report was based on version `NM_000546.5`. Later, bioinformaticians update the [gene annotation](@entry_id:164186), establishing that the true [translation initiation](@entry_id:148125) site is further upstream. This correction results in a new version, `NM_000546.6`. In this new version, the position formerly known as `c.1` in the `.5` transcript might now be `c.10`, shifting all downstream coordinates. The physical nucleotide that was at position `c.215` in the old `.5` reference is now located at `c.224` in the new `.6` reference. An analyst who interprets the unversioned report `c.215C>G` using the newer `NM_000546.6` reference will be looking at a completely different location in the gene, leading to a profound error in interpretation [@problem_id:4343238]. Specifying the full, versioned accession, such as `NM_000546.5:c.215C>G`, ensures that the description remains a stable, reproducible, and accurate pointer to a specific molecular event, regardless of future updates to reference databases.

### The Coordinate Systems: Describing Location Across Molecules

Genetic information flows from the genome (DNA) to transcripts (RNA) to proteins. HGVS provides distinct [coordinate systems](@entry_id:149266) to describe variants relative to each of these molecular substrates. The choice of coordinate system is indicated by a prefix preceding the variant description. [@problem_id:4343290]

**Genomic ($g.$) Coordinates**: This is the most fundamental coordinate system.
-   **Substrate**: A genomic reference sequence, typically a chromosome or a large contig (e.g., from `NC_` accession series).
-   **Numbering**: Positions are numbered sequentially starting from `1` at the first nucleotide of the reference sequence in its standard $5^\prime \to 3^\prime$ orientation.
-   **Key Feature**: The genomic coordinate system is absolute and stable. It does not change based on the location or transcriptional direction of genes. A variant at `g.1000` is always the 1000th base from the start of the chromosome reference, even if a gene at that locus is transcribed on the negative strand.

**Transcript-based DNA Coordinates ($c.$ and $n.$)**: These systems describe variants relative to a transcript sequence, which represents the processed RNA molecule but is written using DNA alphabet ($A, C, G, T$).
-   **Coding DNA ($c.$) Coordinates**: This system is used for protein-coding transcripts (e.g., `NM_` accessions) and is centered on the translation process.
    -   **Substrate**: A conceptual DNA sequence corresponding to the mature, spliced mRNA.
    -   **Numbering**: The **A** of the `ATG` [translation initiation](@entry_id:148125) codon is designated **`c.1`**. Numbering proceeds with positive integers through the [coding sequence](@entry_id:204828) (CDS). This rule is strict; `c.` coordinates can only be used for transcripts with a defined, canonical `ATG` [start codon](@entry_id:263740). For transcripts with non-standard initiation (e.g., a `CTG` [start codon](@entry_id:263740)) or for those where the CDS is uncertain, `c.` coordinates are not permitted. [@problem_id:4343233]
-   **Non-coding DNA ($n.$) Coordinates**: This system is used for transcripts that do not code for protein (e.g., `NR_` accessions for non-coding RNAs) or for coding transcripts where the `c.` system is inappropriate.
    -   **Substrate**: A conceptual DNA sequence corresponding to a non-coding or un-annotated transcript.
    -   **Numbering**: Numbering begins with **`n.1`** at the first nucleotide of the transcript reference sequence and proceeds linearly. It does not rely on translational landmarks.

**RNA ($r.$) Coordinates**:
-   **Substrate**: The RNA sequence itself.
-   **Numbering**: Numbering starts at `r.1` for the first nucleotide of the RNA transcript.
-   **Alphabet**: By convention, RNA descriptions use lowercase letters and uracil (`u`) instead of thymine (`t`), i.e., `a, c, g, u`.

**Protein ($p.$) Coordinates**:
-   **Substrate**: The amino acid sequence.
-   **Numbering**: Numbering begins with `p.1` for the initiator methionine, as predicted from the reference transcript's [start codon](@entry_id:263740).
-   **Alphabet**: Amino acids are typically represented by their three-letter codes (e.g., `Met`, `Arg`, `Gly`).

### Navigating the Transcript: The `c.` Coordinate System in Detail

The coding DNA (`c.`) coordinate system is the most frequently used for clinical reporting and requires a detailed understanding of its conventions for regions outside the main coding sequence.

#### The Untranslated Regions (UTRs)

The portions of a transcript that are not translated into protein are known as the **5' Untranslated Region (5' UTR)**, located upstream of the start codon, and the **3' Untranslated Region (3' UTR)**, located downstream of the stop codon. HGVS has specific notations for these regions [@problem_id:4343329].

-   **5' UTR**: Nucleotides in the 5' UTR are numbered using negative integers, counting backwards from the [start codon](@entry_id:263740). The nucleotide immediately upstream of `c.1` is `c.-1`, the next is `c.-2`, and so on. For instance, a variant located 12 bases upstream of the start codon is described at position `c.-12`. There is no `c.0`.

-   **3' UTR**: Nucleotides in the 3' UTR are numbered using a leading asterisk (`*`) followed by positive integers, counting forward from the last nucleotide of the termination codon. The nucleotide immediately downstream of the [stop codon](@entry_id:261223) is `c.*1`, the next is `c.*2`, and so on. A variant 45 bases into the 3' UTR is described at position `c.*45`.

#### Introns

The `c.` reference sequence represents the mature, spliced transcript; [introns](@entry_id:144362) are, by definition, not part of this sequence. To describe variants within introns, HGVS uses an **offset notation** anchored to the nearest exon boundary [@problem_id:4343243].

Consider an [intron](@entry_id:152563) located between two exons. Let the last nucleotide of the upstream exon be at position `c.123` and the first nucleotide of the downstream exon be at `c.124`.

-   **Splice Donor Site Offsets**: Variants in the first half of the intron (closer to the upstream exon) are described relative to the upstream exon's boundary. A positive sign (`+`) indicates the offset *into* the intron. The first nucleotide of the intron is `c.123+1`, the second is `c.123+2`, and so on.

-   **Splice Acceptor Site Offsets**: Variants in the second half of the intron (closer to the downstream exon) are described relative to the downstream exon's boundary. A negative sign (`-`) indicates the offset *back into* the intron. The last nucleotide of the intron is `c.124-1`, the second-to-last is `c.124-2`, and so on.

The power of this system lies in its ability to translate between [coordinate systems](@entry_id:149266). For example, a variant known to be at genomic position `g.1060` can be described in the context of a transcript. If bioinformatic alignment shows this transcript's Exon 2 ends at `g.1050` (corresponding to `c.50`) and Exon 3 begins at `g.1071` (corresponding to `c.51`), then the variant at `g.1060` is clearly intronic. It is 10 bases downstream of the end of Exon 2 (`1060 - 1050 = 10`) and 11 bases upstream of the start of Exon 3 (`1071 - 1060 = 11`). Since it is closer to the end of Exon 2, its coordinate is `c.50+10` [@problem_id:4343325]. The full description `NM_543210.2:c.50+10A>G` is a precise, transcript-centric name for the genomic event `NC_012345.1:g.1060A>G`.

### Describing the Change: Types of Variants and Normalization

Once a location is specified, the nature of the change is described. Substitutions are straightforward (e.g., `A>G`). Insertions and deletions, especially in repetitive regions, require special rules.

A key distinction is between an **insertion ($ins$)** and a **duplication ($dup$)**. An insertion adds a novel sequence. A duplication adds a copy of an adjacent reference sequence. HGVS mandates that if an inserted sequence is identical to a sequence immediately adjacent to it, the event must be described as a duplication [@problem_id:4343245]. For example, if the sequence `AG` is inserted between `G` and `A` in the reference `...CTAGAGTT...`, creating `...CTAGAGAGTT...`, the inserted `AG` is a copy of the adjacent sequence at `c.105_106`. Therefore, this is a duplication, not an insertion.

This leads to the problem of ambiguity. In the sequence `...CTAGAGAGTT...`, which `AG` was duplicated? The duplication could be described as `c.103_104dup` or `c.105_106dup`. To resolve this, HGVS employs the **3' rule**: for all descriptions, the variant must be shifted as far $3^\prime$ (to the right, towards higher coordinate numbers) as possible. In this case, `c.105_106dup` is the correct, normalized description because its coordinates are more $3^\prime$ than `c.103_104dup` [@problem_id:4343245].

This normalization principle is a frequent source of discordance between different variant-calling standards. The widely used **Variant Call Format (VCF)** employs the opposite strategy: **left-normalization**, where indels are shifted as far $5^\prime$ (to the left) as possible. Consider a deletion of a `TA` unit within a `(TA)4` repeat at `g.1002-1009`. HGVS, using the $3^\prime$ rule, would describe this as a deletion at the rightmost possible position, e.g., `g.1008_1009del`. In contrast, a VCF file, after left-normalization, would represent this same allele with a position (`POS`) anchored at the leftmost possible coordinate, which may be far upstream of the repeat itself. This discrepancy means that a naive database join on genomic coordinates will fail to match a VCF record with its corresponding HGVS record for the same biological event. Recognizing and resolving these different normalization rules is a critical task in bioinformatics [@problem_id:4343292].

### Predicting the Consequence: The `p.` (Protein) Level

The final step in variant description is often to predict its effect on the protein product. This is denoted with the `p.` prefix. However, a DNA-level change only provides a *prediction* of the protein effect. Biological processes like [alternative splicing](@entry_id:142813) or [nonsense-mediated decay](@entry_id:151768) (NMD) can alter the final outcome.

To maintain scientific rigor, HGVS enforces a strict **rule of evidence**: consequences predicted from DNA or RNA analysis alone **must be enclosed in parentheses**. Unparenthesized descriptions are reserved for effects that have been experimentally confirmed at the protein level.

This principle applies to all types of protein changes [@problem_id:4343267] [@problem_id:4343269]:
-   **Missense Variant**: A DNA change predicted to cause an arginine-to-serine substitution at residue 97 is written as `p.(Arg97Ser)`. The description `p.Arg97Ser` implies that the substituted protein has been isolated and sequenced.

-   **Synonymous (Silent) Variant**: A DNA change predicted to result in no amino acid change is written `p.(=)`. This is a prediction because the variant could still affect splicing and produce an altered protein. The description `p.=` is used only when RNA analysis has confirmed normal splicing and protein analysis has confirmed the absence of a change.

-   **Nonsense/Frameshift Variant**: A DNA change predicted to create a frameshift resulting in a premature termination codon is written in parentheses, e.g., `p.(Lys100Argfs*12)`. This prediction is highly uncertain because the cell's NMD machinery may degrade the mutant transcript, resulting in no protein product at all. The unparenthesized form requires experimental proof (e.g., via Western blot) that the [truncated protein](@entry_id:270764) is actually produced.

-   **Unknown Consequence**: When the effect of a variant cannot be confidently predicted (e.g., a deep intronic variant), the description is `p.?`.

It is crucial to recognize that *in silico* predictions of deleteriousness (from tools like SIFT or PolyPhen) do not constitute experimental evidence. No matter how high the confidence score, the predicted protein effect derived from DNA sequencing must be reported in parentheses [@problem_id:4343269]. This disciplined use of parentheses ensures that variant descriptions faithfully represent the level of experimental evidence available, a practice that is fundamental to the integrity of genomic data.