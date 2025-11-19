## Introduction
In the landscape of quantum materials, Dirac and Weyl semimetals represent a fascinating state of matter that bridges the gap between conventional metals and insulators. These materials are defined by a unique electronic structure where the conduction and valence bands touch at discrete points in [momentum space](@entry_id:148936), giving rise to low-energy excitations that behave like massless relativistic particles. This discovery has not only challenged our traditional understanding of electronic states but has also unveiled a rich playground for exploring fundamental concepts from topology and high-energy physics within a tangible solid-state system. This article provides a comprehensive introduction to the physics of these [topological semimetals](@entry_id:137800), addressing the need for a unified understanding of their theoretical principles and experimental manifestations.

To achieve this, our exploration is structured into three distinct parts. First, in **Principles and Mechanisms**, we will dissect the fundamental Hamiltonians, the role of crystal symmetries, and the topological invariants that form the theoretical bedrock of Dirac and Weyl physics. Next, the chapter on **Applications and Interdisciplinary Connections** will bridge theory and reality by examining the hallmark experimental signatures, [anomalous transport](@entry_id:746472) phenomena, and the surprising connections these materials forge with fields like cosmology and quantum information. Finally, **Hands-On Practices** will offer a set of guided problems, allowing you to apply these concepts and solidify your understanding by calculating key properties such as the [density of states](@entry_id:147894) and Landau levels.

## Principles and Mechanisms

This chapter delves into the fundamental principles that govern the electronic structure and properties of Dirac and Weyl semimetals. We will begin by constructing the low-energy effective Hamiltonians that describe the behavior of quasiparticles near the [nodal points](@entry_id:171339). Subsequently, we will explore the critical role of crystalline symmetries in stabilizing these nodes and facilitating the transition between Dirac and Weyl phases. Finally, we will introduce the [topological invariants](@entry_id:138526) that characterize these materials and give rise to their unique, observable phenomena, such as exotic surface states and anomalous [transport properties](@entry_id:203130).

### Low-Energy Excitations and Band Structure

The defining characteristic of Dirac and Weyl semimetals is the linear touching of their conduction and valence bands at discrete points in the three-dimensional [momentum space](@entry_id:148936), known as nodes. This is in stark contrast to conventional metals, where the Fermi energy typically cuts across a parabolic band, forming a two-dimensional Fermi surface.

#### The Weyl Hamiltonian and Nodal Point Fermions

Near a Weyl point, the low-energy quasiparticles are described by the **Weyl equation**, a [relativistic wave equation](@entry_id:158220) for massless spin-1/2 particles. The simplest effective Hamiltonian that captures this physics is a $2 \times 2$ matrix, reflecting the two-fold degeneracy at the node. For a Weyl point located at $\mathbf{k}=0$, this Hamiltonian takes the form:
$$
H(\mathbf{k}) = \hbar v_F (\mathbf{k} \cdot \boldsymbol{\sigma}) = \hbar v_F (k_x \sigma_x + k_y \sigma_y + k_z \sigma_z)
$$
Here, $\mathbf{k}$ is the crystal momentum measured from the node, $v_F$ is the Fermi velocity, $\hbar$ is the reduced Planck constant, and $\boldsymbol{\sigma} = (\sigma_x, \sigma_y, \sigma_z)$ is the vector of Pauli matrices acting on a [pseudospin](@entry_id:147053) degree of freedom, which could be the electron's true spin or an orbital index.

The [energy eigenvalues](@entry_id:144381) of this Hamiltonian are readily found to be:
$$
E_{\pm}(\mathbf{k}) = \pm \hbar v_F |\mathbf{k}| = \pm \hbar v_F \sqrt{k_x^2 + k_y^2 + k_z^2}
$$
This [linear dispersion relation](@entry_id:266313) describes two cones touching at their apices, a structure often called a **Weyl cone**. At the [charge neutrality](@entry_id:138647) point (CNP), where the Fermi energy $E_F$ is exactly at the nodal energy ($E_F=0$), the Fermi surface shrinks to a single, zero-dimensional point in momentum space [@problem_id:1827861]. This point-like Fermi surface is a fundamental distinction from ordinary metals, whose Fermi surfaces are typically two-dimensional spheres or more complex shapes.

This unique dispersion has a profound impact on the material's electronic properties. For instance, the **[density of states](@entry_id:147894) (DOS)**, $g(E)$, which measures the number of available states per unit energy, vanishes at the node and grows quadratically with energy. For a generally anisotropic Weyl cone, described by $H(\mathbf{k}) = \hbar (v_x k_x \sigma_x + v_y k_y \sigma_y + v_z k_z \sigma_z)$, the DOS can be calculated as [@problem_id:1827865]:
$$
g(E) = \frac{E^2}{2\pi^2 \hbar^3 v_x v_y v_z}
$$
This $E^2$ dependence, a direct consequence of the 3D linear dispersion, is a hallmark of Weyl semimetals and differs significantly from the $\sqrt{E}$ dependence in conventional metals with parabolic bands ($E \propto k^2$).

#### The Dirac Hamiltonian and Four-Fold Degeneracy

A Dirac point represents a higher-order degeneracy. It is a point where four bands touch, comprising two overlapping Kramers-degenerate bands. Conceptually, a Dirac point can be viewed as the superposition of two Weyl points with opposite topological charges, forced to coincide at the same momentum and energy by crystal symmetries [@problem_id:1827867].

The low-energy effective Hamiltonian for a Dirac point is necessarily a $4 \times 4$ matrix. A [minimal model](@entry_id:268530) can be constructed using two sets of Pauli matrices, $\boldsymbol{\sigma}$ and $\boldsymbol{\tau}$, which act on different degrees of freedom (e.g., spin and orbital). A representative Dirac Hamiltonian is:
$$
H_D(\mathbf{k}) = \hbar (v_x k_x \tau_x \otimes \sigma_x + v_y k_y \tau_x \otimes \sigma_y + v_z k_z \tau_x \otimes \sigma_z) + m \tau_z \otimes \mathbb{I}_\sigma
$$
In the gapless limit where the mass term $m=0$, this Hamiltonian describes a four-fold degenerate Dirac point at $\mathbf{k}=0$. Breaking specific symmetries of the crystal can lift this degeneracy, splitting the Dirac point into a pair of distinct Weyl points, a process we will explore in the next section.

It is also important to distinguish these point-like nodes from other types of topological band crossings. In **[nodal-line semimetals](@entry_id:144447)**, for example, the conduction and valence bands are degenerate along a continuous one-dimensional curve or loop within the Brillouin zone, rather than at isolated zero-dimensional points [@problem_id:1827877].

### The Central Role of Symmetry

The existence and stability of Dirac and Weyl nodes are fundamentally dictated by the symmetries of the crystal lattice, most notably **time-reversal symmetry (TRS)** and **spatial [inversion symmetry](@entry_id:269948) (IS)**.

A key principle for spin-1/2 electrons is **Kramers' theorem**, which states that in a system with TRS, all [energy eigenstates](@entry_id:152154) are at least two-fold degenerate. The combined symmetry operator $PT$ (where $P$ is inversion) is an anti-unitary symmetry that acts at a fixed momentum point $\mathbf{k}$. For spinful electrons, $(PT)^2 = -1$. A generalized Kramers' theorem then implies that if a system respects both TRS and IS, every energy band is at least two-fold degenerate at *every* point $\mathbf{k}$ in the Brillouin zone.

This has a critical consequence: a single, isolated Weyl point, which is only two-fold degenerate at the node itself but becomes non-degenerate away from it, cannot exist in a system that preserves both TRS and IS [@problem_id:2870328]. Therefore, to realize a Weyl semimetal, at least one of these two fundamental symmetries must be broken [@problem_id:1827852].

1.  **Inversion-Symmetric Weyl Semimetals (TRS preserved, IS broken):** These materials have crystal structures that lack a center of inversion. In the presence of TRS, a Weyl node at momentum $\mathbf{k}$ implies the existence of another node at $-\mathbf{k}$ with the same chirality. To satisfy the global constraint that the total [topological charge](@entry_id:142322) must be zero (the Nielsen-Ninomiya theorem, discussed later), such materials must host at least four Weyl points.

2.  **Time-Reversal-Symmetric Weyl Semimetals (IS preserved, TRS broken):** These are typically magnetic materials where the intrinsic magnetization breaks TRS. In the presence of IS, a Weyl node at $\mathbf{k}$ implies another node at $-\mathbf{k}$ with the opposite chirality. In this case, a pair of Weyl nodes is sufficient to satisfy the zero-charge constraint, representing the [minimal realization](@entry_id:176932) of a Weyl semimetal.

#### From Dirac to Weyl Semimetals

A Dirac semimetal, which requires both TRS and IS for its protection, serves as a natural parent compound for creating Weyl [semimetals](@entry_id:152277). The four-fold degeneracy of the Dirac point is protected by the combined $PT$ symmetry. By breaking either $P$ or $T$, this protection is lifted, and the Dirac point typically splits into a pair of Weyl points with opposite chirality, whose net charge sums to zero [@problem_id:1827867] [@problem_id:2870328].

For instance, consider a Dirac Hamiltonian where a perturbation breaking TRS is introduced, such as a magnetic field inducing a Zeeman term $H_{pert} = b(\tau_z \otimes \sigma_z)$ [@problem_id:1827837]. This term breaks TRS but preserves IS, splitting the Dirac point into a pair of Weyl points. A specific calculation shows that applying a Zeeman field $H_Z = b \sigma_z$ to a gapped Dirac system with mass $m$ leads to the emergence of two Weyl points separated in [momentum space](@entry_id:148936) as soon as the Zeeman energy overcomes the gap, i.e., $|b| > |m|$ [@problem_id:2870337].

Alternatively, an IS-breaking perturbation can be applied. A term of the form $\delta H = \Delta \tau_y$ breaks [inversion symmetry](@entry_id:269948) and, as shown by calculation, splits the Dirac point into two Weyl points separated along the $k_z$ axis by a momentum vector $\delta \mathbf{K} = (0, 0, 2\Delta/v_z)$ [@problem_id:2870320]. These two pathways—breaking $T$ or breaking $P$—provide distinct mechanisms for generating Weyl [semimetals](@entry_id:152277), with TRS-breaking perturbations often separating the nodes in energy, and IS-breaking perturbations separating them in momentum [@problem_id:2870338].

In addition to TRS and IS, crystalline point-group symmetries, such as rotations, can also play a crucial role. For materials that possess both TRS and IS, Dirac points can be stabilized on high-symmetry rotation axes. Analysis based on group theory reveals that such protection is possible for rotation orders $n=3, 4, 6$, but not for $n=1, 2$, because only the former allow for the existence of multiple, distinct representations for the spin-1/2 Kramers pairs, forbidding hybridization at the crossing point [@problem_id:2870288].

### Topological Invariants and Their Consequences

The most profound aspect of Weyl and Dirac [semimetals](@entry_id:152277) is their non-[trivial topology](@entry_id:154009), which is encoded in the geometry of the electronic wavefunctions in momentum space.

#### Chirality as a Topological Charge

Each Weyl point is not merely a [band crossing](@entry_id:161733) but a topologically stable object carrying an integer charge known as **chirality**, denoted by $\chi = \pm 1$. This charge quantifies the handedness of the Weyl fermions near the node. Mathematically, the [chirality](@entry_id:144105) is a robust topological invariant determined by the local [band structure](@entry_id:139379). For a Hamiltonian of the form $H(\mathbf{k}) = \mathbf{d}(\mathbf{k}) \cdot \boldsymbol{\sigma}$, the map from momentum $\mathbf{k}$ to the vector $\mathbf{d}$ near a node at $\mathbf{k}_0$ is approximately linear: $d_i(\mathbf{k}) \approx \sum_j M_{ij} (k_j - k_{0j})$. The node is a stable Weyl point if the matrix $M$ is invertible ($\det(M) \neq 0$), and its [chirality](@entry_id:144105) is given by the sign of this determinant:
$$
\chi = \mathrm{sgn}(\det(M))
$$
This integer charge cannot be changed by small perturbations, such as the addition of a band tilt, which do not close the bulk band gap [@problem_id:3024257].

Physically, a Weyl point acts as a monopole—a source ($\chi=+1$) or a sink ($\chi=-1$)—of **Berry curvature** $\boldsymbol{\Omega}(\mathbf{k})$ in [momentum space](@entry_id:148936) [@problem_id:1827823]. The Berry curvature is an [effective magnetic field](@entry_id:139861) in k-space that describes the geometric phase acquired by an electron as it moves through the Brillouin zone. The chirality is precisely the total flux of this Berry curvature through a closed surface (like a small sphere) enclosing the Weyl point, quantized in units of $2\pi$. This flux is also known as the first **Chern number** $C$:
$$
C = \frac{1}{2\pi} \oint_S \boldsymbol{\Omega}(\mathbf{k}) \cdot d\mathbf{S} = \chi
$$
A direct calculation for the Weyl Hamiltonian $H(\mathbf{q})=\chi v \boldsymbol{\sigma}\cdot \mathbf{q}$ confirms that the Berry curvature for the lower band is that of a [magnetic monopole](@entry_id:149129), $\boldsymbol{\Omega}_{-}(\mathbf{q}) = \frac{\chi}{2} \frac{\mathbf{q}}{|\mathbf{q}|^3}$, and that the integral of its flux indeed yields $2\pi\chi$ [@problem_id:2870330].

A fundamental principle known as the **Nielsen-Ninomiya theorem** states that within the periodic Brillouin zone of a crystal, the total [topological charge](@entry_id:142322) must be zero. This means that Weyl points must always appear in pairs of opposite chirality. This "no-go" theorem for having a single Weyl node on a lattice can be understood from several perspectives: mathematically, it is a consequence of the Poincaré-Hopf theorem applied to the Brillouin zone, which as a 3-torus has an Euler characteristic of zero; physically, it is required to prevent violations of [charge conservation](@entry_id:151839) that would otherwise arise from the [chiral anomaly](@entry_id:142077) [@problem_id:3024297].

A Dirac point, being a superposition of two Weyl points of opposite chirality, thus carries a net topological charge of zero [@problem_id:2870328]. This is consistent with its stability in systems with TRS and IS, where the total Berry curvature must vanish everywhere.

### Phenomenological Signatures of Weyl Semimetals

The non-[trivial topology](@entry_id:154009) of Weyl semimetals gives rise to a host of extraordinary physical phenomena that are not found in conventional materials and serve as their experimental fingerprints.

#### Type-I and Type-II Weyl Semimetals

The simple linear cone model can be refined by including a tilt term in the Hamiltonian, which arises naturally in real materials:
$$
H(\mathbf{k}) = \hbar \mathbf{w} \cdot \mathbf{k} \, \mathbb{I} + \hbar v (\boldsymbol{\sigma} \cdot \mathbf{k})
$$
The eigenvalues are $E(\mathbf{k}) = \hbar \mathbf{w} \cdot \mathbf{k} \pm \hbar v |\mathbf{k}|$. The classification of Weyl [semimetals](@entry_id:152277) depends on the relative magnitude of the tilt velocity $|\mathbf{w}|$ and the cone velocity $v$ [@problem_id:2870322] [@problem_id:1827843].

-   **Type-I Weyl Semimetal:** Occurs when the tilt is small, $|w|  v$. The Weyl cone remains upright. At the nodal energy, the Fermi surface is a single point.
-   **Type-II Weyl Semimetal:** Occurs when the cone is overtilted, $|w| > v$. In this regime, the cone is tipped over so severely that at the nodal energy ($E=0$), there are coexisting electron and [hole pockets](@entry_id:269009) that touch. The Fermi surface is no longer a point but an open, hyperbolic surface.

The transition between Type-I and Type-II phases at the critical point $|w|=v$ is a **Lifshitz transition**, characterized by a change in the topology of the Fermi surface. It is important to note that the tilt term, being proportional to the identity matrix, does not affect the eigenstates' [pseudospin](@entry_id:147053) texture and therefore does not alter the [topological chirality](@entry_id:149735) of the Weyl node [@problem_id:2870322].

#### Fermi Arcs and the Bulk-Boundary Correspondence

Perhaps the most celebrated prediction for Weyl semimetals is the existence of exotic surface states known as **Fermi arcs**. These are a direct manifestation of the **[bulk-boundary correspondence](@entry_id:137647)**, a principle linking the [topological properties](@entry_id:154666) of the bulk to the existence of protected states at the boundary.

A 3D Weyl semimetal can be viewed as a stack of 2D insulating momentum-space slices. For slices that lie between two Weyl nodes of opposite chirality, the net enclosed [topological charge](@entry_id:142322) is non-zero, resulting in a non-zero 2D Chern number for that slice [@problem_id:2870287]. According to the [bulk-boundary correspondence](@entry_id:137647) for 2D Chern insulators, each such slice must host [chiral edge states](@entry_id:138111).

When assembled over the entire Brillouin zone, these [edge states](@entry_id:142513) form a continuous band of [surface states](@entry_id:137922). At the Fermi energy, this band creates a contour of states in the surface Brillouin zone that is not a closed loop, as would be expected for conventional [surface states](@entry_id:137922). Instead, it forms an open curve—a Fermi arc—that terminates at the surface projections of the bulk Weyl nodes of opposite chirality [@problem_id:3024294]. The existence of these arcs, which can be directly imaged by techniques like [angle-resolved photoemission spectroscopy](@entry_id:143943) (ARPES), provides smoking-gun evidence for the Weyl semimetal phase. In contrast, since a Dirac point has zero net [topological charge](@entry_id:142322), Dirac semimetals do not host these simple, topologically guaranteed Fermi arcs [@problem_id:2870328].

#### The Chiral Anomaly

Another profound consequence of the chiral nature of Weyl fermions is the **[chiral anomaly](@entry_id:142077)**, a quantum mechanical effect where the charge associated with a single [chirality](@entry_id:144105) is not conserved in the presence of parallel electric ($\mathbf{E}$) and magnetic ($\mathbf{B}$) fields. While the total electric charge remains conserved, there is a net "pumping" of charges between Weyl nodes of opposite [chirality](@entry_id:144105). The rate of change of the number of particles with a given [chirality](@entry_id:144105) $\chi$ is given by:
$$
\frac{dN_\chi}{dt} = \chi \frac{e^2}{4\pi^2\hbar^2} (\mathbf{E} \cdot \mathbf{B}) V
$$
where $V$ is the volume of the sample [@problem_id:1827855]. This anomalous charge transfer gives rise to unique transport signatures, most notably a large [negative magnetoresistance](@entry_id:136874) when the electric and magnetic fields are aligned. This effect provides a powerful experimental tool for identifying Weyl semimetals through transport measurements.