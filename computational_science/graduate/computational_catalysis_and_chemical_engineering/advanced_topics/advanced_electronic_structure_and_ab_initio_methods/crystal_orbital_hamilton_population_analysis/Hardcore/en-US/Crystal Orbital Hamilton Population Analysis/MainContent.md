## Introduction
In the world of [computational chemistry](@entry_id:143039) and materials science, moving beyond qualitative descriptions of chemical bonding to a quantitative understanding is paramount for rational design. While we intuitively speak of bonds as 'strong' or 'weak', a rigorous, energy-based framework is needed to dissect these interactions within the complex electronic structure of a solid. Crystal Orbital Hamilton Population (COHP) analysis provides exactly such a tool. It addresses the knowledge gap by partitioning the total band-structure energy from Density Functional Theory (DFT) into specific, energy-resolved contributions from atomic pairs, offering a clear picture of bonding, non-bonding, and antibonding interactions.

This article will guide you through this powerful method. First, the **Principles and Mechanisms** chapter will detail the theoretical foundation of COHP, explaining how it is defined, how to interpret its output, and how it is implemented in modern [plane-wave calculations](@entry_id:753473). Following this, the **Applications and Interdisciplinary Connections** chapter will demonstrate the method's utility in solving real-world problems in materials science and heterogeneous catalysis, from characterizing interfaces to designing optimal catalysts. Finally, the **Hands-On Practices** section will offer a series of targeted exercises to solidify your understanding, bridging the gap between theory and practical application.

## Principles and Mechanisms

### Conceptual Foundation: Partitioning the Band Structure Energy

The total energy of a crystalline solid, within the framework of Kohn-Sham Density Functional Theory (DFT), is a complex functional of the electron density. However, significant insight into the system's stability and chemical bonding can be gleaned from the **band structure energy**, $E_{\text{band}}$, which is the sum of the energies of all occupied one-electron states. For a periodic solid described by Bloch's theorem, the band structure energy is given by an integral over the first Brillouin zone:

$$E_{\text{band}} = \sum_{n} \int_{\text{BZ}} w_{\mathbf{k}} f_{n\mathbf{k}} \epsilon_{n\mathbf{k}} \, d\mathbf{k}$$

Here, $n$ is the band index, $\mathbf{k}$ is a crystal momentum vector in the Brillouin zone, $w_{\mathbf{k}}$ is the k-point weight, $f_{n\mathbf{k}}$ is the occupation number (typically 1 or 0 at zero temperature) of the state with energy $\epsilon_{n\mathbf{k}}$.

To understand chemical bonding, it is desirable to partition this total energy into contributions arising from individual atoms and, more importantly, from pairs of atoms representing chemical bonds. This partitioning forms the conceptual basis for many chemical analysis tools in solid-state theory. If we expand the crystal orbitals (Bloch states) $\psi_{n\mathbf{k}}$ in a basis of localized atomic orbitals (LCAO) $\{\phi_{\mu}\}$, the eigenvalue $\epsilon_{n\mathbf{k}}$ for a given state can be expressed as the expectation value of the Hamiltonian operator, $\hat{H}$:

$$\epsilon_{n\mathbf{k}} = \langle \psi_{n\mathbf{k}} | \hat{H} | \psi_{n\mathbf{k}} \rangle = \sum_{\mu, \nu} c_{\mu, n\mathbf{k}}^{*} H_{\mu\nu}(\mathbf{k}) c_{\nu, n\mathbf{k}}$$

where $c_{\mu, n\mathbf{k}}$ are the expansion coefficients and $H_{\mu\nu}(\mathbf{k}) = \langle \phi_{\mu\mathbf{k}} | \hat{H} | \phi_{\nu\mathbf{k}} \rangle$ are the [matrix elements](@entry_id:186505) of the Hamiltonian in the basis of Bloch-symmetrized atomic orbitals. Substituting this back into the expression for $E_{\text{band}}$ reveals that the total band energy is fundamentally a linear sum of terms involving the **Hamiltonian [matrix elements](@entry_id:186505)** $H_{\mu\nu}$.

$$E_{\text{band}} = \sum_{n, \mathbf{k}} f_{n\mathbf{k}} \sum_{\mu, \nu} c_{\mu, n\mathbf{k}}^{*} H_{\mu\nu}(\mathbf{k}) c_{\nu, n\mathbf{k}} = \sum_{\mu, \nu} \text{Tr}[P_{\nu\mu} H_{\mu\nu}]$$

where $P_{\nu\mu}$ is the density matrix. This fundamental relationship demonstrates that any decomposition of the band energy into orbital-pair contributions must be weighted by the Hamiltonian [matrix elements](@entry_id:186505), as they carry the energetic information of the system. Weighting by any other quantity, such as the [overlap matrix](@entry_id:268881) $S_{\mu\nu}$, would not produce a quantity with units of energy that sums to a component of $E_{\text{band}}$ . This Hamiltonian-weighting principle is the cornerstone of the Crystal Orbital Hamilton Population method.

### Formal Definition of Crystal Orbital Hamilton Population (COHP)

The **Crystal Orbital Hamilton Population (COHP)** analysis, introduced by Dronskowski and Blöchl, provides an energy-resolved partitioning of the band structure energy into contributions from pairs of atoms. For a chosen pair of atoms, $A$ and $B$, the COHP value at a [specific energy](@entry_id:271007) $E$, denoted $COHP_{AB}(E)$, quantifies the contribution of the $A-B$ interactions to the density of states at that energy. It is formally defined as:

$$COHP_{AB}(E) = \sum_{n, \mathbf{k}} w_{\mathbf{k}} \delta(E - \epsilon_{n\mathbf{k}}) \text{Re} \left[ \sum_{\mu \in A} \sum_{\nu \in B} c_{\mu, n\mathbf{k}}^{*} H_{\mu\nu}(\mathbf{k}) c_{\nu, n\mathbf{k}} \right]$$

Let us dissect this definition :
*   The sum runs over all bands $n$ and all $\mathbf{k}$-points in the Brillouin zone.
*   The Dirac [delta function](@entry_id:273429), $\delta(E - \epsilon_{n\mathbf{k}})$, projects the contributions onto the energy axis, making COHP an **energy-resolved** quantity. In practice, this is achieved by constructing a histogram over a fine energy grid.
*   The core of the expression is the term $\text{Re}[\dots]$, which represents the contribution of the interaction between orbitals on atom $A$ (indexed by $\mu$) and atom $B$ (indexed by $\nu$) to the energy of state $\psi_{n\mathbf{k}}$.
*   The summation is restricted to pairs of orbitals where one is centered on atom $A$ and the other on atom $B$, thereby isolating the pairwise interaction.

This definition should be contrasted with that of the **Crystal Orbital Overlap Population (COOP)**, which has a similar form but replaces the Hamiltonian matrix $H_{\mu\nu}(\mathbf{k})$ with the **[overlap matrix](@entry_id:268881)** $S_{\mu\nu}(\mathbf{k})$. While COOP provides a valuable, energy-resolved picture of the bonding/antibonding character based on [orbital overlap](@entry_id:143431) (a dimensionless quantity related to bond order), it is not an energy partitioning scheme. COHP, by virtue of its Hamiltonian weighting, directly measures the energetic stabilization or destabilization arising from the interaction . Both differ from the energy-integrated Mulliken population analysis, which provides a single number for the charge in an overlap region.

### Interpreting COHP: Bonding, Antibonding, and Energetic Stabilization

A plot of $COHP(E)$ versus energy provides a powerful visual tool for understanding the chemical bonds in a material. The key to its interpretation lies in the sign of the COHP values.

#### The Meaning of the Sign

By convention, a negative value of $COHP(E)$ at a given energy indicates a **bonding** interaction, which contributes to the stabilization of the structure. Conversely, a positive value of $COHP(E)$ indicates an **antibonding** interaction, which is destabilizing .

This sign convention can be understood from first principles. The contribution of an orbital pair $(\mu, \nu)$ to the energy of a state $(n, \mathbf{k})$ is proportional to $\text{Re}[c_{\mu, n\mathbf{k}}^{*} H_{\mu\nu}(\mathbf{k}) c_{\nu, n\mathbf{k}}]$. For a typical bonding interaction (e.g., between two s-orbitals), the off-diagonal Hamiltonian [matrix element](@entry_id:136260) $H_{\mu\nu}$ is negative. A bonding molecular orbital is formed when the atomic orbital coefficients, $c_{\mu}$ and $c_{\nu}$, are in-phase (i.e., their product is positive). The resulting energy contribution is a product of (positive) $\times$ (negative), yielding a negative, stabilizing value. In contrast, for an antibonding molecular orbital, the coefficients are out-of-phase (their product is negative). The energy contribution becomes (negative) $\times$ (negative), resulting in a positive, destabilizing value . Thus, the sign of $COHP(E)$ directly reflects the energetic consequence of the interaction.

#### The $-COHP$ Convention

While the formal definition associates bonding with negative values, it is common in publications and software outputs to plot **$-COHP(E)$**. This is a simple cosmetic change, defined as:

$$-COHP_{AB}(E) := - (COHP_{AB}(E))$$

In a $-COHP(E)$ plot, positive peaks correspond to bonding interactions, and negative peaks (valleys) correspond to antibonding interactions. This convention is often preferred as it aligns with the intuitive notion that a positive peak represents a "favorable" bonding contribution. When encountering COHP data, it is crucial to identify which convention is being used. The translation is a simple multiplication of the entire curve and its integral by $-1$, without any change to the energy axis .

### From Energy Resolution to Integrated Bond Strength

#### The Integrated COHP (ICOHP)

Integrating the $COHP(E)$ curve up to the Fermi energy, $E_F$, yields the **Integrated Crystal Orbital Hamilton Population (ICOHP)**. This single value represents the net contribution of the specified bond to the total band structure energy, accounting for all occupied [bonding and antibonding states](@entry_id:1121752).

$$ICOHP_{AB} = \int_{-\infty}^{E_F} COHP_{AB}(E) \,dE$$

Following the standard sign convention, a more negative $ICOHP_{AB}$ value indicates a stronger net [covalent bond](@entry_id:146178). For the $-COHP$ convention, the integral is denoted $-ICOHP_{AB}$, and a more positive value signifies a stronger bond. The ICOHP is an extensive quantity, dependent on the size of the unit cell. To compare bond strengths across different materials or structures, it is essential to normalize the value. This is typically done on a "per bond" basis, where the total ICOHP from the unit cell calculation is divided by the number of such bonds within that cell .

#### The Complementary Roles of COHP and ICOHP

While the ICOHP provides a convenient single-metric descriptor for [bond strength](@entry_id:149044), its value can be misleading if considered in isolation. The true power of the COHP method lies in its [energy resolution](@entry_id:180330), which provides diagnostic and predictive insights that complement the integrated value .

Consider a hypothetical metal-carbon ($M-C$) bond on a catalytic surface. The ICOHP might be $-2.5$ eV, indicating a strong net bond. However, the $COHP(E)$ plot might reveal not only a large region of bonding states deep in the valence band but also a small region of antibonding states located just below the Fermi level. The ICOHP value simply sums these contributions. The energy-resolved plot, however, reveals a critical vulnerability: the presence of occupied antibonding states weakens the bond. Furthermore, it might show a significant density of unoccupied antibonding states just *above* the Fermi level. This information allows us to predict the system's response to perturbations. For instance, if electrons are added to the system (doping), the Fermi level will rise, populating these antibonding states and weakening the $M-C$ bond. The ICOHP value alone cannot provide this crucial predictive information; it only reports the current state of the bond .

### Practical Implementation in Plane-Wave DFT

#### Projection from Plane Waves

The conceptual framework of COHP is most naturally described in a basis of localized atomic orbitals. However, the majority of modern solid-state DFT calculations employ [plane waves](@entry_id:189798) as the basis set, which are delocalized over the entire crystal. In a [plane-wave basis](@entry_id:140187), the Hamiltonian and overlap matrices are not naturally partitioned into atom-centered blocks. To perform a COHP analysis, one must therefore project the delocalized plane-wave Kohn-Sham states, $\psi_{n\mathbf{k}}$, onto a suitable localized atomic-orbital-like basis, $\{\chi_{\mu}\}$, to obtain the necessary coefficients $c_{\mu,n\mathbf{k}}$ and Hamiltonian [matrix elements](@entry_id:186505) $H_{\mu\nu}$.

#### The Role of the Projector Augmented-Wave (PAW) Method

The **Projector Augmented-Wave (PAW)** method, a widely used approach that bridges the gap between computationally expensive all-electron calculations and less accurate [pseudopotential](@entry_id:146990) methods, provides a rigorous framework for this projection. The central idea of PAW is a [linear transformation](@entry_id:143080) $\mathcal{T}$ that maps the smooth (pseudo) wavefunctions $\tilde{\psi}$, which are represented by plane waves, to the true, rapidly oscillating all-electron wavefunctions $\psi$. This transformation relies on atom-centered augmentation spheres. Inside each sphere, the transformation adds a correction based on a set of all-electron partial waves $\{\phi_i\}$, smooth partial waves $\{\tilde{\phi}_i\}$, and dual projector functions $\{\tilde{p}_i\}$.

To obtain the coefficients for COHP, one must calculate the overlap $c_{\mu,n\mathbf{k}} = \langle \chi_{\mu} | \psi_{n\mathbf{k}} \rangle$. Using the PAW transformation, this becomes $c_{\mu,n\mathbf{k}} = \langle \chi_{\mu} | \mathcal{T} | \tilde{\psi}_{n\mathbf{k}} \rangle$. The calculation involves two main steps:
1.  The **projector functions** $\tilde{p}_i$ act on the smooth wavefunction $\tilde{\psi}_{n\mathbf{k}}$ to extract its local character within each augmentation sphere, yielding scalar coefficients $\langle \tilde{p}_i | \tilde{\psi}_{n\mathbf{k}} \rangle$.
2.  These coefficients are then used to combine the **partial waves** ($\phi_i$ and $\tilde{\phi}_i$) with the smooth part of the wavefunction to reconstruct the all-electron [overlap integral](@entry_id:175831) .

Similarly, the all-electron Hamiltonian [matrix elements](@entry_id:186505) $H_{\mu\nu} = \langle \chi_{\mu} | \hat{H} | \chi_{\nu} \rangle$ are calculated by transforming the operator into the pseudo-representation: $\langle \tilde{\chi}_{\mu} | \mathcal{T}^{\dagger} \hat{H} \mathcal{T} | \tilde{\chi}_{\nu} \rangle$. This results in a final expression that consists of a "smooth" part calculated in the interstitial region and a sum of on-site corrections within each augmentation sphere. These corrections are constructed from [matrix elements](@entry_id:186505) of the Hamiltonian between the PAW partial waves, e.g., $\langle \phi_i | \hat{H} | \phi_j \rangle - \langle \tilde{\phi}_i | \hat{H} | \tilde{\phi}_j \rangle$, effectively restoring the all-electron physics in the region where it matters most . This machinery enables the robust calculation of COHP from standard plane-wave DFT output.

### Limitations and Advanced Applications in Catalysis

While COHP and ICOHP are powerful tools, relying on ICOHP as a sole descriptor of [bond strength](@entry_id:149044) for predicting catalytic activity can be problematic. In heterogeneous catalysis, reactivity is a frontier-orbital phenomenon, sensitive to the electronic structure near the Fermi level, whereas ICOHP integrates over all occupied states. A large, negative ICOHP might indicate great thermodynamic stability but poor reactivity.

Studies on complex materials like [perovskite oxides](@entry_id:192992) have shown that the ICOHP of a surface bond may not correlate well with catalytic properties like adsorption energies or [vacancy formation](@entry_id:196018) energies. This is because ICOHP, as a measure of [covalent bonding](@entry_id:141465), has several intrinsic limitations :
1.  **Neglect of Ionicity:** In polar materials like oxides, [electrostatic interactions](@entry_id:166363) contribute significantly to bonding energy. ICOHP does not capture this ionic component.
2.  **Conflation of Stability and Reactivity:** By including contributions from deep valence states, ICOHP reflects overall bond stability more than the [lability](@entry_id:155953) of frontier electrons involved in chemical reactions.
3.  **Insensitivity to Near-$E_F$ Features:** As discussed, the integrated value can obscure the crucial effect of occupied antibonding states just below $E_F$.

To build more robust predictive models for catalysis, it is state-of-the-art practice to construct **composite descriptors** that combine the covalent bond information from COHP with other key physical properties. A powerful composite descriptor might include :
*   The normalized ICOHP value to represent covalent strength.
*   The [bond length](@entry_id:144592), a primary geometric parameter.
*   A measure of charge transfer or site charge (e.g., from Bader analysis) to account for [ionicity](@entry_id:750816).
*   A specific metric for the occupation of antibonding states near the Fermi energy, extracted directly from the $COHP(E)$ curve.
*   The center of the metal d-band ($\epsilon_d$), a well-established descriptor of transition metal reactivity.

By combining these features, often within a machine learning framework, researchers can develop models that capture the multifaceted nature of [surface reactivity](@entry_id:1132688), leading to more accurate predictions in the rational design of new catalytic materials.