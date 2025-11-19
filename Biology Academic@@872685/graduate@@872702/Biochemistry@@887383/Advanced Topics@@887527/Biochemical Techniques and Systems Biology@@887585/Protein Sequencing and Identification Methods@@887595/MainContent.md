## Introduction
Determining the [amino acid sequence](@entry_id:163755) of proteins is a foundational pillar of modern biochemistry and molecular biology, providing the blueprint for cellular function and regulation. While genomics reveals the potential [proteome](@entry_id:150306), it is through direct protein analysis that we understand the expressed, modified, and interacting molecules that carry out biological processes. This article addresses the critical question of how scientists sequence and identify proteins, bridging the gap between historical chemical methods and the high-throughput technologies that define contemporary [proteomics](@entry_id:155660). The reader will embark on a journey from first principles to cutting-edge applications. The "Principles and Mechanisms" chapter will deconstruct the core techniques, from the elegant chemistry of Edman degradation to the complex physics of mass spectrometry, including ionization, mass analysis, and [peptide fragmentation](@entry_id:168952). Subsequently, the "Applications and Interdisciplinary Connections" chapter will showcase how these methods are applied to solve complex biological problems in quantitative, structural, and systems biology. Finally, the "Hands-On Practices" section will provide practical exercises to solidify understanding of key concepts like mass calculation and statistical validation. This structured approach will equip the reader with a deep and functional understanding of [protein sequencing](@entry_id:169225) and identification.

## Principles and Mechanisms

This chapter delves into the core principles and physicochemical mechanisms that underpin [protein sequencing](@entry_id:169225) and identification. We will begin with the classical chemical approach that laid the groundwork for the field, then transition to the suite of modern mass spectrometry-based techniques that define contemporary proteomics. The discussion will proceed logically from sample ionization to mass analysis, [peptide fragmentation](@entry_id:168952), and finally, the computational and statistical frameworks used to interpret the vast datasets generated.

### Classical Protein Sequencing: The Edman Degradation

Before the advent of [mass spectrometry](@entry_id:147216), the primary method for determining the amino acid sequence of a protein was through sequential chemical degradation. The most successful and widely adopted of these methods is the **Edman degradation**, a procedure that sequentially removes one amino acid at a time from the N-terminus of a peptide chain. Understanding its mechanism provides fundamental insights into peptide chemistry and the logic of [sequential analysis](@entry_id:176451).

The Edman degradation is a three-step cyclical process: coupling, cleavage, and conversion.

1.  **Coupling:** The peptide is treated with **phenyl [isothiocyanate](@entry_id:750868) (PITC)** under mildly basic conditions (typically pH $9.0$). PITC is an [electrophile](@entry_id:181327) that reacts with nucleophilic uncharged amino groups.

2.  **Cleavage:** After the coupling reaction, the reaction conditions are switched to strongly anhydrous acid (e.g., trifluoroacetic acid, TFA). This acidic environment promotes the cyclization of the newly modified N-terminal residue, which is then cleaved from the rest of the peptide chain as an anilinothiazolinone (ATZ) derivative.

3.  **Conversion and Identification:** The unstable ATZ-amino acid is extracted and converted under aqueous acidic conditions to a more stable **phenylthiohydantoin (PTH)-amino acid**. This PTH derivative is then identified, historically by reversed-phase [high-performance liquid chromatography](@entry_id:186409) (RP-HPLC), by comparing its retention time to that of known PTH-amino acid standards. The remaining peptide, now shortened by one residue, can be recovered and subjected to another cycle of the Edman degradation.

A critical feature of the Edman degradation is its selectivity for the N-terminal $\alpha$-amino group over the internal $\varepsilon$-amino groups of lysine residues. This selectivity is not absolute but is made highly effective through careful control of pH. The principle can be understood quantitatively using the **Henderson-Hasselbalch equation**:

$$
\mathrm{pH} = \mathrm{p}K_a + \log\left(\frac{[\text{Base}]}{[\text{Acid}]}\right)
$$

Here, the 'Base' is the deprotonated, nucleophilic form of the amino group ($-\mathrm{NH}_2$), and the 'Acid' is the protonated, non-nucleophilic form ($-\mathrm{NH}_3^+$). For the reaction with PITC to occur, the amino group must be in its deprotonated state. Let us consider a hypothetical peptide containing lysine, with a typical N-terminal $\alpha$-amino group pKa of $7.6$ and a lysine $\varepsilon$-amino group pKa of $10.5$. At the coupling pH of $9.0$, we can calculate the fraction of each amine that is deprotonated.

For the N-terminal $\alpha$-amine ($\mathrm{p}K_a = 7.6$):
$$
9.0 = 7.6 + \log\left(\frac{[-\mathrm{NH}_2]}{[-\mathrm{NH}_3^+]}\right) \implies \frac{[-\mathrm{NH}_2]}{[-\mathrm{NH}_3^+]} = 10^{1.4} \approx 25.1
$$
The fraction deprotonated is $\frac{25.1}{1+25.1} \approx 0.96$, or $96\%$.

For the lysine $\varepsilon$-amine ($\mathrm{p}K_a = 10.5$):
$$
9.0 = 10.5 + \log\left(\frac{[-\mathrm{NH}_2]}{[-\mathrm{NH}_3^+]}\right) \implies \frac{[-\mathrm{NH}_2]}{[-\mathrm{NH}_3^+]} = 10^{-1.5} \approx 0.0316
$$
The fraction deprotonated is $\frac{0.0316}{1+0.0316} \approx 0.03$, or $3\%$.

This calculation clearly demonstrates that at pH $9.0$, the N-terminal amine is overwhelmingly deprotonated and thus highly nucleophilic, while the lysine side-chain amine remains almost entirely protonated and unreactive. This difference in reactivity, rooted in their differing pKa values, is the chemical basis for the selectivity of the Edman degradation [@problem_id:2593814].

The iterative nature of the Edman degradation, which leaves the remainder of the peptide chain intact for subsequent cycles, distinguishes it fundamentally from earlier methods like Sanger's method. Sanger's reagent, 1-fluoro-2,4-dinitrobenzene (FDNB), irreversibly labels the N-terminal residue. To identify this labeled residue, the entire peptide must be hydrolyzed into its constituent amino acids, destroying the chain and preventing any further sequencing steps.

### Ionization: Bringing Biomolecules into the Gas Phase

While powerful, chemical methods like Edman degradation are low-throughput and require significant amounts of pure sample. Modern [proteomics](@entry_id:155660) relies on mass spectrometry, which can analyze complex mixtures with high speed and sensitivity. A mass spectrometer measures the **mass-to-charge ratio ($m/z$)** of gas-phase ions. The first challenge, therefore, is to convert large, non-volatile biomolecules like proteins and peptides from the solution or solid phase into gas-phase ions without breaking them apart. This is accomplished by "soft" ionization techniques.

#### Electrospray Ionization (ESI)

**Electrospray Ionization (ESI)** is a [soft ionization](@entry_id:180320) technique that generates ions directly from a solution, making it ideally suited for online coupling with [liquid chromatography](@entry_id:185688) (LC). In ESI, a sample solution is pumped through a narrow, conductive capillary held at a high electrical potential (several kilovolts) relative to a counter-electrode. The strong electric field at the capillary tip pulls charges to the liquid surface, forming a conical meniscus known as the **Taylor cone**. From the apex of this cone, a fine spray of charged microdroplets is emitted into a chamber at atmospheric pressure.

These droplets then shrink as the solvent evaporates, aided by a flow of warm drying gas (typically $\text{N}_2$). As the droplet volume decreases, the [charge density](@entry_id:144672) on its surface increases until the electrostatic repulsion between the charges overcomes the droplet's surface tension. This threshold is known as the **Rayleigh stability limit**. At this point, the droplet undergoes **Coulomb fission**, violently expelling a jet of smaller, more highly charged offspring droplets. This process of [evaporation](@entry_id:137264) and fission repeats, ultimately leading to the formation of gas-phase analyte ions. The precise mechanism of final ion formation is described by models such as the Ion Evaporation Model (IEM) and the Charged Residue Model (CRM).

A hallmark of ESI for proteins and large peptides is the production of a distribution of **multiply charged ions**. A protein with multiple basic residues (e.g., Lys, Arg, His, and the N-terminus) can be protonated at several sites. The extent of protonation, and thus the resulting charge state distribution, is highly dependent on the solution pH and the protein's primary sequence. Acidic conditions promote protonation and lead to higher charge states. A typical ESI mass spectrum for a single protein therefore shows a series of peaks, each corresponding to the same molecule with a different number of charges (e.g., $[M+nH]^{n+}$ for $n=..., 8, 9, 10, ...$). This multiple charging is advantageous, as it brings the $m/z$ of very large molecules into a range that is readily measurable by most mass analyzers. [@problem_id:2593797]

#### Matrix-Assisted Laser Desorption/Ionization (MALDI)

**Matrix-Assisted Laser Desorption/Ionization (MALDI)** is another dominant [soft ionization](@entry_id:180320) technique, but it operates on a different principle. The analyte is mixed with a large molar excess of a **matrix**—a small, organic molecule that strongly absorbs ultraviolet light at the wavelength of a specific laser. This mixture is spotted onto a sample plate and allowed to dry, co-crystallizing the analyte within the solid matrix.

A pulsed laser (e.g., a nitrogen laser at $337 \, \text{nm}$) is fired at the sample spot. The matrix absorbs the vast majority of the laser energy, causing it to rapidly heat and sublimate, creating a dense plume of gas-phase matrix and analyte molecules. In this plume, ionization occurs primarily through proton transfer from excited, acidic matrix molecules to the analyte.

In stark contrast to ESI, MALDI typically produces **predominantly singly charged ions**, such as $[M+H]^+$ or cationated species like $[M+Na]^+$ or $[M+K]^+$. While multiply charged ions can be observed, they are far less abundant. Because MALDI starts with a solid sample and uses a pulsed laser, its sample introduction is inherently pulsed and offline from continuous separation methods like LC. To couple LC with MALDI, fractions of the LC eluent must be collected and spotted onto a MALDI plate for subsequent analysis. [@problem_id:2593797]

### Mass Analysis: Sorting Ions by Mass-to-Charge Ratio

Once ions are formed, they are guided into a **[mass analyzer](@entry_id:200422)**, which separates them based on their mass-to-charge ratio ($m/z$). The diversity of mass analyzers is vast, but they can be grouped by their underlying physical principles.

#### Quadrupole Mass Filters

A **[quadrupole mass filter](@entry_id:189866)** consists of four parallel metal rods to which a combination of a constant **Direct Current (DC)** voltage and a sinusoidal **Radio Frequency (RF)** voltage is applied. This creates a time-varying quadrupolar electric field inside the device. The motion of an ion traveling through this field is described by the **Mathieu equation**, a [linear differential equation](@entry_id:169062) with periodic coefficients. The solutions to this equation are of two types: stable (the ion has a bounded trajectory and passes through the filter) or unstable (the ion's trajectory amplitude grows exponentially until it collides with a rod and is ejected).

For a given set of RF and DC parameters, only ions within a narrow range of $m/z$ values will have stable trajectories in both the x- and y-dimensions simultaneously. All other ions are filtered out. By systematically varying the RF and DC voltages, one can scan across a range of $m/z$ values, allowing sequential detection. Thus, the quadrupole acts as a tunable **band-pass filter for $m/z$**. [@problem_id:2593822]

#### Time-of-Flight (TOF) Analyzers

The principle of a **Time-of-Flight (TOF)** analyzer is conceptually simple and elegant. A packet of ions is accelerated by a fixed electrostatic potential difference, $\Delta\phi$. By the law of conservation of energy, each ion gains the same kinetic energy, $E_k = q\Delta\phi$, where $q$ is the ion's charge.

$$
q\Delta\phi = \frac{1}{2}mv^2
$$

From this, we can solve for the ion's velocity, $v$:

$$
v = \sqrt{\frac{2q\Delta\phi}{m}}
$$

The ions then enter a long, field-free "drift tube" of length $L$. The time, $t$, it takes for an ion to travel this distance is simply $t = L/v$. Substituting the expression for $v$, we get:

$$
t = L \sqrt{\frac{m}{2q\Delta\phi}} = \left(\frac{L}{\sqrt{2\Delta\phi}}\right) \sqrt{\frac{m}{q}}
$$

This crucial result shows that the flight time is proportional to the square root of the [mass-to-charge ratio](@entry_id:195338) ($t \propto \sqrt{m/z}$). Lighter ions (smaller $m/z$) travel faster and arrive at the detector first, while heavier ions (larger $m/z$) arrive later. By measuring the arrival times, the $m/z$ of each ion can be precisely determined. [@problem_id:2593822]

#### High-Resolution Trapping Analyzers: FT-ICR and Orbitrap

The highest-performing mass analyzers are those that trap ions and measure their properties over an extended period.

In a **Fourier Transform Ion Cyclotron Resonance (FT-ICR)** [mass spectrometer](@entry_id:274296), ions are trapped within a strong, [uniform magnetic field](@entry_id:263817) ($B$) and a weak electrostatic field. The magnetic field forces the ions into a circular path via the Lorentz force. The angular frequency of this motion, the **[cyclotron frequency](@entry_id:156231)** ($\omega_c$), is given by:

$$
\omega_c = \frac{qB}{m}
$$

Remarkably, this frequency is inversely proportional to the ion's $m/z$ and is independent of the ion's velocity or kinetic energy. The oscillating ions induce a faint image current on detector plates. This time-domain signal, which is a superposition of all the frequencies of the [trapped ions](@entry_id:171044), is recorded and then converted into a frequency-domain spectrum using a **Fourier Transform (FT)**. The frequency spectrum is easily converted to a mass spectrum.

The **Orbitrap** [mass analyzer](@entry_id:200422) is a more recent invention that achieves similarly high performance using only electrostatic fields. Ions are trapped around a central, spindle-shaped electrode. The clever geometry of the electric field forces ions into a complex motion: they simultaneously orbit the central electrode and oscillate along its axis. The frequency of this axial oscillation ($\omega_{axial}$) is given by:

$$
\omega_{axial} = \sqrt{\frac{Cq}{m}}
$$

where $C$ is a constant determined by the trap's geometry and applied voltages. Like in FT-ICR, this characteristic frequency is dependent on the ion's $m/z$ (specifically, $\propto \sqrt{q/m}$) and is independent of the ion's initial kinetic energy. The axial oscillations induce an image current that is processed by Fourier Transform to yield a high-resolution mass spectrum. [@problem_id:2593822]

### Tandem Mass Spectrometry (MS/MS): The Logic of Peptide Fragmentation

While a simple mass spectrum (MS1) provides the $m/z$ of intact peptides, it does not reveal their sequences. To obtain sequence information, we employ **[tandem mass spectrometry](@entry_id:148596) (MS/MS)**. In this process, a specific precursor ion of interest is isolated from the initial MS1 scan, subjected to an activation method that causes it to fragment, and then the $m/z$ ratios of the resulting fragment ions are measured in a second stage of mass analysis (MS2). The pattern of fragment ions is what allows us to deduce the peptide's sequence.

#### Peptide Fragmentation Nomenclature

Peptide fragmentation in MS/MS predominantly occurs along the backbone. The peptide backbone consists of a repeating sequence of three bonds: the $\mathrm{N-C_{\alpha}}$ bond, the $\mathrm{C_{\alpha}-C'}$ bond, and the $\mathrm{C'-N}$ bond (amide bond), where $\mathrm{C'}$ is the carbonyl carbon. Cleavage at any of these sites can produce a fragment ion. The **Roepstorff–Fohlman–Biemann nomenclature** is the standard system for classifying these fragments.

-   Fragments that retain the original N-terminus of the peptide are named **$a$, $b$,** or **$c$ ions**.
-   Fragments that retain the original C-terminus are named **$x$, $y$,** or **$z$ ions**.

The specific letter corresponds to the bond that was cleaved:
-   Cleavage of the $\mathbf{C_{\alpha}-C'}$ bond yields **$a$** and **$x$ ions**.
-   Cleavage of the **$\mathbf{C'-N}$** ([amide](@entry_id:184165)) bond yields **$b$** and **$y$ ions**.
-   Cleavage of the **$\mathbf{N-C_{\alpha}}$** bond yields **$c$** and **$z$ ions**.

The subscript index on a fragment ion, such as $b_n$ or $y_n$, indicates the number of amino acid residues contained within that fragment. For the $a, b, c$ series, residues are counted from the N-terminus; for the $x, y, z$ series, they are counted from the C-terminus. The mass difference between corresponding $a_n$ and $b_n$ ions is the mass of carbon monoxide ($\mathrm{CO}$, [nominal mass](@entry_id:752542) $28 \, \text{Da}$), as the $a_n$ ion is formally a $b_n$ ion that has lost its terminal carbonyl group. Because a peptide of length $L$ has $L-1$ peptide bonds, a maximum of $2(L-1)$ different $b$ and $y$ ions can be formed. [@problem_id:2593766]

#### Collision-Induced Dissociation (CID) and the Mobile Proton Model

The most common fragmentation method is **Collision-Induced Dissociation (CID)**, also known as Collisionally Activated Dissociation (CAD). In low-energy CID, typically performed in an [ion trap](@entry_id:192565), precursor ions are activated through multiple low-energy collisions with an inert gas (e.g., He). This is a "slow heating" process where kinetic energy is converted into internal vibrational energy, which then redistributes throughout the entire molecule before a bond breaks. Such a process is described as **ergodic**. Fragmentation occurs along the path of least resistance—the bond with the lowest activation energy for cleavage.

For a protonated peptide, the weakest bonds are not intrinsically the backbone bonds. The dominant fragmentation pathway is explained by the **Mobile Proton Model**. The ability of a chemical group to hold a proton in the gas phase is quantified by its **gas-phase basicity (GB)**, defined as the negative of the Gibbs free energy change for protonation ($GB(B) = -\Delta G^\circ_{\text{prot}}$). Side chains of residues like arginine and lysine have very high GB and act as strong "proton sinks."

The model posits that if the number of protons on a peptide is less than or equal to the number of high-GB sites, the protons will be sequestered there, and the peptide will be relatively stable and fragment poorly under CID. However, if the number of protons exceeds the number of high-GB sites, at least one proton becomes **mobile**. This mobile proton can migrate along the peptide backbone and transiently protonate a backbone amide group. Protonation of the amide carbonyl oxygen dramatically reduces the [resonance stabilization](@entry_id:147454) of the adjacent $\mathrm{C'-N}$ bond, lowering its bond order and creating a low-energy pathway for cleavage. This charge-directed fragmentation is why CID spectra are characteristically dominated by **$b$ and $y$ ions**. [@problem_id:2593779] [@problem_id:2593736]

Because CID is a low-energy, ergodic process, it also allows for other low-energy fragmentation channels to compete. This often results in the **neutral loss** of small, labile groups from [side chains](@entry_id:182203). Common examples include the loss of phosphoric acid ($\text{H}_3\text{PO}_4$, $-98 \, \text{Da}$) from phosphoserine/threonine, water ($\text{H}_2\text{O}$, $-18 \, \text{Da}$) from serine/threonine, and ammonia ($\text{NH}_3$, $-17 \, \text{Da}$) from lysine, glutamine, etc. These neutral losses can be so facile that they dominate the spectrum, suppressing the desired sequence-informative $b$ and $y$ ions. [@problem_id:2593712]

#### Higher-Energy Collisional Dissociation (HCD)

**Higher-energy Collisional Dissociation (HCD)** is a variant of CID that occurs in a "beam-type" collision cell rather than an [ion trap](@entry_id:192565). Ions are accelerated to a higher kinetic energy before colliding with the gas. While still a collisional method that produces primarily **$b$ and $y$ ions**, the faster and more energetic activation leads to some key differences. HCD spectra often show more extensive fragmentation across the entire peptide, with neutral loss pathways being less dominant relative to the backbone cleavages, leading to better [sequence coverage](@entry_id:170583).

Perhaps the most significant practical difference arises when HCD is coupled with a trapping analyzer like an Orbitrap. Unlike ion-trap CID, which suffers from a **low-mass cutoff** that prevents the detection of fragments below roughly one-third of the precursor's $m/z$, HCD with Orbitrap detection has no such limitation. This allows for the routine detection of low $m/z$ reporter ions, such as **immonium ions**. Immonium ions are small fragments corresponding to a single amino acid residue, and their presence or absence can help confirm the amino acid composition of the peptide. [@problem_id:2593712]

#### Electron Transfer/Capture Dissociation (ETD/ECD)

A complementary fragmentation paradigm is provided by electron-based methods, such as **Electron Capture Dissociation (ECD)** and **Electron Transfer Dissociation (ETD)**. These methods are fundamentally different from [collisional activation](@entry_id:187436). They require a multiply charged precursor cation ($z \geq 2$) and involve the transfer of a low-energy electron to the peptide. In ECD, the peptide captures a free electron directly. In ETD, the electron is transferred from a reagent radical anion.

This [electron capture](@entry_id:158629) event creates a charge-reduced, odd-electron radical species. This initiates a very fast, **non-ergodic** chemical reaction. A hydrogen atom (the captured electron plus a proton) is rapidly transferred to a backbone carbonyl oxygen, forming an aminoketyl radical intermediate. This radical species immediately induces homolytic cleavage of the adjacent, now-weakened **$\mathrm{N-C_{\alpha}}$ bond**. This entire process occurs on a picosecond timescale, much faster than [intramolecular vibrational energy redistribution](@entry_id:176374). The result is the highly specific formation of **$c$ and $z^\bullet$ ions**. [@problem_id:2593736]

The key advantage of this non-ergodic mechanism is that the fragmentation is a localized chemical event, not a global heating of the ion. As a result, weak, non-[covalent bonds](@entry_id:137054) and labile **[post-translational modifications](@entry_id:138431) (PTMs)**, such as phosphorylation or [glycosylation](@entry_id:163537), are not given time to dissociate. They are preserved intact on the $c$ and $z^\bullet$ fragments. This makes ETD and ECD the methods of choice for characterizing fragile PTMs that are often lost during CID. [@problem_id:2593737]

### From Spectra to Sequence: Principles of Database Searching

Generating MS/MS spectra is only half the battle. The final step is to interpret these complex [fragmentation patterns](@entry_id:201894) to identify the originating peptide sequence. This is most commonly done by searching the experimental spectra against a database of known protein sequences.

#### Peptide-Spectrum Matching and Scoring

For a given MS/MS spectrum, the process begins by using the measured precursor $m/z$ to identify all candidate peptide sequences from a database whose theoretical masses fall within a specified tolerance. For each candidate, a theoretical fragmentation spectrum is generated, typically predicting the $m/z$ values of its $b$- and $y$-ions (and other types, depending on the search parameters).

The core of the database search is the **scoring algorithm**, which quantifies the quality of the **peptide-spectrum match (PSM)**. Several principles are used:
-   **Shared Peak Counts and Inner Product:** The simplest scores are based on counting the number of experimental peaks that match a theoretical peak within a given mass tolerance. More sophisticated versions calculate a similarity metric, like a dot product or cosine score, between the experimental and theoretical spectra (represented as vectors), often weighting the match by the intensity of the experimental peaks. This rewards matches to more abundant fragment ions.
-   **Probability-Based Scoring:** Some engines (e.g., Mascot) calculate the probability that the observed match could have occurred by random chance. A high-quality match has a very low probability of being random. This probability ($P$) is often converted into a more intuitive score, such as $-10 \log_{10}(P)$, where higher scores indicate better, less-likely-by-chance matches.
-   **Cross-Correlation (XCorr):** Another powerful method (used by SEQUEST) preprocesses the experimental spectrum and then computes the discrete [cross-correlation function](@entry_id:147301) between it and the theoretical "stick" spectrum. The score is derived from the value of the correlation at zero lag, corrected for the average background correlation observed at other lags. This helps to distinguish true signal from systematic noise. [@problem_id:2593634]

#### Controlling Errors in Large-Scale Analyses

A typical proteomics experiment generates tens of thousands of MS/MS spectra, each resulting in a PSM. This constitutes a massive [multiple hypothesis testing](@entry_id:171420) problem, and a method is needed to control the rate of false-positive identifications.

The most widely accepted statistical framework for this is the **False Discovery Rate (FDR)**. The FDR is the expected proportion of incorrect identifications among all identifications that are accepted as correct. This is distinct from the more stringent **Family-Wise Error Rate (FWER)**, which is the probability of making even a single false-positive identification. For large-scale discovery sciences, controlling the FDR (e.g., at $0.01$, or $1\%$) is generally considered the appropriate balance between making new discoveries and maintaining statistical rigor. The **[q-value](@entry_id:150702)** of an individual PSM is its associated minimum FDR; it is the FDR that would be incurred if the significance threshold were set at that PSM's score.

The standard method for estimating the FDR in proteomics is the **target-decoy strategy**. A decoy database is constructed, typically by reversing each protein sequence from the real (target) database. This creates a decoy database of the same size and amino acid composition as the target database, but which should contain no sequences that are actually present in the sample. The experimental spectra are then searched against a concatenated database containing both target and decoy sequences.

The key assumption is that an incorrect match is equally likely to come from the target database as from the decoy database. Since all matches to the decoy database are, by definition, [false positives](@entry_id:197064), the number of decoy hits at a given score threshold provides a direct estimate of the number of false-positive target hits. The empirical FDR at a score threshold $s^*$ can then be estimated simply as:

$$
\widehat{\text{FDR}}(s^*) \approx \frac{\text{Number of decoy PSMs with score} \ge s^*}{\text{Number of target PSMs with score} \ge s^*}
$$

By calculating this value for every possible score threshold, a [q-value](@entry_id:150702) can be assigned to each PSM, providing a robust statistical foundation for every [peptide identification](@entry_id:753325) reported in the experiment. [@problem_id:2593854]