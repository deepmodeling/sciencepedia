## Introduction
The accurate simulation of atomic and molecular systems is a cornerstone of modern science, but it presents a fundamental dilemma: the high accuracy of *[ab initio](@entry_id:203622)* quantum mechanical methods comes at a prohibitive computational cost, while fast [classical force fields](@entry_id:747367) often lack the necessary physical fidelity. Machine learning potentials (MLPs) have emerged as a revolutionary solution to this accuracy-versus-speed trade-off, enabling simulations with the predictive power of quantum mechanics at a fraction of the cost. These models learn the complex, high-dimensional relationship between atomic positions and potential energy directly from *ab initio* data, opening the door to simulations of unprecedented scale and complexity. This article provides a graduate-level introduction to the theory, application, and practice of building and using machine learning potentials.

Across three chapters, we will journey from foundational theory to practical application. The first chapter, **Principles and Mechanisms**, establishes the theoretical bedrock of MLPs. We will define the target quantity—the Born-Oppenheimer potential energy surface—and explore the critical roles of physical symmetries and the locality principle. You will learn about the key building blocks, from handcrafted descriptors like ACSF and SOAP to modern end-to-end equivariant architectures. The second chapter, **Applications and Interdisciplinary Connections**, shifts focus to the deployment of MLPs in scientific discovery. We will cover advanced training paradigms like [active learning](@entry_id:157812), their use in [molecular simulations](@entry_id:182701) to compute thermodynamic properties and free energies, and their integration into sophisticated multiscale models. Finally, the third chapter, **Hands-On Practices**, will guide you through practical coding exercises to solidify your understanding of how to implement descriptors, train a simple potential, and derive the analytical forces essential for [molecular dynamics](@entry_id:147283). By the end, you will have a comprehensive understanding of how MLPs are constructed, validated, and applied to solve cutting-edge problems in chemistry, materials science, and beyond.

## Principles and Mechanisms

This chapter delves into the fundamental principles that govern the construction of machine learning potentials (MLPs) and the specific mechanisms through which these principles are realized in modern architectures. We will begin by precisely defining the target quantity that MLPs aim to approximate—the Born-Oppenheimer potential energy surface. We will then explore the indispensable roles of physical symmetries and the locality principle in making the learning problem tractable. Subsequently, we will examine the key mechanisms, including invariant and equivariant descriptors and network architectures, that translate these principles into practical, predictive models. Finally, we will address crucial practical considerations, such as the relationship between energy and forces, the implementation of interaction cutoffs, the inherent limitations concerning long-range physics, and the quantification of [model uncertainty](@entry_id:265539).

### The Target: The Born-Oppenheimer Potential Energy Surface

The central task of an [interatomic potential](@entry_id:155887) is to provide the energy of a system of atoms as a function of their nuclear positions, which in turn dictates the forces governing their motion. In the context of quantum mechanics, this potential energy landscape is rigorously defined through the **Born-Oppenheimer (BO) approximation** [@problem_id:2784636]. This approximation is justified by the large disparity between the mass of a nucleus ($m_n$) and the mass of an electron ($m_e$), which implies a vast separation of their respective timescales. Electrons adapt almost instantaneously to any change in the positions of the much slower-moving nuclei.

This separation allows us to conceptually "clamp" the nuclei at a fixed configuration $\mathbf{R} = \{\mathbf{r}_1, \dots, \mathbf{r}_N\}$ and solve for the electronic structure independently. This is accomplished by solving the time-independent electronic Schrödinger equation:
$$
\hat{H}_{\mathrm{el}}(\mathbf{r}; \mathbf{R}) \psi_k(\mathbf{r}; \mathbf{R}) = E_{\mathrm{el},k}(\mathbf{R}) \psi_k(\mathbf{r}; \mathbf{R})
$$
where the electronic Hamiltonian $\hat{H}_{\mathrm{el}}$ includes the kinetic energy of the electrons and all electron-electron and electron-[nuclear potential](@entry_id:752727) energy terms. Solving this equation yields a set of electronic [energy eigenvalues](@entry_id:144381) $E_{\mathrm{el},k}(\mathbf{R})$ and corresponding electronic wavefunctions $\psi_k$ for each electronic state $k$.

The **Born-Oppenheimer Potential Energy Surface (PES)**, denoted $V(\mathbf{R})$, is the [effective potential](@entry_id:142581) governing the motion of the nuclei. For simulations concerned with ground-state chemistry, this corresponds to the lowest-energy electronic solution ($k=0$). The PES is constructed by taking the ground-state electronic eigenvalue and adding the classical nuclear-nuclear repulsion energy, $V_{\mathrm{nn}}(\mathbf{R})$, which was treated as a constant in the electronic problem:
$$
V(\mathbf{R}) = E_{\mathrm{el},0}(\mathbf{R}) + V_{\mathrm{nn}}(\mathbf{R})
$$
This quantity, $V(\mathbf{R})$, which is a scalar function dependent only on the nuclear coordinates $\mathbf{R}$, is the primary target for a machine learning potential.

It is crucial to distinguish $V(\mathbf{R})$ from other related quantities [@problem_id:2784636]. Many electronic structure codes report an "electronic energy" that corresponds only to the eigenvalue $E_{\mathrm{el},0}(\mathbf{R})$, omitting the $V_{\mathrm{nn}}(\mathbf{R})$ term. In such cases, one must explicitly add the nuclear repulsion to obtain the [total potential energy](@entry_id:185512). Furthermore, the BO-PES is a purely mechanical potential at zero Kelvin and must not be confused with thermodynamic quantities like the Helmholtz free energy, $F(T, V, N)$. The free energy is a macroscopic property that depends on temperature and includes contributions from the kinetic energy of the nuclei and the associated configurational and vibrational entropies. The entire BO framework relies on the assumption that the system remains on a single electronic surface (typically the ground state) throughout its dynamics, an assumption known as the **[adiabatic approximation](@entry_id:143074)**. This neglects non-adiabatic couplings between electronic states, which can become important in [photochemistry](@entry_id:140933) or at [conical intersections](@entry_id:191929).

### Fundamental Symmetries of Interatomic Potentials

The laws of physics impose strict symmetry constraints on the form of any valid [potential energy surface](@entry_id:147441). An MLP architecture must respect these symmetries to be physically meaningful and to generalize correctly beyond its training data.

#### Invariance and Equivariance

Symmetry transformations affect [scalar and vector quantities](@entry_id:170784) differently.
- A **scalar** quantity, such as the total potential energy $E$, must be **invariant** under a symmetry operation. This means its value does not change when the system is transformed.
- A **vector** quantity, such as the force $\mathbf{F}_i$ on an atom $i$, must be **equivariant** under a symmetry operation. This means the vector itself transforms in a specific, predictable way that is coupled to the transformation of the system's coordinates [@problem_id:2784640].

#### Euclidean Symmetries

The [homogeneity and isotropy](@entry_id:158336) of free space dictate that the potential energy of an isolated system must be invariant to rigid-body motions: translations and rotations.
- **Translational Invariance**: Shifting the entire system by a constant vector $\mathbf{t}$ does not change its internal geometry, and therefore cannot change its potential energy. Formally, for a system with coordinates $\{\mathbf{r}_i\}$, the energy $E$ must satisfy $E(\{\mathbf{r}_i + \mathbf{t}\}) = E(\{\mathbf{r}_i\})$. The corresponding forces are also invariant to translation: $\mathbf{F}_i(\{\mathbf{r}_j + \mathbf{t}\}) = \mathbf{F}_i(\{\mathbf{r}_j\})$.
- **Rotational Invariance**: Rotating the entire system by an [orthogonal matrix](@entry_id:137889) $R \in \mathrm{O}(3)$ also leaves the potential energy unchanged: $E(\{R\mathbf{r}_i\}) = E(\{\mathbf{r}_i\})$. The forces, being vectors, must rotate along with the system. This is the property of equivariance: $\mathbf{F}_i(\{R\mathbf{r}_j\}) = R\mathbf{F}_i(\{\mathbf{r}_j\})$. A common mistake is to assume forces are also invariant; they are not. For example, rotating a diatomic molecule aligned with the x-axis to be aligned with the y-axis will cause the force vectors, which point along the bond, to rotate by 90 degrees as well [@problem_id:2784640].

#### Permutational Symmetry

The [principle of indistinguishability](@entry_id:150314) of [identical particles](@entry_id:153194) in quantum mechanics requires that the potential energy be invariant to the permutation of the labels of any two atoms of the same chemical species. If $\pi$ is a permutation that swaps the indices of two hydrogen atoms in a water molecule, the energy must satisfy $E(\{\mathbf{r}_{\pi(i)}\}) = E(\{\mathbf{r}_i\})$. The set of force vectors must transform consistently, meaning the force vector that was on atom $i$ is now on atom $\pi(i)$. Formally, $\mathbf{F}_{\pi(i)}(\{\mathbf{r}_{\pi(j)}\}) = \mathbf{F}_i(\{\mathbf{r}_j\})$ [@problem_id:2784640]. This symmetry applies strictly to [identical particles](@entry_id:153194); swapping atoms of different chemical elements, such as Na and Cl in sodium chloride, results in a physically distinct configuration with a different energy.

### The Locality Principle and Energy Decomposition

Modeling the full, high-dimensional [potential energy surface](@entry_id:147441) $V(\mathbf{R})$ for a system of many atoms is a formidable challenge. A key breakthrough in making this problem tractable is the **locality assumption**: the idea that the [total potential energy](@entry_id:185512) can be well approximated as a sum of individual atomic energy contributions, where each contribution depends only on the local chemical environment of that atom.

#### The Locality Assumption

The [total potential energy](@entry_id:185512) is decomposed as:
$$
E(\mathbf{R}, \mathbf{Z}) \approx \sum_{i=1}^{N} \varepsilon_i
$$
Here, $\varepsilon_i$ is the energy assigned to atom $i$, and it is a function only of the positions and identities of neighboring atoms within a finite **[cutoff radius](@entry_id:136708)**, $r_c$, of atom $i$ [@problem_id:2648636] [@problem_id:2784673]. This atom-centered decomposition is a foundational concept in many successful MLP architectures.

#### Justification: The Nearsightedness of Electronic Matter

This locality assumption is not merely a convenient heuristic; it has a deep physical justification in the **[principle of nearsightedness](@entry_id:165063)** of electronic matter, articulated by Walter Kohn [@problem_id:2648636]. This principle states that for a fixed chemical potential, local changes in the external potential (such as moving a single atom) have a negligible effect on electronic properties at distant locations.

The mathematical basis for this lies in the decay properties of the [one-body density matrix](@entry_id:161726), $\rho(\mathbf{r}, \mathbf{r}')$.
- In **insulators and semiconductors**, which are systems with a non-zero [electronic band gap](@entry_id:267916), it has been rigorously proven that the density matrix decays exponentially with distance: $|\rho(\mathbf{r}, \mathbf{r}')| \sim \exp(-\gamma |\mathbf{r}-\mathbf{r}'|)$. This rapid decay provides a strong justification for the finite-cutoff approximation, as the influence of distant atoms is exponentially suppressed.
- In **metals at zero temperature**, the situation is more complex. The absence of a band gap leads to a much slower, [power-law decay](@entry_id:262227) of the [density matrix](@entry_id:139892), often accompanied by Friedel oscillations. This implies that perturbations can have very long-range quantum mechanical effects, making a strict finite-cutoff approximation less accurate.
- However, at any **finite temperature ($T > 0$ K)**, thermal smearing of the electronic occupations via the Fermi-Dirac distribution restores the [exponential decay](@entry_id:136762) of the density matrix, even in metals. This makes the locality assumption more justifiable for metallic systems in simulations run at realistic temperatures.

#### Extensivity as a Consequence

A direct and powerful consequence of combining the energy decomposition with a finite cutoff is that the resulting potential is inherently **extensive** or **size-consistent** [@problem_id:2784673]. Consider two non-interacting subsystems, A and B, separated by a distance greater than the [cutoff radius](@entry_id:136708) $r_c$. According to the locality assumption, the local environment of any atom in subsystem A is completely unaffected by the presence of B, and vice-versa. Therefore, the atomic energy contributions $\varepsilon_i$ for atoms in A are the same as if A were isolated. The total energy of the combined system is simply the sum of the energies of the isolated subsystems: $E(A \cup B) = E(A) + E(B)$. This physically essential property is thus built into the architecture by construction.

### Building Blocks: Descriptors for Atomic Environments

To implement the locality principle, we need a way to represent the [local atomic environment](@entry_id:181716) of an atom $i$ as an input for a machine learning model. This representation, known as a **descriptor** or **fingerprint**, must itself be invariant to translation, rotation, and permutation of identical neighbors.

#### Atom-Centered Symmetry Functions (Behler-Parrinello)

One of the earliest and most influential approaches is the use of atom-centered **[symmetry functions](@entry_id:177113)**, as introduced by Behler and Parrinello [@problem_id:2784613]. These are handcrafted functions of neighbor positions that are explicitly designed to be invariant. They are typically divided into two types:

- **Radial Symmetry Functions ($G^2$):** These probe the radial distribution of neighboring atoms. A common form is a sum of Gaussians centered at various distances $R_s$, weighted by a smooth cutoff function $f_c(r)$:
  $$
  G^2_i = \sum_{j \ne i} \exp\left(-\eta\,(R_{ij}-R_s)^2\right)\, f_c(R_{ij})
  $$
  Here, $R_{ij}$ is the distance between atoms $i$ and $j$, while $\eta$ and $R_s$ are tunable parameters that control the width and center of the radial probe, respectively. By using a set of these functions with different parameters, one can resolve the positions of neighbor shells.

- **Angular Symmetry Functions ($G^4$):** These probe the angular arrangement of neighbors and are functions of triplets of atoms $(i, j, k)$. A general form is:
  $$
  G^4_i = 2^{1-\zeta} \sum_{\substack{j \ne i \\ k>j,\, k \ne i}} \left(1+\lambda \cos \theta_{ijk}\right)^{\zeta}\, \exp\left(-\eta\,[R_{ij}^2+R_{ik}^2+R_{jk}^2]\right)\, f_c(R_{ij})\, f_c(R_{ik})
  $$
  where $\theta_{ijk}$ is the angle centered at atom $i$. The parameters $\lambda \in \{+1, -1\}$ and $\zeta \ge 1$ control the shape of the [angular resolution](@entry_id:159247), while $\eta$ provides radial weighting. The sum over unique pairs of neighbors $(j, k)$ ensures the function is invariant to their permutation.

The collection of values from a set of radial and angular [symmetry functions](@entry_id:177113) with different parameters forms a feature vector $\mathbf{G}_i$ that uniquely describes the environment of atom $i$ while respecting all required symmetries.

#### The Smooth Overlap of Atomic Positions (SOAP)

An alternative and powerful descriptor is the **Smooth Overlap of Atomic Positions (SOAP)** [@problem_id:2784653]. Instead of handcrafted functions, SOAP builds a representation from a more abstract, continuous field. The process involves three steps:

1.  **Construct a Neighbor Density:** A continuous "neighbor density" field $\rho(\mathbf{r})$ is created around a central atom by placing a Gaussian function at the position $\mathbf{R}_i$ of each neighbor and summing them up:
    $$
    \rho(\mathbf{r}) = \sum_i f_c(|\mathbf{R}_i|)\, \left(2\pi \sigma^2\right)^{-3/2} \exp\left(-\dfrac{\|\mathbf{r}-\mathbf{R}_i\|^2}{2\sigma^2}\right)
    $$
    where $\sigma$ is the width of the Gaussians and $f_c$ is a cutoff function.

2.  **Expand in an Orthonormal Basis:** This density field is then expanded in a basis of functions that separates radial and angular information. This is typically a product of a radial basis $\{g_n(r)\}$ and the spherical harmonics $\{Y_{lm}(\hat{\mathbf{r}})\}$. The expansion coefficients are calculated by projection:
    $$
    c_{nlm} = \int_{0}^{r_c} dr\, r^2 \int d\hat{\mathbf{r}}\, g_n(r)\, Y_{lm}^*(\hat{\mathbf{r}})\, \rho(\mathbf{r})
    $$

3.  **Construct the Invariant Power Spectrum:** The expansion coefficients $c_{nlm}$ are not rotationally invariant; they transform according to Wigner D-matrices. To create an invariant descriptor, one constructs the **power spectrum**, which is a rotationally invariant quadratic combination of the coefficients:
    $$
    p_{n n' l} = \sum_{m=-l}^{l} c_{n l m}\, c_{n' l m}^*
    $$
    The collection of these $p_{n n' l}$ values for different $n, n', l$ forms the SOAP descriptor vector. It is systematically improvable and has been shown to be a highly effective representation.

### Architectures: From Descriptors to Energies

Once the [local atomic environment](@entry_id:181716) is encoded in a symmetry-preserving descriptor vector, a regression model is needed to map this vector to an atomic energy contribution.

#### Additive Models (Behler-Parrinello Type)

In the Behler-Parrinello framework, the total energy is the sum of atomic energies, $E = \sum_i \varepsilon_i$, and each atomic energy is the output of a separate [regression model](@entry_id:163386) for each chemical element, $Z_i$ [@problem_id:2784673]. Typically, this model is an atomic artificial neural network (ANN):
$$
\varepsilon_i = f^{(Z_i)}(\mathbf{G}_i)
$$
where $\mathbf{G}_i$ is the symmetry function vector for atom $i$. Using element-specific ANNs ($f^{(Z_i)}$) allows the model to learn the distinct chemical behavior of different atoms (e.g., carbon behaves differently from oxygen). The regression model itself does not need to be an ANN; other models like Gaussian Process (GP) regressors can also be used, as the fundamental properties of invariance and [extensivity](@entry_id:152650) are determined by the descriptor design and the additive architecture, not the specific choice of regressor [@problem_id:2784673].

#### End-to-End Equivariant Architectures (E(3)-GNNs)

A more recent and powerful paradigm involves **E(3)-equivariant Graph Neural Networks (GNNs)**, which build symmetry directly into the learning process, often avoiding the need for handcrafted invariant descriptors [@problem_id:2648604]. In this approach:
- Atoms are nodes in a graph, and edges represent neighboring pairs.
- Node features are not restricted to be scalars (invariants). Instead, they can be vectors, or [higher-rank tensors](@entry_id:200122), that transform according to the [irreducible representations](@entry_id:138184) (irreps) of the rotation group SO(3). For example, a vector feature (like a dipole moment) would be an $l=1$ irrep.
- The network updates features through **[message passing](@entry_id:276725)** layers. A message from atom $j$ to atom $i$ is constructed by coupling the features of atom $j$ with geometric information from the [relative position](@entry_id:274838) vector $\mathbf{r}_{ij}$. This geometric information is encoded using spherical harmonics, which also form bases for irreps.
- The coupling is performed using **tensor products**, and the results are decomposed back into a sum of irreps using **Clebsch-Gordan coefficients**. This mathematical machinery guarantees that if the input features have well-defined transformation properties (equivariance), the output features of the layer will also be equivariant by construction.
- Translational [equivariance](@entry_id:636671) is handled by using only [relative position](@entry_id:274838) vectors as input, which are themselves translationally invariant. Inversion symmetry (parity) can also be incorporated by tracking the parity of the features and using [parity selection rules](@entry_id:203598) in the couplings.
The final energy is obtained by combining equivariant features to produce a scalar ($l=0$) output, which is guaranteed to be invariant.

### Practical Considerations and Advanced Topics

Building a robust and reliable MLP involves several further critical considerations that bridge theory and practice.

#### Forces and Integrability

In [molecular dynamics](@entry_id:147283), both energies and forces are required. Forces can be obtained from an MLP in two ways [@problem_id:2784650]:
1.  **Scalar Energy-Based (Strategy S):** Model a scalar potential energy $E_{\theta}(\mathbf{R})$ and compute forces analytically as its negative gradient, $\mathbf{F}_{\theta}(\mathbf{R}) = -\nabla_{\mathbf{R}} E_{\theta}(\mathbf{R})$. This is typically done using [automatic differentiation](@entry_id:144512) in modern frameworks.
2.  **Vector Force-Based (Strategy V):** Model the force vector field $\mathbf{F}_{\phi}(\mathbf{R})$ directly, without reference to a scalar potential.

The first approach is vastly superior and almost universally adopted. By defining forces as the gradient of a potential, the force field is guaranteed to be **conservative** or **integrable**. This means the curl of the force field is identically zero ($\nabla \times \mathbf{F}_{\theta} = \mathbf{0}$), and the work done by the forces is independent of the path taken. This property is essential for energy conservation in microcanonical (NVE) [molecular dynamics simulations](@entry_id:160737). In contrast, an unconstrained vector model $\mathbf{F}_{\phi}$ will generally have a non-zero curl, leading to [non-conservative forces](@entry_id:164833) that can do [net work](@entry_id:195817) over closed loops. This results in unphysical, systematic [energy drift](@entry_id:748982) in MD simulations, even with a perfect integrator [@problem_id:2784650].

Furthermore, imposing symmetries on the scalar energy $E_{\theta}$ is straightforward, and the correct [equivariance](@entry_id:636671) properties of the forces $\mathbf{F}_{\theta}$ follow automatically from the gradient operation [@problem_id:2648604] [@problem_id:2784650].

#### The Role of the Cutoff Function

The use of a finite cutoff $r_c$ requires a **switching function**, $s(r)$, to smoothly transition the potential and its derivatives to zero [@problem_id:2648588]. Abruptly truncating the potential would create an infinite force (a discontinuity in the energy), which is numerically catastrophic. The smoothness of the potential at the cutoff is critical for stable dynamics:
- **$C^0$ Continuity (Energy):** The potential must be continuous. This is ensured if the switching function $s(r)$ satisfies $s(r_c) = 0$.
- **$C^1$ Continuity (Forces):** The forces must be continuous. This requires the first derivative of the potential to be continuous, which is guaranteed for any underlying potential if $s(r_c) = 0$ and $s'(r_c) = 0$. A discontinuity in the force is equivalent to an unphysical impulse that injects energy into the system, causing drift.
- **$C^2$ Continuity (Hessian):** The Hessian (second derivative of energy) should ideally be continuous. This is ensured if $s(r_c)$, $s'(r_c)$, and $s''(r_c)$ are all zero. Hessian discontinuities create artificial high-frequency vibrations that can limit the maximum [stable time step](@entry_id:755325) of the simulation.

A commonly used form for the cutoff function inside the switching region is a polynomial or a trigonometric function like $f_c(r) = \frac{1}{2}\left[\cos\left(\frac{\pi r}{R_c}\right)+1\right]$ (for a switching region starting at $r=0$) [@problem_id:2784613].

#### The Challenge of Long-Range Interactions

The locality principle, while powerful, is also the source of a fundamental limitation: strictly local, finite-cutoff MLPs cannot, by themselves, describe **long-range interactions** [@problem_id:2648601]. This is particularly problematic for:
- **Electrostatics:** The Coulomb interaction decays as $1/r$, which is too slow to be truncated at typical cutoff radii (e.g., 5-10 Å) without incurring significant errors. In periodic systems, the collective electrostatic interactions require special treatment (e.g., Ewald summation) and depend on the global configuration.
- **Dispersion (van der Waals forces):** These interactions, arising from correlated quantum fluctuations, decay as $1/r^6$. While this is faster than Coulomb interactions, the cumulative effect from all distant atoms can be substantial, especially in condensed phases.
- **Polarization:** In polarizable systems, an atom's [induced dipole moment](@entry_id:262417) depends on the local electric field, which is itself a sum of long-range contributions from all other charges and dipoles in the system. This creates a non-local, self-consistent problem that cannot be captured within a finite cutoff.

For high-accuracy simulations of ionic materials, polar liquids, or systems where dispersion is dominant, it is often necessary to use hybrid models that combine a short-range MLP with an explicit, physics-based model for [long-range interactions](@entry_id:140725).

#### Uncertainty Quantification

Like any model trained on finite data, MLPs have predictive uncertainty. Understanding and quantifying this uncertainty is critical for assessing model reliability and for applications like [active learning](@entry_id:157812). The total uncertainty can be decomposed into two types [@problem_id:2784631]:

- **Epistemic Uncertainty:** This represents the model's "ignorance" due to limited training data. It is high in regions of the [configuration space](@entry_id:149531) that are far from any training examples (e.g., near a transition state not included in the dataset). Epistemic uncertainty is reducible; it can be decreased by adding more training data in the regions where it is high. It is often estimated by measuring the variance in predictions across an ensemble of independently trained models.

- **Aleatoric Uncertainty:** This represents the inherent "noise" or variability in the training data itself. It is an irreducible error for a given data source. For example, [ab initio](@entry_id:203622) energies from Quantum Monte Carlo have an intrinsic statistical error, and energies from Density Functional Theory can have numerical noise from unconverged SCF cycles or finite [k-point sampling](@entry_id:177715). This uncertainty persists even with infinite data. It is typically estimated by having the MLP predict the parameters of a probability distribution (e.g., the mean and variance of a Gaussian) for the output.

Distinguishing these two sources of uncertainty allows for a more nuanced assessment of an MLP's predictions. High [epistemic uncertainty](@entry_id:149866) signals that the model is extrapolating and its prediction should not be trusted, whereas high [aleatoric uncertainty](@entry_id:634772) signals that the underlying reference data is noisy.