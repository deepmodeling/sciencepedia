## Introduction
Studying the [transcriptome](@entry_id:274025)—the full collection of RNA molecules in a cell—is fundamental to understanding gene regulation and cellular function. For decades, this analysis has depended on converting RNA into complementary DNA (cDNA) for sequencing, a process that introduces biases and erases critical layers of biological information. This reliance on an intermediate molecule creates a significant knowledge gap, obscuring the true complexity of RNA's role in health and disease. Long-read native RNA sequencing offers a revolutionary solution by interrogating the RNA molecule directly, capturing a complete and unaltered portrait of the [transcriptome](@entry_id:274025).

This article provides a comprehensive overview of this transformative technology. The first chapter, **Principles and Mechanisms**, will dissect how the technology works, from the biophysics of the nanopore sensor to the computational process of basecalling. Next, **Applications and Interdisciplinary Connections** will explore its impact across diverse fields, demonstrating its power in resolving complex isoforms, detecting cancer-associated gene fusions, and advancing clinical diagnostics. Finally, the **Hands-On Practices** section provides practical exercises to solidify your understanding of the data and its interpretation. We begin by exploring the distinctive paradigm of direct RNA sensing and the fundamental principles that set it apart from all other sequencing methodologies.

## Principles and Mechanisms

### The Distinctive Paradigm of Direct RNA Sensing

The analysis of the transcriptome, the complete set of RNA transcripts in a cell, has traditionally relied on converting RNA into more stable complementary DNA (cDNA) before sequencing. While powerful, these cDNA-based methods, whether short-read or long-read, are indirect. The enzymatic steps of **reverse transcription (RT)** and **Polymerase Chain Reaction (PCR)**, which are central to these workflows, introduce well-characterized biases and can lead to the loss of critical biological information.

**Long-read native RNA sequencing** represents a fundamental paradigm shift by interrogating the RNA molecule directly. This approach bypasses the enzymatic conversion and amplification steps, thereby preserving the native state of the transcript. The unique advantages of this method become clear when we consider the multiple layers of information encoded within an RNA molecule. Beyond the primary nucleotide sequence, a transcript's identity and function are defined by its full-length isoform structure, strand orientation, the length of its 3' polyadenosine tail, and a complex array of chemical modifications known as the [epitranscriptome](@entry_id:204405).

By sequencing the native molecule, this technology provides a direct and comprehensive view of the [transcriptome](@entry_id:274025) that is unattainable with other methods [@problem_id:4356006]. The key distinctions can be summarized as follows:

-   **Full-Length Splice-Junction Phasing ($\Phi$)**: Native long-read sequencing reads an entire RNA molecule from end to end in a single pass. This provides **direct measurement** of the connectivity of all exons and splice junctions within that specific molecule, unambiguously resolving complex isoforms. In contrast, short-read methods lose this information through fragmentation, requiring computational inference to reconstruct putative isoforms. cDNA-based [long-read sequencing](@entry_id:268696) also directly measures phasing, as it sequences full-length cDNA copies.

-   **Native Base Modification State ($M$)**: RNA molecules contain dozens of chemical modifications, such as **N6-methyladenosine ($m^6$A)**, which are not present in the standard A, C, G, T alphabet. Because native RNA sequencing measures the physical properties of the actual RNA strand, it can **directly detect** these modifications as subtle deviations in the sequencing signal. In all cDNA-based methods, this information is **lost** during [reverse transcription](@entry_id:141572), as the polymerase synthesizes a new strand using only the four canonical deoxyribonucleotides.

-   **Polyadenylation Tail Length ($\ell_{\text{poly(A)}}$)**: The poly(A) tail at the 3' end of messenger RNAs (mRNAs) is a critical regulator of stability and translation. Native RNA sequencing, which initiates at the 3' end, can **directly measure** the length of this homopolymeric tract on a per-molecule basis. Standard cDNA-based protocols, both long- and short-read, typically **lose** this information, as [reverse transcriptase](@entry_id:137829) does not efficiently copy the full tail and subsequent amplification does not preserve its original length.

-   **Strand Orientation ($S$)**: The specific molecular biology of the library preparation for native RNA sequencing ensures that the molecule is threaded through the sensor in a known, fixed orientation ($3' \to 5'$). This provides a **direct measurement** of the transcript's strand of origin. In contrast, both short-read and long-read cDNA methods rely on aligning the sequenced copy to a [reference genome](@entry_id:269221) to **infer** its original orientation.

The primary benefit of avoiding RT and PCR is the elimination of their associated artifacts [@problem_id:4356069]. Reverse transcription is prone to errors such as oligo(dT) primer mis-[annealing](@entry_id:159359) at internal A-rich tracts, premature truncation at regions of strong RNA secondary structure, and template switching that creates artificial chimeric molecules. PCR introduces its own distortions, including amplification biases related to GC-content and amplicon length, which can skew the apparent [relative abundance](@entry_id:754219) of transcripts. By omitting these steps, native RNA sequencing provides a more faithful quantitative and qualitative representation of the cellular [transcriptome](@entry_id:274025).

### The Nanopore as a Biophysical Sensor

The core of native RNA sequencing technology is a biological **nanopore**, a protein channel embedded in an electrically resistant membrane. When a voltage is applied across this membrane, a [steady flow](@entry_id:264570) of ions, primarily potassium and chloride, creates a measurable **ionic current**, denoted as $I_0$.

The sequencing process begins when a single-stranded RNA molecule, guided by a **motor protein**, is captured and threaded through the pore. As the RNA strand occupies the narrowest constriction of the pore, it physically obstructs the flow of ions. This causes a characteristic drop in the current to a new level, $I$. The magnitude of this current blockade is exquisitely sensitive to the physicochemical properties of the specific nucleotides residing within the pore's sensing region at that instant [@problem_id:4355974].

Crucially, the sensing region is not a single point but spans a short segment of the RNA strand, typically 5 to 6 nucleotides in length. This is known as the **[k-mer](@entry_id:177437) model**. The measured current level, $\mu$, is a function of the entire k-mer within the constriction, not just a single nucleotide. For a k-mer $s$, the observed current can be modeled as:

$I_n \approx V \left[G_0 - \Delta G(s_{n:n+k-1})\right]$

where $V$ is the applied voltage, $G_0$ is the open-pore conductance, and $\Delta G(s_{n:n+k-1})$ is the sequence-dependent reduction in conductance caused by the k-mer from position $n$ to $n+k-1$. This context-dependent signal is fundamental to the technology's ability to identify not only the canonical bases but also chemical modifications, which alter the k-mer's size, shape, and local electrostatics [@problem_id:4356050].

The translocation of the RNA is not a smooth, continuous process. It is controlled by a motor protein, often a helicase, that hydrolyzes ATP to ratchet the strand through the pore in discrete, single-nucleotide steps. The time the motor pauses between steps is known as the **dwell time**, $\tau$. This process is stochastic; under a simplified model where the motor's stepping has a [constant hazard rate](@entry_id:271158) $\lambda$, the dwell times for successive steps can be approximated as [independent random variables](@entry_id:273896) drawn from an [exponential distribution](@entry_id:273894) with a mean of $1/\lambda$ [@problem_id:4355974]. This results in a raw signal that appears as a series of current plateaus of variable width, where each plateau corresponds to a specific k-mer dwelling in the pore.

### Library Preparation: Enforcing Directional Translocation

A key requirement for interpretable sequencing data is knowing the direction in which the RNA molecule was read. Native RNA sequencing protocols employ a clever molecular biology strategy to enforce a strict **3' to 5' translocation direction**, ensuring that the first part of the signal corresponds to the 3' end of the transcript [@problem_id:4356044].

The process begins with the selective capture of polyadenylated mRNAs from a total RNA sample. This is achieved by using an adapter oligonucleotide that contains an **oligo(deoxythymidine)**, or oligo(dT), sequence. This oligo(dT) segment hybridizes specifically to the poly(A) tail found at the 3' end of most mature eukaryotic mRNAs, forming a short RNA:DNA duplex.

Next, a second, specialized **sequencing adapter** is attached. This adapter comes pre-loaded with the motor protein. Using a DNA ligase, this motor-bearing adapter is ligated to the oligo(dT)-containing adapter already anchored at the RNA's 3' end. The result is a stable molecular complex where the motor protein is precisely positioned at the 3' terminus of the target RNA molecule.

When this library is loaded onto the sequencing flow cell, the motor protein engages the single-stranded RNA and, upon ATP hydrolysis, begins to thread it through the nanopore. Because the motor is anchored at the 3' end and has a fixed polarity of action, it invariably feeds the RNA into the pore starting from the 3' end and proceeding towards the 5' end. This elegant molecular design guarantees that the resulting ionic current trace is a directional representation of the RNA sequence, starting with the poly(A) tail and ending with the [5' cap](@entry_id:147045).

### From Signal to Sequence: The Challenge of Basecalling

The process of converting the raw ionic current time series, $x_{1:T}$, into a nucleotide sequence, $y_{1:L}$, is known as **basecalling**. This is a formidable computational challenge due to several intrinsic features of the nanopore signal [@problem_id:4356016] [@problem_id:4356037].

The most significant challenge arises from **low-complexity sequences**, particularly homopolymer runs (e.g., `AAAAA` or `UUUUU`). As the motor protein steps through a homopolymer, the [k-mer](@entry_id:177437) in the sensing region changes minimally (e.g., `AAAAA` becomes `AAAAA`). Consequently, the mean current level remains nearly constant ($\Delta \mu \approx 0$). This makes it impossible to count the number of bases in the run by detecting discrete changes in the current level. Instead, the basecaller must estimate the length of the run based on the total time the signal spends at that constant level. However, because the dwell time for each step is a random variable, the total duration is also stochastic. This fundamental ambiguity leads to the characteristic error profile of [nanopore sequencing](@entry_id:136932): a higher rate of **[insertion and deletion (indel)](@entry_id:181140) errors**, especially within homopolymer regions. This issue is not resolved by simply increasing the [signal-to-noise ratio](@entry_id:271196), as the problem is a lack of distinguishing signal between states, not electronic noise [@problem_id:4356037]. Further complicating matters, the system's electronics introduce low-pass filtering, which can blur together very short, successive events, further degrading the ability to resolve individual steps.

Modern basecallers employ sophisticated machine learning models, primarily [deep neural networks](@entry_id:636170), to tackle this **alignment-free sequencing problem**. The model is given pairs of raw signals and the corresponding ground-truth sequences but not the exact alignment of which signal frames correspond to which base. Two dominant architectural paradigms are:

1.  **Connectionist Temporal Classification (CTC)**: CTC-based decoders learn to predict, for each time step in the signal, a probability distribution over the possible bases plus a special **blank symbol** ($\epsilon$). The final sequence is generated by collapsing the most probable path, first by removing repeated symbols and then removing all blanks. For example, a path `A-A-$\epsilon$-G-G` would collapse to `AG`. This mechanism elegantly handles the variable-length mapping between the signal and the sequence, naturally accounting for variable dwell times while enforcing a strict monotonic alignment between the signal and the base sequence [@problem_id:4356016].

2.  **Attention-Based Models**: More recent models, often based on the **Transformer** architecture, use an [encoder-decoder](@entry_id:637839) framework. The encoder processes the entire raw signal. The decoder then generates the output sequence one base at a time. At each step, an **[attention mechanism](@entry_id:636429)** allows the decoder to learn a "soft" alignment, weighing the importance of different parts of the entire input signal to predict the current base. Unlike CTC, this does not enforce a strict monotonic progression, allowing the model to integrate non-local, long-range signal context. This can be particularly powerful for resolving complex signals, such as those affected by RNA modifications or secondary structures.

### Unique Biological Insights from Native RNA Reads

The ability to directly measure the properties of native RNA molecules opens up avenues for biological inquiry and clinical diagnostics that are inaccessible to other methods. Rigorous validation of these unique features is paramount, particularly in a clinical setting, and relies on sequencing synthetic **spike-in controls** with a known ground truth [@problem_id:4356053].

#### Resolving the Epitranscriptome

Native RNA sequencing allows for the [direct detection](@entry_id:748463) of RNA modifications, which play critical roles in gene regulation. These modifications are identified by their characteristic perturbations of the [ionic current](@entry_id:175879) and/or dwell time signatures [@problem_id:4356050].

-   **N6-methyladenosine ($m^6$A)**: This modification involves the addition of a methyl group to the N6 position of adenine. The extra steric bulk of the methyl group alters the shape and conformation of the [k-mer](@entry_id:177437) within the pore, producing a context-dependent shift in the ionic current.
-   **Pseudouridine ($\Psi$)**: An isomer of uridine where the base is attached to the ribose via a C-C bond instead of an N-C bond. This change confers an additional [hydrogen bond donor](@entry_id:141108) and enhances local RNA stability. These changes to the [k-mer](@entry_id:177437)'s electronic and structural profile also result in a distinct current signal.

Furthermore, modifications can impact translocation kinetics. A modification that stabilizes the local RNA structure or alters the RNA's interaction with the motor protein can increase the [activation free energy](@entry_id:169953) ($\Delta G^{\ddagger}$) required for the motor to take a step. According to the Arrhenius-like relationship $k_{\text{step}} \propto \exp(-\Delta G^{\ddagger}/(k_\text{B} T))$, this increased energy barrier leads to a decreased stepping rate ($k_{\text{step}}$) and thus prolonged dwell times ($\tau$) at and near the modified site [@problem_id:4356050]. To validate the detection and quantification of these modifications, one can use synthetic RNA spike-ins containing a specific modification at a known position, mixed with their unmodified counterparts at defined ratios (e.g., $0.25, 0.50, 0.75$) to create a ground truth for modification stoichiometry [@problem_id:4356053].

#### Quantifying Poly(A) Tail Lengths

Because translocation proceeds from 3' to 5', the initial segment of a read from a polyadenylated RNA corresponds to its poly(A) tail. This appears as a long stretch of low-complexity signal. The length of this tail can be estimated by a time-to-length conversion [@problem_id:4355988].

The process requires careful calibration. A key parameter is the **non-stall translocation speed** ($v_\text{ns}$), which is the speed of the motor when it is actively moving. This speed can be calibrated by sequencing a spike-in control RNA with a precisely known poly(A) tail length ($L_{\text{spike}}$). The total time the spike-in's tail spends in the pore is calculated from the number of signal samples ($S_{\text{spike}}$) and the [sampling frequency](@entry_id:136613) ($f_s$). After accounting for the fraction of time spent in stalls ($q_{\text{spike}}$), the non-stall speed is calculated as:

$v_\text{ns} = \frac{L_{\text{spike}} \cdot f_s}{(1 - q_{\text{spike}}) \cdot S_{\text{spike}}}$

This calibrated speed can then be applied to estimate the tail length, $L$, of any sample read from its corresponding signal segment ($S$) and stall fraction ($q$):

$L = v_\text{ns} \cdot (1 - q) \cdot \frac{S}{f_s}$

This method enables the measurement of poly(A) tail length distributions for every gene at single-molecule resolution. Validation of this feature requires spike-ins with discrete, known tail lengths (e.g., 20, 60, 100 nt) [@problem_id:4356053].

#### Interrogating RNA Secondary Structure

RNA molecules are not simple linear chains; they fold into complex **secondary structures** like hairpins and stem-loops. These structures can also be detected by native RNA sequencing because they physically impede translocation [@problem_id:4355976].

When the motor protein encounters a stable hairpin, it must exert force to unwind the duplex. This presents a significant kinetic barrier, dramatically slowing or temporarily halting translocation. The resulting signal is characterized by:

-   **Prolonged Dwell Times**: The motor spends significantly more time trying to resolve the structure, leading to a cluster of unusually long dwell times.
-   **Increased Current Variance**: As the structure fluctuates between partially folded and unfolded states at the mouth of the pore, the ionic current becomes more variable and noisy than in unstructured regions.

These dual signatures—kinetic and electrical—can be used to build statistical detectors, such as a **Generalized Likelihood Ratio Test (GLRT)**, to computationally map regions of secondary structure along a transcript *in situ*. This provides a powerful tool for studying the relationship between RNA structure and function at a [transcriptome](@entry_id:274025)-wide scale.