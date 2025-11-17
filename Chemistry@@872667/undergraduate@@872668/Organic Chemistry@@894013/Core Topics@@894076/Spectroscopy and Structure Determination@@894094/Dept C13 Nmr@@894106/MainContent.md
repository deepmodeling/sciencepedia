## Introduction
Carbon-13 Nuclear Magnetic Resonance (¹³C NMR) spectroscopy is one of the most powerful tools for determining a molecule's carbon framework. However, a standard broadband-decoupled spectrum, while providing a census of all unique carbon atoms, has a significant limitation: it offers no direct information about the number of hydrogen atoms attached to each carbon. This knowledge gap is elegantly filled by a sophisticated technique known as Distortionless Enhancement by Polarization Transfer, or DEPT. DEPT NMR not only boosts the inherently weak ¹³C signal but also "edits" the spectrum to differentiate between [methine](@entry_id:185756) ($\text{CH}$), [methylene](@entry_id:200959) ($\text{CH}_2$), and methyl ($\text{CH}_3$) groups, providing an essential layer of structural information.

This article provides a comprehensive guide to understanding and applying DEPT NMR spectroscopy. Across the following sections, you will gain a robust theoretical and practical foundation in this indispensable technique.
- The first section, **"Principles and Mechanisms,"** delves into the core concept of [polarization transfer](@entry_id:753553) from ¹H to ¹³C nuclei and explains how manipulating a final pulse angle allows for the creation of the distinct DEPT-90 and DEPT-135 experiments.
- The second section, **"Applications and Interdisciplinary Connections,"** demonstrates how chemists use DEPT spectra in synergy with other data to solve complex structural puzzles, monitor the progress of chemical reactions, and probe materials at a molecular level.
- Finally, the **"Hands-On Practices"** section offers a series of problems designed to build your skills and confidence in applying these principles to interpret real-world NMR data and solve for unknown structures.

## Principles and Mechanisms

While a standard broadband-decoupled ¹³C NMR spectrum provides a full census of all unique carbon environments within a molecule, it offers no direct information about the number of hydrogen atoms attached to each carbon. To bridge this gap, a family of powerful pulse sequences known as **Distortionless Enhancement by Polarization Transfer (DEPT)** has been developed. DEPT experiments not only enhance the typically weak ¹³C signal but also edit the resulting spectrum to selectively display or differentiate carbon atoms based on their multiplicity, that is, whether they are part of a [methine](@entry_id:185756) ($\text{CH}$), [methylene](@entry_id:200959) ($\text{CH}_2$), or methyl ($\text{CH}_3$) group. This chapter elucidates the fundamental principles governing the DEPT experiment and the mechanisms by which this spectral editing is achieved.

### The Fundamental Principle: Polarization Transfer

The core concept behind DEPT is **[polarization transfer](@entry_id:753553)**. In NMR, signal strength is proportional to the population difference between [nuclear spin](@entry_id:151023) states, a property known as polarization. The proton (¹H) nucleus possesses a significantly larger [gyromagnetic ratio](@entry_id:149290) and nearly 100% natural abundance, making it far more polarized and thus more "sensitive" than the ¹³C nucleus (which has a smaller [gyromagnetic ratio](@entry_id:149290) and only ~1.1% natural abundance). The DEPT experiment cleverly exploits this fact by transferring the much larger polarization of directly attached protons to their neighboring ¹³C nuclei, resulting in a substantial [signal enhancement](@entry_id:754826).

This transfer is not magical; it is mediated by a specific physical interaction: the **one-bond [scalar coupling](@entry_id:203370)** (or **J-coupling**) between a carbon and its directly bonded proton, denoted as ${}^1J_{\text{CH}}$. The DEPT [pulse sequence](@entry_id:753864) contains a series of precisely timed radiofrequency pulses and delays that manipulate the spins of both ¹H and ¹³C nuclei. For the [polarization transfer](@entry_id:753553) to occur, the ${}^1J_{\text{CH}}$ coupling must be present to act as a conduit.

This stringent requirement leads to a foundational rule of all DEPT experiments: only carbons with directly attached protons can produce a signal. Consequently, two major classes of carbons are systematically absent from DEPT spectra:

1.  **Quaternary Carbons ($\text{C}$)**: A carbon atom bonded to four other non-hydrogen atoms has no directly attached protons. Therefore, the ${}^1J_{\text{CH}}$ coupling pathway required for [polarization transfer](@entry_id:753553) does not exist. Such carbons are "invisible" to the DEPT experiment. A common and important example is the carbonyl carbon in ketones, esters, and [amides](@entry_id:182091), which, being quaternary, will not appear in any DEPT spectrum [@problem_id:2166622].

2.  **Solvent Carbons without C-H Bonds**: In many NMR experiments, [deuterated solvents](@entry_id:748344) are used. A ubiquitous example is deuterated chloroform, $\text{CDCl}_3$. While this solvent contains carbon, the carbon is bonded to a deuterium ($^2\text{H}$) nucleus, not a protium ($^1\text{H}$) nucleus. The DEPT [pulse sequence](@entry_id:753864) is specifically designed to interact with the spins of ¹H. Since the carbon in $\text{CDCl}_3$ lacks a bond to a ¹H atom, the [polarization transfer](@entry_id:753553) mechanism cannot be initiated, and the solvent signal is absent from DEPT spectra [@problem_id:2166575].

This principle of [polarization transfer](@entry_id:753553) via ${}^1J_{\text{CH}}$ coupling is the first and most crucial filter applied by the DEPT technique, determining which carbons are observed and which are silenced.

### Spectral Editing: The Role of the Final Pulse Angle

Simply enhancing the signals of protonated carbons is useful, but the true power of DEPT lies in its ability to **edit** the spectrum—that is, to differentiate between $\text{CH}$, $\text{CH}_2$, and $\text{CH}_3$ groups. This editing is accomplished by a specific pulse in the sequence, often called the "editing pulse," which is a proton pulse of a defined angle, $\theta$.

The phase (i.e., whether a peak points up or down) and intensity of the final, observed ¹³C signal for a $\text{CH}_n$ group (where $n=1, 2, \text{ or } 3$) are a direct function of both $n$ and this editing angle $\theta$. While the full derivation using the product [operator formalism](@entry_id:180896) is beyond the scope of this text, the outcome is remarkably elegant. In an idealized model, the phase of the detected signal is governed by a simple trigonometric relationship [@problem_id:2166594]:

$$ \text{Signal Phase} \propto \sin(n\theta) $$

This relationship is the key to understanding how different DEPT experiments work:

-   For a **[methine](@entry_id:185756) ($\text{CH}$)** group, $n=1$, and the signal phase depends on $\sin(\theta)$.
-   For a **methylene ($\text{CH}_2$)** group, $n=2$, and the signal phase depends on $\sin(2\theta)$.
-   For a **methyl ($\text{CH}_3$)** group, $n=3$, and the signal phase depends on $\sin(3\theta)$.

By choosing specific values for the angle $\theta$, a chemist can control which types of carbons appear and with what phase, effectively creating different "views" of the molecule's carbon framework.

### The Standard DEPT Experiments: DEPT-90 and DEPT-135

In practice, chemists primarily rely on two standard DEPT experiments, defined by their choice of the editing angle $\theta$.

#### DEPT-90: Isolating Methine (CH) Carbons

When the editing pulse angle is set to $\theta = 90^\circ$ ($\frac{\pi}{2}$ radians), the experiment is known as **DEPT-90**. Let's examine the outcome for each carbon type using our phase relationship:

-   **$\text{CH}$ ($n=1$)**: Phase $\propto \sin(1 \cdot 90^\circ) = \sin(90^\circ) = +1$. The signal is **positive**.
-   **$\text{CH}_2$ ($n=2$)**: Phase $\propto \sin(2 \cdot 90^\circ) = \sin(180^\circ) = 0$. The signal is **absent**.
-   **$\text{CH}_3$ ($n=3$)**: Phase $\propto \sin(3 \cdot 90^\circ) = \sin(270^\circ) = -1$. While this suggests a negative signal, a more complete intensity model reveals that the $\text{CH}_3$ signal is also nullified at this angle. The intensity of a $\text{CH}_3$ peak can be modeled as being proportional to $3\sin(\theta)\cos^2(\theta)$, which evaluates to $0$ when $\theta = 90^\circ$ [@problem_id:2166614].

The result is unambiguous: the DEPT-90 spectrum is a sub-spectrum that exclusively displays signals for [methine](@entry_id:185756) ($\text{CH}$) carbons. All other carbon types ($\text{C}$, $\text{CH}_2$, and $\text{CH}_3$) are suppressed.

#### DEPT-135: The Comprehensive Editing Spectrum

The most commonly used variant is the **DEPT-135** experiment, where the editing angle is set to $\theta = 135^\circ$ ($\frac{3\pi}{4}$ radians). This angle is chosen because it provides a unique and clear signature for all three types of protonated carbons simultaneously:

-   **$\text{CH}$ ($n=1$)**: Phase $\propto \sin(1 \cdot 135^\circ) \approx +0.707$. The signal is **positive**.
-   **$\text{CH}_2$ ($n=2$)**: Phase $\propto \sin(2 \cdot 135^\circ) = \sin(270^\circ) = -1$. The signal is **negative**.
-   **$\text{CH}_3$ ($n=3$)**: Phase $\propto \sin(3 \cdot 135^\circ) = \sin(405^\circ) = \sin(45^\circ) \approx +0.707$. The signal is **positive**.

This leads to the well-known empirical rules for interpreting a DEPT-135 spectrum:
-   **Positive signals** correspond to $\text{CH}$ and $\text{CH}_3$ groups.
-   **Negative signals** correspond to $\text{CH}_2$ groups.
-   **Absent signals** correspond to quaternary ($\text{C}$) carbons.

The choice of $135^\circ$ is a pragmatic compromise that yields strong, distinguishable signals for all protonated carbon types. A more detailed intensity analysis shows that with this angle, the relative theoretical intensities for $\text{CH}$, $\text{CH}_2$, and $\text{CH}_3$ groups are approximately $0.67$, $-0.94$, and $1.00$, respectively, after normalization [@problem_id:2166581]. This confirms that all three groups give rise to robust signals, making DEPT-135 an exceptionally efficient tool for [multiplicity](@entry_id:136466) assignment.

### A Synergistic Approach to Structure Elucidation

While each DEPT experiment provides valuable information, no single spectrum tells the whole story. A robust structural analysis requires a synergistic combination of a standard broadband-decoupled ¹³C spectrum with one or more DEPT experiments.

First and foremost, one must always acquire a **standard broadband-decoupled ¹³C spectrum**. This spectrum serves as the master inventory, revealing the [chemical shift](@entry_id:140028) of every unique carbon in the molecule. The DEPT spectra are then used to sort these carbons into bins. Specifically, any peak appearing in the broadband spectrum but absent from the DEPT-135 spectrum must be a **quaternary ($\text{C}$) carbon** [@problem_id:2166576].

The DEPT-135 spectrum then provides the next level of sorting. All negative peaks are unambiguously assigned as $\text{CH}_2$ carbons. However, ambiguity remains for the positive peaks, which could be either $\text{CH}$ or $\text{CH}_3$ carbons.

This is precisely where the **DEPT-90** spectrum becomes indispensable. Since the DEPT-90 spectrum exclusively shows $\text{CH}$ carbons, it serves as the definitive tool to resolve the ambiguity within the positive peaks of the DEPT-135 spectrum [@problem_id:2166605]. Any peak appearing in the DEPT-90 spectrum is a $\text{CH}$ group. Consequently, any positive peak in the DEPT-135 spectrum that does *not* appear in the DEPT-90 spectrum must be a $\text{CH}_3$ group.

This logical workflow can be summarized as follows:
1.  **Identify all carbons** using the broadband ¹³C spectrum.
2.  **Identify quaternary ($\text{C}$) carbons** by subtracting all peaks from the DEPT-135 spectrum from the broadband spectrum.
3.  **Identify $\text{CH}_2$ carbons** as the negative peaks in the DEPT-135 spectrum.
4.  **Identify $\text{CH}$ carbons** as the peaks in the DEPT-90 spectrum.
5.  **Identify $\text{CH}_3$ carbons** as the positive peaks in the DEPT-135 spectrum that are absent in the DEPT-90 spectrum.

For instance, consider an unknown compound whose spectra reveal the following: the DEPT-90 spectrum shows a single positive signal, while the DEPT-135 spectrum shows three positive signals and one negative signal [@problem_id:2166633]. Following our workflow, we deduce:
-   From DEPT-90, there is exactly one type of **$\text{CH}$** group.
-   From DEPT-135 (negative signal), there is exactly one type of **$\text{CH}_2$** group.
-   From DEPT-135 (positive signals), there are a total of three $\text{CH}$ or $\text{CH}_3$ groups. Since we already know one of these is a $\text{CH}$ group (from DEPT-90), the remaining $3 - 1 = 2$ positive signals must correspond to two distinct **$\text{CH}_3$** groups.
The compound thus contains one $\text{CH}$, one $\text{CH}_2$, and two $\text{CH}_3$ environments.

### Advanced Topics and Practical Considerations

While the principles outlined above provide a robust framework for interpreting DEPT spectra, real-world applications require an appreciation for some additional complexities.

#### Quantitative Analysis with DEPT

A common pitfall is to assume that the integrated areas of DEPT signals can be used for straightforward [quantitative analysis](@entry_id:149547), such as determining the [molar ratio](@entry_id:193577) of compounds in a mixture. This is generally incorrect. For example, if a student were analyzing an incomplete reaction mixture and integrated all positive peaks for the reactant and all positive peaks for the product, the resulting ratio would likely be misleading. This is because the reactant and product molecules may contain different numbers of $\text{CH}$ and $\text{CH}_3$ carbons, meaning their total positive signal per mole is different [@problem_id:2166595]. For the [hydroboration-oxidation](@entry_id:186160) of 1-methylcyclopentene, the reactant has two carbons (one $\text{CH}$, one $\text{CH}_3$) contributing to the positive DEPT-135 signal, whereas the product, 2-methylcyclopentanol, has three (two $\text{CH}$, one $\text{CH}_3$). A direct comparison of the total positive integrals would therefore overestimate the amount of product by a factor of $\frac{3}{2}$. True quantitative analysis with DEPT requires a careful, peak-by-peak comparison or normalization based on the known carbon count for each signal type.

#### The Influence of the $^1J_{CH}$ Coupling Constant

The efficiency of the [polarization transfer](@entry_id:753553) at the heart of the DEPT experiment is critically dependent on the value of the one-bond C-H [coupling constant](@entry_id:160679), ${}^1J_{\text{CH}}$. The time delays in the [pulse sequence](@entry_id:753864) are optimized for a specific, average [coupling constant](@entry_id:160679), typically denoted $J_{\text{opt}}$, often set around $145$ Hz to accommodate a range of common carbon types.

However, the actual ${}^1J_{\text{CH}}$ value for a given C-H bond varies, primarily with the hybridization of the carbon atom: $sp$-hybridized carbons exhibit the largest couplings (e.g., $\sim 250$ Hz for an alkynyl C-H), followed by $sp^2$-hybridized carbons ($\sim 160$ Hz), and then $sp^3$-hybridized carbons ($\sim 125$ Hz). When the actual ${}^1J_{\text{CH}}$ of a carbon deviates significantly from $J_{\text{opt}}$, the [polarization transfer](@entry_id:753553) becomes less efficient, and the resulting signal intensity is attenuated. The intensity follows a sinusoidal dependence on the ratio of the coupling constants, which for a DEPT-90 experiment can be modeled as $I \propto |\sin(\frac{\pi J_{CH}}{J_{\text{opt}}})|$ [@problem_id:2166631].

This effect has important practical consequences. For a molecule containing both an alkyl $\text{CH}$ group ($J_{CH} \approx 130$ Hz) and a [terminal alkyne](@entry_id:193059) $\text{CH}$ group ($J_{CH} \approx 248$ Hz), a DEPT-90 spectrum run with $J_{\text{opt}} = 145$ Hz will show a significantly weaker signal for the alkynyl carbon than for the alkyl carbon, purely due to this mismatch in coupling constants. This serves as a crucial reminder that while DEPT is an outstanding qualitative tool for identifying [carbon multiplicity](@entry_id:747134), the relative intensities of different peaks within a single DEPT spectrum must be interpreted with caution, as they are modulated by factors beyond simple molar concentration.