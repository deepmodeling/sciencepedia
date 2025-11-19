## Introduction
In the realm of [digital control](@entry_id:275588) and signal processing, ensuring [system stability](@entry_id:148296) is a non-negotiable prerequisite for reliable performance. A discrete-time system's behavior is governed by the locations of its characteristic polynomial's roots relative to the complex unit circle. While conceptually simple, directly calculating these roots for high-order systems is often computationally impractical and numerically sensitive. This article addresses this challenge by providing a comprehensive guide to the Jury stability criterion, a powerful algebraic tool that assesses stability using only a polynomial's coefficients. Across the following sections, you will first master the theoretical principles behind discrete-time stability and the step-by-step mechanics of the Jury test. You will then explore its diverse applications, from designing robust control systems to analyzing the effects of digital implementation. Finally, you will apply your knowledge through a series of hands-on practice problems. We begin by delving into the core principles and mechanisms that define stability in the discrete-time domain.

## Principles and Mechanisms

In the analysis of discrete-time linear time-invariant (LTI) systems, the concept of stability is paramount. It determines whether the system's response to a bounded input or initial condition will remain bounded or decay to an equilibrium. While the previous section introduced the foundational importance of stability, this section delves into the core principles and mechanical procedures used to assess it. We will move from the fundamental definition of stability based on eigenvalue locations to a powerful algebraic tool—the Jury criterion—that bypasses the need for explicit [root-finding](@entry_id:166610).

### The Nature of Stability in Discrete-Time Systems

A discrete-time LTI system can be described by the state-space equation $x_{k+1} = A x_k$, where $x_k \in \mathbb{R}^n$ is the [state vector](@entry_id:154607) at time step $k$ and $A \in \mathbb{R}^{n \times n}$ is the constant [state-transition matrix](@entry_id:269075). The evolution of the system from an initial state $x_0$ is given by the trajectory $x_k = A^k x_0$. The system's stability is entirely determined by the properties of the matrix $A$.

The system is said to be **asymptotically stable** if, for any initial condition $x_0$, the state converges to the origin, i.e., $x_k \to 0$ as $k \to \infty$. This occurs if and only if all eigenvalues $\lambda_i$ of the matrix $A$ have a magnitude strictly less than one. This condition, $\max_i |\lambda_i|  1$, is often referred to as **Schur stability**. The eigenvalues of $A$ are the roots of its characteristic polynomial, $p(z) = \det(zI - A) = 0$. Therefore, assessing [asymptotic stability](@entry_id:149743) is equivalent to determining if all roots of the characteristic polynomial lie strictly inside the open unit disk in the complex plane, $\{z \in \mathbb{C} : |z|  1\}$.

While conceptually simple, finding the roots of a high-degree polynomial can be computationally intensive and numerically sensitive. This motivates the search for algebraic methods that can determine the location of the roots relative to the unit circle using only the polynomial's coefficients.

### On the Boundary: Marginal Stability

Before developing a test for strict stability, it is instructive to understand what happens when one or more eigenvalues lie precisely *on* the unit circle, i.e., $|\lambda_i| = 1$. Such systems are not asymptotically stable, but their behavior can range from bounded oscillations to unbounded growth. The Jury criterion will signal a failure for such cases, but the underlying system dynamics depend on the nature of these unit-modulus eigenvalues.

Consider an eigenvalue $\lambda$ with $|\lambda|=1$. A critical distinction arises based on its [multiplicity](@entry_id:136466). The **[algebraic multiplicity](@entry_id:154240)** is the number of times it appears as a root of the characteristic polynomial. The **geometric multiplicity** is the number of linearly independent eigenvectors associated with it, which is equivalent to the number of Jordan blocks corresponding to that eigenvalue.

**1. Simple Eigenvalues on the Unit Circle:**
If the eigenvalues on the unit circle are simple ([algebraic multiplicity](@entry_id:154240) is one), the system exhibits bounded, oscillatory behavior. For example, the system with matrix $A_1 = \begin{bmatrix} \cos(\theta)  -\sin(\theta) \\ \sin(\theta)  \cos(\theta) \end{bmatrix}$ has distinct [complex conjugate eigenvalues](@entry_id:152797) $e^{\pm i\theta}$ on the unit circle. The state vector $x_k = A_1^k x_0$ rotates at each step but its norm remains constant: $\|x_k\|_2 = \|x_0\|_2$. The system is **Lyapunov stable** (bounded trajectories for bounded [initial conditions](@entry_id:152863)) but not asymptotically stable [@problem_id:2747014].

**2. Repeated Eigenvalues on the Unit Circle:**
If an eigenvalue on the unit circle has an algebraic multiplicity greater than one, the system's stability depends on whether its algebraic and geometric multiplicities are equal.

*   **Equal Multiplicities (Diagonalizable Case):** If the algebraic and geometric multiplicities are equal, the Jordan blocks associated with the eigenvalue are all of size $1 \times 1$. The system is diagonalizable. An example is the system with matrix $A_3 = I_2 = \begin{bmatrix} 1  0 \\ 0  1 \end{bmatrix}$. The eigenvalue $\lambda=1$ has algebraic and geometric multiplicity of two. The trajectory is simply $x_k = x_0$, which is bounded. This system is also Lyapunov stable but not asymptotically stable [@problem_id:2747014].

*   **Unequal Multiplicities (Defective Case):** If the [algebraic multiplicity](@entry_id:154240) exceeds the [geometric multiplicity](@entry_id:155584), there exists at least one Jordan block of size greater than $1 \times 1$. This structure introduces polynomial-in-$k$ terms into the state response, leading to unbounded trajectories. Consider the canonical example $A_2 = \begin{pmatrix} 1  1 \\ 0  1 \end{pmatrix}$. Its characteristic polynomial is $(z-1)^2=0$, giving a repeated eigenvalue $\lambda=1$ with [algebraic multiplicity](@entry_id:154240) two. However, its [geometric multiplicity](@entry_id:155584) is one. The matrix power can be calculated as $A_2^k = \begin{pmatrix} 1  k \\ 0  1 \end{pmatrix}$. For an initial condition like $x_0 = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$, the trajectory is $x_k = \begin{pmatrix} k \\ 1 \end{pmatrix}$. The Euclidean norm of the state, $\|x_k\|_2 = \sqrt{k^2+1}$, grows without bound as $k \to \infty$ [@problem_id:2746999]. Such a system is **unstable**.

This analysis reveals why Schur stability requires all eigenvalues to be *strictly* inside the unit disk. Any eigenvalue on the unit circle leads to a failure of [asymptotic stability](@entry_id:149743), and if it is associated with a non-trivial Jordan block, it causes outright instability.

### The Jury Criterion: An Algebraic Approach

The Jury stability criterion is an algebraic procedure that determines whether a real-coefficient polynomial is Schur stable without computing its roots. It consists of a set of necessary conditions and a tabular or recursive test that provides sufficiency.

#### Initial Necessary Conditions

Let $p(z) = a_{0} z^{n} + a_{1} z^{n-1} + \cdots + a_{n}$ be a polynomial with real coefficients and $a_0  0$. If all its zeros $\{z_i\}$ satisfy $|z_i|  1$, we can derive several simple but powerful necessary conditions directly from its factored form $p(z) = a_{0} \prod_{i=1}^{n} (z - z_{i})$ [@problem_id:2747051].

1.  **Condition at $z=1$: $p(1)  0$**
    Evaluating the polynomial at $z=1$ gives $p(1) = a_{0} \prod_{i=1}^{n} (1 - z_{i})$. Since the polynomial has real coefficients, its [complex roots](@entry_id:172941) come in conjugate pairs.
    *   If $z_i$ is a real root, $|z_i|  1$ implies $-1  z_i  1$, so $(1 - z_i)$ is a positive real number.
    *   If $z_i$ and $\bar{z}_i$ form a [complex conjugate pair](@entry_id:150139), the product of their corresponding factors is $(1-z_i)(1-\bar{z}_i) = |1-z_i|^2$, which is a positive real number (since $z_i \neq 1$).
    Since all terms in the product are positive and $a_0  0$, we must have $p(1)  0$. Geometrically, this condition relates to the vectors drawn from each root to the point $z=1$ in the complex plane.

2.  **Condition at $z=-1$: $(-1)^{n} p(-1)  0$**
    Evaluating at $z=-1$ gives $p(-1) = a_{0} \prod_{i=1}^{n} (-1 - z_{i}) = a_0 (-1)^n \prod_{i=1}^{n} (1 + z_{i})$. Thus, $(-1)^n p(-1) = a_0 \prod_{i=1}^{n} (1 + z_{i})$. By an argument analogous to the one above, the product $\prod (1+z_i)$ is a positive real number, so the condition must hold.

3.  **Condition on the Constant Term: $|a_n|  a_0$**
    The coefficients of the polynomial are related to its roots via Vieta's formulas. The constant term is $a_n = p(0) = a_0 \prod_{i=1}^{n} (-z_i) = a_0 (-1)^n \prod_{i=1}^{n} z_i$. Taking the absolute value gives $|a_n| = |a_0| \prod_{i=1}^{n} |z_i| = a_0 \prod_{i=1}^{n} |z_i|$. Since every root satisfies $|z_i|  1$, their product must also be less than one, i.e., $\prod |z_i|  1$. This directly leads to the inequality $|a_n|  a_0$.

These three conditions are the first checks in the Jury test. For instance, for a quartic polynomial $p(z) = z^4+bz^3+cz^2+dz+e$, the initial test requires $p(1)  0$, $p(-1)0$, and $|e|1$. The product $p(1)p(-1)$ can be conveniently written as $((1+c+e)^2 - (b+d)^2)$, which must be positive [@problem_id:2747051]. While essential, these conditions are not sufficient for stability beyond second-order polynomials.

### The Full Jury Test: Algorithm and Implementation

To establish sufficiency, the Jury criterion employs a systematic procedure that reduces the degree of the polynomial at each step while preserving its stability characteristics. This can be viewed either as a tabular calculation or a polynomial recursion.

#### The Tabular Form

The most common implementation of the Jury test involves constructing a table from the polynomial's coefficients [@problem_id:2747045]. For $p(z) = a_0 z^n + \cdots + a_n$ with $a_0  0$, the table is built as follows:

The first two rows are formed from the coefficients:
*   Row 1: $[a_0, a_1, \dots, a_{n-1}, a_n]$
*   Row 2: $[a_n, a_{n-1}, \dots, a_1, a_0]$ (coefficients in reverse order)

Subsequent rows are generated in pairs. The third row, with coefficients $[b_0, b_1, \dots, b_{n-1}]$, is calculated from the first two rows using the rule:
$b_k = \det \begin{pmatrix} a_0  a_{n-k} \\ a_n  a_k \end{pmatrix} = a_0 a_k - a_n a_{n-k}$ for $k=0, 1, \dots, n-1$.

The fourth row is the reversal of the third: $[b_{n-1}, \dots, b_0]$. This process is repeated, generating a new set of coefficients $[c_0, \dots, c_{n-2}]$ from $[b_0, \dots, b_{n-1}]$ and its reversal, and so on. The table construction continues until a row with only three elements is obtained.

For example, given $p(z) = 4 z^4 - 2 z^3 + 3 z^2 + 1 z + 2$, the first row is $[4, -2, 3, 1, 2]$ and the second is $[2, 1, 3, -2, 4]$. The first reduced row $[b_0, b_1, b_2, b_3]$ is computed as:
*   $b_0 = 4 \cdot 4 - 2 \cdot 2 = 12$
*   $b_1 = 4 \cdot (-2) - 2 \cdot 1 = -10$
*   $b_2 = 4 \cdot 3 - 2 \cdot 3 = 6$
*   $b_3 = 4 \cdot 1 - 2 \cdot (-2) = 8$
The next stage of the test would proceed with the polynomial $12z^3 - 10z^2 + 6z + 8$ [@problem_id:2747045].

The polynomial $p(z)$ is Schur stable if and only if:
1.  $p(1)  0$
2.  $(-1)^n p(-1)  0$
3.  The following $n-1$ constraints on the leading coefficients of each stage hold:
    *   $|a_n|  a_0$
    *   $|b_{n-1}|  |b_0|$
    *   $|c_{n-2}|  |c_0|$
    *   ...and so on, until the final stage.
Note that since we require $a_0  0$, the conditions $b_0  0, c_0  0, \dots$ are implicitly required for the inequalities to be well-defined.

#### The Recursive Form and Stopping Criterion

The tabular method is an implementation of a deeper polynomial recursion [@problem_id:2746994]. Starting with $p^{(0)}(z) = p(z)$, a sequence of polynomials $p^{(k)}(z)$ of decreasing degree $m_k = n-k$ is generated. The key step is the Schur transformation, which relates $p^{(k)}(z)$ to $p^{(k+1)}(z)$. The stability of $p^{(k)}(z)$ is equivalent to the stability of $p^{(k+1)}(z)$ provided that a "[reflection coefficient](@entry_id:141473)" $\kappa_k = a_{m_k}^{(k)} / a_0^{(k)}$ satisfies $|\kappa_k|1$. This is precisely the condition $|a_{m_k}^{(k)}|  a_0^{(k)}$ checked at each stage of the tabular test.

The recursion terminates after $n-1$ steps, yielding a first-degree polynomial, let's call it $P^{(n-1)}(z) = r_1 z + r_0$ [@problem_id:2747019]. For the original system to be stable, this final polynomial must also be stable. According to the fundamental definition, its single root $z^\star = -r_0/r_1$ must satisfy $|z^\star|  1$. This implies:
$|-\frac{r_0}{r_1}|  1 \implies \frac{|r_0|}{|r_1|}  1$.
Since the Jury procedure maintains a positive leading coefficient, we have $r_1  0$, so the condition simplifies to $|r_0|  r_1$. This elegant result shows how the abstract algebraic test connects back to the basic definition of stability at its final step.

### Broader Context and Extensions

The Jury criterion is a cornerstone of discrete-time stability analysis, but it is important to understand its relationships to other methods and its limitations.

#### Relation to the Schur-Cohn Test

The Jury criterion is a specialized, computationally efficient version of the more general **Schur-Cohn test**. The Schur-Cohn test applies to polynomials with complex coefficients and is derived from Issai Schur's work on [analytic functions](@entry_id:139584) that are bounded on the [unit disk](@entry_id:172324) [@problem_id:2747016]. For a simple first-order polynomial with a complex coefficient, $p(z) = z+a$, the standard Jury criterion is not applicable. The Schur-Cohn test, however, applies directly. For a polynomial $a_1 z + a_0$, the condition is $|a_0|  |a_1|$. With $a_1=1$ and $a_0=a$, this immediately gives the stability condition $|a|1$, meaning the coefficient $a$ must lie in the open unit disk of the complex plane [@problem_id:2747052]. The recursive forms of both the Jury and Schur-Cohn tests have a [computational complexity](@entry_id:147058) of $O(n^2)$, making them highly practical.

#### Connection to Continuous-Time Stability

Many [discrete-time systems](@entry_id:263935) arise from the sampling of continuous-time processes. The **[bilinear transform](@entry_id:270755)**, $s = \frac{2}{T} \frac{z-1}{z+1}$, is a standard tool that maps the interior of the [unit disk](@entry_id:172324) in the $z$-plane to the open left-half of the $s$-plane. This provides a direct link between discrete-time stability (Jury criterion) and continuous-time stability (Routh-Hurwitz criterion).

One can verify the stability of a discrete-time system by applying the [bilinear transform](@entry_id:270755) to its [characteristic polynomial](@entry_id:150909) and then using the Routh-Hurwitz test on the resulting $s$-domain polynomial. Conversely, this mapping demonstrates the deep theoretical consistency between the two domains. For example, if a continuous-time system has a [characteristic polynomial](@entry_id:150909) $p_c(s,K) = s^3+3s^2+2s+K$, the Routh-Hurwitz test shows it is stable for $0  K  6$. If we apply the [bilinear transform](@entry_id:270755) (with $T=1$ for simplicity), we obtain a discrete-time characteristic polynomial $p_d(z,K)$. Applying the Jury criterion to $p_d(z,K)$ yields the exact same stability range, $0  K  6$, confirming that the transform preserves the stability boundary [@problem_id:2747065].

#### Limitations and Lyapunov's Method

The Jury criterion's primary limitation is that it applies only to **Linear Time-Invariant (LTI)** systems. It cannot be used to analyze the stability of time-varying or [switched systems](@entry_id:271268), described by $x_{k+1} = A_k x_k$, where the matrix $A_k$ changes over time. Such systems do not have a single, time-invariant characteristic polynomial that governs all possible trajectories [@problem_id:2747000].

For these more complex systems, a more powerful and general approach is required: **Lyapunov [stability theory](@entry_id:149957)**. For a switched system where $A_k$ can be any matrix from a set $\{A_1, A_2, \dots, A_M\}$, stability of each individual matrix $A_i$ is not sufficient to guarantee stability of the switched system. A stronger condition is the existence of a **Common Quadratic Lyapunov Function (CQLF)**, $V(x) = x^T P x$ with $P$ being a [positive definite matrix](@entry_id:150869), such that $V(x)$ decreases for every possible mode. That is, $A_i^T P A_i - P$ must be [negative definite](@entry_id:154306) for all $i$. Finding such a $P$ proves stability under arbitrary switching, a task far beyond the scope of the Jury criterion [@problem_id:2747000]. This highlights that while the Jury criterion is an indispensable tool for LTI systems, the analysis of modern complex systems often requires the more fundamental and versatile framework of Lyapunov theory.