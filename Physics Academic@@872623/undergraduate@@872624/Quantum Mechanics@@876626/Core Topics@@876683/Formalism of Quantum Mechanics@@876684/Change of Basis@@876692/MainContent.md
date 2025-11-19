## Introduction
In quantum mechanics, physical systems are described by abstract state vectors in a Hilbert space. While this provides a powerful, coordinate-free picture, practical calculations require a concrete numerical representation, which is achieved by choosing a basis. Just as a point's location is unchanged whether we use Cartesian or [polar coordinates](@entry_id:159425), the underlying physics of a quantum state is independent of the basis we choose to describe it. The ability to seamlessly translate our description from one basis to another is therefore not just a mathematical convenience, but a fundamental skill for solving physical problems and gaining deeper insight. This article provides a comprehensive guide to mastering the change of basis.

Across the following chapters, you will build a complete understanding of this essential tool. The "Principles and Mechanisms" chapter will lay the mathematical foundation, explaining how to transform the components of state vectors and the [matrix representations](@entry_id:146025) of operators. You will learn about the central role of unitary matrices and discover which [physical quantities](@entry_id:177395) remain invariant. Next, the "Applications and Interdisciplinary Connections" chapter will showcase the power of this formalism, demonstrating how changing basis is used to interpret measurements, solve for [quantum dynamics](@entry_id:138183), analyze multi-particle entanglement, and even connect quantum theory to fields like chemistry and economics. Finally, "Hands-On Practices" will allow you to solidify your knowledge by tackling practical problems, ensuring you can apply these concepts effectively.

## Principles and Mechanisms

In the study of quantum mechanics, a physical state is represented by an abstract state vector $|\psi\rangle$ residing in a [complex vector space](@entry_id:153448) known as a Hilbert space. While this abstract representation is powerful, practical calculations demand a concrete set of numbers to work with. This is achieved by choosing a basis for the Hilbert space. The choice of basis is a matter of convenience and does not alter the underlying physics, much like choosing between Cartesian or [polar coordinates](@entry_id:159425) does not change the location of a point in a plane. The ability to seamlessly translate our description of states and operators from one basis to another is therefore a fundamental skill. This chapter details the principles and mechanisms governing these transformations.

### Representing Quantum States and the Completeness Relation

An **orthonormal basis** is a set of state vectors, which we can denote by $\{|u_i\rangle\}$, that are mutually orthogonal and normalized. That is, they satisfy the condition $\langle u_i | u_j \rangle = \delta_{ij}$, where $\delta_{ij}$ is the Kronecker delta. Any [state vector](@entry_id:154607) $|\psi\rangle$ in the Hilbert space can be expressed as a unique [linear combination](@entry_id:155091) of these basis vectors:

$$|\psi\rangle = \sum_{i} c_i |u_i\rangle$$

The complex coefficients $c_i$ are called the **components** or **amplitudes** of $|\psi\rangle$ in the $\{|u_i\rangle\}$ basis. These components are found by taking the inner product of the basis vectors with the state vector: $c_i = \langle u_i | \psi \rangle$. The collection of these components, often arranged into a column vector $\vec{c}$, serves as the concrete representation of the abstract state $|\psi\rangle$.

The ability to expand any state in this manner is guaranteed by a fundamental property of any orthonormal basis known as the **[completeness relation](@entry_id:139077)** or **[closure relation](@entry_id:747393)**. This relation states that the sum of the outer products of all basis vectors equals the identity operator $\hat{I}$:

$$\sum_{i} |u_i\rangle\langle u_i| = \hat{I}$$

The operator $|u_i\rangle\langle u_i|$ is a **projection operator** that projects any [state vector](@entry_id:154607) onto the direction of $|u_i\rangle$. The [completeness relation](@entry_id:139077) thus asserts that the sum of projections onto all basis directions reconstructs the identity. We can see its utility immediately by applying it to an arbitrary state $|\psi\rangle$:

$$|\psi\rangle = \hat{I}|\psi\rangle = \left( \sum_{i} |u_i\rangle\langle u_i| \right) |\psi\rangle = \sum_{i} |u_i\rangle (\langle u_i | \psi \rangle) = \sum_{i} c_i |u_i\rangle$$

This formally derives the expansion of a [state vector](@entry_id:154607). A simple yet crucial application involves checking the consistency of a set of eigenvectors for an observable. For instance, for a spin-1/2 particle, the eigenvectors of the spin-x operator, $|+\rangle_x$ and $|-\rangle_x$, form a complete [orthonormal basis](@entry_id:147779). As a result, the sum of their projectors must yield the identity matrix in any representation [@problem_id:2084024].

### Transformation of State Vector Components

A central task is to determine how the components of a [state vector](@entry_id:154607) transform when we switch from one [orthonormal basis](@entry_id:147779) to another. Suppose we have two such bases, Basis $U = \{|u_i\rangle\}$ and Basis $V = \{|v_j\rangle\}$. A state $|\psi\rangle$ has components $c_i = \langle u_i | \psi \rangle$ in Basis $U$ and components $d_j = \langle v_j | \psi \rangle$ in Basis $V$. How are the sets of components $\{c_i\}$ and $\{d_j\}$ related?

We can derive this relationship by starting with the definition of $d_j$ and inserting the [completeness relation](@entry_id:139077) for Basis $U$:

$$d_j = \langle v_j | \psi \rangle = \langle v_j | \hat{I} | \psi \rangle = \left\langle v_j \left| \left( \sum_{i} |u_i\rangle\langle u_i| \right) \right| \psi \right\rangle$$

Using the linearity of the inner product, we can rearrange this expression:

$$d_j = \sum_{i} \langle v_j | u_i \rangle \langle u_i | \psi \rangle$$

Recognizing that $\langle u_i | \psi \rangle = c_i$, we arrive at the transformation rule:

$$d_j = \sum_{i} \langle v_j | u_i \rangle c_i$$

This equation shows that the components in the new basis are a linear combination of the components in the old basis. The coefficients of this transformation are the inner products $\langle v_j | u_i \rangle$, which represent the projection of the old basis vector $|u_i\rangle$ onto the new basis vector $|v_j\rangle$.

This relationship is most elegantly expressed in matrix form. Let $\vec{c}$ be the column vector of components in Basis $U$ and $\vec{d}$ be the column vector of components in Basis $V$. Let $S$ be the **[transformation matrix](@entry_id:151616)** (or [change-of-basis matrix](@entry_id:184480)) whose elements are defined as $S_{ji} = \langle v_j | u_i \rangle$. The transformation rule then becomes:

$$\vec{d} = S \vec{c}$$

Note the convention for the indices of $S_{ji}$: the first index $j$ corresponds to the row and the new [basis vector](@entry_id:199546), while the second index $i$ corresponds to the column and the old [basis vector](@entry_id:199546). This convention arises naturally from the derivation [@problem_id:2084035].

For example, consider a [three-level system](@entry_id:147049) (a [qutrit](@entry_id:146257)) where a state $|\psi\rangle$ is known in Basis $U$. To find its components in a new Basis $V$, one simply needs to pre-multiply the column vector of its components in $U$ by the transformation matrix $S$ whose elements are the overlaps $S_{ji} = \langle v_j | u_i \rangle$ between the two bases [@problem_id:2084056].

### The Unitarity of Basis Transformations

The [change-of-basis matrix](@entry_id:184480) $S$ is not just any matrix; it has a crucial property that stems from the requirement that both bases are orthonormal. This property is **unitarity**. A matrix $S$ is unitary if its Hermitian conjugate (conjugate transpose) is also its inverse, i.e., $S^\dagger S = S S^\dagger = I$.

The physical necessity for this property lies in the basis-independence of physical reality. The inner product $\langle\Phi|\Psi\rangle$ between two states $|\Phi\rangle$ and $|\Psi\rangle$ has profound physical meaning; its squared modulus, $|\langle\Phi|\Psi\rangle|^2$, gives the probability of measuring the system to be in state $|\Phi\rangle$ if it was prepared in state $|\Psi\rangle$. Such a physical probability cannot depend on our arbitrary choice of descriptive basis. Therefore, the inner product must be an invariant under a change of basis.

Let's verify this. Let $\vec{c}_\Psi$ and $\vec{c}_\Phi$ be the component vectors of $|\Psi\rangle$ and $|\Phi\rangle$ in Basis $U$, and let $\vec{d}_\Psi$ and $\vec{d}_\Phi$ be their components in Basis $V$. The inner product in Basis $U$ is given by the matrix product $\vec{c}_\Phi^\dagger \vec{c}_\Psi$. In Basis $V$, it is $\vec{d}_\Phi^\dagger \vec{d}_\Psi$. For these to be equal for any pair of states, we must have:

$$\vec{c}_\Phi^\dagger \vec{c}_\Psi = \vec{d}_\Phi^\dagger \vec{d}_\Psi = (S \vec{c}_\Phi)^\dagger (S \vec{c}_\Psi) = (\vec{c}_\Phi^\dagger S^\dagger) (S \vec{c}_\Psi) = \vec{c}_\Phi^\dagger (S^\dagger S) \vec{c}_\Psi$$

For this equality to hold for all possible vectors, the matrix product in the middle must be the identity matrix: $S^\dagger S = I$. This proves that any transformation between two [orthonormal bases](@entry_id:753010) must be unitary.

A direct consequence is the preservation of the [norm of a vector](@entry_id:154882), which is just the inner product of the vector with itself. The total probability of finding the particle anywhere must be 1, which means the state vector must be normalized to unity ($\langle\psi|\psi\rangle=1$) in any basis. The unitarity of the transformation ensures this fundamental consistency [@problem_id:2084058].

### Transformation of Operators

Just as state vectors have different component representations in different bases, so do operators. An operator $\hat{A}$ is represented by a matrix in a given basis. The elements of this matrix in Basis $U = \{|u_i\rangle\}$ are given by $A_{ij} = \langle u_i | \hat{A} | u_j \rangle$. If we change to a new basis $V = \{|v_k\rangle\}$, the new matrix representation $A'$ will have elements $A'_{kl} = \langle v_k | \hat{A} | v_l \rangle$.

To find the relationship between the matrices $A$ and $A'$, we can strategically insert identity operators expressed via the completeness of Basis $U$:

$$A'_{kl} = \langle v_k | \hat{I} \hat{A} \hat{I} | v_l \rangle = \left\langle v_k \left| \left(\sum_i |u_i\rangle\langle u_i|\right) \hat{A} \left(\sum_j |u_j\rangle\langle u_j|\right) \right| v_l \right\rangle$$

Rearranging the sums and constants gives:

$$A'_{kl} = \sum_{i,j} \langle v_k | u_i \rangle \langle u_i | \hat{A} | u_j \rangle \langle u_j | v_l \rangle$$

We recognize the terms in this expression. The first term is the element $S_{ki}$ of the [change-of-basis matrix](@entry_id:184480) $S$. The middle term is the [matrix element](@entry_id:136260) $A_{ij}$ of the operator in the old basis. The last term, $\langle u_j | v_l \rangle$, can be related to $S$ as well: $\langle u_j | v_l \rangle = \langle v_l | u_j \rangle^* = (S_{lj})^*$. This is precisely the element $(j, l)$ of the matrix $S^\dagger$. Thus, we have:

$$A'_{kl} = \sum_{i,j} S_{ki} A_{ij} (S^\dagger)_{jl}$$

This is the definition of matrix multiplication. The relationship between the operator's [matrix representation](@entry_id:143451) in the new basis ($A'$) and the old basis ($A$) is a **[similarity transformation](@entry_id:152935)** mediated by the [unitary matrix](@entry_id:138978) $S$:

$$A' = S A S^\dagger$$

A striking consequence of this is that the properties of an operator's [matrix representation](@entry_id:143451) can change dramatically with the basis. For example, an operator that is diagonal in one basis (its [eigenbasis](@entry_id:151409)) will generally be non-diagonal in another. A common problem involves a Hamiltonian that is diagonal in its energy [eigenbasis](@entry_id:151409) $\{|u_1\rangle, |u_2\rangle\}$, but whose [matrix representation](@entry_id:143451) becomes off-diagonal when transformed to a new basis, such as one formed by superpositions of the energy eigenstates [@problem_id:2084039]. This same transformation rule applies to all [linear operators](@entry_id:149003), including the **[density operator](@entry_id:138151)** $\hat{\rho}$, which describes statistical mixtures of quantum states [@problem_id:2084049].

### Invariants Under Basis Change

While the matrix components of states and operators are basis-dependent, fundamental physical quantities must be invariant. We have already established that the inner product is one such invariant. For operators, the most important invariants are their **eigenvalues**.

The eigenvalues of an operator represent the possible outcomes of a measurement of the corresponding physical observable. These physical outcomes cannot depend on the mathematical framework we choose for our calculations. We can prove this formally by examining the [characteristic equation](@entry_id:149057) used to find the eigenvalues. In the old basis, the eigenvalues $\lambda$ are the roots of $\det(A - \lambda I) = 0$. In the new basis, they are the roots of $\det(A' - \lambda I) = 0$. Using the transformation rule $A' = S A S^\dagger$ and the fact that $S$ is unitary ($I = S S^\dagger$), we find:

$$\det(A' - \lambda I) = \det(S A S^\dagger - \lambda S S^\dagger) = \det(S(A - \lambda I)S^\dagger)$$

Using the property $\det(XYZ) = \det(X)\det(Y)\det(Z)$, this becomes:

$$\det(A' - \lambda I) = \det(S) \det(A - \lambda I) \det(S^\dagger) = \det(A - \lambda I) \det(S S^\dagger) = \det(A - \lambda I)$$

Since the [characteristic equation](@entry_id:149057) is identical in both bases, the eigenvalues $\lambda$ must be the same. This confirms that the set of possible measurement outcomes for an observable is a basis-independent property of the operator [@problem_id:2084052]. Other important operator invariants that follow from the properties of the similarity transformation include the **trace** ($\text{Tr}(A') = \text{Tr}(A)$) and the **determinant** ($\det(A') = \det(A)$).

### Applications and Advanced Topics

#### Changing to an Eigenbasis

One of the most powerful applications of a basis change is transforming from an arbitrary basis to the specific basis formed by the eigenvectors of an operator of interest. In its own [eigenbasis](@entry_id:151409), a Hermitian operator is represented by a [diagonal matrix](@entry_id:637782), where the diagonal entries are its real eigenvalues. This simplifies many calculations, particularly in quantum dynamics.

A canonical example is the spin-1/2 system. The state "spin-up along the z-axis," $|+\rangle_z$, is a basis vector in the [eigenbasis](@entry_id:151409) of the operator $S_z$. However, if we wish to understand the probabilities of measuring the spin along the x-axis, we must express this state in the [eigenbasis](@entry_id:151409) of the $S_x$ operator. This requires first finding the eigenvectors of $S_x$ and then performing a basis change on the state $|+\rangle_z$. This transformation reveals that $|+\rangle_z$ is an equal superposition of "spin-up along x" and "spin-down along x" states: $|+\rangle_z = \frac{1}{\sqrt{2}}|+\rangle_x + \frac{1}{\sqrt{2}}|-\rangle_x$. This means a measurement of $S_x$ on the state $|+\rangle_z$ will yield the eigenvalues $+\hbar/2$ and $-\hbar/2$ with equal probability of 0.5 each [@problem_id:2084038].

#### Commuting Observables and Simultaneous Diagonalization

A profound result in quantum mechanics states that two observables can be specified and measured simultaneously with arbitrary precision if and only if their corresponding operators commute. That is, $[\hat{A}, \hat{B}] = \hat{A}\hat{B} - \hat{B}\hat{A} = 0$. In the language of basis change, this theorem is equivalent to the statement that there exists a common basis of eigenvectors that simultaneously diagonalizes both operators.

The procedure for finding this common basis is straightforward if the eigenvalues of one operator, say $\hat{H}$, are all non-degenerate. In this case, each eigenvector of $\hat{H}$ is unique (up to a phase) and must also be an eigenvector of any operator that commutes with $\hat{H}$.

The situation is more subtle when $\hat{H}$ has [degenerate eigenvalues](@entry_id:187316). If an eigenvalue $E$ has a degeneracy of $N$, it corresponds to an $N$-dimensional eigenspace. Any vector in this eigenspace is an eigenvector of $\hat{H}$ with eigenvalue $E$. Because $\hat{L}$ commutes with $\hat{H}$, it maps this [eigenspace](@entry_id:150590) to itself. Within this degenerate subspace, we can treat $\hat{L}$ as an operator in its own right and find its eigenvectors. These vectors will be the basis vectors that simultaneously diagonalize both $\hat{H}$ and $\hat{L}$ within that subspace. This amounts to performing a change of basis *within* the degenerate eigenspace to resolve the degeneracy with respect to the second operator [@problem_id:2084060].

#### Operator Bases and the Bloch Vector

The concept of a basis can be extended from state vectors to the space of operators itself. For a [two-level system](@entry_id:138452) (a qubit), any $2 \times 2$ matrix can be expressed as a linear combination of a basis of four specific operators: the identity matrix $I$ and the three Pauli matrices $\{\sigma_x, \sigma_y, \sigma_z\}$. These four matrices are orthogonal with respect to the Hilbert-Schmidt inner product, $\text{Tr}(A^\dagger B)$.

This allows for an alternative representation of a qubit's state. The density operator $\hat{\rho}$ of any qubit can be written as:

$$\hat{\rho} = \frac{1}{2}(I + \vec{r} \cdot \vec{\sigma}) = \frac{1}{2}(I + r_x\sigma_x + r_y\sigma_y + r_z\sigma_z)$$

The vector of real coefficients $\vec{r} = (r_x, r_y, r_z)$ is known as the **Bloch vector**, and it provides a complete description of the qubit's state. Finding the Bloch vector components from a given [density matrix](@entry_id:139892) $\hat{\rho}$ is itself a form of basis change—from the [standard matrix](@entry_id:151240) element representation to the Pauli operator basis. The components are found using the orthogonality of the Pauli matrices:

$$r_k = \text{Tr}(\hat{\rho} \sigma_k) \quad \text{for } k \in \{x, y, z\}$$

This representation is invaluable in quantum information theory for visualizing qubit states and analyzing their dynamics under the influence of environmental noise [@problem_id:2084054].

In summary, the change of basis is a mathematical tool that embodies a deep physical principle: the description of a quantum system may change, but the physics remains invariant. Mastering the transformations of state vectors and operators is essential for navigating the rich structure of quantum theory and applying it to physical problems.