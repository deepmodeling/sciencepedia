## Introduction
In the study of [linear systems](@entry_id:147850), a [state-space model](@entry_id:273798) offers a powerful internal description of system dynamics. However, this representation is not unique; the same system can be described by infinitely many sets of [state-space](@entry_id:177074) matrices depending on the chosen coordinates. This raises a fundamental question: how can we analyze a system's essential properties—like stability, [controllability](@entry_id:148402), and its fundamental modes of behavior—in a way that is independent of our chosen mathematical description? The answer lies in the elegant framework of similarity transformations and the revealing power of [canonical forms](@entry_id:153058). This article demystifies these core concepts, showing how a [change of coordinates](@entry_id:273139) can transform a complex, coupled system into a standardized form that makes its intrinsic structure transparent.

This article will guide you through the theory and application of these transformative tools. In **Principles and Mechanisms**, we will establish the mathematical foundation of similarity transformations as a [change of basis](@entry_id:145142), explore the properties that are preserved (invariants), and detail the construction and meaning of crucial [canonical forms](@entry_id:153058) like the Jordan, controllable, and Schur forms. Following this, **Applications and Interdisciplinary Connections** will illustrate how these abstract concepts are applied to solve real-world problems in [control system design](@entry_id:262002), [modal analysis](@entry_id:163921) in mechanical engineering, and even in leveraging [symmetry in physics](@entry_id:144576) and chemistry. Finally, **Hands-On Practices** will provide opportunities to solidify your understanding through guided problem-solving. We begin by delving into the principles that govern how changing our perspective can simplify our understanding.

## Principles and Mechanisms

The concept of a linear system's representation is foundational to its analysis and design. While a state-space model provides a complete internal description of a system's dynamics, this description is not unique. The choice of state variables, which corresponds to selecting a basis for the [state-space](@entry_id:177074), is often arbitrary. Different choices of basis lead to different state-space matrices, yet the intrinsic properties of the system—such as its stability, input-output behavior, and fundamental dynamic modes—must remain unchanged. **Similarity transformations** are the mathematical framework that formalizes this relationship, allowing us to understand which properties are fundamental and which are merely artifacts of a particular coordinate system. By using these transformations to convert a system into a **[canonical form](@entry_id:140237)**, we can reveal its intrinsic structure in a standardized way, simplifying analysis and enabling systematic design.

### The Similarity Transformation as a Change of Basis

At its core, a similarity transformation is a [change of basis](@entry_id:145142) in a vector space. Let us consider a linear operator $L$ that maps a [finite-dimensional vector space](@entry_id:187130) $V$ to itself, $L: V \to V$. If we choose an ordered basis $\beta$ for $V$, we can represent this operator by a square matrix $A$. This matrix $A$, denoted $[L]_{\beta}$, is the unique matrix that describes how the coordinates of a vector $v$ transform when acted upon by $L$. Specifically, if $[v]_{\beta}$ is the [coordinate vector](@entry_id:153319) of $v$ in the basis $\beta$, then the [coordinate vector](@entry_id:153319) of $L(v)$ is given by $[L(v)]_{\beta} = A [v]_{\beta}$.

Now, suppose we choose a different basis, $\gamma$. In this new basis, the same linear operator $L$ will be represented by a different matrix, say $B = [L]_{\gamma}$. The crucial question is: what is the relationship between $A$ and $B$? Since they represent the same underlying operator, they must be deeply related.

The connection is established through the **[change-of-basis matrix](@entry_id:184480)**. Let $T$ be the invertible matrix that transforms coordinates from the $\gamma$ basis to the $\beta$ basis. That is, for any vector $v \in V$, their coordinate representations are related by $[v]_{\beta} = T [v]_{\gamma}$. This matrix $T$ is often denoted $C_{\beta \leftarrow \gamma}$.

To find the relationship between $A$ and $B$, we consider the action of the operator $L$ in the $\gamma$ basis:
$$[L(v)]_{\gamma} = B [v]_{\gamma}$$
We can transform this equation into the $\beta$ coordinate system by multiplying by the [change-of-basis matrix](@entry_id:184480) $T$:
$$T [L(v)]_{\gamma} = T (B [v]_{\gamma})$$
By the definition of the [change-of-basis matrix](@entry_id:184480), the left side is simply the coordinate representation of $L(v)$ in the $\beta$ basis:
$$[L(v)]_{\beta} = T B [v]_{\gamma}$$
We also know that in the $\beta$ basis, the operator's action is described by $A$: $[L(v)]_{\beta} = A [v]_{\beta}$. Substituting $[v]_{\beta} = T [v]_{\gamma}$ into this equation gives:
$$[L(v)]_{\beta} = A (T [v]_{\gamma})$$
By equating our two expressions for $[L(v)]_{\beta}$, we arrive at:
$$A T [v]_{\gamma} = T B [v]_{\gamma}$$
Since this must hold for any vector $v$, and thus for any [coordinate vector](@entry_id:153319) $[v]_{\gamma}$, we obtain the matrix identity $AT = TB$. Because $T$ is a [change-of-basis matrix](@entry_id:184480), it is invertible. Multiplying by $T^{-1}$ on the left, we get the fundamental relationship:
$$B = T^{-1} A T$$
Two matrices $A$ and $B$ related in this manner are said to be **similar**. This derivation establishes the central principle: two matrices are similar if and only if they represent the same [linear operator](@entry_id:136520) with respect to different bases [@problem_id:2905107].

This principle has profound implications for the analysis of linear time-invariant (LTI) systems. Consider a [state-space model](@entry_id:273798):
$$\dot{x} = Ax + Bu, \quad y = Cx + Du$$
The [state vector](@entry_id:154607) $x$ belongs to the state-space, which is a vector space. We can perform a [change of coordinates](@entry_id:273139) by defining a new [state vector](@entry_id:154607) $z$ such that $x = Tz$, where $T$ is an invertible matrix. Substituting this into the [state-space equations](@entry_id:266994) gives:
$$\frac{d}{dt}(Tz) = A(Tz) + Bu$$
$$y = C(Tz) + Du$$
Since $T$ is a constant matrix, we have $T\dot{z} = ATz + Bu$. Multiplying by $T^{-1}$ on the left yields the new state equation:
$$\dot{z} = (T^{-1}AT)z + (T^{-1}B)u$$
The new output equation is:
$$y = (CT)z + Du$$
Thus, the system in the new coordinates $(z)$ is described by a new set of matrices $(\tilde{A}, \tilde{B}, \tilde{C}, \tilde{D})$ where:
$$\tilde{A} = T^{-1}AT, \quad \tilde{B} = T^{-1}B, \quad \tilde{C} = CT, \quad \tilde{D} = D$$
The new state matrix $\tilde{A}$ is similar to the original state matrix $A$. A crucial consequence of this transformation is that the **input-output relationship of the system remains invariant**. This can be verified by examining the transfer function, $G(s) = C(sI - A)^{-1}B + D$. The new transfer function is:
$$\tilde{G}(s) = \tilde{C}(sI - \tilde{A})^{-1}\tilde{B} + \tilde{D} = (CT)(sI - T^{-1}AT)^{-1}(T^{-1}B) + D$$
Using the identity $(sI - T^{-1}AT)^{-1} = T^{-1}(sI-A)^{-1}T$, we find:
$$\tilde{G}(s) = (CT)[T^{-1}(sI-A)^{-1}T](T^{-1}B) + D = C(TT^{-1})(sI-A)^{-1}(TT^{-1})B + D = C(sI-A)^{-1}B + D = G(s)$$
This confirms that a [similarity transformation](@entry_id:152935) on the [state-space](@entry_id:177074) corresponds to an internal change of coordinates that preserves the external behavior of the system [@problem_id:2905107].

### Invariants and Non-Invariants of Similarity

Since [similar matrices](@entry_id:155833) represent the same underlying operator, they must share all of its intrinsic properties. These shared properties are known as **[similarity invariants](@entry_id:149886)**. Identifying these invariants is key to classifying [linear operators](@entry_id:149003) and systems.

The most fundamental invariant is the **characteristic polynomial**, $\varphi_A(\lambda) = \det(\lambda I - A)$. If $B = T^{-1}AT$, then:
$$\varphi_B(\lambda) = \det(\lambda I - B) = \det(\lambda I - T^{-1}AT) = \det(T^{-1}(\lambda I - A)T)$$
Using the property $\det(XYZ) = \det(X)\det(Y)\det(Z)$, we have:
$$\varphi_B(\lambda) = \det(T^{-1})\det(\lambda I - A)\det(T) = \det(\lambda I - A) = \varphi_A(\lambda)$$
Since the characteristic polynomials are identical, [similar matrices](@entry_id:155833) must have the same set of **eigenvalues** with the same **algebraic multiplicities**. Consequently, other properties derived from eigenvalues are also invariant, such as the **trace** ($\operatorname{tr}(A) = \sum \lambda_i$) and the **determinant** ($\det(A) = \prod \lambda_i$) [@problem_id:2905091].

However, it is equally important to recognize what is *not* an invariant. While eigenvalues are preserved, their corresponding **eigenvectors** are not. If $v$ is an eigenvector of $A$ for eigenvalue $\lambda$ (i.e., $Av = \lambda v$), let's see what the corresponding eigenvector of $B=T^{-1}AT$ is. Let $w = T^{-1}v$. Then:
$$Bw = (T^{-1}AT)(T^{-1}v) = T^{-1}A(TT^{-1})v = T^{-1}(Av) = T^{-1}(\lambda v) = \lambda (T^{-1}v) = \lambda w$$
Thus, $w = T^{-1}v$ is the eigenvector of $B$ for the same eigenvalue $\lambda$. The eigenvector is transformed by the inverse of the [change-of-basis matrix](@entry_id:184480) [@problem_id:2905091].

A critical point of caution is that the converse is not true: two matrices having the same eigenvalues are **not necessarily similar**. Similarity is a much stronger condition. For example, consider the matrices:
$$A = \begin{pmatrix} 2  & 1 & 0 \\ 0 & 2 & 1 \\ 0 & 0 & 2 \end{pmatrix}, \quad B = \begin{pmatrix} 2 & 1 & 0 \\ 0 & 2 & 0 \\ 0 & 0 & 2 \end{pmatrix}$$
Both matrices are upper triangular, so their eigenvalues are the diagonal entries. Both have the single eigenvalue $\lambda=2$ with algebraic multiplicity 3. Their [characteristic polynomial](@entry_id:150909) is $(\lambda-2)^3$ and their trace is 6. However, they are not similar. One way to prove this is to examine another similarity invariant: the **minimal polynomial**. The [minimal polynomial](@entry_id:153598) $m_A(\lambda)$ is the [monic polynomial](@entry_id:152311) of least degree such that $m_A(A) = 0$. For $A$, we find $(A-2I)^2 \neq 0$ but $(A-2I)^3 = 0$, so its [minimal polynomial](@entry_id:153598) is $m_A(\lambda) = (\lambda-2)^3$. For $B$, $(B-2I) \neq 0$ but $(B-2I)^2 = 0$, so its minimal polynomial is $m_B(\lambda) = (\lambda-2)^2$. Since the minimal polynomials differ, the matrices are not similar [@problem_id:2905089]. This shows that eigenvalues alone are insufficient to fully characterize the operator; we need a more descriptive [canonical form](@entry_id:140237).

### The Jordan Canonical Form

The **Jordan Canonical Form (JCF)** provides the definitive answer to the similarity question. The Jordan Normal Form Theorem states that any square matrix $A$ over an [algebraically closed field](@entry_id:151401) (like the complex numbers $\mathbb{C}$) is similar to a [block diagonal matrix](@entry_id:150207) $J$, called the Jordan form of $A$.
$$J = \begin{pmatrix} J_1 & & \\ & J_2 & \\ & & \ddots \end{pmatrix}, \quad \text{where} \quad J_k = \begin{pmatrix} \lambda_k & 1 & & \\ & \lambda_k & \ddots & \\ & & \ddots & 1 \\ & & & \lambda_k \end{pmatrix}$$
Each $J_k$ is a **Jordan block**. Two matrices are similar if and only if they have the same Jordan [canonical form](@entry_id:140237), up to a permutation of the blocks.

The structure of the JCF is intimately linked to the concept of **[generalized eigenvectors](@entry_id:152349)**. For an eigenvalue $\lambda$, an ordinary eigenvector $v$ satisfies $(A-\lambda I)v=0$. A **Jordan chain** of length $m$ is a sequence of vectors $\{v_1, v_2, \dots, v_m\}$ that begins with an eigenvector and extends "upwards":
$$(A-\lambda I)v_1 = 0 \quad (v_1 \neq 0)$$
$$(A-\lambda I)v_2 = v_1$$
$$\vdots$$
$$(A-\lambda I)v_m = v_{m-1}$$
The vectors $v_2, \dots, v_m$ are called [generalized eigenvectors](@entry_id:152349). Each such chain of length $m$ corresponds to one Jordan block of size $m \times m$ in the JCF [@problem_id:2905075]. The transformation matrix $T$ that brings $A$ to its Jordan form $J$ (i.e., $A=TJT^{-1}$) is constructed by using the [generalized eigenvectors](@entry_id:152349) from these chains as its columns.

The JCF reveals several key invariants:
*   The **number of Jordan blocks** associated with an eigenvalue $\lambda$ is equal to its **geometric multiplicity**, defined as $\dim(\ker(A-\lambda I))$. This is the number of linearly independent eigenvectors for $\lambda$ [@problem_id:2905075]. In our previous example [@problem_id:2905089], for $A$, the [geometric multiplicity](@entry_id:155584) of $\lambda=2$ is 1 (one block), while for $B$, it is 2 (two blocks).
*   The **sum of the sizes** of all Jordan blocks for $\lambda$ equals its **[algebraic multiplicity](@entry_id:154240)**.
*   The **size of the largest Jordan block** for $\lambda$ determines the exponent of the factor $(\lambda-\lambda_i)$ in the **minimal polynomial**.

### Canonical Forms in State-Space Models

While the JCF provides a complete theoretical classification, other [canonical forms](@entry_id:153058) are often more useful in control theory, as they expose properties like [controllability and observability](@entry_id:174003) in a more direct way.

A prominent example is the **[controllable canonical form](@entry_id:165254)**. For a controllable single-input system, it is always possible to find a basis in which the system dynamics take on a specific "companion matrix" structure. For an $n$-th order system with [characteristic polynomial](@entry_id:150909) $\lambda^n + a_{n-1}\lambda^{n-1} + \dots + a_0 = 0$, the controllable [companion form](@entry_id:747524) is:
$$A_c = \begin{pmatrix} 0 & 1 & 0 & \cdots & 0 \\ 0 & 0 & 1 & \cdots & 0 \\ \vdots & & \ddots & & \vdots \\ 0 & 0 & 0 & \cdots & 1 \\ -a_0 & -a_1 & -a_2 & \cdots & -a_{n-1} \end{pmatrix}, \quad B_c = \begin{pmatrix} 0 \\ 0 \\ \vdots \\ 0 \\ 1 \end{pmatrix}$$
(Note: Variations exist, such as placing the coefficients in the first row or using a lower [companion matrix](@entry_id:148203).)

One way to achieve this form is by choosing a specific basis for the state-space: the **Krylov basis** generated by the input matrix $B$. If a single-input system $(A,b)$ is controllable, its [controllability matrix](@entry_id:271824) $\mathcal{C}(A,b) = [b \ Ab \ \dots \ A^{n-1}b]$ is invertible. If we choose this matrix as our change-of-[basis transformation](@entry_id:189626) $T = \mathcal{C}(A,b)$, the new system matrices will be in controllable [companion form](@entry_id:747524) [@problem_id:2905002]. This transformation is particularly useful as the [companion form](@entry_id:747524) has a maximally sparse structure for a controllable system, with only $2n-1$ non-zero entries.

Conversely, given a transfer function $G(s) = \frac{b(s)}{a(s)}$, we can directly write down a [state-space realization](@entry_id:166670) in a [canonical form](@entry_id:140237). For instance, for $a(s) = s^n + a_{n-1}s^{n-1} + \dots + a_0$ and $b(s) = b_{n-1}s^{n-1} + \dots + b_0$, the following realization, known as the **[observable canonical form](@entry_id:173085)**, has $G(s)$ as its transfer function [@problem_id:2905023]:
$$A_o = \begin{pmatrix} 0 & 0 & \dots & -a_0 \\ 1 & 0 & \dots & -a_1 \\ \vdots & & \ddots & & \vdots \\ 0 & \dots & 1 & -a_{n-1} \end{pmatrix}, \quad B_o = \begin{pmatrix} b_0 \\ b_1 \\ \vdots \\ b_{n-1} \end{pmatrix}, \quad C_o = \begin{pmatrix} 0 & 0 & \dots & 1 \end{pmatrix}$$
The [characteristic polynomial](@entry_id:150909) of $A_o$ is exactly $a(s)$, the denominator of the transfer function.

### Minimality, Realizations, and Decomposition

The connection between transfer functions and [state-space models](@entry_id:137993) brings up the crucial concept of **minimality**. A [state-space realization](@entry_id:166670) is **minimal** if it is both controllable and observable. The dimension of a [minimal realization](@entry_id:176932) is a unique property of the transfer function, known as its **McMillan degree**.

A fundamental theorem of realization theory states that any two minimal realizations of the same transfer function are related by a unique similarity transformation [@problem_id:2905042]. This means that for a given input-output behavior, there is essentially only one internal description, up to a choice of coordinates. This unique similarity transformation $T$ can be explicitly constructed using the [controllability and observability](@entry_id:174003) matrices of the two minimal realizations, $(\mathcal{C}_1, \mathcal{O}_1)$ and $(\mathcal{C}_2, \mathcal{O}_2)$. The transformation is given by [@problem_id:2905065]:
$$T = \mathcal{C}_2 \mathcal{C}_1^{-1} \quad \text{and} \quad T = (\mathcal{O}_1^{-1} \mathcal{O}_2)^{-1} = \mathcal{O}_2^{-1} \mathcal{O}_1$$

What if a realization is not minimal? A non-[minimal realization](@entry_id:176932) has a state dimension larger than the McMillan degree. This implies the presence of "hidden" dynamic modes that are either uncontrollable or unobservable (or both). These modes are canceled out in the [pole-zero cancellation](@entry_id:261496) when computing the transfer function, so they do not affect the input-output behavior [@problem_id:2905042]. Consequently, a non-[minimal realization](@entry_id:176932) can never be similar to a minimal one, as similarity transformations preserve dimension.

The **Kalman Decomposition Theorem** provides a complete framework for understanding the structure of any linear system, minimal or not. It states that any state-space can be decomposed by a [similarity transformation](@entry_id:152935) into four subspaces, revealing which parts of the system are:
1.  Controllable and Observable ($\mathcal{S}_{co}$)
2.  Controllable but Unobservable ($\mathcal{S}_{c\bar{o}}$)
3.  Uncontrollable but Observable ($\mathcal{S}_{\bar{c}o}$)
4.  Uncontrollable and Unobservable ($\mathcal{S}_{\bar{c}\bar{o}}$)

By choosing a basis that respects this decomposition, the system matrices become block-triangular, isolating these four subsystems. The transfer function of the entire system is determined solely by the controllable and observable part, $\mathcal{S}_{co}$ [@problem_id:2905050].

### Numerical Considerations and the Schur Form

While the Jordan form is theoretically perfect, it is **numerically ill-posed**. An arbitrarily small perturbation to a matrix can cause a discontinuous change in its Jordan structure. For example, the matrix $\begin{pmatrix} \lambda & 1 \\ 0 & \lambda \end{pmatrix}$ has one Jordan block of size 2. A tiny perturbation can change it to $\begin{pmatrix} \lambda & 1 \\ \epsilon & \lambda \end{pmatrix}$, which for any $\epsilon \neq 0$ has two distinct eigenvalues $\lambda \pm \sqrt{\epsilon}$ and is therefore diagonalizable (two Jordan blocks of size 1). This instability makes the JCF unsuitable for practical computations involving noisy data from real-world experiments [@problem_id:2905010].

A numerically stable alternative is the **Schur Decomposition**. For any real matrix $A$, there exists an **orthogonal** matrix $Q$ ($Q^T Q = I$) and a **quasi-upper-triangular** matrix $S$ such that:
$$A = QSQ^T$$
The matrix $S$ has the real eigenvalues of $A$ on its diagonal as $1 \times 1$ blocks, and complex conjugate pairs of eigenvalues appear as $2 \times 2$ blocks. The key to numerical stability lies in the orthogonality of $Q$. Orthogonal transformations have a condition number of 1 and do not amplify numerical errors.

While the Schur form is not unique, it can be made into a **[canonical form](@entry_id:140237)** by imposing a fixed set of conventions, such as ordering the eigenvalues along the diagonal according to a specific rule (e.g., lexicographically). This "ordered real Schur form" provides a stable and reliable way to represent the intrinsic dynamics of a system, making it an invaluable tool in system identification and model analysis where data is inevitably corrupted by noise [@problem_id:2905010]. It represents a pragmatic compromise between the theoretical completeness of the Jordan form and the realities of numerical computation.