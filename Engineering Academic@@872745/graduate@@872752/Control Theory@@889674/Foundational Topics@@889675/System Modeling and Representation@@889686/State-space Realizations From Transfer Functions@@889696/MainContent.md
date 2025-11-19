## Introduction
In the study of linear time-invariant (LTI) systems, two powerful perspectives dominate: the external, input-output description given by the transfer function, and the internal, dynamic description provided by [state-space equations](@entry_id:266994). While the transfer function captures how a system responds to external stimuli, the [state-space model](@entry_id:273798) offers a window into the internal mechanisms that produce this behavior. The ability to translate between these two representations is a cornerstone of modern control theory, enabling both high-level analysis and detailed implementation. This article addresses the fundamental problem of constructing an internal state-space model from a given external transfer function—a process known as [state-space realization](@entry_id:166670).

Across the following chapters, you will gain a comprehensive understanding of this critical topic. The first chapter, "Principles and Mechanisms," will lay the theoretical groundwork, exploring the derivation of [transfer functions](@entry_id:756102) from [state-space models](@entry_id:137993) and the more intricate inverse problem of realization. We will uncover why realizations are not unique and define the crucial concept of a [minimal realization](@entry_id:176932), linking it to the system's structural properties of [controllability and observability](@entry_id:174003). The second chapter, "Applications and Interdisciplinary Connections," will demonstrate the practical utility of realization theory in fields ranging from [system identification](@entry_id:201290) and [data-driven modeling](@entry_id:184110) to the construction of physically meaningful models in electrical and [chemical engineering](@entry_id:143883). Finally, the "Hands-On Practices" chapter will provide targeted exercises to solidify your ability to construct and analyze [state-space models](@entry_id:137993), including those with hidden dynamics.

## Principles and Mechanisms

In the preceding chapter, we introduced the dual perspectives of linear time-invariant (LTI) systems: the external, input-output description manifested by the transfer function, and the internal, state-variable description. This chapter delves into the fundamental principles and mechanisms that connect these two worlds. We will explore the process of moving from a [state-space model](@entry_id:273798) to a transfer function, and the more complex inverse problem: constructing a [state-space realization](@entry_id:166670) from a given transfer function. This journey will naturally lead us to critical concepts such as minimality, non-uniqueness, stability, and the structural properties of [controllability and observability](@entry_id:174003) that govern the internal dynamics of a system.

### From State-Space Equations to Transfer Functions

A finite-dimensional LTI system can be described by the standard [state-space equations](@entry_id:266994):
$$
\begin{align}
\dot{x}(t) = A x(t) + B u(t) \\
y(t) = C x(t) + D u(t)
\end{align}
$$
where $x(t) \in \mathbb{R}^{n}$ is the [state vector](@entry_id:154607), $u(t) \in \mathbb{R}^{m}$ is the input vector, and $y(t) \in \mathbb{R}^{p}$ is the output vector. The matrices $(A, B, C, D)$ are constant matrices of compatible dimensions that define the system's dynamics and input-output mapping.

To derive the transfer function, we apply the Laplace transform to these equations, assuming zero [initial conditions](@entry_id:152863), i.e., $x(0) = 0$. The derivative property of the Laplace transform, $\mathcal{L}\{\dot{x}(t)\} = sX(s) - x(0)$, simplifies to $sX(s)$. The transformed equations become:
$$
\begin{align}
sX(s) = AX(s) + BU(s) \\
Y(s) = CX(s) + DU(s)
\end{align}
$$
Our goal is to find a matrix $G(s)$ that directly relates the input transform $U(s)$ to the output transform $Y(s)$ via $Y(s) = G(s)U(s)$. We can achieve this by first solving the state equation for $X(s)$:
$$
sX(s) - AX(s) = BU(s) \implies (sI - A)X(s) = BU(s)
$$
Provided that the matrix $(sI - A)$ is invertible, which is true for all complex numbers $s$ that are not eigenvalues of $A$, we can write:
$$
X(s) = (sI - A)^{-1}BU(s)
$$
Substituting this expression for the state vector into the output equation yields:
$$
Y(s) = C\left((sI - A)^{-1}BU(s)\right) + DU(s) = \left(C(sI - A)^{-1}B + D\right)U(s)
$$
By comparing this with the definition $Y(s) = G(s)U(s)$, we identify the [transfer function matrix](@entry_id:271746) of the system as:
$$
G(s) = C(sI - A)^{-1}B + D
$$
This fundamental equation provides the bridge from an internal [state-space](@entry_id:177074) description $(A,B,C,D)$ to its external transfer function representation $G(s)$. Any quadruple of matrices $(A,B,C,D)$ that generates a given $G(s)$ through this formula is called a **[state-space realization](@entry_id:166670)** of $G(s)$ [@problem_id:2907652].

### Proper and Strictly Proper Systems

An immediate and crucial consequence of the realization formula concerns the behavior of $G(s)$ at very high frequencies, i.e., as $s \to \infty$. Let us examine the term $(sI-A)^{-1}$:
$$
(sI - A)^{-1} = \frac{1}{s}\left(I - \frac{1}{s}A\right)^{-1}
$$
For large $|s|$, the matrix $\frac{1}{s}A$ has a small norm, allowing the use of the Neumann series expansion $(I-X)^{-1} = I + X + X^2 + \dots$. This gives:
$$
(sI - A)^{-1} = \frac{1}{s}\left(I + \frac{1}{s}A + \frac{1}{s^2}A^2 + \dots\right) = \frac{1}{s}I + \frac{1}{s^2}A + \frac{1}{s^3}A^2 + \dots
$$
As $s \to \infty$, every term in this expansion approaches the zero matrix. Therefore, the dynamic part of the transfer function vanishes at infinite frequency:
$$
\lim_{s \to \infty} C(sI - A)^{-1}B = 0
$$
This reveals a profound property of any standard [state-space realization](@entry_id:166670):
$$
\lim_{s \to \infty} G(s) = \lim_{s \to \infty} \left(C(sI - A)^{-1}B + D\right) = 0 + D = D
$$
The matrix $D$, often called the **direct term** or **feedthrough matrix**, represents the instantaneous gain of the system from input to output at infinite frequency.

This result connects directly to the classification of [transfer functions](@entry_id:756102). A rational transfer function (or matrix of rational functions) is defined as **proper** if its limit as $s \to \infty$ is a finite constant matrix. It is **strictly proper** if this limit is the [zero matrix](@entry_id:155836) [@problem_id:2907652]. In terms of the polynomials in each scalar entry $g_{ij}(s) = N_{ij}(s)/P_{ij}(s)$, properness means $\deg(N_{ij}) \le \deg(P_{ij})$ for all entries, while strict properness implies $\deg(N_{ij})  \deg(P_{ij})$ [@problem_id:2749006].

From our derivation, we see that any transfer function $G(s)$ generated by a finite-dimensional state-space model is necessarily proper, as its limit at infinity is the finite matrix $D$. Conversely, an **improper** transfer function (where at least one entry tends to infinity as $s \to \infty$) cannot be represented by a standard [state-space model](@entry_id:273798); it would require a more general formulation involving derivatives of the input. Furthermore, the identity $D = \lim_{s \to \infty} G(s)$ holds for *any* realization of a proper $G(s)$. It follows directly that a transfer function $G(s)$ is strictly proper if and only if the direct term $D$ is zero in any of its [state-space](@entry_id:177074) realizations [@problem_id:2907652].

### The Existence and Non-Uniqueness of Realizations

Having established how to obtain a transfer function from a [state-space model](@entry_id:273798), we now consider the [inverse problem](@entry_id:634767): given a proper rational [transfer function matrix](@entry_id:271746) $G(s)$, can we find a [state-space realization](@entry_id:166670) $(A,B,C,D)$?

The answer is yes, and a [constructive proof](@entry_id:157587) illuminates the process. For any proper rational matrix $G(s)$, we can perform a decomposition. First, we determine the constant part by taking the limit at infinity:
$$
D = \lim_{s \to \infty} G(s)
$$
This $D$ will be the direct feedthrough matrix of our realization. We can then define a new transfer function $\tilde{G}(s) = G(s) - D$. By construction, $\lim_{s \to \infty} \tilde{G}(s) = D - D = 0$, so $\tilde{G}(s)$ is strictly proper. The task is now reduced to finding a realization $(A,B,C)$ for the strictly proper part, such that $\tilde{G}(s) = C(sI-A)^{-1}B$. The complete realization for $G(s)$ will then be $(A,B,C,D)$.

There are several systematic procedures, or **[canonical forms](@entry_id:153058)**, for constructing a realization $(A,B,C)$ for a strictly proper $\tilde{G}(s)$ [@problem_id:2749006]. For instance, for a SISO system, the controllable and observable [canonical forms](@entry_id:153058) yield matrices whose entries are taken directly from the coefficients of the numerator and denominator polynomials of the transfer function. For a real-rational $G(s)$ (composed of polynomials with real coefficients), these construction methods naturally produce real-valued matrices $(A,B,C,D)$. This guarantees that any proper real-rational transfer function admits a finite-dimensional [state-space realization](@entry_id:166670) over the real numbers.

This existence of realizations leads to a new question. Is the realization for a given $G(s)$ unique? The answer is a definitive no. Consider a change of [state variables](@entry_id:138790) defined by an invertible matrix $T$, such that the new [state vector](@entry_id:154607) is $\bar{x}(t) = Tx(t)$. The original state is recovered by $x(t) = T^{-1}\bar{x}(t)$. Substituting this into the original [state-space equations](@entry_id:266994) gives:
$$
\begin{align}
\frac{d}{dt}(T^{-1}\bar{x}(t)) = A(T^{-1}\bar{x}(t)) + Bu(t) \\
y(t) = C(T^{-1}\bar{x}(t)) + Du(t)
\end{align}
$$
Multiplying the first equation by $T$ gives the new [state-space model](@entry_id:273798) in terms of $\bar{x}$:
$$
\begin{align}
\dot{\bar{x}}(t) = (TAT^{-1})\bar{x}(t) + (TB)u(t) \\
y(t) = (CT^{-1})\bar{x}(t) + Du(t)
\end{align}
$$
This new realization, $(\bar{A}, \bar{B}, \bar{C}, \bar{D}) = (TAT^{-1}, TB, CT^{-1}, D)$, is said to be related to the original by a **[similarity transformation](@entry_id:152935)**. If we compute the transfer function of this new realization, we find:
$$
\bar{G}(s) = \bar{C}(sI-\bar{A})^{-1}\bar{B} + \bar{D} = (CT^{-1})(sI - TAT^{-1})^{-1}(TB) + D
$$
Using the identity $(sI - TAT^{-1})^{-1} = T(sI-A)^{-1}T^{-1}$, we get:
$$
\bar{G}(s) = C(T^{-1}T)(sI-A)^{-1}(T^{-1}T)B + D = C(sI-A)^{-1}B + D = G(s)
$$
The transfer function is invariant under similarity transformations. Since there are infinitely many [invertible matrices](@entry_id:149769) $T$, for any given realization, there exists an infinite family of other realizations that produce the exact same input-output behavior [@problem_id:2727827]. This non-uniqueness is not a flaw, but an inherent property reflecting our freedom to choose any valid basis for the state-space. All realizations related by a similarity transformation are considered equivalent as they describe the same [system dynamics](@entry_id:136288), just from different coordinate perspectives.

### Minimal Realizations: Controllability and Observability

While all realizations in a similarity class are externally equivalent, they are not all equally efficient. A realization might include states that are redundant or have no bearing on the input-output relationship. This motivates the concept of a **[minimal realization](@entry_id:176932)**, which is a realization that achieves the desired transfer function $G(s)$ with the smallest possible state dimension, $n$. This minimum required dimension is an [intrinsic property](@entry_id:273674) of the transfer function itself and is called the **McMillan degree** of the system, denoted $\delta(G)$.

For a multi-input, multi-output (MIMO) system, the McMillan degree is formally defined through the **Smith-McMillan form** of the transfer matrix $G(s)$. This canonical form diagonalizes the rational matrix using unimodular polynomial [matrix transformations](@entry_id:156789), revealing the system's fundamental pole-zero structure. The Smith-McMillan form is given by $M(s) = \text{diag}(\frac{\alpha_1(s)}{\beta_1(s)}, \dots, \frac{\alpha_r(s)}{\beta_r(s)}, 0, \dots, 0)$, where the polynomials satisfy specific divisibility properties. The McMillan degree is the sum of the degrees of the denominator polynomials: $\delta(G) = \sum_{i=1}^r \deg \beta_i(s)$ [@problem_id:2748932]. A realization is then minimal if its state dimension $n$ is equal to this value.

A fundamental theorem of realization theory provides a powerful algebraic condition for minimality: **A [state-space realization](@entry_id:166670) is minimal if and only if it is both completely controllable and completely observable** [@problem_id:2748882].

-   **Controllability** refers to the ability of the input $u(t)$ to steer the [state vector](@entry_id:154607) $x(t)$ to any desired location in the [state-space](@entry_id:177074). A realization $(A,B)$ is controllable if the **[controllability matrix](@entry_id:271824)** $\mathcal{R}_n = \begin{bmatrix} B  AB  \cdots  A^{n-1}B \end{bmatrix}$ has full row rank, i.e., $\operatorname{rank}(\mathcal{R}_n) = n$.

-   **Observability** refers to the ability to determine the initial state $x(0)$ by observing the system's output $y(t)$ over a finite time interval. A realization $(A,C)$ is observable if the **[observability matrix](@entry_id:165052)** $\mathcal{O}_n = \begin{bmatrix} C \\ CA \\ \vdots \\ CA^{n-1} \end{bmatrix}$ has full column rank, i.e., $\operatorname{rank}(\mathcal{O}_n) = n$.

These rank tests, also known as the Kalman rank conditions, are the primary tools for checking minimality. Equivalent frequency-domain tests, known as the Popov-Belevitch-Hautus (PBH) tests, state that a system is controllable (observable) if and only if the matrix $\begin{bmatrix} \lambda I - A  B \end{bmatrix}$ (respectively $\begin{bmatrix} (\lambda I - A)^T  C^T \end{bmatrix}^T$) has rank $n$ for all complex numbers $\lambda$ [@problem_id:2748882]. Another equivalent test for minimality is based on the rank of the block **Hankel matrix** formed from the system's Markov parameters ($H_k = CA^{k-1}B$), which must also equal $n$ [@problem_id:2748882].

For asymptotically stable systems, where all eigenvalues of $A$ have negative real parts, minimality can also be assessed using energy-related concepts. The **controllability Gramian** $P$ and **[observability](@entry_id:152062) Gramian** $Q$ are defined by the Lyapunov equations:
$$
\begin{align}
AP + PA^{\top} + BB^{\top} = 0 \\
A^{\top}Q + QA + C^{\top}C = 0
\end{align}
$$
For a stable system, the pair $(A,B)$ is controllable if and only if $P$ is [positive definite](@entry_id:149459) ($P \succ 0$), and the pair $(A,C)$ is observable if and only if $Q$ is [positive definite](@entry_id:149459) ($Q \succ 0$). Consequently, a stable realization is minimal if and only if both its Gramians are [positive definite](@entry_id:149459) [@problem_id:2749003]. If either Gramian is singular (not positive definite), the realization is non-minimal, and its dimension $n$ must be strictly greater than the McMillan degree $\delta(G)$ [@problem_id:2749003].

### The Mechanism of Non-Minimality: Hidden Modes

The connection between minimality and [controllability](@entry_id:148402)/[observability](@entry_id:152062) clarifies what happens when a realization is non-minimal. A non-[minimal realization](@entry_id:176932) must be either uncontrollable, or unobservable, or both. This means there are internal dynamics, or **modes**, that are "hidden" from the input-output map.

Consider a transfer function with an obvious [pole-zero cancellation](@entry_id:261496), such as $G(s) = \frac{s+1}{(s+1)(s+2)}$. After cancellation, the simplified transfer function is $G(s) = \frac{1}{s+2}$. The McMillan degree of this system is $\delta(G)=1$. If one were to construct a second-order ($n=2$) realization based on the original denominator $s^2+3s+2$, this realization would necessarily be non-minimal. It must contain a mode that corresponds to the cancelled pole at $s=-1$, and this mode must be either uncontrollable or unobservable [@problem_id:1706947].

This phenomenon can be explained more deeply. The poles of the transfer function $G(s)$ correspond to the eigenvalues of the controllable and observable part of the system. The eigenvalues of $A$ that are either uncontrollable or unobservable are called **hidden modes**. These hidden modes do not appear as poles of $G(s)$ because of a precise cancellation mechanism. It can be shown that any uncontrollable or unobservable eigenvalue of the matrix $A$ is also an **invariant zero** of the [state-space realization](@entry_id:166670) $(A,B,C,D)$. Invariant zeros are frequencies $s$ at which the Rosenbrock [system matrix](@entry_id:172230), $\mathcal{S}(s) = \begin{bmatrix} sI-A  -B \\ C  D \end{bmatrix}$, loses rank. When we write the transfer function as $G(s) = \frac{C\,\text{adj}(sI-A)B}{\det(sI-A)}$, these invariant zeros appear as roots of the numerator polynomial, cancelling the corresponding factors in the denominator $\det(sI-A)$ [@problem_id:2749011].

### Implications for System Stability

The existence of hidden modes has profound implications for system stability. We must distinguish between two types of stability:

1.  **External (BIBO) Stability**: This relates to the input-output map. A system is Bounded-Input, Bounded-Output (BIBO) stable if every bounded input produces a bounded output. For an LTI system with a rational transfer function $G(s)$, this is equivalent to all poles of $G(s)$ lying in the open left-half of the complex plane.

2.  **Internal (Lyapunov) Stability**: This relates to the [state-space realization](@entry_id:166670). A realization $(A,B,C,D)$ is internally stable if, for zero input, the state $x(t)$ returns to the origin from any initial condition. This is equivalent to all eigenvalues of the state matrix $A$ lying in the open [left-half plane](@entry_id:270729) (i.e., $A$ is a Hurwitz matrix).

The relationship between these two is not symmetric. If a realization is internally stable, all eigenvalues of $A$ are stable. Since the poles of $G(s)$ are a subset of the eigenvalues of $A$, all poles of $G(s)$ must also be stable. Thus, **[internal stability](@entry_id:178518) implies external stability**.

The converse, however, is not true. A system can be externally stable (a stable $G(s)$) but possess an internally unstable realization. This dangerous situation occurs if the realization is non-minimal, and the unstable mode (an eigenvalue of $A$ in the [right-half plane](@entry_id:277010)) is a hidden mode—that is, it is uncontrollable or unobservable. The instability is masked from the input-output response due to a [pole-zero cancellation](@entry_id:261496), but the internal state can still grow without bound, leading to catastrophic failure. This highlights a critical principle: for any **[minimal realization](@entry_id:176932)**, the set of poles of $G(s)$ is identical to the set of eigenvalues of $A$. Therefore, for minimal realizations, external stability and [internal stability](@entry_id:178518) are equivalent concepts [@problem_id:2748980].

### Extension to Descriptor Systems

The standard state-space model is a special case of the more general **descriptor** or **generalized state-space** form:
$$
\begin{align}
E\dot{x}(t) = Ax(t) + Bu(t) \\
y(t) = Cx(t) + Du(t)
\end{align}
$$
Here, the matrix $E$ may be singular. This form is powerful for modeling systems with algebraic constraints or improper [transfer functions](@entry_id:756102). The transfer function becomes $G(s) = C(sE-A)^{-1}B+D$. For this expression to be meaningful, the [matrix pencil](@entry_id:751760) $sE-A$ must be **regular**, meaning its determinant is not identically zero [@problem_id:2749000].

The concepts of minimality, controllability, and [observability](@entry_id:152062) are extended to this framework. Minimality still requires the absence of hidden modes, but now this includes modes at **infinity**, which can arise when $E$ is singular. The tests for minimality must therefore be augmented to check for [controllability and observability](@entry_id:174003) at infinite frequency, in addition to all finite frequencies [@problem_id:2749000].

A key insight connecting this generalized form back to our main topic is that if a transfer function $G(s)$ is known to be proper, any minimal descriptor realization of it must have an invertible $E$ matrix. An invertible $E$ allows one to pre-multiply the state equation by $E^{-1}$, recovering the [standard state](@entry_id:145000)-[space form](@entry_id:203017) $\dot{x} = (E^{-1}A)x + (E^{-1}B)u$. Thus, the descriptor form's unique power—the singular $E$—is only necessary for realizing improper [transfer functions](@entry_id:756102) [@problem_id:2749000].