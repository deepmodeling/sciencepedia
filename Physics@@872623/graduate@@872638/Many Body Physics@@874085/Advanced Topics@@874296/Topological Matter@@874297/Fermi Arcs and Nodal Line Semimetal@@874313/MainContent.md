## Introduction
Topological semimetals are a cutting-edge class of quantum matter where the electronic bands touch in a manner that is protected by the fundamental topology of their [band structure](@entry_id:139379). Unlike accidental degeneracies in conventional materials, these protected crossings—either as zero-dimensional points (Weyl nodes) or one-dimensional lines ([nodal lines](@entry_id:169397))—are robust and give rise to a wealth of exotic phenomena not found elsewhere. The central knowledge gap this article addresses is the connection between these abstract topological concepts and their concrete, measurable physical consequences, most notably the emergence of unique [surface states](@entry_id:137922) like Fermi arcs and [drumhead states](@entry_id:145881).

This article provides a comprehensive exploration of these fascinating materials. The journey begins in the "Principles and Mechanisms" chapter, which lays the theoretical groundwork for Weyl and [nodal-line semimetals](@entry_id:144447), explaining the origin of their topological stability and the nature of their [bulk-boundary correspondence](@entry_id:137647). Building on this foundation, the "Applications and Interdisciplinary Connections" chapter surveys the rich experimental signatures in transport, thermodynamics, and optics, and explores connections to fields like [high-energy physics](@entry_id:181260) and [materials engineering](@entry_id:162176). Finally, the "Hands-On Practices" section offers targeted problems that allow you to apply these concepts to concrete physical scenarios, solidifying your understanding of this vibrant field.

## Principles and Mechanisms

Topological semimetals represent a fascinating class of [quantum matter](@entry_id:162104) where the conduction and valence bands touch at discrete points or along continuous lines within the Brillouin zone. Unlike in conventional semimetals, where such band touchings are often accidental and can be removed by small perturbations, the degeneracies in [topological semimetals](@entry_id:137800) are robust, protected by the underlying topology of the electronic band structure, often in conjunction with crystalline symmetries. These protected degeneracies, known as nodes, act as sources and sinks of Berry curvature in [momentum space](@entry_id:148936), giving rise to a host of exotic physical phenomena, most notably the appearance of unique [surface states](@entry_id:137922) that have no counterpart in ordinary materials. This chapter explores the fundamental principles governing the two primary classes of [topological semimetals](@entry_id:137800): Weyl [semimetals](@entry_id:152277), which host point-like nodes, and [nodal-line semimetals](@entry_id:144447), which feature line-like degeneracies.

### Topological Stability of Band Crossings

The defining characteristic of a topological [band crossing](@entry_id:161733) is its stability against perturbations that preserve the protecting symmetries, if any. To appreciate this stability, it is instructive to compare a topologically protected node with an accidental, unprotected one. Consider a generic two-band system described by a Bloch Hamiltonian near a band-touching point $\mathbf{k}_0$. By expanding in terms of the momentum deviation $\mathbf{q} = \mathbf{k} - \mathbf{k}_0$, the Hamiltonian can be written as $H(\mathbf{q}) = \mathbf{d}(\mathbf{q}) \cdot \boldsymbol{\sigma}$, where $\boldsymbol{\sigma}$ is the vector of Pauli matrices representing a [pseudospin](@entry_id:147053) degree of freedom. The bands are degenerate where $\mathbf{d}(\mathbf{q}) = \mathbf{0}$.

A **Weyl node** is a [band crossing](@entry_id:161733) where the vector function $\mathbf{d}(\mathbf{q})$ is linear in all three momentum directions. A [minimal model](@entry_id:268530) is:
$$
H_{\mathrm{W}}(\mathbf{q}) = v_x q_x \sigma_x + v_y q_y \sigma_y + v_z q_z \sigma_z
$$
Here, the degeneracy condition $\mathbf{d}(\mathbf{q})=\mathbf{0}$ corresponds to three independent [linear equations](@entry_id:151487) ($q_x=0, q_y=0, q_z=0$) in three variables, which has a stable, isolated solution at $\mathbf{q}=\mathbf{0}$.

In contrast, consider an **accidental band touching** where the dispersion is not linear in all directions, for instance:
$$
H_{\mathrm{acc}}(\mathbf{q}) = v_x q_x \sigma_x + v_y q_y \sigma_y + \mathcal{O}(|\mathbf{q}|^2)
$$
Here, the degeneracy condition $\mathbf{d}(\mathbf{q})=\mathbf{0}$ provides only two [linear constraints](@entry_id:636966) on the three components of $\mathbf{q}$. This is insufficient to pin the degeneracy to an [isolated point](@entry_id:146695); its existence is fragile and relies on fine-tuning. A generic, small perturbation, such as adding a constant term $\delta H = m \sigma_z$, will lift the degeneracy and open a full energy gap throughout the Brillouin zone.

The stability of the Weyl node is rooted in topology. The node acts as a monopole of **Berry curvature** in momentum space. The integral of the Berry curvature of a band over a closed surface $S$ enclosing the node yields a quantized, integer value known as the **first Chern number**, $C$. This integer, called the **[chirality](@entry_id:144105)** of the node, cannot change under small, continuous deformations of the Hamiltonian. A non-zero chirality ($\chi = C \neq 0$) thus acts as a [topological invariant](@entry_id:142028) that protects the node from being gapped. For the accidental touching, the corresponding Chern number is zero, signifying no [topological protection](@entry_id:145388) [@problem_id:3024309].

### Weyl Semimetals

Weyl semimetals are the realization of this topologically stable band touching. Their low-energy excitations behave like massless Weyl fermions, which were originally proposed in [high-energy physics](@entry_id:181260) but have yet to be observed as fundamental particles. In condensed matter, they emerge as collective [electronic excitations](@entry_id:190531).

#### The Weyl Hamiltonian and Chirality

The minimal Hamiltonian for a Weyl node is a linear mapping from momentum space $\mathbf{k}$ to the space of Hamiltonian parameters $\mathbf{d}$. Near a node at $\mathbf{k}_0$, this can be expressed as $d_i(\mathbf{k}) \approx \sum_{j} M_{ij} (k_j - k_{0j})$, where the matrix $M$ is the Jacobian $M_{ij} = \partial d_i / \partial k_j$ evaluated at $\mathbf{k}_0$. A point node exists if this [system of linear equations](@entry_id:140416) has an isolated solution, which requires the matrix $M$ to be invertible, i.e., $\det(M) \neq 0$.

The topological charge, or **chirality** $\chi$, of this Weyl node is given by the sign of the determinant of this Jacobian matrix:
$$
\chi = \mathrm{sgn}(\det(M))
$$
This integer charge, which can be $\chi = +1$ or $\chi = -1$, quantifies the winding of the normalized vector field $\hat{\mathbf{d}}(\mathbf{k}) = \mathbf{d}(\mathbf{k})/|\mathbf{d}(\mathbf{k})|$ around the node. It is precisely the Chern number calculated on a small sphere enclosing the node. For example, for a Hamiltonian with a linearized component matrix $M$ with $\det(M)=-4$, the node is a Weyl node with [chirality](@entry_id:144105) $\chi = -1$ [@problem_id:3024257]. A term proportional to the identity matrix, such as a "tilt" term $t_\ell(\mathbf{k})\mathbb{I}$, shifts the energy of the entire cone but does not affect the eigenvectors or the [band topology](@entry_id:182035), leaving the [chirality](@entry_id:144105) unchanged.

Explicitly, the Chern number $C$ for a given band over a closed surface $S$ in [momentum space](@entry_id:148936) is defined as the integral of the Berry curvature $\mathbf{F}(\mathbf{k})$:
$$
C = \frac{1}{2\pi} \oint_S \mathbf{F}(\mathbf{k}) \cdot d\mathbf{S}
$$
For a Weyl node, this integral over an enclosing sphere yields its integer chirality, $\chi$. This confirms that a Weyl node is a source ($\chi=+1$) or sink ($\chi=-1$) of Berry flux, analogous to a [magnetic monopole](@entry_id:149129) in [momentum space](@entry_id:148936) [@problem_id:1135130].

#### Nielsen-Ninomiya Theorem and Symmetry

A profound constraint on any lattice system, known as the **Nielsen-Ninomiya theorem**, dictates that Weyl nodes must come in pairs. Specifically, the sum of the chiralities of all Weyl nodes over the entire Brillouin zone must be zero:
$$
\sum_{i} \chi_i = 0
$$
This "no-go" theorem implies that it is impossible to have a single Weyl node in a crystal. The minimum number of nodes is two: one with $\chi=+1$ and one with $\chi=-1$.

The number and arrangement of Weyl nodes are further constrained by the crystal's symmetries.
- **Time-Reversal Symmetry (TRS):** For a spin-1/2 system, TRS maps a state at momentum $\mathbf{k}$ to one at $-\mathbf{k}$. It dictates that if a Weyl node of chirality $\chi$ exists at $\mathbf{k}$, another node of the *same* [chirality](@entry_id:144105) $\chi$ must exist at $-\mathbf{k}$. To satisfy the zero-sum rule, there must be at least one other such pair with the opposite chirality. Consequently, the minimum number of Weyl nodes in a system that preserves TRS but breaks [inversion symmetry](@entry_id:269948) is four [@problem_id:1135081].
- **Inversion Symmetry (P):** Inversion symmetry maps $\mathbf{k}$ to $-\mathbf{k}$ but flips the [chirality](@entry_id:144105): if a node of [chirality](@entry_id:144105) $\chi$ exists at $\mathbf{k}$, a node of [chirality](@entry_id:144105) $-\chi$ must exist at $-\mathbf{k}$. A system with only two Weyl nodes must break TRS but can preserve [inversion symmetry](@entry_id:269948).
- **Crystal Symmetries:** Additional crystal symmetries, such as rotations, can enforce a larger number of nodes. For instance, in a system with the full cubic symmetry of a body-centered cubic (BCC) lattice, a single pair of Weyl nodes is forbidden. Any node at a generic momentum point would be replicated by the rotational symmetries, leading to a larger multiplet of nodes [@problem_id:1135099].

#### Bulk-Boundary Correspondence and Fermi Arcs

The most striking consequence of the non-trivial bulk topology of Weyl [semimetals](@entry_id:152277) is the emergence of protected surface states known as **Fermi arcs**. The connection between the bulk topological charge and the surface phenomena is an example of the **bulk-boundary correspondence**.

One way to understand the origin of Fermi arcs is to conceptually slice the 3D Brillouin zone into a stack of 2D planes, parameterized by a momentum component, say $k_z$. For a pair of Weyl nodes at $\mathbf{k}_{\pm}$ with chiralities $\pm 1$, a 2D slice of the BZ taken at a $k_z$ value lying *between* the $k_z$ coordinates of the two nodes will intersect a net Berry flux. This 2D subsystem behaves as a Chern insulator with a non-zero Chern number ($C=\pm 1$). A fundamental result of 2D [topological insulators](@entry_id:137834) is that they must host [chiral edge states](@entry_id:138111).

As we vary $k_z$, each "insulating" slice between the Weyl nodes contributes a chiral state at the boundary. The collection of these states, as a function of the in-plane momenta $(k_x, k_y)$, forms a continuous band of [surface states](@entry_id:137922). The constant-energy contour of this band at the Fermi level forms an open curve in the surface Brillouin zone. This curve is the **Fermi arc**. It terminates at the surface projections of the two bulk Weyl nodes, as these are the points where the bulk gap closes and the surface state merges into the bulk continuum [@problem_id:3024294]. Thus, Fermi arcs are topologically mandated to connect the projections of bulk Weyl nodes of opposite chirality.

The equation for a Fermi arc can be derived by solving the Schrödinger equation in a semi-infinite geometry with appropriate boundary conditions. This typically involves finding zero-energy solutions that are localized at the surface and decay into the bulk. For a Weyl semimetal with nodes on the $k_z$-axis, a surface at $z=0$ can host a linear Fermi arc described by a simple equation such as $k_x=0$ in the $(k_x, k_y)$ surface Brillouin zone [@problem_id:1135078]. Furthermore, these surface states exhibit a property called **[spin-momentum locking](@entry_id:139865)**, where the spin (or [pseudospin](@entry_id:147053)) [polarization vector](@entry_id:269389) is locked to the electron's momentum. The spin polarization vector of the surface state winds by an integer multiple of $2\pi$ along a closed loop encircling a Weyl node projection, with the winding number related to the node's chirality [@problem_id:1135059].

### Nodal-Line Semimetals

In [nodal-line semimetals](@entry_id:144447), the conduction and valence bands touch not at isolated points, but along one-dimensional lines or loops in the Brillouin zone. Such a degeneracy requires two conditions to be satisfied simultaneously in the three-dimensional Brillouin zone (e.g., in a two-band model $H = d_x\sigma_x + d_y\sigma_y + d_z\sigma_z$, the nodal line is defined by $d_x(\mathbf{k})=0$ and $d_y(\mathbf{k})=0$).

#### Protection and Generation of Nodal Lines

Nodal lines are typically not stable in the absence of symmetry. However, certain crystalline symmetries, such as the combined time-reversal and [inversion symmetry](@entry_id:269948) ($\mathcal{PT}$ symmetry) or non-symmorphic symmetries like glide reflections, can enforce the necessary conditions and protect the nodal line from being gapped [@problem_id:1135076], [@problem_id:1135063].

A nodal ring can serve as a parent state for Weyl semimetals. Breaking the protecting symmetry can gap out the nodal line everywhere except at a [discrete set](@entry_id:146023) of points, which then become Weyl nodes. For example, in a model of a [nodal-line semimetal](@entry_id:193545) with a ring in the $k_z=0$ plane, applying a perturbation of the form $\gamma k_y \sigma_x$ can break a protecting symmetry and leave behind a pair of Weyl nodes located on the $k_x$-axis, with a separation determined by the model parameters [@problem_id:1135058].

#### Topological Signature: The π Berry Phase

The defining [topological invariant](@entry_id:142028) of a nodal line is a quantized **Berry phase**. While the Chern number on a surface enclosing a segment of the line is zero (as the line has no thickness), a non-trivial topological signature is found by considering a closed loop in [momentum space](@entry_id:148936) that *links* with the nodal line, like a link in a chain.

For any such linking loop $\mathcal{C}$, an electron traversing this path in a given band accumulates a Berry phase of $\gamma_{\mathcal{C}} = \pi$ (modulo $2\pi$) [@problem_id:1135131]. This $\pi$ Berry phase is a robust topological invariant. It can be viewed as a $\mathbb{Z}_2$ invariant $\nu = \gamma_{\mathcal{C}}/\pi \pmod 2$, which takes the value $\nu=1$ for any loop linking the nodal line and $\nu=0$ for any loop that does not [@problem_id:1135135]. This is a universal feature, regardless of whether the nodal line is protected by $\mathcal{PT}$ symmetry or glide symmetry [@problem_id:1135076], [@problem_id:1135063]. In stark contrast, a loop that lies in a plane parallel to the nodal line, and thus does not link it, will accumulate a trivial Berry phase of 0, underscoring the critical importance of the linking condition [@problem_id:1135141].

#### Surface States: Drumhead States

Similar to Weyl [semimetals](@entry_id:152277), [nodal-line semimetals](@entry_id:144447) exhibit their own unique form of topologically protected surface states. When a nodal line exists in the bulk, a corresponding surface can host a nearly flat, zero-energy band of [surface states](@entry_id:137922) that fills the two-dimensional region of the surface Brillouin zone bounded by the projection of the bulk nodal line. These are known as **[drumhead states](@entry_id:145881)** because their dispersion resembles the flat surface of a drum, with the projected nodal line acting as the rim.

The existence of these states can be understood through a domain-wall argument. For a surface perpendicular to the $x$-direction, the Hamiltonian for fixed surface momenta $(k_y, k_z)$ can be viewed as a 1D model. A surface state appears if the mass term of this 1D model has a different sign inside the material compared to the vacuum outside. For a [nodal line semimetal](@entry_id:137021) with a ring of radius $R_0 = \sqrt{m_0/t}$ in the $k_y$-$k_z$ plane, the [drumhead states](@entry_id:145881) exist for all surface momenta $(k_y, k_z)$ inside this ring, i.e., for $k_y^2+k_z^2  R_0^2$. The area of this region is therefore $\pi R_0^2 = \pi m_0/t$ [@problem_id:1135079], [@problem_id:1135128]. These surface states are localized at the boundary and decay exponentially into the bulk, with a characteristic [penetration depth](@entry_id:136478) that depends on the material parameters [@problem_id:1135095].

### Advanced and Exotic Nodal Structures

The principles of [nodal points](@entry_id:171339) and lines can be extended to describe more complex and exotic topological structures.

**Nodal Chains and Links:** In certain materials with appropriate symmetries, multiple nodal loops can coexist in the Brillouin zone. These loops can intersect at specific points, forming **nodal chains**, or be intertwined without touching, forming **nodal links**. These structures can be engineered in multi-band models, for instance, by considering a block-diagonal Hamiltonian where each block contributes a nodal loop in a different plane. The intersection points of a nodal chain are found where the degeneracy conditions for both loops are met simultaneously [@problem_id:1135105]. For nodal links, the non-[trivial topology](@entry_id:154009) is characterized by a non-zero [linking number](@entry_id:268210) between the loops, a concept borrowed from knot theory [@problem_id:1135112].

**Non-Hermitian Systems and Exceptional Rings:** The framework of [topological semimetals](@entry_id:137800) has also been extended to non-Hermitian systems, which can effectively describe systems with gain and loss. In this context, the role of Hermitian degeneracies (like Weyl points) is played by **[exceptional points](@entry_id:199525) (EPs)**, which are special degeneracies where both the eigenvalues and the corresponding eigenvectors of the non-Hermitian Hamiltonian coalesce. A remarkable feature is that a point-like Weyl node in a Hermitian system can be deformed into a stable line or ring of [exceptional points](@entry_id:199525)—an **exceptional ring**—upon the introduction of a non-Hermitian term. For instance, adding a term $i\gamma\sigma_z$ to a Weyl Hamiltonian can transform the Weyl point at $\mathbf{k}=\mathbf{0}$ into an exceptional ring in the $k_z=0$ plane defined by $k_x^2 + k_y^2 = (\gamma/v_F)^2$ [@problem_id:1135083]. These non-Hermitian topological structures lead to their own unique bulk-boundary correspondence and novel surface state phenomena.