## Introduction
Discrete-time [state-space representation](@entry_id:147149) is a cornerstone of modern [systems theory](@entry_id:265873), offering a powerful and unified framework for modeling dynamic processes across science and engineering. From [digital filters](@entry_id:181052) to robotic control and economic forecasting, understanding how a system's internal state evolves is paramount. However, merely writing down the [state equations](@entry_id:274378) is not enough; the core challenge lies in solving them to predict future behavior and analyze fundamental properties like stability and performance. Without a rigorous understanding of the solution's structure, engineers and scientists risk designing unstable systems or misinterpreting complex transient phenomena.

This article provides a comprehensive exploration of the solutions to [discrete-time state-space equations](@entry_id:183866), bridging fundamental theory with practical application. We will dissect the solution into its constituent parts, revealing how a system's response is shaped by both its [initial conditions](@entry_id:152863) and external inputs.

Our exploration unfolds across three interconnected chapters. We will begin in **Principles and Mechanisms**, where we rigorously derive the general solution, explore the critical concepts of stability and [modal analysis](@entry_id:163921), and uncover the nuances of non-normal system dynamics. Building on this theoretical bedrock, the **Applications and Interdisciplinary Connections** chapter will showcase how these solutions are applied in fields like [digital control](@entry_id:275588), stochastic estimation, and large-scale computational modeling. To solidify this knowledge, the **Hands-On Practices** chapter offers guided exercises, allowing you to move from theory to implementation and gain a deeper, intuitive grasp of the material.

## Principles and Mechanisms

This chapter delves into the core principles governing the behavior of [discrete-time state-space](@entry_id:261361) systems. We will derive the general solution to the [state-space equations](@entry_id:266994), analyze its constituent parts, and explore the crucial concepts of stability, modal dynamics, and causality. The focus will be on building a rigorous understanding from first principles, moving from the fundamental structure of the solution to advanced topics in [system dynamics](@entry_id:136288) and numerical computation.

### The Structure and Solution of the State-Space Equations

A linear time-invariant (LTI) discrete-time system is described by a pair of equations: the state equation and the output equation.

$$
\begin{align}
x[k+1]  = A x[k] + B u[k] \\
y[k]  = C x[k] + D u[k]
\end{align}
$$

Here, $x[k]$ is the **[state vector](@entry_id:154607)** at time $k$, a column vector in $\mathbb{R}^n$ that encapsulates the system's memory. The vector $u[k] \in \mathbb{R}^m$ is the **input vector**, representing external influences on the system, and $y[k] \in \mathbb{R}^p$ is the **output vector**, representing the observable signals. The matrices $A, B, C,$ and $D$ are constant matrices that define the system's dynamics and mappings.

The dimensions of these matrices are not arbitrary; they are strictly determined by the rules of linear algebra to ensure the equations are well-defined. By analyzing the matrix-vector products and additions, we can deduce these dimensions [@problem_id:2905356]. In the state equation, since $x[k]$ and $x[k+1]$ are both $n \times 1$ vectors, the terms $A x[k]$ and $B u[k]$ must also be $n \times 1$ vectors.
- For the product $A x[k]$ to yield an $n \times 1$ vector from an $n \times 1$ vector $x[k]$, the matrix $A$ must be square, with dimensions $n \times n$. This is the **state matrix** or **dynamics matrix**.
- For the product $B u[k]$ to yield an $n \times 1$ vector from an $m \times 1$ vector $u[k]$, the matrix $B$ must have dimensions $n \times m$. This is the **input matrix**.

Similarly, in the output equation, $y[k]$ is a $p \times 1$ vector.
- For the product $C x[k]$ to yield a $p \times 1$ vector, the matrix $C$ must have dimensions $p \times n$. This is the **output matrix**.
- For the product $D u[k]$ to yield a $p \times 1$ vector, the matrix $D$ must have dimensions $p \times m$. This is the **feedthrough** or **direct transmission matrix**.

To find the solution for the state vector $x[k]$ at any time $k \ge 0$ given an initial state $x[0]$ and an input sequence $\{u[i]\}_{i \ge 0}$, we can iterate the state equation:
$$
\begin{align}
x[1]  = A x[0] + B u[0] \\
x[2]  = A x[1] + B u[1] = A(A x[0] + B u[0]) + B u[1] = A^2 x[0] + A B u[0] + B u[1] \\
x[3]  = A x[2] + B u[2] = A(A^2 x[0] + A B u[0] + B u[1]) + B u[2] = A^3 x[0] + A^2 B u[0] + A B u[1] + B u[2]
\end{align}
$$
Observing the pattern, we can write the general solution for $x[k]$ as the sum of two components:
$$
x[k] = A^k x[0] + \sum_{i=0}^{k-1} A^{k-1-i} B u[i]
$$
The first term, $A^k x[0]$, is the **[zero-input response](@entry_id:274925)**, representing the evolution of the state due solely to the initial condition $x[0]$. The second term, a [discrete convolution](@entry_id:160939) sum, is the **[zero-state response](@entry_id:273280)**, which describes the evolution of the state from a zero initial condition driven entirely by the input sequence.

A fundamental property of this system is its **causality**. Examining the solution for $x[k]$, we see that it depends on the initial state $x[0]$ and the input samples $u[0], u[1], \dots, u[k-1]$. The state at time $k$ is not influenced by the input at the current time, $u[k]$, or any future inputs. The mapping from the input sequence $u[\cdot]$ to the state sequence $x[\cdot]$ is therefore **strictly causal** [@problem_id:2905373]. It is important to note that the output $y[k]$, however, may depend on the current input $u[k]$ if the feedthrough matrix $D$ is non-zero. The stability of the matrix $A$ has no bearing on this fundamental [causal structure](@entry_id:159914).

### The Zero-Input Response and the State-Transition Matrix

Let us focus on the autonomous (unforced) system, where $u[k] \equiv 0$:
$$
x[k+1] = A x[k]
$$
The solution simplifies to $x[k] = A^k x[0]$. This motivates the definition of the **[state-transition matrix](@entry_id:269075) (STM)** for a discrete-time LTI system as:
$$
\Phi[k] \triangleq A^k
$$
The STM maps the initial state at time $0$ to the state at time $k$: $x[k] = \Phi[k] x[0]$. The set of matrices $\{\Phi[k]\}_{k \ge 0}$ forms a [semigroup](@entry_id:153860) under [matrix multiplication](@entry_id:156035), reflecting the composition of state transitions: $\Phi[k+j] = \Phi[k]\Phi[j]$.

A critical property arises at $k=0$. Logically, the state at time $0$ must be the initial state itself, so we must have $x[0] = \Phi[0] x[0]$. Since this relation must hold for *any* possible initial state $x[0] \in \mathbb{R}^n$, the matrix $\Phi[0]$ must be the identity matrix, $I$ [@problem_id:2905364]. From the definition, this corresponds to the algebraic convention that any [non-singular matrix](@entry_id:171829) raised to the power of zero is the identity, $A^0 = I$. This identity property is also a requirement for $\Phi[0]$ to be the [identity element](@entry_id:139321) of the [transition semigroup](@entry_id:193053).

The dynamic behavior of the [zero-input response](@entry_id:274925) is encoded in the powers of the matrix $A$. A powerful tool for understanding this behavior is the **Spectral Mapping Theorem**. It provides a direct link between the eigenvalues of the dynamics matrix $A$ and the eigenvalues of the [state-transition matrix](@entry_id:269075) $\Phi[k] = A^k$.

**Theorem (Spectral Mapping for Matrix Powers):** If the multiset of eigenvalues of a matrix $A \in \mathbb{C}^{n \times n}$ is $\{\lambda_1, \lambda_2, \dots, \lambda_n\}$, then for any integer $k \ge 1$, the multiset of eigenvalues of $A^k$ is $\{\lambda_1^k, \lambda_2^k, \dots, \lambda_n^k\}$.

This can be seen by considering the Jordan canonical form of $A$, where $A=PJP^{-1}$. Then $A^k = PJ^kP^{-1}$, meaning $A^k$ and $J^k$ share the same eigenvalues. Since $J$ is upper triangular with the eigenvalues of $A$ on its diagonal, $J^k$ is also upper triangular with the values $\lambda_i^k$ on its diagonal. This theorem is fundamental because it tells us that the [natural frequencies](@entry_id:174472) of the system's dynamic response are determined by the powers of the eigenvalues of $A$ [@problem_id:2905359].

### Modal Analysis: Decomposing the System's Behavior

The Spectral Mapping Theorem suggests that the system's response is a combination of terms evolving as $\lambda_i^k$. This idea is made precise through **[modal analysis](@entry_id:163921)**, which is most clearly illustrated when the matrix $A$ is **diagonalizable**. A matrix is diagonalizable if it has a full set of $n$ [linearly independent](@entry_id:148207) eigenvectors. In this case, we can write $A = V \Lambda V^{-1}$, where the columns of $V$ are the eigenvectors $v_i$ of $A$, and $\Lambda$ is a [diagonal matrix](@entry_id:637782) containing the corresponding eigenvalues $\lambda_i$.

The power $A^k$ is then given by $A^k = (V \Lambda V^{-1})^k = V \Lambda^k V^{-1}$. The zero-input solution becomes:
$$
x[k] = V \Lambda^k V^{-1} x[0]
$$
This expression reveals the underlying structure of the solution. Let us define the vector of **modal coordinates** $\alpha = V^{-1} x[0]$. This vector represents the coordinates of the initial state $x[0]$ in the basis of eigenvectors. The initial state can be expressed as a linear combination of eigenvectors: $x[0] = \sum_{i=1}^n \alpha_i v_i$. Substituting this into the solution, we get:
$$
x[k] = A^k \left( \sum_{i=1}^n \alpha_i v_i \right) = \sum_{i=1}^n \alpha_i (A^k v_i) = \sum_{i=1}^n \alpha_i \lambda_i^k v_i
$$
This equation is the heart of [modal analysis](@entry_id:163921). It shows that the state trajectory is a superposition of the system's **modes**. Each mode corresponds to an eigenvector $v_i$ and evolves independently in time according to the simple [geometric progression](@entry_id:270470) $\lambda_i^k$. The coefficients $\alpha_i$ determine how much each mode is excited by the initial condition.

The output $y[k]$ is then found by applying the output matrix $C$:
$$
y[k] = C x[k] = \sum_{i=1}^n \alpha_i (C v_i) \lambda_i^k
$$
This form shows that the output is also a weighted sum of the exponential terms $\lambda_i^k$. The term $C v_i$, which is the inner product of the $j$-th row of $C$ with the $i$-th eigenvector, determines how strongly the $i$-th mode of the state appears in the $j$-th component of the output. If $C v_i = 0$ for a particular mode $i$, that mode is **unobservable** in the output, even if it is present in the state trajectory (i.e., $\alpha_i \neq 0$) [@problem_id:2905376]. For instance, if a system has modes associated with eigenvalues $\lambda_1 = 0.5$ and $\lambda_2 = -0.25$, but the output matrix $C$ is orthogonal to the eigenvector $v_1$ associated with $\lambda_1$, the output will only contain the term $(-0.25)^k$, completely hiding the presence of the first mode.

### Stability of the Zero-Input Response

A primary concern in [system analysis](@entry_id:263805) is stability: does the state remain bounded, or does it converge to the origin? For the zero-input system $x[k+1] = Ax[k]$, the origin $x=0$ is an equilibrium point. Its stability is determined by the long-term behavior of the [state-transition matrix](@entry_id:269075) $\Phi[k] = A^k$. The norm of the state is bounded by:
$$
\|x[k]\| = \|\Phi[k] x[0]\| \le \|\Phi[k]\| \|x[0]\|
$$
where $\|\cdot\|$ denotes any [vector norm](@entry_id:143228) and its [induced operator norm](@entry_id:750614). This inequality is central to stability analysis because the scalar sequence $\|\Phi[k]\|$ provides a uniform bound on the amplification of the initial state's norm for *any* initial condition [@problem_id:2905341]. This leads to precise definitions of stability:

-   **Lyapunov Stability:** The origin is Lyapunov stable if $\|\Phi[k]\|$ is uniformly bounded for all $k \ge 0$. This ensures that trajectories starting close to the origin remain close to the origin. If $\|\Phi[k]\|$ is unbounded, the origin is unstable [@problem_id:2905341, F].
-   **Asymptotic Stability:** The origin is asymptotically stable if $\|\Phi[k]\| \to 0$ as $k \to \infty$. This ensures that all trajectories converge to the origin.
-   **Exponential Stability:** The origin is exponentially stable if there exist constants $M > 0$ and $\alpha \in (0,1)$ such that $\|\Phi[k]\| \le M \alpha^k$ for all $k \ge 0$. This specifies a minimum rate of convergence. For LTI systems, asymptotic and [exponential stability](@entry_id:169260) are equivalent.

For LTI systems, these norm-based conditions are equivalent to conditions on the eigenvalues of $A$. The system is asymptotically stable if and only if all eigenvalues of $A$ have a magnitude strictly less than 1. This is often stated as the **[spectral radius](@entry_id:138984)** of $A$, $\rho(A) = \max_i |\lambda_i|$, must be less than 1. The [spectral mapping theorem](@entry_id:264489) provides the link: if $\rho(A)  1$, then the eigenvalues of $A^k$ are $\lambda_i^k$, which all go to zero as $k \to \infty$. This, in turn, ensures that $\|A^k\| \to 0$. Conversely, if $A^k \to 0$, its eigenvalues $\lambda_i^k$ must go to zero, which implies $|\lambda_i|  1$ for all $i$.

It follows from the relation $\rho(A^m) = (\rho(A))^m$ that if a system is asymptotically stable ($\rho(A)  1$), any $m$-step downsampled version of it, governed by $A^m$, is also asymptotically stable. Conversely, if an $m$-step system is stable ($\rho(A^m)  1$), then the original one-step system must also be stable [@problem_id:2905359].

### Advanced Topics in System Dynamics

While [eigenvalue analysis](@entry_id:273168) is powerful, it can be misleading if not applied with care, particularly for systems whose dynamics matrix $A$ is **non-normal**. A matrix is normal if it commutes with its conjugate transpose ($AA^* = A^*A$); examples include symmetric, skew-symmetric, and unitary matrices. Matrices that are not normal can exhibit complex transient behaviors not predicted by their eigenvalues alone.

#### Transient Behavior in Non-Normal Systems

For a stable LTI system ($\rho(A)  1$), all trajectories eventually decay to zero. However, the norm of the state, $\|x[k]\|$, does not necessarily decrease monotonically. It can experience significant temporary amplification, a phenomenon known as **transient growth**, before the eventual decay takes hold. This is a hallmark of [non-normal systems](@entry_id:270295) [@problem_id:2905346].

The intuition from [modal analysis](@entry_id:163921) can be deceptive here. One might assume that if all modes $\lambda_i^k$ are decaying, their sum should also decay. This fails for [non-normal systems](@entry_id:270295) because their eigenvectors are not orthogonal. If the eigenvectors are nearly parallel, the eigenvector matrix $V$ is highly **ill-conditioned** (its condition number $\kappa(V) = \|V\|\|V^{-1}\|$ is very large). In this case, to represent an initial state $x[0]$ with a small norm, the [modal coefficients](@entry_id:752057) $\alpha = V^{-1}x[0]$ might be very large and nearly canceling. As these large coefficients decay at different rates ($\lambda_i^k$), the delicate cancellation is undone, and the resulting [state vector](@entry_id:154607) $x[k] = V \Lambda^k \alpha$ can have a much larger norm for some finite $k$.

A more robust way to understand this is via the **Schur decomposition**, $A=QTQ^*$, where $Q$ is unitary and $T$ is upper-triangular with the eigenvalues of $A$ on its diagonal. Since $Q$ is unitary, it preserves the Euclidean norm, and $\|x[k]\|_2 = \|A^k x[0]\|_2 = \|Q T^k Q^* x[0]\|_2 = \|T^k (Q^* x[0])\|_2$. The behavior of $\|x[k]\|_2$ is identical to the behavior of the system governed by $T$. The off-diagonal elements of $T$ represent coupling between the system's modes (represented by the Schur vectors, the columns of $Q$). A large off-diagonal element $T_{ij}$ can "pump" energy from the decaying mode associated with $\lambda_j$ into the mode associated with $\lambda_i$, causing transient growth in the components of the [state vector](@entry_id:154607) in the Schur basis. For a [normal matrix](@entry_id:185943), $T$ is diagonal, there is no coupling, and no transient growth can occur. For a stable normal system, $\|A^k\|_2 = \rho(A)^k$, ensuring monotonic decay of the worst-case [amplification factor](@entry_id:144315) [@problem_id:2905346].

#### Computational Considerations for Matrix Powers

The distinction between normal and [non-normal systems](@entry_id:270295) has profound practical consequences for computation. When we need to calculate the state $x[k]=A^k x[0]$ for large $k$, we might consider using a [matrix decomposition](@entry_id:147572).
- The eigen-decomposition method computes $A^k = V \Lambda^k V^{-1}$.
- The Schur-based method computes $A^k = Q T^k Q^*$.

For a [non-normal matrix](@entry_id:175080) with an ill-conditioned eigenvector matrix $V$, the eigen-decomposition approach is **numerically unstable** [@problem_id:2905343]. The large condition number $\kappa(V)$ acts as an amplification factor for any [floating-point](@entry_id:749453) roundoff errors introduced during the computation. An error of size $u$ (the machine precision) can be magnified to an error of size $\kappa(V)u$ in the final result.

In contrast, the Schur-based method is **numerically stable**. The transformation matrix $Q$ is unitary and thus perfectly conditioned ($\kappa_2(Q)=1$). It does not amplify errors. The numerical stability of the overall computation is determined by the stability of computing the power of the triangular matrix, $T^k$. This can be done robustly. The Schur method's accuracy is limited only by the intrinsic sensitivity of the problem of computing $A^k$, not by an additional penalty from an ill-conditioned basis change. This makes it the preferred method for reliable computation of [matrix powers](@entry_id:264766) for general matrices.

### The Forced Response and Impulse Response

Returning to the full solution, we now consider the [zero-state response](@entry_id:273280) driven by the input $u[k]$:
$$
x_{zs}[k] = \sum_{i=0}^{k-1} A^{k-1-i} B u[i]
$$
A fundamental characterization of an LTI system is its **impulse response**, which is the output produced by a [unit impulse](@entry_id:272155) input, assuming the system starts from rest ($x[0]=0$). For a multi-input, multi-output (MIMO) system, we define an impulse [response matrix](@entry_id:754302), $g[k] \in \mathbb{R}^{p \times m}$. The $j$-th column of $g[k]$ is the system's output $y[k]$ when the input is an impulse on the $j$-th input channel, i.e., $u[k] = \delta[k] e_j$, where $e_j$ is the $j$-th standard basis vector.

By applying the solution formula, we can find the expression for $g[k]$.
For $k > 0$, the input is $u[0] = e_j$ and $u[i]=0$ for $i>0$.
$$
x[k] = A^{k-1} B e_j
$$
The output is $y[k] = C x[k] + D u[k] = C A^{k-1} B e_j$ (since $u[k]=0$ for $k>0$).
For $k=0$, the state sum is empty ($x[0]=0$), and the output is $y[0] = D u[0] = D e_j$.
The $j$-th column of $g[k]$ is thus $C A^{k-1} B e_j$ for $k \ge 1$ and $D e_j$ for $k=0$. Assembling all columns, we find the impulse [response matrix](@entry_id:754302):
$$
g[k] = \begin{cases} D  k=0 \\ C A^{k-1} B  k \ge 1 \end{cases}
$$
By linearity, the response to a general impulse input $u[k]=\delta[k]v$ for an arbitrary [direction vector](@entry_id:169562) $v \in \mathbb{R}^m$ can be found by decomposing $v = \sum v_i e_i$. The output is the superposition of the responses to each component, which results in $y[k] = g[k]v$ [@problem_id:2905378]. More generally, the zero-state output response is the [discrete convolution](@entry_id:160939) of the input sequence with the impulse [response matrix](@entry_id:754302): $y_{zs}[k] = \sum_{i=0}^k g[k-i] u[i]$.

### Extension to Linear Periodic Systems

The stability analysis based on eigenvalues of a constant matrix $A$ is a special property of LTI systems. For linear time-varying (LTV) systems, where $x[k+1] = A[k]x[k]$, the situation is more complex. A particularly important class of LTV systems are those with periodic coefficients, where $A[k+p] = A[k]$ for some period $p$.

In this case, the instantaneous eigenvalues of $A[k]$ do not determine stability [@problem_id:2905345]. Because the matrices $A[k]$ at different times may not commute, the spectrum of their product (which governs the evolution over multiple steps) is not related in a simple way to their individual spectra. It is possible to construct a system where every matrix $A[k]$ has eigenvalues with magnitude greater than 1, yet the system as a whole is stable.

Stability is instead determined by examining the system's evolution over one full period. We define the **[monodromy matrix](@entry_id:273265)** as the [state-transition matrix](@entry_id:269075) over one period, starting from some time $k_0$:
$$
M \triangleq \Phi[k_0+p, k_0] = A[k_0+p-1] \cdots A[k_0+1] A[k_0]
$$
The state sampled every $p$ steps evolves according to a simple LTI system: $x[k_0 + (n+1)p] = M x[k_0 + np]$. Therefore, the long-term stability of [the periodic system](@entry_id:185882) is governed by the powers of the constant matrix $M$. The system is asymptotically stable if and only if the [spectral radius](@entry_id:138984) of the [monodromy matrix](@entry_id:273265) is less than one, $\rho(M)  1$. The eigenvalues of $M$ are called the **Floquet multipliers**. This powerful result, a cornerstone of Floquet theory, shows that for periodic systems, stability is determined not by instantaneous properties, but by the aggregate dynamics over a complete cycle.