## Introduction
Lie superalgebras represent a powerful and elegant extension of Lie algebras, incorporating a graded structure that unifies the concepts of commutation and [anticommutation](@entry_id:182725). This mathematical framework is not merely an abstract curiosity; it is the essential language for describing [supersymmetry](@entry_id:155777) (SUSY), a proposed fundamental symmetry of nature linking [bosons and fermions](@entry_id:145190). The study of their representations reveals a world far richer and more complex than that of ordinary Lie algebras, addressing a crucial knowledge gap in our understanding of symmetries that mix spacetime and internal properties.

This article provides a comprehensive exploration of the [representation theory](@entry_id:137998) of Lie superalgebras, guiding the reader from foundational concepts to advanced applications. In the first chapter, **Principles and Mechanisms**, we will dissect the fundamental algebraic structure, defining the supercommutator, exploring key examples like $\mathfrak{gl}(1|1)$, and introducing the pivotal distinction between [typical and atypical representations](@entry_id:192811). Following this, the chapter on **Applications and Interdisciplinary Connections** will demonstrate the profound impact of this theory, showing how superalgebra representations are realized as supermultiplets in quantum field theory, drive integrable structures in string theory, and forge unexpected connections to fields like knot theory and number theory. Finally, the **Hands-On Practices** section will solidify these theoretical ideas through guided computational exercises, allowing you to engage directly with the mechanics of the theory.

## Principles and Mechanisms

### The Fundamental Structure of Lie Superalgebras

A Lie superalgebra is a natural generalization of a Lie algebra, incorporating a structure known as a $\mathbb{Z}_2$-grading. This grading is the cornerstone of its definition and is responsible for the unique physical and mathematical properties associated with [supersymmetry](@entry_id:155777).

#### The Graded Vector Space and the Supercommutator

A Lie superalgebra $\mathfrak{g}$ is, first and foremost, a vector space that decomposes into a [direct sum](@entry_id:156782) of two subspaces: an **even subspace** $\mathfrak{g}_0$ and an **odd subspace** $\mathfrak{g}_1$. We write this as $\mathfrak{g} = \mathfrak{g}_0 \oplus \mathfrak{g}_1$. Elements of $\mathfrak{g}_0$ are often called **bosonic**, while elements of $\mathfrak{g}_1$ are called **fermionic**, borrowing terminology from physics.

Any element $X \in \mathfrak{g}$ that belongs entirely to either $\mathfrak{g}_0$ or $\mathfrak{g}_1$ is called **homogeneous**. We associate a **degree** or **parity** $|X|$ to such elements: $|X|=0$ if $X \in \mathfrak{g}_0$ and $|X|=1$ if $X \in \mathfrak{g}_1$.

The structure of a Lie superalgebra is completed by a bilinear operation, called the **graded Lie bracket** or **supercommutator**, denoted $[\cdot, \cdot]$. This bracket maps two elements of $\mathfrak{g}$ to another element in $\mathfrak{g}$ and must respect the grading in a specific way: $[\mathfrak{g}_i, \mathfrak{g}_j] \subseteq \mathfrak{g}_{i+j \pmod 2}$. For two homogeneous elements $X$ and $Y$, the supercommutator is defined as:
$$
[X, Y] = XY - (-1)^{|X||Y|} YX
$$
This single definition elegantly unifies the familiar commutator and anticommutator:
- If at least one of the elements, say $X$, is even ($|X|=0$), the sign factor $(-1)^{|X||Y|}$ is simply $1$. The bracket becomes the standard **commutator**: $[X, Y] = XY - YX$. This implies that $\mathfrak{g}_0$ is itself an ordinary Lie algebra, and that the elements of $\mathfrak{g}_0$ act on the odd space $\mathfrak{g}_1$ via commutation.
- If both elements are odd ($|X|=|Y|=1$), the sign factor is $-1$. The bracket becomes the **anticommutator**: $[X, Y] = \{X, Y\} = XY + YX$. This is the most distinctive feature of a superalgebra: the "product" of two odd elements is an even element.

Like an ordinary Lie bracket, the supercommutator must satisfy two axioms: graded skew-symmetry, $[X, Y] = -(-1)^{|X||Y|}[Y, X]$, and the graded Jacobi identity.

#### An Introductory Example: The Lie Superalgebra $\mathfrak{gl}(1|1)$

The simplest non-trivial Lie superalgebras provide the clearest illustration of these rules. Consider the general linear Lie superalgebra $\mathfrak{gl}(1|1)$, which can be represented by $2 \times 2$ matrices. The grading is defined by a block structure:
$$
\text{Even elements } (\mathfrak{g}_0): \begin{pmatrix} a & 0 \\ 0 & d \end{pmatrix}, \quad \text{Odd elements } (\mathfrak{g}_1): \begin{pmatrix} 0 & b \\ c & 0 \end{pmatrix}
$$
A standard basis for $\mathfrak{gl}(1|1)$ consists of two even generators, $C$ (the identity) and $H$, and two odd generators, $\psi^+$ and $\psi^-$:
$$
H = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}, \quad C = \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}, \quad \psi^+ = \begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix}, \quad \psi^- = \begin{pmatrix} 0 & 0 \\ 1 & 0 \end{pmatrix}
$$
Let us compute the supercommutator $[H, \psi^+]$. Since $H$ is even ($|H|=0$) and $\psi^+$ is odd ($|\psi^+|=1$), this is an ordinary commutator:
$$
[H, \psi^+] = H\psi^+ - \psi^+H = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}\begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix} - \begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix}\begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix} = \begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix} - \begin{pmatrix} 0 & -1 \\ 0 & 0 \end{pmatrix} = \begin{pmatrix} 0 & 2 \\ 0 & 0 \end{pmatrix} = 2\psi^+
$$
Now consider the supercommutator of two odd elements, $[\psi^+, \psi^-]$. This is an anticommutator:
$$
[\psi^+, \psi^-] = \{\psi^+, \psi^-\} = \psi^+\psi^- + \psi^-\psi^+ = \begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix}\begin{pmatrix} 0 & 0 \\ 1 & 0 \end{pmatrix} + \begin{pmatrix} 0 & 0 \\ 1 & 0 \end{pmatrix}\begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix} = \begin{pmatrix} 1 & 0 \\ 0 & 0 \end{pmatrix} + \begin{pmatrix} 0 & 0 \\ 0 & 0 \end{pmatrix} = \begin{pmatrix} 1 & 0 \\ 0 & 0 \end{pmatrix}
$$
Notice that the result is an even matrix. In this basis, we find it is a linear combination of $H$ and $C$: $\frac{1}{2}(C+H)$. This confirms the grading rule: $[\mathfrak{g}_1, \mathfrak{g}_1] \subseteq \mathfrak{g}_0$.

The algebraic relations among basis generators, such as $[H, \psi^+] = 2\psi^+$, define the **structure constants** of the algebra. For a more complex algebra like $\mathfrak{sl}(1|2)$, whose even part is $\mathfrak{u}(1) \oplus \mathfrak{sl}(2, \mathbb{C})$, calculating the anticommutator of its odd generators $Q_1 = E_{01}$ and $S_1 = E_{10}$ (where $E_{ij}$ are matrix units) yields $\{Q_1, S_1\} = E_{00} + E_{11}$. Expressing this result in terms of the even basis generators reveals the specific [structure constants](@entry_id:157960) that couple the odd and even sectors of the algebra [@problem_id:757714].

#### The Supertrace and the Special Linear Superalgebras

For the family of matrix superalgebras $\mathfrak{gl}(m|n)$, a crucial invariant is the **[supertrace](@entry_id:183947)**. For a [block matrix](@entry_id:148435) $M = \begin{pmatrix} A & B \\ C & D \end{pmatrix}$ where $A$ is $m \times m$ and $D$ is $n \times n$, the [supertrace](@entry_id:183947) is defined as:
$$
\text{str}(M) = \text{tr}(A) - \text{tr}(D)
$$
This definition leads to the important property $\text{str}([X,Y]) = 0$ for any $X, Y \in \mathfrak{gl}(m|n)$, making it the appropriate generalization of the ordinary trace.

The [supertrace](@entry_id:183947) is used to define the **special linear Lie superalgebra**, $\mathfrak{sl}(m|n)$, as the subalgebra of $\mathfrak{gl}(m|n)$ consisting of matrices with zero [supertrace](@entry_id:183947).

As an example, let's return to $\mathfrak{gl}(1|1)$ and consider two operators $X = [H, \psi^+] = 2\psi^+$ and $Y = [H, \psi^-] = -2\psi^-$. Their product in the [universal enveloping algebra](@entry_id:188071) is $Z=XY = -4\psi^+\psi^-$. Using [matrix multiplication](@entry_id:156035), we find $Z = -4 \begin{pmatrix} 1 & 0 \\ 0 & 0 \end{pmatrix}$. Applying the [supertrace](@entry_id:183947) definition with $A = (-4)$ and $D = (0)$, we get $\text{str}(Z) = -4 - 0 = -4$ [@problem_id:757646].

### Invariants and Fundamental Structures

Lie superalgebras and their representations possess unique invariants and structures that generalize those of ordinary Lie algebras.

#### Super Vector Spaces and Superdimension

The concept of a graded vector space is formalized as a **super vector space** $V = V_0 \oplus V_1$. A key characteristic of such a space is its **superdimension**, defined as the difference between the dimensions of its even and odd subspaces:
$$
\text{sdim}(V) = \dim(V_0) - \dim(V_1)
$$
The superdimension is a fundamental invariant that often appears in supersymmetric theories, for instance, in [index theorems](@entry_id:637636) where it can be related to topological quantities.

A primary example of a super vector space is the Lie superalgebra itself, under the **[adjoint representation](@entry_id:146773)**, where $V_0 = \mathfrak{g}_0$ and $V_1 = \mathfrak{g}_1$. Let's calculate the superdimension of the adjoint representation of $\mathfrak{sl}(m|n)$.
- The even subspace $\mathfrak{g}_0$ consists of block-[diagonal matrices](@entry_id:149228) $\begin{pmatrix} A & 0 \\ 0 & D \end{pmatrix}$. The dimension of the space of all $m \times m$ matrices is $m^2$ and for $n \times n$ matrices is $n^2$. The condition $\text{str}(X) = \text{tr}(A) - \text{tr}(D) = 0$ imposes one linear constraint, so $\dim(\mathfrak{g}_0) = m^2 + n^2 - 1$.
- The odd subspace $\mathfrak{g}_1$ consists of off-[diagonal matrices](@entry_id:149228) $\begin{pmatrix} 0 & B \\ C & 0 \end{pmatrix}$. The dimension of the space of $m \times n$ matrices $B$ is $mn$, and for $n \times m$ matrices $C$ is $nm$. Thus, $\dim(\mathfrak{g}_1) = 2mn$.
- The superdimension of the [adjoint representation](@entry_id:146773) is therefore:
$$
\text{sdim}(\text{ad}(\mathfrak{sl}(m|n))) = (m^2 + n^2 - 1) - 2mn = (m-n)^2 - 1
$$
For the specific case of $\mathfrak{sl}(2|1)$, we have $m=2, n=1$, so the superdimension is $(2^2 + 1^2 - 1) - 2(2)(1) = 4 - 4 = 0$ [@problem_id:757697]. This vanishing superdimension is a special property of algebras of the type $\mathfrak{sl}(k+1|k)$.

#### Constructing Representations: Tensor Products and Exterior Powers

Just as with ordinary vector spaces, one can construct new super [vector spaces](@entry_id:136837) from existing ones. The tensor product $V \otimes W$ of two super [vector spaces](@entry_id:136837) is itself a super vector space. Its grading is defined by declaring a product of two homogeneous vectors $v \otimes w$ to be even if $|v|+|w|$ is even, and odd if $|v|+|w|$ is odd. This leads to:
$$
(V \otimes W)_0 = (V_0 \otimes W_0) \oplus (V_1 \otimes W_1)
$$
$$
(V \otimes W)_1 = (V_0 \otimes W_1) \oplus (V_1 \otimes W_0)
$$
From the [tensor product](@entry_id:140694) $V \otimes V$, one can define the **graded [symmetric square](@entry_id:137676)** $S^2(V)$ and the **graded [exterior square](@entry_id:141620)** $\Lambda^2(V)$. The graded [exterior square](@entry_id:141620) is spanned by elements of the form $v \otimes w - (-1)^{|v||w|} w \otimes v$. This definition implies that for two even vectors, we take the standard antisymmetric combination $v \otimes w - w \otimes v$, but for two odd vectors, we must take the symmetric combination $v \otimes w + w \otimes v$.

Let's compute the superdimension of $\Lambda^2(V)$ where $V$ is the natural representation of $\mathfrak{gl}(2|1)$. Here $V = \mathbb{C}^{2|1}$, so $\dim(V_0)=2$ and $\dim(V_1)=1$. The even part of $\Lambda^2(V)$ consists of $\Lambda^2(V_0)$ (antisymmetric products of even vectors) and $S^2(V_1)$ (symmetric products of odd vectors). The odd part consists of $V_0 \otimes V_1$.
- $\dim(\Lambda^2(V_0)) = \binom{2}{2} = 1$.
- $\dim(S^2(V_1)) = \binom{1+2-1}{2} = 1$. (Dimension of symmetric powers of a 1D space)
- $\dim(V_0 \otimes V_1) = \dim(V_0)\dim(V_1) = 2 \times 1 = 2$.
The superdimension is then $\text{sdim}(\Lambda^2(V)) = (\dim(\Lambda^2(V_0)) + \dim(S^2(V_1))) - \dim(V_0 \otimes V_1) = (1+1) - 2 = 0$ [@problem_id:757632].

#### Invariant Bilinear Forms

A key structure on a Lie superalgebra is a non-degenerate, symmetric, and [invariant bilinear form](@entry_id:137662) $\kappa(\cdot, \cdot)$. Invariance means $\kappa([X,Y], Z) = \kappa(X, [Y,Z])$ for all $X, Y, Z \in \mathfrak{g}$. For matrix superalgebras, this form is naturally provided by the [supertrace](@entry_id:183947):
$$
\kappa(X, Y) = \text{str}(XY)
$$
This form plays a role analogous to the Killing form for ordinary semisimple Lie algebras and is essential for constructing Casimir operators. Let's compute this form for two odd elements $F_1 = Q_1 + S_2$ and $F_2 = Q_2 - S_1$ in $\mathfrak{sl}(2|1)$, where the basis matrices are given as off-diagonal matrix units. By direct matrix multiplication, one can find the product matrix $P = F_1 F_2$. Then, by identifying the diagonal blocks of $P$ and applying the [supertrace](@entry_id:183947) definition, one can calculate the value of the form. For instance, in the case presented in [@problem_id:757749], the result is $\kappa(F_1, F_2) = -2$. This calculation demonstrates how the product of two odd matrices yields an even matrix, whose [supertrace](@entry_id:183947) provides a [scalar invariant](@entry_id:159606).

### The Theory of Representations

The [representation theory](@entry_id:137998) of Lie superalgebras is significantly richer than that of ordinary Lie algebras, largely due to the distinction between [typical and atypical representations](@entry_id:192811).

#### Highest-Weight Representations and Casimir Invariants

Similar to ordinary Lie algebras, many important representations are **highest-weight representations**. A representation is built from a **highest-weight state** $|\Lambda\rangle$, which is an eigenvector of the Cartan subalgebra generators and is annihilated by all **raising operators**. The full representation space, or module, is then generated by acting on $|\Lambda\rangle$ with the **lowering operators**.

A central concept in [representation theory](@entry_id:137998) is the **Casimir operator**, an operator built from the algebra's generators that commutes with every generator. By Schur's lemma, a Casimir operator must act as a multiple of the identity on an irreducible representation. Its eigenvalue is an invariant that helps classify the representation.

Let's examine the **orthosymplectic Lie superalgebra $\mathfrak{osp}(1|2)$**. Its even part is $\mathfrak{g}_0 \cong \mathfrak{sl}(2)$, and it has a two-dimensional odd part. For an irreducible highest-weight representation of $\mathfrak{osp}(1|2)$ with [highest weight](@entry_id:202808) $j$ (the eigenvalue of the Cartan generator $J_0$), the eigenvalue of the quadratic Casimir operator $C_2$ is given by a simple formula:
$$
\lambda_{C_2} = j(j + 1/2)
$$
Consider the defining 3-dimensional representation of $\mathfrak{osp}(1|2)$. By identifying the highest-weight state as the vector annihilated by the raising operators $J_+$ and $Q_+$, we can find its weight. For instance, if the state is $|e_1\rangle$, its eigenvalue under $J_0$ is found to be $j=1/2$. Plugging this into the formula gives the Casimir eigenvalue $\lambda_{C_2} = \frac{1}{2}(\frac{1}{2} + \frac{1}{2}) = \frac{1}{2}$ [@problem_id:757622].

#### Decomposing Representations under the Even Subalgebra

A powerful technique for analyzing a representation of a superalgebra $\mathfrak{g}$ is to see how it behaves as a representation of its even subalgebra $\mathfrak{g}_0$. Since the action of $\mathfrak{g}_0$ preserves the grading (i.e., $[\mathfrak{g}_0, \mathfrak{g}_i] \subseteq \mathfrak{g}_i$), any representation $V=V_0 \oplus V_1$ of $\mathfrak{g}$ immediately provides two representations of $\mathfrak{g}_0$: one on $V_0$ and one on $V_1$.

A canonical example is the adjoint representation of $\mathfrak{g}$ itself. The full space $\mathfrak{g} = \mathfrak{g}_0 \oplus \mathfrak{g}_1$ decomposes into two modules for the even subalgebra. For $\mathfrak{osp}(3|2)$, the even subalgebra is $\mathfrak{g}_0 = \mathfrak{so}(3) \oplus \mathfrak{sp}(2)$, which is isomorphic to $\mathfrak{su}(2) \oplus \mathfrak{su}(2)$. Its representations are labeled by pairs of spins $(\ell, s)$.
- The even part $\mathfrak{g}_0$ transforms under itself as the [direct sum](@entry_id:156782) of the adjoint representations of its components, which corresponds to the sum of irreps $(1,0) \oplus (0,1)$.
- The odd part $\mathfrak{g}_1$ transforms as the [tensor product](@entry_id:140694) of the fundamental (vector) representations of $\mathfrak{so}(3)$ and $\mathfrak{sp}(2)$, which corresponds to the irrep $(1, 1/2)$.

One can then analyze invariants, such as the trace of the $\mathfrak{g}_0$ Casimir operator over the entire space $\mathfrak{g}$, by summing its contributions from each of these [irreducible components](@entry_id:153033) [@problem_id:757601].

### Typical and Atypical Representations: A Key Distinction

The most profound departure from ordinary Lie algebra [representation theory](@entry_id:137998) is the classification of representations into **typical** and **atypical** types.

#### Verma Modules, Reducibility, and Null Vectors

A **Verma module** $V(\Lambda)$ is a "maximal" highest-weight module with highest weight $\Lambda$. For ordinary semisimple Lie algebras, Verma modules are almost always irreducible. For Lie superalgebras, the situation is different. A Verma module may be reducible, meaning it contains a proper, non-trivial submodule. Such a representation is called **atypical**. If the Verma module is irreducible, the representation is called **typical**.

Reducibility occurs if and only if the Verma module contains a **null vector** (or [singular vector](@entry_id:180970)). A null vector is a state $|v\rangle$, created by acting on the highest-weight state $|\Lambda\rangle$ with lowering operators, that is itself a highest-weight vector (i.e., it is annihilated by all raising operators). The submodule generated from this null vector can then be "factored out" to obtain an [irreducible representation](@entry_id:142733).

The existence of a null vector imposes a constraint on the highest-weight labels $(\lambda_1, \lambda_2, \dots)$. To find this condition, we can construct a potential null vector and enforce that it is annihilated by all raising operators. For example, in a simple superalgebra with one pair of odd generators $Q^\pm$, the simplest possible null vector would be at "level one," given by $|v\rangle = Q^-|\Lambda\rangle$. For $|v\rangle$ to be a null vector, it must satisfy $Q^+|v\rangle=0$. We can evaluate this condition:
$$
Q^+|v\rangle = Q^+Q^-|\Lambda\rangle = (\{Q^+, Q^-\} - Q^-Q^+)|\Lambda\rangle = \{Q^+, Q^-\}|\Lambda\rangle
$$
The last step follows because $Q^+|\Lambda\rangle = 0$. Since the anticommutator $\{Q^+, Q^-\}$ is an even operator in the Cartan subalgebra, $\{Q^+, Q^-\}|\Lambda\rangle$ will be proportional to $|\Lambda\rangle$. For $|v\rangle$ to be a null vector, this must be zero. This leads to an algebraic condition on the highest-weight labels. For a hypothetical algebra with $\{Q^+, Q^-\} = C + \beta H$, where $H|\Lambda\rangle = h|\Lambda\rangle$ and $C|\Lambda\rangle = c|\Lambda\rangle$, the atypicality condition is $c + \beta h = 0$ [@problem_id:757626].

#### The Formal Condition for Typicality

This idea can be formalized. For a Lie superalgebra with a set of positive even roots $\Delta_0^+$ and positive odd roots $\Delta_1^+$, a [highest weight](@entry_id:202808) $\Lambda$ is typical if and only if:
$$
(\Lambda + \rho, \beta) \neq 0 \quad \text{for all odd roots } \beta \in \Delta_1^+
$$
Here, $(\cdot, \cdot)$ is the [invariant bilinear form](@entry_id:137662) on the dual of the Cartan subalgebra, and $\rho$ is the **super-Weyl vector** (or graded Weyl vector), defined as $\rho = \rho_0 - \rho_1$, where $\rho_0 = \frac{1}{2}\sum_{\alpha \in \Delta_0^+} \alpha$ and $\rho_1 = \frac{1}{2}\sum_{\beta \in \Delta_1^+} \beta$. The minus sign in the definition of $\rho$ is a uniquely "super" feature.

For $\mathfrak{gl}(2|1)$, with [highest weight](@entry_id:202808) $\Lambda = (\lambda_1, \lambda_2, d)$ and positive odd roots $\beta_1 = \epsilon_1 - \delta_1$ and $\beta_2 = \epsilon_2 - \delta_1$, one can compute the super-Weyl vector $\rho$ and evaluate the two conditions $(\Lambda+\rho, \beta_1) \neq 0$ and $(\Lambda+\rho, \beta_2) \neq 0$. This yields a polynomial condition for typicality: $(\lambda_1 + d + 1)(\lambda_2 + d) \neq 0$ [@problem_id:757694]. The representation is atypical if this product is zero.

#### The Explicit Construction of Null Vectors

When an atypicality condition is satisfied, a null vector is guaranteed to exist. To make this concept concrete, we can explicitly construct it. Consider the Lie superalgebra $\mathfrak{sl}(2|1)$ and a Verma module whose highest weight $(\lambda, j)$ satisfies an atypicality condition. For the specific case where $\lambda - j = 2$, a null vector $|\chi\rangle$ exists at level 2. This means it is a linear combination of states formed by applying two lowering operators to $|\Lambda\rangle$. This vector can be written as:
$$
|\chi\rangle = f|\Lambda\rangle + C \, q_-s_-|\Lambda\rangle
$$
where $f, q_-, s_-$ are lowering operators and $C$ is a constant to be determined. The condition that $|\chi\rangle$ is a null vector is that it must be annihilated by all raising operators, e.g., $e|\chi\rangle = 0$. By applying $e$ and using the commutation relations of the algebra, we can solve for $C$.
$$
e|\chi\rangle = e(f|\Lambda\rangle) + C e(q_-s_-|\Lambda\rangle) = [e,f]|\Lambda\rangle + C ([e,q_-]s_- + q_-[e,s_-])|\Lambda\rangle
$$
Evaluating the (anti)commutators and using the fact that $|\Lambda\rangle$ is a highest-weight state allows one to express the entire result in terms of $|\Lambda\rangle$. Setting the total coefficient to zero yields an equation for $C$. For a module with weights $\lambda=1, j=-1$, this procedure gives $C = -1$ [@problem_id:757628]. This explicit construction demonstrates the tangible consequences of atypicality and provides the starting point for building [irreducible representations](@entry_id:138184) by factoring out the submodules generated by such [null vectors](@entry_id:155273).