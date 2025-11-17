## Introduction
The [state-space representation](@entry_id:147149) is a cornerstone of modern control theory, providing a detailed internal description of a system's dynamics that contrasts with the external, input-output behavior captured by its transfer function. A critical question arises from this distinction: does a system's external behavior uniquely determine its internal model? The answer is a definitive no, a fact that has profound theoretical and practical implications. This fundamental non-uniqueness is not a flaw but a core feature of the state-space framework.

This article delves into this essential concept. The first chapter, "Principles and Mechanisms," lays the theoretical groundwork, explaining how similarity transformations generate infinite equivalent models and introducing the crucial concepts of minimality, [controllability](@entry_id:148402), and observability. The second chapter, "Applications and Interdisciplinary Connections," explores the practical consequences of this principle in control design, system identification, and diverse fields such as economics, signal processing, and biology. Finally, "Hands-On Practices" provides opportunities to apply these concepts through guided exercises, solidifying the connection between theory and practice and demonstrating how the freedom in [state-space](@entry_id:177074) coordinates is both a challenge and an opportunity.

## Principles and Mechanisms

### The State-Space Realization and its Transfer Function

A fundamental concept in modern control theory is the distinction between a system's internal dynamics and its external, input-output behavior. A [state-space model](@entry_id:273798) provides an internal description of a finite-dimensional linear time-invariant (LTI) system. For a continuous-time system, this is given by the equations:

$$
\begin{align}
\dot{x}(t) = A x(t) + B u(t) \\
y(t) = C x(t) + D u(t)
\end{align}
$$

and for a discrete-time system by:

$$
\begin{align}
x_{k+1} = A x_{k} + B u_{k} \\
y_{k} = C x_{k} + D u_{k}
\end{align}
$$

In these models, $x \in \mathbb{F}^n$ is the **state vector**, $u \in \mathbb{F}^m$ is the input vector, and $y \in \mathbb{F}^p$ is the output vector, where the field $\mathbb{F}$ is typically the real numbers $\mathbb{R}$ or complex numbers $\mathbb{C}$. The matrices $(A, B, C, D)$ are of compatible dimensions and are known as the **[state-space](@entry_id:177074) quadruple**.

The external behavior, on the other hand, is captured by the **[transfer function matrix](@entry_id:271746)**, which relates the transform of the output to the transform of the input, assuming zero [initial conditions](@entry_id:152863) ($x(0) = \mathbf{0}$ or $x_0 = \mathbf{0}$). Applying the Laplace transform to the continuous-time equations yields:

$$
\begin{align}
sX(s) = AX(s) + BU(s) \\
Y(s) = CX(s) + DU(s)
\end{align}
$$

Solving for $X(s)$ from the first equation gives $X(s) = (sI - A)^{-1}BU(s)$, which is valid for all complex numbers $s$ that are not eigenvalues of $A$, i.e., where $\det(sI - A) \neq 0$. Substituting this into the output equation, we find the relationship between the input and output transforms:

$$
Y(s) = \left[C(sI - A)^{-1}B + D\right] U(s)
$$

The matrix $G(s) = C(sI - A)^{-1}B + D$ is the [transfer function matrix](@entry_id:271746) of the system. An identical algebraic procedure using the $z$-transform for the discrete-time system yields its transfer function $G(z) = C(zI - A)^{-1}B + D$. The quadruple $(A, B, C, D)$ is called a **[state-space realization](@entry_id:166670)** of the transfer function $G$. [@problem_id:2727820] [@problem_id:2727834]

For a proper transfer function, the limit as $|s| \to \infty$ is well-defined. The term $C(sI - A)^{-1}B$ is strictly proper, meaning it approaches the zero matrix as $|s| \to \infty$. Consequently, the **direct feedthrough matrix** $D$ is uniquely determined by the high-frequency gain of the system: $D = \lim_{|s| \to \infty} G(s)$. [@problem_id:2727861]

### The Fundamental Non-Uniqueness: Similarity Transformations

A crucial question arises: given an external description $G(s)$, is the internal description $(A,B,C,D)$ unique? The answer is a definitive no, and this non-uniqueness is at the heart of state-space theory.

The state vector $x(t)$ represents an internal variable, and the choice of basis for the state space $\mathbb{F}^n$ is arbitrary. Let us consider a change of basis defined by an [invertible matrix](@entry_id:142051) $T \in \mathrm{GL}_n(\mathbb{F})$, where $\mathrm{GL}_n(\mathbb{F})$ is the [general linear group](@entry_id:141275) of degree $n$. Let a new [state vector](@entry_id:154607) be $\tilde{x}(t) = T x(t)$. The original state can be recovered via $x(t) = T^{-1}\tilde{x}(t)$. Substituting this into the continuous-time [state equations](@entry_id:274378):

$$
\begin{align}
\frac{d}{dt}(T^{-1}\tilde{x}(t)) = A(T^{-1}\tilde{x}(t)) + B u(t) \\
y(t) = C(T^{-1}\tilde{x}(t)) + D u(t)
\end{align}
$$

This leads to a new [state-space model](@entry_id:273798) for the state $\tilde{x}$:

$$
\begin{align}
\dot{\tilde{x}}(t) = (TAT^{-1})\tilde{x}(t) + (TB)u(t) \\
y(t) = (CT^{-1})\tilde{x}(t) + Du(t)
\end{align}
$$

We have a new realization, $(\tilde{A}, \tilde{B}, \tilde{C}, \tilde{D})$, where $\tilde{A} = TAT^{-1}$, $\tilde{B} = TB$, $\tilde{C} = CT^{-1}$, and $\tilde{D}=D$. This transformation is known as a **similarity transformation**. Does this new realization produce the same external behavior? Let's compute its transfer function $\tilde{G}(s)$:

$$
\tilde{G}(s) = \tilde{C}(sI - \tilde{A})^{-1}\tilde{B} + \tilde{D} = (CT^{-1})(sI - TAT^{-1})^{-1}(TB) + D
$$

The key to this expression lies in the inverse term. We use the identity $(sI - TAT^{-1})^{-1} = T(sI - A)^{-1}T^{-1}$, which holds for any invertible $T$ and any $s$ not in the spectrum of $A$. [@problem_id:2727834] Substituting this back gives:

$$
\tilde{G}(s) = (CT^{-1})\left[T(sI - A)^{-1}T^{-1}\right](TB) + D = C(T^{-1}T)(sI - A)^{-1}(T^{-1}T)B + D = C(sI - A)^{-1}B + D = G(s)
$$

The transfer function is invariant under any similarity transformation. Since the group $\mathrm{GL}_n(\mathbb{F})$ contains infinitely many matrices, for any given realization, there exists an infinite family of other realizations that produce the exact same input-output behavior. [@problem_id:2727861] This demonstrates that from external measurements alone, one cannot uniquely determine the internal state coordinates. The set of all realizations related by similarity forms an [equivalence class](@entry_id:140585), or an **orbit**, under the [group action](@entry_id:143336) of $\mathrm{GL}_n(\mathbb{F})$. [@problem_id:2727823]

### External Invariants and Minimality

While the internal matrices $(A,B,C)$ are not unique, certain combinations of them that characterize external behavior must be invariant. One such set of quantities are the **Markov parameters**. For a discrete-time system, the output resulting from an impulse input $u_0=1, u_k=0$ for $k>0$ (and $x_0=0$) is the sequence $y_0=D$, $y_1=CB$, $y_2=CAB$, and in general, $y_k = CA^{k-1}B$ for $k \ge 1$. These quantities, $g_0 = D$ and $g_k = CA^{k-1}B$, are the Markov parameters. They are invariant under similarity transformations, as can be easily verified:

$$
\tilde{g}_k = \tilde{C}(\tilde{A})^{k-1}\tilde{B} = (CT^{-1})(TAT^{-1})^{k-1}(TB) = C(T^{-1}T)A^{k-1}(T^{-1}T)B = CA^{k-1}B = g_k
$$
This result confirms, from a time-domain perspective, that the input-output map is unchanged. [@problem_id:2727859]

This non-uniqueness motivates a search for the simplest possible realization. A realization is defined as **minimal** if its state dimension $n$ is the smallest possible among all realizations of a given $G(s)$. This intuitive notion of simplicity has a precise algebraic characterization. A realization $(A,B,C)$ is minimal if and only if it is both **controllable** and **observable**. [@problem_id:2727840] Controllability refers to the ability to steer the state to any value using the input, while [observability](@entry_id:152062) refers to the ability to determine the initial state from future output measurements. Both [controllability and observability](@entry_id:174003) are invariant under similarity transformations. [@problem_id:2727834]

The dimension of a [minimal realization](@entry_id:176932) is itself a unique property of the transfer function, known as the **McMillan degree** of $G(s)$. For a scalar rational transfer function, the McMillan degree is simply the degree of the denominator polynomial after all common factors with the numerator have been canceled. [@problem_id:2727840]

### The Uniqueness Theorem for Minimal Realizations

We have established that for a given $G(s)$, there are infinitely many [state-space](@entry_id:177074) realizations. However, if we restrict ourselves to minimal ones, the situation becomes much more structured. This is captured by the fundamental theorem of realization theory:

**Theorem:** Any two minimal state-space realizations of the same transfer function $G(s)$ are related by a unique [similarity transformation](@entry_id:152935).

This theorem implies that while a [minimal realization](@entry_id:176932) is not unique in an absolute sense, its non-uniqueness is completely characterized by the choice of [state-space](@entry_id:177074) basis. All minimal realizations of $G(s)$ belong to a single [equivalence class](@entry_id:140585) (orbit) and share the same dimension (the McMillan degree), the same set of eigenvalues for their $A$ matrices (the [system poles](@entry_id:275195)), and the same transfer function. [@problem_id:2727823] [@problem_id:2727840]

This is where **[canonical forms](@entry_id:153058)** (such as controllable, observable, or modal [canonical forms](@entry_id:153058)) find their purpose. A canonical form is a standardized structure for the matrices $(A,B,C)$. For any [minimal realization](@entry_id:176932), one can find a [similarity transformation](@entry_id:152935) $T$ that converts it to a desired [canonical form](@entry_id:140237). This process does not *resolve* the non-uniqueness; rather, it *exploits* the freedom of similarity transformations to select a single, convenient representative from the infinite class of equivalent realizations. Starting from a [canonical form](@entry_id:140237), any other [similarity transformation](@entry_id:152935) will generate an equally valid, but non-canonical, [minimal realization](@entry_id:176932) of the same $G(s)$. [@problem_id:2727827]

### The Structure of Non-Minimal Realizations: Hidden Modes

If a realization is not minimal, its dimension is greater than the McMillan degree of its transfer function. This implies the existence of states that are superfluous to the input-output dynamics. These are associated with **hidden modes**. A hidden mode is an eigenvalue of the [system matrix](@entry_id:172230) $A$ that does not appear as a pole of the transfer function $G(s)$. This occurs when there is a [pole-zero cancellation](@entry_id:261496) in the expression $G(s) = C(sI-A)^{-1}B+D$.

The **Kalman decomposition theorem** provides a rigorous framework for understanding this phenomenon. It states that through a suitable similarity transformation, any state space can be decomposed into a direct sum of four mutually orthogonal subspaces:
1.  $\mathcal{S}_{co}$: The controllable and observable subspace.
2.  $\mathcal{S}_{c\bar{o}}$: The controllable but [unobservable subspace](@entry_id:176289).
3.  $\mathcal{S}_{\bar{c}o}$: The uncontrollable but observable subspace.
4.  $\mathcal{S}_{\bar{c}\bar{o}}$: The uncontrollable and [unobservable subspace](@entry_id:176289).

In a basis aligned with this decomposition, the system matrices take on a special block-triangular structure. For instance, the transformed matrices $(\bar{A}, \bar{B}, \bar{C})$ have the form:
$$
\bar{A} = \begin{bmatrix}
A_{co}  & 0  & A_{13}  & 0 \\
A_{21}  & A_{c\bar{o}}  & A_{23}  & A_{24} \\
0  & 0  & A_{\bar{c}o}  & 0 \\
0  & 0  & A_{43}  & A_{\bar{c}\bar{o}}
\end{bmatrix}, \quad
\bar{B} = \begin{bmatrix}
B_{co} \\ B_{c\bar{o}} \\ 0 \\ 0
\end{bmatrix}, \quad
\bar{C} = \begin{bmatrix}
C_{co}  & 0  & C_{\bar{c}o}  & 0
\end{bmatrix}
$$
The zero blocks appear because states in uncontrollable subspaces cannot be affected by the input (hence zero rows in $\bar{B}$), and states in unobservable subspaces cannot affect the output (hence zero columns in $\bar{C}$). When computing the transfer function for this decomposed system, a remarkable simplification occurs:

$$
G(s) = \bar{C}(sI - \bar{A})^{-1}\bar{B} + D = C_{co} (sI - A_{co})^{-1} B_{co} + D
$$

This result proves that the input-output behavior of any LTI system is determined exclusively by its controllable and observable part. [@problem_id:2727862] The eigenvalues of $A_{c\bar{o}}$, $A_{\bar{c}o}$, and $A_{\bar{c}\bar{o}}$ are the hidden modes. They are part of the internal dynamics but are invisible from the perspective of the transfer function. For instance, one can construct a realization for $G(s) = \frac{1}{s+1}$ by starting with a minimal part ($A_{co}=[-1], B_{co}=[1], C_{co}=[1]$) and appending an unobservable part:

$$
A=\mathrm{diag}(-1,\lambda), \quad B=\begin{bmatrix}1\\1\end{bmatrix}, \quad C=\begin{bmatrix}1 & 0\end{bmatrix}, \quad D=0
$$

The mode associated with eigenvalue $\lambda$ is controllable but unobservable. A direct calculation confirms that the transfer function remains $G(s) = \frac{1}{s+1}$ for any choice of $\lambda$. This shows that unobservability alone is sufficient to hide a mode. Likewise, uncontrollability is also sufficient. [@problem_id:2727822]

### Failure of Uniqueness for Non-Minimal Realizations

The uniqueness theorem for minimal realizations does not extend to non-minimal ones. Two non-minimal realizations of the same transfer function are **not necessarily similar**. This is a profound point. While similarity transformations preserve the eigenvalues of the state matrix $A$, two non-minimal realizations of the same $G(s)$ can have different sets of eigenvalues.

Consider the following two realizations of $G(s) = \frac{1}{s+1}$:
- $\Sigma_{1}: A_{1} = \begin{bmatrix} -1  & 0 \\ 0  & 0 \end{bmatrix},\; B_{1} = \begin{bmatrix} 1 \\ 0 \end{bmatrix},\; C_{1} = \begin{bmatrix} 1  & 0 \end{bmatrix},\; D_{1} = 0.$
- $\Sigma_{2}: A_{2} = \begin{bmatrix} -1  & 0 \\ 0  & 2 \end{bmatrix},\; B_{2} = \begin{bmatrix} 1 \\ 0 \end{bmatrix},\; C_{2} = \begin{bmatrix} 1  & 0 \end{bmatrix},\; D_{2} = 0.$

Both realizations are non-minimal and a quick calculation confirms they both yield $G(s) = \frac{1}{s+1}$. However, the eigenvalues of $A_1$ are $\{-1, 0\}$, while the eigenvalues of $A_2$ are $\{-1, 2\}$. Since similarity transformations preserve eigenvalues, the matrices $A_1$ and $A_2$ cannot be similar. Therefore, the realizations $\Sigma_1$ and $\Sigma_2$ are not similar. [@problem_id:2727855] This illustrates that for non-minimal systems, the non-uniqueness is more severe: different realizations can represent fundamentally different internal dynamical structures, so long as the "extra" dynamics are hidden from the input and output. This has critical implications for system identification, where only the minimal, controllable, and observable part of a system can be identified from its external behavior.