## Introduction
The search for eigenvalues is a fundamental task in scientific computing, yet the standard QR algorithm can be prohibitively slow, especially when eigenvalues are closely spaced. This performance bottleneck necessitates the use of acceleration techniques, known as shifts, to achieve practical convergence speeds. Among these, the Wilkinson shift stands out as a remarkably effective and elegant strategy for [symmetric matrices](@entry_id:156259), transforming a linear process into one with astonishing [cubic convergence](@entry_id:168106). This article provides a deep dive into this cornerstone of numerical linear algebra. The first chapter, "Principles and Mechanisms," will dissect the definition of the Wilkinson shift, analyze its [cubic convergence](@entry_id:168106) rate, and explain the implicit bulge-chasing technique that makes it computationally efficient. Following this, "Applications and Interdisciplinary Connections" will broaden the perspective, exploring how the shift's core ideas extend to non-symmetric problems, the SVD, and find conceptual parallels in fields like control theory and computational physics. Finally, "Hands-On Practices" offers a curated set of exercises to solidify understanding of its numerical implementation and performance benefits.

## Principles and Mechanisms

The convergence of the unshifted QR algorithm, as discussed in the preceding sections, can be impractically slow, especially when eigenvalues are close in magnitude. The transformative power of the QR iteration is truly unlocked through the use of spectral shifts. A judicious choice of shift can accelerate convergence from a linear to a quadratic or even cubic rate. In the realm of symmetric [eigenvalue problems](@entry_id:142153), the most celebrated and effective strategy is the **Wilkinson shift**. This section elucidates the definition, mechanism, and implementation of this remarkable technique.

### The Wilkinson Shift: Definition and Calculation

For a real [symmetric tridiagonal matrix](@entry_id:755732) $T \in \mathbb{R}^{n \times n}$, the goal of a shifted QR step is to select a shift $\mu$ that rapidly forces a subdiagonal entry, typically the last one, $t_{n,n-1}$, toward zero. This process, known as **deflation**, decouples the last eigenvalue and reduces the problem size. The Wilkinson shift strategy provides an exceptionally effective choice for $\mu$ based on local information within the matrix.

The Wilkinson shift is defined as the eigenvalue of the trailing $2 \times 2$ [principal submatrix](@entry_id:201119) of $T$ that is closer to the bottom-right diagonal entry, $t_{n,n}$  . Let the matrix $T$ have diagonal entries $a_1, \dots, a_n$ and subdiagonal entries $b_1, \dots, b_{n-1}$. The trailing $2 \times 2$ submatrix is:
$$
S = \begin{pmatrix} a_{n-1} & b_{n-1} \\ b_{n-1} & a_n \end{pmatrix}
$$
The eigenvalues of this submatrix, which we denote $\lambda_{\pm}$, are the roots of its [characteristic polynomial](@entry_id:150909), $\det(S - \lambda I) = 0$. This yields the quadratic equation:
$$
(\lambda - a_{n-1})(\lambda - a_n) - b_{n-1}^2 = 0
$$
Solving for $\lambda$ gives the two eigenvalues of $S$. The Wilkinson shift $\mu_W$ is then chosen as the eigenvalue that is closer in absolute value to $a_n$.

To illustrate, consider the following hypothetical submatrix :
$$
S = \begin{pmatrix} 10 & 2 \\ 2 & 1 \end{pmatrix}
$$
Here, $a_{n-1}=10$, $b_{n-1}=2$, and $a_n=1$. The characteristic equation is $(\lambda - 10)(\lambda - 1) - 4 = 0$, or $\lambda^2 - 11\lambda + 6 = 0$. The quadratic formula yields the eigenvalues:
$$
\lambda_{\pm} = \frac{11 \pm \sqrt{121 - 24}}{2} = \frac{11 \pm \sqrt{97}}{2}
$$
The two eigenvalues are $\lambda_+ \approx 10.424$ and $\lambda_- \approx 0.576$. To select the Wilkinson shift, we compare their distances to the corner entry $a_n = 1$:
$$
|\lambda_+ - 1| = \left| \frac{11 + \sqrt{97}}{2} - 1 \right| = \frac{9 + \sqrt{97}}{2} \approx 9.424
$$
$$
|\lambda_- - 1| = \left| \frac{11 - \sqrt{97}}{2} - 1 \right| = \frac{9 - \sqrt{97}}{2} \approx |-0.424| = 0.424
$$
Since $\lambda_-$ is closer to $1$, the Wilkinson shift for this step is $\mu_W = \lambda_- = \frac{11 - \sqrt{97}}{2}$.

#### A Numerically Stable Formula

While the standard quadratic formula is sufficient for theoretical discussion, its direct application in [finite-precision arithmetic](@entry_id:637673) can lead to catastrophic cancellation. This occurs when the term $b_{n-1}^2$ is very small compared to $(a_{n-1}-a_n)^2$. A more robust formulation is essential for high-quality software .

Let us rewrite the eigenvalues of $S$ by defining $\delta = (a_{n-1} - a_n)/2$. The eigenvalues are:
$$
\lambda_{\pm} = \frac{a_{n-1}+a_n}{2} \pm \sqrt{\left(\frac{a_{n-1}-a_n}{2}\right)^2 + b_{n-1}^2} = (a_n + \delta) \pm \sqrt{\delta^2 + b_{n-1}^2}
$$
The Wilkinson shift is the one closer to $a_n$, which can be expressed as:
$$
\mu_W = a_n + \delta - \operatorname{sgn}(\delta) \sqrt{\delta^2 + b_{n-1}^2}
$$
(where $\operatorname{sgn}(0)$ is conventionally taken as $+1$). This formula involves the subtraction of two nearly equal quantities if $|\delta| \gg |b_{n-1}|$, leading to a potential loss of significant digits. By rationalizing the expression for the shift increment, we arrive at a numerically stable formula:
$$
\mu_W = a_n - \frac{\operatorname{sgn}(\delta) b_{n-1}^2}{|\delta| + \sqrt{\delta^2 + b_{n-1}^2}}
$$
This form is stable because the denominator involves an addition of two non-negative terms, thus avoiding [subtractive cancellation](@entry_id:172005).

### The Mechanism of Acceleration and Convergence Rates

The remarkable efficacy of the Wilkinson shift stems from its profound connection to another fundamental iterative method: **[inverse iteration](@entry_id:634426)** . A single shifted QR step, defined by $T - \mu I = QR$ and $T_+ = RQ + \mu I$, is equivalent to the similarity transformation $T_+ = Q^T T Q$. The [orthogonal matrix](@entry_id:137889) $Q$ is implicitly related to the inverse of the shifted matrix, $(T - \mu I)^{-1}$.

The power of [inverse iteration](@entry_id:634426) lies in its ability to amplify the component of an eigenvector whose corresponding eigenvalue is closest to the shift $\mu$. The matrix $(T - \mu I)^{-1}$ has eigenvalues $(\lambda_i - \mu)^{-1}$. If $\mu$ is an excellent approximation to a specific eigenvalue $\lambda_j$, then $|\lambda_j - \mu|$ is very small, making $|(\lambda_j - \mu)^{-1}|$ enormous compared to all other $|(\lambda_i - \mu)^{-1}|$. Consequently, applying [power iteration](@entry_id:141327) to $(T - \mu I)^{-1}$ (which is the definition of [inverse iteration](@entry_id:634426)) converges with extreme [rapidity](@entry_id:265131) to the eigenvector associated with $\lambda_j$.

The Wilkinson shift provides exactly such an excellent approximation. By using the eigenvalues of the local $2 \times 2$ submatrix, it generates a guess $\mu_W$ that is, by virtue of [eigenvalue interlacing](@entry_id:180866) properties, a high-fidelity estimate for an eigenvalue of the full matrix $T$. This turns the shifted QR step into a highly accelerated implicit [inverse iteration](@entry_id:634426), causing the subdiagonal entry $b_{n-1}$ to decay at a superlinear rate.

To appreciate the improvement, let us compare the convergence rates of different shift strategies for the trailing subdiagonal entry $b_{n-1}$ :

*   **Unshifted QR ($\mu=0$)**: This method exhibits **[linear convergence](@entry_id:163614)**. The error is reduced by a constant factor at each step, which can be slow if eigenvalues have similar magnitudes.

*   **Rayleigh Quotient Shift ($\mu = a_n$)**: This choice corresponds to the Rayleigh quotient of the [basis vector](@entry_id:199546) $e_n$. It generally achieves **[quadratic convergence](@entry_id:142552)**, where $|b_{n-1}^{(k+1)}| \approx C |b_{n-1}^{(k)}|^2$. This is a major improvement over the linear rate.

*   **Wilkinson Shift**: This strategy achieves **[cubic convergence](@entry_id:168106)** under generic conditions, meaning $|b_{n-1}^{(k+1)}| \approx C |b_{n-1}^{(k)}|^3$. The number of correct digits in the result roughly triples with each iteration, leading to exceptionally fast deflation.