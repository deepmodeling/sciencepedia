## Introduction
The accurate prediction of electronic excited states is fundamental to understanding a vast range of phenomena in chemistry and physics, from photosynthesis and vision to the design of new materials for solar energy and display technologies. The Algebraic Diagrammatic Construction (ADC) schemes represent a family of powerful, reliable, and systematically improvable quantum chemical methods designed for this purpose. These methods offer a compelling balance between computational efficiency and accuracy, providing a robust alternative to other popular approaches.

This article addresses the need for a comprehensive yet accessible guide to the ADC formalism. It bridges the gap between abstract many-body theory and practical application, equipping you with the knowledge to use and interpret ADC calculations effectively. By navigating the theoretical underpinnings and diverse applications, you will gain a deep appreciation for the versatility and predictive power of the ADC framework.

You will begin in the first chapter, **Principles and Mechanisms**, by exploring the theoretical foundations of ADC, tracing its origins from the polarization propagator and establishing its practical form through the Intermediate State Representation (ISR). The second chapter, **Applications and Interdisciplinary Connections**, showcases the method's broad utility, from simulating complex spectra to modeling challenging chemical systems like diradicals and heavy elements, and highlights its connections to other areas like TDDFT and condensed matter physics. Finally, the **Hands-On Practices** section will allow you to solidify your understanding by working through problems that apply these core concepts to tangible chemical scenarios.

## Principles and Mechanisms

The Algebraic Diagrammatic Construction (ADC) schemes for the polarization propagator represent a powerful and systematic family of methods for computing the electronic excited states of molecular systems. Having introduced the general context, this chapter delves into the fundamental principles and mechanisms that underpin the ADC formalism. We will begin by establishing the formal connection between ADC and many-body Green's functions, proceed to the practical formulation known as the Intermediate State Representation (ISR), explore the structural properties of the resulting equations, discuss the interpretation and practical aspects of ADC calculations, and conclude with key computational and numerical considerations.

### The Propagator Foundation of ADC

The theoretical origin of the ADC methods lies in the framework of many-body Green's functions, or propagators. A propagator describes the evolution of a quantum system after a particular perturbation. Different types of excitations are associated with different propagators.

The primary object of interest for describing electronically excited states—transitions within the same electron number ($N$) sector—is the **polarization propagator**, also known as the density-density correlation function or the two-point linear response function. In its Lehmann or spectral representation, the polarization propagator's poles (singularities) correspond precisely to the system's exact neutral excitation energies, $\Omega_f = E_f^N - E_0^N$. The residues at these poles are related to the transition moments between the ground state $|\Psi_0^N\rangle$ and the excited states $|\Psi_f^N\rangle$.

In contrast, transitions involving a change in electron number, such as ionization and electron attachment, are described by the **one-particle Green's function**, or electron propagator, $\mathbf{G}(\omega)$. Its Lehmann representation reveals two distinct sets of poles [@problem_id:2761030]:
1.  Poles at energies $\omega = E_r^{N+1} - E_0^N$, which correspond to the **electron affinities** (EAs) of the system.
2.  Poles at energies $\omega = -(E_s^{N-1} - E_0^N)$, which are the negative of the **ionization potentials** (IPs).

It is crucial to recognize that the polarization propagator and the electron propagator describe fundamentally different physical processes. Consequently, the ADC methods derived from them target distinct physical quantities. The standard ADC schemes for excited states, such as ADC(1), ADC(2), and ADC(3), are approximations to the polarization propagator and yield neutral excitation energies. The corresponding methods for charged excitations are denoted IP-ADC($n$) and EA-ADC($n$) and are approximations to the electron propagator. The spectra of these two classes of methods are not expected to coincide [@problem_id:2761030].

The core idea of the Algebraic Diagrammatic Construction, as conceived by Jochen Schirmer, is to formulate an approximate spectral representation of the exact propagator. This is achieved by constructing a frequency-independent, effective Hamiltonian matrix, $\mathbf{M}$, whose spectral decomposition (i.e., its eigenvalues and eigenvectors) is designed to reproduce the diagrammatic perturbation expansion of the exact propagator up to a specific order, $n$, in the electron-electron interaction. This procedure transforms the complex, frequency-dependent problem of finding the poles of a propagator into a standard, frequency-independent Hermitian eigenvalue problem.

### The Intermediate State Representation (ISR)

The practical realization of the ADC framework is the **Intermediate State Representation (ISR)**. This representation translates the abstract propagator formalism into a concrete matrix eigenvalue problem suitable for computational implementation. The foundation of the ISR is a basis of excited configuration state functions, termed **intermediate states** (IS), which are constructed by applying excitation operators to the reference ground state, typically the Hartree-Fock (HF) determinant $|\Phi_0\rangle$.

The choice of intermediate states depends on the target propagator.
-   For **neutral excitations** (polarization propagator), the IS manifold is built from particle-hole excitations. The lowest-order space consists of singly-excited configurations ($1p1h$), denoted $|\Phi_i^a\rangle$. Higher-order spaces include doubly-excited configurations ($2p2h$), $|\Phi_{ij}^{ab}\rangle$, and so on.
-   For **ionization potentials** (IP-ADC), the target states are in the $(N-1)$-electron space. The IS manifold is therefore constructed from hole and particle-hole configurations relative to the $N$-electron reference. The simplest states are single-hole ($1h$) configurations, $|\Phi_i\rangle$, followed by two-hole-one-particle ($2h1p$) configurations, $|\Phi_{ij}^a\rangle$, etc.

The configuration spaces for neutral and charged excitations are fundamentally different, spanning different sectors of the Fock space [@problem_id:2761030].

In the ISR, the ADC equations take the form of a Hermitian eigenvalue problem:
$$ \mathbf{M} \mathbf{Y}_k = \Omega_k \mathbf{Y}_k $$
Here, $\mathbf{M}$ is the effective ADC Hamiltonian matrix represented in the basis of orthonormalized intermediate states. $\Omega_k$ are the computed excitation energies (approximations to the propagator poles), and the eigenvectors $\mathbf{Y}_k$ are the so-called effective transition moments, which contain the amplitudes of the various intermediate states contributing to the final excited state. Because $\mathbf{M}$ is constructed to be Hermitian (or real-symmetric for real orbital bases), its eigenvalues $\Omega_k$ are guaranteed to be real. This means that standard ADC methods describe stable excited states with infinite lifetimes (zero linewidths). Capturing finite-lifetime effects, such as those in resonance phenomena, requires extensions to a non-Hermitian framework [@problem_id:2761030] [@problem_id:2761029].

### Properties and Hierarchy of the ADC Matrix

The structure of the ADC matrix $\mathbf{M}$ is dictated by the underlying physics and the perturbative order of the method. This structure imparts key properties to the resulting solutions.

#### Symmetry and Selection Rules

For a molecule with spatial symmetry and in the absence of spin-orbit coupling, the electronic Hamiltonian commutes with the total spin operators ($\hat{S}^2$, $\hat{S}_z$) and the point group symmetry operators. The ADC effective Hamiltonian $\mathbf{M}$ inherits these symmetries.
-   **Spin Symmetry**: When constructed in a basis of spin-adapted configurations (e.g., pure singlet and triplet states), the ADC matrix becomes block-diagonal with respect to the total spin [quantum number](@entry_id:148529) $S$ [@problem_id:2761014]. This allows for the separate calculation of singlet and triplet excited state manifolds. The energy difference between singlet and triplet states arising from the same spatial orbital transition stems from the structure of the two-electron interaction. In the singles-singles block of the ADC matrix, the matrix elements for a singlet state include a direct Coulomb-type term, which is absent for the corresponding triplet state. This term is responsible for raising the singlet state's energy relative to the triplet, leading to the characteristic positive singlet-triplet gap for most excitations [@problem_id:2761014].
-   **Spatial Symmetry**: The ADC matrix also block-diagonalizes according to the irreducible representations (irreps) of the molecular point group. A matrix element between intermediate states belonging to different irreps is strictly zero. Electron correlation does not mix states of different spatial symmetry [@problem_id:2761014].
-   **Transition Properties**: These symmetries give rise to selection rules. The electric dipole operator is spin-independent, meaning it cannot connect states of different spin multiplicity. Therefore, in the absence of spin-orbit coupling, transitions between the singlet ground state and any triplet excited state are strictly forbidden; their **oscillator strengths** are identically zero [@problem_id:2761014]. Similarly, a transition is spatially allowed only if the direct product of the irreps of the initial state, the final state, and the dipole operator contains the totally symmetric irrep.

#### The ADC($n$) Hierarchy and Relation to Other Methods

The ADC methods form a hierarchy of improving accuracy based on the order $n$ to which the propagator is reproduced.
-   **ADC(1)**: This is the simplest level. The ADC(1) matrix is simply the Hamiltonian represented in the space of single excitations. This method is identical to Configuration Interaction Singles (CIS) and to the Tamm-Dancoff Approximation (TDA) of Time-Dependent Hartree-Fock (TDHF) [@problem_id:2761023].
-   **ADC(2)**: This is the most widely used ADC variant, providing a good balance between accuracy and cost. It is correct through second order in perturbation theory for excitation energies. ADC(2) is considered "equivalent in content" to the Second-Order Polarization Propagator Approximation (SOPPA), meaning they are both derived from the second-order expansion of the polarization propagator but employ different computational strategies to extract the excitation energies. A key feature of ADC(2) and other propagator methods is that they yield **size-intensive** excitation energies, a crucial property for applications to large systems [@problem_id:2761023]. The relationship with second-order coupled-cluster theory is subtle: the stricter "ADC(2)-s" variant is algebraically equivalent to the CC2 method, while the standard, more accurate "ADC(2)-x" variant is not [@problem_id:2761023].
-   **ADC(3)**: This method is correct through third order. For states dominated by single excitations, ADC(3) provides results that are numerically very close to those from the more computationally expensive Equation-of-Motion Coupled Cluster with Singles and Doubles (EOM-CCSD) method, often considered a benchmark for this class of states [@problem_id:2761023].

A defining advantage of the entire ADC hierarchy over methods like TDHF/RPA is its formulation as a Hermitian eigenvalue problem, which guarantees real excitation energies and avoids potential numerical instabilities associated with the non-Hermitian structure of TDHF/RPA [@problem_id:2761023].

### Practical Application and Interpretation

Beyond computing excitation energies, ADC provides a wealth of information for characterizing excited states. A correct interpretation of the output is vital for a meaningful chemical analysis.

#### Characterizing Excited States with Diagnostics

The eigenvector $\mathbf{Y}_k$ for a given state contains the amplitudes of the constituent intermediate states. Analyzing these amplitudes provides deep insight into the nature of the excitation.
-   **Spectroscopic Factor ($Z_k$)**: For a neutral excitation, the sum of the squared amplitudes of all $1p1h$ configurations is the one-particle-one-hole character, or **spectroscopic factor**, $Z_k$. Since the eigenvector is normalized to one, $Z_k$ ranges from 0 to 1. A state with $Z_k \approx 1$ is a "clean" single excitation, well-described by methods like ADC(2). A state with a significantly lower $Z_k$ has substantial multi-excitation (e.g., $2p2h$) character. Such states are often poorly described at lower orders of theory [@problem_id:2761019].
-   **Method Spread**: The difference in excitation energy for a state computed at two different levels, e.g., $\Delta E_k = E_k^{\text{ADC(3)}} - E_k^{\text{ADC(2)}}$, serves as a powerful diagnostic. A small $|\Delta E_k|$ suggests the perturbative series is converging well and that the ADC(2) result is likely reliable. Conversely, a large $|\Delta E_k|$ signals poor convergence and indicates that the ADC(2) result should be treated with caution.

For instance, consider a hypothetical state with a low spectroscopic factor ($Z_k=0.58$) and a large method spread ($\Delta E_k = 0.70$ eV). This combination strongly indicates substantial double-excitation and/or charge-transfer character, for which the ADC(2) description is qualitatively unreliable. The magnitude of the spread itself serves as a reasonable estimate of the uncertainty in the ADC(2) energy. In contrast, a state with a high spectroscopic factor ($Z_k=0.92$) and a small spread ($\Delta E_k=0.18$ eV) can be confidently characterized as a predominantly single-excitation state for which ADC(2) is reliable to within approximately 0.2 eV [@problem_id:2761019]. For IP-ADC, the eigenvector components are directly related to **spectroscopic amplitudes**, and their total norm is the spectroscopic factor, which measures the probability of describing the ionization process as the removal of a single electron from a specific ground-state orbital [@problem_id:2761030].

#### Basis Set Effects: The Role of Diffuse Functions

The accuracy of any quantum chemical calculation is critically dependent on the quality of the one-particle basis set. For excited states, this dependency is highly state-specific. According to the Hylleraas-Undheim-MacDonald theorem, the eigenvalues of the ADC matrix in a truncated basis set are upper bounds to the complete-basis-set energies. Thus, expanding the basis set can only lower the computed excitation energies. The magnitude of this effect varies dramatically with the nature of the state.

We can classify low-lying excitations into three main types:
1.  **Valence states**: Excitations between orbitals that are spatially compact and localized on the molecule (e.g., $n \to \pi^*$, $\pi \to \pi^*$).
2.  **Rydberg states**: Excitations where an electron is promoted to a very diffuse, high-principal-quantum-number orbital that weakly orbits a cationic molecular core.
3.  **Charge-Transfer (CT) states**: Excitations in a multicomponent system (e.g., a donor-acceptor pair) where an electron moves from one component to another over a significant distance.

Valence states are reasonably well-described by standard correlation-consistent basis sets (e.g., cc-pVDZ). However, Rydberg and CT states have spatially extended electron distributions that cannot be accurately represented without the inclusion of **diffuse functions** (functions with very small Gaussian exponents) in the basis set. A basis lacking these functions imposes an artificial spatial confinement on the excited electron, leading to a large, non-physical kinetic energy penalty and a severe overestimation of the excitation energy. Adding diffuse functions (e.g., moving from cc-pVDZ to aug-cc-pVDZ) remedies this fundamental deficiency, causing a dramatic and essential reduction in the computed energies for Rydberg and CT states. This stabilization is often so large that it can change the energetic ordering of the states. Subsequent increases in basis set cardinality (e.g., aug-cc-pVDZ to aug-cc-pVTZ) lead to smaller, more routine refinements for all state types [@problem_id:2761024].

#### Core-Level Excitations: The Core-Valence Separation (CVS)

Computing core-level excitations (e.g., from a 1s orbital) with ADC presents a challenge: these high-energy states are embedded in a dense quasi-continuum of valence-excited states. The **Core-Valence Separation (CVS)** approximation offers a practical solution. The ADC matrix is partitioned into a core-excited block, a valence-excited block, and the coupling between them. CVS consists of simply neglecting this coupling, block-diagonalizing the matrix and solving the eigenvalue problem only within the small core-excited subspace [@problem_id:2761017].

Using non-degenerate perturbation theory, we can analyze the error introduced by this approximation. The leading error in a core excitation energy is second-order in the core-valence coupling strength $V_{cv}$ and scales as $|V_{cv}|^2/\Delta$, where $\Delta$ is the energy gap between the core and valence manifolds. Since core states lie far above valence states, this correction is always positive, meaning CVS slightly underestimates the true core excitation energy due to the neglect of level repulsion from the lower-lying valence states. For a typical case with a core excitation at $400$ eV, a valence manifold starting at $10$ eV, and a coupling of $3$ eV, this second-order correction is a mere $+0.023$ eV, demonstrating the high accuracy of the CVS approximation. However, the error in properties like oscillator strengths is first-order in the coupling, scaling as $|V_{cv}|/\Delta$, and can be more significant [@problem_id:2761017].

### Computational and Numerical Aspects

Efficient and robust implementation of ADC methods requires attention to computational scaling and numerical stability.

#### Computational Cost and the RI/DF Approximation

The computational cost of ADC methods is a significant consideration. The most expensive steps often involve contractions of the two-electron repulsion integrals (ERIs) with trial vectors. For example, a key contraction in ADC(2) involves the term $\Sigma_{abij} \leftarrow \sum_{cd} (ab|cd) R_{cdij}$, where $i,j$ are occupied orbital indices and $a,b,c,d$ are virtual orbital indices. The computational cost of this step scales as $O(n_o^2 n_v^4)$, where $n_o$ is the number of occupied orbitals and $n_v$ is the number of virtual orbitals. This steep scaling severely limits the applicability of the method to larger systems.

To alleviate this bottleneck, the **Resolution of the Identity (RI)** or **Density Fitting (DF)** approximation is commonly employed. The four-center ERIs are factorized into products of three-center integrals: $(ab|cd) \approx \sum_{P} B_{ab}^{P} B_{cd}^{P}$, where $P$ indexes a compact auxiliary basis set of size $n_{\text{aux}}$. This allows the expensive $O(n_o^2 n_v^4)$ step to be broken into two more manageable steps:
1.  Form an intermediate: $X_{Pij} = \sum_{cd} B_{cd}^{P} R_{cdij}$ with cost $O(n_{\text{aux}} n_o^2 n_v^2)$.
2.  Contract the intermediate: $\Sigma_{abij} \leftarrow \sum_{P} B_{ab}^{P} X_{Pij}$ with cost $O(n_{\text{aux}} n_o^2 n_v^2)$.

The total cost now scales as $O(n_{\text{aux}} n_o^2 n_v^2)$. For a typical system where $n_v \gg n_o$ and $n_{\text{aux}} \approx 3(n_o+n_v)$, the speedup factor $S = \frac{n_v^2}{2 n_{\text{aux}}}$ can easily be on the order of 50-100, making RI-ADC a dramatically more efficient method [@problem_id:2761015].

#### Numerical Stability and Verification

The large ADC eigenvalue problem is solved iteratively, typically using a **Davidson-type algorithm**. The convergence of this algorithm is monitored by the norm of the residual vector, $\|r_k\|$, for each sought-after state. A stringent convergence threshold on $\|r_k\|$ ensures an even more accurate result for the eigenvalue, as the error in the eigenvalue scales quadratically with the residual norm for a well-separated state [@problem_id:2761025].

Numerical stability can be a concern, particularly when using large, diffuse basis sets that may contain near-linear dependencies. Such dependencies can lead to ill-conditioning of the ADC matrix and cause the iterative solver to produce small, unphysical imaginary components for the eigenvalues, even though the matrix is formally Hermitian. Standard remedies include tighter re-orthogonalization of the solver's subspace vectors or removing the linear dependencies from the basis set [@problem_id:2761025].

Finally, a correct implementation of ADC must satisfy several fundamental physical principles, which can be used as rigorous unit tests [@problem_id:2761029]:
-   **Non-interacting limit**: In the absence of electron-electron interaction, ADC($n$) must exactly reproduce the single-particle excitation energies (HF orbital energy differences).
-   **Separability**: For two non-interacting systems, the excitation spectrum of the combined system must be the union of the individual monomer spectra. This property, a consequence of size-intensivity, should hold up to the numerical precision of the calculation [@problem_id:2761025] [@problem_id:2761029].
-   **Hermiticity**: The ISR ADC matrix must be constructed to be exactly Hermitian, a checkable property [@problem_id:2761029].
-   **Sum Rules**: While not satisfied exactly by ADC($n$), the Thomas-Reiche-Kuhn (TRK) sum rule, which states that the sum of all oscillator strengths equals the number of electrons, serves as a powerful validation check. In a finite basis, the computed sum should approach the total number of electrons from below as the basis and energy range increase [@problem_id:2761025].

By understanding these principles, from the abstract propagator origins to the concrete details of implementation and interpretation, one can effectively leverage the ADC methodology as a robust and insightful tool for computational spectroscopy.