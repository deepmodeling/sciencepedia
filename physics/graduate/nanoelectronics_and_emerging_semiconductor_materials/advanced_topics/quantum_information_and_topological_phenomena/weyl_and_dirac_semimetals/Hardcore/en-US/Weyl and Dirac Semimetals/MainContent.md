## Introduction
In the landscape of modern condensed matter physics, the discovery of topological materials has ignited a revolution, revealing quantum states of matter with properties fundamentally protected by topology. Among the most fascinating of these are Weyl and Dirac semimetals, which bridge the gap between insulators and metals with an exotic electronic structure that hosts relativistic quasiparticles analogous to fundamental particles in high-energy physics. Understanding these materials is not just an academic pursuit; it is key to unlocking a new generation of electronic and spintronic devices with unprecedented functionalities. This article provides a comprehensive exploration of these topological semimetals, addressing the core principles that define them, the experimental phenomena they exhibit, and the practical skills needed to study them.

The journey begins in the **Principles and Mechanisms** chapter, where we will deconstruct the very essence of a Weyl semimetal, starting with the Weyl node as a topological monopole in momentum space and exploring the critical role of crystal symmetries in distinguishing between Weyl and Dirac phases. We will then transition to **Applications and Interdisciplinary Connections**, demonstrating how these abstract principles manifest as measurable signatures like Fermi arcs and the chiral anomaly, and how they connect to diverse fields from high-energy physics to thermoelectricity. Finally, the **Hands-On Practices** section provides guided problems that translate theory into computational practice, allowing you to calculate key properties like the density of states and visualize the enigmatic Fermi arcs.

## Principles and Mechanisms

The exotic phenomena exhibited by Weyl and Dirac semimetals are direct consequences of their unique electronic band structures, which are fundamentally governed by crystalline symmetries and topology. This chapter elucidates the core principles defining these states of matter, from the nature of individual quasiparticle excitations to the macroscopic consequences of their collective topological character.

### The Weyl Node: A Topological Monopole in Momentum Space

The fundamental building block of a Weyl semimetal is the **Weyl point**, or **Weyl node**. This is an isolated point in the three-dimensional momentum space (the Brillouin zone) where two electronic bands cross with a linear dispersion. In the vicinity of such a node, located at momentum $\mathbf{k}_0$, the behavior of electrons can be described by a low-energy effective Hamiltonian. For an isotropic crossing, this takes the form of the celebrated Weyl equation:

$H(\mathbf{q}) = \chi v \boldsymbol{\sigma} \cdot \mathbf{q}$

Here, $\mathbf{q} = \mathbf{k} - \mathbf{k}_0$ is the momentum vector measured relative to the node, $v$ is the Fermi velocity, $\boldsymbol{\sigma} = (\sigma_x, \sigma_y, \sigma_z)$ is the vector of Pauli matrices representing a pseudospin degree of freedom, and $\chi \in \{+1, -1\}$ is an integer quantum number known as the **chirality** of the node [@problem_id:4312379]. The energy eigenvalues are $E(\mathbf{q}) = \pm v |\mathbf{q}|$, forming a symmetric cone structure—a 3D analogue of graphene's Dirac cone.

The chirality is not merely a label but a robust, quantized **topological charge**. Its physical meaning is revealed through the concept of **Berry curvature**, $\mathbf{\Omega}(\mathbf{k})$, which acts as a fictitious magnetic field in momentum space. A Weyl node behaves as a point source (for $\chi=+1$) or a sink (for $\chi=-1$) of this Berry curvature. Mathematically, the Berry curvature emanating from a single Weyl node is analogous to the magnetic field of a magnetic monopole [@problem_id:1827823]. For the conduction band of the Weyl Hamiltonian, the curvature is given by:

$\mathbf{\Omega}_{+}(\mathbf{q}) = \chi \frac{\mathbf{q}}{2|\mathbf{q}|^3}$

The topological charge is confirmed by calculating the total flux of this curvature through any closed 2D surface $S$ enclosing the node in momentum space. This flux integral yields the first **Chern number**, which is quantized and directly proportional to the chirality [@problem_id:4312379]:

$\Phi_B = \int_S \mathbf{\Omega}(\mathbf{k}) \cdot d\mathbf{S} = 2\pi \chi$

This integer charge cannot be removed by small perturbations of the crystal, granting the Weyl node its topological protection. Just as electric charges must be created in neutralizing pairs, so too must these topological charges. This is formalized by the **Nielsen-Ninomiya theorem**, which dictates that for any periodic crystal lattice, the sum of the chiralities of all Weyl nodes within the first Brillouin zone must be zero [@problem_id:1827866]. Consequently, Weyl nodes must always appear in pairs (or multiples thereof) with a total chirality of zero. For instance, a material with two nodes of chirality $+1$ and one of chirality $-1$ is physically impossible, as the net charge would be $+1$, whereas a material with four $+1$ nodes and four $-1$ nodes is perfectly valid [@problem_id:1827866].

### The Role of Symmetry: From Dirac to Weyl Semimetals

The existence of these topological charges is intimately linked to the fundamental symmetries of the crystal, namely **time-reversal symmetry (TRS)**, represented by the operator $\mathcal{T}$, and **inversion symmetry (IS)**, represented by the operator $\mathcal{P}$. The Berry curvature transforms under these symmetries as $\mathcal{T}: \mathbf{\Omega}(\mathbf{k}) \mapsto -\mathbf{\Omega}(-\mathbf{k})$ and $\mathcal{P}: \mathbf{\Omega}(\mathbf{k}) \mapsto \mathbf{\Omega}(-\mathbf{k})$.

If a crystal possesses both TRS and IS, the combined symmetry $\mathcal{P}\mathcal{T}$ forces the Berry curvature to be identically zero everywhere in the Brillouin zone, since $\mathbf{\Omega}(\mathbf{k}) = -\mathbf{\Omega}(\mathbf{k})$. This forbids the existence of Berry curvature monopoles. Therefore, a necessary condition for a material to be a Weyl semimetal is that it must break either time-reversal symmetry or inversion symmetry (or both) [@problem_id:1827852].

What happens in systems where both TRS and IS are preserved? In such cases, a different type of topological semimetal can emerge: the **Dirac semimetal**. In these materials, the band crossings are four-fold degenerate and are known as **Dirac points**. This four-fold degeneracy arises because the combined $\mathcal{P}\mathcal{T}$ symmetry, for spinful electrons, enforces that every energy band is at least two-fold degenerate (Kramers degeneracy) at every point $\mathbf{k}$ in the Brillouin zone. A Dirac point is formed by the crossing of two such doubly-degenerate bands [@problem_id:1827867].

A Dirac point can be elegantly conceptualized as a superposition of two Weyl points with opposite chirality ($\chi=+1$ and $\chi=-1$) located at the exact same point in momentum space [@problem_id:5305979]. This superposition results in a net topological charge of zero, consistent with the constraints of $\mathcal{P}\mathcal{T}$ symmetry. If one of the protecting symmetries is broken, the degeneracy is lifted, and the Dirac point splits into a pair of distinct Weyl points separated in momentum space [@problem_id:1827852].

However, the stability of a Dirac point is more subtle than that of a Weyl point. The presence of TRS and IS alone is *not* sufficient to guarantee that the four-fold degeneracy is robust against all possible perturbations. It is possible to construct a "mass term" in the Hamiltonian that respects both $\mathcal{T}$ and $\mathcal{P}$, which would open a band gap at the Dirac point, annihilating the topological phase [@problem_id:1827868]. True, stable Dirac semimetals require protection by **additional crystalline symmetries**, such as rotation or non-symmorphic glide-plane symmetries. These additional symmetries can forbid the problematic mass terms by ensuring that the two crossing Kramers doublets belong to different irreducible representations of the crystal's point group, thus preventing them from mixing and gapping out [@problem_id:5305979].

### Hallmark Phenomena and Experimental Signatures

The nontrivial bulk topology of Weyl semimetals gives rise to unique and directly observable phenomena that are absent in conventional metals.

#### Fermi Arc Surface States

The most celebrated hallmark of a Weyl semimetal is the existence of exotic electronic states on its surfaces, known as **Fermi arcs**. These are open-ended segments of a Fermi surface that connect the projections of bulk Weyl nodes of opposite chirality onto the surface Brillouin zone. Their origin is a profound manifestation of the **bulk-boundary correspondence**.

This can be understood by considering the 3D Weyl semimetal as a stack of 2D electronic systems, parameterized by a momentum component, say $k_z$ [@problem_id:2870287]. For any value of $k_z$ that does not coincide with the $k_z$-coordinate of a Weyl node, the corresponding 2D $(k_x, k_y)$ slice of the bulk band structure is fully gapped, behaving as a 2D insulator. We can assign a topological invariant, the Chern number $C(k_z)$, to each such gapped slice.

As one varies $k_z$ across the location of a Weyl node, the value of $C(k_z)$ changes by an integer equal to the node's chirality. For a minimal Weyl semimetal with one node of $\chi=+1$ at $k_z=-k_0$ and another of $\chi=-1$ at $k_z=+k_0$, the Chern number $C(k_z)$ will be non-zero (equal to 1) for the entire momentum range between the nodes, i.e., for $|k_z| \lt k_0$, and zero outside this range.

According to the bulk-boundary correspondence, a 2D insulator with a non-zero Chern number $C$ must host $|C|$ chiral states on its edge. In our stacked picture, this means that for every $k_z$ between $-k_0$ and $+k_0$, there must be a topologically protected state localized on the surface of the crystal. These states collectively form a surface band that exists only within this specific momentum window. The contour defined by the intersection of this surface band with the Fermi energy is the Fermi arc. It is an "arc" because it is not a closed loop; it must terminate at the points where the bulk gap closes—the projections of the Weyl nodes [@problem_id:2870287]. The existence of these arcs is a direct and unambiguous signature of the Weyl semimetal phase. It is important to note that the formation of a Fermi arc depends on the surface termination; if Weyl nodes are separated along an axis normal to the surface, their projections coincide, and no topologically mandated arc will form on that surface [@problem_id:2870287].

#### The Chiral Anomaly

Another quintessential feature is the **chiral anomaly**, a phenomenon rooted in quantum field theory that manifests as a striking transport effect in Weyl semimetals. While the total number of electrons is conserved, the number of electrons of a specific chirality is not. In the presence of parallel electric ($\mathbf{E}$) and magnetic ($\mathbf{B}$) fields, there is a net transfer of charge between Weyl nodes of opposite chirality. This process is described by:

$$
\frac{dN_\chi}{dt} = \chi \frac{e^2}{4\pi^2\hbar^2} (\mathbf{E} \cdot \mathbf{B}) V
$$

where $N_\chi$ is the number of particles with chirality $\chi$, and $V$ is the sample volume [@problem_id:1827855]. For right-handed particles ($\chi=+1$), their number increases, while for left-handed ones ($\chi=-1$), their number decreases by the same amount, ensuring total charge conservation. This "pumping" of charges between nodes leads to a large enhancement of conductivity in the direction of the magnetic field, observed experimentally as a strong **negative longitudinal magnetoresistance**.

### Type-I and Type-II Weyl Semimetals

The simple, symmetric conical dispersion $E(\mathbf{q}) = \pm v |\mathbf{q}|$ describes what is known as a **Type-I Weyl semimetal**. In this case, at the energy of the Weyl node, the Fermi surface consists of a single point. However, more complex band structures can lead to a different classification. A **Type-II Weyl semimetal** arises when the cone is so strongly tilted by other terms in the Hamiltonian that it tips over [@problem_id:1827843].

This can be modeled by a Hamiltonian of the form $H(\mathbf{k}) = T k_z \mathbb{I} + V \boldsymbol{\sigma} \cdot \mathbf{k}$, where the $T k_z$ term represents a strong tilt along the $k_z$ direction. The condition for the system to be Type-II is that the tilt velocity $|T|$ exceeds the cone velocity $|V|$. A dramatic consequence of this overtilted dispersion is that the conduction and valence bands are no longer separated in all directions. At the nodal energy ($E=0$), the Fermi surface is no longer a single point. Instead, the tipped-over cone intersects the zero-energy plane, creating finite-sized **electron and hole pockets** that touch at the Weyl node. The shape of this zero-energy Fermi surface is typically a cone or hyperboloid, a stark contrast to the point-like Fermi surface of a Type-I system [@problem_id:1827843]. This modification profoundly affects the material's density of states, transport properties, and optical response.