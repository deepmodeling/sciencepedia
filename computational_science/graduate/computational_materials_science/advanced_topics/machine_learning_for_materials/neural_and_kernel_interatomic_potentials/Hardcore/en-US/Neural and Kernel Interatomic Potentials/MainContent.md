## Introduction
In the quest to understand and design materials from the atom up, computational simulation plays a pivotal role. However, a fundamental challenge persists: the trade-off between accuracy and computational cost. While first-principles methods like Density Functional Theory (DFT) offer high fidelity, they are too computationally expensive for large systems or long timescales. Conversely, classical empirical potentials are fast but often lack the accuracy and transferability to describe complex chemical bonding and reactions. Neural and kernel [interatomic potentials](@entry_id:177673) have emerged as a revolutionary solution, bridging this gap by using machine [learning to learn](@entry_id:638057) the potential energy surface directly from quantum mechanical data, combining the accuracy of first principles with the efficiency of classical models.

This article provides a graduate-level exploration of the theoretical foundations, practical applications, and advanced frontiers of these powerful computational tools. It addresses the knowledge gap between the abstract concepts of machine learning and their concrete implementation for physical simulation. The reader will gain a comprehensive understanding of how these potentials are constructed, validated, and applied to solve real-world problems in science and engineering.

We will begin in the **Principles and Mechanisms** chapter by dissecting the core hypotheses of locality and additivity, exploring the non-negotiable role of physical symmetries, and detailing the mathematical machinery used to encode atomic environments into machine-learnable representations. Next, the **Applications and Interdisciplinary Connections** chapter demonstrates how these models are used to predict macroscopic material properties, simulate complex reactive dynamics, and tackle the critical challenges of model reliability through [uncertainty quantification](@entry_id:138597) and active learning. Finally, the **Hands-On Practices** section provides a series of conceptual problems designed to solidify your understanding of key theoretical and practical aspects discussed throughout the article.

## Principles and Mechanisms

This chapter delves into the foundational principles and core mechanisms that underpin the construction and application of neural and kernel-based [interatomic potentials](@entry_id:177673). Building upon the introduction, we will dissect the essential hypotheses of locality and additivity, explore the non-negotiable role of physical symmetries, and detail the sophisticated mathematical machinery developed to satisfy these constraints. We will examine how atomic environments are encoded into machine-learnable representations and how different learning paradigms—from kernel regression to deep neural networks—leverage these representations to predict potential energies and forces.

### The Locality and Additivity Hypothesis

The computational efficiency of modern machine-learning [interatomic potentials](@entry_id:177673) (MLIPs) hinges on a central simplifying assumption: the **additivity** of atomic energies. This hypothesis posits that the [total potential energy](@entry_id:185512) $E$ of a system of atoms can be expressed as a sum of individual contributions from each atom:

$$E = \sum_{i} \varepsilon_i$$

where $\varepsilon_i$ is the energy assigned to atom $i$. This decomposition transforms the problem of learning a single, high-dimensional function of all atomic coordinates into the more tractable problem of learning a mapping for the energy of a single atom.

For this decomposition to be meaningful, the atomic energy $\varepsilon_i$ cannot depend on the entire system. Instead, it is assumed to be determined by the local chemical environment of atom $i$. This is the **locality hypothesis**, which formalizes the physical principle of **nearsightedness** of electronic matter. This principle, articulated by Walter Kohn, suggests that in many systems (particularly those with an [electronic band gap](@entry_id:267916)), local changes to the external potential (such as moving a single atom) have effects that decay exponentially with distance. Consequently, the energy of an atom should be primarily determined by its immediate neighbors.

Mathematically, the locality hypothesis states that there exists a universal atomic energy map $\varepsilon$ such that the energy of atom $i$ is a function of its local atomic neighborhood $\mathcal{N}_i$. This neighborhood is defined as the set of all atoms $j$ within a finite **[cutoff radius](@entry_id:136708)** $R_c$ of the central atom $i$. The input to the energy map is thus the collection of chemical species and [relative position](@entry_id:274838) vectors of these neighbors :

$$\varepsilon_i = \varepsilon(\mathcal{N}_i) = \varepsilon(\{(Z_j, \mathbf{r}_{ji}) : \|\mathbf{r}_{ji}\| \le R_c\})$$

where $Z_j$ is the species of neighbor $j$ and $\mathbf{r}_{ji} = \mathbf{r}_j - \mathbf{r}_i$ is the [relative position](@entry_id:274838) vector. The total energy is then written as $E = \sum_{i} \varepsilon(\mathcal{N}_i)$.

While powerful, this strictly local formulation has a profound limitation: it is fundamentally incapable of capturing **[long-range interactions](@entry_id:140725)** that decay algebraically with distance, such as the $1/r$ Coulomb interaction between charges or the $1/r^6$ van der Waals dispersion interaction. For a periodic ionic crystal, for instance, the total [electrostatic energy](@entry_id:267406) involves a [lattice sum](@entry_id:189839) over all periodic images. This sum is **conditionally convergent**, meaning its value depends on the order of summation, a physically ambiguous situation that reflects the influence of macroscopic boundary conditions. Simply truncating this sum at a finite cutoff $R_c$ yields an incorrect and arbitrary result .

Therefore, for systems where long-range forces are significant (e.g., [ionic solids](@entry_id:139048), polar molecules, and metals), a purely local MLIP is insufficient. The [standard solution](@entry_id:183092) is to adopt a **hybrid model** where the total energy is partitioned into a learned short-range component and an analytical long-range component:

$$E = E_{\text{short-range}}^{\text{learned}} + E_{\text{long-range}}^{\text{analytic}}$$

The short-range part, $E_{\text{short-range}}^{\text{learned}}$, is modeled by the local MLIP as described above. The long-range electrostatic part is typically handled by the **Ewald summation** technique or its efficient implementation, the Particle Mesh Ewald (PME) method. This method exactly recasts the conditionally convergent [lattice sum](@entry_id:189839) into two rapidly converging sums: one in real space, which is short-ranged and can be incorporated with the learned potential, and one in reciprocal (Fourier) space, which captures the long-range behavior. A comprehensive hybrid model for a periodic system of point charges $\{q_i\}$ thus takes the form :

$$E = \sum_{i=1}^{N} U_i(\mathbf{D}_i; R_c) + \frac{1}{2} \sum_{i,j=1}^{N} \sum_{\mathbf{n} \in \mathbb{Z}^3}' q_i q_j \frac{\text{erfc}(\sqrt{\alpha}|\mathbf{r}_i-\mathbf{r}_j+\mathbf{R_n}|)}{|\mathbf{r}_i-\mathbf{r}_j+\mathbf{R_n}|} + \frac{2\pi}{V} \sum_{\mathbf{G} \neq 0} \frac{\exp(-\frac{G^2}{4\alpha})}{G^2} \left|\sum_{k=1}^{N} q_k \exp(-i\mathbf{G}\cdot\mathbf{r}_k)\right|^2 - \frac{\sqrt{\alpha}}{\sqrt{\pi}} \sum_{i=1}^{N} q_i^2$$

Here, $U_i$ is the learned short-range energy based on a local descriptor $\mathbf{D}_i$, the second term is the short-range [real-space](@entry_id:754128) Ewald sum over [lattice vectors](@entry_id:161583) $\mathbf{R_n}$, the third is the long-range [reciprocal-space sum](@entry_id:754152) over [reciprocal lattice vectors](@entry_id:263351) $\mathbf{G}$, and the final term corrects for self-interaction. The parameter $\alpha$ controls the splitting between the real and [reciprocal space](@entry_id:139921) sums. The remainder of this chapter focuses on the construction of the learned component $U_i$.

### The Role of Fundamental Symmetries

For the atomic energy function $\varepsilon(\mathcal{N}_i)$ to be physically valid, it must respect the fundamental symmetries of space and the nature of [identical particles](@entry_id:153194). These symmetries impose strict constraints on its mathematical form .

1.  **Translation Invariance**: The laws of physics are the same everywhere. Shifting the entire system by a constant vector should not change its energy. This is naturally satisfied if the energy function $\varepsilon$ depends only on the relative positions of neighbors, $\mathbf{r}_{ji}$, and not on the absolute position of the central atom, $\mathbf{r}_i$. The definition of the local neighborhood $\mathcal{N}_i$ already enforces this.

2.  **Rotation Invariance**: The laws of physics are isotropic; they do not depend on direction. Rotating the entire system should not change its energy. Since energy is a scalar, this means that if the neighborhood $\mathcal{N}_i$ is rotated by a [rotation matrix](@entry_id:140302) $\mathbf{Q}$, the energy must remain unchanged: $\varepsilon(\mathbf{Q}\mathcal{N}_i) = \varepsilon(\mathcal{N}_i)$. This is a highly non-trivial constraint. The function $\varepsilon$ cannot depend directly on the components of the vectors $\mathbf{r}_{ji}$ but must be constructed from rotationally invariant quantities, such as interatomic distances $\|\mathbf{r}_{ji}\|$, [bond angles](@entry_id:136856) (derived from dot products like $\mathbf{r}_{ji} \cdot \mathbf{r}_{ki}$), and other scalar contractions.

3.  **Permutation Invariance**: Identical particles are indistinguishable. Swapping the labels of two neighboring atoms of the same chemical species must not change the energy. This requires $\varepsilon$ to be a symmetric function of its arguments. If it takes as input a list of neighbor descriptions, the output must be the same regardless of the order of identical neighbors in that list.

Satisfying these symmetries is the central challenge in designing MLIPs. Two dominant strategies have emerged:

*   **Invariant Descriptors**: This approach involves a two-step process. First, the Cartesian coordinates of the local neighborhood $\mathcal{N}_i$ are converted into a fixed-length vector of numbers, known as a **descriptor** or **fingerprint**. This descriptor is designed to be invariant by construction to translation, rotation, and permutation of identical neighbors. This invariant descriptor is then used as the input to a standard machine learning model, such as a kernel model or a simple feed-forward neural network, which does not need to have any special symmetry-aware architecture.

*   **Equivariant Architectures**: This more recent approach, primarily used in [graph neural networks](@entry_id:136853), builds the symmetries directly into the model's architecture. Instead of mapping coordinates to invariant scalars at the input, the network operates on geometric objects like vectors and tensors. Each layer is designed to be **equivariant**, meaning that if the input is rotated, the output features are rotated in a predictable, corresponding way. This allows the model to reason about directional information throughout its layers, only producing a final invariant scalar energy at the very end.

### Invariant Descriptors: From Functions to Tensors

The invariant descriptor approach provides a robust and modular way to build MLIPs. The key is the design of the descriptor itself, which must uniquely characterize the local environment while satisfying all required symmetries.

#### Atom-Centered Symmetry Functions

A pioneering and intuitive set of descriptors are the **Atom-Centered Symmetry Functions (ACSFs)**, introduced by Behler and Parrinello for their neural network potentials . These functions are designed to probe the radial and angular structure of the neighborhood.

The simplest type is the **[radial symmetry](@entry_id:141658) function**, often denoted $G^2$, which describes the distribution of pairwise distances:

$$G_{i}^{2}(\eta, R_{s}) = \sum_{j \neq i} \exp[-\eta(r_{ij} - R_{s})^{2}] \, f_{c}(r_{ij}; R_{c})$$

Here, the sum over all neighbors $j$ ensures [permutation invariance](@entry_id:753356). The function depends only on the interatomic distance $r_{ij}$, ensuring [rotational invariance](@entry_id:137644). The Gaussian term is centered at a distance $R_s$ with a width controlled by $\eta$, allowing the function to act as a "soft" radial distribution function bin. The **cutoff function** $f_c(r_{ij}; R_{c})$, such as $f_c(r) = \frac{1}{2}[\cos(\pi r/R_c)+1]$, ensures the descriptor smoothly goes to zero as $r_{ij}$ approaches the [cutoff radius](@entry_id:136708) $R_c$. By using a set of these functions with different parameters $(\eta, R_s)$, one can build a descriptor vector that characterizes the radial structure of the environment.

To capture three-body correlations, **angular [symmetry functions](@entry_id:177113)** like $G^4$ are used, which sum over all triplets of atoms $(i,j,k)$:

$$G_{i}^{4}(\eta, \zeta, \lambda) = 2^{1-\zeta} \sum_{j \neq i} \sum_{k \neq i, k \neq j} [1 + \lambda \cos\theta_{ijk}]^{\zeta} \exp[-\eta(r_{ij}^{2} + r_{ik}^{2} + r_{jk}^{2})] \, f_{c}(r_{ij}) f_{c}(r_{ik}) f_{c}(r_{jk})$$

This function is manifestly symmetric under the exchange of neighbors $j$ and $k$. It depends on the angle $\theta_{ijk}$ and the distances within the triplet, making it rotationally invariant. The parameter $\lambda \in \{-1, +1\}$ shifts the function's sensitivity, while the exponent $\zeta$ sharpens the [angular resolution](@entry_id:159247). A vector composed of many such $G^2$ and $G^4$ functions with various parameters forms the final invariant descriptor for the neural network.

#### Descriptors from the Atomic Neighbor Density

A more systematic approach to generating descriptors begins with the concept of an **atomic neighbor density**, $\rho_i(\mathbf{r})$. This is a field that represents the positions of all neighbors of atom $i$ as a sum of (typically Gaussian-smeared) delta functions:

$$\rho_i(\mathbf{r}) = \sum_{j \in \mathcal{N}(i)} \delta(\mathbf{r} - \mathbf{r}_{ij})$$

The **Smooth Overlap of Atomic Positions (SOAP)** descriptor, central to Gaussian Approximation Potentials (GAP), is derived from this density . The process involves expanding the neighbor density in a basis of functions that separates radial and angular components:

$$\rho_i(\mathbf{r}) = \sum_{n,l,m} c_{nlm}(i) \, g_n(r) Y_{lm}(\hat{\mathbf{r}})$$

where $g_n(r)$ are radial basis functions and $Y_{lm}(\hat{\mathbf{r}})$ are the [spherical harmonics](@entry_id:156424). The expansion coefficients $c_{nlm}(i)$ capture the full geometric information of the neighborhood. To achieve [rotational invariance](@entry_id:137644), one constructs the **power spectrum**, which involves summing over the [magnetic quantum number](@entry_id:145584) $m$ for a fixed angular momentum channel $l$:

$$p_{nn'l}(i) = \sum_{m=-l}^{l} c_{nlm}(i) \, c_{n'lm}^{*}(i)$$

This operation effectively integrates out the orientation of the environment, yielding a set of rotationally invariant numbers. The collection of all such power spectrum components $\{p_{nn'l}(i)\}$ forms the SOAP descriptor vector. This descriptor can then be used in any machine learning model. For example, in [kernel methods](@entry_id:276706), the similarity between two environments $A$ and $B$ is measured by a [kernel function](@entry_id:145324), such as a normalized dot product of their power spectrum vectors .

#### Moment Tensor Potentials

An even more general and mathematically rigorous framework for constructing invariants is provided by **Moment Tensor Potentials (MTPs)**. This approach starts by defining **moment tensors** of the local atomic neighborhood :

$$M_{\mu,\nu} = \sum_{j \in \mathcal{N}(i)} f_{\mu}(r_{ij}) \,\underbrace{\mathbf{r}_{ij} \otimes \cdots \otimes \mathbf{r}_{ij}}_{\nu \text{ times}}$$

Here, $f_{\mu}(r)$ are radial basis functions, and $\otimes$ denotes the [outer product](@entry_id:201262). $M_{\mu,\nu}$ is a symmetric tensor of rank $\nu$. Under a rotation $\mathbf{R}$, these tensors transform covariantly. To obtain the required [scalar invariants](@entry_id:193787) for an energy model, one constructs all possible independent full contractions of these tensors. For example:

*   The trace of a rank-2 moment tensor is an invariant: $\text{Tr}(M_{\mu,2}) = \sum_{\alpha} M_{\mu,2;\alpha\alpha} = \sum_{j} f_{\mu}(r_{ij}) \|\mathbf{r}_{ij}\|^2$.
*   The inner product of two rank-1 moment tensors (vectors) is an invariant: $M_{\mu,1} \cdot M_{\nu,1} = \sum_{j,k} f_{\mu}(r_{ij}) f_{\nu}(r_{ik}) (\mathbf{r}_{ij} \cdot \mathbf{r}_{ik})$.
*   The Frobenius inner product of two rank-2 tensors is an invariant: $\sum_{\alpha,\beta} M_{\mu,2;\alpha\beta} M_{\nu,2;\alpha\beta} = \sum_{j,k} f_{\mu}(r_{ij}) f_{\nu}(r_{ik}) (\mathbf{r}_{ij} \cdot \mathbf{r}_{ik})^2$.

By systematically generating these scalar contractions up to a certain [tensor rank](@entry_id:266558) and number of products, one can construct a complete basis of polynomial invariants of the atomic neighborhood. This provides a powerful and extensible foundation for descriptor design.

### Equivariant Neural Networks

Instead of discarding directional information at the input by using invariant descriptors, **[equivariant neural networks](@entry_id:137437)** process geometric information throughout the model. The key concept is **[equivariance](@entry_id:636671)**. A function $f$ is equivariant with respect to a transformation group (like rotations) if transforming the input and then applying the function is equivalent to applying the function and then transforming the output.

For a rotation $\mathbf{R}$, an equivariant layer $f$ processing a set of features $\{\mathbf{u}_i\}$ satisfies:

$$f(\{\mathbf{R}\mathbf{u}_i\}) = \mathbf{R}f(\{\mathbf{u}_i\})$$ (for vector features)

More generally, these networks operate on features that are **irreducible representations** of the rotation group $\mathrm{SO}(3)$, also known as spherical tensors of type-$l$. A type-$l$ feature $\mathbf{u}^{(l)}$ is a vector in $\mathbb{C}^{2l+1}$ that transforms under rotation via the $(2l+1) \times (2l+1)$ **Wigner D-matrix**, $D^{(l)}(\mathbf{R})$:

$$\mathbf{u}^{(l)} \mapsto D^{(l)}(\mathbf{R}) \mathbf{u}^{(l)}$$

Scalars are type-0 features, vectors are type-1, and so on. Equivariant networks, such as E(3)-equivariant [message-passing](@entry_id:751915) neural networks, are constructed from operations that respect these transformation rules . For example, the **tensor product** of two spherical tensors of type $l_1$ and $l_2$ produces a new set of tensors with types ranging from $|l_1 - l_2|$ to $l_1 + l_2$. By carefully combining features from neighboring atoms (e.g., by taking tensor products with [spherical harmonics](@entry_id:156424) of the [relative position](@entry_id:274838) vectors), the network can pass messages and update atomic features while ensuring that all features maintain a well-defined tensorial type. This allows the model to explicitly represent and reason with directional and anisotropic information, which is lost in invariant models. The final energy, a scalar, is obtained at the output layer by ensuring the final feature has type-$l=0$.

### Learning Algorithms and Model Properties

Once a suitable representation of the atomic environment is chosen, a learning algorithm is needed to map these representations to energies.

#### Kernel-Based Learning: Gaussian Process Regression

Kernel-based methods, such as **Gaussian Approximation Potentials (GAP)**, are [non-parametric models](@entry_id:201779) that rely on a **[kernel function](@entry_id:145324)** $K(\mathcal{N}_i, \mathcal{N}_j)$ to measure the similarity between two atomic environments. The SOAP descriptor, for instance, is typically used within a kernel framework. The predicted energy of a new environment is a kernel-weighted sum of the energies of training environments.

The underlying statistical framework is **Gaussian Process (GP) regression** . In this paradigm, the atomic energy function $\varepsilon(\mathcal{N})$ is assumed to be a draw from a Gaussian Process prior, which is a distribution over functions defined by a mean function (usually zero) and a [covariance function](@entry_id:265031), which is the kernel $k$. Given a set of training environments $\{\mathbf{x}_i\}$ (where $\mathbf{x}_i$ is the descriptor for environment $i$) and corresponding noisy energy labels $\{y_i\}$, the GP framework provides a [closed-form expression](@entry_id:267458) for the posterior distribution of the energy $f_* = \varepsilon(\mathbf{x}_*)$ of a new environment $\mathbf{x}_*$. The posterior mean and variance are given by:

$$m_* = k_*^T (K + \sigma^2 I)^{-1} y$$

$$s_*^2 = k_{**} - k_*^T (K + \sigma^2 I)^{-1} k_*$$

where $K$ is the kernel matrix of the training data, $k_*$ is the vector of kernel similarities between the new point and the training points, $k_{**}$ is the [self-similarity](@entry_id:144952) of the new point, and $\sigma^2$ is the variance of the observation noise. The [posterior mean](@entry_id:173826) $m_*$ provides the energy prediction, while the posterior variance $s_*^2$ offers a powerful, built-in measure of the model's uncertainty about its prediction.

#### The Concept of Body-Order

A crucial physical property of any potential is its **body-order**, which describes how many particles are involved in a fundamental interaction term. A [pairwise potential](@entry_id:753090) is 2-body, while an angle-dependent potential must be at least 3-body. MLIPs based on local environment descriptors are intrinsically many-body, as the energy of one atom depends on all neighbors within its cutoff sphere. The specific functional form of the model determines the maximum body-order it can represent.

For example, consider a SOAP-based kernel of the form $K(i, k) = (\sum_{n,n',l} p_{nn'l}(i) \, p_{nn'l}(k))^{\zeta}$, where $p(i)$ is the power spectrum of environment $i$. The [power spectrum](@entry_id:159996) itself is constructed from products of expansion coefficients, $c_{nlm}(i) \propto \sum_j \dots$, making it a 3-body interaction (central atom plus two neighbors). The kernel involves a product of two power spectra, $p(i)p(k)$. When raised to the power $\zeta$, a single term in the expansion of $K$ will contain $\zeta$ products of the form $p(i)p(k)$. Therefore, the final energy expression for atom $i$ will involve terms that depend on up to $2\zeta$ distinct neighbors, meaning the potential has a maximum **body-order** of $2\zeta+1$ . This shows a direct link between the mathematical form of the kernel and the complexity of the [many-body interactions](@entry_id:751663) the model can capture.

#### The Connection Between Kernels and Neural Networks

While [kernel methods](@entry_id:276706) and neural networks appear to be distinct modeling paradigms, a deep theoretical connection exists between them. The **Neural Tangent Kernel (NTK)** theorem shows that in the limit of infinite width, a neural network trained with [gradient descent](@entry_id:145942) behaves exactly like a kernel machine . The specific kernel for this equivalent machine is the NTK, $\Theta(\mathbf{z}, \mathbf{z}')$, which is determined by the neural network's architecture.

This implies that a Gaussian Approximation Potential using a kernel $k$ and an infinitely wide neural network using the same descriptor space will produce identical predictions for any dataset if and only if their respective kernels are proportional, i.e., $k(\mathbf{z}, \mathbf{z}') \propto \Theta(\mathbf{z}, \mathbf{z}')$. This remarkable result unifies the two fields, showing that choices in neural [network architecture](@entry_id:268981) implicitly define a kernel that governs the function learned by the network. It provides a powerful lens through which to understand the function space explored by wide neural networks and to bridge the gap between the predictive power of deep learning and the analytical tractability of [kernel methods](@entry_id:276706).