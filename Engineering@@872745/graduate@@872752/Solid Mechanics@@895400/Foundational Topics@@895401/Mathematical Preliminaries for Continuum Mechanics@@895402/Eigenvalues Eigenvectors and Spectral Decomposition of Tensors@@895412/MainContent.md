## Introduction
In the study of [continuum mechanics](@entry_id:155125), tensors are the fundamental mathematical objects used to describe [physical quantities](@entry_id:177395) that possess both magnitude and direction-dependent properties, such as stress and strain. While a tensor can be represented by a matrix of components, its true physical nature is revealed through its intrinsic characteristics, which are independent of any chosen coordinate system. Eigenvalues, eigenvectors, and the powerful concept of [spectral decomposition](@entry_id:148809) are the primary tools for uncovering these intrinsic properties. They bridge the gap between abstract linear algebra and tangible physical phenomena, allowing us to distill complex [tensor fields](@entry_id:190170) into their most meaningful components: [principal values](@entry_id:189577) and [principal directions](@entry_id:276187). This article provides a graduate-level exploration of this essential topic, demonstrating why [spectral analysis](@entry_id:143718) is a cornerstone of modern [solid mechanics](@entry_id:164042).

To build a comprehensive understanding, our discussion is structured across three key chapters. The first, **Principles and Mechanisms**, establishes the theoretical foundation, beginning with the algebraic definition of the eigenvalue problem and its physical interpretation for stress. It delves into the profound consequences of [tensor symmetry](@entry_id:191651), culminating in the Spectral Theorem and the formulation of spectral decomposition. The chapter also explores advanced topics, including functions of tensors and the analysis of non-[symmetric tensors](@entry_id:148092) via Singular Value Decomposition (SVD). The second chapter, **Applications and Interdisciplinary Connections**, showcases these principles in action, illustrating their use in the kinematics of [deformable bodies](@entry_id:201887), the formulation of [material failure criteria](@entry_id:189510), and the development of robust computational methods. Finally, the **Hands-On Practices** section provides a set of guided problems to solidify your computational skills and deepen your physical intuition, from calculating [principal stresses](@entry_id:176761) to verifying fundamental tensor theorems.

## Principles and Mechanisms

### The Eigenvalue Problem for Second-Order Tensors

#### The Algebraic Definition of Eigenvalues and Eigenvectors

At its most fundamental level, the concept of an eigenvector of a linear operator is purely algebraic. Consider a second-order tensor $\mathbf{T}$ as a [linear map](@entry_id:201112) that transforms vectors within a vector space $V$, i.e., $\mathbf{T}: V \to V$. An **eigenvector** of $\mathbf{T}$ is a non-[zero vector](@entry_id:156189) $\mathbf{n} \in V$ whose direction is unchanged by the transformation. The action of $\mathbf{T}$ on $\mathbf{n}$ is merely to scale it by a factor $\lambda$. This relationship is captured by the fundamental **[eigenvalue equation](@entry_id:272921)**:

$$
\mathbf{T}\mathbf{n} = \lambda\mathbf{n}
$$

Here, the scalar $\lambda$ is the **eigenvalue** associated with the eigenvector $\mathbf{n}$. This definition relies solely on the vector space axioms ([vector addition and scalar multiplication](@entry_id:151375)) and the linearity of the operator $\mathbf{T}$. It notably does not require any geometric notions such as length, angle, or orthogonality, which are introduced by an inner product [@problem_id:2633198].

The eigenvalue equation can be rearranged into a homogeneous linear system:

$$
(\mathbf{T} - \lambda\mathbf{I})\mathbf{n} = \mathbf{0}
$$

where $\mathbf{I}$ is the identity tensor. For a non-zero eigenvector $\mathbf{n}$ to exist, the operator $(\mathbf{T} - \lambda\mathbf{I})$ must be singular, which means its determinant must be zero. This gives rise to the **[characteristic equation](@entry_id:149057)**:

$$
\det(\mathbf{T} - \lambda\mathbf{I}) = 0
$$

For a tensor in three-dimensional space, this is a cubic polynomial in $\lambda$. Its roots are the eigenvalues of $\mathbf{T}$. For each eigenvalue $\lambda_i$, the corresponding eigenvectors form a subspace called the **eigenspace**, which is the kernel (or null space) of the operator $(\mathbf{T} - \lambda_i\mathbf{I})$.

#### Physical Interpretation: Principal Stresses and Directions

The abstract concept of eigenvalues and eigenvectors finds a profound and tangible application in continuum mechanics in the analysis of stress. At any point within a deformable body, the state of [internal forces](@entry_id:167605) is described by the symmetric Cauchy stress tensor, $\boldsymbol{\sigma}$. According to Cauchy's stress theorem, the [traction vector](@entry_id:189429) $\mathbf{t}$ (force per unit area) acting on an arbitrary internal plane with [unit normal vector](@entry_id:178851) $\mathbf{n}$ is given by the [linear transformation](@entry_id:143080):

$$
\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}
$$

In general, the traction vector $\mathbf{t}$ has both a normal component (parallel to $\mathbf{n}$) and a shear component (tangential to the plane). A question of primary physical interest is to identify the specific planes on which the shear stress vanishes. On such a plane, the traction vector $\mathbf{t}$ must be purely normal, meaning it is collinear with the normal vector $\mathbf{n}$. This physical condition can be written as:

$$
\mathbf{t} = \lambda\mathbf{n}
$$

where $\lambda$ is the magnitude of the normal stress on that plane. Combining this with Cauchy's theorem, we arrive directly at the [eigenvalue equation](@entry_id:272921) for the stress tensor:

$$
\boldsymbol{\sigma}\mathbf{n} = \lambda\mathbf{n}
$$

This provides a powerful physical interpretation:
- The **eigenvalues** of the Cauchy stress tensor $\boldsymbol{\sigma}$ are the **principal stresses**. These are the [normal stresses](@entry_id:260622) on planes where the shear stress is zero.
- The **eigenvectors** of $\boldsymbol{\sigma}$ are the **[principal directions](@entry_id:276187)**. These are the normal vectors to the planes of zero shear stress [@problem_id:2633158].

#### Invariance and Objectivity of Principal Values

A key reason for the importance of [principal stresses and directions](@entry_id:193792) is that they are **objective [physical observables](@entry_id:154692)**. Their values do not depend on the coordinate system chosen by an observer to describe them. This can be shown by considering a change of [orthonormal basis](@entry_id:147779), represented by an orthogonal tensor $\mathbf{Q}$. The components of the stress tensor in the new basis are given by the transformation rule $\boldsymbol{\sigma}' = \mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^{\mathsf{T}}$, and a vector's components transform as $\mathbf{n}' = \mathbf{Q}\mathbf{n}$.

If $\boldsymbol{\sigma}\mathbf{n} = \lambda\mathbf{n}$ in the original basis, we can examine the action of the transformed tensor $\boldsymbol{\sigma}'$ on the transformed vector $\mathbf{n}'$:
$$
\boldsymbol{\sigma}'\mathbf{n}' = (\mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^{\mathsf{T}})(\mathbf{Q}\mathbf{n}) = \mathbf{Q}\boldsymbol{\sigma}(\mathbf{Q}^{\mathsf{T}}\mathbf{Q})\mathbf{n} = \mathbf{Q}(\boldsymbol{\sigma}\mathbf{n})
$$
Substituting the original eigenvalue equation gives:
$$
\boldsymbol{\sigma}'\mathbf{n}' = \mathbf{Q}(\lambda\mathbf{n}) = \lambda(\mathbf{Q}\mathbf{n}) = \lambda\mathbf{n}'
$$
This demonstrates that the transformed tensor $\boldsymbol{\sigma}'$ has the *exact same eigenvalue* $\lambda$ with a corresponding eigenvector $\mathbf{n}'$. Thus, the principal stresses (eigenvalues) are [scalar invariants](@entry_id:193787). The [principal directions](@entry_id:276187) (eigenvectors) are also invariant physical directions in space, whose representations simply transform from one coordinate system to another [@problem_id:2633158].

### The Spectral Theorem for Symmetric Tensors

#### The Role of Symmetry and Inner Products

While the [eigenvalue problem](@entry_id:143898) can be stated purely algebraically, its most powerful and elegant properties emerge when the tensor possesses **symmetry**. In the context of continuum mechanics, the [balance of angular momentum](@entry_id:181848) requires the Cauchy stress tensor $\boldsymbol{\sigma}$ to be symmetric.

Formally, a tensor $\mathbf{T}$ is defined as **self-adjoint** or **symmetric** with respect to a given inner product $\langle \cdot, \cdot \rangle$ if it satisfies the condition:
$$
\langle \mathbf{T}\mathbf{u}, \mathbf{v} \rangle = \langle \mathbf{u}, \mathbf{T}\mathbf{v} \rangle \quad \text{for all } \mathbf{u}, \mathbf{v} \in V
$$
It is crucial to recognize that symmetry is a property defined relative to an inner product. A tensor that is symmetric with respect to one inner product may not be symmetric with respect to another. However, in standard Euclidean space, the canonical inner product is the dot product, and a tensor is symmetric with respect to the dot product if and only if its component matrix is symmetric ($T_{ij} = T_{ji}$) in any [orthonormal basis](@entry_id:147779) [@problem_id:2633198]. For the remainder of this chapter, "symmetric" will imply self-adjointness with respect to the standard dot product unless otherwise specified.

#### The Spectral Theorem

The symmetry of a tensor has profound geometric consequences for its eigensystem, which are summarized by the **Spectral Theorem** for real [symmetric tensors](@entry_id:148092). For any symmetric second-order tensor $\mathbf{T}$ in a finite-dimensional real [inner product space](@entry_id:138414), the following are true:
1.  All eigenvalues of $\mathbf{T}$ are real numbers.
2.  Eigenvectors corresponding to distinct eigenvalues are mutually orthogonal.
3.  There exists an [orthonormal basis](@entry_id:147779) for the entire space consisting of eigenvectors of $\mathbf{T}$.

The reality of eigenvalues ensures that concepts like principal stresses are always real [physical quantities](@entry_id:177395). The orthogonality of eigenvectors corresponding to distinct eigenvalues is a direct consequence of symmetry. If $\boldsymbol{\sigma}\mathbf{n}_1 = \sigma_1\mathbf{n}_1$ and $\boldsymbol{\sigma}\mathbf{n}_2 = \sigma_2\mathbf{n}_2$ with $\sigma_1 \neq \sigma_2$, then:
$$
\sigma_1 (\mathbf{n}_1 \cdot \mathbf{n}_2) = (\sigma_1 \mathbf{n}_1) \cdot \mathbf{n}_2 = (\boldsymbol{\sigma}\mathbf{n}_1) \cdot \mathbf{n}_2 = \mathbf{n}_1 \cdot (\boldsymbol{\sigma}\mathbf{n}_2) = \mathbf{n}_1 \cdot (\sigma_2 \mathbf{n}_2) = \sigma_2 (\mathbf{n}_1 \cdot \mathbf{n}_2)
$$
This implies $(\sigma_1 - \sigma_2)(\mathbf{n}_1 \cdot \mathbf{n}_2) = 0$. Since $\sigma_1 \neq \sigma_2$, we must have $\mathbf{n}_1 \cdot \mathbf{n}_2 = 0$, confirming orthogonality [@problem_id:2686494].

#### Spectral Decomposition

The existence of an [orthonormal basis of eigenvectors](@entry_id:180262) $\{\mathbf{n}_1, \mathbf{n}_2, \mathbf{n}_3\}$ allows any symmetric tensor $\mathbf{T}$ to be expressed in a simple and powerful form known as its **[spectral decomposition](@entry_id:148809)**:

$$
\mathbf{T} = \sum_{i=1}^{3} \lambda_i \mathbf{n}_i \otimes \mathbf{n}_i
$$

Here, $\lambda_i$ is the eigenvalue corresponding to the unit eigenvector $\mathbf{n}_i$, and the term $\mathbf{n}_i \otimes \mathbf{n}_i$ is the **[dyadic product](@entry_id:748716)**, which represents a [rank-one tensor](@entry_id:202127). This tensor acts as an orthogonal projector onto the one-dimensional subspace spanned by $\mathbf{n}_i$. The decomposition expresses the tensor $\mathbf{T}$ as a weighted sum of its orthogonal [spectral projectors](@entry_id:755184). This form is exceptionally useful as it diagonalizes the tensor; in the basis of its own eigenvectors, the [matrix representation](@entry_id:143451) of $\mathbf{T}$ is simply:

$$
[\mathbf{T}]_{\{\mathbf{n}_i\}} = \begin{pmatrix} \lambda_1 & 0 & 0 \\ 0 & \lambda_2 & 0 \\ 0 & 0 & \lambda_3 \end{pmatrix}
$$

For example, consider the symmetric stress tensor given by the matrix $\boldsymbol{\sigma} = \begin{pmatrix} 5 & 2 & 0 \\ 2 & 1 & 0 \\ 0 & 0 & 3 \end{pmatrix}$. Its eigenvalues are found to be $\sigma_1 = 3+2\sqrt{2}$, $\sigma_2 = 3-2\sqrt{2}$, and $\sigma_3 = 3$. The corresponding orthonormal eigenvectors (principal directions) can be calculated. The spectral decomposition then expresses the original tensor as a sum of three weighted projectors, one for each principal direction [@problem_id:2686494].

#### Connection to Principal Invariants

The eigenvalues of a tensor are intrinsically linked to its **[principal invariants](@entry_id:193522)**, which are scalar quantities that remain unchanged under any change of basis. For a second-order tensor $\mathbf{T}$ in three dimensions, the three [principal invariants](@entry_id:193522) are:

$$
\begin{align*}
I_1(\mathbf{T}) = \mathrm{tr}(\mathbf{T}) \\
I_2(\mathbf{T}) = \frac{1}{2} \left[ (\mathrm{tr}\mathbf{T})^2 - \mathrm{tr}(\mathbf{T}^2) \right] \\
I_3(\mathbf{T}) = \det(\mathbf{T})
\end{align*}
$$

These invariants are, in fact, the coefficients of the characteristic polynomial. The [characteristic equation](@entry_id:149057) for any eigenvalue $\lambda$ can be written as:

$$
\lambda^3 - I_1(\mathbf{T})\lambda^2 + I_2(\mathbf{T})\lambda - I_3(\mathbf{T}) = 0
$$

This relationship is profound because it means that the eigenvalues (e.g., principal stresses) are completely determined by the tensor's invariants. In terms of the eigenvalues $\lambda_1, \lambda_2, \lambda_3$, the invariants are the [elementary symmetric polynomials](@entry_id:152224):
- $I_1 = \lambda_1 + \lambda_2 + \lambda_3$
- $I_2 = \lambda_1\lambda_2 + \lambda_2\lambda_3 + \lambda_3\lambda_1$
- $I_3 = \lambda_1\lambda_2\lambda_3$

For a [symmetric tensor](@entry_id:144567), all three eigenvalues are guaranteed to be real. They are distinct if and only if the discriminant of the characteristic cubic polynomial is positive, $\Delta > 0$, where $\Delta = 18 I_1 I_2 I_3 - 4 I_1^3 I_3 + I_1^2 I_2^2 - 4 I_2^3 - 27 I_3^2$ [@problem_id:2633187].

### Generalizations and Advanced Topics

#### Functions of Symmetric Tensors

The spectral decomposition provides an elegant and powerful way to define functions of a symmetric tensor. For a polynomial function $p(x)$, the tensor $p(\mathbf{T})$ is defined naturally. Using the spectral decomposition and the property that $(\mathbf{n}_i \otimes \mathbf{n}_i)(\mathbf{n}_j \otimes \mathbf{n}_j) = \delta_{ij}(\mathbf{n}_i \otimes \mathbf{n}_i)$, it is straightforward to show that:
$$
\mathbf{T}^k = \sum_{i=1}^{3} \lambda_i^k \mathbf{n}_i \otimes \mathbf{n}_i
$$
From this, it follows that for any polynomial $p(x)$,
$$
p(\mathbf{T}) = \sum_{i=1}^{3} p(\lambda_i) \mathbf{n}_i \otimes \mathbf{n}_i
$$
This result is known as the **[spectral mapping theorem](@entry_id:264489) for polynomials**.

This definition can be extended from polynomials to any continuous function $f(x)$ on an interval containing the eigenvalues of $\mathbf{T}$. By the Weierstrass Approximation Theorem, any such continuous function can be uniformly approximated by a sequence of polynomials $\{p_k\}$. The tensor function $f(\mathbf{T})$ is then defined as the limit of $p_k(\mathbf{T})$. This leads to the general definition for a **function of a [symmetric tensor](@entry_id:144567)**:

$$
f(\mathbf{T}) = \sum_{i=1}^{3} f(\lambda_i) \mathbf{n}_i \otimes \mathbf{n}_i
$$

This form of **[functional calculus](@entry_id:138358)** is indispensable in modern [continuum mechanics](@entry_id:155125) for defining key tensors in constitutive laws. For instance, in [finite strain theory](@entry_id:176941), the [right stretch tensor](@entry_id:193756) $\mathbf{U}$ is defined as the unique [positive definite](@entry_id:149459) square root of the right Cauchy-Green tensor $\mathbf{C}$, i.e., $\mathbf{U} = \mathbf{C}^{1/2}$. This is computed by applying the function $f(x) = \sqrt{x}$ to the eigenvalues of $\mathbf{C}$ in its spectral decomposition [@problem_id:2633190].

#### The Case of Degenerate Eigenvalues

A situation of special interest arises when two or more eigenvalues of a [symmetric tensor](@entry_id:144567) are equal, a condition known as **degeneracy**. For instance, an axisymmetric stress state leads to two equal principal stresses. If $\lambda_1 = \lambda_2 = \lambda \neq \lambda_3$, the [eigenspace](@entry_id:150590) associated with $\lambda$ is no longer a unique line but a two-dimensional plane (the plane orthogonal to the eigenvector for $\lambda_3$).

In this case, any non-[zero vector](@entry_id:156189) in this plane is an eigenvector. It is no longer possible to identify a unique pair of eigenvectors for the degenerate eigenvalue; any orthonormal basis for the plane will consist of valid eigenvectors. However, the [spectral decomposition](@entry_id:148809) itself remains unique and well-defined. The key is to express the decomposition in terms of projectors onto the distinct **eigenspaces**. The decomposition becomes:

$$
\mathbf{T} = \lambda \mathbf{P}_{12} + \lambda_3 \mathbf{P}_3
$$

Here, $\mathbf{P}_3 = \mathbf{n}_3 \otimes \mathbf{n}_3$ is the unique rank-1 projector onto the eigenspace of $\lambda_3$. The object $\mathbf{P}_{12}$ is the **unique** rank-2 projector onto the degenerate eigenspace (the plane). While $\mathbf{P}_{12}$ can be written as $\mathbf{e}_1 \otimes \mathbf{e}_1 + \mathbf{e}_2 \otimes \mathbf{e}_2$ for any orthonormal basis $\{\mathbf{e}_1, \mathbf{e}_2\}$ of the plane, the projector tensor $\mathbf{P}_{12}$ itself is independent of this choice. It can be uniquely determined from the identity $\mathbf{P}_{12} = \mathbf{I} - \mathbf{P}_3$, or directly from the tensor and its eigenvalues via the formula:
$$
\mathbf{P}_{12} = \frac{\mathbf{T} - \lambda_3 \mathbf{I}}{\lambda - \lambda_3}
$$
This demonstrates that while individual eigenvectors are not unique in a degenerate eigenspace, the [spectral projectors](@entry_id:755184) and the overall decomposition remain unique and objective properties of the tensor [@problem_id:2633191].

#### The Deviatoric Tensor

In many areas of mechanics, particularly plasticity, it is useful to decompose a tensor into its volumetric (or spherical) and deviatoric parts. The **deviatoric part** of a tensor $\mathbf{T}$, denoted $\mathrm{dev}(\mathbf{T})$ or $\mathbf{T}'$, is defined as:

$$
\mathrm{dev}(\mathbf{T}) = \mathbf{T} - \frac{1}{3}(\mathrm{tr}\mathbf{T})\mathbf{I}
$$

By construction, the [deviatoric tensor](@entry_id:185837) is always **traceless**: $\mathrm{tr}(\mathrm{dev}\mathbf{T}) = 0$. The deviator operation is covariant, meaning that under an orthogonal [change of basis](@entry_id:145142), $\mathrm{dev}(\mathbf{Q}\mathbf{T}\mathbf{Q}^{\mathsf{T}}) = \mathbf{Q}(\mathrm{dev}\mathbf{T})\mathbf{Q}^{\mathsf{T}}$. A remarkable property is that a [symmetric tensor](@entry_id:144567) and its deviator share the same eigenvectors (principal directions). If $\mathbf{T}$ has eigenvalues $\{\lambda_1, \lambda_2, \lambda_3\}$, its deviator $\mathrm{dev}(\mathbf{T})$ has the same eigenvectors, with eigenvalues given by:

$$
\lambda'_i = \lambda_i - \frac{1}{3}(\lambda_1 + \lambda_2 + \lambda_3) = \lambda_i - \frac{1}{3} I_1(\mathbf{T})
$$

This simple relationship makes the analysis of deviatoric quantities straightforward once the eigensystem of the full tensor is known [@problem_id:2633192].

### Beyond Symmetry: Non-Normal Tensors and SVD

The elegant properties of the spectral theorem rely on [tensor symmetry](@entry_id:191651). Many important tensors in mechanics, such as the [velocity gradient](@entry_id:261686) and the deformation gradient, are not symmetric. For a general non-symmetric tensor $\mathbf{L}$, the theory becomes more complex.

#### Left and Right Eigenvectors

For a non-[symmetric tensor](@entry_id:144567) $\mathbf{L}$, one must distinguish between **right eigenvectors** ($\mathbf{r}$) and **left eigenvectors** ($\boldsymbol{\ell}$). They are defined by the following equations:
- Right Eigenvalue Problem: $\mathbf{L}\mathbf{r} = \lambda\mathbf{r}$
- Left Eigenvalue Problem: $\mathbf{L}^{\mathsf{T}}\boldsymbol{\ell} = \lambda\boldsymbol{\ell}$ (or equivalently, $\boldsymbol{\ell}^{\mathsf{T}}\mathbf{L} = \lambda\boldsymbol{\ell}^{\mathsf{T}}$)

While the sets of right and left eigenvalues are identical, the right and left eigenvectors corresponding to the same eigenvalue are generally different. Furthermore, for a non-[symmetric tensor](@entry_id:144567), the guarantee of an orthogonal [eigenbasis](@entry_id:151409) is lost. Eigenvectors corresponding to distinct eigenvalues are still linearly independent, but they are typically not orthogonal [@problem_id:2633185].

The class of tensors that *do* possess an [orthonormal basis of eigenvectors](@entry_id:180262) are called **normal tensors**, defined by the condition $\mathbf{L}^{\mathsf{T}}\mathbf{L} = \mathbf{L}\mathbf{L}^{\mathsf{T}}$. Symmetric tensors are a subset of normal tensors. For a diagonalizable non-normal tensor, the sets of [left and right eigenvectors](@entry_id:173562) form a **biorthogonal** system, meaning $\boldsymbol{\ell}_i \cdot \mathbf{r}_j = 0$ for $\lambda_i \neq \lambda_j$.

#### The Superiority of Singular Value Decomposition (SVD)

For a general non-[symmetric tensor](@entry_id:144567) like the deformation gradient $\mathbf{F}$, its [eigenvalue decomposition](@entry_id:272091) is often of limited physical use. The eigenvalues can be complex, and they are not objective quantities under observer transformations. A far more powerful and physically meaningful tool for analyzing such tensors is the **Singular Value Decomposition (SVD)**.

The SVD theorem states that any real second-order tensor $\mathbf{F}$ can be decomposed into the product:
$$
\mathbf{F} = \mathbf{U}\boldsymbol{\Sigma}\mathbf{V}^{\mathsf{T}}
$$
where:
- $\mathbf{U}$ and $\mathbf{V}$ are orthogonal tensors. The columns of $\mathbf{U}$ are the **[left singular vectors](@entry_id:751233)** and the columns of $\mathbf{V}$ are the **[right singular vectors](@entry_id:754365)**.
- $\boldsymbol{\Sigma}$ is a diagonal matrix whose entries $\sigma_i \ge 0$ are the **singular values** of $\mathbf{F}$.

The SVD is intimately connected to the spectral decomposition of the symmetric, [positive semi-definite](@entry_id:262808) Cauchy-Green strain tensors:
- The right Cauchy-Green tensor: $\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F} = \mathbf{V}\boldsymbol{\Sigma}^2\mathbf{V}^{\mathsf{T}}$
- The left Cauchy-Green tensor: $\mathbf{B} = \mathbf{F}\mathbf{F}^{\mathsf{T}} = \mathbf{U}\boldsymbol{\Sigma}^2\mathbf{U}^{\mathsf{T}}$

This reveals the profound physical meaning of the SVD components in finite-strain [kinematics](@entry_id:173318):
- The **singular values** ($\sigma_i$) of $\mathbf{F}$ are the square roots of the eigenvalues of $\mathbf{C}$ and $\mathbf{B}$. They are the **[principal stretches](@entry_id:194664)**, which are objective and physically measure the stretching of material lines.
- The **[right singular vectors](@entry_id:754365)** (columns of $\mathbf{V}$) are the eigenvectors of $\mathbf{C}$. They represent the orthogonal [principal directions](@entry_id:276187) of strain in the undeformed, reference configuration.
- The **[left singular vectors](@entry_id:751233)** (columns of $\mathbf{U}$) are the eigenvectors of $\mathbf{B}$. They represent the orthogonal principal directions of strain in the deformed, current configuration.

Because SVD directly provides these physically meaningful and objective quantities, it is a cornerstone of [finite deformation](@entry_id:172086) analysis, largely supplanting the standard [eigenvalue decomposition](@entry_id:272091) for non-[symmetric tensors](@entry_id:148092) like $\mathbf{F}$ [@problem_id:2633175].

### Perturbation and Differentiability of Eigensystems

In many advanced problems, such as in [computational mechanics](@entry_id:174464) or when analyzing evolving material properties, tensors depend on a parameter, e.g., $\boldsymbol{\sigma}(\varepsilon)$. This raises questions about the smoothness and differentiability of the corresponding [eigenvalues and eigenvectors](@entry_id:138808).

The behavior of the eigensystem is highly sensitive to eigenvalue degeneracy. If an eigenvalue is simple (non-degenerate), its corresponding eigenvalue and eigenvector vary smoothly with the parameter $\varepsilon$. However, at a point of degeneracy where $\boldsymbol{\sigma}(\varepsilon_0)$ has a repeated eigenvalue, the situation is more subtle.

Consider a symmetric tensor where a perturbation splits a repeated eigenvalue. If one attempts to track an individual eigenvector by ordering the split eigenvalues by magnitude, the resulting eigenvector path is often not continuous, let alone differentiable, at the point of degeneracy. The eigenvector can "jump" from one direction to another as the ordering of eigenvalues switches [@problem_id:2633164].

Despite this, not all is lost. While individual eigenvector paths may not be smooth, the spectral projector onto the entire degenerate eigenspace can be differentiable, provided the group of degenerating eigenvalues remains separated from other eigenvalues. Furthermore, it is often possible to choose a basis of eigenvectors within the evolving eigenspace that depends smoothly on the parameter, even across points of degeneracy. Discovering this smooth basis, however, requires a more sophisticated analysis than simple eigenvalue ordering and is a key topic in advanced [perturbation theory](@entry_id:138766) [@problem_id:2633164]. This subtlety highlights the care that must be taken when working with eigensystems in a computational or dynamic context.