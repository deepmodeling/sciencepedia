## Introduction
The spatial arrangement of atoms is the single most important factor determining the properties of a solid material. To move from a qualitative picture to a predictive science, we need a quantitative framework for describing how these atoms fill space. This is where the concepts of **Coordination Number (CN)** and **Atomic Packing Factor (APF)** become indispensable. They provide a simple yet powerful language to describe both the local environment of an atom and the global [packing efficiency](@entry_id:138204) of an entire crystal. This article bridges the gap between these foundational geometric concepts and their far-reaching consequences for real-world materials.

You will begin in "Principles and Mechanisms" by establishing the rigorous definitions of CN and APF, learning how to calculate them for common [crystal structures](@entry_id:151229), and exploring advanced concepts like Voronoi tessellation. Next, "Applications and Interdisciplinary Connections" will demonstrate how these principles are applied to predict [crystal structures](@entry_id:151229), understand pressure-induced phase transitions, and explain mechanical and transport properties across various disciplines. Finally, "Hands-On Practices" will challenge you to apply your knowledge to solve practical problems involving 2D [lattices](@entry_id:265277), [interstitial sites](@entry_id:149035), and the analysis of amorphous structures, solidifying your command of these essential materials science tools.

## Principles and Mechanisms

The spatial arrangement of atoms is a foundational concept in materials science, determining a vast range of physical and chemical properties. In this chapter, we will dissect two of the most fundamental quantitative descriptors of atomic arrangement: the **coordination number (CN)** and the **[atomic packing factor](@entry_id:143259) (APF)**. We will begin by establishing their precise definitions, then proceed to calculate their values for common [crystal structures](@entry_id:151229), and finally, explore their application and extension to more complex and realistic material systems.

### Fundamental Concepts: Defining How Atoms Occupy Space

To quantify the structure of a solid, we must first have a language to describe both the local environment of an atom and the overall efficiency with which atoms fill space.

#### Coordination Number: Counting Nearest Neighbors

The most immediate characteristic of an atom's local environment is the number of its closest neighbors. This quantity is known as the **coordination number (CN)**. In its simplest conception, within the **[hard-sphere model](@entry_id:145542)** where atoms are pictured as rigid, touching spheres, the CN is simply the number of spheres in direct contact with a central sphere. For example, in the common metallic structures, this geometric count is straightforward: 6 for the [simple cubic lattice](@entry_id:160687), 8 for the body-centered cubic lattice, and 12 for both the face-centered cubic and [hexagonal close-packed](@entry_id:150929) lattices.

However, a more nuanced understanding distinguishes between different types of "coordination."
*   The **geometric coordination number** refers strictly to the number of atoms located at the shortest interatomic distance from a central atom. This is a purely spatial definition.
*   The **topological coordination number** refers to the number of atoms connected by chemical bonds.

In many materials, such as metals with non-directional [metallic bonding](@entry_id:141961), these two numbers are identical. An atom in a [face-centered cubic](@entry_id:156319) (FCC) metal is bonded to its 12 nearest geometric neighbors, so its topological and geometric CN are both 12 [@problem_id:2475673]. However, in materials with strong, directional [covalent bonds](@entry_id:137054), the two can differ. A prime example is the diamond-cubic structure adopted by silicon and carbon (diamond). Geometrically, each atom has 4 nearest neighbors at a distance of $\frac{a\sqrt{3}}{4}$ (where $a$ is the [lattice constant](@entry_id:158935)) and 12 second-nearest neighbors at a greater distance of $\frac{a}{\sqrt{2}}$. The strong [covalent bonding](@entry_id:141465) is tetrahedral, meaning each atom forms exactly four bonds with its four nearest neighbors. Therefore, its topological CN is 4, which matches its geometric nearest-neighbor count [@problem_id:2475673]. If one were to define a broader "coordination" by including both the first and second shells, the count would rise to $4+12=16$, but this would lose the essential chemical information about primary bonding.

For systems without perfect periodicity, such as liquids or [amorphous solids](@entry_id:146055), or to provide a more rigorous physical basis for the definition, we turn to the **[pair distribution function](@entry_id:145441)**, $g(r)$. This function describes the probability of finding another atom at a distance $r$ from a reference atom. The function exhibits a series of peaks, corresponding to successive coordination shells. A standard, robust method for defining the CN is to integrate the number of atoms in spherical shells around the reference atom out to the first minimum of $g(r)$, denoted $r_c$. The [coordination number](@entry_id:143221) $N(r_c)$ is then given by:
$$ N(r_c) = 4\pi \rho \int_{0}^{r_c} r^{2} g(r)\,\mathrm{d}r $$
where $\rho$ is the average [number density](@entry_id:268986) of the material. This integral formalism provides an average count of the nearest-neighbor shell and is indispensable for characterizing disordered materials. It is critical to recognize that this geometric or structural coordination number is distinct from **chemical valence**. For instance, solid argon (FCC) has a CN of 12 but a chemical valence of 0, while metallic copper (FCC) has a CN of 12 but a primary valence of +1 or +2 [@problem_id:2475636].

#### Atomic Packing Factor: Quantifying Packing Efficiency

While the coordination number describes the local environment, the **[atomic packing factor](@entry_id:143259) (APF)** quantifies the [global efficiency](@entry_id:749922) of space filling in a crystal structure. It is defined as the fraction of the total volume of a unit cell that is occupied by the constituent atoms, modeled as hard spheres.
$$ \text{APF} = \frac{V_{\text{atoms}}}{V_{\text{cell}}} = \frac{N \times V_{\text{atom}}}{V_{\text{cell}}} $$
Here, $N$ is the number of atoms per unit cell, $V_{\text{atom}}$ is the volume of a single atom (sphere), and $V_{\text{cell}}$ is the volume of the unit cell. The APF is a dimensionless ratio, typically derived assuming the [atomic radius](@entry_id:139257) $r$ is half the nearest-neighbor distance, meaning adjacent atoms are in contact.

It is crucial to distinguish APF from other macroscopic quantities [@problem_id:2475686].
*   **Mass Density ($\rho$)**: Density is mass per unit volume ($\rho = \frac{N \cdot m_{\text{atom}}}{V_{\text{cell}}}$). While both APF and density depend on the unit cell volume, density is also a function of atomic mass. Two isotopes of an element forming the same crystal structure (e.g., FCC) will have identical [lattice parameters](@entry_id:191810) and thus the same APF, but different mass densities due to their different atomic masses.
*   **Porosity ($\phi$)**: Porosity refers to the fraction of *macroscopic* void volume (pores, cracks) within a bulk material. A theoretically perfect single crystal is considered fully dense, with zero porosity ($\phi=0$). The empty space inherent to the atomic arrangement, represented by $1 - \text{APF}$, is known as the **interstitial volume** and is a feature of the ideal crystal structure, not a macroscopic defect.

The APF is a purely geometric property of an ideal crystal lattice. For a given structure defined by hard-sphere contact, its value is a constant, independent of the [atomic radius](@entry_id:139257) or mass [@problem_id:2475686].

### Calculating CN and APF for Common Crystal Structures

The calculation of APF is a foundational exercise that connects the geometry of a unit cell to its [packing efficiency](@entry_id:138204). The process involves three steps: determining the number of atoms per unit cell ($N$), finding the relationship between the [atomic radius](@entry_id:139257) ($r$) and the lattice constant ($a$), and then applying the APF definition.

#### Simple Cubic (SC) Structure

The simple cubic (SC) structure is the most straightforward, with atoms located only at the eight corners of a cubic unit cell.

*   **Atoms per cell ($N$)**: Each of the 8 corner atoms is shared by 8 unit cells, so $N = 8 \times \frac{1}{8} = 1$.
*   **Relation between $a$ and $r$**: Nearest neighbors are along the cube edge. Two atoms touch along the edge, so the lattice constant is equal to two atomic radii: $a = 2r$.
*   **Coordination Number (CN)**: An atom at any corner has 6 nearest neighbors along the $\pm x, \pm y, \pm z$ directions. Thus, $\text{CN} = 6$.
*   **APF Calculation**:
    $$ \text{APF}_{\text{SC}} = \frac{N \cdot (\frac{4}{3}\pi r^3)}{a^3} = \frac{1 \cdot \frac{4}{3}\pi r^3}{(2r)^3} = \frac{\frac{4}{3}\pi r^3}{8r^3} = \frac{\pi}{6} \approx 0.5236 $$
The SC structure is relatively open, with just over half its volume occupied by atoms [@problem_id:2475655].

#### Body-Centered Cubic (BCC) Structure

The [body-centered cubic](@entry_id:151336) (BCC) structure has atoms at the eight corners and one atom at the geometric center of the cube.

*   **Atoms per cell ($N$)**: $N = (8 \times \frac{1}{8})_{\text{corners}} + (1)_{\text{center}} = 2$.
*   **Relation between $a$ and $r$**: Nearest neighbors are the corner and body-center atoms. Contact occurs along the body diagonal of the cube. The length of the body diagonal is $\sqrt{a^2+a^2+a^2} = a\sqrt{3}$. This distance spans one radius from a corner atom, the diameter of the central atom, and one radius from the opposite corner atom. Thus, $a\sqrt{3} = 4r$.
*   **Coordination Number (CN)**: The central atom is in contact with all 8 corner atoms. By symmetry, each corner atom is also surrounded by 8 neighbors. Thus, $\text{CN} = 8$.
*   **APF Calculation**:
    $$ \text{APF}_{\text{BCC}} = \frac{2 \cdot \frac{4}{3}\pi r^3}{a^3} = \frac{\frac{8}{3}\pi r^3}{(\frac{4r}{\sqrt{3}})^3} = \frac{\frac{8}{3}\pi r^3}{\frac{64r^3}{3\sqrt{3}}} = \frac{\pi\sqrt{3}}{8} \approx 0.6802 $$
The BCC structure is significantly denser than SC, which is consistent with its higher [coordination number](@entry_id:143221) [@problem_id:2475682].

#### Face-Centered Cubic (FCC) Structure

The face-centered cubic (FCC) structure has atoms at the eight corners and at the center of each of the six faces.

*   **Atoms per cell ($N$)**: $N = (8 \times \frac{1}{8})_{\text{corners}} + (6 \times \frac{1}{2})_{\text{faces}} = 1 + 3 = 4$.
*   **Relation between $a$ and $r$**: Nearest neighbors are a corner atom and an adjacent face-center atom. Contact occurs along the face diagonal. The length of the face diagonal is $\sqrt{a^2+a^2} = a\sqrt{2}$. This distance spans $4r$. Thus, $a\sqrt{2} = 4r$.
*   **Coordination Number (CN)**: An atom at any site is surrounded by 12 equidistant nearest neighbors. For instance, an atom at a face center has 4 neighbors in its own plane (at the corners), and 4 neighbors in each of the two adjacent unit cells. Thus, $\text{CN} = 12$.
*   **APF Calculation**:
    $$ \text{APF}_{\text{FCC}} = \frac{4 \cdot \frac{4}{3}\pi r^3}{a^3} = \frac{\frac{16}{3}\pi r^3}{(\frac{4r}{\sqrt{2}})^3} = \frac{\frac{16}{3}\pi r^3}{\frac{64r^3}{2\sqrt{2}}} = \frac{\frac{16}{3}\pi r^3}{16\sqrt{2}r^3} = \frac{\pi}{3\sqrt{2}} \approx 0.7405 $$
This value, approximately 74%, represents the maximum possible packing density for identical spheres, a state known as [close-packing](@entry_id:139822) [@problem_id:2475638].

### Close-Packed Structures and Their Significance

The FCC structure is one example of a **close-packed** arrangement. These structures are of particular interest as they represent the most efficient way to fill space with identical spheres.

#### The Hexagonal Close-Packed (HCP) Structure

Another common close-packed structure is the **[hexagonal close-packed](@entry_id:150929) (HCP)** structure. It is built by stacking close-packed planes of atoms in an ABAB... sequence, whereas the FCC structure corresponds to an ABCABC... sequence.

Despite the difference in long-range stacking order, the local environment in HCP is identical to FCC. Each atom is surrounded by 12 nearest neighbors, so its **CN is 12**. For an ideal HCP structure, the [hard-sphere model](@entry_id:145542) dictates a specific ratio of the height of the hexagonal unit cell ($c$) to its basal edge length ($a$). This ideal ratio can be derived by considering the geometry of stacking and is found to be $\frac{c}{a} = \sqrt{\frac{8}{3}} \approx 1.633$ [@problem_id:2475665].

When the APF for this ideal HCP structure is calculated, it yields a remarkable result:
$$ \text{APF}_{\text{HCP}} = \frac{\pi}{3\sqrt{2}} \approx 0.7405 $$
This is exactly the same as the APF for the FCC structure. This demonstrates that different crystallographic symmetries can achieve the same maximum packing density and local coordination, a consequence of both being based on the stacking of close-packed planes.

#### The Diamond Cubic Structure: An 'Open' Packing

In contrast to the close-packed metals, the diamond-cubic structure provides a compelling example where [packing efficiency](@entry_id:138204) is secondary to the nature of [chemical bonding](@entry_id:138216) [@problem_id:2475673]. As determined earlier, its CN is 4 due to the tetrahedral sp³ covalent bonds. The APF calculation reveals:
$$ \text{APF}_{\text{Diamond}} = \frac{8 \cdot \frac{4}{3}\pi (\frac{a\sqrt{3}}{8})^3}{a^3} = \frac{\pi\sqrt{3}}{16} \approx 0.3401 $$
This packing factor is extremely low—less than half that of the [close-packed structures](@entry_id:160940). This "open" structure is a direct consequence of the rigid, directional nature of covalent bonds, which lock atoms into a specific tetrahedral arrangement, preventing a denser packing. This powerfully illustrates that maximizing APF is not the sole driving force for crystal [structure formation](@entry_id:158241); the electronic requirements of bonding are often paramount. Furthermore, comparing the DC and FCC structures disproves any notion that APF is simply proportional to CN. While the CN increases by a factor of 3 (from 4 to 12), the APF increases by a factor of $\frac{16}{3\sqrt{6}} \approx 2.18$, not 3 [@problem_id:2475673].

### Advanced and Applied Concepts

The simple [hard-sphere model](@entry_id:145542) provides an excellent foundation, but a more rigorous and versatile framework is needed to handle the full complexity of real materials.

#### Rigorous Definitions: Voronoi Tessellation and the Wigner-Seitz Cell

A parameter-free, mathematically rigorous way to partition space in a crystal is through **Voronoi tessellation**. For a set of points (atomic sites), the Voronoi cell of a given point is the region of space closer to that point than to any other. When the set of points is a Bravais lattice, the resulting Voronoi cell is called the **Wigner-Seitz cell** [@problem_id:2475641].

The Wigner-Seitz cell represents the volume uniquely associated with a single lattice point. It is a [primitive unit cell](@entry_id:159354), and thus the APF for a monatomic Bravais lattice can be elegantly redefined as the ratio of the volume of one atomic sphere to the volume of the Wigner-Seitz cell [@problem_id:2475641].

One might intuitively assume that the number of faces of the Wigner-Seitz cell would equal the [coordination number](@entry_id:143221). After all, each face is a [perpendicular bisector](@entry_id:176427) plane between the central atom and another atom. This holds true for the SC and FCC [lattices](@entry_id:265277). However, it is not a general rule. The BCC lattice provides a classic counterexample: its CN is 8, but its Wigner-Seitz cell (a truncated octahedron) has 14 faces. Eight large faces correspond to the 8 nearest neighbors, while six smaller faces correspond to the 6 second-nearest neighbors. The number of Voronoi faces equals the coordination number if and only if only nearest-neighbor atoms contribute faces to the cell [@problem_id:2475641]. For systems with atoms of different sizes, this concept is extended using the **radical Voronoi diagram** (or [power diagram](@entry_id:175943)), which correctly partitions space based on a power distance that accounts for atomic radii [@problem_id:2475641].

#### Coordination in Multi-Component Systems: The Radius Ratio Rules

In [ionic compounds](@entry_id:137573), where cations and [anions](@entry_id:166728) have different sizes, the coordination environment is largely governed by geometric constraints. The **[radius ratio rules](@entry_id:158810)** provide a powerful guideline for predicting the coordination number of a smaller ion (typically the cation, radius $r$) fitting into an interstitial site within a lattice of larger ions (anions, radius $R$).

By calculating the limiting geometric condition where the cation touches all coordinating anions and the anions also touch each other, we can derive critical values for the radius ratio $\rho = r/R$ that define the stability range for different [coordination polyhedra](@entry_id:157778) [@problem_id:2475639].

*   **Trigonal (CN=3)**: The cation fits in the planar void between three touching anions. Lower bound: $\rho = \frac{2}{\sqrt{3}} - 1 \approx 0.155$.
*   **Tetrahedral (CN=4)**: The cation fits in the void at the center of a tetrahedron of [anions](@entry_id:166728). Lower bound: $\rho = \frac{\sqrt{6}}{2} - 1 \approx 0.225$.
*   **Octahedral (CN=6)**: The cation fits in the void at the center of an octahedron of [anions](@entry_id:166728). Lower bound: $\rho = \sqrt{2} - 1 \approx 0.414$.
*   **Cubic (CN=8)**: The cation fits in the void at the center of a cube of [anions](@entry_id:166728). Lower bound: $\rho = \sqrt{3} - 1 \approx 0.732$.

If the actual radius ratio of a compound falls within a certain range, it is likely to adopt the corresponding coordination. For example, a ratio between 0.414 and 0.732 suggests octahedral coordination is most stable.

#### Coordination in Imperfect and Disordered Systems

Real materials are never perfect. They contain defects and can be fully disordered (amorphous). Our concepts must extend to these cases [@problem_id:2475632].

Consider a crystalline compound like rock salt (AB) where the A-sublattice has vacancies. Each B-site is geometrically surrounded by 6 A-sites. If each A-site is vacant with probability $p$, then the **local coordination number** of a specific B-site is not fixed at 6, but can be any integer from 0 to 6. This becomes a statistical problem. The probability of a randomly chosen B-site having exactly $m$ occupied A-neighbors follows the [binomial distribution](@entry_id:141181):
$$ P(m) = \binom{6}{m}(1-p)^m p^{6-m} $$
While the local CN varies, the **average [coordination number](@entry_id:143221)** across the entire B-sublattice is a well-defined quantity, equal to the expectation of this distribution, which is $6(1-p)$. The variance is $6p(1-p)$.

This statistical viewpoint is essential for [amorphous materials](@entry_id:143499). In a glassy network, there is no single [coordination number](@entry_id:143221). Instead, there is a **distribution of coordination numbers**. For an amorphous material where sites have a local CN of 3, 4, or 5 with respective probabilities $q$, $r$, and $s$, the local CN is still well-defined for any given site, but the system as a whole is characterized by the distribution. The average [coordination number](@entry_id:143221) is the weighted mean, $3q + 4r + 5s$. In such [disordered systems](@entry_id:145417), a single-number APF also loses its unique definition, as assigning fixed atomic radii becomes an approximation dependent on how one interprets the broad peaks of the [pair distribution function](@entry_id:145441) [@problem_id:2475632].

From the simple counting of touching spheres in perfect crystals to the statistical distributions in [disordered solids](@entry_id:136759), the concepts of [coordination number](@entry_id:143221) and [atomic packing factor](@entry_id:143259) provide a powerful, scalable framework for describing the structure of matter.