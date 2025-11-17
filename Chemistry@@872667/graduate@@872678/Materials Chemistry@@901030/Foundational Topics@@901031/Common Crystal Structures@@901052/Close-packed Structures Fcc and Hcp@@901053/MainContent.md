## Introduction
The arrangement of atoms into ordered [crystal lattices](@entry_id:148274) is a cornerstone of materials science, defining the very properties that make materials useful. Among the most fundamental and efficient of these arrangements are the [close-packed structures](@entry_id:160940), which describe how identical spheres can be packed with maximum density. This principle gives rise to two primary configurations found ubiquitously in elemental metals and alloys: the [face-centered cubic (fcc)](@entry_id:146825) and [hexagonal close-packed (hcp)](@entry_id:142132) structures. While both achieve the same packing density, a subtle difference in their layer-by-layer stacking creates a profound divergence in their mechanical, thermodynamic, and chemical behaviors. This article bridges the gap between simple geometry and complex material properties by systematically deconstructing these two critical structures.

In the following chapters, we will first delve into the **Principles and Mechanisms**, deriving the geometric rules of stacking and the formal crystallographic descriptions that define fcc and hcp. Next, we will explore their **Applications and Interdisciplinary Connections**, revealing how their structural differences impact everything from the [ductility of metals](@entry_id:271399) to the behavior of catalysts. Finally, a series of **Hands-On Practices** will provide an opportunity to apply these concepts quantitatively, solidifying your understanding of these foundational [crystal structures](@entry_id:151229).

## Principles and Mechanisms

The introductory chapter has established the prevalence and importance of [close-packed structures](@entry_id:160940) in crystalline materials. We now transition from this broad context to a rigorous examination of the geometric principles and physical mechanisms that govern their formation and properties. This chapter will deconstruct the elegant simplicity of close packing, starting from the arrangement of a single layer of spheres and building up to the complex three-dimensional architectures of the [face-centered cubic (fcc)](@entry_id:146825) and [hexagonal close-packed (hcp)](@entry_id:142132) structures. We will derive their fundamental geometric properties, explore their formal crystallographic descriptions, and investigate the subtle differences that distinguish them, ultimately leading to a thermodynamic perspective on their [relative stability](@entry_id:262615).

### The Geometric Foundation: Stacking of Close-Packed Planes

The concept of "close packing" originates from a simple yet profound question: what is the most efficient way to arrange identical, non-overlapping spheres in space? The solution begins in two dimensions. A single layer of spheres achieves its maximum possible density when each sphere is in contact with six neighbors, forming a **triangular (or hexagonal) lattice**. The centers of the spheres form a perfect 2D hexagonal grid.

To build a three-dimensional structure, we stack these close-packed planes. Consider a base layer, which we will label as having an **A registry**. When we place a second layer on top of the first, a sphere in this new layer cannot be placed directly on top of a sphere in the A layer, as this would be an unstable, low-density arrangement. Instead, to maintain high density, the spheres of the second layer must rest in the hollows or depressions of the first layer.

A close inspection of the A layer reveals two distinct sets of triangular hollows. If we consider a triangle of spheres in the A layer, its [centroid](@entry_id:265015) marks the position of a hollow. Let the [primitive vectors](@entry_id:142930) of the 2D hexagonal lattice be $\mathbf{a}_1$ and $\mathbf{a}_2$, with $|\mathbf{a}_1|=|\mathbf{a}_2|=a$, where $a$ is the nearest-neighbor distance (equal to twice the sphere radius, $2r$). One set of hollows is located at in-plane positions $\frac{1}{3}(\mathbf{a}_1 + \mathbf{a}_2)$ relative to a lattice point; we label the registry corresponding to these hollows as **B**. The other set of hollows is located at in-plane positions $\frac{2}{3}(\mathbf{a}_1 + \mathbf{a}_2)$; we label this registry as **C**. These two sets of hollows, B and C, are crystallographically inequivalent because they cannot be mapped onto each other by a lattice translation of the A layer [@problem_id:2473207] [@problem_id:2473259].

The vertical separation, $h$, between two adjacent close-packed layers is fixed by the condition that a sphere in one layer must be in contact with the three spheres forming the hollow in which it rests. Consider a sphere in a B layer resting on three spheres in the A layer. The four sphere centers form a regular tetrahedron with edge length $a$. The height of this tetrahedron is the inter-planar distance $h$. Using the Pythagorean theorem, we can relate the inter-sphere distance $a$ to the height $h$ and the in-plane distance from a vertex of the base triangle to its [centroid](@entry_id:265015), which is $\frac{a}{\sqrt{3}}$. This gives the relation:

$h^2 + \left(\frac{a}{\sqrt{3}}\right)^2 = a^2$

Solving for $h$, we find the fixed vertical separation between any two close-packed layers:

$h = \sqrt{a^2 - \frac{a^2}{3}} = a\sqrt{\frac{2}{3}}$

This fundamental geometric constraint dictates the z-dimension of all ideal [close-packed structures](@entry_id:160940) [@problem_id:2473259].

### The Two Canonical Stacking Sequences: FCC and HCP

With the three possible layer registries (A, B, C) defined, the variety of three-dimensional [close-packed structures](@entry_id:160940) arises from the specific periodic sequence in which these layers are stacked. While an infinite number of stacking sequences is possible, two are overwhelmingly common in nature due to their simplicity and high symmetry.

1.  **The ABAB... Stacking Sequence**: This is the simplest two-layer repeat. A layer with B registry is placed on an A layer, and the third layer is placed in the hollows of the B layer that lie directly above the spheres of the original A layer. This returns the stacking to the A registry. The resulting periodic sequence, ...ABABAB..., defines the **Hexagonal Close-Packed (HCP)** structure.

2.  **The ABCABC... Stacking Sequence**: This is the simplest three-layer repeat. An A layer is followed by a B layer, and the third layer is placed in the hollows of the B layer that do *not* lie above the spheres of the A layer, thus adopting the C registry. The fourth layer is then placed in the hollows of the C layer that align with the original A spheres. This periodic sequence, ...ABCABC..., defines the **Face-Centered Cubic (FCC)** structure. As we will see, this seemingly complex stacking paradoxically results in a structure with cubic symmetry.

### Fundamental Properties: Coordination Number and Packing Fraction

Despite their different long-range stacking order, the FCC and HCP structures share two key properties that stem from their identical local packing geometry.

The **[coordination number](@entry_id:143221) (CN)** is the number of nearest neighbors in direct contact with a given atom. In any ideal close-packed structure, any atom has six neighbors in its own plane, three in the layer above, and three in the layer below. Thus, for both FCC and HCP, the [coordination number](@entry_id:143221) is $6 + 3 + 3 = 12$, the highest possible for identical spheres [@problem_id:1766854].

The **[atomic packing factor](@entry_id:143259) (APF)** is the fraction of total volume occupied by spheres. Since the local arrangement and coordination are identical for every atom, it is intuitive that the overall packing density should also be the same. Both FCC and HCP structures share the maximum possible [packing fraction](@entry_id:156220) for identical spheres, which can be calculated to be:

$\text{APF} = \frac{\pi}{3\sqrt{2}} \approx 0.74048$

While this equality is a direct consequence of the identical local packing, it can be rigorously verified. For the HCP structure, this verification involves the **axial ratio**, $c/a$. Here, $a$ is the nearest-neighbor distance within the basal plane, and $c$ is the height of the conventional hexagonal unit cell, which spans two layers (from one A layer to the next A layer). The height $c$ is therefore twice the inter-planar spacing, $c = 2h$. Using our previously derived value for $h$, we find the ideal $c/a$ ratio for an HCP structure composed of perfect hard spheres [@problem_id:2473216]:

$\frac{c}{a} = \frac{2h}{a} = \frac{2(a\sqrt{2/3})}{a} = \sqrt{\frac{8}{3}} \approx 1.633$

Any deviation from this ideal ratio implies that the nearest-neighbor distances are no longer uniform; either the in-plane or out-of-plane neighbors become closer. A mathematical analysis shows that the [packing fraction](@entry_id:156220) is maximized precisely at this ideal ratio, confirming that this geometry represents the optimal packing for the ABAB... sequence [@problem_id:2473239].

### Crystallographic Description: Lattice, Basis, and Space Group

To fully characterize these structures, we must employ the formal language of crystallography, which distinguishes between a **Bravais lattice** (an infinite array of equivalent points) and a **basis** (the atom or group of atoms associated with each lattice point).

The set of all atomic positions in the **FCC** structure is, by itself, a Bravais lattice. This means that every atom has an identical environment, and any atom can be reached from any other atom by a pure translation of the lattice. Consequently, the FCC structure can be described with a **one-atom basis** placed on the sites of a [face-centered cubic](@entry_id:156319) Bravais lattice [@problem_id:1809054]. The full symmetry of this structure is described by the [space group](@entry_id:140010) $\mathrm{Fm}\bar{3}\mathrm{m}$ (No. 225). In this description, the single-atom basis occupies the Wyckoff 4a site at [fractional coordinates](@entry_id:203215) $(0,0,0)$ in the conventional cubic cell. The close-packed planes are the $\{111\}$ [family of planes](@entry_id:171035), and the ABC stacking occurs along the $\langle 111 \rangle$ directions [@problem_id:2473205].

In contrast, the set of atomic positions in the **HCP** structure is *not* a Bravais lattice. The environment of an atom in an A layer is different from that of an atom in a B layer with respect to long-range stacking; they are related by a rotation and a non-lattice translation, not by a pure lattice translation alone. Therefore, the HCP structure cannot be described by a one-atom basis. It is correctly described as a simple hexagonal Bravais lattice with a **two-atom basis** [@problem_id:1809054]. The full symmetry is captured by the [space group](@entry_id:140010) $\mathrm{P}6_3/\mathrm{mmc}$ (No. 194). The two atoms of the basis occupy the Wyckoff 2c sites at [fractional coordinates](@entry_id:203215) $(\frac{1}{3},\frac{2}{3},\frac{1}{4})$ and $(\frac{2}{3},\frac{1}{3},\frac{3}{4})$ within the conventional hexagonal cell. The ABAB... stacking occurs along the $[0001]$ direction (the $c$-axis) [@problem_id:2473205].

### Interstitial Sites: The Voids Between Atoms

The packing of spheres, even at maximum density, inevitably leaves empty spaces known as **[interstitial sites](@entry_id:149035)** or voids. The size, number, and location of these sites are critical for understanding alloys, the behavior of impurities, and [diffusion mechanisms](@entry_id:158710). In [close-packed structures](@entry_id:160940), there are two primary types of [interstitial sites](@entry_id:149035), named after the coordination polyhedron formed by the centers of the surrounding host atoms.

-   **Tetrahedral Sites**: Each site is surrounded by four host atoms forming a tetrahedron.
-   **Octahedral Sites**: Each site is surrounded by six host atoms forming an octahedron.

A remarkable and universal feature of all ideal [close-packed structures](@entry_id:160940), including both FCC and HCP, is the ratio of these sites to the host atoms. For every $N$ atoms in the structure, there are always $N$ octahedral sites and $2N$ tetrahedral sites [@problem_id:2473245].

In the **FCC** [conventional cell](@entry_id:747851), which contains 4 atoms, there are 4 octahedral sites (one at the body center $(\frac{1}{2},\frac{1}{2},\frac{1}{2})$ and one at the center of each of the 12 edges, with each edge site shared by 4 cells) and 8 tetrahedral sites (located at positions like $(\frac{1}{4},\frac{1}{4},\frac{1}{4})$ in each of the 8 "[octants](@entry_id:176379)" of the cubic cell).

In the **HCP** [conventional cell](@entry_id:747851), which contains 2 atoms, there are 2 octahedral sites (at positions like $(0,0,0)$ and $(0,0,\frac{1}{2})$ in a specific setting) and 4 tetrahedral sites (at positions like $(\frac{1}{3},\frac{2}{3},\frac{7}{8})$) [@problem_id:2473245].

In both cases, the ratio holds: 1 octahedral site per atom and 2 tetrahedral sites per atom. The existence of these two distinct types of voids with their fixed stoichiometry is a cornerstone of [materials chemistry](@entry_id:150195).

### Distinguishing FCC and HCP: Beyond Nearest Neighbors

Given that FCC and HCP structures share the same [coordination number](@entry_id:143221), [packing fraction](@entry_id:156220), and interstitial site count, a natural question arises: how can they be experimentally distinguished? Their identical local environments mean that any probe sensitive only to the first shell of neighbors will see no difference. The distinction lies in the **long-range order**, which manifests in the arrangement of the second, third, and subsequent neighbor shells.

A careful geometric analysis reveals that the divergence begins at the **second-neighbor shell**.
- In **FCC**, an atom has 6 second-neighbors at a distance of $a\sqrt{2}$.
- In **HCP** (with an ideal $c/a$ ratio), an atom has 2 second-neighbors at a distance of $a\sqrt{8/3}$.

The third-neighbor shells are also different.
-   In **FCC**, the third-neighbor shell consists of 24 atoms at a distance of $a\sqrt{3}$.
-   In **HCP**, the third-neighbor shell consists of 6 atoms at a distance of $a\sqrt{3}$.

This profound difference in the structure of outer coordination shells gives FCC and HCP distinct fingerprints in scattering experiments (e.g., X-ray or [neutron diffraction](@entry_id:140330)). These experiments measure the **[pair distribution function](@entry_id:145441), $g(r)$**, which gives the probability of finding another atom at a distance $r$ from a reference atom. For a perfect crystal, $g(r)$ is a series of sharp peaks (delta functions) located at the neighbor-shell radii. While the first peak of $g(r)$ for FCC and HCP would be identical, their subsequent peaks appear at different distances and with different multiplicities, allowing for unambiguous identification [@problem_id:2473226].

### Thermodynamic Perspective: Stability and Transformations

The existence of two primary [close-packed structures](@entry_id:160940) with nearly identical energies raises questions about their [relative stability](@entry_id:262615). Many elemental metals exhibit [polymorphism](@entry_id:159475), adopting one structure at low temperatures and transitioning to the other at higher temperatures. This behavior cannot be explained by hard-sphere geometry alone; it requires a thermodynamic framework that considers the subtle energetic differences between the stacking sequences.

The energy cost associated with a disruption in the perfect [stacking sequence](@entry_id:197285) (e.g., an ABC**A**BC layer in an FCC crystal) is known as the **[stacking fault energy](@entry_id:145736), $\gamma_{sf}$**. Materials with low [stacking fault energy](@entry_id:145736) have a small energy difference between the FCC and HCP configurations, making transformations between them more likely.

A powerful, albeit abstract, way to model this transformation is through **Landau theory**. We can define a [scalar order parameter](@entry_id:197670), $\eta$, that represents the "character" of the stacking, where, for instance, $\eta > 0$ favors FCC and $\eta  0$ favors HCP. Because the ABAB... and ABCABC... sequences are not related by a simple inversion, the Landau expansion of the free energy, $F(\eta)$, can contain an odd-powered (cubic) term:

$F(\eta;T,h) = a(T)\eta^{2} - w\eta^{3} + b\eta^{4} - h\eta$

The cubic term, $-w\eta^3$, is crucial; it breaks the symmetry between positive and negative $\eta$ and is the signature of a **[first-order phase transition](@entry_id:144521)**. Such a transition is characterized by a discontinuous jump in the order parameter $\eta$ as temperature is varied. The external field, $h$, can be physically related to the material's intrinsic [stacking fault energy](@entry_id:145736). The theory predicts that if the [stacking fault energy](@entry_id:145736) is sufficiently high (exceeding a critical value $\gamma_{sf}^{\ast}$), the sharp, discontinuous transition between HCP and FCC is "rounded" into a smooth crossover [@problem_id:2473254]. This advanced model provides a continuous and unified thermodynamic framework for understanding the intimate and competitive relationship between the two most fundamental ways of packing spheres.