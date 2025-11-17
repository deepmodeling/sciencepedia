## Introduction
Spinors are fundamental mathematical objects in modern theoretical physics, indispensable for describing particles with intrinsic angular momentum, or spin, within the framework of relativity. Unlike vectors and tensors, which are familiar from classical physics, spinors represent a deeper level of geometric reality, arising from the [representation theory](@entry_id:137998) of [spacetime symmetry](@entry_id:179029) groups. Understanding them requires a journey into the elegant interplay between algebra and geometry, a journey that reveals the underlying structure of the Lorentz group and its profound implications for the quantum world. This article bridges the conceptual gap between intuitive spacetime notions and the abstract formalism required to describe fermionic matter like electrons and quarks.

Across the following chapters, we will systematically build the theory of spinors in Minkowski spacetime from the ground up. The "Principles and Mechanisms" chapter will establish the core mathematical foundation, revealing how the group SL(2,C) serves as the universal cover of the Lorentz group and how this leads directly to the concept of a [spinor](@entry_id:154461). We will then derive the celebrated Dirac equation, explore its covariance, and dissect the structure of its solutions. Next, in "Applications and Interdisciplinary Connections," we will witness the power of this formalism by exploring its pivotal role in quantum field theory, the coupling of fermions to [curved spacetime](@entry_id:184938) in general relativity, and its use in advanced concepts like [supersymmetry](@entry_id:155777) and [twistor theory](@entry_id:158749). Finally, the "Hands-On Practices" section will provide a series of targeted problems designed to solidify your command of the algebraic techniques and their physical interpretations, transforming abstract theory into practical skill.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms governing spinors in Minkowski spacetime. We will build upon the introductory concepts by first establishing the profound connection between the geometry of spacetime and the algebraic structure of the [special linear group](@entry_id:139538) $SL(2, \mathbb{C})$. We will then explore the Lie algebra of the Lorentz group, leading to an understanding of [relativistic kinematics](@entry_id:159064), including the Wigner rotation. Subsequently, we will introduce the Dirac equation and its [spinor](@entry_id:154461) solutions, examining their transformation properties and structure. Finally, we will construct physical states and demonstrate the Lorentz invariance of key observables, providing a robust foundation for the application of [spinors](@entry_id:158054) in relativistic quantum theory.

### The Lorentz Group and its Spinor Representation

The relationship between four-vectors in Minkowski spacetime and the theory of spinors is founded on a remarkable algebraic correspondence. Any [four-vector](@entry_id:160261) $x^\mu = (x^0, x^1, x^2, x^3)$ can be uniquely mapped to a $2 \times 2$ Hermitian matrix, often called a "spinor-matrix" or Pauli vector, defined as:
$$
X = x^\mu \sigma_\mu = x^0 \sigma_0 + x^1 \sigma_1 + x^2 \sigma_2 + x^3 \sigma_3
$$
Here, $\sigma_0$ is the $2 \times 2$ identity matrix $I_2$, and $\sigma_k$ for $k=1,2,3$ are the familiar Pauli matrices:
$$
\sigma_1 = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}, \quad \sigma_2 = \begin{pmatrix} 0 & -i \\ i & 0 \end{pmatrix}, \quad \sigma_3 = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}
$$
Explicitly, the matrix $X$ takes the form:
$$
X = \begin{pmatrix} x^0+x^3 & x^1-ix^2 \\ x^1+ix^2 & x^0-x^3 \end{pmatrix}
$$
A key property of this matrix is its determinant. A straightforward calculation reveals:
$$
\det(X) = (x^0+x^3)(x^0-x^3) - (x^1-ix^2)(x^1+ix^2) = (x^0)^2 - (x^3)^2 - ((x^1)^2 + (x^2)^2) = \eta_{\mu\nu}x^\mu x^\nu
$$
The determinant of the matrix $X$ is precisely the Lorentz-invariant squared interval of the four-vector $x^\mu$. This provides the link to the Lorentz group. Consider a transformation of $X$ by an arbitrary complex $2 \times 2$ matrix $M$ via a **[congruence transformation](@entry_id:154837)**:
$$
X' = M X M^\dagger
$$
where $M^\dagger$ is the conjugate transpose of $M$. This transformation preserves the Hermiticity of the matrix, meaning $X'$ can also be written in the form $x'^\mu \sigma_\mu$. If we now demand that the Lorentz interval be preserved, i.e., $\det(X') = \det(X)$, we must have:
$$
\det(M X M^\dagger) = \det(M) \det(X) \det(M^\dagger) = |\det(M)|^2 \det(X) = \det(X)
$$
This requires $|\det(M)|^2 = 1$. The simplest non-trivial choice is to restrict $M$ to the group of matrices with unit determinant, the **[special linear group](@entry_id:139538) in two complex dimensions**, denoted $SL(2, \mathbb{C})$.

Any transformation on $X$ by an element $M \in SL(2, \mathbb{C})$ induces a linear transformation on the components of the four-vector, $x'^\mu = \Lambda^\mu_{\ \nu} x^\nu$. This transformation $\Lambda$ preserves the Minkowski inner product and, as can be shown, also preserves the direction of time and has a determinant of $+1$. It is therefore an element of the **proper orthochronous Lorentz group**, $SO^+(1,3)$. This establishes a [group homomorphism](@entry_id:140603) from $SL(2, \mathbb{C})$ to $SO^+(1,3)$. It is a **2-to-1 homomorphism**, as both $M$ and $-M$ in $SL(2, \mathbb{C})$ produce the same Lorentz transformation $\Lambda$, since the transformation on $X$ is quadratic in $M$. This makes $SL(2, \mathbb{C})$ the **universal (double) [covering group](@entry_id:161571)** of $SO^+(1,3)$. Objects that transform under $SL(2, \mathbb{C})$ are the simplest type of [spinors](@entry_id:158054), known as **Weyl spinors**.

To make this correspondence concrete, we can extract the components of the Lorentz matrix $\Lambda$ given a specific $SL(2, \mathbb{C})$ matrix $M$. The components of the transformed vector $x'^\mu$ can be recovered from the [matrix elements](@entry_id:186505) of $X'$ using the trace properties of Pauli matrices, for example, $x'^1 = \frac{1}{2}\text{Tr}(X'\sigma_1) = \frac{1}{2}(X'_{12} + X'_{21})$. As an illustrative exercise [@problem_id:1028170], consider the matrix $M = \begin{pmatrix} 1+i & 2 \\ i & \frac{3+i}{2} \end{pmatrix}$. To find the component $\Lambda^1_{\ 2}$ of the corresponding Lorentz transformation, we can consider its action on a basis vector, say $x^\mu = (0,0,1,0)$. This corresponds to the matrix $X = \sigma_2$. The transformed matrix is $X' = M \sigma_2 M^\dagger$. By performing the matrix multiplication, one finds the $(1,2)$ component of $X'$ to be $X'_{12} = 3-2i$. Since $X'$ must be Hermitian, $X'_{21} = \overline{X'_{12}} = 3+2i$. The new vector component $x'^1$ is then given by $x'^1 = \frac{1}{2}(X'_{12} + X'_{21}) = \text{Re}(X'_{12}) = 3$. Since the initial vector was a unit vector in the $x^2$ direction, this resulting $x'^1$ component is precisely the value of $\Lambda^1_{\ 2}$.

### Generators, Lie Algebra, and Relativistic Kinematics

The deep connection between groups is most clearly revealed at the level of their Lie algebras. An infinitesimal Lorentz transformation can be written as $\Lambda^\mu_{\ \nu} \approx \delta^\mu_\nu + \omega^\mu_{\ \nu}$, where $\omega_{\mu\nu}$ is an [antisymmetric tensor](@entry_id:191090) of infinitesimal parameters. The corresponding $SL(2, \mathbb{C})$ matrix is infinitesimally close to the identity: $A \approx I + G$, where $G$ is an element of the Lie algebra $sl(2, \mathbb{C})$. The condition $\det(A)=1$ implies, to first order, that $\text{Tr}(G)=0$. The algebra $sl(2, \mathbb{C})$ is the set of all $2 \times 2$ complex traceless matrices. A convenient basis for this algebra is given by the three Pauli matrices $\sigma_k$.

The six generators of the Lorentz group correspond to three rotations and three boosts. We can find their explicit form in the $sl(2, \mathbb{C})$ algebra. A rotation by an infinitesimal angle $\delta\theta$ about the $x^3$-axis is given by $\omega_{12} = -\omega_{21} = \delta\theta$. The corresponding generator in $SL(2, \mathbb{C})$ is $J_3 = \frac{i}{2}\sigma_3$. In general, the generators of rotations about an axis $\mathbf{n}$ are given by $J(\mathbf{n}) = \frac{i}{2}(\mathbf{n}\cdot\boldsymbol{\sigma})$. The factor of $i$ makes these generators anti-Hermitian, as required for unitary rotation matrices $R = \exp(\theta_k J_k)$.

A boost is characterized by a [rapidity](@entry_id:265131) vector $\boldsymbol{\zeta}$. An infinitesimal boost with rapidity $\delta\eta$ along the $x^1$-axis is given by $\omega^0_{\ 1} = \omega^1_{\ 0} = \delta\eta$. The associated generator in $sl(2, \mathbb{C})$ can be found by expanding the fundamental relation $A \sigma^\mu A^\dagger = \Lambda^\mu_{\ \nu} \sigma^\nu$ to first order in the infinitesimal parameters. For a boost along $x^1$, we set $A \approx I + \delta\eta K_1$ and $\Lambda^\mu_{\ \nu} \approx \delta^\mu_\nu + \delta\eta(\delta^\mu_0\delta^1_\nu + \delta^\mu_1\delta^0_\nu)$. Substituting these into the transformation law and keeping terms of order $\delta\eta$ yields the relation $[K_1, \sigma^\mu] + \{\sigma^\mu, K_1^\dagger\} = \delta^\mu_0\sigma^1 + \delta^\mu_1\sigma^0$. Solving this system of [matrix equations](@entry_id:203695) for the traceless matrix $K_1$ reveals that $K_1 = \frac{1}{2}\sigma_1$ [@problem_id:1028264]. In general, the generator for a boost in the direction $\mathbf{n}$ is $K(\mathbf{n}) = \frac{1}{2}(\mathbf{n}\cdot\boldsymbol{\sigma})$. These generators are Hermitian, yielding non-unitary boost matrices $B = \exp(-\zeta_k K_k)$.

A profound consequence of the Lorentz group's structure is that the composition of two non-collinear boosts is not a pure boost, but a boost combined with a rotation. This is known as **Wigner rotation**. This phenomenon can be elegantly demonstrated using the Lie algebra of $SL(2, \mathbb{C})$. Consider two successive infinitesimal boosts, $B(\delta\boldsymbol{\zeta}_1)$ followed by $B(\delta\boldsymbol{\zeta}_2)$. The composite transformation is $A_{comp} = B(\delta\boldsymbol{\zeta}_2)B(\delta\boldsymbol{\zeta}_1)$. Using the Baker-Campbell-Hausdorff (BCH) formula for small generators $X$ and $Y$, $\exp(Y)\exp(X) \approx \exp(X + Y + \frac{1}{2}[Y,X])$. Here, the generators are $X = -\frac{1}{2}(\delta\boldsymbol{\zeta}_1 \cdot \boldsymbol{\sigma})$ and $Y = -\frac{1}{2}(\delta\boldsymbol{\zeta}_2 \cdot \boldsymbol{\sigma})$. The commutator is:
$$
[Y,X] = \frac{1}{4} [-\delta\boldsymbol{\zeta}_2 \cdot \boldsymbol{\sigma}, -\delta\boldsymbol{\zeta}_1 \cdot \boldsymbol{\sigma}] = \frac{1}{4} (\delta\zeta_{2,i})(\delta\zeta_{1,j}) [\sigma_i, \sigma_j]
$$
Using the Pauli matrix commutation relation $[\sigma_i, \sigma_j] = 2i\epsilon_{ijk}\sigma_k$, we find:
$$
[Y,X] = \frac{1}{4} (\delta\zeta_{2,i})(\delta\zeta_{1,j}) (2i\epsilon_{ijk}\sigma_k) = \frac{i}{2} (\delta\boldsymbol{\zeta}_2 \times \delta\boldsymbol{\zeta}_1) \cdot \boldsymbol{\sigma}
$$
The generator of the composite transformation is therefore approximately:
$$
G_{comp} \approx -\frac{1}{2}(\delta\boldsymbol{\zeta}_1 + \delta\boldsymbol{\zeta}_2) \cdot \boldsymbol{\sigma} + \frac{1}{2}[Y,X] = -\frac{1}{2}(\delta\boldsymbol{\zeta}_1 + \delta\boldsymbol{\zeta}_2) \cdot \boldsymbol{\sigma} + \frac{i}{4} (\delta\boldsymbol{\zeta}_2 \times \delta\boldsymbol{\zeta}_1) \cdot \boldsymbol{\sigma}
$$
The first term is the generator of a new boost with [rapidity](@entry_id:265131) $\delta\boldsymbol{\zeta}_{tot} \approx \delta\boldsymbol{\zeta}_1 + \delta\boldsymbol{\zeta}_2$. The second term is in the form of a rotation generator. Comparing $\frac{i}{4} (\delta\boldsymbol{\zeta}_2 \times \delta\boldsymbol{\zeta}_1) \cdot \boldsymbol{\sigma}$ to the rotation generator in the form $- \frac{i}{2} (\delta\boldsymbol{\theta}_W \cdot \boldsymbol{\sigma})$, we can identify the infinitesimal Wigner rotation vector as $\delta\boldsymbol{\theta}_W = \frac{1}{2}(\delta\boldsymbol{\zeta}_1 \times \delta\boldsymbol{\zeta}_2)$ [@problem_id:1028161]. This result elegantly shows that the non-commutativity of boost generators gives rise to rotations.

### The Dirac Equation and its Covariance

While Weyl spinors provide the most fundamental representations of the Lorentz group, P.A.M. Dirac sought a [relativistic wave equation](@entry_id:158220) linear in space and time derivatives that could describe spin-1/2 particles like the electron. The Klein-Gordon equation, $(\partial^\mu\partial_\mu + m^2)\phi=0$, is second-order and posed difficulties for a probabilistic interpretation. Dirac's insight was to effectively take the "square root" of the Klein-Gordon operator. He proposed an equation of the form:
$$
(i\gamma^\mu \partial_\mu - m)\psi = 0
$$
where $\psi$ is a multi-component [spinor](@entry_id:154461) field (a **Dirac spinor**), and the $\gamma^\mu$ are four matrices whose properties are to be determined. For this "Dirac operator" to square to the Klein-Gordon operator, we require:
$$
(i\gamma^\nu \partial_\nu + m)(i\gamma^\mu \partial_\mu - m)\psi = 0
$$
Expanding this operator product reveals a profound algebraic identity [@problem_id:1028178]. The cross-terms involving $m$ cancel, and the leading term becomes $(i\gamma^\nu \partial_\nu)(i\gamma^\mu \partial_\mu) = -\gamma^\nu\gamma^\mu \partial_\nu\partial_\mu$. We can symmetrize the indices of the [partial derivatives](@entry_id:146280), yielding $-\frac{1}{2}(\gamma^\nu\gamma^\mu + \gamma^\mu\gamma^\nu)\partial_\nu\partial_\mu$. For this to reduce to the Klein-Gordon operator $-\partial^\mu\partial_\mu = -\eta^{\mu\nu}\partial_\mu\partial_\nu$, the gamma matrices must satisfy the defining relation of the **Clifford algebra**:
$$
\{\gamma^\mu, \gamma^\nu\} \equiv \gamma^\mu\gamma^\nu + \gamma^\nu\gamma^\mu = 2\eta^{\mu\nu}I
$$
where $I$ is the identity matrix in the spinor space. With this condition, the operator product becomes $(i\gamma^\nu\partial_\nu + m)(i\gamma^\mu\partial_\mu - m) = -(\eta^{\mu\nu}\partial_\mu\partial_\nu + m^2) = -(\partial^\alpha\partial_\alpha + m^2)I$. Thus, any solution to the Dirac equation is automatically a solution to the Klein-Gordon equation. The smallest dimension in which four matrices satisfying the Clifford algebra can be realized is $4 \times 4$. Hence, Dirac spinors are four-component objects.

For the Dirac equation to be a valid relativistic law, it must be **covariant**; that is, it must retain its form in all inertial frames. If a Lorentz transformation is given by $x'=\Lambda x$, the [spinor](@entry_id:154461) field must transform as $\psi'(x') = S(\Lambda)\psi(x)$, where $S(\Lambda)$ is a $4 \times 4$ matrix representing the Lorentz transformation in the spinor space. Substituting this into the Dirac equation in the primed frame, $(i\gamma^\mu \partial'_\mu - m)\psi'(x')=0$, and demanding it be equivalent to the original equation, leads to the requirement:
$$
S(\Lambda)^{-1} \gamma^\mu S(\Lambda) = \Lambda^\mu_{\ \nu} \gamma^\nu
$$
This is the fundamental covariance condition. For an infinitesimal transformation $\Lambda^\mu_{\ \nu} = \delta^\mu_\nu + \omega^\mu_{\ \nu}$, the [spinor transformation](@entry_id:161968) matrix is $S(\Lambda) \approx I - \frac{i}{2}\omega_{\mu\nu}S^{\mu\nu}$, which defines the generators of the Lorentz group in the Dirac representation, $S^{\mu\nu}$. It can be shown that these generators are constructed from the gamma matrices themselves:
$$
S^{\mu\nu} = \frac{i}{4}[\gamma^\mu, \gamma^\nu]
$$
The covariance condition is satisfied if these generators have the correct commutation relation with the [gamma matrices](@entry_id:147400): $[S^{\mu\nu}, \gamma^\rho] = i(\eta^{\rho\mu}\gamma^\nu - \eta^{\rho\nu}\gamma^\mu)$. This identity can be proven using only the Clifford algebra, and it underpins the entire relativistic structure of the theory [@problem_id:1028176].

### Structure of the Spinor Representation

The specific form of the gamma matrices is not unique; any set related by a similarity transformation will satisfy the Clifford algebra. Different choices, or **representations**, are useful for different purposes. A particularly insightful choice is the **chiral (or Weyl) representation**:
$$
\gamma^0 = \begin{pmatrix} 0 & I_2 \\ I_2 & 0 \end{pmatrix}, \quad \gamma^i = \begin{pmatrix} 0 & \sigma^i \\ -\sigma^i & 0 \end{pmatrix}
$$
In this basis, the Dirac [spinor](@entry_id:154461) naturally decomposes into two two-component Weyl spinors, $\psi_L$ and $\psi_R$:
$$
\psi = \begin{pmatrix} \psi_L \\ \psi_R \end{pmatrix}
$$
The Lorentz generators $S^{\mu\nu}$ also take on a revealing structure in this basis. Let's compute the generator for rotations in the $xy$-plane, $S^{12}$ [@problem_id:1028216].
$$
S^{12} = \frac{i}{4}[\gamma^1, \gamma^2] = \frac{i}{4} \left[ \begin{pmatrix} 0 & \sigma^1 \\ -\sigma^1 & 0 \end{pmatrix}, \begin{pmatrix} 0 & \sigma^2 \\ -\sigma^2 & 0 \end{pmatrix} \right] = \frac{i}{4} \begin{pmatrix} -[\sigma^1, \sigma^2] & 0 \\ 0 & -[\sigma^1, \sigma^2] \end{pmatrix}
$$
Using the Pauli algebra $[\sigma^1, \sigma^2] = 2i\sigma^3$, we find:
$$
S^{12} = \frac{i}{4} \begin{pmatrix} -2i\sigma^3 & 0 \\ 0 & -2i\sigma^3 \end{pmatrix} = \frac{1}{2} \begin{pmatrix} \sigma^3 & 0 \\ 0 & \sigma^3 \end{pmatrix}
$$
This block-[diagonal form](@entry_id:264850) is general for all rotation generators $S^{ij}$. It shows that under rotations, the upper two components ($\psi_L$) and the lower two components ($\psi_R$) transform among themselves, each according to the standard $SU(2)$ representation of rotations.

In contrast, the boost generators, such as $S^{01} = \frac{i}{4}[\gamma^0, \gamma^1]$, are block-off-diagonal:
$$
S^{01} = \frac{i}{4} \left[ \begin{pmatrix} 0 & I_2 \\ I_2 & 0 \end{pmatrix}, \begin{pmatrix} 0 & \sigma^1 \\ -\sigma^1 & 0 \end{pmatrix} \right] = \frac{i}{4} \begin{pmatrix} -2\sigma^1 & 0 \\ 0 & 2\sigma^1 \end{pmatrix} = \frac{i}{2} \begin{pmatrix} -\sigma^1 & 0 \\ 0 & \sigma^1 \end{pmatrix}
$$
This structure means that Lorentz boosts mix the left- and right-handed components. The Dirac equation itself, written in the chiral basis, makes this coupling explicit. For a momentum-space spinor $u(p)$, the equation $(\gamma^\mu p_\mu - m)u(p)=0$ becomes a set of coupled equations for the Weyl components $u_L$ and $u_R$:
$$
(p^0 - \vec{p}\cdot\vec{\sigma})u_R = m u_L \\
(p^0 + \vec{p}\cdot\vec{\sigma})u_L = m u_R
$$
For [massless particles](@entry_id:263424) ($m=0$), these equations decouple. The fields $u_L$ and $u_R$ become independent solutions describing left- and right-handed [massless particles](@entry_id:263424), respectively. The mass term is what couples the two chiralities.

### Physical States and Invariant Bilinears

We can construct explicit solutions to the Dirac equation for a particle of mass $m$ and a given four-momentum $p^\mu$. In the more traditional **Dirac-Pauli representation**, where $\gamma^0 = \text{diag}(I_2, -I_2)$, a positive-energy spinor can be written as $u(p) = \begin{pmatrix} u_A \\ u_B \end{pmatrix}$. The Dirac equation $(\gamma^\mu p_\mu - m)u=0$ leads to the relation $u_B = \frac{\vec{\sigma}\cdot\vec{p}}{E+m}u_A$, where $E = p^0$. For a particle at rest, $\vec{p}=0$ and $u_B=0$. The two basis solutions can be chosen as spin-up and spin-down along the $z$-axis, with $u_A$ being $\chi_+ = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$ or $\chi_- = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$. For a particle with arbitrary momentum, these rest-frame spinors are then boosted. For instance, given a momentum $\vec{p}=(p\cos\phi, p\sin\phi, 0)$, one can construct the corresponding spinors and analyze their properties [@problem_id:1028244].

The transformation of these explicit solutions under Lorentz boosts vividly illustrates the underlying principles. Consider a spin-down particle initially moving along the $z$-axis, described by a [spinor](@entry_id:154461) $u_-(p)$. If we apply a Lorentz boost along the $x$-axis, the spinor transforms to $u'(p') = S(\Lambda_x)u_-(p)$. In the chiral basis, the boost operator $S(\Lambda_x)$ acts differently on the upper ($\psi_L$) and lower ($\psi_R$) components. This mixing of components under a boost is a key feature of massive Dirac [spinors](@entry_id:158054) and reflects the fact that helicity (the projection of spin onto momentum) is not a Lorentz invariant for massive particles [@problem_id:1028213].

From spinor fields, one can construct physical observables. These must be Lorentz scalars, vectors, or tensors. To do this, we introduce the **Dirac adjoint** of a [spinor](@entry_id:154461), defined as $\bar{\psi} = \psi^\dagger \gamma^0$. The inclusion of $\gamma^0$ is crucial. While $\psi^\dagger\psi$ is not Lorentz invariant, the **[scalar density](@entry_id:161438)** $\bar{\psi}\psi$ is. We can verify this property with a direct calculation. The adjoint spinor transforms as $\bar{\psi}' = \bar{\psi}S(\Lambda)^{-1}$. Therefore, the bilinear transforms as:
$$
\bar{\psi}'\psi' = (\bar{\psi}S(\Lambda)^{-1}) (S(\Lambda)\psi) = \bar{\psi}\psi
$$
The cancellation is only possible if $S(\Lambda)^{-1} = \gamma^0 S(\Lambda)^\dagger \gamma^0$, which is a defining property of the [spinor representation](@entry_id:149925) matrices $S(\Lambda)$.

Let's verify this invariance for a concrete example [@problem_id:1028125]. Consider a spin-up particle at rest, $\Psi = (1, 0, 0, 0)^T$ in the Dirac-Pauli basis. Its [scalar density](@entry_id:161438) is $\bar{\Psi}\Psi = \Psi^\dagger \gamma^0 \Psi = 1$. Now, let's apply a boost with rapidity $\eta$ in the direction $\mathbf{n}=(\cos\phi, \sin\phi, 0)$. The transformation matrix is $S(\Lambda) = \cosh(\eta/2)I + (\mathbf{n}\cdot\boldsymbol{\alpha})\sinh(\eta/2)$, where $\alpha^i = \gamma^0\gamma^i$. Applying this to $\Psi$ yields the transformed spinor:
$$
\Psi' = \begin{pmatrix}\cosh(\eta/2) \\ 0 \\ 0 \\ e^{i\phi}\sinh(\eta/2)\end{pmatrix}
$$
Now we compute the new [scalar density](@entry_id:161438), $\bar{\Psi'}\Psi' = \Psi'^\dagger\gamma^0\Psi'$:
$$
\bar{\Psi'}\Psi' = \begin{pmatrix}\cosh(\eta/2) & 0 & 0 & e^{-i\phi}\sinh(\eta/2)\end{pmatrix} \begin{pmatrix} I_2 & 0 \\ 0 & -I_2 \end{pmatrix} \begin{pmatrix}\cosh(\eta/2) \\ 0 \\ 0 \\ e^{i\phi}\sinh(\eta/2)\end{pmatrix}
$$
$$
\bar{\Psi'}\Psi' = \begin{pmatrix}\cosh(\eta/2) & 0 & 0 & -e^{-i\phi}\sinh(\eta/2)\end{pmatrix} \begin{pmatrix}\cosh(\eta/2) \\ 0 \\ 0 \\ e^{i\phi}\sinh(\eta/2)\end{pmatrix}
$$
$$
\bar{\Psi'}\Psi' = \cosh^2(\eta/2) - \sinh^2(\eta/2) = 1
$$
The [scalar density](@entry_id:161438) remains unchanged, beautifully illustrating the Lorentz invariance of this bilinear. This invariance, along with the covariance of other bilinears like the vector current $\bar{\psi}\gamma^\mu\psi$, forms the bedrock upon which relativistic quantum field theories, such as Quantum Electrodynamics, are built.