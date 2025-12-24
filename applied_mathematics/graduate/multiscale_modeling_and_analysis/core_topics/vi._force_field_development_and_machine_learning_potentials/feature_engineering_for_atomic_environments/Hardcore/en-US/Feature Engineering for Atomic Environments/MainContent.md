## Introduction
Predicting the properties of materials at the atomic scale, from their energy to the forces acting upon them, is a central goal in computational science. Machine learning has emerged as a powerful tool to achieve this, but these models cannot directly interpret raw atomic coordinates. This creates a critical knowledge gap: how do we translate the complex, variable arrangement of atoms into a fixed, numerical format that is both understandable to an algorithm and respectful of the underlying laws of physics? This process, known as [feature engineering](@entry_id:174925), is the cornerstone of building robust and accurate atomic-scale models.

This article provides a comprehensive guide to the theory and practice of feature engineering for atomic environments. The first chapter, "Principles and Mechanisms," will establish the fundamental requirements for any valid descriptor, including symmetry, locality, and smoothness, and explore the main strategies for their construction. The second chapter, "Applications and Interdisciplinary Connections," will showcase how these descriptors are used to build powerful [machine-learned interatomic potentials](@entry_id:751582) and drive discovery in materials science, chemistry, and biology. Finally, the "Hands-On Practices" section will offer practical exercises to solidify these concepts, from implementing a basic radial descriptor to analyzing its physical and mathematical properties. By mastering these components, you will gain the essential skills to bridge the gap between raw atomic data and [predictive modeling](@entry_id:166398).

## Principles and Mechanisms

The construction of predictive models for atomic-scale properties, such as energy and forces, hinges on a crucial intermediate step: the transformation of raw Cartesian coordinates of atoms into a fixed-dimensional numerical representation, known as a **descriptor** or **feature vector**. This descriptor, denoted $\mathbf{s}_i$ for atom $i$, serves as the input to a machine learning model, such as a neural network or kernel regression model. To be physically meaningful and practically effective, this representation must rigorously adhere to a set of fundamental principles derived from the underlying physics of the system. This chapter elucidates these core principles—symmetry, locality, and smoothness—and details the primary mechanisms through which they are implemented in modern descriptor design.

### Fundamental Requirements: Symmetries of Physical Law

The ultimate target for most [machine-learned interatomic potentials](@entry_id:751582) is the Born-Oppenheimer potential energy surface, $E_{\mathrm{BO}}(\{\mathbf{r}_a\})$. This energy surface is the ground-state eigenvalue of the non-relativistic quantum mechanical Hamiltonian for a given configuration of atomic nuclei $\{\mathbf{r}_a\}$. This Hamiltonian, and consequently the energy surface itself, possesses [fundamental symmetries](@entry_id:161256) because the underlying physical laws are independent of the observer's frame of reference and do not distinguish between [identical particles](@entry_id:153194) . Any faithful model of this energy surface must, therefore, inherit these same symmetries.

The primary symmetries are those of the **Euclidean group** $E(3)$—global translations and rotations—and the **[permutation group](@entry_id:146148)** $S_N$ for the relabeling of identical atoms.

#### Invariance and Equivariance

The manner in which a descriptor must respect these symmetries depends on the nature of the quantity it represents. We distinguish between two types of symmetric behavior: **invariance** and **equivariance**.

A **scalar** quantity, such as energy, must be **invariant**. This means its value does not change when a symmetry operation is applied to the atomic system. Let $d$ be a scalar descriptor for a system of $N$ atoms with positions $\{\mathbf{r}_i\}$ and species labels $\{s_i\}$. The descriptor is invariant if, for any translation vector $\mathbf{t} \in \mathbb{R}^3$, any rotation matrix $\mathbf{R} \in SO(3)$, and any permutation $\sigma$ that only exchanges labels of atoms of the same species, the following identity holds :
$$
d\big(\{\mathbf{r}_i, s_i\}_{i=1}^N\big) = d\big(\{\mathbf{R}\mathbf{r}_{\sigma(i)} + \mathbf{t}, s_{\sigma(i)}\}_{i=1}^N\big)
$$
This single equation rigorously encodes invariance under translation, rotation, and permutation of identical species.

In contrast, **vector** or **tensor** quantities, such as forces or the stress tensor, are not invariant but rather **equivariant** (or covariant). This means that they transform in a well-defined way that mirrors the transformation applied to the system. For example, if the entire atomic configuration is rotated, the force vector on each atom should rotate in exactly the same way. For a per-atom vector descriptor $\{\mathbf{v}_i\}_{i=1}^N$, [equivariance](@entry_id:636671) under rotations and permutations is formally expressed as :
$$
\mathbf{v}_{\sigma(i)}\big(\{\mathbf{R}\mathbf{r}_j, s_j\}_{j=\sigma(1)}^{\sigma(N)}\big) = \mathbf{R}\,\mathbf{v}_i\big(\{\mathbf{r}_j, s_j\}_{j=1}^N\big)
$$
Here, the transformation of the input coordinates by $\mathbf{R}$ and $\sigma$ results in an output that is both rotated by $\mathbf{R}$ and re-indexed according to $\sigma$. This property is crucial for models that aim to predict vectorial quantities directly. For a global [rank-2 tensor](@entry_id:187697) descriptor $\mathbf{T}$, rotational [equivariance](@entry_id:636671) requires $\mathbf{T}(\{\mathbf{R}\mathbf{r}_i\}) = \mathbf{R}\mathbf{T}(\{\mathbf{r}_i\})\mathbf{R}^\top$.

These symmetry constraints are not mere mathematical niceties. As a direct consequence of Noether's theorem, enforcing these symmetries in the energy model ensures the satisfaction of fundamental physical conservation laws. Translational invariance of the total energy guarantees that the net force on an isolated system is zero, corresponding to the [conservation of linear momentum](@entry_id:165717). Rotational invariance guarantees that the [net torque](@entry_id:166772) is zero, corresponding to the conservation of angular momentum . Building these symmetries into the descriptor is the most robust way to ensure the resulting physical model is well-behaved.

### Fundamental Requirements: Locality and Smoothness

Beyond symmetries, two further principles are essential for constructing computationally efficient and physically realistic models: locality and smoothness.

#### The Principle of Locality and Nearsightedness

A central tenet of modern condensed matter physics is the **[principle of nearsightedness](@entry_id:165063)**, which states that local properties of a system are primarily determined by the local environment . For example, the energy contribution of an atom $i$ is largely insensitive to changes in the position of a distant atom $j$. This principle justifies the use of descriptors that are functions of a finite local neighborhood, typically defined by a **cutoff radius**, $r_c$. All atoms beyond this radius are ignored, which is essential for making the computational cost of the model scale linearly with the number of atoms, $O(N)$.

The validity of this approximation, and the rate at which the error from this truncation decays, depends on the electronic structure of the material.
*   In **insulating materials** (or any system with a non-zero [electronic band gap](@entry_id:267916)), the influence of distant perturbations decays exponentially. The truncation error $\Delta P_i(r_c)$ for a local property is thus bounded by an exponential function: $\Delta P_i(r_c) \le C' \exp(-r_c/\xi)$, where $\xi$ is a characteristic length scale. This implies that the required cutoff radius to achieve a target accuracy $\epsilon$ scales only logarithmically with the error: $r_c \propto \xi \ln(1/\epsilon)$ .
*   In **metallic materials** at zero temperature, the absence of a band gap leads to a much slower, algebraic decay of correlations. This means that local models with finite cutoffs may be less accurate or require much larger cutoffs to achieve the same level of precision.
*   At **finite temperature**, thermal effects effectively smooth the electronic structure even in metals, restoring an exponential decay of correlations and justifying the local cutoff approximation once again .

#### The Principle of Smoothness (Differentiability)

In atomistic simulations, forces are as important as energies. They govern atomic motion in molecular dynamics and are used for geometry optimization. The force $\mathbf{F}_k$ on atom $k$ is the negative gradient of the potential energy with respect to its coordinates, $\mathbf{F}_k = -\nabla_{\mathbf{r}_k} E$. For forces to be well-defined and continuous functions of atomic positions—a prerequisite for stable [numerical integration](@entry_id:142553) and energy conservation—the [potential energy function](@entry_id:166231) $E$ must be at least once continuously differentiable ($C^1$) .

A mapping $\mathbf{D}_i$ from the space of all atomic coordinates $\mathbf{R} \in \mathbb{R}^{3N}$ to the descriptor space $\mathbb{R}^m$ is differentiable at $\mathbf{R}_0$ if its change can be locally approximated by a [linear map](@entry_id:201112), the Jacobian $J_{\mathbf{D}_i}(\mathbf{R}_0)$ . Given a total energy model of the form $E(\mathbf{R}) = \sum_i \varepsilon(\mathbf{D}_i(\mathbf{R}))$, where $\varepsilon$ is the learned energy contribution per atom, the force on an atom $k$ is given by the chain rule:
$$
\mathbf{F}_k = - \nabla_{\mathbf{r}_k} E = - \sum_{i=1}^N \frac{\partial \varepsilon}{\partial \mathbf{D}_i} \frac{\partial \mathbf{D}_i}{\partial \mathbf{r}_k}
$$
This expression makes it clear that to compute forces analytically, both the gradient of the learning model with respect to the descriptor, $\partial \varepsilon / \partial \mathbf{D}_i$, and the gradient of the descriptor with respect to atomic coordinates (its Jacobian), $\partial \mathbf{D}_i / \partial \mathbf{r}_k$, must exist and be well-defined.

This requirement has profound practical implications. Descriptor constructions that involve non-differentiable operations, such as sorting neighbor distances or taking the maximum value of a function over neighbors, are unsuitable for force-prediction models. Such operations lead to discontinuous gradients, which manifest as non-physical impulses in a simulation, violating energy conservation , . To ensure smoothness, descriptors are constructed using continuously differentiable functions, and the locality cutoff $r_c$ is implemented via a **smooth cutoff function** $f_c(r)$ that not only goes to zero at $r_c$ but whose derivative also vanishes, i.e., $f_c(r_c)=0$ and $f_c'(r_c)=0$. This guarantees that both the energy and force contributions of an atom go smoothly to zero as it crosses the cutoff boundary , .

### Constructing Invariant Descriptors: Building Blocks and Strategies

With the fundamental requirements of symmetry, locality, and smoothness established, we can now explore common strategies for descriptor construction. The most direct approach is to build invariant features from elementary invariant building blocks.

The simplest geometric quantities that are inherently invariant under global translations and rotations are the scalar **interatomic distances** $r_{ij} = \|\mathbf{r}_i - \mathbf{r}_j\|$, **[bond angles](@entry_id:136856)** $\theta_{ijk}$ between three atoms, and **[dihedral angles](@entry_id:185221)** involving four atoms . A descriptor can be constructed as a function of these quantities. To ensure [permutation invariance](@entry_id:753356) for identical atoms, contributions from all equivalent neighbors are typically summed. This simple summation is a powerful mechanism for satisfying [permutation symmetry](@entry_id:185825), as the order of addition is irrelevant .

For systems with multiple chemical elements, information about atomic species must be encoded. Two common strategies are:
1.  **Species Channeling**: Separate descriptors are calculated for each type of neighboring element or combination of elements. For a radial descriptor, one might have separate components for all neighboring Si atoms and all neighboring O atoms. This is a very expressive and robust method .
2.  **Species Weighting**: A single descriptor is calculated, but the contribution of each neighbor is weighted by a factor $w_{s_j}$ that depends on its species $s_j$. This is more compact but may be less expressive than full channeling .

#### A Concrete Example: Atom-Centered Symmetry Functions (ACSFs)

A canonical example of this construction strategy is the **Atom-Centered Symmetry Functions (ACSFs)** developed by Behler and Parrinello . These functions are designed to describe the radial and angular environment around a central atom $i$. A typical implementation involves two main types:

A **[radial symmetry](@entry_id:141658) function** ($G^2$) probes the distribution of neighbors at different distances. A common form is a sum of Gaussians centered at various radii $R_s$, modulated by a width parameter $\eta$ and a smooth cutoff function $f_c(r_{ij})$:
$$
G_i^{2}(\eta, R_s) = \sum_{j \neq i} \exp\left[-\eta (r_{ij}-R_s)^2\right] f_c(r_{ij})
$$
By using a set of different $(R_s, \eta)$ parameters, one can build a [feature vector](@entry_id:920515) that captures the detailed structure of the radial distribution function. Conceptually, this function can be seen as a form of **[kernel density estimation](@entry_id:167724)**, where the [discrete set](@entry_id:146023) of neighbor positions (a sum of Dirac delta functions) is smoothed by a Gaussian kernel to produce a continuous representation of the density . The parameter $R_s$ shifts the region of sensitivity, while $\eta$ controls the radial resolution: a larger $\eta$ corresponds to a narrower Gaussian and thus higher resolution .

An **angular symmetry function** ($G^4$) is designed to capture three-body information, i.e., the [angular distribution](@entry_id:193827) of neighbors. A typical form involves triplets of atoms $(i, j, k)$ and depends on the angle $\theta_{ijk}$ as well as all three interatomic distances in the triplet:
$$
G_i^{4}(\eta, \zeta, \lambda) = 2^{1-\zeta} \sum_{j \neq i, k \neq i, j} (1+\lambda \cos\theta_{ijk})^{\zeta} \exp\left[-\eta (r_{ij}^2 + r_{ik}^2 + r_{jk}^2)\right] f_c(r_{ij}) f_c(r_{ik}) f_c(r_{jk})
$$
Here, $\zeta$ controls the [angular resolution](@entry_id:159247), and $\lambda$ is typically chosen as $+1$ or $-1$ to create functions that are sensitive to different angular ranges. The summation over all pairs of neighbors $(j, k)$ ensures [permutation invariance](@entry_id:753356) .

### Advanced Construction: Invariants from Equivariant Representations

While building descriptors from invariants is intuitive, a more powerful and systematic approach involves first constructing an **equivariant** representation of the atomic environment and then deriving invariant features from it. This is the core idea behind many modern descriptors, such as the Smooth Overlap of Atomic Positions (SOAP).

The process begins by representing the atomic neighborhood not as a [discrete set](@entry_id:146023) of points, but as a continuous **neighbor density field**. This is done by placing a smooth, localized function, typically a Gaussian, at the position of each neighboring atom $j$:
$$
\rho_i(\mathbf{r}) = \sum_{j \neq i} w_{s_j} \exp\left(-\frac{\|\mathbf{r} - \mathbf{r}_j\|^2}{2\sigma^2}\right)
$$
Here, $\mathbf{r}$ is a point in space relative to the central atom $i$, and $\sigma$ is a smearing width. The choice of $\sigma$ represents a trade-off: a small $\sigma$ yields high spatial resolution but creates a representation with significant high-frequency components, requiring a larger basis set to describe. A large $\sigma$ acts as a low-pass filter, simplifying the representation at the cost of losing fine structural detail .

The next step is to expand this density field $\rho_i(\mathbf{r})$ in a complete, orthonormal basis that has well-defined transformation properties under rotation. A natural choice for a 3D field is a product basis of radial functions $R_{nl}(r)$ and **[spherical harmonics](@entry_id:156424)** $Y_{lm}(\hat{\mathbf{r}})$:
$$
\rho_i(\mathbf{r}) = \sum_{n,l,m} c_{nlm}^{(i)} R_{nl}(r) Y_{lm}(\hat{\mathbf{r}})
$$
The expansion coefficients $c_{nlm}^{(i)}$ form an equivariant representation of the neighbor density. Under a rotation of the environment, the coefficients for a given $(n,l)$ transform among themselves according to the [irreducible representations](@entry_id:138184) of the [rotation group](@entry_id:204412), the Wigner D-matrices $D^{(l)}$ .

The final step is to construct rotationally invariant features from these equivariant coefficients. This is achieved by forming the **power spectrum**, which is an inner product of the coefficient vectors for different radial channels $(n, n')$ within each angular momentum channel $l$:
$$
p_{nn'l}^{(i)} = \sum_{m=-l}^{l} c_{nlm}^{(i)} c_{n'lm}^{(i)*}
$$
Because the Wigner D-matrices are unitary, this inner product is invariant under rotation. The proof relies on the fact that the rotation matrices cancel out due to the [unitarity](@entry_id:138773) condition $\mathbf{D}^{(l)}\mathbf{D}^{(l)\dagger} = \mathbf{I}$ . The resulting set of power spectrum components $\{p_{nn'l}^{(i)}\}$ forms the SOAP descriptor. It is systematically improvable (by increasing the number of basis functions) and has been shown to be a highly effective representation for a wide range of materials.

### The Goal of Descriptor Design: Completeness

The ultimate theoretical goal of descriptor design is to create a **complete** representation. A descriptor $\phi$ is said to be complete if it provides a unique fingerprint for every physically distinct atomic configuration. More formally, this means that two configurations, $X$ and $Y$, produce the same descriptor vector if and only if they are equivalent up to the [fundamental symmetries](@entry_id:161256) of translation, rotation, and permutation of identical species .
$$
\phi(X) = \phi(Y) \iff X \sim Y
$$
This condition has two parts:
1.  **Invariance ($\implies$)**: If two configurations are symmetrically equivalent ($X \sim Y$), they must have the same descriptor. This is the basic symmetry requirement discussed throughout this chapter.
2.  **Uniqueness ($\impliedby$)**: If two configurations have the same descriptor, they must be symmetrically equivalent. This ensures that the descriptor does not accidentally map two physically distinct environments to the same representation.

Achieving full completeness is a challenging theoretical and practical goal. Descriptors like SOAP have been proven to be complete, meaning they can distinguish any two non-equivalent environments given a sufficiently large basis set. In practice, however, one must always truncate the basis, leading to a trade-off between the descriptor's completeness, its computational cost, and the complexity of the machine learning model that will utilize it. The principles and mechanisms outlined in this chapter provide the essential toolkit for navigating these trade-offs and engineering robust, physically grounded, and effective descriptors for multiscale modeling and analysis.