## Introduction
Calculating interatomic forces and the macroscopic stress tensor is fundamental to predicting and understanding material behavior from first principles. These quantities, representing the response of a system's total energy to atomic displacements and lattice deformations, bridge the gap between quantum mechanical descriptions and observable macroscopic properties. However, deriving these derivatives efficiently and accurately from a complex quantum calculation presents a significant theoretical and practical challenge. This article provides a comprehensive overview of the solution: the Hellmann-Feynman theorem and its ecosystem of related concepts. In the first chapter, 'Principles and Mechanisms,' we will delve into the theoretical foundation of the theorem, explore its application within Density Functional Theory, and address crucial practical corrections like Pulay forces. Subsequently, 'Applications and Interdisciplinary Connections' will demonstrate how these computed forces and stresses are the workhorse behind [geometry optimization](@entry_id:151817), [molecular dynamics](@entry_id:147283), and the prediction of mechanical and thermodynamic properties. Finally, the 'Hands-On Practices' chapter offers practical exercises to solidify the theoretical concepts, transforming abstract principles into tangible computational skills.

## Principles and Mechanisms

The ability to calculate forces on atoms and the macroscopic stress tensor within a material is a cornerstone of modern computational materials science. These quantities are the derivatives of the total energy with respect to atomic positions and unit cell deformations, respectively. They provide the gateway to understanding a vast range of physical phenomena, from the equilibrium geometry of molecules and crystals to their vibrational properties, elastic response, and the atomistic pathways of [phase transformations](@entry_id:200819). This chapter elucidates the fundamental principles and practical mechanisms governing the calculation of forces and stresses, centered around the Hellmann-Feynman theorem and its application within the framework of Density Functional Theory (DFT).

### The Hellmann-Feynman Theorem: The Foundational Principle

The theoretical basis for most force calculations in quantum mechanics is the **Hellmann-Feynman theorem**. Let us consider a quantum system described by a Hamiltonian $\hat{H}(\lambda)$ that depends on a continuous parameter $\lambda$, such as an atomic coordinate or a strain component. If $|\Psi(\lambda)\rangle$ is an exact, normalized [eigenstate](@entry_id:202009) of $\hat{H}(\lambda)$ with eigenvalue $E(\lambda)$, then the total energy is given by the expectation value $E(\lambda) = \langle\Psi(\lambda)|\hat{H}(\lambda)|\Psi(\lambda)\rangle$.

The derivative of this energy with respect to the parameter $\lambda$ is found by applying the product rule:
$$
\frac{dE}{d\lambda} = \left\langle \frac{\partial\Psi}{\partial\lambda} \middle| \hat{H} \middle| \Psi \right\rangle + \left\langle \Psi \middle| \frac{\partial\hat{H}}{\partial\lambda} \middle| \Psi \right\rangle + \left\langle \Psi \middle| \hat{H} \middle| \frac{\partial\Psi}{\partial\lambda} \right\rangle
$$
Since $\hat{H}|\Psi\rangle = E|\Psi\rangle$ and the Hamiltonian is Hermitian, we can simplify the first and third terms:
$$
\frac{dE}{d\lambda} = E\left\langle \frac{\partial\Psi}{\partial\lambda} \middle| \Psi \right\rangle + \left\langle \Psi \middle| \frac{\partial\hat{H}}{\partial\lambda} \middle| \Psi \right\rangle + E\left\langle \Psi \middle| \frac{\partial\Psi}{\partial\lambda} \right\rangle
$$
These terms combine to $E \frac{d}{d\lambda}\langle\Psi|\Psi\rangle$. Because the eigenstate is normalized for all values of $\lambda$, its norm is constant, $\langle\Psi|\Psi\rangle = 1$, and thus its derivative is zero. This leaves us with the elegant result known as the Hellmann-Feynman theorem:
$$
\frac{dE}{d\lambda} = \left\langle \Psi(\lambda) \middle| \frac{\partial\hat{H}(\lambda)}{\partial\lambda} \middle| \Psi(\lambda) \right\rangle
$$
This powerful theorem states that to find the change in energy, we do not need to know how the wavefunction changes with the parameter ($\frac{\partial\Psi}{\partial\lambda}$); we only need the expectation value of the explicit derivative of the Hamiltonian operator itself. The force on an ion $I$ along a Cartesian direction $\alpha$, $F_{I\alpha}$, is then simply $-\frac{\partial E}{\partial R_{I\alpha}}$.

In the context of Kohn-Sham DFT, the situation is more nuanced. The ground state is found by minimizing the Kohn-Sham energy functional $E_{KS}[\{\psi_i\}]$ with respect to the orbitals $\{\psi_i\}$, typically through a **Self-Consistent Field (SCF)** procedure. A common misconception is that because the effective Kohn-Sham Hamiltonian $\hat{H}_{KS}$ depends on the electron density $\rho$, which in turn depends on the parameter $\lambda$, the theorem is inapplicable [@problem_id:3456488]. However, it is precisely the **variational nature** of the DFT ground state that salvages the theorem. At convergence, the energy functional is stationary with respect to first-order variations in the electronic degrees of freedom (the orbitals). This [stationarity condition](@entry_id:191085), $\frac{\delta E_{KS}}{\delta\psi_i^*} = 0$, ensures that the implicit dependence of the orbitals on the parameter $\lambda$ does not contribute to the total [energy derivative](@entry_id:268961). Consequently, the [total derivative](@entry_id:137587) $\frac{dE_{KS}}{d\lambda}$ is equal to the partial derivative $\frac{\partial E_{KS}}{\partial\lambda}$, where the latter includes all explicit dependencies on $\lambda$, including those in the operators and in the basis set used to represent the orbitals [@problem_id:3456488].

### Pulay Forces and Stresses: The Consequence of Incomplete Basis Sets

The ideal form of the Hellmann-Feynman theorem holds perfectly if our description of the wavefunction is complete. In any practical calculation, however, we represent the orbitals using a finite, and therefore incomplete, basis set $\{\phi_\mu\}$. If these basis functions themselves depend on the parameter $\lambda$ (e.g., atom-centered orbitals that move with an atom), an additional contribution to the force arises.

Let us model the computed total energy $E_N(R)$ as the sum of a reference energy $E_{\mathrm{ref}}(R)$ (the energy we would get with a complete, parameter-independent basis) and a basis-dependent error term $\Delta_N(R)$ that vanishes only as the basis size $N$ approaches completeness [@problem_id:3456509]. The exact physical force is the derivative of the total computed energy:
$$
F_{\mathrm{exact}}(R) = -\frac{d E_N(R)}{d R} = -\frac{d E_{\mathrm{ref}}(R)}{d R} - \frac{d \Delta_N(R)}{d R}
$$
The first term, $-\frac{d E_{\mathrm{ref}}(R)}{d R}$, corresponds to the pure Hellmann-Feynman force. The second term, $-\frac{d \Delta_N(R)}{d R}$, is the contribution arising from the change in the basis set with the parameter $R$. This correction is known as the **Pulay force**, named after Péter Pulay who first identified it. It is a correction for the fact that the basis set is not "force-free" because the energy has not been minimized with respect to the basis function parameters (e.g., their positions), only with respect to their [linear combination](@entry_id:155091) coefficients [@problem_id:3456488].

The existence of Pulay forces depends on the choice of basis set and the parameter of differentiation.
-   **Atomic Forces**: With a **[plane-wave basis set](@entry_id:204040)**, the basis functions $e^{i(\mathbf{k}+\mathbf{G})\cdot\mathbf{r}}$ do not depend on atomic positions $\mathbf{R}_I$. Therefore, when calculating atomic forces ($\lambda = R_{I\alpha}$), there are no Pulay contributions [@problem_id:3456481]. In contrast, atom-centered [basis sets](@entry_id:164015) (like Gaussian or Slater-type orbitals) move with the atoms, giving rise to significant Pulay forces.
-   **Stress Tensor**: The **stress tensor**, $\sigma_{\alpha\beta} = \frac{1}{\Omega} \frac{\partial E}{\partial \epsilon_{\alpha\beta}}$, involves differentiation with respect to strain $\epsilon_{\alpha\beta}$. Strain deforms the unit cell, which in turn alters the [reciprocal lattice vectors](@entry_id:263351) $\mathbf{G}$. This means that even a [plane-wave basis set](@entry_id:204040) depends on strain. Consequently, calculating the stress tensor with a finite [plane-wave basis](@entry_id:140187) (i.e., a finite [kinetic energy cutoff](@entry_id:186065)) requires the inclusion of a **Pulay stress** correction [@problem_id:3456481].

A clear illustration of this effect can be seen in real-space grid methods [@problem_id:3456468]. If an integral for the energy is approximated by a sum over grid points that are fixed in [fractional coordinates](@entry_id:203215), these grid points move in real space as the cell is strained. The calculated stress via finite differences of the discretized energy will differ from the ideal continuum stress. This difference is a direct analogue of the Pulay stress, arising because the numerical quadrature scheme (the "basis") depends on the strain parameter.

### Case Studies in Force and Stress Calculation

The general principles can be made concrete by examining how forces and stresses arise from specific terms in the DFT Hamiltonian and its common extensions.

#### Contribution from Non-Local Pseudopotentials

Modern [pseudopotentials](@entry_id:170389) replace the strong core potential and the core electrons, and typically include a non-local part, $\hat{V}_{NL}$, to accurately describe the valence [electron scattering](@entry_id:159023). A common form is the separable Kleinman-Bylander projector, e.g., $\hat{V}_{\mathrm{NL}}(R) = |p(R)\rangle D \langle p(R)|$, where the projector function $|p(R)\rangle$ is centered on an ion and thus depends on its position $R$ [@problem_id:3456467].

The force contribution from this term is a direct application of the Hellmann-Feynman theorem, assuming a parameter-independent basis set and a variationally optimized electronic state. The force is the [expectation value](@entry_id:150961) of the negative derivative of the operator:
$$
F = - \left\langle \psi \left| \frac{\partial \hat{V}_{\mathrm{NL}}(R)}{\partial R} \right| \psi \right\rangle
$$
Differentiating the operator gives:
$$
\frac{\partial \hat{V}_{\mathrm{NL}}(R)}{\partial R} = D \left[ \left( \frac{\partial |p(R)\rangle}{\partial R} \right) \langle p(R)| + |p(R)\rangle \left( \frac{\partial \langle p(R)|}{\partial R} \right) \right]
$$
This leads to a force expression involving overlaps of the wavefunction $|\psi\rangle$ with the projector $|p(R)\rangle$ and its derivative $|\frac{\partial p(R)}{\partial R}\rangle$. For a system with real wavefunctions and projectors, this simplifies to $F = -2D \langle \psi | p \rangle \langle \psi | p' \rangle$, providing a direct and computable formula [@problem_id:3456467]. This demonstrates how forces arise from any term in the Hamiltonian with explicit dependence on atomic coordinates.

#### Additive Energy Corrections: DFT+U and DFT-D

Many modern DFT calculations include semi-empirical corrections to account for physical effects that are poorly described by standard exchange-correlation functionals, such as van der Waals (dispersion) interactions or strong electronic correlation in d- or [f-electron systems](@entry_id:139022). If the total energy is written as $E_{\mathrm{total}} = E_{\mathrm{KS}} + E_{\mathrm{corr}}$, the total force and stress are simply the sum of the contributions from each term: $\mathbf{F}_{\mathrm{total}} = \mathbf{F}_{\mathrm{KS}} + \mathbf{F}_{\mathrm{corr}}$ and $\boldsymbol{\sigma}_{\mathrm{total}} = \boldsymbol{\sigma}_{\mathrm{KS}} + \boldsymbol{\sigma}_{\mathrm{corr}}$.