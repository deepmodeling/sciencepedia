## Introduction
The periodic arrangement of atoms in [crystalline solids](@entry_id:140223) is the key to understanding their wide-ranging physical properties, from mechanical strength to electronic behavior. To unlock this understanding, we require a precise mathematical framework to describe the underlying order of these materials. This article addresses this need by providing a detailed exploration of the crystal lattice, the conceptual scaffolding upon which real crystals are built. It bridges the gap between abstract geometry and tangible material characteristics.

This article unfolds across three key chapters. The first, **Principles and Mechanisms**, lays out the foundational language of crystallography, defining Bravais lattices, unit cells, and the powerful concept of the reciprocal lattice. Following this, the chapter on **Applications and Interdisciplinary Connections** demonstrates how this geometric blueprint dictates real-world phenomena in fields from materials science and chemistry to structural biology and photonics. Finally, **Hands-On Practices** will provide opportunities to solidify your understanding by applying these concepts to solve practical problems related to crystal geometry and properties.

## Principles and Mechanisms

The periodic arrangement of atoms in [crystalline solids](@entry_id:140223) is one of the most fundamental concepts in condensed matter physics. This underlying order is responsible for many of the macroscopic properties of materials, from their mechanical strength and [electrical conductivity](@entry_id:147828) to their optical characteristics. To understand these properties, we must first develop a precise mathematical language to describe the geometry of this atomic arrangement. This chapter lays out the foundational principles of [crystal lattices](@entry_id:148274), the distinction between a simple lattice and a real crystal structure, and the powerful concept of the [reciprocal lattice](@entry_id:136718), which is indispensable for analyzing wave phenomena in crystals.

### The Ideal Crystal: Bravais Lattices and Crystal Structures

At the heart of a perfect crystal is an idealized mathematical framework known as a lattice. It provides the scaffolding upon which the actual [atomic structure](@entry_id:137190) is built.

#### The Bravais Lattice: A Framework of Points

A **Bravais lattice** is an infinite array of discrete points with an arrangement and orientation that appear exactly the same from whichever of the points the array is viewed. This property of identical environment is the defining characteristic of a Bravais lattice. Formally, a three-dimensional Bravais lattice consists of all points with [position vectors](@entry_id:174826) $\mathbf{R}$ of the form:

$$\mathbf{R} = n_1 \mathbf{a}_1 + n_2 \mathbf{a}_2 + n_3 \mathbf{a}_3$$

where $n_1, n_2, n_3$ are any integers, and the vectors $\mathbf{a}_1, \mathbf{a}_2, \mathbf{a}_3$ are the **[primitive lattice vectors](@entry_id:270646)**. These three vectors must span the space, meaning they cannot be coplanar. Any point in the lattice can be reached from any other point by a **lattice translation vector** $\mathbf{T}$, which is itself a vector of the form of $\mathbf{R}$. The choice of [primitive vectors](@entry_id:142930) for a given lattice is not unique, but they always define a **[primitive unit cell](@entry_id:159354)**, a volume of space which, when translated by all [lattice translation vectors](@entry_id:197310), fills all of space without overlapping.

To illustrate, consider the **Face-Centered Cubic (FCC)** lattice, a common structure for metals like copper and aluminum. Its points can be described by a set of [primitive vectors](@entry_id:142930) relative to a conventional cubic cell of side length $a$. A standard choice for these vectors is:

$$\mathbf{a}_1 = \frac{a}{2}(\hat{\mathbf{y}} + \hat{\mathbf{z}}), \quad \mathbf{a}_2 = \frac{a}{2}(\hat{\mathbf{z}} + \hat{\mathbf{x}}), \quad \mathbf{a}_3 = \frac{a}{2}(\hat{\mathbf{x}} + \hat{\mathbf{y}})$$

where $\hat{\mathbf{x}}, \hat{\mathbf{y}}, \hat{\mathbf{z}}$ are orthonormal [unit vectors](@entry_id:165907) along the Cartesian axes. Using these, we can specify the position of any lattice point and calculate geometric properties. For instance, the lattice point described by the vector $\mathbf{R} = 2\mathbf{a}_1 - \mathbf{a}_2 + \mathbf{a}_3$ can be found by [vector addition](@entry_id:155045) [@problem_id:1811399]. Expressing $\mathbf{R}$ in Cartesian coordinates:

$$\mathbf{R} = 2\left(\frac{a}{2}(\hat{\mathbf{y}} + \hat{\mathbf{z}})\right) - \frac{a}{2}(\hat{\mathbf{z}} + \hat{\mathbf{x}}) + \frac{a}{2}(\hat{\mathbf{x}} + \hat{\mathbf{y}}) = a(0\hat{\mathbf{x}} + \frac{3}{2}\hat{\mathbf{y}} + \frac{1}{2}\hat{\mathbf{z}})$$

The squared distance from the origin to this point is simply the squared magnitude of $\mathbf{R}$, which is $|\mathbf{R}|^2 = (0)^2 + (\frac{3a}{2})^2 + (\frac{a}{2})^2 = \frac{9a^2}{4} + \frac{a^2}{4} = \frac{5}{2}a^2$. This exercise demonstrates how the abstract lattice is built from a few basis vectors, generating a perfectly regular, infinite structure.

#### Crystal Structure: Lattice with a Basis

A Bravais lattice is a purely geometric concept. A real crystal is formed by placing an identical group of one or more atoms, called the **basis**, at every point of a Bravais lattice. Therefore, we can summarize this fundamental concept as:

**Crystal Structure = Bravais Lattice + Basis**

This distinction is crucial. Many important and common crystal structures are *not* themselves Bravais [lattices](@entry_id:265277). This occurs when the basis contains more than one atom, and as a result, not all atomic positions in the crystal have identical environments.

A canonical example is the [diamond cubic structure](@entry_id:159542), adopted by silicon and germanium, the foundational materials of the semiconductor industry. The [diamond structure](@entry_id:199042) can be described as an FCC Bravais lattice with a two-atom basis. The two identical atoms in the basis are located at positions $\mathbf{b}_1 = (0,0,0)$ and $\mathbf{b}_2 = \frac{a}{4}(1,1,1)$ relative to each FCC lattice point [@problem_id:1811395]. This means the structure consists of two interpenetrating FCC sublattices, one shifted from the other by the vector $\mathbf{b}_2$.

To prove that the [diamond structure](@entry_id:199042) is not a Bravais lattice, we must show that the environment is not identical for all atoms. Consider an atom at a lattice site, for instance at the origin $(0,0,0)$ (from the first sublattice), and an atom at a basis-shifted site, like $(\frac{a}{4}, \frac{a}{4}, \frac{a}{4})$ (from the second sublattice). The four nearest neighbors of the atom at the origin form a tetrahedron oriented in one direction. However, the four nearest neighbors of the atom at $(\frac{a}{4}, \frac{a}{4}, \frac{a}{4})$ form a tetrahedron with the opposite orientation (an inverted tetrahedron). Since orientation is part of the environment, and these two orientations cannot be made to coincide by a pure translation, the two atomic sites are not equivalent. Thus, the [diamond structure](@entry_id:199042) is not a Bravais lattice. In contrast, any two atoms *within the same sublattice* (e.g., an atom at the origin and one at an FCC face center like $(\frac{a}{2}, \frac{a}{2}, 0)$) are related by a Bravais lattice translation and therefore have perfectly identical environments.

A simpler, hypothetical example further clarifies this point. Consider a structure described by points at the corners of a cubic lattice, $(n_1 a, n_2 a, n_3 a)$, and additional points at the centers of the "base" faces, $((n_1 + 1/2)a, (n_2 + 1/2)a, n_3 a)$ [@problem_id:1811398]. If we examine the environment of a corner point (e.g., at the origin) and a base-centered point (e.g., at $(a/2, a/2, 0)$), we find their neighborhoods are different. For the corner point, the nearest neighbors are four base-centered points at a distance of $a/\sqrt{2}$, and the next-nearest neighbors are six corner points at a distance of $a$. For the base-centered point, the nearest neighbors are four corner points at a distance of $a/\sqrt{2}$, but the next-nearest neighbors are six base-centered points at a distance of $a$. Because the *type* of next-nearest neighbors differs (corner vs. base-centered), the environments are not identical, and this structure is not a Bravais lattice.

### Describing the Lattice: Unit Cells

To work with infinite lattices, we isolate a finite repeating unit, the unit cell, which contains all the necessary information about the crystal's geometry.

#### Primitive and Conventional Unit Cells

A **unit cell** is a volume of space that, when translated through all the [lattice vectors](@entry_id:161583), perfectly tiles all of space without any overlaps or voids. While the shape of a unit cell can be chosen in many ways, the one with the smallest possible volume is called a **[primitive unit cell](@entry_id:159354)**. By definition, a [primitive unit cell](@entry_id:159354) contains exactly one lattice point.

Often, for reasons of conceptual clarity, a larger **[conventional unit cell](@entry_id:273158)** is used. Conventional cells are chosen to have a simple shape (e.g., a cube) and to clearly display the full [rotational symmetry](@entry_id:137077) of the lattice. For example, the [conventional cell](@entry_id:747851) of the FCC lattice is a cube with [lattice points](@entry_id:161785) at the 8 corners and 6 face centers. This cube is not a [primitive cell](@entry_id:136497); it contains more than one lattice point. By counting the fractions of points inside the cell (a corner point is shared by 8 cells, a face-center point by 2), we find the FCC [conventional cell](@entry_id:747851) contains $8 \times (1/8) + 6 \times (1/2) = 4$ lattice points.

Understanding the distinction between these cell types is essential for correctly determining the number of atoms within a repeating unit. Let's return to the [diamond cubic structure](@entry_id:159542) [@problem_id:1811332]. As established, it consists of an FCC lattice with a two-atom basis.
- The number of atoms in the **[conventional unit cell](@entry_id:273158)** is the number of [lattice points](@entry_id:161785) in that cell (4) multiplied by the number of atoms in the basis (2), giving a total of $N_{\text{conv}} = 4 \times 2 = 8$ atoms.
- The number of atoms in a **[primitive unit cell](@entry_id:159354)** is the number of [lattice points](@entry_id:161785) in that cell (always 1) multiplied by the number of atoms in the basis (2), giving a total of $N_{\text{prim}} = 1 \times 2 = 2$ atoms.
This shows that the density of atoms is consistent regardless of the cell chosen: the [conventional cell](@entry_id:747851) has 4 times the volume of the [primitive cell](@entry_id:136497) and also 4 times the number of atoms.

#### The Wigner-Seitz Cell

While the choice of primitive cell is not unique, there is one particularly useful and elegant construction known as the **Wigner-Seitz cell**. The Wigner-Seitz cell about a lattice point is defined as the region of space containing all points that are closer to that lattice point than to any other lattice point.

The construction is straightforward:
1.  Choose a lattice point and call it the origin.
2.  Draw vectors from the origin to all other [lattice points](@entry_id:161785) (in practice, only the nearest and sometimes next-nearest neighbors are needed).
3.  Construct the planes that are the [perpendicular bisectors](@entry_id:163148) of these vectors.
4.  The Wigner-Seitz cell is the smallest volume enclosed by these planes around the origin.

Let's construct this cell for a simple two-dimensional square lattice with [lattice constant](@entry_id:158935) $a$ [@problem_id:1811381]. Starting from the origin $(0,0)$, the nearest neighbors are at $(a,0), (-a,0), (0,a),$ and $(0,-a)$. The [perpendicular bisector](@entry_id:176427) of the vector to $(a,0)$ is the line $x = a/2$. Similarly, for the other three nearest neighbors, we get the lines $x = -a/2$, $y = a/2$, and $y = -a/2$. These four lines form a square centered at the origin. This square is the Wigner-Seitz cell. Its vertices are the points where these boundary lines intersect: $(\frac{a}{2}, \frac{a}{2}), (-\frac{a}{2}, \frac{a}{2}), (-\frac{a}{2}, -\frac{a}{2}),$ and $(\frac{a}{2}, -\frac{a}{2})$. This cell has the full symmetry of the square lattice and is a [primitive cell](@entry_id:136497).

### Symmetry in Lattices

The defining property of a crystal is its symmetry. Translational symmetry is built into the definition of a Bravais lattice, but lattices can also possess point symmetries, such as rotations and reflections, about a lattice point.

#### Permitted Rotational Symmetries

Not all rotational symmetries are compatible with the [translational symmetry](@entry_id:171614) of a Bravais lattice. A remarkable result, known as the **[crystallographic restriction theorem](@entry_id:137789)**, states that the only rotational symmetries a periodic lattice can possess are 2-fold, 3-fold, 4-fold, and 6-fold (and the trivial 1-fold). A 5-fold or 7-fold (or higher) [rotational symmetry](@entry_id:137077) is impossible.

We can prove this with a simple geometric argument [@problem_id:1811337]. Consider a lattice point $A$ and one of its nearest neighbors $B$, separated by a lattice vector $\mathbf{t}$. Assume the lattice has an $n$-fold rotational symmetry by an angle $\theta = 2\pi/n$ about any lattice point.
- If we rotate the entire lattice by $\theta$ about point $A$, point $B$ moves to a new position $B'$. Since this is a symmetry operation, $B'$ must also be a lattice point. The vector from $A$ to $B'$ is $\mathbf{t}' = R(\theta)\mathbf{t}$, where $R(\theta)$ is the [rotation operator](@entry_id:136702).
- Similarly, if we rotate the lattice by $-\theta$ about point $B$, point $A$ moves to a new position $A'$, which must also be a lattice point.
- The vector connecting the new lattice points $A'$ and $B'$, namely $\vec{B'} - \vec{A'}$, must also be a lattice vector. A geometric analysis reveals that this vector is parallel to $\mathbf{t}$ and can be written as $(2\cos\theta-1)\mathbf{t}$. Since this new vector must be an integer multiple of $\mathbf{t}$ (i.e., $m\mathbf{t}$ for some integer $m$), the quantity $2\cos\theta-1$ must be an integer.

This leads to the powerful condition:
$$ 2\cos\theta = m+1 = \text{integer} $$

Let's test the possible values for $n$-fold symmetry ($\theta=2\pi/n$):
- 2-fold ($n=2, \theta=\pi$): $2\cos(\pi) = -2$ (Integer, allowed)
- 3-fold ($n=3, \theta=2\pi/3$): $2\cos(2\pi/3) = -1$ (Integer, allowed)
- 4-fold ($n=4, \theta=\pi/2$): $2\cos(\pi/2) = 0$ (Integer, allowed)
- 6-fold ($n=6, \theta=\pi/3$): $2\cos(\pi/3) = 1$ (Integer, allowed)
- 5-fold ($n=5, \theta=2\pi/5$): $2\cos(2\pi/5) = (\sqrt{5}-1)/2 \approx 0.618$ (Not an integer, forbidden)

This elegant proof demonstrates why we cannot tile a plane with regular pentagons, and why five-fold symmetry, while common in molecules and [quasicrystals](@entry_id:141956), is forbidden in periodic Bravais lattices.

#### Building 3D Lattices: Stacking of Planes

Many common three-dimensional [crystal structures](@entry_id:151229) can be understood as different ways of stacking two-dimensional close-packed layers of atoms. A close-packed layer is the densest possible arrangement of spheres in a plane, like a rack of billiard balls.

Let us label the positions of atoms in the first layer as 'A'. To stack a second close-packed layer, its atoms must be placed in the hollows of the 'A' layer. There are two sets of hollows; we'll place the second layer in one of them and call its position 'B'. For the third layer, two possibilities exist to maintain close packing:
1.  Place the third layer's atoms directly above the 'A' layer atoms. This creates an **ABABAB...** [stacking sequence](@entry_id:197285). This structure has hexagonal symmetry and is known as the **Hexagonal Close-Packed (HCP)** structure.
2.  Place the third layer's atoms in the other set of hollows, which are not directly above either 'A' or 'B' atoms. We call this new position 'C'. This creates an **ABCABC...** [stacking sequence](@entry_id:197285) [@problem_id:1811357].

This ABC [stacking sequence](@entry_id:197285) is of particular importance because it generates the **Face-Centered Cubic (FCC)** lattice. The close-packed planes in the FCC structure correspond to the family of $\{111\}$ planes. If you view an FCC crystal along the $[111]$ direction (the body diagonal of the cube), you will see this precise ABC stacking of hexagonal layers.

### Directions and Planes in Crystals

To discuss physical processes that depend on directionality, such as deformation or wave propagation, we need a standardized way to specify directions and planes within the crystal lattice.

#### Crystallographic Planes and Miller Indices

The orientation of a plane in a crystal is specified by a set of three integers called **Miller indices**, denoted as $(hkl)$. The procedure for determining the Miller indices of a plane is as follows:
1.  Find the intercepts of the plane with the crystallographic axes, expressed as multiples of the [lattice parameters](@entry_id:191810) $a, b, c$. If a plane is parallel to an axis, its intercept is at infinity.
2.  Take the reciprocals of these numbers.
3.  Multiply by a common factor to clear any fractions and reduce the numbers to the smallest set of integers having the same ratio.

Let's find the Miller indices for a plane in an orthorhombic crystal that intercepts the axes at $x = a/2, y = b,$ and $z = c/3$ [@problem_id:1811390].
1.  The intercepts in units of the [lattice vectors](@entry_id:161583) are $(1/2, 1, 1/3)$.
2.  Taking the reciprocals gives $(2, 1, 3)$.
3.  These are already integers. So, the Miller indices for this plane are $(213)$.

If a plane is parallel to an axis, its intercept is $\infty$, and the reciprocal is $0$. For a plane intercepting the x-axis at $a$ and the z-axis at $-c/2$, while being parallel to the y-axis, the intercepts are $(1, \infty, -1/2)$. The reciprocals are $(1, 0, -2)$. The Miller indices are written as $(10\bar{2})$, where the bar denotes a negative intercept.

For lattices with orthogonal axes (cubic, tetragonal, orthorhombic), the vector normal to the plane $(hkl)$ has components proportional to $(h/a, k/b, l/c)$. In the special case of a cubic lattice, the direction $[hkl]$ is perpendicular to the plane $(hkl)$. This geometric relationship is extremely useful for calculating angles between crystal planes.

### The Reciprocal Lattice: A Dual Description

While the Bravais lattice (or "[real-space](@entry_id:754128)" lattice) describes the periodic positions of atoms, many physical phenomena, especially those involving waves, are more naturally described in a different, [dual space](@entry_id:146945): the **[reciprocal lattice](@entry_id:136718)**.

#### Definition and Importance

The [reciprocal lattice](@entry_id:136718) is a lattice in Fourier space (also known as [k-space](@entry_id:142033) or momentum space). Its points correspond to the set of [plane waves](@entry_id:189798) that have the same periodicity as the [real-space](@entry_id:754128) lattice. It is the natural framework for understanding X-ray diffraction, where scattering only occurs for momentum transfers that correspond to [reciprocal lattice vectors](@entry_id:263351), and for describing the behavior of electrons in a periodic potential, which leads to the formation of electronic band structures.

Given a set of [primitive vectors](@entry_id:142930) $\{\mathbf{a}_1, \mathbf{a}_2, \mathbf{a}_3\}$ for the real-space lattice, the [primitive vectors](@entry_id:142930) for the [reciprocal lattice](@entry_id:136718), $\{\mathbf{b}_1, \mathbf{b}_2, \mathbf{b}_3\}$, are defined by the condition:
$$ \mathbf{a}_i \cdot \mathbf{b}_j = 2\pi \delta_{ij} $$
where $\delta_{ij}$ is the Kronecker delta (1 if $i=j$, and 0 otherwise). This condition ensures that each reciprocal vector $\mathbf{b}_i$ is orthogonal to the real-space vectors $\mathbf{a}_j$ for $j \neq i$. This definition leads to the explicit construction formulas:
$$ \mathbf{b}_1 = 2\pi \frac{\mathbf{a}_2 \times \mathbf{a}_3}{V}, \quad \mathbf{b}_2 = 2\pi \frac{\mathbf{a}_3 \times \mathbf{a}_1}{V}, \quad \mathbf{b}_3 = 2\pi \frac{\mathbf{a}_1 \times \mathbf{a}_2}{V} $$
where $V = \mathbf{a}_1 \cdot (\mathbf{a}_2 \times \mathbf{a}_3)$ is the volume of the [real-space](@entry_id:754128) [primitive unit cell](@entry_id:159354).

#### The Duality of Real and Reciprocal Space

There is a beautiful duality between real and reciprocal lattices. A famous example is that the reciprocal lattice of a **Body-Centered Cubic (BCC)** lattice is a **Face-Centered Cubic (FCC)** lattice, and vice-versa.

Let's demonstrate this explicitly [@problem_id:1811356]. A set of [primitive vectors](@entry_id:142930) for a BCC lattice with [conventional cell](@entry_id:747851) side $a$ is:
$$\mathbf{a}_1 = \frac{a}{2}(\hat{\mathbf{x}} + \hat{\mathbf{y}} - \hat{\mathbf{z}}), \quad \mathbf{a}_2 = \frac{a}{2}(-\hat{\mathbf{x}} + \hat{\mathbf{y}} + \hat{\mathbf{z}}), \quad \mathbf{a}_3 = \frac{a}{2}(\hat{\mathbf{x}} - \hat{\mathbf{y}} + \hat{\mathbf{z}})$$

First, we calculate the volume of the [primitive cell](@entry_id:136497): $V = \mathbf{a}_1 \cdot (\mathbf{a}_2 \times \mathbf{a}_3) = a^3/2$. Then, we calculate the reciprocal vectors using the construction formulas. For example, for $\mathbf{b}_1$:
$$\mathbf{a}_2 \times \mathbf{a}_3 = \frac{a^2}{4} (-\hat{\mathbf{x}} + \hat{\mathbf{y}} + \hat{\mathbf{z}}) \times (\hat{\mathbf{x}} - \hat{\mathbf{y}} + \hat{\mathbf{z}}) = \frac{a^2}{4}(2\hat{\mathbf{x}} + 2\hat{\mathbf{y}}) = \frac{a^2}{2}(\hat{\mathbf{x}} + \hat{\mathbf{y}})$$
$$\mathbf{b}_1 = 2\pi \frac{\frac{a^2}{2}(\hat{\mathbf{x}} + \hat{\mathbf{y}})}{a^3/2} = \frac{2\pi}{a}(\hat{\mathbf{x}} + \hat{\mathbf{y}})$$

Performing similar calculations for $\mathbf{b}_2$ and $\mathbf{b}_3$ yields:
$$\mathbf{b}_1 = \frac{2\pi}{a}(\hat{\mathbf{x}} + \hat{\mathbf{y}}), \quad \mathbf{b}_2 = \frac{2\pi}{a}(\hat{\mathbf{y}} + \hat{\mathbf{z}}), \quad \mathbf{b}_3 = \frac{2\pi}{a}(\hat{\mathbf{z}} + \hat{\mathbf{x}})$$
These are, up to a scaling factor, precisely the form of the [primitive vectors](@entry_id:142930) for an FCC lattice. If we define the [conventional cell](@entry_id:747851) side length of this [reciprocal lattice](@entry_id:136718) as $a^*$, then its [primitive vectors](@entry_id:142930) are $\frac{a^*}{2}(\hat{\mathbf{x}}+\hat{\mathbf{y}})$, etc. Comparing the two sets of vectors, we see that $\frac{a^*}{2} = \frac{2\pi}{a}$, which gives the side length of the FCC [conventional cell](@entry_id:747851) in reciprocal space as $a^* = \frac{4\pi}{a}$. This inverse relationship between the lattice constants highlights the reciprocal nature of the two spaces: a large lattice in real space corresponds to a small one in reciprocal space, and vice-versa.

#### Applications of the Reciprocal Lattice

The [reciprocal lattice](@entry_id:136718) provides direct insight into the length scales of periodicity in a crystal. A [reciprocal lattice vector](@entry_id:276906) $\mathbf{G}$ can be shown to be normal to a family of lattice planes $(hkl)$ in the real-space lattice, and its magnitude is related to the spacing between these planes, $d_{hkl}$, by $|\mathbf{G}| = 2\pi/d_{hkl}$.

Consider a thought experiment where a probe scans along a specific line in a 2D square lattice, effectively creating a 1D crystal [@problem_id:1811355]. Let the 2D lattice have [primitive vectors](@entry_id:142930) $\mathbf{a}_1 = a\hat{\mathbf{i}}$ and $\mathbf{a}_2 = a\hat{\mathbf{j}}$. If the probe moves along the direction $\mathbf{v} = 3\hat{\mathbf{i}} + 4\hat{\mathbf{j}}$, the positions of the atoms projected onto this line form a 1D lattice. The spacing $d$ of this effective 1D lattice is the smallest projected distance between any two 2D [lattice points](@entry_id:161785). This spacing can be calculated to be $d = a/\sqrt{3^2+4^2} = a/5$. For any 1D lattice with spacing $d$, the magnitude of the smallest non-zero [reciprocal lattice vector](@entry_id:276906) is given by the fundamental relation $G_1 = 2\pi/d$. Therefore, for our effective 1D lattice, this magnitude is $G_1 = 2\pi / (a/5) = 10\pi/a$. This example illustrates the intimate connection between geometric spacing in real space and the fundamental length scale of the [reciprocal lattice](@entry_id:136718).