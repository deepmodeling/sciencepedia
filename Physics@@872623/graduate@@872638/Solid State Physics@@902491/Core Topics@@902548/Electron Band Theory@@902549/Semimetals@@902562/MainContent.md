## Introduction
Semimetals represent a unique phase of [quantum matter](@entry_id:162104), positioned fascinatingly between metals and insulators. Unlike conventional materials, their electronic structure is defined by valence and conduction bands that touch at discrete points or along lines, leading to exotic [quasiparticle excitations](@entry_id:138475) that mimic fundamental particles from high-energy physics. The significance of semimetals lies in their rich [topological properties](@entry_id:154666), which give rise to a wealth of novel physical phenomena not found in ordinary materials. However, a gap often exists between the abstract theoretical models describing these materials and a concrete understanding of their measurable consequences and broader scientific impact. This article aims to bridge that gap. We will begin in the 'Principles and Mechanisms' chapter by establishing the theoretical foundations of Weyl, Dirac, and [nodal-line semimetals](@entry_id:144447), exploring the roles of symmetry and topology. Following this, the 'Applications and Interdisciplinary Connections' chapter will showcase how these principles translate into tangible experimental signatures and create profound links to fields like quantum computing and cosmology. Finally, the 'Hands-On Practices' section will provide opportunities to apply these concepts through guided problems, solidifying the connection between theory and practice.

## Principles and Mechanisms

The defining characteristic of a semimetal is the touching of its valence and conduction bands at discrete points or along lines in the [momentum space](@entry_id:148936), known as the Brillouin zone (BZ). Unlike metals, which possess a continuous Fermi surface and a large [density of states](@entry_id:147894) at the Fermi level, ideal semimetals have a vanishing density of states at the band-touching energy. Unlike semiconductors or insulators, they have no energy gap. The nature of these band-touching points—their dimensionality, stability, and underlying topological properties—gives rise to a rich classification of semimetals, including Weyl, Dirac, and [nodal-line semimetals](@entry_id:144447). This chapter will elucidate the fundamental principles governing these phases of matter.

### Weyl Semimetals: Chiral Fermions in Crystals

The simplest and most fundamental type of [topological semimetal](@entry_id:158907) is the Weyl semimetal. Its low-energy excitations behave as Weyl fermions, which are chiral, massless particles that have long been sought in particle physics but have so far only been observed as quasiparticles in crystalline solids.

#### The Weyl Hamiltonian and Chiral Quasiparticles

Near an isolated band-touching point between two non-degenerate bands, the low-energy physics can be described by a generic $2 \times 2$ effective Hamiltonian. Any such Hamiltonian can be expanded on the basis of the identity matrix $\mathbb{1}_2$ and the three Pauli matrices $\boldsymbol{\sigma} = (\sigma_x, \sigma_y, \sigma_z)$:

$H(\mathbf{k}) = d_0(\mathbf{k})\mathbb{1}_2 + \mathbf{d}(\mathbf{k}) \cdot \boldsymbol{\sigma}$

Here, $\mathbf{k}$ is the crystal momentum, and $d_0(\mathbf{k})$ and the components of $\mathbf{d}(\mathbf{k})$ are real functions of $\mathbf{k}$. The [energy eigenvalues](@entry_id:144381) are $E_{\pm}(\mathbf{k}) = d_0(\mathbf{k}) \pm |\mathbf{d}(\mathbf{k})|$. A band degeneracy occurs when $E_+ = E_-$, which requires $|\mathbf{d}(\mathbf{k})| = 0$. This is equivalent to simultaneously satisfying three independent equations: $d_x(\mathbf{k}) = 0$, $d_y(\mathbf{k}) = 0$, and $d_z(\mathbf{k}) = 0$. In a three-dimensional Brillouin zone, solving three equations for three variables $(k_x, k_y, k_z)$ generically yields solutions at isolated points. These points are the band-touching nodes. [@problem_id:3007282]

For the simplest case of a linear crossing, the functions $d_i(\mathbf{k})$ are linear in the momentum deviation $\mathbf{q}$ from the node. This leads to the canonical **Weyl Hamiltonian**:

$H(\mathbf{q}) = \hbar \sum_{i,j} v_{ij} q_i \sigma_j$

where $v_{ij}$ are the components of a velocity tensor. For an isotropic system, this simplifies to $H(\mathbf{q}) = \hbar v \mathbf{q} \cdot \boldsymbol{\sigma}$. The energy spectrum of this Hamiltonian is $E_{\pm}(\mathbf{q}) = \pm \hbar v |\mathbf{q}|$, describing two cones that touch at their apex, $\mathbf{q}=0$. This conical dispersion is the hallmark of a **Weyl cone**, and the band touching point is a **Weyl point** or **Weyl node**. The quasiparticles described by this Hamiltonian are effectively massless and exhibit a linear energy-momentum relationship. [@problem_id:1827865]

#### Symmetry, Chirality, and Topological Charge

The existence of Weyl nodes is deeply intertwined with crystal symmetries. In a system that possesses both **[time-reversal symmetry](@entry_id:138094) (T)** and **[inversion symmetry](@entry_id:269948) (P)**, every energy band is at least two-fold degenerate at every point $\mathbf{k}$ in the Brillouin zone. This is a consequence of the fact that the combined operator $PT$ is anti-unitary and, for spinful electrons, $(PT)^2 = -1$. This universal degeneracy forbids the existence of two-fold Weyl nodes, as the bands away from a Weyl node are non-degenerate. Therefore, to realize a Weyl semimetal phase, a crystal must break either [time-reversal symmetry](@entry_id:138094) or inversion symmetry. [@problem_id:1827852] [@problem_id:2870328]

Each Weyl node carries an integer [topological charge](@entry_id:142322) known as **chirality**, denoted by $\chi = \pm 1$. This charge is a robust, quantized property that makes the Weyl node topologically stable against small perturbations that preserve the bulk gaplessness. The chirality signifies that the Weyl node acts as a monopole—a source ($\chi=+1$) or a sink ($\chi=-1$)—of **Berry curvature** in [momentum space](@entry_id:148936). [@problem_id:1827823] The Berry curvature, $\boldsymbol{\Omega}(\mathbf{k})$, is a geometric property of the Bloch wavefunctions that acts like a magnetic field in momentum space, influencing the [semiclassical dynamics](@entry_id:140913) of electrons.

Formally, the [chirality](@entry_id:144105) of a Weyl node is defined as the integer Chern number calculated by integrating the Berry curvature flux over any closed 2D surface $S$ enclosing the node in momentum space:

$\chi = \frac{1}{2\pi} \oint_S \boldsymbol{\Omega}(\mathbf{k}) \cdot d\mathbf{S}$

For example, for a simple isotropic Weyl Hamiltonian $H(\mathbf{q}) = \chi \hbar v \mathbf{q} \cdot \boldsymbol{\sigma}$, the Berry curvature of the lower (valence) band can be calculated to be $\boldsymbol{\Omega}_{-}(\mathbf{q}) = -\chi \frac{\mathbf{q}}{2|\mathbf{q}|^3}$ (assuming $v=1$). The integral of this field over a sphere surrounding the origin indeed yields $-2\pi\chi$, which corresponds to a Chern number of $-\chi$ for the [valence band](@entry_id:158227). [@problem_id:2870315]

The velocity tensor $v_{ij}$ can be anisotropic, which distorts the Weyl cone. This anisotropy modifies the local distribution of Berry curvature on a constant-energy surface. The curvature tends to be concentrated in the "slow" directions of [momentum space](@entry_id:148936), where the band separation is smallest. However, the total integrated flux—the [topological charge](@entry_id:142322)—remains quantized and is independent of such material-specific details, highlighting its topological nature. [@problem_id:2870315]

### The Nielsen-Ninomiya "No-Go" Theorem

A profound constraint on the realization of Weyl fermions in crystals is the **Nielsen-Ninomiya theorem**, often called the [fermion doubling](@entry_id:144782) theorem. It states that for any local, Hermitian, and translationally invariant [tight-binding model](@entry_id:143446) on a lattice, the net chirality of all Weyl nodes within the entire Brillouin zone must be zero. [@problem_id:2870291]

$\sum_{i \in \text{BZ}} \chi_i = 0$

This theorem can be understood through an elegant topological argument. Due to lattice [periodicity](@entry_id:152486), the Brillouin zone has the [topology of a torus](@entry_id:271267), which is a [compact manifold](@entry_id:158804) without a boundary. The Weyl nodes are the [sources and sinks](@entry_id:263105) of the Berry curvature field $\boldsymbol{\Omega}(\mathbf{k})$. Applying the [divergence theorem](@entry_id:145271) to this field over the entire BZ, we find:

$\int_{\text{BZ}} (\nabla_{\mathbf{k}} \cdot \boldsymbol{\Omega}) \, d^3k = \oint_{\partial \text{BZ}} \boldsymbol{\Omega} \cdot d\mathbf{S}$

Since the BZ has no boundary ($\partial \text{BZ} = \emptyset$), the surface integral on the right-hand side is identically zero. The volume integral on the left-hand side is the sum of all monopole charges (chiralities) contained within the BZ. Therefore, the total charge must sum to zero. [@problem_id:2870291]

The immediate consequence of this theorem is that Weyl nodes must always appear in pairs (or larger even multiples) with opposite [chirality](@entry_id:144105). A single Weyl node cannot exist in isolation in a periodic crystal. The simplest possible Weyl semimetal must host at least two Weyl nodes: one source and one sink of Berry curvature. The theorem's assumptions are critical; its conclusions can be evaded by, for example, breaking [translational invariance](@entry_id:195885), a scenario realized on the surface of a material. [@problem_id:2870291]

### Dirac Semimetals: A Symphony of Symmetries

When a material preserves both time-reversal ($T$) and inversion ($P$) symmetries, Weyl nodes are forbidden. However, a different kind of stable band-touching point can emerge: a **Dirac point**. A Dirac point is a four-fold degenerate node where four bands cross. Materials hosting such points are called **Dirac semimetals**. [@problem_id:1827852]

A Dirac point can be fundamentally understood as a composite object: it is a superposition of two Weyl points with opposite [chirality](@entry_id:144105) ($\chi=+1$ and $\chi=-1$) that are degenerate in both energy and momentum. The presence of both $T$ and $P$ symmetries forces this degeneracy, preventing the two constituent Weyl nodes from separating. [@problem_id:2870328]

This composite nature means that the net topological charge of a Dirac point is zero. The Berry curvature flux emanating from the source monopole is precisely cancelled by the flux entering the sink monopole, as they are located at the same point. The total Chern number on a surface enclosing a Dirac point is therefore always zero ($C = (+1) + (-1) = 0$). [@problem_id:2870328]

The intimate relationship between Dirac and Weyl semimetals becomes clear when considering symmetry breaking. If one starts with a Dirac semimetal and breaks either inversion symmetry (e.g., by applying a strain or growing a [non-centrosymmetric crystal](@entry_id:158606)) or [time-reversal symmetry](@entry_id:138094) (e.g., by magnetic doping or applying a magnetic field), the protection for the four-fold degeneracy is lifted. The two constituent Weyl nodes are no longer required to be at the same point and can separate in [momentum space](@entry_id:148936). This process constitutes a [topological phase transition](@entry_id:137214) from a Dirac semimetal to a Weyl semimetal. [@problem_id:1827852] [@problem_id:2870328]

### Beyond Point Nodes: Nodal-Line Semimetals

The concept of **[codimension](@entry_id:273141)** provides a systematic way to classify the dimensionality of band degeneracies. The codimension is the number of independent conditions that must be satisfied for a degeneracy to occur. In a $D$-dimensional BZ, the dimension of the degeneracy manifold is $d = D - C$, where $C$ is the [codimension](@entry_id:273141). [@problem_id:3007282]

As we have seen, for a generic two-band model in 3D, a degeneracy requires satisfying three equations ($d_x=d_y=d_z=0$). This corresponds to a [codimension](@entry_id:273141) $C=3$, and the resulting degeneracy is a point ($d = 3-3=0$). This is the case for Weyl and Dirac points.

To realize a one-dimensional degeneracy—a **nodal line** or **nodal loop**—the [codimension](@entry_id:273141) must be reduced to $C=2$. This requires an additional crystalline symmetry that constrains the Hamiltonian such that one of the three conditions for degeneracy is automatically satisfied over a plane or a line in the BZ. [@problem_id:3007282]

A prime example is **[mirror symmetry](@entry_id:158730)**. Consider a mirror plane in the crystal, for instance, the $k_z=0$ plane in the BZ. Bloch states on this plane can be classified by their mirror eigenvalue. If two bands that cross have opposite mirror eigenvalues, they are forbidden by symmetry from hybridizing with each other anywhere on this plane. This forces one component of the $\mathbf{d}(\mathbf{k})$ vector to be identically zero on the entire $k_z=0$ plane. The degeneracy condition is then reduced to two equations to be solved in the two variables $(k_x, k_y)$, which generically defines a 1D curve. This curve is the nodal line, which is protected by the mirror symmetry and is confined to the mirror-invariant plane. [@problem_id:3007282]

### Observable Signatures and Further Classification

Topological semimetals exhibit a range of unique physical properties that serve as experimental signatures and allow for further classification.

#### Density of States

A key thermodynamic property that can distinguish semimetals from conventional metals is the electronic **density of states (DOS)**, $g(E)$. For a single Weyl node with a linear, anisotropic dispersion $E(\mathbf{q}) = \pm \sqrt{(\hbar v_x q_x)^2 + (\hbar v_y q_y)^2 + (\hbar v_z q_z)^2}$, the total DOS (including both bands and spin) can be calculated. The result is:

$g(E) = \frac{|E|^2}{2\pi^2\hbar^3 v_x v_y v_z}$

The crucial feature is the quadratic dependence on energy, $g(E) \propto E^2$. This implies that the DOS vanishes at the energy of the Weyl node ($E=0$), a stark contrast to conventional metals which have a large, finite DOS at the Fermi level. This quadratic energy dependence is a key signature that can be probed by [scanning tunneling microscopy](@entry_id:145374) and other spectroscopic techniques. [@problem_id:1827865] [@problem_id:206926]

#### Fermi Arcs and the Bulk-Boundary Correspondence

Perhaps the most celebrated hallmark of a Weyl semimetal is the existence of exotic surface states known as **Fermi arcs**. Their existence is a direct consequence of the non-trivial bulk topology, an example of the **bulk-boundary correspondence**.

This can be understood by viewing the 3D Weyl semimetal as a continuous stack of 2D systems, parameterized by the momentum component parallel to the surface normal. Let's consider a surface normal to $\hat{\mathbf{x}}$ and two Weyl nodes separated along the $k_z$ axis at $k_z=\pm k_0$ with chiralities $\mp 1$. The momentum $k_z$ is a [good quantum number](@entry_id:263156) for the surface. Each fixed-$k_z$ slice of the 3D BZ can be treated as a 2D gapped system (an insulator), except for the slices at $k_z = \pm k_0$. Each of these 2D insulating slices can be characterized by a 2D Chern number, $C(k_z)$. [@problem_id:2870287]

The value of $C(k_z)$ changes only when the $k_z$-slice crosses a Weyl node, at which point it jumps by the [chirality](@entry_id:144105) of that node. For the simple case described, $C(k_z)$ will be non-zero (e.g., $C(k_z)=1$) for the entire range of momenta between the nodes ($-k_0  k_z  +k_0$) and zero outside this range. [@problem_id:2870287]

According to the [bulk-boundary correspondence](@entry_id:137647) for 2D [topological insulators](@entry_id:137834), a non-zero Chern number $C$ guarantees the existence of $|C|$ [chiral edge states](@entry_id:138111). Applying this principle to our stack, every 2D slice with $k_z$ between $-k_0$ and $+k_0$ must host a chiral state on the surface. The collection of these states forms a continuous band of [surface states](@entry_id:137922) that exists only within this specific momentum range. The Fermi level will intersect this band, creating a contour in the surface Brillouin zone that is not a closed loop. This open contour is the Fermi arc, which terminates at the surface projections of the bulk Weyl nodes, effectively connecting a source of Berry curvature to a sink. [@problem_id:2870287] This exotic Fermi surface is unique to [topological semimetals](@entry_id:137800) and is directly observable in [angle-resolved photoemission spectroscopy](@entry_id:143943) (ARPES). In contrast, Dirac semimetals, with their trivial net topological charge, do not have this guaranteed protection for Fermi arcs. [@problem_id:2870328]

#### Type-I and Type-II Weyl Semimetals

The idealized Weyl cone can be tilted in realistic materials. This is captured by adding a tilt term to the Hamiltonian:

$H(\mathbf{k}) = \hbar \mathbf{w} \cdot \mathbf{k} \, \mathbb{1}_{2\times 2} + \hbar v \boldsymbol{\sigma} \cdot \mathbf{k}$

where $\mathbf{w}$ is a tilt vector. The [energy spectrum](@entry_id:181780) becomes $E_{\pm}(\mathbf{k}) = \hbar \mathbf{w} \cdot \mathbf{k} \pm \hbar v |\mathbf{k}|$. The magnitude of the tilt relative to the cone velocity leads to a crucial classification: [@problem_id:2870322]

*   **Type-I Weyl Semimetal:** When the tilt is small ($|\mathbf{w}|  v$), the dispersion remains cone-like. At the energy of the Weyl node ($\mu=0$), the Fermi surface is a single point. The DOS vanishes at the node.

*   **Type-II Weyl Semimetal:** When the cone is "overtilted" ($|\mathbf{w}| > v$), the situation changes dramatically. At the nodal energy $\mu=0$, the conduction and valence bands both cross this energy level, creating coexisting electron and [hole pockets](@entry_id:269009) that touch at the Weyl node. The Fermi surface is no longer a point but an open, finite-area surface. This results in a finite DOS at the nodal energy, a property more akin to a conventional metal.

The transition between Type-I and Type-II phases at the critical tilt $|\mathbf{w}| = v$ is a topological transition in the Fermi surface geometry known as a **Lifshitz transition**. Importantly, the topological charge (chirality) of the Weyl node is a robust property of the band-touching itself and is unaffected by the tilt. [@problem_id:2870322]