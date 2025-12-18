## Introduction
In computational science and engineering, the simulation of physical phenomena often leads to mathematical models of immense scale and complexity. For linear time-invariant (LTI) systems, such as those arising from the [discretization](@entry_id:145012) of Maxwell's equations or in large-scale [circuit analysis](@entry_id:261116), direct simulation can be computationally prohibitive, creating a significant bottleneck in design and analysis workflows. Krylov subspace [model reduction](@entry_id:171175) offers a powerful and elegant solution to this challenge, providing a systematic framework for generating low-order approximations that accurately capture the input-output behavior of the original large-scale system. This article provides a comprehensive journey into this essential technique. The first chapter, "Principles and Mechanisms," lays the theoretical groundwork, exploring how [moment matching](@entry_id:144382) and projection are used to construct reduced models and how physical properties like stability and passivity are preserved. Following this, the "Applications and Interdisciplinary Connections" chapter demonstrates the practical utility of these methods in fields ranging from computational electromagnetics to [real-time control](@entry_id:754131). Finally, the "Hands-On Practices" section provides a guided pathway to translate theory into practice, with exercises focused on [error estimation](@entry_id:141578) and adaptive model construction.

## Principles and Mechanisms

This chapter elucidates the fundamental principles and core mechanisms underpinning Krylov subspace model reduction. We begin by establishing the theoretical foundation of [moment matching](@entry_id:144382) via projection, which forms the basis of all Krylov-based methods. We then explore the practical frameworks of Galerkin and Petrov-Galerkin projections, paying special attention to the crucial challenge of preserving the physical properties of the original system, such as stability and passivity. Finally, we discuss practical implementation strategies and advanced topics, including the trade-offs between single-point and multipoint methods, the algorithmic choice between Lanczos and Arnoldi processes, and the specialized techniques required for handling descriptor systems and [differential-algebraic equations](@entry_id:748394).

### The Foundation: Moment Matching and Projection

The central objective of [model order reduction](@entry_id:167302) for a linear time-invariant (LTI) system is to approximate its input-output behavior, encapsulated by the transfer function, with a model of significantly lower complexity. For a system described by the [state-space equations](@entry_id:266994) $E \dot{x}(t) = A x(t) + B u(t)$ with output $y(t) = C x(t) + D u(t)$, the transfer function in the frequency domain is given by:

$$H(s) = C (sE - A)^{-1} B + D$$

where $s$ is the complex frequency. The core idea behind Krylov subspace methods is to construct a [reduced-order model](@entry_id:634428), $\hat{H}(s)$, whose behavior matches that of the original model, $H(s)$, in the vicinity of a chosen frequency or expansion point, $s_0$.

This matching is formalized through the concept of **moments**. The moments of a transfer function at an expansion point $s_0$ are the coefficients of its Taylor series expansion around that point. If two transfer functions, $H(s)$ and $\hat{H}(s)$, have the same first $q$ moments at $s_0$, their Taylor series expansions will be identical up to the term of order $(s-s_0)^{q-1}$. This implies that the functions and their first $q-1$ derivatives match at $s_0$, ensuring excellent local accuracy .

To understand how projection achieves [moment matching](@entry_id:144382), we can analyze the resolvent term $(sE - A)^{-1}$ by expanding it as a series around $s_0$. Note that $(sE - A)^{-1} = -(A - sE)^{-1}$. To maintain a notationally clean expansion without an alternating sign in the [power series](@entry_id:146836), we expand $(A - sE)^{-1}$. Assuming the [matrix pencil](@entry_id:751760) $(A - s_0 E)$ is invertible, we can write:

$$A - s E = A - s_0 E - (s - s_0) E = (A - s_0 E) [I - (s-s_0)(A - s_0 E)^{-1}E]$$

Using the Neumann [series expansion](@entry_id:142878) for the inverse, we get:

$$(A - s E)^{-1} = \left( \sum_{k=0}^{\infty} (s-s_0)^k [(A-s_0E)^{-1}E]^k \right) (A-s_0E)^{-1}$$

Substituting this into the transfer function (omitting the direct feed-through term $D$ for clarity), we obtain the series:

$$H(s) \approx -C \left( \sum_{k=0}^{\infty} (s-s_0)^k [(A-s_0E)^{-1}E]^k (A-s_0E)^{-1} \right) B$$

The $k$-th moment of the system is the matrix term $m_k = -C [(A-s_0E)^{-1}E]^k (A-s_0E)^{-1} B$. To construct a reduced model that matches the first $q$ moments, we must project the system onto a subspace that contains the vector blocks that generate these moments. These are precisely the vectors $\{ r, M r, M^2 r, \dots, M^{q-1} r \}$, where the generating matrix is $M = (A-s_0E)^{-1}E$ and the starting block vector is $r = (A-s_0E)^{-1}B$.

This leads us to the definition of a **Krylov subspace**. For a square matrix $M$ and a vector (or block of vectors) $r$, the $q$-th order polynomial Krylov subspace is defined as:

$$\mathcal{K}_q(M, r) = \mathrm{span}\{r, M r, M^2 r, \dots, M^{q-1} r\}$$

The subspace generated by $M = (A-s_0E)^{-1}E$ and $r = (A-s_0E)^{-1}B$ is known as a **Rational Krylov Subspace (RKS)**. The term "rational" signifies that the generating matrix $M$ is a rational function of the system matrices $A$ and $E$. Projecting the original system onto this subspace yields a reduced model that, by construction, matches the first $q$ moments of $H(s)$ at $s_0$ . This approach is particularly powerful for descriptor systems arising in [computational electromagnetics](@entry_id:269494), where the matrix $E$ can be singular. Methods that require computing $E^{-1}$ are inapplicable in such cases. The RKS formulation elegantly circumvents this issue by only requiring the invertibility of $(A - s_0 E)$, which is generally true for any expansion point $s_0$ that is not a pole of the system.

From a more formal perspective, this moment-matching procedure is intrinsically linked to **Padé approximation**. A Padé approximant is a [rational function](@entry_id:270841) that provides a [best approximation](@entry_id:268380) to a given function by matching the initial terms of its Taylor series. It can be shown that projecting onto a Krylov subspace is equivalent to constructing an implicit Padé-type approximant of the transfer function. For instance, matching moments at $s=\infty$ corresponds to matching the leading terms of the Laurent series of the resolvent, $(zI - A)^{-1} = \sum_{k=0}^{\infty} z^{-k-1} A^k$, which is the basis for constructing Padé approximants for [matrix functions](@entry_id:180392) .

### Projection Frameworks: Galerkin and Petrov-Galerkin

The mechanism of projection is realized through a change of coordinates. We approximate the high-dimensional [state vector](@entry_id:154607) $x \in \mathbb{C}^n$ with a low-dimensional representation, $x \approx V \hat{x}$, where $\hat{x} \in \mathbb{C}^r$ with $r \ll n$, and the columns of the matrix $V \in \mathbb{C}^{n \times r}$ form a basis for the approximation subspace. The choice of this subspace, known as the **trial subspace**, is critical and is typically a rational Krylov subspace as described above.

To derive the dynamics for the reduced state $\hat{x}$, we enforce a condition on the residual of the original state equation, $E V \dot{\hat{x}} - A V \hat{x} - B u$. The **Petrov-Galerkin** framework imposes that this residual be orthogonal to a **test subspace**, spanned by the columns of a matrix $W \in \mathbb{C}^{n \times r}$. This [orthogonality condition](@entry_id:168905), $W^* (E V \dot{\hat{x}} - A V \hat{x} - B u) = 0$, yields the [reduced-order model](@entry_id:634428):

$$\hat{E} \dot{\hat{x}}(t) = \hat{A} \hat{x}(t) + \hat{B} u(t), \quad \hat{y}(t) = \hat{C} \hat{x}(t) + D u(t)$$

where the reduced system matrices are given by:
$$\hat{E} = W^{*} E V, \quad \hat{A} = W^{*} A V, \quad \hat{B} = W^{*} B, \quad \text{and} \quad \hat{C} = C V.$$

In this framework, the choice of both $V$ and $W$ is crucial. To match moments from the input side, the trial subspace (columns of $V$) is typically chosen as the right Krylov subspace built from the input matrix $B$. To match moments from the output side, the test subspace (columns of $W$) must be chosen as the left Krylov subspace, which is constructed from the dual system involving $A^*$ and the output matrix $C$ .

A special and important case of this framework is the **Galerkin projection**, where the test subspace is chosen to be identical to the trial subspace, i.e., $W=V$. This simplifies the reduced matrices to $\hat{E} = V^{*} E V$, $\hat{A} = V^{*} A V$, and so on. A Galerkin approach is sufficient and often preferred when the system possesses inherent symmetries. For example, in systems with structural properties such as being $E$-self-adjoint ($A^*E=EA$) or $E$-skew-adjoint ($A^*E=-EA$), the left and right Krylov subspaces are intrinsically linked. In such cases, constructing a single basis $V$ (e.g., one that is $E$-orthonormal, $V^*EV=I$) and using a Galerkin projection is sufficient to match moments and, critically, preserve the underlying system structure. For general, non-symmetric systems lacking such structure, a full Petrov-Galerkin approach ($W \neq V$), often enforcing [bi-orthogonality](@entry_id:175698) ($W^*EV = I$), is necessary to ensure two-sided [moment matching](@entry_id:144382) and produce a high-fidelity reduced model .

### Preservation of Physical Properties

A fundamental requirement in modeling physical systems is that the [reduced-order model](@entry_id:634428) must inherit the essential physical properties of the full-order system. A model that violates physical laws, for instance by generating energy spontaneously, is not only incorrect but can also lead to catastrophic failures in simulation and design. Krylov subspace methods, in their basic form, do not automatically guarantee the preservation of such properties.

#### Stability

Asymptotic stability, a property indicating that a system's response will decay to zero without external excitation, is not inherently preserved by a general Petrov-Galerkin projection. A poor choice of the test basis $W$ relative to the trial basis $V$ can render a stable system unstable.

Consider, for example, a stable dissipative system $E \dot{x} = A x$ with $E$ [symmetric positive definite](@entry_id:139466) (SPD) and the symmetric part of $A$ being [negative definite](@entry_id:154306). A Petrov-Galerkin projection yields the reduced system $\hat{E} \dot{\hat{x}} = \hat{A} \hat{x}$. If one chooses $V = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$ and $W = \begin{pmatrix} 1 \\ -2/5 \end{pmatrix}$ for the stable system with $E=\begin{pmatrix} 1  0 \\ 0  2 \end{pmatrix}$ and $A=\begin{pmatrix} -1  0 \\ 0  -3 \end{pmatrix}$, the resulting scalar reduced system has an eigenvalue of $+1$, indicating instability .

To guarantee stability preservation, [sufficient conditions](@entry_id:269617) can be derived from a Lyapunov stability argument. The reduced system is guaranteed to be stable if the [reduced mass](@entry_id:152420) matrix $\hat{E} = W^{*} E V$ is SPD and the symmetric part of the reduced system matrix, $\hat{A}_S = \frac{1}{2}(\hat{A} + \hat{A}^{*})$, is [negative definite](@entry_id:154306). A straightforward way to satisfy these conditions is to use a Galerkin projection ($W=V$) on a system where $A$'s symmetric part is [negative definite](@entry_id:154306). The congruent transformation $V^* A V$ preserves the definiteness property, thus ensuring the reduced model is also stable .

#### Passivity

Passivity is a property of systems that do not generate energy. In the frequency domain, for LTI systems, passivity is equivalent to the transfer function being **positive-real (PR)**. A [matrix function](@entry_id:751754) $H(s)$ is PR if it is analytic in the open right-half plane $\text{Re}(s)0$ and its Hermitian part is positive semidefinite, i.e., $H(s) + H(s)^* \succeq 0$, for all $\text{Re}(s)0$ .

Many systems derived from physical principles, such as RLC circuits modeled via Modified Nodal Analysis (MNA), possess a specific mathematical structure that guarantees passivity. For instance, their system matrices may satisfy $E=E^T \succeq 0$ and $A=A^T \preceq 0$. Standard [projection methods](@entry_id:147401) do not necessarily preserve this structure. The **Passive Reduced-order Interconnect Macromodeling Algorithm (PRIMA)** was specifically designed to address this. PRIMA employs a Galerkin projection ($W=V$), which results in a **congruent transformation** of the system matrices: $\hat{E} = V^T E V$ and $\hat{A} = V^T A V$. A congruent transformation is known to preserve matrix symmetry and definiteness. Therefore, if the original system has the passivity-enforcing structure, the reduced model generated by PRIMA is guaranteed to have the same structure and is thus provably passive .

#### Energy Conservation

Other physical systems, such as the [electromagnetic fields](@entry_id:272866) inside a lossless [resonant cavity](@entry_id:274488), are energy-conserving rather than dissipative. The [finite element discretization](@entry_id:193156) of such systems often leads to a descriptor system $E \dot{x} = A x$ where $E$ is SPD and the system matrix $A$ is skew-symmetric ($A^T = -A$). The eigenvalues of such a system are purely imaginary, corresponding to undamped oscillations (resonances). To preserve this energy-conserving structure, a Galerkin projection using an $E$-[orthonormal basis](@entry_id:147779) ($V^T E V = I$) is the appropriate choice. The reduced [system matrix](@entry_id:172230) $\hat{A} = V^T A V$ will also be skew-symmetric, ensuring the reduced model's eigenvalues also lie on the imaginary axis, thereby correctly capturing the resonant, non-dissipative nature of the original system .

### Practical Implementation and Advanced Topics

Beyond the core principles, several practical considerations and advanced concepts are crucial for the successful application of Krylov subspace [model reduction](@entry_id:171175).

#### Single-Point vs. Multipoint Methods

The simplest Krylov methods perform a single-point expansion, matching a high number of moments at a single frequency $s_0$. This approach is analogous to a Taylor [series approximation](@entry_id:160794). Its accuracy is excellent near $s_0$ but deteriorates as the frequency of interest moves away from the expansion point. The theoretical limit of this local approximation is the **radius of convergence**, which is the distance from $s_0$ to the nearest pole of the system's transfer function. For applications requiring accuracy over a broad frequency band—a common scenario in electromagnetics—a single-point expansion is often inadequate, as the approximation may be poor or even divergent at the band edges .

The solution is to use **multipoint methods**. These methods construct a rational Krylov subspace that simultaneously matches a smaller number of moments at several expansion points (or shifts) $\{s_1, s_2, \dots, s_m\}$ distributed across the frequency band of interest. By "stitching" together multiple local approximations, a multipoint method can produce a [reduced-order model](@entry_id:634428) that is highly accurate over a wide bandwidth. For a system with several distinct resonances, placing shifts near each resonance is a far more efficient strategy for achieving broadband accuracy than attempting to capture all features with a very high-order expansion at a single central point . Furthermore, distributing a fixed number of moments across multiple shifts generally leads to better [numerical conditioning](@entry_id:136760) compared to computing a single high-order Krylov subspace .

#### Algorithmic Aspects: Lanczos vs. Arnoldi

The construction of an orthonormal basis for a Krylov subspace is an iterative process. Two main algorithms are used: the **Arnoldi algorithm** and the **Lanczos algorithm**. The Arnoldi algorithm is the most general; it builds the basis via a long recurrence, meaning that each new basis vector must be explicitly orthogonalized against all previously generated vectors. The Lanczos algorithm is significantly more efficient as it relies on a short, [three-term recurrence](@entry_id:755957), where the new vector only needs to be orthogonalized against the previous two.

The choice between these algorithms depends on a fundamental property of the generating matrix $M$ with respect to the inner product used for [orthogonalization](@entry_id:149208). A short recurrence exists if and only if the matrix $M$ is **self-adjoint** (Hermitian) in that inner product. For the rational Krylov operator $T_s = (A-sE)^{-1}E$ used in model reduction of systems with symmetric $A$ and SPD $E$, the natural choice of inner product is the $E$-inner product, $(u,v)_E = u^*Ev$. With respect to this inner product, the operator $T_s$ is self-adjoint if and only if the expansion point $s$ is a real number. Consequently, for real shifts, the more efficient Lanczos algorithm can be used. For complex shifts, which are often necessary to target specific frequency-domain features, the operator is not self-adjoint, and the more general Arnoldi algorithm with its long recurrence must be employed .

#### Handling Descriptor Systems and DAEs

As noted earlier, many physical models, particularly those from [finite element analysis](@entry_id:138109), result in descriptor systems where the matrix $E$ is singular. These systems are more formally known as **Differential-Algebraic Equations (DAEs)**, as they contain a mixture of differential and algebraic constraints.

The degree of difficulty in handling a DAE is characterized by its **tractability index** (or differentiation index), $\nu$. This index represents the minimum number of times the algebraic constraints must be differentiated to fully decouple the system and express the time derivatives of all state variables as an explicit function of the state variables and inputs. In the language of the Weierstrass [canonical form](@entry_id:140237) of the [matrix pencil](@entry_id:751760) $(E,A)$, the index $\nu$ is precisely the index of [nilpotency](@entry_id:147926) of the nilpotent block corresponding to the algebraic part of the system .

For a DAE with index $\nu > 1$, direct simulation or reduction can be numerically challenging. A robust strategy is to first **deflate** the system. This involves finding projectors that explicitly separate the [state vector](@entry_id:154607) $x(t)$ into its dynamic component $x_d(t)$, which evolves according to an [ordinary differential equation](@entry_id:168621) (ODE), and its algebraic component $x_a(t)$, which is determined by the inputs and their derivatives. Once this separation is achieved, standard model reduction techniques, such as a rational Krylov method, can be applied to the well-behaved dynamic ODE subsystem, while the algebraic constraints are handled separately . This deflation process provides a rigorous pathway for applying powerful MOR techniques to the complex DAEs that frequently arise in computational science and engineering.