## Introduction
Equation-of-Motion Coupled-Cluster (EOM-CC) theory stands as a pillar of modern quantum chemistry, offering a powerful and accurate framework for investigating the world beyond the electronic ground state. Its ability to describe [electronic excitations](@entry_id:190531), [ionization](@entry_id:136315), and electron attachment with high fidelity has made it an indispensable tool for interpreting complex spectroscopic data, unraveling [photochemical reaction](@entry_id:195254) mechanisms, and designing novel materials. The challenge in computational chemistry is not just to describe the ground state accurately, but to do so for a diverse array of electronic states in a balanced and physically sound manner. EOM-CC addresses this gap by building upon the robust foundation of ground-state [coupled-cluster theory](@entry_id:141746), providing a systematically improvable and size-intensive approach to excited-state problems that elude simpler methods.

This article provides a comprehensive journey into the EOM-CC formalism. In the first chapter, **Principles and Mechanisms**, we will dissect the theoretical core of the method, from the [exponential ansatz](@entry_id:176399) to the non-Hermitian [eigenvalue problem](@entry_id:143898) that defines it. Following this, the chapter on **Applications and Interdisciplinary Connections** will showcase the method's versatility, demonstrating how it is applied to solve real-world problems in spectroscopy, photochemistry, and materials science. Finally, the **Hands-On Practices** section will provide you with practical exercises to reinforce your understanding of the key computational concepts, solidifying the bridge between theory and application.

## Principles and Mechanisms

This chapter delves into the theoretical foundations and operational mechanisms of the Equation-of-Motion Coupled-Cluster (EOM-CC) framework. We will begin by examining the structure of the [coupled-cluster](@entry_id:190682) ground state, which serves as the reference for all subsequent EOM calculations. From there, we will derive the central EOM-CC eigenvalue equation, explore its properties, and discuss its implementation and practical application for various types of [electronic states](@entry_id:171776).

### The Coupled-Cluster Ground State: An Exponential Ansatz

The accuracy and properties of EOM-CC theory are intrinsically linked to the underlying description of the electronic ground state. In single-reference [coupled-cluster theory](@entry_id:141746), the correlated ground state wavefunction, $\vert \Psi_0 \rangle$, is constructed by applying an exponential wave operator to a single-determinant reference, typically the Hartree-Fock (HF) determinant $\vert \Phi_0 \rangle$. This relationship is expressed as:

$\vert \Psi_0 \rangle = e^{\hat{T}} \vert \Phi_0 \rangle$

The operator $\hat{T}$ is known as the **cluster operator**. It is a linear combination of excitation operators that generate all possible [particle-hole excitations](@entry_id:137289) from the reference determinant. It is formally written as a sum:

$\hat{T} = \hat{T}_1 + \hat{T}_2 + \hat{T}_3 + \dots$

where $\hat{T}_n$ is the operator that generates all $n$-tuple excitations. For example, $\hat{T}_1$ and $\hat{T}_2$ are given by:

$\hat{T}_1 = \sum_{i,a} t_i^a \hat{a}_a^\dagger \hat{a}_i$

$\hat{T}_2 = \frac{1}{4} \sum_{i,j,a,b} t_{ij}^{ab} \hat{a}_a^\dagger \hat{a}_b^\dagger \hat{a}_j \hat{a}_i$

Here, the indices $i, j, \dots$ denote occupied spin-orbitals (holes) in $\vert \Phi_0 \rangle$, and $a, b, \dots$ denote virtual spin-orbitals (particles). The coefficients $t_i^a$, $t_{ij}^{ab}$, etc., are the **cluster amplitudes**, which are the unknown parameters determined by solving the CC equations.

A crucial feature of the cluster operator $\hat{T}$ is that it includes only **connected** excitation operators. An operator is connected if it cannot be written as a product of lower-rank operators. For example, $\hat{T}_2$ is connected, whereas the product of two single-excitation operators, $\hat{T}_1^2$, represents a disconnected double excitation. The power of the [exponential ansatz](@entry_id:176399) lies in its Taylor [series expansion](@entry_id:142878):

$e^{\hat{T}} = 1 + \hat{T} + \frac{1}{2!} \hat{T}^2 + \frac{1}{3!} \hat{T}^3 + \dots$

This expansion automatically and systematically generates products of the connected cluster operators. For instance, the term $\frac{1}{2}\hat{T}_1^2$ generates disconnected double excitations, the $\hat{T}_1 \hat{T}_2$ term generates disconnected triple excitations, and so on. This elegant structure is the basis of the **Linked-Cluster Theorem**. When applied to the CC energy expression, this theorem guarantees that all contributions from disconnected diagrams cancel out, leaving an energy expression that depends only on connected diagrams. This property ensures that the CC energy is **size-extensive**: for a system of two non-interacting fragments, $A$ and $B$, the total energy is the sum of the energies of the individual fragments, $E_{AB} = E_A + E_B$. This holds true for any level of truncation of the cluster operator $\hat{T}$ [@problem_id:2772692] [@problem_id:2772666].

This is a profound advantage over truncated Configuration Interaction (CI) methods. In a truncated CI expansion, such as CI with Singles and Doubles (CISD), the wavefunction is a linear combination of determinants. For a non-interacting system $A+B$, the CISD space does not include simultaneous excitations on both fragments (e.g., a single on $A$ and a single on $B$, which is a double on $AB$). This omission of necessary product terms means that truncated CI is not size-extensive, a significant deficiency that worsens as system size increases [@problem_id:2772666].

### The Equation-of-Motion for Excited States

With the correlated ground state $\vert \Psi_0 \rangle = e^{\hat{T}} \vert \Phi_0 \rangle$ established, the EOM-CC method parameterizes target excited states, $\vert \Psi_k \rangle$, by applying a linear excitation operator, $\hat{R}_k$, to this ground state:

$\vert \Psi_k \rangle = \hat{R}_k e^{\hat{T}} \vert \Phi_0 \rangle = \hat{R}_k \vert \Psi_0 \rangle$

The operator $\hat{R}_k$ is a general [linear operator](@entry_id:136520) whose form determines the nature of the target state (e.g., its particle number and [spin multiplicity](@entry_id:263865)). For now, let us consider it a particle-number-conserving excitation operator. To find the [excitation energies](@entry_id:190368) $\omega_k = E_k - E_0$, where $E_0$ is the CC [ground-state energy](@entry_id:263704), we start with the time-independent Schrödinger equation for the state $\vert \Psi_k \rangle$:

$\hat{H} \vert \Psi_k \rangle = E_k \vert \Psi_k \rangle$

Substituting the EOM-CC [ansatz](@entry_id:184384) for $\vert \Psi_k \rangle$ and multiplying from the left by $e^{-\hat{T}}$ gives:

$e^{-\hat{T}} \hat{H} \hat{R}_k e^{\hat{T}} \vert \Phi_0 \rangle = E_k e^{-\hat{T}} \hat{R}_k e^{\hat{T}} \vert \Phi_0 \rangle$

Inserting the [identity operator](@entry_id:204623) $e^{\hat{T}}e^{-\hat{T}}$ after the Hamiltonian yields:

$(e^{-\hat{T}} \hat{H} e^{\hat{T}}) (e^{-\hat{T}} \hat{R}_k e^{\hat{T}}) \vert \Phi_0 \rangle = E_k (e^{-\hat{T}} \hat{R}_k e^{\hat{T}}) \vert \Phi_0 \rangle$

We define the **similarity-transformed Hamiltonian** as $\bar{H} = e^{-\hat{T}} \hat{H} e^{\hat{T}}$. The EOM-CC problem is thus equivalent to finding the eigenvalues of $\bar{H}$. A more convenient form of the working equation is obtained by recognizing that $\bar{H} \vert \Phi_0 \rangle = E_0 \vert \Phi_0 \rangle$ within the space of the reference determinant. This allows the problem to be expressed in terms of the excitation energy $\omega_k$:

$[\bar{H}, \hat{R}_k] \vert \Phi_0 \rangle = \omega_k \hat{R}_k \vert \Phi_0 \rangle$

This [commutator equation](@entry_id:143442) shows that EOM-CC is a theory for energy differences. Indeed, if the Hamiltonian is shifted by a constant $C$, such that $\hat{H}' = \hat{H} + C$, the transformed Hamiltonian becomes $\bar{H}' = \bar{H} + C$. Since a constant commutes with any operator, the commutator is unchanged, $[ \bar{H}', \hat{R}_k] = [\bar{H}, \hat{R}_k]$, and the [excitation energies](@entry_id:190368) $\omega_k$ are invariant to such a shift [@problem_id:2889801].

### The Non-Hermitian Eigenvalue Problem

A defining characteristic of EOM-CC is that it leads to a **non-Hermitian [eigenvalue problem](@entry_id:143898)**. The similarity-transformed Hamiltonian, $\bar{H} = e^{-\hat{T}} \hat{H} e^{\hat{T}}$, is generally non-Hermitian even though the original Hamiltonian $\hat{H}$ is Hermitian. This arises because the transformation operator $e^{\hat{T}}$ is not unitary. A [unitary transformation](@entry_id:152599) requires that the operator in the exponent be anti-Hermitian, i.e., $\hat{T}^\dagger = -\hat{T}$. However, the cluster operator $\hat{T}$ is composed exclusively of excitation operators. Its adjoint, $\hat{T}^\dagger$, is composed exclusively of de-excitation operators. Since $\hat{T}^\dagger \neq -\hat{T}$, the transformation is non-unitary, and the Hermiticity of $\hat{H}$ is not preserved [@problem_id:2772698].

It is crucial to understand that this non-Hermiticity is an intrinsic feature of the standard CC ansatz, not an artifact of truncating $\hat{T}$ at a finite excitation level. Even if $\hat{T}$ were to include all possible excitations (the Full CI limit), it would still be a pure excitation operator, and $\bar{H}$ would remain non-Hermitian [@problem_id:2772698].

This non-Hermiticity has several important consequences:

1.  **Distinct Left and Right Eigenvectors**: A non-Hermitian operator possesses distinct sets of [left and right eigenvectors](@entry_id:173562). The operator $\hat{R}_k$ we have been discussing is the right excitation operator. There exists a corresponding left excitation operator, $\hat{L}_k$, which is the solution to the left-[eigenvalue problem](@entry_id:143898): $\langle \Phi_0 \vert \hat{L}_k \bar{H} = \omega_k \langle \Phi_0 \vert \hat{L}_k$. The [left and right eigenvectors](@entry_id:173562) corresponding to different eigenvalues are biorthogonal: $\langle \Psi_L^j \vert \Psi_R^k \rangle = \langle \Phi_0 \vert \hat{L}_j \hat{R}_k \vert \Phi_0 \rangle \propto \delta_{jk}$.

2.  **Non-Variational Energies**: The variational principle, which guarantees that energies calculated from an approximate wavefunction are [upper bounds](@entry_id:274738) to the true energies, applies only to Hermitian [eigenvalue problems](@entry_id:142153). Since the EOM-CC method diagonalizes the non-Hermitian operator $\bar{H}$, the resulting [excitation energies](@entry_id:190368) are **not variational** [@problem_id:2889801].

Despite being non-Hermitian, $\bar{H}$ possesses a property that ensures physically meaningful solutions. By construction, $\bar{H}$ is related to the original Hamiltonian $\hat{H}$ by a similarity transformation. A [fundamental theorem of linear algebra](@entry_id:190797) states that a similarity transformation preserves the [spectrum of an operator](@entry_id:272027). Therefore, $\bar{H}$ is **isospectral** to $\hat{H}$. Since $\hat{H}$ is Hermitian, its eigenvalues (the exact energies of the system) are all real. Consequently, the exact eigenvalues of $\bar{H}$ must also be real. This provides the formal justification for obtaining real [excitation energies](@entry_id:190368) from a non-Hermitian quantum chemical theory [@problem_id:2772698].

### Size-Intensivity of Excitation Energies

A paramount advantage of EOM-CC is that its [excitation energies](@entry_id:190368) are **size-intensive**. This means that the energy of an excitation localized on one part of a system is independent of the size of another, non-interacting part of the system. This property is inherited directly from the size-extensive nature of the CC ground state.

To prove this, let us consider a system composed of two non-interacting fragments, $A$ and $B$. The total Hamiltonian is separable, $\hat{H} = \hat{H}_A + \hat{H}_B$, and the reference determinant is a product, $\vert \Phi_0 \rangle = \vert \Phi_0^A \rangle \otimes \vert \Phi_0^B \rangle$. Because the fragments do not interact, the CC equations decouple, and the total cluster operator is a simple sum: $\hat{T} = \hat{T}_A + \hat{T}_B$. Since operators acting on different fragments commute (e.g., $[\hat{H}_A, \hat{T}_B] = 0$), the similarity-transformed Hamiltonian also becomes separable [@problem_id:2455498]:

$\bar{H} = e^{-(\hat{T}_A + \hat{T}_B)} (\hat{H}_A + \hat{H}_B) e^{(\hat{T}_A + \hat{T}_B)} = (e^{-\hat{T}_A} \hat{H}_A e^{\hat{T}_A}) + (e^{-\hat{T}_B} \hat{H}_B e^{\hat{T}_B}) = \bar{H}_A + \bar{H}_B$

Now, consider an excitation localized entirely on fragment $A$. The corresponding excitation operator will also be localized on $A$, so $\hat{R}_k = \hat{R}_A$. The EOM-CC eigenvalue equation becomes:

$[\bar{H}_A + \bar{H}_B, \hat{R}_A] \vert \Phi_0^A \Phi_0^B \rangle = \omega_k \hat{R}_A \vert \Phi_0^A \Phi_0^B \rangle$

Since $\bar{H}_B$ and $\hat{R}_A$ act on different subspaces, they commute, and the equation simplifies to:

$([\bar{H}_A, \hat{R}_A] \vert \Phi_0^A \rangle) \otimes \vert \Phi_0^B \rangle = \omega_k (\hat{R}_A \vert \Phi_0^A \rangle) \otimes \vert \Phi_0^B \rangle$

This is precisely the EOM-CC equation for the isolated fragment $A$. The resulting excitation energy $\omega_k$ is identical to that of fragment $A$ alone, completely independent of the presence of the spectator fragment $B$. This proves that EOM-CC [excitation energies](@entry_id:190368) are size-intensive at any level of truncation. This property is essential for obtaining physically reliable results for large molecules and extended systems [@problem_id:2455498].

### The Fock-Space Hierarchy: EE, IP, and EA

The EOM framework is remarkably flexible. By choosing different forms for the [linear operator](@entry_id:136520) $\hat{R}_k$, one can target states in different sectors of the **Fock space** (the space of all possible electron numbers). The particle number of the target state $\vert \Psi_k \rangle = \hat{R}_k e^{\hat{T}} \vert \Phi_0 \rangle$ relative to the $N$-electron reference is determined entirely by the structure of $\hat{R}_k$, since the ground-state operator $e^{\hat{T}}$ is particle-number conserving [@problem_id:2772686]. This leads to a family of EOM-CC methods:

*   **EOM-EE (Excitation Energies)**: This is the variant we have discussed so far. To target $N$-electron [excited states](@entry_id:273472), $\hat{R}_k$ must be a particle-number-conserving operator. It is therefore constructed from a linear combination of particle-hole excitation operators: $1h1p, 2h2p, \dots$. The eigenvalues are [vertical excitation](@entry_id:200515) energies.

*   **EOM-IP (Ionization Potentials)**: To target $(N-1)$-electron states (cations), $\hat{R}_k$ must be an operator that effectively removes one electron. It is constructed from operators that have one more [annihilation operator](@entry_id:149476) than [creation operators](@entry_id:191512). The leading term is a one-hole ($1h$) operator, which annihilates an electron from an occupied orbital. Higher-rank terms include $2h1p, 3h2p, \dots$ operators, which correspond to ionization accompanied by excitation. The eigenvalues are vertical ionization potentials.

*   **EOM-EA (Electron Affinities)**: To target $(N+1)$-electron states (anions), $\hat{R}_k$ must be an operator that effectively adds one electron. It is constructed from operators that have one more [creation operator](@entry_id:264870) than [annihilation operators](@entry_id:180957). The leading term is a one-particle ($1p$) operator, which adds an electron to a virtual orbital. Higher-rank terms include $2p1h, 3p2h, \dots$ operators, corresponding to electron attachment accompanied by excitation. The eigenvalues are vertical electron affinities.

This unified Fock-space approach is one of the most powerful features of EOM-CC theory, allowing for a balanced and consistent description of various types of [electronic states](@entry_id:171776) within a single theoretical framework [@problem_id:2772686].

### Practical Implementation: EOM-CCSD

The most widely used variant of EOM-CC is **EOM-EE-CCSD**, which builds upon a ground state described by Coupled-Cluster Singles and Doubles (CCSD). In this model, the cluster operator is truncated at double excitations, $\hat{T} \approx \hat{T}_1 + \hat{T}_2$. For a consistent description, the excitation operator is also truncated at the same level: $\hat{R}_k \approx c_0 + \hat{R}_1 + \hat{R}_2$. For excited states, the constant term $c_0$ is zero, so the operator manifold is spanned by single ($1p1h$) and double ($2p2h$) excitations [@problem_id:2772708].

Even with this truncation, the resulting EOM-CCSD wavefunction $\vert \Psi_k \rangle = (\hat{R}_1 + \hat{R}_2)e^{\hat{T}_1+\hat{T}_2}\vert \Phi_0 \rangle$ is highly complex. Due to the exponential operator, the wavefunction contains contributions from determinants with excitation ranks far beyond doubles. For instance, the term $\hat{R}_2 (\frac{1}{2}\hat{T}_2^2) \vert \Phi_0 \rangle$ can generate up to six-fold excitations. This implicit inclusion of higher-rank excitations is key to the method's high accuracy [@problem_id:2889801].

The EOM-CCSD [eigenvalue problem](@entry_id:143898) is solved in the space of all singly and doubly excited determinants. For a molecule of even moderate size, the dimension of this space can be enormous ($10^6$ to $10^9$ or more), making the explicit construction and [diagonalization](@entry_id:147016) of the $\bar{H}$ matrix computationally impossible. Instead, the eigenvalues are found using **[iterative eigensolvers](@entry_id:193469)**, such as the **Davidson algorithm** [@problem_id:2772675].

These algorithms are designed to find a small number of eigenvalues (e.g., the lowest few) without ever storing the full matrix. The core computational step is the [matrix-vector product](@entry_id:151002), or **sigma-vector build**: $\vec{\sigma} = \bar{H} \vec{r}$, where $\vec{r}$ is a trial vector of excitation amplitudes. This product is computed "on-the-fly" by evaluating the action of the constituent terms of the Baker-Campbell-Hausdorff expansion of $\bar{H}$ on $\vec{r}$, a process typically implemented with efficient diagrammatic techniques. The computational cost of finding a few states is thus dominated by a small number of these sigma-vector builds, making the problem tractable [@problem_id:2772675]. To accelerate convergence, these [iterative methods](@entry_id:139472) employ a **[preconditioner](@entry_id:137537)**, which is an approximation to the inverse of $(\omega \mathbf{I} - \bar{H})$. A common and effective choice for the [preconditioner](@entry_id:137537) is the diagonal of this matrix, which, in a canonical HF basis, is simply approximated by orbital energy differences (e.g., $\epsilon_a - \epsilon_i$ for a single excitation) [@problem_id:2772675].

### Accuracy, Limitations, and Beyond

EOM-EE-CCSD is a highly successful method, often providing [excitation energies](@entry_id:190368) for states dominated by single-excitation character with an accuracy of $0.1-0.3$ eV. However, it can struggle to provide a balanced description for all types of [excited states](@entry_id:273472).

A notable challenge arises for states with dominant **double-excitation character** [@problem_id:2772655]. While the EOM-CCSD operator manifold explicitly includes the $\hat{R}_2$ operator required to describe such states, the calculated energies are often significantly less accurate than for singly-[excited states](@entry_id:273472). The root cause of this imbalance lies in the truncation of the ground-state cluster operator. The CCSD ground state, with $\hat{T} \approx \hat{T}_1 + \hat{T}_2$, provides an excellent description of dynamic correlation for the reference determinant. However, the doubly-excited determinants are themselves in need of correlation, primarily through coupling to triply-excited determinants. The operators that describe this coupling in $\bar{H}$ depend on the triple-excitation cluster operator, $\hat{T}_3$. Since $\hat{T}_3$ is absent in the CCSD approximation, the doubles block of the $\bar{H}$ matrix is effectively "under-correlated," leading to an unbalanced description and larger errors for doubly-excited states [@problem_id:2772655].

The systematic way to remedy this is to include higher-rank operators, such as moving to EOM-CCSDT ($\hat{T} = \hat{T}_1+\hat{T}_2+\hat{T}_3$, $\hat{R} = \hat{R}_1+\hat{R}_2+\hat{R}_3$). However, the iterative cost of CCSDT is prohibitively high for most applications. A more pragmatic approach is to estimate the effect of triple excitations using **non-iterative corrections** [@problem_id:2772656].

These methods are typically based on a perturbative treatment of the triples space. One can partition the excitation space into the [model space](@entry_id:637948) $P$ (singles and doubles) and the complementary space $Q$ (triples). The effect of the $Q$ space on an EOM-CCSD energy $\omega_k$ is then calculated perturbatively. Methods like **CR-EOMCC(2,3)** compute a state-specific, additive correction to the EOM-CCSD energy. This correction depends on the left and right EOM-CCSD eigenvectors for the state of interest and an approximate energy denominator (resolvent). The correction formula is constructed to approximate the effects of both $\hat{T}_3$ in the ground state and $\hat{R}_3$ in the excited state, without ever solving the expensive iterative equations for the corresponding amplitudes. The "CR" (Completely Renormalized) designation refers to a specific formulation that includes extra terms to ensure the final corrected energy remains size-intensive. Such non-iterative corrections provide a powerful and cost-effective route to improving the accuracy of EOM-CCSD, particularly for challenging cases like states with significant double-excitation character [@problem_id:2772656].