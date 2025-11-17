## Introduction
In the world of [crystalline solids](@entry_id:140223), the quest for energetic stability often translates into a simple geometric principle: packing atoms as densely as possible. This drive gives rise to [close-packed structures](@entry_id:160940), which form the structural backbone of countless metallic elements and compounds. While seemingly minor variations in the [stacking sequence](@entry_id:197285) of atomic layers—such as the ABAB... pattern of the Hexagonal Close-Packed (HCP) structure versus the ABCABC... of the Face-Centered Cubic (FCC) lattice—might appear trivial, they lead to profound differences in a material's mechanical, electronic, and thermodynamic properties. This article demystifies these connections, bridging the gap from abstract geometry to tangible material behavior.

Across the following chapters, you will build a comprehensive understanding of this fundamental topic. First, in **Principles and Mechanisms**, we will deconstruct [close-packed structures](@entry_id:160940) from first principles, deriving their geometry and exploring the subtle energetic balance that dictates stability. Next, in **Applications and Interdisciplinary Connections**, we will examine the far-reaching consequences of stacking order, linking it to [plastic deformation](@entry_id:139726), electronic band structures, and [phase transformations](@entry_id:200819). Finally, **Hands-On Practices** will provide an opportunity to solidify your knowledge by tackling problems in [structural analysis](@entry_id:153861) and computational materials science. We begin our journey by exploring the fundamental geometry and rules that govern the stacking of atomic spheres.

## Principles and Mechanisms

The arrangement of atoms in [crystalline solids](@entry_id:140223) is governed by the imperative to minimize the system's total energy. For many simple metallic elements, where bonding is non-directional, this principle manifests as a geometric problem: how to pack identical spheres as densely as possible. The solutions to this problem give rise to the [close-packed structures](@entry_id:160940), which form the foundation for understanding a vast array of materials. In this chapter, we will deconstruct these structures from first principles, exploring their geometric properties, the variations in their stacking sequences, the defects they can host, and the subtle energetic factors that dictate which specific structure is realized in nature.

### The Geometry of Sphere Packing: The Close-Packed Monolayer

The starting point for any three-dimensional close-packed structure is the two-dimensional close-packed layer. Intuitively, the most efficient way to arrange identical circles on a plane is in a hexagonal (or triangular) lattice, where each circle is in contact with six neighbors. This arrangement maximizes the use of space in two dimensions.

Let us formalize this by considering the centers of identical hard spheres of radius $r$. In a close-packed monolayer, the distance between the centers of any two touching spheres is $2r$. We can define this layer using two [primitive lattice vectors](@entry_id:270646). A convenient choice, forming a $60^{\circ}$ angle, is $\mathbf{a}_1 = 2r(1,0)$ and $\mathbf{a}_2 = 2r(\frac{1}{2}, \frac{\sqrt{3}}{2})$. The center of any sphere in this layer can be described by a vector $\mathbf{R} = m\mathbf{a}_1 + n\mathbf{a}_2$ for integers $m$ and $n$.

A crucial feature of this hexagonal net is the presence of hollows, or **interstices**, between the spheres. Close inspection reveals two distinct sets of triangular hollows. If we imagine the triangles formed by the centers of three mutually touching spheres, one set of triangles points "up" and the other "down". These two sets of hollows provide the possible locations for spheres in the next layer.

### Stacking Layers: The ABCs of Close-Packing

To build a three-dimensional structure, we stack a second identical monolayer on top of the first. To maintain high density, the spheres of the second layer must nestle into the hollows of the first. Let us designate the positions of the spheres in the first layer as **A registry**. If we place the spheres of the second layer over one set of hollows, say the "up" triangles, we call this the **B registry**. If we were to place them over the "down" triangles, we would call this the **C registry**.

The precise lateral positions of these registries can be derived geometrically. The center of a hollow is located at the [centroid](@entry_id:265015) of the equilateral triangle formed by the three spheres creating it. For a triangle with vertices at positions $\mathbf{0}$, $\mathbf{a}_1$, and $\mathbf{a}_2$ (using the basis vectors defined previously), the centroid is at $\frac{1}{3}(\mathbf{a}_1 + \mathbf{a}_2)$. This corresponds to one of the hollow sites. Another inequivalent hollow site can be found at $\frac{2}{3}(\mathbf{a}_1 + \mathbf{a}_2)$ [@problem_id:2808538]. Therefore, relative to the A-layer sites at $(0,0)$ in [fractional coordinates](@entry_id:203215), the B-sites and C-sites are located at [fractional coordinates](@entry_id:203215) such as $(\frac{1}{3}, \frac{1}{3})$ and $(\frac{2}{3}, \frac{2}{3})$. Note that the exact [fractional coordinates](@entry_id:203215) depend on the choice of basis vectors; for example, a basis with a $120^{\circ}$ angle yields coordinates $(\frac{1}{3}, \frac{2}{3})$ and $(\frac{2}{3}, \frac{1}{3})$ for the two hollow sites [@problem_id:2808475]. Regardless of the convention, the physical locations remain the same: they are the two distinct sets of threefold hollows.

The vertical separation between these close-packed layers is also fixed by geometry. A sphere in the B-layer touches three spheres in the A-layer below it. The centers of these four mutually touching spheres form a regular tetrahedron with an edge length of $a = 2r$. The height of this tetrahedron, $h$, corresponds to the interlayer spacing. Using the Pythagorean theorem, we can relate the edge length $a$, the in-plane distance from a vertex to the triangle's [centroid](@entry_id:265015) ($d = a/\sqrt{3}$), and the height $h$. The condition for contact is that the distance between a B-sphere center and an A-sphere center is $a=2r$. This gives $h^2 + d^2 = a^2$, which leads to:

$h^2 = a^2 - \left(\frac{a}{\sqrt{3}}\right)^2 = \frac{2}{3}a^2 \implies h = a\sqrt{\frac{2}{3}} = 2r\sqrt{\frac{2}{3}}$

This height is approximately $h \approx 1.633r$. A key consequence of this geometry is that stacking a layer directly on top of another of the same registry (e.g., an A layer on an A layer) is forbidden due to sphere overlap. Therefore, the general stacking rule for [close-packed structures](@entry_id:160940) is that **no two consecutive layers can have the same registry**. After laying down an A layer and a B layer, the third layer can only be placed in either the A registry or the C registry. This choice gives rise to the two canonical [close-packed structures](@entry_id:160940) [@problem_id:2808538].

### The Two Canonical Close-Packed Structures: HCP and FCC

The restriction that adjacent layers must be different leaves two simple periodic possibilities for stacking the third layer and all subsequent layers.

#### Hexagonal Close-Packed (HCP)

If the third layer is placed directly above the first layer (in A registry), the [stacking sequence](@entry_id:197285) becomes **ABAB...**. This structure has a two-layer repeat period. The resulting three-dimensional crystal structure has hexagonal symmetry and is called the **Hexagonal Close-Packed (HCP)** structure. Its [conventional unit cell](@entry_id:273158) is a hexagonal prism with basal [lattice parameter](@entry_id:160045) $a$ (the nearest-neighbor distance, $2R$) and height $c$. Since the height $c$ spans two interlayer spacings ($c=2h$), we can derive the ideal **axial ratio** for the HCP structure from first principles [@problem_id:2808468]:

$\frac{c}{a} = \frac{2h}{a} = \frac{2a\sqrt{2/3}}{a} = 2\sqrt{\frac{2}{3}} = \sqrt{\frac{8}{3}} \approx 1.633$

Metals with an axial ratio close to this ideal value, such as magnesium ($c/a \approx 1.624$) and cobalt ($c/a \approx 1.623$), are considered to be well-described by the ideal [hard-sphere model](@entry_id:145542).

#### Face-Centered Cubic (FCC)

If the third layer is placed in the remaining C registry, the sequence becomes **ABCABC...**. This structure has a three-layer repeat period. While not immediately obvious, this [stacking sequence](@entry_id:197285) generates the highly symmetric **Face-Centered Cubic (FCC)** structure. The close-packed $\{111\}$ planes of the cubic system correspond to the A, B, and C layers. To relate the geometries, we note that the nearest-neighbor distance in both structures is $a_{HCP} = 2R$. In the FCC lattice with cubic parameter $a_{fcc}$, nearest neighbors lie along the face diagonal. The length of the face diagonal is $\sqrt{2}a_{fcc}$, which must be equal to $4R$. Thus, $a_{fcc} = 4R/\sqrt{2} = 2\sqrt{2}R$. Since $a_{HCP}=2R$, we find the simple relation $a_{fcc} = \sqrt{2} a_{HCP}$ [@problem_id:2808428].

#### Maximum Packing Density

A key property of both FCC and ideal HCP structures is their **[atomic packing fraction](@entry_id:272449) (APF)**, the fraction of total volume occupied by the spheres. For the FCC structure, the [conventional unit cell](@entry_id:273158) has a volume of $V_{cell} = a_{fcc}^3 = (2\sqrt{2}R)^3 = 16\sqrt{2}R^3$. It contains 4 atoms (8 corners $\times 1/8$ + 6 faces $\times 1/2$). The total volume of these spheres is $V_{spheres} = 4 \times \frac{4}{3}\pi R^3$. The [packing fraction](@entry_id:156220) is therefore:

$\text{APF}_{fcc} = \frac{V_{spheres}}{V_{cell}} = \frac{16/3 \pi R^3}{16\sqrt{2}R^3} = \frac{\pi}{3\sqrt{2}} \approx 0.7405$

A similar calculation for the ideal HCP structure yields the exact same value [@problem_id:2808428]. This value represents the maximum possible density for packing identical spheres, a fact conjectured by Kepler in 1611 and proven mathematically only in 1998 (the Kepler conjecture). The identical packing density of FCC and HCP underscores their close energetic and geometric relationship [@problem_id:2808472].

### Beyond the Basics: Polytypism and Interstitial Sites

While FCC and HCP are the most common [close-packed structures](@entry_id:160940), the stacking possibilities are infinite.

#### Polytypism and Ramsdell Notation

Any [stacking sequence](@entry_id:197285) that follows the rule of no identical adjacent layers is a valid close-packed structure. The phenomenon where an element or compound can exist in multiple different stacking sequences is known as **[polytypism](@entry_id:180847)**. A convenient shorthand for describing these structures is the **Ramsdell notation**, $nL$. Here, $n$ is an integer denoting the number of layers in the repeating unit (the periodicity), and $L$ is a letter indicating the resulting Bravais lattice type: C for Cubic, H for Hexagonal, or R for Rhombohedral.

Using this notation, the FCC structure is designated **3C** (3-layer repeat, Cubic lattice), and the HCP structure is **2H** (2-layer repeat, Hexagonal lattice). Many materials, such as silicon carbide (SiC), exhibit a rich variety of [polytypes](@entry_id:186015), including more complex sequences like **4H** (e.g., ABAC...) and **6H** (e.g., ABCACB...). Longer period repeats, such as **15R**, also exist and are characterized by a rhombohedral Bravais lattice [@problem_id:2808433].

#### Interstitial Sites

The empty spaces between the spheres in a close-packed structure are known as **[interstitial sites](@entry_id:149035)** or voids. These sites are critically important for forming alloys, for [diffusion mechanisms](@entry_id:158710), and for housing impurity atoms. There are two primary types of [interstitial sites](@entry_id:149035), named after the coordination polyhedron formed by the surrounding host atoms:

*   **Tetrahedral Sites:** A tetrahedral site is surrounded by four host atoms, whose centers form a regular tetrahedron. These sites are located at the center of the tetrahedra we discussed when deriving the interlayer spacing.
*   **Octahedral Sites:** An octahedral site is surrounded by six host atoms, forming a regular octahedron. These sites are located between two back-to-back triangular arrangements of atoms from adjacent layers.

In any close-packed structure, there is a fixed ratio of these sites to the host atoms. A detailed analysis of the FCC structure reveals that per [conventional unit cell](@entry_id:273158) (which contains 4 host atoms), there are 8 tetrahedral sites and 4 octahedral sites. This gives the fundamental ratio: for every one host atom, there are **two tetrahedral sites** and **one octahedral site** [@problem_id:2808518].

### Planar Defects: Stacking Faults and Partial Dislocations

Deviations from the perfect, infinite [stacking sequence](@entry_id:197285) constitute [planar defects](@entry_id:161449), which have profound effects on the mechanical and electronic properties of materials.

#### Stacking Faults

A **[stacking fault](@entry_id:144392)** is a one- or two-layer interruption in the regular [stacking sequence](@entry_id:197285). In an FCC (3C) crystal, two main types are defined:

*   **Intrinsic Stacking Fault:** This fault is formed by the effective *removal* of a single close-packed plane. For example, if we remove a C-plane from a perfect ...ABC**A**BC... sequence, the crystal above collapses, resulting in the sequence ...ABC|BC... . Because the layers relabel themselves to maintain the no-adjacent-rule, this becomes ...AB|A... . The full sequence across the fault is ...ABC**AB**ABC... The fault introduces a two-layer slab of local HCP (AB) stacking within the FCC matrix [@problem_id:2808520].

*   **Extrinsic Stacking Fault:** This fault is formed by the *insertion* of an extra close-packed plane. This disrupts a perfect ...ABCABC... sequence to become, for example, ...ABC**AC**ABC... . This fault introduces a two-layer slab of local HCP-like stacking (e.g., CAC) and can be viewed as two intrinsic faults on adjacent planes [@problem_id:2808520].

#### Shockley Partial Dislocations

Stacking faults are intimately connected to the motion of dislocations, the line defects responsible for plastic deformation in [crystalline materials](@entry_id:157810). A perfect dislocation in an FCC crystal, with a Burgers vector of type $\mathbf{b} = \frac{a}{2}\langle 110 \rangle$, can often lower its strain energy by dissociating into two **Shockley partial dislocations**, separated by a ribbon of intrinsic stacking fault.

The Burgers vector of a Shockley partial, $\mathbf{b}_p$, corresponds to the minimal vector required to shift atoms from one valid layer registry to the next, for instance, from an A-site to an adjacent B-site. A geometric derivation on the (111) plane shows that this vector is of the type $\frac{a}{6}\langle 112 \rangle$. The dissociation reaction can be written as:

$\frac{a}{2}[1\bar{1}0] \rightarrow \frac{a}{6}[2\bar{1}\bar{1}] + \frac{a}{6}[1\bar{2}1]$

This process is fundamental to the glide of dislocations and the mechanical behavior of FCC metals [@problem_id:2808430].

### The Energetics of Stacking: Why One Structure is Preferred

Given that the FCC and HCP structures are so similar—they have the same packing density and identical first and second nearest-neighbor coordinations—a critical question arises: what determines which structure an element prefers? The energy difference is exceedingly small and arises from very subtle effects.

#### Pair-Potential Models

One approach is to calculate the cohesive energy by summing pairwise interactions, such as the Lennard-Jones potential, over all neighbors. The energy difference per atom, $\Delta E = E_{fcc} - E_{hcp}$, can be expressed as a sum over coordination shells. Since the first two shells are identical for FCC and HCP, their contributions to $\Delta E$ cancel exactly. The first non-zero contribution comes from the third nearest neighbors and beyond. Calculations using a Lennard-Jones potential show that the energy difference is minuscule, on the order of $\Delta E / \varepsilon \approx -2 \times 10^{-4}$, where $\varepsilon$ is the potential well depth. This demonstrates that while one structure may be slightly favored (HCP in this case), the energy difference is so small that simple pair potentials are often insufficient to reliably predict the stable phase [@problem_id:2808508].

#### Electronic Structure Arguments

The true origin of the structural preference lies in the quantum mechanical nature of electrons in the solid, specifically the **band structure energy**. The total energy of the electrons depends on how their allowed energy states, described by the electronic band structure, are filled.

A powerful concept for understanding this is the interaction between the **Fermi surface** (the surface in reciprocal space enclosing all occupied electron states at zero temperature) and the **Brillouin zone** (the primitive cell of the [reciprocal lattice](@entry_id:136718)). According to the **Hume-Rothery mechanism**, a crystal structure is stabilized if its Brillouin zone boundaries happen to coincide with the Fermi surface. This contact opens an energy gap (or [pseudogap](@entry_id:143755)) in the [electronic density of states](@entry_id:182354), which lowers the overall band energy.

The FCC and HCP structures have Brillouin zones with different shapes and symmetries. For a given number of valence electrons per atom, the Fermi surface may make more favorable contact with the Brillouin zone of one structure over the other. For example, for some [early transition metals](@entry_id:153592), the nearly spherical Fermi surface can intersect multiple families of Brillouin zone planes in the HCP structure (e.g., the $\{10\bar{1}0\}$ and $\{0002\}$ planes) simultaneously. In the FCC structure, a similar Fermi surface might only make strong contact with one [family of planes](@entry_id:171035) (e.g., $\{111\}$). In such cases, the greater overall Fermi surface-Brillouin zone interaction can lead to a larger reduction in band energy, stabilizing the HCP structure over the FCC structure [@problem_id:2808488]. This delicate interplay between the geometry of the crystal lattice in [reciprocal space](@entry_id:139921) and the electronic filling ultimately tips the energetic balance, deciding the final, stable close-packed arrangement.