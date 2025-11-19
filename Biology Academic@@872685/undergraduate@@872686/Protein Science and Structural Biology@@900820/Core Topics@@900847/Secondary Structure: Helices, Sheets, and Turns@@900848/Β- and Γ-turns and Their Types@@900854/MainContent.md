## Introduction
The functional form of a protein is a complex, three-dimensional marvel, dictated not just by its regular secondary structures like α-helices and β-sheets, but also by the short, elegant segments that connect them. These connecting elements, known as turns, are essential for reversing the polypeptide chain's direction, enabling the compact, globular architecture required for biological activity. A central challenge in [structural biology](@entry_id:151045) is understanding how these turns achieve their specific conformations and what rules govern their formation. This article demystifies two of the most fundamental motifs: the [β-turn](@entry_id:181262) and the [γ-turn](@entry_id:185283).

In the chapters that follow, you will gain a comprehensive understanding of these crucial structural elements. The first chapter, **Principles and Mechanisms**, will lay the groundwork by defining turns, distinguishing them from loops, and detailing the classification and stabilizing forces of β- and γ-turns, including the stereochemical roles of key amino acids. Next, **Applications and Interdisciplinary Connections** will explore the broader impact of turns, from their role in [protein stability](@entry_id:137119) and [molecular recognition](@entry_id:151970) to their involvement in disease and as targets in modern drug discovery. Finally, **Hands-On Practices** will provide opportunities to apply this knowledge, challenging you to classify turns from structural data and predict their formation from amino acid sequences.

## Principles and Mechanisms

The intricate three-dimensional architecture of a protein is not constructed solely from long stretches of regular secondary structures like $\alpha$-helices and $\beta$-sheets. Equally crucial are the connecting segments that enable the polypeptide chain to reverse direction, facilitating the compact, globular folds characteristic of functional proteins. These chain reversals are often accomplished by short, well-defined structural motifs known as **turns**. This chapter will explore the principles governing the structure and classification of the most fundamental of these motifs: the [β-turn](@entry_id:181262) and the [γ-turn](@entry_id:185283).

### Distinguishing Turns from Loops

While both turns and the more general **loops** (or coils) serve to connect regular secondary structure elements, a critical distinction lies in their structural definition. A defined turn, such as a β- or [γ-turn](@entry_id:185283), is characterized by a specific, recurring intramolecular hydrogen-bonding pattern that stabilizes a compact chain reversal over a fixed number of residues. These motifs also exhibit characteristic sets of backbone [dihedral angles](@entry_id:185221). In contrast, loops are more structurally heterogeneous. They can vary widely in length and conformation and, while they may contain incidental hydrogen bonds, they lack the specific, defining hydrogen-bond pattern that typifies a turn [@problem_id:2151434]. Turns are thus considered a distinct class of secondary structure, whereas loops are regions that lack assignment to any regular [secondary structure](@entry_id:138950) element.

### The γ-Turn: A Three-Residue Reversal

The tightest and simplest defined turn is the **[γ-turn](@entry_id:185283)**. This motif involves three consecutive amino acid residues, conventionally indexed as $i$, $i+1$, and $i+2$. The defining feature of a classic [γ-turn](@entry_id:185283) is a single [intramolecular hydrogen bond](@entry_id:750785) that creates a seven-membered pseudo-ring. This bond forms between the carbonyl oxygen ($-\mathrm{C{=}O}$) of residue $i$ and the amide hydrogen ($-\mathrm{NH}-$) of residue $i+2$ [@problem_id:2151380]. In this interaction, the carbonyl oxygen acts as the [hydrogen bond acceptor](@entry_id:139503), and the amide group acts as the [hydrogen bond donor](@entry_id:141108).

The classic [γ-turn](@entry_id:185283) requires the central residue, $i+1$, to adopt backbone [dihedral angles](@entry_id:185221) ($\phi$, $\psi$) that are in a sterically strained region of the Ramachandran plot. This inherent strain, combined with the less-than-ideal geometry of the [hydrogen bond](@entry_id:136659) within the tight seven-membered ring, makes the classic [γ-turn](@entry_id:185283) significantly less common in proteins than its larger counterpart, the [β-turn](@entry_id:181262). A variation, the **inverse [γ-turn](@entry_id:185283)**, utilizes more favorable [dihedral angles](@entry_id:185221) and is more frequently observed.

### The β-Turn: The Archetypal Four-Residue Turn

The **[β-turn](@entry_id:181262)** is the most common type of turn found in proteins, playing a pivotal role in creating antiparallel $\beta$-sheets and enabling the [polypeptide chain](@entry_id:144902) to fold back upon itself. A [β-turn](@entry_id:181262) spans four consecutive amino acid residues, indexed $i$, $i+1$, $i+2$, and $i+3$.

The primary stabilizing feature of a [β-turn](@entry_id:181262) is a characteristic [intramolecular hydrogen bond](@entry_id:750785) formed between the backbone carbonyl oxygen of residue $i$ and the backbone amide hydrogen of residue $i+3$ [@problem_id:2151394]. This $i \to i+3$ interaction closes a ten-membered pseudo-ring, which is large enough to permit a nearly ideal, low-strain [hydrogen bond geometry](@entry_id:191901). For instance, in a peptide segment where the four residues `Ser-Val-Gly-Asn` form a [β-turn](@entry_id:181262), the stabilizing [hydrogen bond](@entry_id:136659) would be established between the carbonyl oxygen of Serine (residue $i$) and the [amide](@entry_id:184165) hydrogen of Asparagine (residue $i+3$) [@problem_id:2151394].

### Classification of β-Turns by Backbone Geometry

[β-turns](@entry_id:176784) are not a single, rigid structure but rather a family of conformations. They are primarily classified into different types based on the backbone [dihedral angles](@entry_id:185221), $\phi$ and $\psi$, of the two central residues, $i+1$ and $i+2$.

#### Type I and Type II Turns

The two most common [β-turn](@entry_id:181262) classes are Type I and Type II. They share similar conformations for residue $i+1$ but differ dramatically at residue $i+2$. The ideal [dihedral angles](@entry_id:185221) are:

*   **Type I β-Turn**:
    *   Residue $i+1$: $(\phi, \psi) \approx (-60^\circ, -30^\circ)$
    *   Residue $i+2$: $(\phi, \psi) \approx (-90^\circ, 0^\circ)$ [@problem_id:2151392]

*   **Type II β-Turn**:
    *   Residue $i+1$: $(\phi, \psi) \approx (-60^\circ, 120^\circ)$
    *   Residue $i+2$: $(\phi, \psi) \approx (80^\circ, 0^\circ)$

The most profound structural consequence of these different [dihedral angles](@entry_id:185221) lies in the orientation of the planar peptide group that links residues $i+1$ and $i+2$. In a Type II turn, this peptide plane is effectively flipped by approximately $180^\circ$ relative to its orientation in a Type I turn. This reorientation causes the carbonyl oxygen of residue $i+1$ to point in nearly the opposite direction from where it points in a Type I turn, a visually striking difference that arises directly from the distinct values of $\psi_{i+1}$ and $\phi_{i+2}$ [@problem_id:2151399].

#### Prime Turns: The Mirror Images

For every major turn type, there exists a corresponding **prime (') turn**, which is its stereochemical mirror image. For instance, a **Type I' [β-turn](@entry_id:181262)** is the mirror image of a Type I turn. This relationship means that the [dihedral angle](@entry_id:176389) pairs ($\phi, \psi$) for the central residues are inverted in sign relative to the non-prime version.

*   **Type I' β-Turn**:
    *   Residue $i+1$: $(\phi, \psi) \approx (60^\circ, 30^\circ)$
    *   Residue $i+2$: $(\phi, \psi) \approx (90^\circ, 0^\circ)$ [@problem_id:2151417]

Prime turns are sterically favored when the constituent amino acids have the opposite chirality to the rest of the protein; for example, they can accommodate a D-amino acid within a polypeptide chain otherwise composed of L-amino acids. The same principle applies to Type II and II' turns.

#### Type VI Turns and the *cis*-Peptide Bond

While most [β-turns](@entry_id:176784) are defined by their [dihedral angles](@entry_id:185221), the **Type VI turn** is uniquely characterized by a different conformational feature: the presence of a ** *cis*-[peptide bond](@entry_id:144731)** between residues $i+1$ and $i+2$. In most proteins, over $99.9\%$ of peptide bonds are in the lower-energy *trans* configuration. The exception is often found with [proline](@entry_id:166601) residues. Due to its cyclic side chain, the energy difference between the *cis* and *trans* conformations of an X-Pro peptide bond is much smaller. Consequently, Type VI turns almost always have a **proline** residue at position $i+2$, as this stabilizes the requisite *cis* conformation of the preceding [peptide bond](@entry_id:144731) [@problem_id:2151425].

### The Role of Specific Amino Acids in Turn Formation

The observation that certain amino acids appear with high frequency at specific positions within turns is not coincidental. It is a direct consequence of their unique stereochemical properties.

#### Proline at Position *i*+1

Proline is frequently found at the $i+1$ position of Type I [β-turns](@entry_id:176784). The reason for this high propensity is structural pre-organization. Proline is unique among the [standard amino acids](@entry_id:166527) because its side chain is a cyclic structure that links back to its own backbone nitrogen atom. This ring severely restricts the rotational freedom around the N-Cα bond, constraining the $\phi$ [dihedral angle](@entry_id:176389) to a value of approximately $-60^\circ$. This value is an almost perfect match for the ideal $\phi_{i+1}$ angle required for a Type I turn. By having this conformationally restricted residue at the $i+1$ position, the polypeptide chain is already "pre-organized" into the correct turn geometry, which significantly reduces the entropic penalty associated with folding the chain into this specific motif [@problem_id:2151407].

#### Glycine at Position *i*+2

Just as proline is favored at $i+1$ in Type I turns, glycine shows an overwhelming preference for the $i+2$ position in Type II [β-turns](@entry_id:176784). The structural basis for this lies in a severe [steric hindrance](@entry_id:156748) inherent to the Type II conformation. The required [dihedral angles](@entry_id:185221) for residue $i+2$ in a Type II turn, particularly the positive $\phi_{i+2}$ value of $\approx 80^\circ$, force the side chain of this residue into close proximity with the carbonyl oxygen of the preceding residue ($i+1$). For any amino acid with a side chain larger than a hydrogen atom (i.e., any residue with a Cβ atom), this proximity results in a severe van der Waals clash, making the conformation energetically prohibitive. Glycine, with only a single hydrogen atom as its side chain, is the only residue that can comfortably occupy this position without incurring the steric penalty [@problem_id:2151424]. This makes the presence of [glycine](@entry_id:176531) at position $i+2$ a strong indicator of a Type II [β-turn](@entry_id:181262).

### Conclusion: Structural Stability and Prevalence

In the hierarchy of protein structure, [β-turns](@entry_id:176784) are observed with far greater frequency than γ-turns. This disparity can be attributed to fundamental principles of structural stability. The 10-membered hydrogen-bonded ring of a [β-turn](@entry_id:181262) is conformationally less strained than the tight 7-membered ring of a [γ-turn](@entry_id:185283). This allows the defining $i \to i+3$ hydrogen bond in a [β-turn](@entry_id:181262) to adopt a more linear and, therefore, more energetically favorable geometry. In contrast, the [γ-turn](@entry_id:185283)'s $i \to i+2$ hydrogen bond is necessarily more distorted and weaker. Furthermore, the central residues of most [β-turn](@entry_id:181262) types can adopt [dihedral angles](@entry_id:185221) that fall within allowed or favorable regions of the Ramachandran plot. The classic [γ-turn](@entry_id:185283), however, demands that its central residue adopt a conformation associated with significant [torsional strain](@entry_id:195818). Together, these factors of reduced hydrogen bond stability and increased conformational strain render the [γ-turn](@entry_id:185283) a less favorable, and thus less common, means of reversing a polypeptide chain compared to the versatile and stable family of [β-turns](@entry_id:176784) [@problem_id:2151400].