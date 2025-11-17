## Introduction
The representation theory of Lie algebras is a cornerstone of modern mathematics and theoretical physics, providing the language to describe symmetries in settings from quantum mechanics to string theory. At the heart of this theory lies a powerful geometric framework: the [weight space](@entry_id:195741) and its associated [lattices](@entry_id:265277). These structures transform the abstract algebraic properties of representations into a concrete geometric arena where states can be visualized as points, and [symmetry operations](@entry_id:143398) as reflections and rotations. This article addresses the fundamental challenge of how to navigate this space, offering a comprehensive guide to its key features and computational tools. You will begin by exploring the core principles and mechanisms, learning how to define the geometry of the [weight space](@entry_id:195741), switch between the crucial bases of [simple roots](@entry_id:197415) and [fundamental weights](@entry_id:200855), and understand the symmetries imposed by the Weyl group. Next, the article illuminates the profound utility of this framework through a tour of its applications and interdisciplinary connections, revealing how [weight diagrams](@entry_id:204634) organize the particle zoo, describe the electronic structure of solids, and even model random processes. Finally, a series of hands-on practices will allow you to solidify your understanding by performing concrete calculations within this elegant mathematical landscape.

## Principles and Mechanisms

Having introduced the foundational concepts of simple Lie algebras, we now delve into the geometric and algebraic structures that govern their [representation theory](@entry_id:137998). The central stage for this exploration is the **[weight space](@entry_id:195741)**, a Euclidean space whose intricate features are defined by roots, weights, and the symmetries of the Weyl group. This chapter will dissect the principles that define this space and the mechanisms that operate within it.

### The Weight Space as a Geometric Arena

For a semi-simple Lie algebra $\mathfrak{g}$ of rank $r$, with a chosen Cartan subalgebra $\mathfrak{h}$, the **[weight space](@entry_id:195741)** is the real vector space $\mathfrak{h}^*$, the dual of $\mathfrak{h}$. Crucially, $\mathfrak{h}^*$ is endowed with a positive-definite [symmetric bilinear form](@entry_id:148281), or inner product, denoted $(\cdot, \cdot)$. This inner product is induced by the Killing form on $\mathfrak{g}$ and provides $\mathfrak{h}^*$ with the structure of a Euclidean space. It allows us to define geometric notions such as lengths (norms) of vectors, angles between them, and reflections across hyperplanes.

In practical calculations, it is often convenient to realize $\mathfrak{h}^*$ as a specific subspace of $\mathbb{R}^n$ with the standard dot product. For instance, for the Lie algebra $\mathfrak{g} = \mathfrak{sl}_n(\mathbb{C})$ (type $A_{n-1}$), the [weight space](@entry_id:195741) can be identified with the subspace of $\mathbb{R}^n$ consisting of vectors whose components sum to zero. For $\mathfrak{sl}_4$ (type $A_3$), any vector $x = \sum_{i=1}^4 x_i \epsilon_i$ in its [weight space](@entry_id:195741) satisfies $\sum x_i = 0$, where $\{\epsilon_i\}$ is an orthonormal basis. This geometric setting is fundamental for calculating properties such as the angle between two weight vectors [@problem_id:842236]. For other algebras, such as the symplectic algebra $\mathfrak{sp}_{2n}$ or the orthogonal algebra $\mathfrak{so}_m$, the [weight space](@entry_id:195741) can often be identified directly with $\mathbb{R}^n$ equipped with the standard dot product [@problem_id:842132] [@problem_id:842127].

### The Dual Bases of Roots and Weights

The structure of the [weight space](@entry_id:195741) is organized by two distinguished sets of vectors that form bases for $\mathfrak{h}^*$: the [simple roots](@entry_id:197415) and the [fundamental weights](@entry_id:200855).

The **[simple roots](@entry_id:197415)**, denoted $\Pi = \{\alpha_1, \dots, \alpha_r\}$, form a basis for the [root system](@entry_id:202162) $\Phi$. They are the elementary building blocks of all roots. The geometric relationship between the [simple roots](@entry_id:197415)—their relative lengths and angles—is completely encoded in the **Cartan matrix** $A$, a non-degenerate $r \times r$ matrix with integer entries defined as:
$$
A_{ij} = \langle \alpha_j, \alpha_i^\vee \rangle = \frac{2(\alpha_i, \alpha_j)}{(\alpha_i, \alpha_i)}
$$
Here, $\alpha_i^\vee = \frac{2\alpha_i}{(\alpha_i, \alpha_i)}$ is the **simple coroot** associated with $\alpha_i$.

Complementary to the [simple roots](@entry_id:197415) are the **[fundamental weights](@entry_id:200855)**, denoted $\{\omega_1, \dots, \omega_r\}$. These vectors are defined by their duality relationship with the simple [coroots](@entry_id:193338):
$$
\langle \omega_i, \alpha_j^\vee \rangle = \frac{2(\omega_i, \alpha_j)}{(\alpha_j, \alpha_j)} = \delta_{ij}
$$
where $\delta_{ij}$ is the Kronecker delta. This definition establishes the [fundamental weights](@entry_id:200855) as a basis for $\mathfrak{h}^*$ that is dual to the basis of simple [coroots](@entry_id:193338). While roots describe the structure of the algebra itself (the [adjoint representation](@entry_id:146773)), [fundamental weights](@entry_id:200855) are the natural building blocks for all other finite-dimensional irreducible representations. The highest weight of any such representation is a non-negative integer [linear combination](@entry_id:155091) of the [fundamental weights](@entry_id:200855).

A crucial aspect of the theory is the ability to translate between these two fundamental bases. A [simple root](@entry_id:635422) $\alpha_k$ can be expressed as a linear combination of the [fundamental weights](@entry_id:200855). By taking the inner product of $\alpha_k$ with a simple coroot $\alpha_j^\vee$ and applying the definition of the Cartan matrix and the duality of the [fundamental weights](@entry_id:200855), we find:
$$
\langle \alpha_k, \alpha_j^\vee \rangle = A_{jk} = \left\langle \sum_{i=1}^r c_i \omega_i, \alpha_j^\vee \right\rangle = \sum_{i=1}^r c_i \langle \omega_i, \alpha_j^\vee \rangle = \sum_{i=1}^r c_i \delta_{ij} = c_j
$$
This reveals that the coefficients for expressing a [simple root](@entry_id:635422) in the fundamental weight basis are given by the entries of the transposed Cartan matrix:
$$
\alpha_k = \sum_{j=1}^r A_{jk} \omega_j
$$
For example, for the Lie algebra $\mathfrak{sl}_4$ (type $A_3$), the Cartan matrix is symmetric. The expression for the [simple root](@entry_id:635422) $\alpha_2$ is obtained by reading the second row (or column) of the Cartan matrix, yielding $\alpha_2 = -\omega_1 + 2\omega_2 - \omega_3$ [@problem_id:842108].

Conversely, expressing [fundamental weights](@entry_id:200855) in terms of [simple roots](@entry_id:197415) requires inverting this relationship. This leads to the equation:
$$
\omega_i = \sum_{j=1}^r (A^{-1})_{ji} \alpha_j
$$
This relationship is pivotal for determining when a given weight belongs to the lattice spanned by the roots, as we will see next.

### The Root and Weight Lattices

Within the continuous vector space $\mathfrak{h}^*$, two discrete [lattices](@entry_id:265277) play a central role.

The **root lattice**, denoted $Q$, is the set of all integer linear combinations of the [simple roots](@entry_id:197415):
$$
Q = \mathbb{Z}\{\alpha_1, \dots, \alpha_r\} = \left\{ \sum_{i=1}^r k_i \alpha_i \mid k_i \in \mathbb{Z} \right\}
$$
All roots of the algebra, by definition, belong to this lattice.

The **[weight lattice](@entry_id:195778)**, denoted $P$, is the set of all vectors $\lambda \in \mathfrak{h}^*$ whose pairing with every simple coroot is an integer:
$$
P = \left\{ \lambda \in \mathfrak{h}^* \mid \langle \lambda, \alpha_i^\vee \rangle \in \mathbb{Z} \text{ for all } i=1, \ldots, r \right\}
$$
From the duality condition $\langle \omega_i, \alpha_j^\vee \rangle = \delta_{ij}$, it is clear that each fundamental weight $\omega_i$ satisfies this integrality condition. Therefore, the [weight lattice](@entry_id:195778) can be equivalently defined as the integer span of the [fundamental weights](@entry_id:200855):
$$
P = \mathbb{Z}\{\omega_1, \dots, \omega_r\}
$$
The [weight lattice](@entry_id:195778) contains all possible weights of all finite-dimensional representations of $\mathfrak{g}$.

Since each [simple root](@entry_id:635422) $\alpha_i$ has integer pairings with all simple [coroots](@entry_id:193338) (the integers being the Cartan matrix entries $A_{ji}$), every [simple root](@entry_id:635422) is an element of the [weight lattice](@entry_id:195778) $P$. Because $P$ is closed under integer linear combinations, it follows that the entire root lattice is a sublattice of the [weight lattice](@entry_id:195778), i.e., $Q \subseteq P$.

A practical question is to determine when a weight $\lambda$, given in the fundamental weight basis as $\lambda = \sum_i m_i \omega_i$, belongs to the root lattice $Q$. This is equivalent to asking whether the coefficients in its [simple root](@entry_id:635422) expansion are all integers. Using the change-of-basis formula, we have:
$$
\lambda = \sum_{i=1}^r m_i \omega_i = \sum_{i=1}^r m_i \left( \sum_{j=1}^r (A^{-1})_{ji} \alpha_j \right) = \sum_{j=1}^r \left( \sum_{i=1}^r m_i (A^{-1})_{ji} \right) \alpha_j
$$
Thus, $\lambda \in Q$ if and only if the coefficients $c_j = \sum_{i=1}^r m_i (A^{-1})_{ji}$ are integers for all $j=1, \dots, r$. This provides a clear algorithm for checking membership in the root lattice. For instance, in a problem involving the Lie algebra $\mathfrak{so}_8$ (type $D_4$), this condition can be used to find parameters for which a highest weight of an irreducible representation lies in the root lattice, which in turn implies that all weights of that representation belong to the root lattice [@problem_id:842234].

### Geometric Calculations in the Weight Space

The inner product on $\mathfrak{h}^*$ allows for the computation of lengths and angles, revealing the rich geometry of the weight and [root systems](@entry_id:198970). The inner products of the [fundamental weights](@entry_id:200855) themselves hold important information. These can be related to the Cartan matrix. Starting from the relation $\alpha_i = \sum_j A_{ji} \omega_j$, one can derive the matrix of inner products of the [fundamental weights](@entry_id:200855). Let $M$ be the matrix with entries $M_{ij} = (\omega_i, \omega_j)$ and $D'$ be the [diagonal matrix](@entry_id:637782) with entries $D'_{ii} = (\alpha_i, \alpha_i)/2$. The relationship is given by $M = (A^T)^{-1} D'$.

In the important special case of a **simply-laced** algebra (types A, D, E), all roots have the same length. By convention, we can normalize the inner product such that $(\alpha_i, \alpha_i) = 2$ for all $i$. In this case, $D'$ becomes the identity matrix, and the Cartan matrix $A$ is symmetric. The formula simplifies dramatically to $M = A^{-1}$. Thus, for simply-laced algebras:
$$
(\omega_i, \omega_j) = (A^{-1})_{ij}
$$
This powerful result reduces the geometric problem of finding inner products of [fundamental weights](@entry_id:200855) to the algebraic problem of inverting the Cartan matrix. For example, to compute the squared norm of the vector $\lambda = \omega_2 - \omega_4$ for $\mathfrak{so}_{10}$ (type $D_5$, a simply-laced algebra), one can calculate $||\lambda||^2 = (\omega_2, \omega_2) - 2(\omega_2, \omega_4) + (\omega_4, \omega_4)$ by finding the corresponding entries of the inverse Cartan matrix [@problem_id:842127].

With these inner products, we can compute any geometric quantity. For example, the cosine of the angle $\theta$ between two weight vectors $\lambda_1$ and $\lambda_2$ is given by the standard formula:
$$
\cos \theta = \frac{(\lambda_1, \lambda_2)}{\sqrt{(\lambda_1, \lambda_1)(\lambda_2, \lambda_2)}}
$$
To apply this, one typically expresses the weights in a convenient [orthonormal basis](@entry_id:147779) (like the $\{\epsilon_i\}$ basis) or uses the inner product matrix $M=A^{-1}$ as described above [@problem_id:842236].

### The Weyl Group: Symmetries of the Lattice

The [weight space](@entry_id:195741) is endowed with a fundamental set of symmetries, embodied by the **Weyl group** $W$. The Weyl group is a finite [reflection group](@entry_id:203838) generated by the simple reflections $\{s_1, \dots, s_r\}$, where $s_i$ is the reflection across the hyperplane orthogonal to the [simple root](@entry_id:635422) $\alpha_i$. The action of a simple reflection $s_i$ on a weight $\lambda \in \mathfrak{h}^*$ is given by the formula:
$$
s_i(\lambda) = \lambda - \langle \lambda, \alpha_i^\vee \rangle \alpha_i
$$
Since $\lambda \in P$, the coefficient $\langle \lambda, \alpha_i^\vee \rangle$ is an integer. This action preserves the [weight lattice](@entry_id:195778) $P$ (and also the root lattice $Q$).

To calculate the result of such a reflection, one must evaluate the integer pairing $\langle \lambda, \alpha_i^\vee \rangle$ and express the [simple root](@entry_id:635422) $\alpha_i$ in the desired basis. For instance, to calculate $s_{\alpha_2}(\omega_2)$ for $\mathfrak{sp}_6$ (type $C_3$), we use the facts that $\langle \omega_2, \alpha_2^\vee \rangle = \delta_{22} = 1$ and $\alpha_2 = -\omega_1 + 2\omega_2 - \omega_3$ (reading from the $C_3$ Cartan matrix) to find $s_{\alpha_2}(\omega_2) = \omega_2 - \alpha_2 = \omega_1 - \omega_2 + \omega_3$ [@problem_id:842238]. General elements of the Weyl group are products of these simple reflections, and their action can be computed by applying the reflections sequentially [@problem_id:842268].

A central concept in representation theory is the **Weyl group orbit** of a weight $\lambda$, defined as the set of all distinct weights obtained by acting on $\lambda$ with elements of the Weyl group: $W(\lambda) = \{w(\lambda) \mid w \in W\}$. For an irreducible representation with highest weight $\Lambda$, the set of all its weights is invariant under the action of $W$, and the orbit of the highest weight, $W(\Lambda)$, consists of all the "extreme" weights of the representation.

The size of an orbit can be computed efficiently using the **[orbit-stabilizer theorem](@entry_id:145230)**:
$$
|W(\lambda)| = \frac{|W|}{|W_\lambda|}
$$
Here, $|W|$ is the order of the full Weyl group, and $W_\lambda = \{w \in W \mid w(\lambda) = \lambda\}$ is the [stabilizer subgroup](@entry_id:137216) of $\lambda$. The stabilizer $W_\lambda$ is itself a Weyl group. It is generated by those simple reflections $s_j$ that fix $\lambda$. A reflection $s_j$ fixes $\lambda$ if and only if $\lambda$ lies on the reflection [hyperplane](@entry_id:636937), which means $\langle \lambda, \alpha_j^\vee \rangle = 0$.

This provides a beautiful connection to the Dynkin diagram. The Dynkin diagram of the stabilizer $W_\lambda$ is obtained by removing the nodes corresponding to [simple roots](@entry_id:197415) $\alpha_j$ for which $\langle \lambda, \alpha_j^\vee \rangle \neq 0$. For a fundamental weight $\omega_i$, the condition simplifies: we remove node $j$ if $\langle \omega_i, \alpha_j^\vee \rangle = \delta_{ij} \neq 0$. This means we only remove node $i$. For example, to find the orbit size of $\omega_2$ for $\mathfrak{sl}_4$ (type $A_3$), we note that $\langle \omega_2, \alpha_1^\vee \rangle=0$ and $\langle \omega_2, \alpha_3^\vee \rangle=0$, but $\langle \omega_2, \alpha_2^\vee \rangle \neq 0$. The stabilizer $W_{\omega_2}$ is generated by $s_1$ and $s_3$. The $A_3$ diagram is $\circ_1 - \circ_2 - \circ_3$. Removing node 2 leaves two disconnected nodes, corresponding to the algebra $A_1 \times A_1$. Thus, $|W_{\omega_2}| = |W(A_1 \times A_1)| = |S_2 \times S_2| = 2 \times 2 = 4$. Since $|W(A_3)| = |S_4| = 24$, the orbit size is $|W(\omega_2)| = 24/4 = 6$ [@problem_id:842159].

### The Fundamental Group and the Quotient Lattice

The inclusion of the root lattice $Q$ into the [weight lattice](@entry_id:195778) $P$ is of fundamental importance. The quotient group $P/Q$ is a finite abelian group, sometimes called the **fundamental group** of the Lie algebra. This group carries deep information, being isomorphic to the center of the simply connected Lie group $G_{sc}$ corresponding to $\mathfrak{g}$, and also to the topological fundamental group of the corresponding adjoint group, $\pi_1(G_{ad})$.

The order of this group, which is the index of the sublattice $Q$ in $P$, is given by a remarkably simple formula:
$$
|P/Q| = [P:Q] = |\det(A)|
$$
where $A$ is the Cartan matrix. This connects the algebraic structure of the [lattices](@entry_id:265277) directly to the determinant of the matrix encoding the geometry of the [simple roots](@entry_id:197415). For example, for $\mathfrak{so}_7$ (type $B_3$), one can compute the Cartan matrix from the definition of its [simple roots](@entry_id:197415) and find its determinant to be 2, meaning there are two cosets of the root lattice in the [weight lattice](@entry_id:195778) [@problem_id:842121].

The determinant gives the order of $P/Q$, but not necessarily its full structure as an [abelian group](@entry_id:139381). To determine the structure (i.e., its decomposition into cyclic groups), one must find the Smith Normal Form of the Cartan matrix. For example, for Lie algebras of type $D_n$ with $n \ge 4$, the determinant of the Cartan matrix is always 4. However, the structure of the group $P/Q$ depends on the parity of $n$:
- If $n$ is odd, $P/Q \cong \mathbb{Z}_4$.
- If $n$ is even, $P/Q \cong \mathbb{Z}_2 \times \mathbb{Z}_2$.

Therefore, for $\mathfrak{so}_{12}$ (type $D_6$), the quotient group is $P/Q \cong \mathbb{Z}_2 \times \mathbb{Z}_2$. This group has 4 elements, one of which is the identity (corresponding to the root lattice $Q$ itself), leaving 3 non-trivial elements [@problem_id:842262]. Each of these non-trivial elements corresponds to a family of representations whose weights do not belong to the root lattice.

In this chapter, we have journeyed through the [weight space](@entry_id:195741), mapping its essential features from the ground up. We defined its geometry via the inner product, established the dual roles of roots and weights, charted the discrete lattices they form, and analyzed the symmetries imposed by the Weyl group. This intricate yet elegant framework is not merely an abstract construction; it is the essential machinery for classifying and understanding the representations of Lie algebras, a cornerstone of modern mathematics and physics.