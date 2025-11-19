## Introduction
In the world of quantum chemistry, the elegant and often complex shapes of molecular orbitals are not random; they are strictly governed by the symmetry of the molecule they inhabit. This relationship between symmetry and electronic structure provides a profound framework for predicting and understanding nearly every aspect of chemical behavior, from bonding and structure to reactivity and spectroscopy. The key to unlocking this framework is a [formal language](@entry_id:153638) derived from mathematical group theory, which allows us to assign a specific **symmetry label** to every orbital. These labels, known as Mulliken symbols, offer a concise and powerful description of an orbital's properties. This article demystifies these labels, bridging the gap between abstract group theory and its practical chemical consequences.

This article is structured to build your expertise from the ground up. In **Principles and Mechanisms**, you will learn the fundamental language of symmetry, including operations, [character tables](@entry_id:146676), and the systematic rules for decoding and assigning Mulliken symbols to orbitals in molecules of varying complexity. Next, **Applications and Interdisciplinary Connections** will reveal the predictive power of these labels, exploring how they are used to construct [molecular orbital diagrams](@entry_id:155456), interpret spectroscopic data, explain the outcomes of chemical reactions, and even understand the properties of advanced materials. Finally, the **Hands-On Practices** section provides curated problems to help you solidify your skills and apply your newfound knowledge to real-world chemical scenarios.

## Principles and Mechanisms

In the study of quantum chemistry, the symmetry of a molecule provides a profound and powerful framework for classifying its [electronic states](@entry_id:171776) and understanding its chemical properties. Molecular orbitals, which describe the spatial distribution of electrons, are not arbitrary in shape; they must conform to the symmetry of the molecular framework. This conformance is rigorously described by assigning each orbital a **symmetry label**, a concise notation derived from the principles of mathematical group theory. These labels, known as **Mulliken symbols**, classify orbitals into **[irreducible representations](@entry_id:138184)** (irreps) of the molecule's point group. Understanding the principles behind these labels allows us to predict bonding interactions, interpret spectroscopic data, and rationalize [chemical reactivity](@entry_id:141717).

### The Language of Symmetry: Operations and Characters

The symmetry of a molecular orbital is defined by how its wavefunction, $\psi(\mathbf{r})$, behaves when subjected to the [symmetry operations](@entry_id:143398) of the molecule's point group. A symmetry operation is a transformation (like a rotation or reflection) that leaves the molecule's nuclear framework indistinguishable from its original state. When such an operation, represented by an operator $\hat{R}$, is applied to an orbital, the wavefunction may be left unchanged, inverted in sign, or transformed in a more complex manner.

The simplest way to quantify this transformation for one-dimensional (non-degenerate) orbitals is through the **character**, denoted by the Greek letter $\chi$. The character of an operation $\hat{R}$ for a given orbital $\psi$ is a single number that summarizes the transformation.

- If the orbital is symmetric with respect to the operation, $\hat{R}\psi = +\psi$, the character is $\chi(\hat{R}) = +1$.
- If the orbital is antisymmetric with respect to the operation, $\hat{R}\psi = -\psi$, the character is $\chi(\hat{R}) = -1$.

A fundamental symmetry operation that illustrates this concept is **inversion**, denoted by the operator $\hat{i}$. This operation transforms every point $(x, y, z)$ to $(-x, -y, -z)$ through a center of symmetry. Orbitals in molecules possessing an inversion center ([centrosymmetric molecules](@entry_id:166437)) are classified based on their behavior under this operation.
- An orbital that is symmetric with respect to inversion is termed **gerade** (German for "even") and is given the subscript **g**. For such an orbital, $\chi(i) = +1$.
- An orbital that is antisymmetric with respect to inversion is termed **ungerade** (German for "odd") and is given the subscript **u**. For such an orbital, $\chi(i) = -1$.

The parity of an atomic orbital is directly related to its angular momentum quantum number, $l$. The transformation is given by $\hat{i} \psi_l = (-1)^l \psi_l$. Consequently, s-orbitals ($l=0$) and d-orbitals ($l=2$) are inherently *gerade*, while p-orbitals ($l=1$) and [f-orbitals](@entry_id:153583) ($l=3$) are inherently *[ungerade](@entry_id:147965)*.

For instance, let's consider a $p_z$ orbital and a $d_{xy}$ orbital, both centered at the origin [@problem_id:1384807]. The wavefunction of a $p_z$ orbital is proportional to the coordinate $z$. Under inversion, $z \mapsto -z$, so the wavefunction flips its sign. It is *[ungerade](@entry_id:147965)*, and its character under inversion is $\chi(i) = -1$. In contrast, the $d_{xy}$ orbital has an angular dependence proportional to the product $xy$. Under inversion, this becomes $(-x)(-y) = xy$, leaving the wavefunction unchanged. It is *gerade*, with a character $\chi(i) = +1$.

### Irreducible Representations and Mulliken Symbols

While the character of a single operation is informative, a complete symmetry description requires examining the characters for all symmetry operations in the molecule's [point group](@entry_id:145002). The full set of characters for a given orbital constitutes a row in a **character table** and defines an **irreducible representation (irrep)** of the group. A Mulliken symbol is the conventional name for such an irrep.

Mulliken symbols have a systematic structure that encodes the key symmetry properties of the representation:

- **Dimensionality (Main Letter)**: The primary letter indicates the dimension of the irrep, which corresponds to the degeneracy of the orbitals belonging to it.
    - **A** and **B** denote one-dimensional irreps (non-[degenerate orbitals](@entry_id:154323)).
    - **E** denotes a two-dimensional irrep (doubly [degenerate orbitals](@entry_id:154323)).
    - **T** (or sometimes F) denotes a three-dimensional irrep (triply [degenerate orbitals](@entry_id:154323)).
    - **G** and **H** denote four- and five-dimensional irreps, respectively, found only in high-[symmetry groups](@entry_id:146083) like the icosahedral group.

- **Symmetry with respect to Principal Axis (A vs. B)**: For one-dimensional irreps, the distinction between **A** and **B** is made based on the character of the principal rotation axis, $C_n$.
    - **A** indicates symmetry with respect to the principal rotation ($\chi(C_n) = +1$).
    - **B** indicates antisymmetry with respect to the principal rotation ($\chi(C_n) = -1$).

- **Subscripts `1` and `2`**: These further distinguish one-dimensional irreps based on their symmetry with respect to a secondary operation, typically a $C_2$ axis perpendicular to the principal axis or a vertical [mirror plane](@entry_id:148117) ($\sigma_v$). A subscript of **1** indicates symmetry ($\chi = +1$), while **2** indicates [antisymmetry](@entry_id:261893) ($\chi = -1$).

- **Superscripts `'` and `''`**: These are used for irreps in [point groups](@entry_id:142456) that contain a horizontal mirror plane, $\sigma_h$. A single prime (**`'`**) indicates symmetry with respect to this plane ($\chi(\sigma_h) = +1$), while a double prime (**`''`**) indicates [antisymmetry](@entry_id:261893) ($\chi(\sigma_h) = -1$).

- **Subscripts `g` and `u`**: As previously discussed, these denote symmetry with respect to inversion in centrosymmetric [point groups](@entry_id:142456).

### Assigning Symmetry Labels: A Systematic Approach

The process of assigning a Mulliken symbol involves determining the characters of an orbital under the [symmetry operations](@entry_id:143398) of its [point group](@entry_id:145002) and matching this set of characters to a row in the group's character table.

#### The Simplest Case: The $C_1$ Point Group

The power and logic of group theory are elegantly demonstrated even in the simplest possible case: a molecule with no [symmetry elements](@entry_id:136566) other than the trivial identity operation, $E$. Such a molecule, for example the chiral bromochlorofluoromethane ($\text{CHFClBr}$), belongs to the $C_1$ [point group](@entry_id:145002) [@problem_id:1384811].

A fundamental theorem of group theory states that the sum of the squares of the dimensions ($d_i$) of the irreps must equal the order of the group ($h$, the number of [symmetry operations](@entry_id:143398)). For the $C_1$ group, $h=1$. Thus, $\sum d_i^2 = 1$. The only integer solution is a single irrep of dimension $d_1=1$. This means the $C_1$ [point group](@entry_id:145002) has only one irreducible representation, and it is one-dimensional.

The character for the identity operation, $\chi(E)$, is always equal to the dimension of the irrep, so here $\chi(E) = 1$. Since this is the only operation, the complete set of characters is simply $\{1\}$. An irrep whose characters are all $+1$ is known as the **totally symmetric representation**. For a one-dimensional irrep, the main letter is A or B. Since there is no principal axis to distinguish them, the totally symmetric representation is universally labeled **A**. Because there is only one irrep, no subscripts are needed. Therefore, the single [irreducible representation](@entry_id:142733) of the $C_1$ group is **A**. Consequently, every molecular orbital in a $C_1$ molecule must transform according to this irrep, and all orbitals are assigned the symmetry label A.

#### Orbitals on a Central Atom

For molecules with higher symmetry, the assignment process becomes more involved. Consider an atomic orbital on an atom located at the center of the coordinate system, which is also the intersection of all [symmetry elements](@entry_id:136566).

A good example is classifying the valence p-orbitals in a molecule of $D_{3h}$ symmetry, such as boron trichloride ($\text{BCl}_3$), with the boron atom at the origin and the molecule in the $xy$-plane [@problem_id:2297476]. The $p_z$ orbital is aligned with the principal $C_3$ axis ($z$-axis). It is unchanged by rotation about this axis ($\chi(C_3)=+1$) but is inverted by reflection through the horizontal plane $\sigma_h$ (the $xy$-plane), yielding $\chi(\sigma_h)=-1$. By inspecting the $D_{3h}$ [character table](@entry_id:145187), we find these properties match the **$A_2''$** irrep.

The $p_x$ and $p_y$ orbitals, however, cannot be treated in isolation. As a degenerate pair, they transform together. A $C_3$ rotation by $120^{\circ}$ will mix the $x$ and $y$ coordinates. The character for a degenerate set of orbitals is the trace of the matrix that describes their transformation. For a rotation by angle $\theta$ in a 2D space, the character is $2\cos(\theta)$. For the $C_3$ operation, $\theta = 120^\circ$, so $\chi(C_3) = 2\cos(120^\circ) = -1$. Under the $\sigma_h$ reflection, the $p_x$ and $p_y$ orbitals are in the plane and remain unchanged, so the transformation is the identity matrix in 2D, giving a character of $\chi(\sigma_h) = 2$. This set of characters, along with others, unambiguously identifies the $(p_x, p_y)$ pair as belonging to the **$E'$** [irreducible representation](@entry_id:142733).

This principle extends to all point groups. For ammonia ($\text{NH}_3$), which has $C_{3v}$ symmetry, the degenerate $(p_x, p_y)$ orbitals on the central nitrogen atom transform together. By analyzing their transformations under the $C_{3v}$ operations ($E, C_3, \sigma_v$), we find the characters to be $(2, -1, 0)$, which corresponds to the **E** irrep in the $C_{3v}$ [character table](@entry_id:145187) [@problem_id:1384780].

#### High-Symmetry Environments

In highly symmetric systems, such as octahedral ($O_h$) or icosahedral ($I_h$) complexes, orbitals can exhibit higher degeneracies. In any [point group](@entry_id:145002), there exists one unique irrep for which all characters are $+1$. This is the **totally symmetric representation**, labeled **$A_{1g}$** in the $O_h$ group. Any orbital or combination of orbitals that is completely invariant under every symmetry operation of the group, such as the in-phase sum of all six ligand [sigma orbitals](@entry_id:165959) in an octahedral complex, will have this symmetry [@problem_id:1384808].

In the exceptionally high symmetry of an icosahedral field, such as that experienced by an atom at the center of a buckminsterfullerene ($\text{C}_{60}$) cage, the five atomic d-orbitals can remain degenerate. The [d-orbitals](@entry_id:261792) are five-dimensional ($d=5$) and have [even parity](@entry_id:172953) (gerade, since $l=2$). Consulting the [character table](@entry_id:145187) for the $I_h$ point group reveals only one irrep that fits this description: **$H_g$**. This indicates that in such a symmetric environment, the [d-orbitals](@entry_id:261792) transform as a single, five-fold degenerate set [@problem_id:1384812].

### Symmetry of Molecular Orbitals and SALCs

The principles of symmetry labeling apply with equal rigor to [molecular orbitals](@entry_id:266230) (MOs) formed from [linear combinations](@entry_id:154743) of atomic orbitals (LCAOs). Before constructing MO diagrams, it is often convenient to first form **Symmetry-Adapted Linear Combinations (SALCs)** from the basis of atomic orbitals. Each SALC by definition transforms as a pure [irreducible representation](@entry_id:142733) of the [molecular point group](@entry_id:191277).

Consider the two hydrogen 1s orbitals in a water molecule ($\text{H}_2\text{O}$, [point group](@entry_id:145002) $C_{2v}$). These two orbitals, $1s_{H_a}$ and $1s_{H_b}$, can form two SALCs. Let us determine the symmetry of the out-of-phase combination, $\psi = 1s_{H_a} - 1s_{H_b}$ [@problem_id:1384783]. We analyze its transformation under the operations of the $C_{2v}$ group, noting that the operations will permute the positions of atoms $H_a$ and $H_b$.
- **$E$**: The identity leaves both orbitals untouched. $\hat{E}\psi = 1s_{H_a} - 1s_{H_b} = \psi$. So, $\chi(E)=1$.
- **$C_2(z)$**: This rotation exchanges the two hydrogen atoms. $\hat{C}_2\psi = 1s_{H_b} - 1s_{H_a} = - (1s_{H_a} - 1s_{H_b}) = -\psi$. So, $\chi(C_2)=-1$.
- **$\sigma_v(xz)$**: This reflection plane bisects the H-O-H angle and also exchanges the two hydrogen atoms. $\hat{\sigma}_v(xz)\psi = 1s_{H_b} - 1s_{H_a} = -\psi$. So, $\chi(\sigma_v(xz))=-1$.
- **$\sigma_v'(yz)$**: This is the molecular plane, which contains both hydrogen atoms. They are not moved. $\hat{\sigma}_v'(yz)\psi = 1s_{H_a} - 1s_{H_b} = \psi$. So, $\chi(\sigma_v'(yz))=1$.

The resulting character set is $(1, -1, -1, 1)$. Comparing this to the $C_{2v}$ character table, we find it corresponds to the **$B_2$** irreducible representation.

This same logic applies to the MOs of [diatomic molecules](@entry_id:148655). For a homonuclear [diatomic molecule](@entry_id:194513) (point group $D_{\infty h}$), the MOs are classified by their [angular momentum projection](@entry_id:746441) ($\sigma, \pi, \delta, ...$) and their parity ($g, u$). Let's re-examine the concept of parity with the $\sigma_{1s}^*$ [antibonding orbital](@entry_id:261662), formed from $\psi_{\sigma^*} = N(\phi_{1s, A} - \phi_{1s, B})$, where A and B are the two nuclei [@problem_id:1384787]. The inversion operation swaps the positions of nuclei A and B. Since 1s orbitals are spherically symmetric, the orbital on A becomes an identical orbital on B, and vice versa.
$$ \hat{i}\psi_{\sigma^*} = N(\phi_{1s, B} - \phi_{1s, A}) = -N(\phi_{1s, A} - \phi_{1s, B}) = -\psi_{\sigma^*} $$
The wavefunction changes sign upon inversion, so the $\sigma_{1s}^*$ orbital is **[ungerade](@entry_id:147965)**, labeled $\sigma_u$. A similar analysis can be applied to all MOs formed from the valence $2s$ and $2p$ atomic orbitals. The symmetry of each MO is a direct consequence of the symmetry of the constituent AOs and the phase relationship (bonding or antibonding) of the combination [@problem_id:1384828]. For example:
- $\Psi = \phi_{2s,A} + \phi_{2s,B}$ transforms as $\mathbf{\sigma_g}$.
- $\Psi = \phi_{2p_z,A} + \phi_{2p_z,B}$ transforms as $\mathbf{\sigma_g}$.
- $\Psi = \phi_{2p_x,A} + \phi_{2p_x,B}$ transforms as $\mathbf{\pi_u}$.
- $\Psi = \phi_{2p_y,A} - \phi_{2p_y,B}$ transforms as $\mathbf{\pi_g}$.

Finally, symmetry labels can often be assigned by visual inspection of an orbital's [nodal planes](@entry_id:149354) and phase patterns, combined with knowledge of the group's [symmetry operations](@entry_id:143398) and axis conventions. For example, consider a $\pi$-type MO in formaldehyde ($\text{CH}_2\text{O}$, point group $C_{2v}$) constructed from the out-of-phase combination of $p_x$ orbitals on the carbon and oxygen atoms, perpendicular to the molecular plane [@problem_id:1384818]. A $C_2$ rotation about the C=O bond axis ($z$-axis) inverts the $x$-coordinate, flipping the phase of the entire orbital ($\chi=-1$). Reflection through the $xz$-plane leaves the $x$-coordinate unchanged ($\chi=+1$), while reflection through the $yz$-plane (the molecular plane) inverts the $x$-coordinate ($\chi=-1$). This character set $(1, -1, 1, -1)$ identifies the orbital as having **$B_1$** symmetry.

In summary, [orbital symmetry](@entry_id:142623) labels are not mere descriptive tags; they are a direct consequence of the mathematical properties of wavefunctions in the symmetric environment of a molecule. Mastering the principles behind these labels is a foundational skill in modern chemistry, enabling a deeper, more predictive understanding of [molecular structure](@entry_id:140109) and behavior.