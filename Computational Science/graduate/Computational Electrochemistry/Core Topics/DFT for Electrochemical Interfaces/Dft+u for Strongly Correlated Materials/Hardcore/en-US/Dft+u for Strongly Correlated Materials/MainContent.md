## Introduction
Materials with [strongly correlated electrons](@entry_id:145212), such as [transition-metal oxides](@entry_id:1133348), are at the forefront of modern technology, driving innovations in fields from energy storage to electronics. However, capturing the behavior of their localized $d$ and $f$ electrons presents a major hurdle for one of the most widely used tools in computational science, Density Functional Theory (DFT). Standard approximations within DFT suffer from [self-interaction](@entry_id:201333) errors that lead to a poor description of [electron localization](@entry_id:261499), often resulting in qualitatively wrong predictions, such as describing known insulators as metals. This article addresses this critical knowledge gap by providing a comprehensive guide to the DFT+$U$ method, a powerful and widely adopted correction scheme.

Across the following chapters, you will gain a robust understanding of this essential technique. The journey begins in **Principles and Mechanisms**, where we will dissect the fundamental failures of standard DFT and detail the theoretical formalism of the DFT+$U$ correction. Next, **Applications and Interdisciplinary Connections** will demonstrate the method's practical power by exploring its success in predicting the properties of energy materials, catalysts, and other complex solids. Finally, **Hands-On Practices** will offer guided exercises to translate theoretical knowledge into practical computational skills. We will begin by exploring the foundational principles that make DFT+$U$ an indispensable tool for modeling the complex world of [strongly correlated materials](@entry_id:198946).

## Principles and Mechanisms

The description of electron behavior in many materials of technological importance, such as [transition-metal oxides](@entry_id:1133348) used in batteries and catalysts, poses a significant challenge to standard computational methods. These materials often feature partially filled $d$ or $f$ [electron shells](@entry_id:270981), where electrons are spatially localized and interact strongly with one another. This phenomenon, known as **[strong electron correlation](@entry_id:183841)**, gives rise to a rich spectrum of physical properties, including metal-insulator transitions, complex [magnetic ordering](@entry_id:143206), and exotic superconductivity. Standard approximations within Density Functional Theory (DFT), such as the Local Density Approximation (LDA) and the Generalized Gradient Approximation (GGA), often fail to capture these effects, leading to qualitatively incorrect predictions. This chapter delineates the fundamental reasons for this failure and details the principles and mechanisms of the DFT+$U$ method, a widely used corrective approach that has become an indispensable tool in [computational materials science](@entry_id:145245) and electrochemistry.

### The Origin of Strong Correlation Errors in Semilocal DFT

At the heart of standard DFT's difficulties with [strongly correlated materials](@entry_id:198946) is the **self-interaction error (SIE)**. In exact DFT, the repulsive Hartree energy of an electron interacting with the total electron density includes an unphysical interaction of the electron with itself. This spurious self-interaction is supposed to be canceled exactly by the exchange-correlation functional. For any one-electron system, this cancellation must be perfect. However, in approximate semilocal functionals like LDA and GGA, this cancellation is incomplete. An electron "feels" a residual repulsion from its own charge density, an artifact that has profound consequences.

A fundamental property of the exact energy functional, $E(N)$, is its **[piecewise linearity](@entry_id:201467)** as a function of the number of electrons, $N$. The energy should vary linearly between integer electron counts. The derivative of the energy with respect to occupation, $\partial E / \partial N$, should be constant for fractional $N$, jumping discontinuously at integer values. The SIE inherent in semilocal functionals violates this condition. It introduces a spurious **[convexity](@entry_id:138568)** to the $E(N)$ curve, meaning the energy of a system with a fractional number of electrons is artificially lowered relative to the linear interpolation between the adjacent integer-electron states.

This artifact leads directly to the **[delocalization error](@entry_id:166117)**. To understand this, consider a simple but illustrative model of a single excess electron to be placed on one of two equivalent atomic sites, A and B, in a material . The physically correct ground state should have the electron fully localized on one site, e.g., with occupations $(n_A, n_B) = (1, 0)$ or $(0, 1)$. The exact piecewise-[linear functional](@entry_id:144884) would correctly predict this. However, a functional with a convex energy dependence on occupation will erroneously predict a lower energy for a delocalized state where the electron is spread across both sites, such as $(n_A, n_B) = (\frac{1}{2}, \frac{1}{2})$. Mathematically, if the site energy $E_{\text{site}}(n)$ is a convex function of occupation $n$, Jensen's inequality dictates that the energy of the delocalized state, $2 E_{\text{site}}(\frac{1}{2})$, is lower than the energy of the localized state, $E_{\text{site}}(1) + E_{\text{site}}(0)$ .

This bias towards delocalization causes semilocal DFT to incorrectly predict metallic behavior for materials that are, in fact, insulators (e.g., Mott insulators like NiO) and to systematically underestimate quantities that depend on [electron localization](@entry_id:261499), such as [band gaps](@entry_id:191975) and local magnetic moments.

### The DFT+$U$ Correction: A Hubbard-Model-Inspired Solution

To address the shortcomings of semilocal DFT, the DFT+$U$ method introduces a corrective term inspired by the **Hubbard model**, a cornerstone of condensed matter physics for describing interacting [localized electrons](@entry_id:751389). The core idea is to add an explicit on-site Coulomb repulsion term to the DFT [energy functional](@entry_id:170311), which acts specifically on a chosen set of [localized orbitals](@entry_id:204089) (the **correlated subspace**, e.g., the $3d$ orbitals of a transition metal). This correction is designed to counteract the spurious [delocalization](@entry_id:183327) by adding an energy penalty for fractional occupations.

This added interaction is typically parameterized by two main quantities :

-   The **on-site Coulomb parameter ($U$)**: This represents the screened direct Coulomb repulsion, which is the energy cost of placing two electrons on the same localized orbital. Its primary effect is to penalize charge fluctuations and double occupancy, thus promoting [electron localization](@entry_id:261499) and opening a correlation-induced band gap.

-   The **intra-atomic exchange parameter ($J$)**: This parameter, also known as the Hund's exchange parameter, arises from the Pauli exclusion principle. It energetically favors aligning the spins of electrons in different orbitals on the same atom, consistent with Hund's rules. Its main effect is to stabilize high-spin configurations and influence [magnetic ordering](@entry_id:143206).

By adding a term that increases the energy of partially occupied states, DFT+$U$ introduces a [negative curvature](@entry_id:159335) to the energy functional that counteracts the positive [convexity](@entry_id:138568) of the underlying DFT approximation. For a sufficiently large $U$, this correction restores a preference for integer occupations, thereby promoting the localization of electrons onto specific atomic sites.

### Formalism of the DFT+$U$ Method

The total energy in a DFT+$U$ calculation is expressed as:
$E_{\text{DFT+}U} = E_{\text{DFT}} + E_{U} - E_{\text{DC}}$
Here, $E_{\text{DFT}}$ is the standard energy from a semilocal functional, $E_{U}$ is the added Hubbard interaction energy, and $E_{\text{DC}}$ is a **double-counting** term, which will be discussed shortly.

#### The Correlated Subspace and the Occupation Matrix

The DFT+$U$ correction is not applied to all electrons, but only to those within a predefined **correlated subspace**. This subspace is typically spanned by a set of localized, atom-centered orbitals, such as the $d$-orbitals of a transition metal or $f$-orbitals of a lanthanide.

The central quantity in the formalism is the **occupation matrix**, a representation of the electronic density projected onto this local subspace. For a given correlated site $I$ and spin channel $\sigma \in \{\uparrow, \downarrow\}$, its elements are defined as:
$n_{mm'}^{I\sigma} = \sum_{k,v} f_{kv\sigma} \langle \phi_{Im} | \psi_{kv\sigma} \rangle \langle \psi_{kv\sigma} | \phi_{Im'} \rangle$
where $|\phi_{Im}\rangle$ are the localized projector orbitals, $|\psi_{kv\sigma}\rangle$ are the calculated Kohn-Sham orbitals of the crystal, and $f_{kv\sigma}$ are their Fermi-Dirac occupations .

This occupation matrix has several important properties:
-   It is **Hermitian**: $n_{mm'}^{I\sigma} = (n_{m'm}^{I\sigma})^*$.
-   Its trace, $\mathrm{Tr}(n^{I\sigma}) = \sum_m n_{mm}^{I\sigma}$, gives the total number of electrons with spin $\sigma$ in the correlated subspace of atom $I$.
-   The diagonal elements, $n_{mm}^{I\sigma}$, represent the occupation of the local orbital $m$.
-   The off-diagonal elements, $n_{m \neq m'}^{I\sigma}$, represent **[orbital mixing](@entry_id:188404)** or quantum coherences between different local orbitals, induced by the [crystal field](@entry_id:147193) environment or chemical bonding. They are crucial for a correct description, and their presence necessitates a rotationally invariant formulation of the theory. 

In standard collinear spin calculations without spin-orbit coupling, the spin-up and spin-down channels are independent. The full occupation matrix is block-diagonal in spin, with no coupling between the $n^{I\uparrow}$ and $n^{I\downarrow}$ blocks .

#### The Hubbard Energy Correction and Rotational Invariance

Several formulations for the Hubbard [energy correction](@entry_id:198270) $E_U$ exist. A widely used and conceptually clear form is the simplified, **rotationally invariant** approach proposed by Dudarev et al. This approach combines the $U$ and $J$ parameters into a single effective parameter, $U_{\text{eff}} = U - J$. The [energy correction](@entry_id:198270) for a site $I$ is given by:
$E_U = \frac{U_{\text{eff}}}{2} \sum_{\sigma} \left[ \mathrm{Tr}(n^{I\sigma}) - \mathrm{Tr}\left((n^{I\sigma})^2\right) \right]$
This expression depends on the trace of the occupation matrix and the trace of its square, which are both invariant under a unitary rotation of the basis orbitals $\{|\phi_{Im}\rangle\}$. This rotational invariance is a critical property, ensuring that the calculated energy does not depend on the arbitrary orientation of the [local coordinate system](@entry_id:751394).

Physically, this energy term acts as a penalty for non-integer occupations. The quantity within the brackets, $\sum_i (\lambda_i - \lambda_i^2)$ where $\lambda_i$ are the eigenvalues of the occupation matrix, is zero only when all eigenvalues are either $0$ or $1$. Any fractional eigenvalue, corresponding to a partially occupied orbital, results in a positive energy penalty, thus driving the system toward a state of integer occupations .

#### The Double-Counting Problem

The approximate DFT [exchange-correlation functional](@entry_id:142042) already contains a mean-field description of the on-site [electron-electron interactions](@entry_id:139900). Simply adding the Hubbard term $E_U$ would amount to counting these interactions twice. To correct for this, a **double-counting (DC) correction**, $E_{\text{DC}}$, must be subtracted.

The [exact form](@entry_id:273346) of the DC term is unknown because the exact portion of the on-site interaction described by the DFT functional is unknown. This has led to the development of several approximate DC schemes, with two being most prominent :

1.  **Fully Localized Limit (FLL)**: This scheme assumes that the underlying DFT functional should be corrected for a system of fully localized, integer-occupation orbitals, i.e., the atomic limit. The DC term subtracts the average interaction energy of an isolated atom with a fixed integer number of electrons, $N$. For a total occupation $N = \sum_\sigma N_\sigma$ with $N_\sigma = \mathrm{Tr}(n^{I\sigma})$, the FLL DC term is:
    $E_{\text{DC}}^{\text{FLL}} = \frac{U}{2} N(N-1) - \frac{J}{2} \sum_{\sigma} N_{\sigma}(N_{\sigma}-1)$
    The FLL scheme is physically appropriate for systems where electrons are expected to be highly localized, such as in Mott or [charge-transfer](@entry_id:155270) insulators.  

2.  **Around Mean-Field (AMF)**: This scheme is designed for the opposite limit of more itinerant or metallic systems. It assumes that the underlying DFT functional provides a good description of the average, or mean-field, state where electrons are distributed uniformly across the correlated orbitals. The DC term is then set equal to the value of the Hubbard energy for this average configuration. The key feature of the AMF correction is that $E_U - E_{\text{DC}}^{\text{AMF}}$ is zero for a uniform occupation distribution and penalizes deviations from it. This makes it suitable for metallic systems or materials with significant [covalency](@entry_id:154359) where one does not wish to impose strong localization. 

The choice of DC scheme is a critical part of a DFT+$U$ calculation, as it defines the [reference state](@entry_id:151465) from which the Hubbard correction is applied and can significantly impact calculated properties like [band gaps](@entry_id:191975) and reaction energies.

### Consequences of the Hubbard Correction: A Case Study of NiO

The effects of the DFT+$U$ correction can be vividly illustrated using the prototypical correlated insulator, nickel oxide (NiO). Standard LDA or GGA calculations incorrectly predict NiO to be a metal. In the [rocksalt structure](@entry_id:192480), the Ni ion is in a $2+$ [oxidation state](@entry_id:137577) with a $d^8$ [electron configuration](@entry_id:147395). In the octahedral [crystal field](@entry_id:147193), these are split into filled $t_{2g}^6$ states and partially-filled high-spin $e_g^2$ states. LSDA calculations show these $e_g$ states forming bands that cross the Fermi level, with highly fractional occupations .

When a finite $U_{\text{eff}}$ is applied to the Ni $3d$ states, the DFT+$U$ method introduces a spin- and orbital-dependent potential. In the Dudarev formalism, this potential is approximately $V_m^\sigma \approx \frac{U_{\text{eff}}}{2}(1-2n_m^\sigma)$.
-   For the nearly **filled** majority-spin $e_g$ orbitals ($n^\uparrow \approx 1$), the potential is negative ($V^\uparrow \approx -U_{\text{eff}}/2$), shifting these states downward in energy.
-   For the nearly **empty** minority-spin $e_g$ orbitals ($n^\downarrow \approx 0$), the potential is positive ($V^\downarrow \approx +U_{\text{eff}}/2$), shifting these states upward in energy.

This "scissor-like" action of the potential forcefully drives the occupied and unoccupied $d$-states apart, opening a substantial band gap. The separation between the occupied and unoccupied manifolds increases approximately linearly with $U_{\text{eff}}$. Furthermore, by penalizing fractional occupations, the correction drives the occupations toward integer values ($n^\uparrow \to 1$, $n^\downarrow \to 0$), which significantly enhances the spin polarization and thus increases the calculated **[local magnetic moment](@entry_id:142147)** on the Ni site, bringing it into much better agreement with experimental values .

### Broader Impacts: Electron Localization and Polaron Formation

The ability of DFT+$U$ to correctly describe [electron localization](@entry_id:261499) has implications beyond [band gaps](@entry_id:191975) and magnetism. A key example is the formation of **small [polarons](@entry_id:191083)**. A [small polaron](@entry_id:145105) is a quasiparticle formed when a charge carrier (an electron or hole) becomes trapped by a local distortion of the crystal lattice that it induces itself. This [self-trapping](@entry_id:144773) is an intrinsic electron-lattice coupling phenomenon.

The formation of a stable [polaron](@entry_id:137225) involves a competition. The lattice can lower its energy by distorting around a localized charge, an energy gain that is typically proportional to the square of the localized charge density. This favors localization. However, the electron's kinetic energy is lowered by delocalizing. In semilocal DFT, the [delocalization error](@entry_id:166117) adds a spurious electronic energy stabilization for the delocalized state, which can overwhelm the lattice's preference for localization. As a result, standard DFT often fails to predict the formation of [polarons](@entry_id:191083), instead favoring delocalized band-like states.

DFT+$U$ resolves this issue. By adding the Hubbard penalty for fractional occupations, it removes the spurious energetic bias towards [delocalization](@entry_id:183327). This allows the system to correctly access the localized electronic state, which in turn enables the favorable [lattice distortion](@entry_id:1127106) to occur, leading to the formation of a stable [small polaron](@entry_id:145105). This illustrates that DFT+$U$ is not merely a gap-correction scheme but a more fundamental tool for restoring the correct balance between localized and delocalized electronic states in [correlated materials](@entry_id:138171) .

### Determining the Hubbard U: Ab Initio Approaches

While $U$ is sometimes treated as an empirical parameter adjusted to match experimental data, this approach undermines the predictive power of DFT. To maintain a first-principles framework, several *[ab initio](@entry_id:203622)* methods have been developed to calculate $U$.

#### Linear Response Method

The [linear response method](@entry_id:751324) provides a direct way to compute $U$ from the system's electronic response to a small perturbation . The Hubbard $U$ can be rigorously defined as the second derivative of the energy with respect to the occupation of the correlated orbitals. This can be calculated by applying a small perturbing potential $\alpha$ to the correlated subspace and measuring the change in its occupation, $n_I$. The response is characterized by two susceptibilities:
-   The **bare susceptibility**, $\chi_0 = \partial n_I / \partial \alpha$, which is the response of the non-interacting Kohn-Sham system.
-   The **screened susceptibility**, $\chi = \partial n_I / \partial \alpha$, which is the full, self-consistent response of the interacting system, including all [electronic screening](@entry_id:146288).

The relationship between these quantities leads to a simple expression for the Hubbard parameter:
$U = \chi_0^{-1} - \chi^{-1}$
This method captures the [electronic screening](@entry_id:146288) from the entire system and provides a robust, physically transparent way to determine $U$. For instance, the presence of a polarizable environment like an aqueous electrolyte provides additional screening channels, which increases the magnitude of $\chi$ and consequently reduces the calculated value of $U$ .

#### Constrained Random Phase Approximation (cRPA)

Another powerful *ab initio* technique is the constrained Random Phase Approximation (cRPA). This method aims to calculate the effective interaction $U$ for the correlated subspace that is screened by all electrons *except* those within the correlated subspace itself. The logic is that the correlations *within* the subspace will be handled by the Hubbard model, so their [screening effect](@entry_id:143615) should not be included in the parameter $U$.

The procedure involves :
1.  Decomposing the total [electronic polarizability](@entry_id:275814) (or polarization) of the system, $P(\omega)$, into two parts: a contribution from transitions within the correlated subspace, $P_C(\omega)$, and a contribution from all other transitions, $P_R(\omega)$.
2.  Calculating a partially [screened interaction](@entry_id:136395), $U(\omega)$, by screening the bare Coulomb interaction $v$ only with the "rest" polarization, $P_R(\omega)$. This is achieved via a constrained [dielectric function](@entry_id:136859) $\varepsilon_R(\omega) = 1 - v P_R(\omega)$.
3.  Taking the [static limit](@entry_id:262480) ($\omega \to 0$) of the real part of this frequency-dependent interaction to obtain the static $U$ parameter used in DFT+$U$: $U = \mathrm{Re}[U(\omega=0)]$.

Both linear response and cRPA provide systematic, non-empirical routes to parameterize DFT+$U$ calculations, greatly enhancing their predictive capability.

### An Advanced Topic: The Definition of the Correlated Subspace

A final, crucial point is that the Hubbard $U$ is not a fundamental physical observable but a parameter of an effective model. Its numerical value and physical interpretation depend critically on the **definition of the correlated subspace**. This choice is typically between two common constructs :

1.  **Atomic-like Projectors**: The subspace is defined by orbitals that are mathematically constructed to resemble pure, isolated atomic orbitals (e.g., atomic $d$-orbitals). These are highly localized.
2.  **Wannier Functions**: The subspace is defined by maximally localized Wannier functions constructed from a set of Bloch bands around the Fermi level. In [transition-metal oxides](@entry_id:1133348), these bands often have significant character from both the metal $d$ and ligand (e.g., oxygen $p$) orbitals. These Wannier functions are therefore more spatially extended and represent hybridized, covalent states.

This choice creates a fundamental trade-off. When moving from a localized [atomic basis](@entry_id:1121220) to a more extended Wannier basis:
-   The **bare Coulomb interaction** [matrix elements](@entry_id:186505) decrease because the orbitals are more spread out.
-   The **screening is reduced**. This is because [electronic screening](@entry_id:146288) channels that were previously external to the subspace (e.g., transitions involving oxygen $p$-states) are now considered internal to the new, larger Wannier-function subspace. In cRPA, these internal screening channels are excluded from the calculation of $U$.

The final value of $U$ depends on the competition between these two opposing effects. It is often found that the reduction in screening is the dominant effect, leading to a *larger* $U$ for a more extended Wannier-function basis. More importantly, the **physical interpretation changes**. For an atomic subspace, $U$ represents a purely intra-atomic repulsion. For a Wannier subspace, $U$ represents an effective interaction between electrons in delocalized, covalent-[bonding orbitals](@entry_id:165952). This highlights the essential nature of DFT+$U$ as an effective low-energy model, where consistency between the definition of the subspace and the calculation and application of the parameter $U$ is paramount for physically meaningful results.