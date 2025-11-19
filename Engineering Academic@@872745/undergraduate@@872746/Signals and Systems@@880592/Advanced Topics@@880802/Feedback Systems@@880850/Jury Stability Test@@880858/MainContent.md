## Introduction
Stability is a fundamental requirement for any well-behaved discrete-time system, from a digital audio filter to a drone's flight controller. A system is considered stable if its output remains bounded for any bounded input, a property directly linked to the location of its poles in the z-domain. For stability, all poles must lie strictly inside the unit circle. While calculating the poles—the roots of the system's [characteristic polynomial](@entry_id:150909)—is a direct way to check this, it becomes computationally prohibitive and impractical for higher-order systems or when dealing with symbolic design parameters. The Jury Stability Test offers an elegant and powerful algebraic alternative, allowing engineers and scientists to assess stability directly from the polynomial's coefficients without solving for the roots.

This article provides a comprehensive guide to mastering the Jury test. The first chapter, **Principles and Mechanisms**, will deconstruct the test's algorithm, from its simple preliminary conditions and the special case of [second-order systems](@entry_id:276555) to the full Jury array for higher-order analysis. Next, **Applications and Interdisciplinary Connections** will demonstrate the test's practical utility in tuning digital controllers, designing stable filters, and even analyzing models in fields like ecology. Finally, **Hands-On Practices** will offer guided problems to solidify your understanding and build practical skills. By navigating these chapters, you will gain the theoretical knowledge and practical expertise to confidently apply this indispensable tool to a wide range of [system analysis](@entry_id:263805) and design challenges.

## Principles and Mechanisms

In the study of discrete-time linear time-invariant (LTI) systems, ensuring stability is of paramount importance. A system is defined as Bounded-Input, Bounded-Output (BIBO) stable if and only if every bounded input signal produces a bounded output signal. This crucial property translates to a specific mathematical constraint in the z-domain: all poles of the system's transfer function, $H(z)$, must lie strictly inside the unit circle. The poles are the roots of the denominator polynomial of $H(z)$, commonly referred to as the **characteristic polynomial**, denoted $A(z)$.

While one could, in principle, find all the roots of $A(z)$ to check their locations, this process is computationally intensive and often impractical for high-order polynomials or when coefficients are symbolic parameters. The **Jury Stability Test**, named after Eliahu I. Jury, provides a powerful algebraic method to determine if all roots of a polynomial lie within the unit circle without calculating the roots themselves. This chapter elucidates the principles and mechanics of this test, from foundational concepts to advanced applications.

### The Jury Stability Criterion: Core Conditions

The Jury test is an algorithmic procedure applied to the coefficients of the characteristic polynomial. Let the polynomial be represented as:

$$A(z) = a_n z^n + a_{n-1} z^{n-1} + \dots + a_1 z + a_0$$

where the coefficients $a_k$ are real numbers. A fundamental prerequisite for the standard test procedure is that the leading coefficient, $a_n$, must be positive. If one encounters a [characteristic polynomial](@entry_id:150909) with a negative leading coefficient, such as in the analysis of a particular climate control system model [@problem_id:1732192], the entire polynomial must first be multiplied by $-1$. This operation does not alter the roots, thus preserving the stability properties of the system, while satisfying the precondition $a_n > 0$.

The Jury test provides a set of conditions that are both necessary and sufficient for stability. These conditions can be categorized into simple preliminary checks and a more involved iterative procedure.

### Preliminary Checks: A First Line of Defense

Before constructing the full Jury test array, a few necessary (but not generally sufficient) conditions can be rapidly checked. If any of these conditions fail, the system is guaranteed to be unstable, and no further testing is needed. For a polynomial $A(z)$ with $a_n > 0$, these conditions are:

1.  $A(1) > 0$
2.  $(-1)^n A(-1) > 0$
3.  $|a_0|  a_n$

Failure to meet these conditions provides immediate insight into the nature of the instability. The first condition, $A(1) > 0$, is related to the absence of poles at or beyond $z=1$ on the real axis. The second condition, $(-1)^n A(-1) > 0$, is related to the absence of poles at or beyond $z=-1$. The third condition, $|a_0|  a_n$, relates to the product of the magnitudes of the roots. Since Vieta's formulas tell us that $a_0/a_n = (-1)^n \prod_{k=1}^n z_k$, where $z_k$ are the roots, the condition $|a_0|  a_n$ implies $|\prod_{k=1}^n z_k|  1$. This is a necessary consequence of all roots having magnitudes less than 1, i.e., $|z_k|1$ for all $k$.

For example, consider a third-order system with the characteristic polynomial $A(z) = z^3 - 2.5z^2 + 2z - 0.8$ [@problem_id:1732234]. Here, $n=3$ and $a_3=1$. Let's check the first two necessary conditions:
- $A(1) = 1 - 2.5 + 2 - 0.8 = -0.3$. Since $A(1)  0$, the first condition is violated.
- $A(-1) = (-1)^3 - 2.5(-1)^2 + 2(-1) - 0.8 = -1 - 2.5 - 2 - 0.8 = -6.3$.
- $(-1)^3 A(-1) = (-1)(-6.3) = 6.3 > 0$. The second condition is met.

Since the first condition failed, we can conclude the system is unstable without proceeding further. The satisfaction of these preliminary conditions is mandatory, but for systems of degree $n > 2$, it does not guarantee stability.

### The Special Case of Second-Order Systems

For [second-order systems](@entry_id:276555), a case frequently encountered in control and signal processing, the three necessary conditions listed above are also **sufficient** for stability. This provides a remarkably simple and direct stability test. For a polynomial $A(z) = a_2 z^2 + a_1 z + a_0$ with $a_2 > 0$, the system is stable if and only if:

1.  $A(1) = a_2 + a_1 + a_0 > 0$
2.  $A(-1) = a_2 - a_1 + a_0 > 0$
3.  $|a_0|  a_2$

These three inequalities define a triangular region in the space of coefficients, often called the **[stability triangle](@entry_id:275779)** for monic polynomials (where $a_2=1$). Any pair of coefficients $(a_1, a_0)$ that lies within this triangle corresponds to a stable system.

Let's analyze a system described by the [difference equation](@entry_id:269892) $y[n] - y[n-1] + 0.25y[n-2] = x[n] + x[n-1]$ [@problem_id:1732216]. The transfer function is found by taking the Z-transform:
$H(z) = \frac{z^2+z}{z^2 - z + 0.25}$.
The characteristic polynomial is $A(z) = z^2 - z + 0.25$. Here, $n=2$, $a_2=1$, $a_1=-1$, and $a_0=0.25$. We check the three conditions:
1.  $A(1) = 1 - 1 + 0.25 = 0.25 > 0$. Condition met.
2.  $A(-1) = 1 - (-1) + 0.25 = 2.25 > 0$. Condition met.
3.  $|a_0| = |0.25|  a_2=1$. Condition met.

Since all three conditions are satisfied, the system is BIBO stable.

This framework is particularly useful in design problems. Consider a [unity feedback](@entry_id:274594) loop with a proportional controller $C(z)=K$ and a plant $G(z) = \frac{1}{(z-0.5)(z+0.2)}$ [@problem_id:1732206]. The closed-loop characteristic polynomial is $A(z) = (z-0.5)(z+0.2) + K = z^2 - 0.3z + (K-0.1)$. Here, $a_2=1$, $a_1=-0.3$, and $a_0 = K-0.1$. Applying the stability conditions to find the stable range for $K>0$:
1.  $A(1) = 1 - 0.3 + K - 0.1 = K + 0.6 > 0 \implies K > -0.6$.
2.  $A(-1) = 1 - (-0.3) + K - 0.1 = K + 1.2 > 0 \implies K > -1.2$.
3.  $|a_0|  a_2 \implies |K-0.1|  1 \implies -1  K-0.1  1 \implies -0.9  K  1.1$.

To satisfy all conditions for $K>0$, we must have $0  K  1.1$. This demonstrates how the Jury test provides direct constraints on design parameters.

When a system approaches instability, it means its poles are moving towards the unit circle. The specific boundary of the [stability region](@entry_id:178537) that is crossed determines the nature of the instability [@problem_id:1732201].
-   **Monotonic Instability**: A pole crosses the unit circle at $z=+1$. This occurs when $A(1) = 0$.
-   **Oscillatory Instability**: This can happen in two ways. A real pole crosses at $z=-1$, which corresponds to the boundary $A(-1)=0$. Alternatively, a pair of complex-[conjugate poles](@entry_id:166341) crosses the unit circle at $z = e^{\pm j\theta}$, which corresponds to the boundary $|a_0| = a_2$.

### The General Jury Array for Higher-Order Systems

For polynomials of degree $n > 2$, satisfying the three preliminary conditions is not enough. The full Jury test requires the construction of a table, known as the **Jury array**, which systematically reduces the order of the problem at each step.

The array is built from the coefficients of $A(z) = a_n z^n + \dots + a_0$ (with $a_n>0$). The first two rows are formed directly from the coefficients:

| Row | $z^0$ | $z^1$ | $\dots$ | $z^{n-1}$ | $z^n$ |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | $a_0$ | $a_1$ | $\dots$ | $a_{n-1}$ | $a_n$ |
| 2 | $a_n$ | $a_{n-1}$ | $\dots$ | $a_1$ | $a_0$ |

Subsequent rows are calculated in pairs. The third row, with coefficients $b_k$, is of length $n$ and is calculated as:
$$b_k = \det \begin{pmatrix} a_0  a_{n-k} \\ a_n  a_k \end{pmatrix} \quad \text{for } k=0, 1, \dots, n-1$$
The fourth row is the reverse of the third row:

| Row | $z^0$ | $z^1$ | $\dots$ | $z^{n-1}$ |
| :--- | :--- | :--- | :--- | :--- |
| 3 | $b_0$ | $b_1$ | $\dots$ | $b_{n-1}$ |
| 4 | $b_{n-1}$ | $b_{n-2}$ | $\dots$ | $b_0$ |

This process is repeated, creating a new set of coefficients ($c_0, \dots, c_{n-2}$) from the $b_k$ coefficients, until a row with only three elements is generated.
$$c_k = \det \begin{pmatrix} b_0  b_{n-1-k} \\ b_{n-1}  b_k \end{pmatrix} \quad \text{for } k=0, 1, \dots, n-2$$

The complete set of stability conditions for an $n$-th order polynomial is:
1. $A(1)>0$
2. $(-1)^n A(-1) > 0$
3. And the following constraints derived from the Jury array:
    $|a_0|  a_n$
    $|b_0| > |b_{n-1}|$
    $|c_0| > |c_{n-2}|$
    $\vdots$
    (The final condition is on the row with 3 coefficients, which becomes a simple second-order check).

If all of these conditions hold, the system is stable. If any one condition fails, the test terminates, and the system is declared unstable.

Let's analyze the polynomial $Q(z) = 2z^3 - z^2 + 3z - 1$, obtained from a system model after ensuring a positive leading coefficient [@problem_id:1732192]. Here $n=3$, $a_3=2, a_2=-1, a_1=3, a_0=-1$.
The preliminary checks $Q(1)=3>0$ and $(-1)^3 Q(-1) = 7 > 0$ are met. The first array condition is $|a_0| = |-1|  a_3=2$, which also holds. We must proceed to the next stage.
The first two rows of the Jury array are:
Row 1: $[-1, 3, -1, 2]$
Row 2: $[2, -1, 3, -1]$

The coefficients for the next row ($n-1=2$nd degree) are:
$b_0 = \det \begin{pmatrix} -1  2 \\ 2  -1 \end{pmatrix} = 1 - 4 = -3$
$b_1 = \det \begin{pmatrix} -1  -1 \\ 2  3 \end{pmatrix} = -3 - (-2) = -1$
$b_2 = \det \begin{pmatrix} -1  3 \\ 2  -1 \end{pmatrix} = 1 - 6 = -5$

The next stability condition is $|b_0| > |b_{n-1}| = |b_2|$. We check: $|-3| > |-5|$, which is $3 > 5$. This is false. The condition is violated, so the system is unstable. The analysis stops here.

A full successful run of the test can be seen for a fourth-order polynomial such as $A(z) = 10z^4 + 6z^3 + 4z^2 + 2z + 1$ [@problem_id:1732218]. After verifying the three preliminary checks, the iterative construction of the array would continue until the final condition is checked. In this case, every condition is met, confirming the system's stability.

### Interpreting Test Outcomes: Counting Unstable Poles

The Jury test can do more than give a binary stable/unstable verdict. By examining the signs of the pivotal coefficients in the array, one can determine the exact number of poles outside the unit circle. This extension is closely related to the Schur-Cohn test.

The number of roots of $A(z)$ lying outside the unit circle is equal to the number of negative values in the sequence of test quantities $P_1, P_2, \dots, P_n$, where:
$P_1 = |a_0|  a_n$
$P_2 = |b_0| > |b_{n-1}|$
$P_3 = |c_0| > |c_{n-2}|$
... and so on. A more direct method for counting roots is to inspect the signs of the first elements of each new row: $b_0, c_0, d_0, \dots$. The number of roots outside the unit circle is the number of negative values in this sequence, assuming the test is not terminated prematurely by other condition failures.

Let's apply this to count the [unstable poles](@entry_id:268645) for $A(z) = 2z^3 - z^2 - 4z + 1.5$ [@problem_id:1732220]. Here, $a_3=2, a_2=-1, a_1=-4, a_0=1.5$.
First, let's verify the main stability conditions.
1. $A(1) = 2 - 1 - 4 + 1.5 = -1.5  0$. The test fails. The system is unstable.
2. $(-1)^3 A(-1) = -(2(-1)^3 - (-1)^2 - 4(-1) + 1.5) = -(-2 - 1 + 4 + 1.5) = -2.5  0$. This test also fails.

Since the preliminary tests fail, we already know the system is unstable. To count the number of [unstable poles](@entry_id:268645), we continue with the array.
The first two rows are:
Row 1: $[1.5, -4, -1, 2]$
Row 2: $[2, -1, -4, 1.5]$

The coefficients for the next row are:
$b_0 = \det \begin{pmatrix} 1.5  2 \\ 2  1.5 \end{pmatrix} = 2.25 - 4 = -1.75$
$b_1 = \det \begin{pmatrix} 1.5  -1 \\ 2  -4 \end{pmatrix} = -6 - (-2) = -4$
$b_2 = \det \begin{pmatrix} 1.5  -4 \\ 2  -1 \end{pmatrix} = -1.5 - (-8) = 6.5$
The next polynomial is $A_2(z) = 6.5z^2 - 4z - 1.75$. Let's call its coefficients $a'_{2}, a'_{1}, a'_{0}$.
To continue, we would need $a'_2 > 0$, which is true ($6.5 > 0$). Now we form the next row based on $A_2(z)$:
$c_0 = \det \begin{pmatrix} a'_0  a'_2 \\ a'_2  a'_0 \end{pmatrix} = (a'_0)^2 - (a'_2)^2 = (-1.75)^2 - (6.5)^2 = 3.0625 - 42.25 = -39.1875$.

The sequence of first elements is $b_0 = -1.75$ and $c_0 = -39.1875$. Both are negative. This indicates there are two poles outside the unit circle. (Indeed, the roots are approximately $1.55$, $0.34$, and $-1.39$). This counting method offers powerful diagnostic information beyond a simple stability check. For instance, for a third-order polynomial where $|a_0| > |a_3|$ but $A(1)>0$ and $(-1)^3 A(-1)>0$ are satisfied, a careful analysis using Vieta's formulas and the Intermediate Value Theorem can prove that there must be exactly two poles outside the unit circle [@problem_id:1732211].

### Singular Cases and Poles on the Unit Circle

The Jury test procedure can encounter singular cases, which are not failures but indicators of poles lying exactly on the unit circle ([marginal stability](@entry_id:147657)).

A critical singular case occurs when an entire row in the Jury array becomes zero. This happens if and only if the polynomial corresponding to the *previous* row is **self-reciprocal** (or anti-self-reciprocal). A self-reciprocal polynomial has roots that occur in reciprocal pairs $(z_k, 1/z_k)$. For a root to lie on the unit circle, its conjugate is its reciprocal, $\bar{z}_k = 1/z_k$, meaning it is part of such a pair.

When this singularity occurs, the test is modified:
1.  Form an **[auxiliary polynomial](@entry_id:264690)**, $P_{aux}(z)$, from the coefficients of the last non-zero row.
2.  The roots of $P_{aux}(z)$ are precisely the roots of the original polynomial that occur in reciprocal pairs (including those on the unit circle).
3.  To check the stability of the remaining roots, one can analyze the polynomial $A(z) / P_{aux}(z)$ using a new Jury test.

Consider a system where a gain parameter $K$ can be tuned, with characteristic polynomial $A(z) = z^3 + \frac{3}{4}z^2 + Kz + \frac{1}{4}$ [@problem_id:1732217]. A singular case in the Jury array that leads to a pair of complex-[conjugate poles](@entry_id:166341) on the unit circle implies that $A(z)$ must have a factor of the form $(z^2 - (2\cos\theta)z + 1)$. By performing [polynomial division](@entry_id:151800), we can find that for $K=9/8$, the polynomial factors into $(z^2 + \frac{1}{2}z + 1)(z + \frac{1}{4})$. The roots of the quadratic factor are $-\frac{1}{4} \pm j\frac{\sqrt{15}}{4}$, which lie on the unit circle, and the root of the linear factor is $z=-1/4$, which is stable.

This procedure is powerful even for high-order systems. For the fifth-order polynomial $A(z) = 2z^5 + z^4 + 3z^3 + z - 1$ [@problem_id:1732244], the construction of the Jury array leads to a row of coefficients $[-3, -3, -6, -3, -3]$. This row is palindromic, indicating the associated polynomial is self-reciprocal. This is the row used to form the [auxiliary polynomial](@entry_id:264690) $P_{aux}(z) = -3z^4 - 3z^3 - 6z^2 - 3z - 3$. Finding the roots of $P_{aux}(z)=0$ gives $z=\pm i$ and $z = -\frac{1}{2} \pm i\frac{\sqrt{3}}{2}$. These four roots, all of which are on the unit circle, are therefore the subset of roots of the original fifth-order polynomial that cause its [marginal stability](@entry_id:147657).

In conclusion, the Jury Stability Test is a comprehensive and systematic tool. It not only provides a definitive answer regarding system stability but also offers deep insights into the number of [unstable poles](@entry_id:268645) and the locations of poles on the unit circle in cases of [marginal stability](@entry_id:147657), making it an indispensable method in the analysis and design of [discrete-time systems](@entry_id:263935).