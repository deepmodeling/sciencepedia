## Introduction
Reverse Transcription Polymerase Chain Reaction (RT-PCR) is a revolutionary technique in molecular science, providing the ability to detect and quantify RNA with unparalleled sensitivity and specificity. Its central role in fields ranging from viral diagnostics to cancer research underscores its importance. However, transitioning from a theoretical understanding of RT-PCR to the successful design and execution of a robust and reliable assay presents a significant challenge. Many factors, from enzyme choice and RNA quality to [data normalization](@entry_id:265081), can profoundly impact the validity of the results, creating a critical knowledge gap between basic principles and expert application.

This article bridges that gap by providing a comprehensive exploration of RT-PCR for RNA targets. The first chapter, **Principles and Mechanisms**, will dissect the core components of the assay, detailing the enzymes, priming strategies, and design principles necessary for quality control and specificity. Following this, the **Applications and Interdisciplinary Connections** chapter will illustrate the technique's versatility through real-world examples in clinical diagnostics, oncology, and gene regulation studies. Finally, the **Hands-On Practices** section will offer practical exercises to solidify your understanding of data analysis and assay validation. By progressing through these chapters, you will gain the expertise needed to confidently apply RT-PCR in your own research and diagnostic work.

## Principles and Mechanisms

Reverse Transcription Polymerase Chain Reaction (RT-PCR) stands as a cornerstone technique in modern molecular biology and diagnostics, enabling the sensitive detection and quantification of ribonucleic acid (RNA) targets. The power of this method resides in a two-part process that first translates the information encoded in RNA into a more stable deoxyribonucleic acid (DNA) form, which is then exponentially amplified to detectable levels. This chapter elucidates the fundamental principles and mechanisms that govern each step of this process, from the enzymatic core of [reverse transcription](@entry_id:141572) to the sophisticated strategies required for robust assay design, quality control, and data interpretation.

### The Heart of the Assay: The Reverse Transcriptase Enzyme

At the core of RT-PCR is the **reverse transcriptase** (RT), an RNA-dependent DNA polymerase. This enzyme catalyzes the synthesis of a complementary DNA (cDNA) strand using an RNA molecule as a template, a process that is a direct reversal of the canonical flow of genetic information described by the Central Dogma.

#### Catalytic Mechanism and Key Properties

Like other nucleic acid polymerases, reverse transcriptases catalyze [phosphodiester bond formation](@entry_id:169832) via a **[two-metal ion mechanism](@entry_id:167167)**. The enzyme's active site coordinates two divalent metal cations, typically magnesium ions ($Mg^{2+}$), which are essential for catalysis. These ions facilitate the [nucleophilic attack](@entry_id:151896) by the $3'$-hydroxyl group of the growing primer strand on the $\alpha$-phosphate of an incoming deoxynucleoside triphosphate (dNTP), leading to the incorporation of the new nucleotide and the release of pyrophosphate. The fidelity and efficiency of this process are dictated by several intrinsic properties of the enzyme.

*   **Thermostability**: The ability of an enzyme to maintain its structure and function at elevated temperatures is a critical property. Many RNA templates, particularly long non-coding RNAs or viral genomes, are rich in secondary structures such as stable hairpins and loops. These structures can impede the progress of the [reverse transcriptase](@entry_id:137829), causing it to pause or dissociate from the template, resulting in truncated, incomplete cDNA products. By performing the reverse transcription reaction at a higher temperature, these RNA secondary structures can be denatured or "melted," presenting the enzyme with a more linear template. For instance, to accurately reverse transcribe an RNA with a predicted hairpin [melting temperature](@entry_id:195793) ($T_m$) of $58^{\circ}\mathrm{C}$, an enzyme must be active at or above this temperature to ensure processivity [@problem_id:5157252].

*   **Fidelity**: Fidelity refers to the accuracy of the enzyme, or its propensity to avoid incorporating incorrect nucleotides. Different reverse transcriptases exhibit different intrinsic error rates. High fidelity is crucial for applications where the resulting cDNA will be sequenced or used for cloning, but it is also important in quantitative assays to ensure consistent amplification efficiency.

*   **RNase H Activity**: Many retroviral reverse transcriptases, including native forms of Avian Myeloblastosis Virus (AMV) and Moloney Murine Leukemia Virus (MMLV) RTs, possess a second enzymatic function: a **ribonuclease H (RNase H)** domain. This domain is an endonuclease that specifically degrades the RNA strand of the RNA/DNA hybrid that forms behind the polymerase as it synthesizes cDNA. While this activity is part of the natural retroviral life cycle, it can be detrimental in vitro, especially for synthesizing long cDNAs. If the polymerase pauses (e.g., at a [secondary structure](@entry_id:138950)), the lagging RNase H activity can "catch up" and degrade the RNA template near the growing point, preventing the polymerase from re-initiating and leading to truncated products.

#### A Bestiary of Reverse Transcriptases

The choice of [reverse transcriptase](@entry_id:137829) is a critical decision in assay design, dictated by the specific requirements of the experiment.

*   **Moloney Murine Leukemia Virus Reverse Transcriptase (MMLV RT)**: This is one of the most commonly used RTs. Wild-type MMLV RT has a relatively low optimal temperature (around $37\text{–}42^{\circ}\mathrm{C}$) and is rapidly inactivated at temperatures above $50^{\circ}\mathrm{C}$. It has lower RNase H activity than AMV RT, and, crucially, it has been genetically engineered to create variants that are completely RNase H-deficient (RNase H-minus). These RNase H-minus variants are preferred for synthesizing long cDNAs, but their low thermostability still makes them unsuitable for highly structured templates.

*   **Avian Myeloblastosis Virus Reverse Transcriptase (AMV RT)**: AMV RT exhibits a higher optimal temperature (around $42\text{–}50^{\circ}\mathrm{C}$) than MMLV RT but retains robust RNase H activity, making it a poor choice for generating full-length cDNA from long transcripts.

*   **Thermostable Engineered Reverse Transcriptases**: To overcome the limitations of retroviral enzymes, a variety of engineered and novel RTs have been developed. These include enzymes like the **Thermostable Group II Intron Reverse Transcriptase (TGIRT)**. Such enzymes offer superior performance characteristics, including high thermostability (optimal temperatures of $55\text{–}65^{\circ}\mathrm{C}$ or higher), high [processivity](@entry_id:274928) (ability to synthesize long cDNAs without dissociating), and high fidelity. They typically lack RNase H activity. For a demanding application, such as synthesizing a full-length, $4.2\,\text{kb}$ cDNA from a template with hairpins that melt at $58^{\circ}\mathrm{C}$, a thermostable enzyme like TGIRT is the only appropriate choice. It can operate at a temperature (e.g., $60^{\circ}\mathrm{C}$) that melts the [secondary structure](@entry_id:138950), and its high [processivity](@entry_id:274928) and lack of RNase H activity ensure the synthesis of a complete and accurate cDNA copy [@problem_id:5157252].

### Initiating Synthesis: cDNA Priming Strategies

Reverse transcriptase, like all template-dependent DNA polymerases, cannot initiate synthesis *de novo*. It requires a short nucleic acid primer to be annealed to the template, providing a free $3'$-hydroxyl group from which to begin extension. The choice of priming strategy is a pivotal decision that defines the specificity and coverage of the resulting cDNA library.

#### Three Core Strategies

1.  **Oligo(dT) Priming**: This strategy employs a short polymer of deoxythymidine, which specifically anneals to the polyadenylated (poly(A)) tail found at the $3'$ end of most mature eukaryotic messenger RNAs (mRNAs). This makes oligo(dT) priming an excellent choice for specifically converting the mRNA population into cDNA, while excluding non-polyadenylated RNAs like ribosomal RNA (rRNA), transfer RNA (tRNA), and most microRNAs. However, its reliance on an intact path from the $3'$ end to the $5'$ end makes it highly sensitive to RNA degradation.

2.  **Random Hexamer Priming**: This strategy uses a mixture of short oligonucleotides (typically 6-mers) representing all possible sequence combinations. These primers can anneal at multiple complementary sites along the entire length of all RNA molecules in a sample. This approach is advantageous for several reasons: it provides more uniform cDNA coverage along a transcript, it allows for the reverse transcription of non-polyadenylated RNAs (such as some lncRNAs, viral genomes, or bacterial RNAs), and, critically, it is the most robust method for working with partially degraded RNA.

3.  **Gene-Specific Priming (GSP)**: In this strategy, a primer is designed to be complementary to a specific, known sequence within the single RNA target of interest. This approach offers the highest specificity, as only the target RNA is converted into cDNA. GSPs are essential for one-step RT-PCR workflows (discussed later) and can be used in two-step protocols to enrich for a low-abundant target.

#### Application in Degraded RNA

The choice of priming strategy is paramount when working with RNA of compromised integrity, such as that extracted from formalin-fixed, paraffin-embedded (FFPE) tissues. RNA degradation can be modeled as a random process of cleavage events. If we assume a Poisson break process with a rate $\lambda$ of breaks per nucleotide, the probability that a segment of length $x$ is intact is $e^{-\lambda x}$.

Consider an assay designed to detect a region near the $5'$ end of a $2000$ nucleotide mRNA transcript where the average intact fragment length is only $200$ nucleotides.
*   With **oligo(dT) priming**, the reverse transcriptase must traverse the entire length of the transcript from the $3'$ poly(A) tail. The probability of success is $e^{-2000/200} = e^{-10}$, which is vanishingly small.
*   With a **[gene-specific primer](@entry_id:182159)** placed $100$ nucleotides from the $5'$ end, the required intact length is only $100$ nucleotides, yielding a probability of $e^{-100/200} = e^{-0.5}$, which is far better.
*   With **random hexamers**, a successful priming event can occur anywhere, including very close to the $5'$ end. If priming within $30$ nucleotides of the end is sufficient, the probability of success is determined by the integrity of this short segment, $e^{-30/200} = e^{-0.15}$, the highest of the three strategies.

This quantitative example demonstrates that for degraded RNA, **random hexamer priming provides the highest probability of retaining representation of the $5'$ ends of transcripts** in the cDNA library, followed by $5'$-proximal gene-specific primers. Oligo(dT) priming is the least effective and leads to a strong $3'$ bias in the data [@problem_id:5157237].

### Ensuring Quality and Specificity: Assay Design Principles

A successful RT-PCR assay is not merely the result of mixing enzymes and primers; it is a carefully designed system that incorporates quality control measures and strategies to ensure specificity for the intended target.

#### RNA Quality Control: The RNA Integrity Number (RIN)

Before committing a precious clinical sample to an assay, it is essential to assess the quality of the extracted RNA. The **RNA Integrity Number (RIN)** is the industry standard for this purpose. The RIN is an algorithm-based score from 1 (completely degraded) to 10 (perfectly intact) derived from the electrophoretic profile of a total RNA sample, typically obtained via microfluidic [capillary electrophoresis](@entry_id:171495). For eukaryotic RNA, the algorithm primarily analyzes the characteristics of the highly abundant $18S$ and $28S$ ribosomal RNA (rRNA) peaks, using their ratio, sharpness, and the amount of signal in the baseline (representing a smear of degraded fragments) to infer the integrity of the entire transcriptome, including the less abundant mRNA population [@problem_id:5157244].

The RIN score has direct practical implications for assay design and data interpretation:
*   **Amplifiable Fragment Length**: As RNA degrades (lower RIN), the probability of finding an intact template of a given length decreases exponentially. This means the distribution of amplifiable fragment lengths shifts toward shorter lengths for low-RIN samples. Assays designed for low-RIN samples should therefore use the shortest possible amplicons.
*   **Positional Bias**: As discussed previously, low RIN exacerbates the $3'$ bias in cDNA synthesized with oligo(dT) primers, as the probability of the enzyme reaching targets distal from the $3'$ end diminishes. This phenomenon is known as **$5'$-end dropout**. Therefore, for low-RIN samples, it is critical to design amplicons as close to the $3'$ end of the transcript as possible to ensure reliable detection [@problem_id:5157244].

#### Workflow Choices: One-Step vs. Two-Step RT-PCR

RT-PCR assays can be performed in two main formats, each with distinct advantages and disadvantages, particularly in a high-throughput diagnostic setting.

*   **Two-Step RT-PCR**: This classic workflow involves two separate reactions. First, the RNA is reverse transcribed into cDNA in one tube. Then, an aliquot of the resulting cDNA is transferred to a second tube for the qPCR amplification. This approach offers great flexibility; different priming strategies (oligo(dT), random hexamers, or a mix) can be used in the RT step to create a complex cDNA library that can be archived and used as a template for multiple different qPCR assays.

*   **One-Step RT-PCR**: In this format, the reverse transcription and PCR amplification occur sequentially in the same, closed reaction tube. All necessary enzymes (RT and thermostable DNA polymerase) and primers (which must be gene-specific) are present from the start. A thermal profile is used that includes an initial RT step at a moderate temperature, followed by an enzyme inactivation/DNA polymerase activation step, and finally the standard thermal cycling for PCR.

For high-throughput clinical diagnostics, **one-step RT-PCR is often superior due to its reduced contamination risk and faster turnaround time**. Every time a sample is transferred between tubes, there is a risk of introducing contaminating nucleic acids from the environment or from other samples (carryover). A quantitative comparison highlights this: if a one-step workflow involves 2 liquid handling steps per sample and a two-step workflow involves 4, the two-step process has double the risk of contamination-induced false positives. Furthermore, by combining two reactions into one, the one-step process reduces hands-on time, reagent costs, and total instrument time, making it more efficient for processing large numbers of samples [@problem_id:5157258].

#### Combating Contamination: The Challenge of Genomic DNA

A persistent challenge in RT-PCR is the potential for contaminating genomic DNA (gDNA) in the RNA preparation to serve as a template in the PCR step, leading to false-positive signals. While treating the RNA sample with DNase can help, the most robust solution is to design the assay to be inherently specific for the spliced mRNA template. This is achieved by designing an **exon-exon junction spanning amplicon**.

In eukaryotes, genes are transcribed into pre-mRNA, which contains both coding regions (**exons**) and intervening non-coding regions (**introns**). Through **splicing**, [introns](@entry_id:144362) are removed, and exons are ligated together to form the mature mRNA. This process creates a novel sequence at the exon-exon boundary that exists in the mature mRNA (and its cDNA copy) but not as a contiguous stretch in the gDNA.

An assay designed to span an exon-exon junction exploits this difference in two ways:
1.  **Primer Binding Specificity**: At least one of the PCR primers is designed to anneal directly over the junction, with its sequence being complementary to the last few bases of the upstream exon and the first few bases of the downstream exon. This primer will bind efficiently to the contiguous target site on the cDNA. On the gDNA template, however, the two halves of the primer's target sequence are separated by hundreds or thousands of bases of the intron. The primer cannot find a stable, contiguous binding site, particularly at its crucial $3'$ end, which prevents the DNA polymerase from initiating synthesis.
2.  **Amplicon Size**: Even if the primers were designed to lie entirely within two adjacent exons, the resulting amplicon from cDNA would be short and efficiently amplified. The corresponding product from gDNA would have to span the intron, making it orders of magnitude longer. Standard PCR conditions use short extension times that are kinetically insufficient to amplify such massive fragments, effectively preventing signal generation from the gDNA template [@problem_id:5157282].

#### Designing for Diverse RNA Targets

Different classes of RNA possess unique structural and biochemical features that demand highly tailored assay designs. A "one size fits all" approach is doomed to failure. Consider an experiment aiming to quantify four distinct RNA species:

*   **Messenger RNA (mRNA)**: As a polyadenylated, spliced transcript primarily located in the cytoplasm, the optimal strategy is to use oligo(dT) priming on a cytoplasmic RNA fraction and design qPCR primers that span an exon-exon junction.
*   **Mature MicroRNA (miRNA)**: These are very short ($\approx 22$ nucleotides), non-polyadenylated cytoplasmic molecules. Standard RT-PCR methods fail because the molecule is too short for conventional primer binding. The gold-[standard solution](@entry_id:183092) is **stem-loop reverse transcription**. A specially designed primer with a hairpin structure binds specifically to the $3'$ end of the mature miRNA and provides a long template for the RT to extend, creating a chimeric cDNA that can then be amplified with a specific forward primer and a universal reverse primer.
*   **Precursor MicroRNA (pre-miRNA)**: These nuclear-enriched hairpin precursors ($\approx 70$ nucleotides) are too long and structured for a miRNA-specific stem-loop primer. They are best targeted using a **gene-specific linear RT primer** on a nuclear RNA fraction.
*   **Long Non-coding RNA (lncRNA)**: These long transcripts are often nuclear-retained and can be variably polyadenylated. To ensure quantification of the entire population (both polyadenylated and non-polyadenylated forms), **random hexamer priming** is the most robust strategy.

This example illustrates that a rigorous RT-PCR study requires a deep understanding of RNA biogenesis to select the appropriate combination of cellular fractionation, RT priming, and qPCR design for each target of interest [@problem_id:5157256].

### Signal Generation and Interpretation in Real-Time PCR

Real-time PCR, or qPCR, monitors the amplification process in real time by detecting a fluorescent signal. The **cycle threshold ($C_t$)** is the cycle number at which the fluorescence crosses a defined threshold, with a lower $C_t$ indicating a higher initial amount of target. The chemistry used to generate this signal is a key determinant of assay specificity and [multiplexing](@entry_id:266234) capability.

#### Detection Chemistries

*   **Intercalating Dyes (e.g., SYBR Green)**: These dyes, such as SYBR Green I, exhibit low fluorescence in solution but fluoresce brightly upon binding to the minor groove of any double-stranded DNA (dsDNA). The signal is proportional to the total mass of dsDNA in the reaction. This method is simple and inexpensive, but its signal is non-specific. It cannot distinguish between the intended product, off-target amplicons, or [primer-dimers](@entry_id:195290). **Melt-curve analysis**, performed after the PCR, can help assess product specificity by identifying the characteristic [melting temperature](@entry_id:195793) ($T_m$) of the desired amplicon, but this is a post-hoc check. Because all dsDNA products generate the same signal, SYBR Green is fundamentally unsuitable for robust [multiplexing](@entry_id:266234) (detecting multiple targets in one tube) [@problem_id:5157262].

*   **Hydrolysis Probes (e.g., TaqMan)**: This chemistry provides a third layer of specificity. A short, sequence-specific oligonucleotide probe, labeled with a reporter [fluorophore](@entry_id:202467) on one end and a quencher on the other, is designed to bind to the target sequence between the PCR primers. The intact probe produces no signal due to quenching. During PCR extension, the DNA polymerase's $5' \to 3'$ nuclease activity cleaves the bound probe, separating the reporter from the quencher and generating a target-specific fluorescent signal. Because signal is generated only upon specific probe hybridization and cleavage, the method is highly specific and does not detect [primer-dimers](@entry_id:195290) or non-specific products. By using probes labeled with spectrally distinct reporter dyes, **[hydrolysis probes](@entry_id:199713) enable robust multiplex qPCR**, where multiple targets can be simultaneously quantified in a single reaction by monitoring different fluorescence channels [@problem_id:5157262].

#### Essential Controls for Valid Data

To ensure that the generated data are reliable, every RT-qPCR experiment must include a panel of controls. These are indispensable for troubleshooting and for validating the results of each run.

*   **No-Template Control (NTC)**: This reaction contains all assay reagents but no sample template. Its purpose is to detect contamination of reagents or the laboratory environment with target nucleic acid. Any signal in the NTC indicates contamination, which can invalidate results, especially for negative samples.

*   **No-Reverse-Transcriptase (No-RT) Control**: This reaction contains all reagents, including the sample template, but the reverse transcriptase enzyme is omitted. Its purpose is to test for signal originating from contaminating DNA. Since the DNA polymerase cannot use RNA as a template, any amplification in the No-RT control indicates the presence of a DNA template (e.g., gDNA or plasmid) that is being amplified, representing a false positive for RNA detection.

*   **Internal Positive Control (IPC)**: This is a control template added to every reaction, including test samples and controls. It can be an endogenous gene (a housekeeping gene) or, more robustly, an exogenous synthetic RNA molecule spiked in at a known concentration. The IPC serves as an omnibus control to monitor for reaction failure or inhibition within each individual tube. If a patient sample is negative for the target gene but the IPC also fails to amplify or shows a significantly delayed $C_t$, the result is invalid due to inhibition, preventing a dangerous false-negative report.

In a well-designed duplex assay for a target with $10^4$ initial RNA copies and an IPC with $10^3$ copies, one would expect the target to have a $C_t \approx 16.6$ and the IPC a $C_t \approx 19.9$. The NTC would show no target signal but an IPC signal at $\approx 19.9$ (confirming reaction competency), and the No-RT control would show no signal for either target [@problem_id:5157284].

#### Overcoming Inhibition in Clinical Samples

Clinical matrices such as blood, plasma, and urine are complex mixtures containing substances that can inhibit the enzymatic reactions of RT-PCR. Understanding their mechanisms is key to mitigation.

*   **Hemoglobin**: Carryover from red blood cells, specifically the heme [prosthetic group](@entry_id:174921), is a potent inhibitor. Heme can bind to polymerases and may promote oxidative damage. Mitigation strategies include thorough protein removal during RNA extraction, or adding a sacrificial protein like **bovine serum albumin (BSA)** to the reaction mix to sequester the heme [@problem_id:5157259].

*   **Heparin**: This common anticoagulant is a highly sulfated polyanion. It mimics the [nucleic acid backbone](@entry_id:177492) and inhibits by electrostatically binding to the positively charged DNA-binding cleft of polymerases and by sequestering essential $Mg^{2+}$ [cofactors](@entry_id:137503). The best mitigation is pre-analytical: avoiding heparin collection tubes. Post-extraction, samples can be treated with the enzyme **heparinase**, or the PCR can be supplemented with additional $Mg^{2+}$ [@problem_id:5157259].

*   **Urea**: Found in high concentrations in urine, urea is a **chaotrope**. It disrupts the hydrogen-bonding network of water, which in turn destabilizes the tertiary structure of proteins (denaturing the enzymes) and the duplex stability of nucleic acids (lowering the $T_m$ of primer-template hybrids). Mitigation involves diluting the sample, adding protein-stabilizing **compatible osmolytes** like betaine to the reaction, or lowering the PCR [annealing](@entry_id:159359) temperature to compensate for the reduced $T_m$ [@problem_id:5157259].

### From Raw Data to Biological Insight: Quantitative Analysis

For RT-qPCR to provide meaningful biological data, particularly in studies comparing gene expression between groups (e.g., cases vs. controls), the raw $C_t$ values must be properly normalized.

#### The Principle of Normalization

Technical variability is inherent in any multi-step laboratory process. In RT-PCR, sample-to-sample differences in initial cell count, RNA extraction efficiency, RNA quality, and reverse transcription efficiency can introduce significant non-biological variation. This variability introduces a [multiplicative scaling](@entry_id:197417) error on the measured quantities. To correct for this, data are normalized using one or more **reference genes** (often historically called [housekeeping genes](@entry_id:197045)). The core assumption of this approach is that the chosen reference gene is expressed at a constant level across all samples and is unaffected by the experimental conditions being studied [@problem_id:5157276]. By calculating the ratio of the gene of interest (GOI) to the reference gene (RG), sample-specific technical noise is cancelled out. In practice, this is typically done by calculating the delta-$C_t$: $\Delta C_t = C_{t, GOI} - C_{t, RG}$.

#### Choosing Stable Reference Genes

The validity of normalization hinges entirely on the stability of the chosen reference gene. A gene that is itself regulated by the experimental condition cannot serve as a stable baseline. Therefore, a critical preliminary step in any gene expression study is the validation of candidate reference genes. Several algorithms exist for this purpose, each with different strengths.

*   **geNorm**: This popular algorithm evaluates stability based on the pairwise variation of expression ratios among a set of candidate genes. It calculates a stability measure, $M$, for each gene and iteratively removes the least stable one. A key weakness of this approach is that it is easily misled by **co-regulated genes**. If two genes are transcriptionally regulated in the same manner, their expression ratio will be highly stable, and geNorm will erroneously rank them as the most stable candidates, even if both are strongly affected by the experimental condition.

*   **NormFinder**: This algorithm uses a more sophisticated model-based approach, akin to an Analysis of Variance (ANOVA). It explicitly estimates both the intra-group variation (random noise within a group) and the inter-group variation (systematic change between experimental groups). It then combines these into a single stability value, penalizing genes with high variation from either source. By directly modeling and penalizing the systematic inter-group difference, NormFinder is far more robust against being fooled by co-regulated genes. For instance, given two co-regulated genes that both show a systematic 2-fold upregulation in a disease state, geNorm might rank them highly, whereas NormFinder would penalize their large inter-group variation and correctly identify a different gene with minimal expression change between groups as the superior choice [@problem_id:5157276].

By carefully considering these foundational principles, from the catalytic action of a single enzyme to the statistical models for [data normalization](@entry_id:265081), a researcher can design, execute, and interpret RT-PCR assays with the rigor required for drawing valid scientific and clinical conclusions.