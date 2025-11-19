## Introduction
The three-dimensional arrangement of atoms in a molecule is fundamental to its identity, dictating its reactivity, polarity, and biological role. But how can we predict this intricate geometry from a simple [chemical formula](@entry_id:143936)? This article explores a powerful predictive tool: the Valence Shell Electron Pair Repulsion (VSEPR) model. Based on the simple principle that electron pairs repel each other, VSEPR theory provides a systematic framework for determining molecular shapes and [bond angles](@entry_id:136856). In the chapters that follow, you will first delve into the **Principles and Mechanisms** of the VSEPR model, learning to distinguish between electron-domain and molecular geometries and understanding the factors that cause [bond angles](@entry_id:136856) to deviate from ideal values. Next, the section on **Applications and Interdisciplinary Connections** will demonstrate how these geometric principles explain macroscopic properties and are applied in fields from [organic chemistry](@entry_id:137733) to materials science. Finally, **Hands-On Practices** will allow you to apply your knowledge to solve concrete chemical problems, solidifying your understanding of this cornerstone of chemical theory.

## Principles and Mechanisms

The three-dimensional arrangement of atoms in a molecule—its geometry—is a principal determinant of its physical and chemical properties, including its polarity, reactivity, and biological function. The Valence Shell Electron Pair Repulsion (VSEPR) model provides a remarkably powerful, albeit qualitative, framework for predicting molecular shapes based on a simple electrostatic principle: electron pairs in the valence shell of a central atom arrange themselves to minimize repulsion, thereby maximizing the distance between them. This chapter will systematically develop the principles of the VSEPR model, explore its application in predicting geometries and bond angles, and examine the nuances and exceptions that provide a more complete picture of [molecular structure](@entry_id:140109).

### The Electron Domain Model

The cornerstone of VSEPR theory is the concept of an **electron domain**, which represents a region of localized electron density in the valence shell of a central atom. An electron domain can be a non-bonding pair of electrons (**lone pair**) or it can be the electrons in a covalent bond. Crucially, for the purpose of determining geometry, it does not matter whether a bond is single, double, or triple. All share a common axis between two nuclei and are thus confined to the same general region of space. Therefore, a single bond, a double bond, and a triple bond each count as a single electron domain.

For instance, consider the central carbon atom in ethyne ($\mathrm{H-C\equiv C-H}$), hydrogen [cyanide](@entry_id:154235) ($\mathrm{H-C\equiv N}$), and carbon dioxide ($\mathrm{O=C=O}$). In each case, the central carbon atom is surrounded by only two electron domains: a single bond and a triple bond in ethyne and hydrogen [cyanide](@entry_id:154235), and two double bonds in carbon dioxide. The VSEPR model predicts that to minimize repulsion, these two domains will position themselves on opposite sides of the central atom, leading to a linear geometry with [bond angles](@entry_id:136856) of $180^\circ$ in all three molecules [@problem_id:2013346].

The total number of electron domains around a central atom is called its **steric number (SN)**, calculated as:

$SN = (\text{number of bonded atoms}) + (\text{number of lone pairs on the central atom})$

The steric number dictates the parent geometry for the arrangement of electron domains, known as the **[electron-domain geometry](@entry_id:136747)**.

### Ideal Geometries Based on Steric Number

When a central atom is bonded only to other atoms and has no lone pairs, the repulsion between all electron domains is identical. This leads to highly symmetrical arrangements that represent the ideal geometries for a given steric number.

*   **SN = 2:** Two electron domains result in a **linear** [electron-domain geometry](@entry_id:136747) with an ideal bond angle of $180^\circ$. Examples include $\mathrm{CO_2}$, $\mathrm{BeCl_2}$, and $\mathrm{HCN}$.

*   **SN = 3:** Three electron domains arrange themselves in a **[trigonal planar](@entry_id:147464)** geometry. The domains lie in a single plane and point towards the vertices of an equilateral triangle, with ideal [bond angles](@entry_id:136856) of $120^\circ$. A classic example is sulfur trioxide, $\mathrm{SO_3}$, where the central sulfur atom is bonded to three oxygen atoms with no lone pairs [@problem_id:2013300]. Another is the nitrate ion, $\mathrm{NO_3^{-}}$, which, due to resonance, has three equivalent N-O bonds and a trigonal planar geometry [@problem_id:2013313].

*   **SN = 4:** Four electron domains produce a **tetrahedral** geometry, where the domains point to the vertices of a tetrahedron. This three-dimensional arrangement results in an ideal bond angle of $109.5^\circ$. Methane ($\mathrm{CH_4}$) and [tetramethylsilane](@entry_id:755877) ($\mathrm{Si(CH_3)_4}$) are quintessential examples. The geometry is so regular that, given a Si-C bond length of $R$, the coordinates of the carbon atoms can be precisely calculated relative to the central silicon atom [@problem_id:2013307].

*   **SN = 5:** Five electron domains adopt a **[trigonal bipyramidal](@entry_id:141216)** geometry. This shape is composed of two distinct types of positions: three **equatorial** positions arranged in a trigonal plane ($120^\circ$ apart) and two **axial** positions located above and below this plane ($90^\circ$ to the equatorial plane). The angle between the two axial positions is $180^\circ$. Phosphorus pentafluoride ($\mathrm{PF_5}$) is a typical example [@problem_id:2013352].

*   **SN = 6:** Six electron domains lead to an **octahedral** geometry. All six positions are equivalent, pointing to the vertices of an octahedron. All adjacent bond angles are $90^\circ$. Sulfur hexafluoride ($\mathrm{SF_6}$) exemplifies this arrangement.

### The Influence of Lone Pairs: Molecular vs. Electron-Domain Geometry

The presence of [lone pairs](@entry_id:188362) on the central atom introduces a crucial distinction. The **[electron-domain geometry](@entry_id:136747)** still describes the arrangement of all electron domains (bonding pairs and lone pairs), but the **[molecular geometry](@entry_id:137852)** describes the arrangement of only the atoms. Lone pairs are electronically significant and dictate the positions of the atoms, but they are not included when naming the final [molecular shape](@entry_id:142029).

This distinction is complicated by the fact that repulsions involving lone pairs are not equivalent to those of bonding pairs. The electron cloud of a lone pair is under the influence of only one atomic nucleus, making it more diffuse and spatially demanding than a bonding pair, which is localized between two nuclei. This leads to a fundamental hierarchy of repulsion strengths [@problem_id:2013305]:

**Lone Pair-Lone Pair (LP-LP) > Lone Pair-Bonding Pair (LP-BP) > Bonding Pair-Bonding Pair (BP-BP)**

This hierarchy has profound consequences, causing [bond angles](@entry_id:136856) to deviate from their ideal values and dictating the preferred positions of lone pairs in less symmetrical geometries.

Let's explore the molecular geometries that arise from parent electron-domain geometries when lone pairs are present. We use the notation $AX_nE_m$, where $A$ is the central atom, $X$ is a bonded atom, and $E$ is a lone pair.

**From a Tetrahedral Electron Domain (SN = 4):**
*   **$AX_3E_1$**: The four electron domains are arranged tetrahedrally, but one position is a lone pair. The resulting [molecular geometry](@entry_id:137852) is **trigonal pyramidal**. The stronger LP-BP repulsions push the three bonding pairs closer together, compressing the X-A-X bond angle to a value less than the ideal $109.5^\circ$. Ammonia ($\mathrm{NH_3}$) is a prime example, with an H-N-H angle of $\approx 107.8^\circ$.
*   **$AX_2E_2$**: Two lone pairs occupy two vertices of the tetrahedron. The remaining two bonding pairs give the molecule a **bent** (or angular) shape. With two highly repulsive [lone pairs](@entry_id:188362), the bond angle compression is even more severe. In water ($\mathrm{H_2O}$), the H-O-H angle is approximately $104.5^\circ$ [@problem_id:2013320].

**From a Trigonal Bipyramidal Electron Domain (SN = 5):**
In a trigonal bipyramid, the positions are not equivalent. A lone pair placed in an axial position would experience three strong $90^\circ$ LP-BP repulsions with the equatorial domains. A lone pair in an equatorial position experiences only two such $90^\circ$ repulsions with the axial domains. To minimize total repulsion, **lone pairs always occupy equatorial positions in a [trigonal bipyramidal](@entry_id:141216) arrangement.**
*   **$AX_4E_1$**: One lone pair occupies an equatorial site. The four bonded atoms occupy the remaining two axial and two equatorial positions. This arrangement is called a **seesaw** (or disphenoidal) geometry [@problem_id:2013315] [@problem_id:2013339]. An example is tellurium tetrachloride, $\mathrm{TeCl_4}$ [@problem_id:2013351].
*   **$AX_3E_2$**: Two [lone pairs](@entry_id:188362) occupy two of the three equatorial positions. The three bonded atoms are arranged in a **T-shaped** geometry, with two atoms in axial positions and one in an equatorial position [@problem_id:2013347].
*   **$AX_2E_3$**: With three lone pairs occupying all three equatorial positions, the two bonded atoms are forced into the axial positions, resulting in a **linear** molecular geometry.

**From an Octahedral Electron Domain (SN = 6):**
In an octahedron, all positions are initially equivalent. The first lone pair can be placed anywhere. To minimize the powerful LP-LP repulsion, a second lone pair must be placed on the opposite side of the central atom (a *trans* arrangement at $180^\circ$).
*   **$AX_5E_1$**: One lone pair results in a **square pyramidal** [molecular geometry](@entry_id:137852).
*   **$AX_4E_2$**: The two [lone pairs](@entry_id:188362) are trans to each other, leaving the four bonded atoms in a single plane. This results in a **square planar** molecular geometry, with bond angles of $90^\circ$. The tetrachlorobromate(III) ion, $[\mathrm{BrCl_4}]^{-}$, is an example of this structure [@problem_id:2013332].

The comparison of the nitronium ion ($\mathrm{NO_2^{+}}$), nitrite ion ($\mathrm{NO_2^{-}}$), and nitrate ion ($\mathrm{NO_3^{-}}$) provides an excellent summary. $\mathrm{NO_2^{+}}$ (SN=2, $AX_2$) is linear. $\mathrm{NO_3^{-}}$ (SN=3, $AX_3$) is trigonal planar. $\mathrm{NO_2^{-}}$ also has SN=3, but its formula is $AX_2E_1$, giving it a [trigonal planar](@entry_id:147464) [electron-domain geometry](@entry_id:136747) but a bent [molecular geometry](@entry_id:137852) [@problem_id:2013313].

### Factors Causing Deviations in Bond Angles

Beyond the primary compression caused by [lone pairs](@entry_id:188362), several secondary effects can fine-tune [bond angles](@entry_id:136856). Understanding these factors allows for more precise predictions and comparisons between related molecules.

1.  **Multiple Bonds:** A double or [triple bond](@entry_id:202498), while counted as a single domain, contains a higher density of electrons than a single bond. It therefore exerts a greater repulsive force on adjacent electron domains. In phosgene ($\mathrm{COCl_2}$), the central carbon has three electron domains (one C=O double bond, two C-Cl single bonds), leading to a [trigonal planar](@entry_id:147464) geometry. The "larger" C=O domain repels the C-Cl domains more strongly, compressing the Cl-C-Cl bond angle to a value less than the ideal $120^\circ$ [@problem_id:2013345].

2.  **Ligand Electronegativity:** Highly electronegative ligand atoms pull the electrons in the bonding pair further away from the central atom. This reduces the electron density of the bonding domain near the central atom, weakening its repulsive power. Consequently, [lone pairs](@entry_id:188362) or other domains can compress the bond angle more effectively. This is clearly seen in the phosphorus trihalide series ($\mathrm{PX_3}$). As the halogen electronegativity decreases from F to Br, the P-X bonding pair density shifts closer to the phosphorus atom, increasing BP-BP repulsion and widening the X-P-X bond angle. Thus, the bond angles follow the trend $\mathrm{PF_3}  \mathrm{PCl_3}  \mathrm{PBr_3}$ [@problem_id:2013314]. A similar effect explains why the F-N-F angle in $\mathrm{NF_3}$ ($\approx 102.5^\circ$) is significantly smaller than the H-N-H angle in $\mathrm{NH_3}$ ($\approx 107.8^\circ$) [@problem_id:2013309].

3.  **Steric Hindrance:** Very large or "bulky" ligand groups can physically crowd each other, creating [steric repulsion](@entry_id:169266) that forces them apart. This effect counteracts the compression from [lone pairs](@entry_id:188362) and can lead to wider bond angles. The most striking example is trimethylamine, $\mathrm{N(CH_3)_3}$. Despite having the same $AX_3E_1$ structure as ammonia, the bulky methyl groups repel each other so strongly that the C-N-C bond angle ($108.7^\circ$) is pushed open, becoming much closer to the ideal tetrahedral angle than in ammonia [@problem_id:2013309].

4.  **Competing Effects:** Often, these factors are in competition. In the series $\mathrm{H_2O}$, $\mathrm{OF_2}$, and $\mathrm{Cl_2O}$, all molecules are bent ($AX_2E_2$). In $\mathrm{OF_2}$, the extreme electronegativity of fluorine pulls bonding electrons away from oxygen, allowing the lone pairs to dramatically compress the angle to $\approx 103^\circ$. In $\mathrm{Cl_2O}$, chlorine is less electronegative than oxygen but is a much larger atom than hydrogen or fluorine. Here, the [steric repulsion](@entry_id:169266) between the two large chlorine atoms dominates, prying the bond angle open to $\approx 111^\circ$, a value larger than in water. Thus, the final order of bond angles is $\theta_{\mathrm{Cl_2O}} > \theta_{\mathrm{H_2O}} > \theta_{\mathrm{OF_2}}$ [@problem_id:201297]. A more subtle case is the comparison of phosgene ($\mathrm{COCl_2}$) and thiophosgene ($\mathrm{CSCl_2}$). Since oxygen is more electronegative than sulfur, the C=O bond's electron density is pulled further from the central carbon than that of the C=S bond. The C=S domain is therefore effectively "larger" at the central atom, exerting more repulsion and compressing the Cl-C-Cl angle in thiophosgene more than in phosgene. This leads to the relationship $\angle_{\text{Cl-C-Cl, CSCl}_2}  \angle_{\text{Cl-C-Cl, COCl}_2}  120^\circ$ [@problem_id:2013327].

### Molecular Geometry and Polarity

A [covalent bond](@entry_id:146178) between two atoms of different [electronegativity](@entry_id:147633) is polar, creating a **bond dipole**. The overall polarity of a molecule is determined by its **net dipole moment**, which is the vector sum of all its individual bond dipoles. A molecule's geometry is the critical factor in determining whether these vectors cancel out.

A molecule will be **nonpolar** if it meets two conditions:
1.  All terminal atoms are identical.
2.  The arrangement of terminal atoms is perfectly symmetrical (linear, trigonal planar, tetrahedral, [trigonal bipyramidal](@entry_id:141216), octahedral) and there are no [lone pairs](@entry_id:188362) on the central atom.

In such cases, the bond dipoles are arranged symmetrically and their vector sum is zero. For example, in sulfur trioxide ($\mathrm{SO_3}$), the three polar S-O bonds are arranged in a [trigonal planar](@entry_id:147464) geometry. The three bond dipole vectors, pointing from the central S to the vertices of an equilateral triangle, perfectly cancel, rendering the molecule nonpolar [@problem_id:2013300].

Conversely, a molecule is almost always **polar** if:
1.  It contains lone pairs on the central atom that break the symmetry (e.g., bent $\mathrm{SO_2}$, trigonal pyramidal $\mathrm{NH_3}$).
2.  It contains different terminal atoms, as this breaks the symmetry of the dipole magnitudes (e.g., $\mathrm{CH_3Cl}$).

A fascinating case is a [trigonal bipyramidal](@entry_id:141216) molecule like $\mathrm{PnBr_4F}$, a hypothetical derivative of the nonpolar $\mathrm{PnF_5}$. Whether the single fluorine atom occupies an axial or an equatorial position, the symmetry is broken. The Pn-F bond dipole has a different magnitude than the Pn-Br dipoles, making it impossible for the vectors to cancel. Therefore, both possible isomers of $\mathrm{PnBr_4F}$ are polar [@problem_id:2013352].

### Advanced Topics and Limitations of VSEPR

While VSEPR is a powerful predictive tool, it is a simplified model. Certain phenomena require more advanced concepts to be fully understood.

**Valence Bond Theory and Hybridization**
VSEPR theory provides the shape, and [valence bond theory](@entry_id:145047) provides a quantum mechanical rationale using the concept of **hybrid orbitals**. The steric number often directly predicts the [hybridization](@entry_id:145080) of the central atom: SN=2 implies $sp$ [hybridization](@entry_id:145080) (linear), SN=3 implies $sp^2$ ([trigonal planar](@entry_id:147464)), and SN=4 implies $sp^3$ (tetrahedral) [@problem_id:2013345]. However, for heavier elements, this direct correspondence can break down.

**The Failure of Hybridization for Heavy Elements**
For [hydrides](@entry_id:154188) of third-period elements and below (e.g., phosphine $\mathrm{PH_3}$, hydrogen sulfide $\mathrm{H_2S}$), observed [bond angles](@entry_id:136856) are close to $90^\circ$, not the $\approx 109.5^\circ$ predicted for a tetrahedral [electron geometry](@entry_id:191006). This suggests that hybridization is not occurring. The energetic cost of promoting an electron from the $s$ orbital to a $p$ orbital to form [hybrid orbitals](@entry_id:260757) is significant. For smaller atoms like nitrogen, this cost is more than offset by the formation of stronger bonds and reduced repulsion. For larger atoms like phosphorus, this energetic benefit is smaller. A simplified energy analysis can show that for $\mathrm{PH_3}$, a model where bonding occurs via overlap of the three orthogonal $3p$ orbitals of phosphorus with hydrogen $1s$ orbitals (predicting $90^\circ$ angles) is energetically more favorable than an $sp^3$ hybridized model [@problem_id:2013304]. In this "unhybridized" picture, the lone pair resides in the low-energy $3s$ orbital.

**Stereochemically Inactive Lone Pairs**
For very heavy central atoms with high coordination numbers, a lone pair can sometimes fail to influence the molecular geometry, becoming **stereochemically inactive**. This "inert pair" occupies a spherical, non-directional valence $s$ orbital. This is observed in the hexachlorotellurate(IV) ion, $[\mathrm{TeCl_6}]^{2-}$. VSEPR would predict a distorted shape from its $AX_6E_1$ classification, but the ion is perfectly octahedral. In contrast, the hexafluoroiodate(V) ion, $[\mathrm{IF_6}]^{-}$, which is also $AX_6E_1$, exhibits the expected distortion. The tendency for a lone pair to be active is influenced by factors like the [oxidation state](@entry_id:137577) of the central atom and the electronegativity of the ligands, with higher [oxidation states](@entry_id:151011) and more electronegative ligands generally promoting stereochemical activity [@problem_id:2013356].

**Electron-Deficient Compounds: Diborane**
Some molecules lack sufficient valence electrons to form traditional two-center, two-electron (2c-2e) bonds between all atoms. Diborane, $\mathrm{B_2H_6}$, is the classic example. Its structure features two boron atoms and four terminal hydrogen atoms ($H_t$) in a plane, with two bridging hydrogens ($H_b$) above and below the plane. The B-$H_t$ bonds are standard 2c-2e bonds. The bridging units, however, are explained by **three-center, two-electron (3c-2e) bonds**, where a single pair of electrons binds three atoms (B, $H_b$, and B) in a bent configuration. Geometric analysis of the B-$H_b$-B-$H_b$ rhombus, using experimental bond lengths, reveals the internal angles of this unique ring structure [@problem_id:2013324]. Such molecules represent a class where simple Lewis structures and VSEPR rules must be augmented with more sophisticated bonding models.