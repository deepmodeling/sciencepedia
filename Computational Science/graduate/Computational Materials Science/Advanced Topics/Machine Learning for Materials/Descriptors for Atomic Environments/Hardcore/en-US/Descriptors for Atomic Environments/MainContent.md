## Introduction
In the field of computational materials science, the ability to predict material properties from atomic structures is paramount. While quantum mechanical methods offer high accuracy, their computational cost limits them to small systems and short timescales. Atomistic machine learning bridges this gap by creating fast, accurate [surrogate models](@entry_id:145436), but these models face a fundamental challenge: how can a machine learning algorithm process the raw, variable-sized list of atomic coordinates in a way that respects the [fundamental symmetries](@entry_id:161256) of physics? The answer lies in the concept of **atomic environment descriptors**—fixed-size numerical vectors that represent the local chemical environment around an atom in a consistent and physically meaningful way.

This article provides a graduate-level exploration of these crucial tools. We will dissect the theory and practice behind designing and using descriptors to build powerful predictive models for materials.

First, in **Principles and Mechanisms**, we will establish the foundational requirements for any descriptor, such as [rotational invariance](@entry_id:137644) and differentiability, and explore why they are non-negotiable for physical modeling. We will then dive into the detailed construction of two leading descriptor families: the Atom-Centered Symmetry Functions (ACSF) and the Smooth Overlap of Atomic Positions (SOAP) framework, comparing their [expressivity](@entry_id:271569) and inherent body order.

Next, **Applications and Interdisciplinary Connections** will demonstrate how these descriptors are used to construct [machine-learned interatomic potentials](@entry_id:751582) (MLIPs), which power large-scale [molecular dynamics simulations](@entry_id:160737). We will discuss how descriptors enable the prediction of defect energies, serve as fingerprints for structural classification, and can be extended to incorporate richer physics like electrostatics and magnetism.

Finally, the **Hands-On Practices** section will solidify these concepts through a series of computational exercises. These problems will guide you through implementing descriptors from scratch, testing their limitations, and understanding the practical considerations necessary for building robust simulation tools.

## Principles and Mechanisms

The primary goal of atomistic machine learning is to construct a model that accurately predicts properties of a material system, most notably its potential energy, based solely on the positions of its constituent atoms. As established in the Introduction, such models rely on a crucial intermediate step: the transformation of raw Cartesian coordinates into a fixed-size numerical vector, known as a **descriptor** or **feature vector**. This descriptor, denoted $\mathcal{D}$, serves as the input to a machine learning algorithm. Its design is paramount; a well-designed descriptor captures the essential physics and chemistry of a [local atomic environment](@entry_id:181716), while a poorly designed one will invariably lead to a predictive model that is inaccurate, unphysical, or both. This chapter elucidates the fundamental principles that govern the design of effective descriptors and details the mechanisms of two prominent families: Atom-Centered Symmetry Functions (ACSF) and the Smooth Overlap of Atomic Positions (SOAP) framework.

### Fundamental Principles of Descriptor Design

In the absence of external fields, the Born-Oppenheimer [potential energy surface](@entry_id:147441), $E(\mathbf{R})$, where $\mathbf{R} = \{\mathbf{r}_1, \dots, \mathbf{r}_N\}$ is the set of all atomic positions, must obey certain [fundamental symmetries](@entry_id:161256) of physics. Any descriptor used to model this energy must respect these symmetries.

#### Invariance Requirements

A descriptor that represents a [local atomic environment](@entry_id:181716) around a central atom $i$ must be invariant to transformations that do not alter the system's energy. These are:

1.  **Translational Invariance:** Shifting the entire system by a constant vector must not change the descriptor. This is naturally satisfied by defining the environment in terms of [relative position](@entry_id:274838) vectors, $\mathbf{r}_{ij} = \mathbf{r}_j - \mathbf{r}_i$, where $i$ is the central atom and $j$ indexes its neighbors.
2.  **Permutational Invariance:** The descriptor must be invariant to the re-labeling of identical atoms. If neighbors $j$ and $k$ are of the same chemical species, swapping their positions must yield the exact same descriptor vector. This is typically achieved by using operations like summation or by sorting lists of neighbor contributions.
3.  **Rotational Invariance:** Rotating the entire system around the central atom must not change the descriptor. This is the most challenging invariance to enforce and is a primary differentiator between descriptor families. It requires constructing the descriptor from rotational invariants, such as distances, angles, or more complex integrated quantities.

A failure to enforce these invariances forces the machine learning model to learn these [fundamental symmetries](@entry_id:161256) from data, a task that is inefficient and prone to error. Consider, for instance, a hypothetical descriptor based on a simple histogram of absolute neighbor positions in a lab-fixed Cartesian grid. Such a descriptor is neither translationally nor rotationally invariant; a small shift or rotation of the system could drastically change the descriptor vector, even though the physical environment is unchanged. This would require the learning algorithm to see examples of the same environment in every possible orientation to learn that they are equivalent, which is computationally intractable .

#### Differentiability

A cornerstone of atomistic simulations is the ability to compute forces as the negative gradient of the potential energy, $\mathbf{F}_k = -\nabla_{\mathbf{r}_k} E$. For an atom-centered model where the total energy is a sum of local energy contributions, $E = \sum_i \varepsilon(\mathcal{D}_i)$, the [chain rule](@entry_id:147422) dictates that the force on an atom $k$ depends on the derivative of the descriptor with respect to atomic positions:
$$
\mathbf{F}_k = -\sum_{i} \frac{\partial \varepsilon}{\partial \mathcal{D}_i} \frac{\partial \mathcal{D}_i}{\partial \mathbf{r}_k}
$$
For this expression to yield well-defined, [conservative forces](@entry_id:170586), the descriptor mapping $\mathbf{R} \mapsto \mathcal{D}_i(\mathbf{R})$ must be a continuous and differentiable function of the atomic coordinates.

This requirement immediately rules out many seemingly simple descriptor ideas. For example, a descriptor based on a sorted list of neighbor distances, while satisfying all invariance requirements, is not everywhere differentiable. At configurations where two neighbor distances become equal, their order in the sorted list can swap, creating a non-differentiable "kink" in the descriptor function. This leads to ill-defined or infinite forces, which would break any molecular dynamics simulation . Similarly, any descriptor based on sharp [binning](@entry_id:264748) or a sharp [cutoff radius](@entry_id:136708) is discontinuous and thus not differentiable at the boundaries, leading to unphysical "impulse" forces when an atom crosses a boundary . Consequently, the use of **smooth cutoff functions** that gently drive descriptor contributions to zero at a finite [cutoff radius](@entry_id:136708) $r_c$ is a near-universal feature of modern descriptors.

### The Neighbor Density Approach: Smooth Overlap of Atomic Positions (SOAP)

The SOAP framework provides a systematic and mathematically rigorous way to generate descriptors that satisfy the fundamental principles. It begins by representing the local environment not as a discrete list of atoms, but as a continuous field known as the **neighbor density**.

#### The Smoothed Neighbor Density

For a central atom at the origin, the positions of its neighbors $\{\mathbf{R}_i\}$ can be represented by a sum of Dirac delta functions, $\rho^{(0)}(\mathbf{r}) = \sum_i \delta(\mathbf{r} - \mathbf{R}_i)$. To create a smooth and differentiable object, this distribution is convolved with a smoothing function, typically a normalized Gaussian $g_{\sigma}(\mathbf{r})$ of width $\sigma$. This yields the smoothed neighbor density:
$$
\tilde{\rho}(\mathbf{r}) = \int_{\mathbb{R}^{3}} \rho^{(0)}(\mathbf{r}^{\prime})\, g_{\sigma}(\mathbf{r}-\mathbf{r}^{\prime})\, \mathrm{d}^{3}\mathbf{r}^{\prime} = \sum_{i} g_{\sigma}(\mathbf{r} - \mathbf{R}_i)
$$
The smoothed density is thus a superposition of Gaussian "clouds" centered at each neighbor's position. The parameter $\sigma$ is a crucial hyperparameter: a small $\sigma$ yields sharp, highly resolved features, while a large $\sigma$ washes out fine details.

A natural way to compare two atomic environments, $A$ and $B$, is to compute the overlap integral of their respective smoothed densities, $S = \int \tilde{\rho}_{A}(\mathbf{r}) \tilde{\rho}_{B}(\mathbf{r}) \mathrm{d}^{3}\mathbf{r}$. This overlap forms the conceptual basis of SOAP. By using properties of Gaussian integrals, this overlap can be shown to be a sum of pairwise Gaussian interactions between the atoms of the two environments :
$$
S = \sum_{i \in A} \sum_{j \in B} (4\pi \sigma^{2})^{-3/2} \exp\left(-\frac{|\mathbf{R}_{i}^{A}-\mathbf{R}_{j}^{B}|^{2}}{4\sigma^{2}}\right)
$$
This kernel measures the similarity between two environments in a rotationally invariant way.

#### Expansion and the Power Spectrum

To create a descriptor vector for a single environment, SOAP expands the neighbor density $\tilde{\rho}(\mathbf{r})$ in a complete, orthonormal basis that separates radial and angular components. This basis consists of products of radial basis functions $R_n(r)$ and the complex [spherical harmonics](@entry_id:156424) $Y_{lm}(\hat{\mathbf{r}})$:
$$
\tilde{\rho}(\mathbf{r}) = \sum_{n,l,m} c_{nlm} R_n(r) Y_{lm}(\hat{\mathbf{r}})
$$
The expansion coefficients $c_{nlm}$ are found by projection:
$$
c_{nlm} = \int \tilde{\rho}(\mathbf{r}) R_n(r) Y_{lm}^*(\hat{\mathbf{r}}) \,d^3\mathbf{r} = \sum_{j} \int g_{\sigma}(\mathbf{r} - \mathbf{R}_j) R_n(r) Y_{lm}^*(\hat{\mathbf{r}}) \,d^3\mathbf{r}
$$
These coefficients form a complete representation of the density but are not rotationally invariant. Under a rotation of the environment, they transform according to the Wigner D-matrices. To achieve [rotational invariance](@entry_id:137644), SOAP constructs the **power spectrum** by summing the squared magnitudes of the coefficients over the magnetic index $m$ for each angular momentum channel $l$:
$$
p_{nn'l} = \sum_{m=-l}^{l} c_{nlm}^* c_{n'lm}
$$
The vector composed of these $p_{nn'l}$ values for all relevant $n, n', l$ is the SOAP descriptor. It is rotationally invariant by construction. The number of components in this vector depends on the number of species and the hyperparameters chosen for the basis, namely the number of radial functions $n_{max}$ and the maximum angular momentum $l_{max}$ . For example, the calculation of a single coefficient $c_{100}$ for a simplified density demonstrates how the geometry of the environment ($R$) and the hyperparameters ($\sigma, \alpha$) are encoded in the expansion .

### The Invariant Coordinate Approach: Atom-Centered Symmetry Functions (ACSF)

The ACSF framework, pioneered by Behler and Parrinello, takes a more direct route to constructing descriptors. Instead of creating a complex object (the density) and then systematically making it invariant, ACSF builds the descriptor from functions of coordinates that are already invariant under rotation, namely interatomic distances and angles.

#### Radial and Angular Symmetry Functions

ACSFs are categorized by the number of atoms they involve.

**Two-body functions ($G^2$):** These functions capture the radial distribution of neighbors. They depend only on the distances $r_{ij}$ between the central atom $i$ and its neighbors $j$. A common form is:
$$
G^2 = \sum_j e^{-\eta(r_{ij} - R_s)^2} f_c(r_{ij})
$$
Here, the Gaussian term is centered on a specific radius $R_s$ with a width controlled by $\eta$, making the function sensitive to atoms in a particular radial shell. The sum over all neighbors $j$ ensures permutational invariance. The descriptor vector consists of a set of $G^2$ values for different choices of parameters $(\eta, R_s)$. Because each term depends on a single neighbor $j$, these are considered **2-body** descriptors (including the central atom).

**Three-body functions (e.g., $G^4, G^5$):** To capture the crucial angular information related to chemical bonding, functions must depend on triplets of atoms $(i, j, k)$. These functions depend on the angle $\theta_{ijk}$ between the vectors $\mathbf{r}_{ij}$ and $\mathbf{r}_{ik}$. A typical angular function has the form:
$$
G^4 = 2^{1-\zeta} \sum_{j \neq k} (1 + \lambda \cos\theta_{ijk})^{\zeta} \times \text{RadialWeight}(r_{ij}, r_{ik}, r_{jk}) \times \text{Cutoffs}
$$
The angular part $(1 + \lambda \cos\theta_{ijk})^{\zeta}$ provides [angular resolution](@entry_id:159247), controlled by parameters $\lambda$ and $\zeta$. The radial weighting term and cutoff functions localize the interaction. Since each term in the sum depends on a pair of neighbors $\{j, k\}$, these are **3-body** descriptors . Different families of angular functions, like G4 and G5, vary primarily in their choice of radial weighting and cutoff terms, which can subtly alter their behavior .

A finite linear combination of these predefined functions forms the final ACSF descriptor vector. By construction, each element is smooth, differentiable, and invariant to translation, permutation, and rotation.

### Expressivity, Pathologies, and Body Order

While both SOAP and ACSF are powerful and widely used, they have distinct characteristics and limitations. A key concept for comparison is **[expressivity](@entry_id:271569)**, or the ability of a descriptor to distinguish between two different, non-equivalent atomic environments.

#### Radial vs. Angular Information

A descriptor is said to be **complete** if it can uniquely distinguish any two geometrically distinct environments (up to the [fundamental symmetries](@entry_id:161256)). A descriptor based only on the set of central-atom-to-neighbor distances $\{r_{ij}\}$ is fundamentally incomplete. It cannot distinguish between environments that have the same radial distribution but different angular structures.

A classic example is comparing a tetrahedral arrangement of four neighbors with a square planar arrangement, both at the same distance $r_0$ from the central atom. Any purely radial descriptor, such as an ACSF vector composed only of $G^2$ functions, will produce the exact same feature vector for both environments, as the set of distances $\{r_0, r_0, r_0, r_0\}$ is identical in both cases. In contrast, descriptors that incorporate angular information, such as angular ACSFs or SOAP with an angular basis including $l \ge 2$, can easily distinguish them  .

#### Body Order

The **body order** of a descriptor component specifies the number of interacting particles it describes. A 2-body term depends on the central atom and one neighbor. A 3-body term depends on the central atom and two neighbors, and so on. Higher body-order terms are necessary to capture complex [many-body interactions](@entry_id:751663).
*   ACSF $G^2$ functions are 2-body.
*   ACSF $G^4$ functions are 3-body.
*   The standard SOAP power spectrum ($p_{nn'l}$) is quadratic in the expansion coefficients ($c_{nlm}$), which are themselves sums over single neighbors. This results in terms that depend on pairs of neighbors $(j, k)$, making the SOAP power spectrum intrinsically a **3-body** descriptor .

To capture higher-order correlations (4-body and beyond), one must go beyond these standard forms. For ACSF, this would require defining functions of four or more atoms. For SOAP, this can be achieved by constructing [higher-order spectra](@entry_id:191458), such as the bispectrum (a 4-body quantity involving products like $c \cdot c \cdot c$), or by using polynomial kernels on the [power spectrum](@entry_id:159996) vector. For instance, a kernel of the form $K(\mathcal{X}, \mathcal{Y}) = (\hat{\mathbf{p}}(\mathcal{X}) \cdot \hat{\mathbf{p}}(\mathcal{Y}))^\zeta$ implicitly maps the 3-body power spectrum into a feature space containing correlations up to body-order $(2\zeta+1)$ .

#### Pathologies and Limitations

No descriptor is perfect. A critical limitation of the SOAP power spectrum is that it is invariant under spatial inversion ($\mathbf{r} \to -\mathbf{r}$). This means it cannot distinguish between an environment and its mirror image (a pair of [enantiomers](@entry_id:149008)). This can be proven mathematically by analyzing the transformation properties of spherical harmonics under inversion, which shows that the power spectrum remains unchanged . This is a significant "pathology" for modeling chiral systems.

Furthermore, for any descriptor based on a finite number of features (e.g., a finite ACSF set or a truncated SOAP basis), there can be "accidental" degeneracies where two distinct, non-symmetric environments produce identical descriptor vectors  . Achieving true completeness requires, in theory, an infinite basis.

### Practical Aspects: Hyperparameters and Computational Scaling

The practical utility of a descriptor depends on the trade-off between its descriptive power and its computational cost. This trade-off is governed by a set of **hyperparameters**.

For SOAP, these include the [cutoff radius](@entry_id:136708) $r_c$, the Gaussian smoothing width $\sigma$, and the basis set size defined by $n_{max}$ and $l_{max}$. These parameters are not independent. For instance, the spatial resolution is limited by $\sigma$, which in turn suggests a natural choice for the [angular resolution](@entry_id:159247), e.g., $l_{max} \approx r_c / \sigma$ . Increasing $n_{max}$ and $l_{max}$ increases the descriptor's resolution but also its size and the cost of computing it.

The computational cost of generating descriptors for a system of $A$ atoms, each with an average of $z$ neighbors, can be significant.
*   For ACSF, the cost scales with $z$ for radial functions and $z^2$ for angular functions.
*   For SOAP, the cost involves accumulating coefficients (scaling with $z \cdot n_{max} \cdot l_{max}^2$) and computing the power spectrum (scaling with $n_{max}^2 \cdot l_{max}^2$).

For large systems or high-resolution descriptors, these costs can become prohibitive. This motivates **sparsification**, where only the most significant components of the descriptor are computed and stored. By defining [surrogate models](@entry_id:145436) for the magnitudes of descriptor components, one can establish thresholds to discard components that are likely to be near zero, significantly reducing the memory footprint and computational effort without substantial loss of information . This systematic management of descriptor complexity is essential for applying these methods to large-scale materials simulations.