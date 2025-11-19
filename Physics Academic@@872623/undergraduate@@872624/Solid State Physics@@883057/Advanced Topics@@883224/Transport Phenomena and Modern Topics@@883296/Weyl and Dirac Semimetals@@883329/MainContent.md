## Introduction
The world of materials is often neatly divided into insulators, semiconductors, and metals, defined by the behavior of electrons within their band structure. However, a revolutionary class of materials known as Weyl and Dirac [semimetals](@entry_id:152277) blurs these lines. These topological materials host [electronic excitations](@entry_id:190531) that do not behave like ordinary electrons, but rather as massless relativistic particles described by equations once reserved for high-energy physics. This exotic behavior unlocks a treasure trove of new physical phenomena and potential technological applications.

This article bridges the conceptual gap between the conventional [band theory of solids](@entry_id:144910) and the advanced topological framework required to understand these materials. It demystifies the properties that make Weyl and Dirac [semimetals](@entry_id:152277) one of the most exciting frontiers in modern [condensed matter](@entry_id:747660) physics.

You will embark on a journey through three distinct chapters. We will begin in "Principles and Mechanisms" by exploring the fundamental nature of Weyl and Dirac points, the crucial role of symmetry in their existence, and profound topological concepts like the [bulk-boundary correspondence](@entry_id:137647). Following this, "Applications and Interdisciplinary Connections" will illuminate the experimental signatures, unique physical properties, and the remarkable links these materials forge with fields like cosmology and particle physics. Finally, the "Hands-On Practices" section will provide an opportunity to apply these concepts to concrete problems, solidifying your understanding of this cutting-edge field.

## Principles and Mechanisms

### Fundamental Band Crossings: The Nature of Weyl and Dirac Points

In the landscape of electronic materials, solids are broadly categorized based on their electronic band structure. Insulators and semiconductors possess a finite energy gap between the highest occupied electronic states (the [valence band](@entry_id:158227)) and the lowest unoccupied states (the conduction band). In contrast, metals have partially filled bands, resulting in a finite [density of states](@entry_id:147894) at the **Fermi energy** ($E_F$) and a continuous **Fermi surface**—the boundary in momentum space separating occupied from unoccupied states. Semimetals represent an intermediate case, where the valence and conduction bands touch at discrete points or along lines in momentum space, leading to a vanishing density of states precisely at the touching points.

Weyl and Dirac [semimetals](@entry_id:152277) are distinguished by the nature of these band touching points. Unlike the quadratic band touching found in some conventional semimetals, these [topological materials](@entry_id:142123) feature linear [dispersion relations](@entry_id:140395), reminiscent of relativistic particles. The most fundamental of these is the **Weyl point**, a two-fold degenerate point crossing in the three-dimensional Brillouin zone. In the vicinity of a Weyl point, which we can place at $\mathbf{k}=0$ for simplicity, the low-energy electronic behavior is described by the elegant Weyl Hamiltonian:

$$
H(\mathbf{k}) = \chi \hbar v_F (k_x \sigma_x + k_y \sigma_y + k_z \sigma_z) = \chi \hbar v_F \mathbf{k} \cdot \boldsymbol{\sigma}
$$

Here, $\mathbf{k} = (k_x, k_y, k_z)$ is the electron wavevector relative to the Weyl point, $\hbar$ is the reduced Planck constant, $v_F$ is the material-dependent Fermi velocity, and $\boldsymbol{\sigma} = (\sigma_x, \sigma_y, \sigma_z)$ is the vector of Pauli matrices acting on the electron's spin or a pseudo-spin degree of freedom. The integer $\chi = \pm 1$ is a topological invariant known as the **chirality** of the Weyl point, which we will explore later. The [energy eigenvalues](@entry_id:144381) of this Hamiltonian are:

$$
E(\mathbf{k}) = \pm \hbar v_F |\mathbf{k}|
$$

This linear dispersion forms a conical structure in energy-momentum space, known as a **Weyl cone**. This has a profound consequence for the Fermi surface. For a conventional three-dimensional metal with a parabolic dispersion, $E(\mathbf{k}) \propto |\mathbf{k}|^2$, the Fermi surface defined by $E(\mathbf{k}) = E_F$ is a two-dimensional sphere in momentum space. However, for an ideal Weyl semimetal at its **[charge neutrality](@entry_id:138647) point (CNP)**, where the Fermi energy precisely intersects the Weyl point ($E_F=0$), the Fermi surface condition $E(\mathbf{k})=0$ is only satisfied at the [singular point](@entry_id:171198) $\mathbf{k}=0$. Thus, the Fermi surface shrinks from a 2D surface to a set of 0-dimensional points—the Weyl points themselves [@problem_id:1827861]. This zero-dimensional Fermi surface is the defining characteristic of an ideal Weyl semimetal.

A **Dirac point** is a related but distinct type of crossing. It is a four-fold degenerate point where two doubly degenerate bands touch. Conceptually, a Dirac point can be thought of as a pair of Weyl points with opposite [chirality](@entry_id:144105) ($\chi=+1$ and $\chi=-1$) that are degenerate in both energy and momentum. The stability of this degeneracy, and the conditions under which it can be lifted, are dictated by the [fundamental symmetries](@entry_id:161256) of the crystal.

### The Role of Symmetry: From Dirac to Weyl Semimetals

The existence and stability of Dirac and Weyl points are intimately linked to two [fundamental symmetries](@entry_id:161256) in [solid-state physics](@entry_id:142261): **[time-reversal symmetry](@entry_id:138094) (T)** and **[inversion symmetry](@entry_id:269948) (P)**.

**Time-reversal symmetry** dictates that the laws of physics are invariant under the transformation $t \to -t$. In quantum mechanics, for a spin-1/2 electron, the time-reversal operator $\mathcal{T}$ is anti-unitary and satisfies $\mathcal{T}^2 = -1$. This property leads to **Kramers' theorem**, which guarantees that for any system with time-reversal symmetry, every energy [eigenstate](@entry_id:202009) has a degenerate partner. In a crystal, $\mathcal{T}$ relates the state at momentum $\mathbf{k}$ to a state at $-\mathbf{k}$. Specifically, it enforces that the [energy bands](@entry_id:146576) satisfy $E(\mathbf{k}) = E(-\mathbf{k})$.

**Inversion symmetry** means the crystal structure is invariant under the transformation $\mathbf{r} \to -\mathbf{r}$. The inversion operator $\mathcal{P}$ is unitary and also forces the band structure to be symmetric: $E(\mathbf{k}) = E(-\mathbf{k})$.

When a crystal possesses *both* time-reversal and [inversion symmetry](@entry_id:269948), the combined symmetry operation $\mathcal{P}\mathcal{T}$ has a powerful effect. This operator is anti-unitary and satisfies $(\mathcal{P}\mathcal{T})^2 = \mathcal{P}^2 \mathcal{T}^2 = (1)(-1) = -1$. Crucially, $\mathcal{P}\mathcal{T}$ leaves the momentum vector $\mathbf{k}$ invariant. Applying Kramers' theorem to this combined symmetry, we find that it enforces a two-fold degeneracy for *every* electronic band at *every* point $\mathbf{k}$ in the Brillouin zone. A Dirac point arises when two of these Kramers-degenerate bands cross. If this crossing is further protected by an additional crystal symmetry (like a rotation), the result is a stable, four-fold degenerate Dirac point [@problem_id:1827867].

The transition from a Dirac to a Weyl semimetal is achieved by breaking this protective symmetry shield. If either time-reversal symmetry or inversion symmetry is broken, the combined $\mathcal{P}\mathcal{T}$ symmetry is lost. The constraint that forced a two-fold degeneracy at every $\mathbf{k}$ is lifted. This allows the four-fold degenerate Dirac point to split into a pair of two-fold degenerate Weyl points, which are now separated in [momentum space](@entry_id:148936) and/or energy.
*   **Breaking Inversion (P), Preserving Time-Reversal (T):** The Dirac point splits into a pair of Weyl points. Due to the remaining T-symmetry, a Weyl point at $\mathbf{k}_W$ must be accompanied by another one at $-\mathbf{k}_W$ with the same [chirality](@entry_id:144105). The Nielsen-Ninomiya theorem (discussed below) then requires another such pair with opposite chirality, leading to a minimum of four Weyl points.
*   **Breaking Time-Reversal (T), Preserving Inversion (P):** The Dirac point splits into a pair of Weyl points. The remaining P-symmetry requires that a Weyl point at $\mathbf{k}_W$ with [chirality](@entry_id:144105) $\chi$ is mirrored by a Weyl point at $-\mathbf{k}_W$ with the opposite chirality $-\chi$.

Therefore, a Weyl semimetal phase can be realized from a parent Dirac semimetal by breaking either T or P symmetry [@problem_id:1827852]. This can be achieved, for example, by applying a magnetic field (which breaks T) or by using a crystal structure that lacks a [center of inversion](@entry_id:273028) (which breaks P).

We can see this explicitly with a simplified model Hamiltonian for a Dirac semimetal [@problem_id:1827837]:
$$
H_{D}(\mathbf{k}) = v(k_x \tau_x \otimes \sigma_x + k_y \tau_x \otimes \sigma_y + k_z \tau_x \otimes \sigma_z)
$$
Here, $\sigma_i$ and $\tau_i$ are two sets of Pauli matrices representing spin and orbital degrees of freedom, respectively. This Hamiltonian is protected by both inversion $P = \tau_z \otimes \mathbb{I}_{\sigma}$ and time-reversal $T = (\mathbb{I}_{\tau} \otimes i\sigma_y) K$, where $K$ is [complex conjugation](@entry_id:174690). Adding a perturbation term of the form $H_{pert} = b (\tau_z \otimes \sigma_z)$ breaks time-reversal symmetry (since $T H_{pert} T^{-1} = -H_{pert}$) but preserves inversion symmetry ($P H_{pert} P^{-1} = H_{pert}$). This term acts like a Zeeman field that couples differently to the two pairs of bands, splitting the four-fold Dirac point into two two-fold Weyl points separated in momentum, thereby inducing a Weyl semimetal phase.

### Topological Charge and the Nielsen-Ninomiya Theorem

Weyl points are not merely accidental degeneracies; they are topologically stable objects. Their stability is rooted in the concept of **Berry curvature**, $\mathbf{\Omega}(\mathbf{k})$, which can be thought of as a fictitious magnetic field that lives in momentum space. The Berry curvature describes how the wavefunction of an electron evolves as its momentum is varied.

In this picture, Weyl points act as **monopoles** of the Berry curvature [@problem_id:1827823]. A Weyl point is either a source (monopole) or a sink (anti-monopole) of Berry flux. The topological charge of this monopole is its **chirality**, $\chi$. This is an integer invariant, typically $\pm 1$, given by the total flux of the Berry curvature through any closed surface $S$ enclosing the Weyl point in [momentum space](@entry_id:148936):
$$
\chi = \frac{1}{2\pi} \oint_S \mathbf{\Omega}(\mathbf{k}) \cdot d\mathbf{S}
$$
Because this charge is quantized, a Weyl point cannot be created or destroyed in isolation. An isolated Weyl point cannot be removed by small perturbations to the Hamiltonian without annihilating it with another Weyl point of opposite [chirality](@entry_id:144105).

This topological nature leads to a powerful constraint known as the **Nielsen-Ninomiya theorem**. It states that on any periodic crystal lattice, the sum of the chiralities of all Weyl points within the first Brillouin zone must be zero [@problem_id:1827866].
$$
\sum_{i \in \text{BZ}} \chi_i = 0
$$
This theorem is a direct consequence of the fact that the Brillouin zone is a closed, periodic manifold (a torus). Just as the net magnetic flux out of any closed surface in real space is zero (Gauss's law for magnetism), the net flux of Berry curvature out of the closed Brillouin zone must also be zero. This implies that Weyl points must always come in pairs of opposite chirality. A material cannot have a single Weyl point, nor can it have an unequal number of positive and negative chirality points. For instance, a crystal with three Weyl points—two with $\chi=+1$ and one with $\chi=-1$—is physically impossible because its net [chirality](@entry_id:144105) would be $+1$. The simplest Weyl semimetal must contain at least one pair: one source and one sink of Berry curvature.

### Bulk-Boundary Correspondence and Fermi Arcs

One of the most spectacular consequences of the non-trivial bulk topology of Weyl semimetals is the emergence of unique, protected states on their surfaces. This is an example of the **[bulk-boundary correspondence](@entry_id:137647)**, a guiding principle in [topological physics](@entry_id:142619): a non-trivial [topological invariant](@entry_id:142028) characterizing the bulk of a material mandates the existence of gapless states at its boundary.

For Weyl semimetals, these surface states take the form of **Fermi arcs**. Unlike the closed Fermi surfaces of conventional metals or the point-like Fermi surface of the bulk Weyl semimetal at the CNP, Fermi arcs are open, disconnected segments of a Fermi surface that exist only on the crystal's surface. These arcs connect the projections of bulk Weyl points of opposite [chirality](@entry_id:144105) onto the surface Brillouin zone.

The existence and robustness of Fermi arcs are a direct experimental signature of the Weyl semimetal phase [@problem_id:1827857]. Consider two semimetallic materials, one a Weyl semimetal (Material A) and the other a trivial metal (Material B). Using a surface-sensitive technique like Angle-Resolved Photoemission Spectroscopy (ARPES), one would observe open Fermi arcs on Material A's surface. On Material B, one might see conventional closed-loop surface states. If a thin layer of a trivial insulator is then deposited on both, the trivial [surface states](@entry_id:137922) of Material B can be easily destroyed, or "gapped out." In stark contrast, the Fermi arcs on Material A will persist. They are topologically protected by the bulk band structure and cannot be removed by any weak perturbation that does not close the bulk band gap and destroy the Weyl points themselves.

These Fermi arcs facilitate exotic transport phenomena. An electron can travel through the bulk of the crystal, emerge on a surface, traverse a Fermi arc to the projection of a different Weyl point, and re-enter the bulk, completing a novel transport loop sometimes referred to as a "wormhole orbit" in [momentum space](@entry_id:148936) [@problem_id:1827830]. This process connects the two opposite surfaces of the material through the bulk, a direct consequence of the [chiral anomaly](@entry_id:142077).

### Classifications and Advanced Concepts

The family of [topological semimetals](@entry_id:137800) is rich and diverse. Further classifications arise from more detailed features of the band structure.

#### Type-I and Type-II Weyl Semimetals
The idealized linear cone of a Weyl point can be tilted. The general dispersion near a Weyl point is given by $E_{\pm}(\mathbf{k}) = \mathbf{w} \cdot \mathbf{k} \pm v_F |\mathbf{k}|$, where $\mathbf{w}$ is a tilt velocity vector. The classification depends on the relative magnitude of the tilt term $|\mathbf{w}|$ and the conic term $v_F$:
*   **Type-I Weyl Semimetal:** The tilt is small, $|\mathbf{w}|  v_F$. The Weyl cone remains upright. At the CNP, the [constant energy surface](@entry_id:262911) $E(\mathbf{k})=0$ is still a single point.
*   **Type-II Weyl Semimetal:** The tilt is so large that $|\mathbf{w}| > v_F$. The Weyl cone is tipped over. This dramatic tilting means that even at the energy of the Weyl node, there are other states that cross the Fermi level. The result is that at the CNP, a Type-II Weyl semimetal possesses both **electron and [hole pockets](@entry_id:269009)** that touch at the Weyl point, forming a finite Fermi surface [@problem_id:1827824]. This is a sharp contrast to the point-like Fermi surface of a Type-I Weyl semimetal.

#### Symmetry Protection of Dirac Points
While we have focused on Dirac points protected by the combination of T and P symmetries, this is not the only mechanism. Certain crystal symmetries known as **non-symmorphic symmetries** can also protect four-fold degenerate Dirac points. These symmetries involve a [point group](@entry_id:145002) operation (like a rotation or reflection) followed by a fractional translation of the crystal lattice.

A key qualitative difference arises from the protection mechanism [@problem_id:1827841]. Dirac points protected by T and P symmetry can occur at generic, low-symmetry points within the Brillouin zone. Their exact location is determined by material-specific parameters. In contrast, Dirac points protected by non-symmorphic symmetries are rigorously pinned by symmetry to lie on high-symmetry planes or lines, typically at the boundary of the Brillouin zone. This distinction highlights the deep and multifaceted relationship between [crystal symmetry](@entry_id:138731) and topological [electronic states](@entry_id:171776).