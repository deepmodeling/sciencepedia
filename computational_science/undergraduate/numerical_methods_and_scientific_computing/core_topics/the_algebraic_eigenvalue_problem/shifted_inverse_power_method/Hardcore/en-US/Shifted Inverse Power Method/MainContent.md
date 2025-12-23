## Introduction
While standard numerical techniques excel at finding the largest or smallest eigenvalues of a matrix, many critical problems in science and engineering require targeting specific *interior* eigenvalues. For example, how can we determine if a bridge has a [resonant frequency](@entry_id:265742) near that of common wind patterns, or find a [specific energy](@entry_id:271007) level in a quantum system? The inability of basic methods to answer such questions represents a significant knowledge gap.

The **Shifted Inverse Power Method** is a powerful and elegant algorithm designed precisely to fill this gap. It provides a "spectral searchlight" to find the eigenvalue-eigenvector pair closest to any user-specified target value. This article provides a comprehensive exploration of this essential numerical tool.

In the following sections, you will embark on a journey from theory to application. In **Principles and Mechanisms**, we will deconstruct the core "[shift-and-invert](@entry_id:141092)" strategy, explaining how it transforms the problem and detailing the practical iterative algorithm. Then, **Applications and Interdisciplinary Connections** will showcase the method's versatility by exploring its use in diverse fields like [structural engineering](@entry_id:152273), quantum chemistry, and machine learning. Finally, **Hands-On Practices** will provide you with practical exercises to solidify your understanding and implement the method for real-world scenarios. By the end, you will have a thorough grasp of not just how the shifted [inverse power method](@entry_id:148185) works, but also why it is a cornerstone of modern scientific computing.

## Principles and Mechanisms

While the standard power and inverse power methods provide robust tools for finding the extremal eigenvalues of a matrix, many scientific and engineering problems require knowledge of [interior eigenvalues](@entry_id:750739)—those that are neither the largest nor the smallest in magnitude. For instance, in structural engineering, one might be interested in a specific resonant frequency of a structure that is not the fundamental (lowest) or highest frequency . Similarly, in quantum mechanics, one may need to compute an energy level of a system that is close to a particular experimental value. The **shifted [inverse power method](@entry_id:148185)** is a powerful and versatile extension of the [inverse power method](@entry_id:148185) designed precisely for this task: finding the eigenvalue-eigenvector pair $(\lambda, v)$ where the eigenvalue $\lambda$ is closest to a user-specified target value, or **shift**, $\sigma$.

### The Core Principle: The Shift-and-Invert Transformation

The genius of the shifted [inverse power method](@entry_id:148185) lies in a simple yet profound transformation of the original eigenvalue problem, $Av = \lambda v$. The strategy is to manipulate the matrix $A$ in such a way that the desired eigenvalue, which is "hidden" in the interior of the spectrum, becomes the [dominant eigenvalue](@entry_id:142677) of a new, related matrix. This allows us to apply the logic of the standard power method to find it. The transformation consists of two steps: a "shift" followed by an "inversion."

Let us consider a matrix $A$ with eigenvalues $\{\lambda_1, \lambda_2, \ldots, \lambda_n\}$ and a corresponding set of eigenvectors $\{v_1, v_2, \ldots, v_n\}$.

1.  **The Shift:** We select a scalar shift $\sigma$ that we believe is close to our target eigenvalue. We then form a new matrix, $A - \sigma I$, where $I$ is the identity matrix. The effect of this shift on the eigenvalues is straightforward to determine. If $Av_i = \lambda_i v_i$, then:
    $$(A - \sigma I)v_i = Av_i - \sigma I v_i = \lambda_i v_i - \sigma v_i = (\lambda_i - \sigma)v_i$$
    This demonstrates that the matrix $A - \sigma I$ has the same eigenvectors $v_i$ as the original matrix $A$, but its eigenvalues are now $\{\lambda_1 - \sigma, \lambda_2 - \sigma, \ldots, \lambda_n - \sigma\}$. The entire spectrum of $A$ has been shifted by $-\sigma$.

2.  **The Inversion:** Next, we take the inverse of the shifted matrix, forming $(A - \sigma I)^{-1}$. This step is only possible if $A - \sigma I$ is invertible, which means $\sigma$ cannot be exactly equal to one of the eigenvalues $\lambda_i$. We will return to this important condition later. A fundamental property of matrix inverses is that if a matrix $M$ has an eigenvalue $\mu$ with eigenvector $v$, its inverse $M^{-1}$ has the same eigenvector $v$ with eigenvalue $1/\mu$. Applying this to our shifted matrix $M = A - \sigma I$, we find:
    $$(A - \sigma I)^{-1}v_i = \frac{1}{\lambda_i - \sigma} v_i$$
    This is the central relationship of the method. The "[shift-and-invert](@entry_id:141092)" matrix, $B = (A - \sigma I)^{-1}$, has the same eigenvectors as $A$, and its eigenvalues are given by $\mu_i = \frac{1}{\lambda_i - \sigma}$ .

Now, consider what happens when we apply the standard [power method](@entry_id:148021) to our new matrix $B$. The power method converges to the eigenvector corresponding to the eigenvalue with the largest absolute value. The largest eigenvalue of $B$, let's call it $\mu_{dom}$, is the one for which $|\mu_i| = \left|\frac{1}{\lambda_i - \sigma}\right|$ is maximized. Maximizing this fraction is equivalent to minimizing its denominator, $|\lambda_i - \sigma|$.

Therefore, the [power method](@entry_id:148021) applied to $(A - \sigma I)^{-1}$ will converge to the eigenvector $v_j$ corresponding to the eigenvalue $\lambda_j$ of the original matrix $A$ that is **closest** to the shift $\sigma$. This elegantly transforms the problem of finding an interior eigenvalue into a problem of finding a dominant one. The standard [inverse power method](@entry_id:148185) can be seen as a special case of this method where the shift is chosen as $\sigma=0$, thereby finding the eigenvalue closest to zero (i.e., the one with the smallest magnitude) .

For example, if a matrix $A$ has eigenvalues $\{7, 2, -1\}$ and we choose a shift $\sigma=2.2$, the distances from the shift are $|7-2.2|=4.8$, $|2-2.2|=0.2$, and $|-1-2.2|=3.2$. The minimum distance is $0.2$, corresponding to the eigenvalue $\lambda=2$. The shifted [inverse power method](@entry_id:148185) will thus converge to the eigenpair associated with $\lambda=2$, whereas the standard [inverse power method](@entry_id:148185) (with $\sigma=0$) would converge to the eigenpair for $\lambda=-1$ since $|-1|$ is the minimum absolute value  .

### A Geometric Perspective on Convergence

To gain a deeper intuition for why the method works, we can analyze the geometric action of a single iteration. An arbitrary starting vector $x_k$ can be expressed as a [linear combination](@entry_id:155091) of the eigenvectors of $A$ (assuming $A$ is diagonalizable):
$$x_k = \sum_{i=1}^n c_i v_i$$
One iteration of the (unnormalized) shifted [inverse power method](@entry_id:148185) computes the next vector $x_{k+1}$ as:
$$x_{k+1} = (A - \sigma I)^{-1} x_k = (A - \sigma I)^{-1} \left(\sum_{i=1}^n c_i v_i\right)$$
By linearity, we can distribute the matrix operator:
$$x_{k+1} = \sum_{i=1}^n c_i \left((A - \sigma I)^{-1} v_i\right) = \sum_{i=1}^n c_i \left(\frac{1}{\lambda_i - \sigma} v_i\right) = \sum_{i=1}^n \left(\frac{c_i}{\lambda_i - \sigma}\right) v_i$$
This result is profoundly illustrative. In the coordinate system defined by the eigenvectors, a single iteration is simply a **coordinate-wise scaling**. The component of the vector along each eigenvector $v_i$ is scaled by the factor $\frac{1}{\lambda_i - \sigma}$.

Let's say our target eigenvalue is $\lambda_j$, which is much closer to $\sigma$ than any other eigenvalue $\lambda_i$. This means the denominator $|\lambda_j - \sigma|$ is very small, and consequently, the scaling factor $\frac{1}{\lambda_j - \sigma}$ is very large in magnitude. For all other components, the denominators $|\lambda_i - \sigma|$ are larger, making their scaling factors smaller.

Geometrically, each iteration dramatically amplifies the component of the vector in the direction of the desired eigenvector $v_j$, while simultaneously attenuating all other components. After a few iterations, the vector $x_k$ becomes almost perfectly aligned with $v_j$, effectively isolating it from all other eigenvectors .

### The Shifted Inverse Power Algorithm

The theoretical principle relies on applying the [power method](@entry_id:148021) to the matrix $B = (A - \sigma I)^{-1}$. In practice, explicitly computing the [inverse of a matrix](@entry_id:154872) is a computationally expensive and numerically unstable operation that should almost always be avoided.

Instead of computing $y_{k+1} = (A - \sigma I)^{-1} x_k$, we rearrange this equation into the equivalent linear system:
$$(A - \sigma I) y_{k+1} = x_k$$
We then solve this system for the vector $y_{k+1}$ using a robust and efficient linear solver. This is the heart of the practical algorithm. For a fixed shift $\sigma$, the matrix $A - \sigma I$ remains constant throughout the iteration. This allows for significant optimization. For instance, one can compute the LU decomposition of $A - \sigma I$ once, before the iterations begin. Then, in each step, solving for $y_{k+1}$ only requires a much faster forward and [backward substitution](@entry_id:168868).

The complete iterative procedure is as follows :
Given a matrix $A$, a shift $\sigma$, an initial non-zero random vector $x_0$, and a tolerance $\tau$.

1.  **Setup (Optional but Recommended):** Compute the LU factorization of the matrix $A - \sigma I$.
2.  **Iteration Loop:** For $k=1, 2, 3, \ldots$
    a.  **Solve:** Solve the linear system $(A - \sigma I) y_k = x_{k-1}$ for the vector $y_k$.
    b.  **Normalize:** Compute the next eigenvector approximation by normalizing: $x_k = \frac{y_k}{\|y_k\|}$.
    c.  **Estimate Eigenvalue:** Compute the Rayleigh quotient to get an estimate of the eigenvalue: $\lambda_k = x_k^T A x_k$.
    d.  **Check Convergence:** If the change in $\lambda_k$ or $x_k$ is below the tolerance $\tau$, stop and return $(\lambda_k, x_k)$.

### A Numerical Example

Let's perform a single iteration to solidify the process. Consider the matrix $A = \begin{pmatrix} 3 & -1 & -1 \\ -1 & 3 & -1 \\ -1 & -1 & 3 \end{pmatrix}$ and suppose we want to find the eigenvalue closest to the shift $\sigma = 5$. We start with an initial vector $x_0 = \begin{pmatrix} 1 \\ 0 \\ 0 \end{pmatrix}$ .

**Step 1: Form the shifted matrix and the linear system.**
The shifted matrix is $A - \sigma I = \begin{pmatrix} 3 & -1 & -1 \\ -1 & 3 & -1 \\ -1 & -1 & 3 \end{pmatrix} - 5 \begin{pmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix} = \begin{pmatrix} -2 & -1 & -1 \\ -1 & -2 & -1 \\ -1 & -1 & -2 \end{pmatrix}$.
The linear system to solve is $(A - 5I)y_1 = x_0$:
$$\begin{pmatrix} -2 & -1 & -1 \\ -1 & -2 & -1 \\ -1 & -1 & -2 \end{pmatrix} y_1 = \begin{pmatrix} 1 \\ 0 \\ 0 \end{pmatrix}$$

**Step 2: Solve the system for $y_1$.**
Solving this system of equations yields the vector $y_1 = \begin{pmatrix} -3/4 \\ 1/4 \\ 1/4 \end{pmatrix}$.

**Step 3: Estimate the eigenvalue.**
The vector $y_1$ is an approximation of the eigenvector of $(A-5I)^{-1}$. The corresponding eigenvalue, $\mu$, is approximately given by the Rayleigh quotient $\frac{x_0^T y_1}{x_0^T x_0}$.
$$\mu \approx \frac{\begin{pmatrix} 1 & 0 & 0 \end{pmatrix} \begin{pmatrix} -3/4 \\ 1/4 \\ 1/4 \end{pmatrix}}{\begin{pmatrix} 1 & 0 & 0 \end{pmatrix} \begin{pmatrix} 1 \\ 0 \\ 0 \end{pmatrix}} = \frac{-3/4}{1} = -\frac{3}{4}$$
This is our estimate for the largest eigenvalue of $(A-5I)^{-1}$. To find the corresponding eigenvalue $\lambda$ of $A$, we use the relationship $\mu \approx \frac{1}{\lambda - \sigma}$:
$$\lambda \approx \sigma + \frac{1}{\mu} = 5 + \frac{1}{-3/4} = 5 - \frac{4}{3} = \frac{11}{3}$$
After just one iteration, our estimate for the eigenvalue of $A$ closest to $5$ is $\frac{11}{3} \approx 3.667$. The actual eigenvalues of this matrix are $1, 4, 4$, so our target is $\lambda=4$. Our initial estimate is already reasonably close. Subsequent iterations would refine both the eigenvector and this eigenvalue estimate.

### Analysis of Convergence and Practical Considerations

#### Rate of Convergence

The asymptotic [rate of convergence](@entry_id:146534) of the shifted [inverse power method](@entry_id:148185) is determined by the separation of the [dominant eigenvalue](@entry_id:142677) of the transformed matrix $B = (A - \sigma I)^{-1}$ from the others. Let $\lambda_*$ be the eigenvalue of $A$ closest to $\sigma$, and let $\lambda_{next}$ be the second-closest eigenvalue. The corresponding eigenvalues of $B$ with the largest and second-largest magnitudes will be $\mu_* = \frac{1}{\lambda_* - \sigma}$ and $\mu_{next} = \frac{1}{\lambda_{next} - \sigma}$.

The convergence rate is governed by the ratio of these magnitudes:
$$R = \left| \frac{\mu_{next}}{\mu_*} \right| = \left| \frac{1/(\lambda_{next} - \sigma)}{1/(\lambda_* - \sigma)} \right| = \frac{|\lambda_* - \sigma|}{|\lambda_{next} - \sigma|}$$
A smaller ratio $R$ implies faster convergence. This formula reveals two key insights :
1.  **Proximity of Shift:** To accelerate convergence, we should choose $\sigma$ as close as possible to our target eigenvalue $\lambda_*$. This makes the numerator $|\lambda_* - \sigma|$ very small.
2.  **Eigengap:** The method converges faster if the target eigenvalue $\lambda_*$ is well-separated from other eigenvalues. A large "eigengap" $|\lambda_{next} - \sigma|$ makes the denominator large, leading to a small $R$.

For example, if we wish to find $\lambda_*=3$ for a matrix with other eigenvalues at $-2$ and $10$, a shift of $\sigma_1=3.2$ gives a convergence factor of $\frac{|3-3.2|}{|-2-3.2|} = \frac{0.2}{5.2} \approx 0.038$. A shift of $\sigma_2=2.5$ gives a factor of $\frac{|3-2.5|}{|-2-2.5|} = \frac{0.5}{4.5} \approx 0.111$. The first shift, being closer to the target, provides significantly faster convergence .

#### Pathological Cases and Algorithmic Failure

The formulation of the method carries assumptions that can fail in practice, leading to computational difficulties.

First, as previously mentioned, the shift $\sigma$ cannot be exactly equal to an eigenvalue of $A$. If $\sigma = \lambda_j$ for some $j$, the matrix $A - \sigma I$ has a zero eigenvalue, meaning it is **singular** and its inverse does not exist. Computationally, this means the linear system $(A - \sigma I) y_k = x_{k-1}$ is ill-posed; it may have no solution or infinitely many solutions, and any standard numerical solver will fail .

Second, a more subtle issue arises when the shift $\sigma$ is nearly equidistant from two distinct eigenvalues, say $\lambda_p$ and $\lambda_{p+1}$. This situation implies that $|\lambda_p - \sigma| \approx |\lambda_{p+1} - \sigma|$. In this case, the convergence factor $R = \frac{|\lambda_p - \sigma|}{|\lambda_{p+1} - \sigma|}$ will be very close to $1$, leading to extremely slow convergence. The algorithm will struggle to distinguish between the two competing eigenvectors $v_p$ and $v_{p+1}$. In the exact but illustrative case where $\sigma$ is perfectly halfway between them (i.e., $\sigma = (\lambda_p+\lambda_{p+1})/2$), the two dominant eigenvalues of the transformed matrix have equal magnitude but opposite sign. This can cause the iterates $x_k$ to fail to converge to a single vector, instead oscillating between two directions in the subspace spanned by $\{v_p, v_{p+1}\}$ . In practice, the iteration will first rapidly project the vector onto the two-dimensional subspace $\text{span}\{v_p, v_{p+1}\}$ and then very slowly resolve the competition between the two modes .

#### The Dilemma of Choosing an Optimal Shift

The analysis of the convergence rate suggests a simple strategy: pick $\sigma$ as close to the target eigenvalue $\lambda_*$ as possible. However, this advice comes with a significant practical caveat, creating a fundamental trade-off in the algorithm's application.

As $\sigma$ approaches $\lambda_*$, the matrix $A - \sigma I$ approaches a singular matrix. In [finite-precision arithmetic](@entry_id:637673), this means the matrix becomes increasingly **ill-conditioned**. The condition number $\kappa(A - \sigma I)$—a measure of how sensitive the solution of a linear system is to perturbations—grows very large, scaling as $1/|\sigma - \lambda_*|$.

This leads to a dilemma :
*   **Fast Convergence:** A small $|\sigma - \lambda_*|$ leads to a small convergence ratio $R$, meaning we need fewer outer iterations to reach a desired accuracy.
*   **Costly Iterations:** A small $|\sigma - \lambda_*|$ leads to a large condition number $\kappa(A - \sigma I)$. Solving the linear system for such an [ill-conditioned matrix](@entry_id:147408) is computationally expensive and numerically unstable, especially if an [iterative linear solver](@entry_id:750893) is used. Each iteration takes more work and is more susceptible to [floating-point](@entry_id:749453) errors.

Therefore, choosing a shift is not simply a matter of getting as close as possible to the target. There exists an optimal shift distance $\delta^* = |\sigma - \lambda_*|$ that balances the decreasing number of required iterations with the increasing cost per iteration. Finding this exact optimum can be complex, but understanding this trade-off is crucial for the effective use of the shifted [inverse power method](@entry_id:148185). A shift that is "close, but not too close" is often the most practical choice. This has led to the development of more advanced adaptive methods, such as Rayleigh Quotient Iteration, where the shift $\sigma$ is dynamically updated in each step to be the current best estimate of the eigenvalue, a topic we will explore in a later chapter.