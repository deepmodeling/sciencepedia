## Introduction
The [ordinary least squares](@entry_id:137121) (OLS) method is a cornerstone of data analysis, providing a simple way to fit models to data by minimizing the [sum of squared errors](@entry_id:149299). However, its underlying assumption—that all errors are independent and equally distributed—is often violated in real-world scenarios where measurements have varying precision or are correlated. Furthermore, many scientific and engineering problems require that model parameters adhere to strict physical laws or other [linear constraints](@entry_id:636966). This introduces a critical knowledge gap: how can we find the best-fit parameters for a model when dealing with non-ideal data and explicit constraints?

This article addresses this challenge by providing a comprehensive exploration of weighted and [constrained least squares](@entry_id:634563) methods. It offers a graduate-level treatment of the theory and numerical practice, equipping you with the tools to handle complex, real-world estimation problems.

In the first chapter, **Principles and Mechanisms**, we will delve into the statistical foundations of [weighted least squares](@entry_id:177517), derive the normal equations, and analyze the numerical stability of different solution methods like QR factorization. We will also introduce equality constraints via Lagrange multipliers and explore robust solution strategies like the [null-space method](@entry_id:636764).

The second chapter, **Applications and Interdisciplinary Connections**, showcases the remarkable versatility of these methods. We will see how they are used to enforce physical laws in data reconciliation, deconvolve mixed signals in bioinformatics, parameterize complex force fields in computational chemistry, and serve as a foundation for advanced statistical frameworks.

Finally, the **Hands-On Practices** chapter provides an opportunity to solidify your understanding through practical exercises, tackling problems that highlight the nuances of numerical stability, constraint handling, and solution interpretation. By the end, you will have a deep appreciation for the power and elegance of this fundamental optimization framework.

## Principles and Mechanisms

This chapter delves into the fundamental principles and numerical mechanisms underpinning weighted and [constrained least squares](@entry_id:634563) problems. Building upon the introductory concepts of [ordinary least squares](@entry_id:137121) (OLS), we will explore how to optimally handle non-ideal data characteristics, such as non-uniform [measurement uncertainty](@entry_id:140024) and correlation, and how to incorporate exact [linear constraints](@entry_id:636966) into the estimation process. We will examine these problems from both statistical and numerical perspectives, deriving the core equations and analyzing the stability and efficiency of various solution methodologies.

### Weighted Least Squares

The standard linear [least squares problem](@entry_id:194621) seeks to solve an [overdetermined system](@entry_id:150489) $Ax \approx b$ by minimizing the Euclidean norm of the residual, $\|Ax - b\|_2$. This approach implicitly assumes that all components of the residual are of equal importance, which corresponds to the statistical assumption that the errors in the observations $b$ are independent and identically distributed (i.i.d.). In many scientific and engineering applications, this assumption is invalid. Some measurements may be more precise than others, or the errors in different measurements may be correlated. Weighted Least Squares (WLS) provides a rigorous framework for addressing these scenarios.

#### Statistical Foundations and the Choice of Weights

Consider the linear model $y = Ax + \varepsilon$, where $y \in \mathbb{R}^m$ is the vector of observations, $A \in \mathbb{R}^{m \times n}$ is a known model matrix, $x \in \mathbb{R}^n$ is the vector of parameters to be estimated, and $\varepsilon \in \mathbb{R}^m$ is a vector of unobserved measurement errors. In the general case, the error term $\varepsilon$ is a random vector with a mean of zero, $\mathbb{E}[\varepsilon] = 0$, and a [symmetric positive definite](@entry_id:139466) (SPD) covariance matrix $\operatorname{Cov}(\varepsilon) = \Sigma$.

When the errors are not independent and identically distributed, $\Sigma$ is not a multiple of the identity matrix, $\Sigma \neq \sigma^2 I$. This situation arises from **[heteroscedasticity](@entry_id:178415)** (unequal variances, i.e., the diagonal entries of $\Sigma$ are not all equal) and **correlation** (the off-diagonal entries of $\Sigma$ are non-zero).

To derive an [optimal estimator](@entry_id:176428) in this setting, we can appeal to the principle of **Maximum Likelihood Estimation (MLE)**. If we assume the errors follow a multivariate normal (Gaussian) distribution, $\varepsilon \sim \mathcal{N}(0, \Sigma)$, then the probability density function of the error vector is given by:
$$ p(\varepsilon) = \frac{1}{\sqrt{(2\pi)^m \det(\Sigma)}} \exp\left(-\frac{1}{2} \varepsilon^{\top} \Sigma^{-1} \varepsilon\right) $$
Given our model, the residual $r(x) = y - Ax$ is an observation of the noise $\varepsilon$. The likelihood of observing the data $y$ for a given parameter vector $x$ is thus $L(x|y) = p(y-Ax)$. Maximizing this likelihood is equivalent to minimizing the [negative log-likelihood](@entry_id:637801). The [negative log-likelihood](@entry_id:637801) is proportional to the [quadratic form](@entry_id:153497) in the exponent:
$$ (y - Ax)^{\top} \Sigma^{-1} (y - Ax) $$
This expression is the squared **Mahalanobis distance** between the observed data $y$ and the model prediction $Ax$. It generalizes the squared Euclidean distance by accounting for the covariance structure of the data. This leads to the formulation of the [weighted least squares](@entry_id:177517) problem:
$$ \min_{x} (y - Ax)^{\top} W (y - Ax) $$
From the MLE derivation, it becomes clear that the statistically optimal weight matrix is the inverse of the noise covariance matrix, $W = \Sigma^{-1}$ . Intuitively, this choice gives less weight to measurements with higher variance (and combinations of measurements with high covariance), thereby prioritizing the more reliable information in the data.

#### Prewhitening and Equivalence to Ordinary Least Squares

The WLS [objective function](@entry_id:267263), $\|y - Ax\|_W^2 = (y - Ax)^{\top} W (y - Ax)$, can be transformed into a standard OLS problem. Since the weight matrix $W$ is symmetric and [positive definite](@entry_id:149459), it admits a "square root" factorization $W = C^{\top}C$ for some [invertible matrix](@entry_id:142051) $C \in \mathbb{R}^{m \times m}$. The WLS objective can then be rewritten as:
$$ (y - Ax)^{\top} C^{\top} C (y - Ax) = (C(y - Ax))^{\top} (C(y - Ax)) = \|C(y - Ax)\|_2^2 $$
Letting $\tilde{y} = Cy$ and $\tilde{A} = CA$, the problem becomes equivalent to minimizing $\|\tilde{y} - \tilde{A}x\|_2^2$, which is a standard OLS problem for the transformed data . This transformation is known as **prewhitening** or **whitening**.

If we consider the statistical model $y = Ax + \varepsilon$ with $\operatorname{Cov}(\varepsilon) = \Sigma$, and we choose the optimal weight matrix $W=\Sigma^{-1}$, the prewhitening transformation has a profound statistical interpretation. Let $\Sigma = LL^{\top}$ be the Cholesky factorization of the covariance matrix, where $L$ is a [lower triangular matrix](@entry_id:201877). Then $\Sigma^{-1} = (LL^{\top})^{-1} = (L^{\top})^{-1}L^{-1} = (L^{-1})^{\top}L^{-1}$. We can choose our whitening matrix as $C = L^{-1}$. The transformed error term becomes $\tilde{\varepsilon} = C\varepsilon = L^{-1}\varepsilon$. The covariance of this transformed noise is:
$$ \operatorname{Cov}(\tilde{\varepsilon}) = \operatorname{Cov}(L^{-1}\varepsilon) = L^{-1} \operatorname{Cov}(\varepsilon) (L^{-1})^{\top} = L^{-1} \Sigma (L^{-1})^{\top} = L^{-1} (LL^{\top}) (L^{\top})^{-1} = I $$
The transformed model $\tilde{y} = \tilde{A}x + \tilde{\varepsilon}$ now satisfies the classic OLS assumptions: its error components are uncorrelated and have unit variance. Prewhitening thus transforms the data to a new coordinate system where standard OLS is statistically optimal .

Common choices for the matrix $C$ such that $W = C^{\top}C$ include the transpose of the Cholesky factor ($C = L^{\top}$ where $W=LL^{\top}$) or the unique [symmetric positive definite](@entry_id:139466) square root ($C = W^{1/2}$). An important numerical insight is that any two matrices $C_1$ and $C_2$ that satisfy $C_1^{\top}C_1 = W$ and $C_2^{\top}C_2 = W$ are related by an [orthogonal matrix](@entry_id:137889) $U$, such that $C_2 = UC_1$. Consequently, the singular values of the transformed data matrices $C_1 A$ and $C_2 A$ are identical, which implies that their $2$-norm condition numbers are also identical: $\kappa_2(C_1 A) = \kappa_2(C_2 A)$. The choice of whitening matrix does not affect the conditioning of the resulting OLS problem .

#### Numerical Solution Methods and Stability

Two primary approaches exist for solving the WLS problem numerically.

**1. The Normal Equations Method**

The most direct approach is to set the gradient of the WLS [objective function](@entry_id:267263) with respect to $x$ to zero. This yields the **weighted normal equations**:
$$ (A^{\top}WA)x = A^{\top}Wb $$
When $A$ has full column rank and $W$ is SPD, the matrix $A^{\top}WA$ is also SPD, and this system can be solved efficiently, for example, using a Cholesky factorization of $A^{\top}WA$.

However, this method can be numerically unstable. The core issue lies in the explicit formation of the Gram matrix $A^{\top}WA$. Let $\tilde{A} = W^{1/2}A$. The [normal equations](@entry_id:142238) matrix is $\tilde{A}^{\top}\tilde{A}$. It is a fundamental result in [numerical linear algebra](@entry_id:144418) that the condition number of this Gram matrix is the square of the condition number of $\tilde{A}$:
$$ \kappa_2(A^{\top}WA) = \kappa_2(\tilde{A}^{\top}\tilde{A}) = \kappa_2(\tilde{A})^2 = \kappa_2(W^{1/2}A)^2 $$
This squaring of the condition number can lead to a severe loss of [numerical precision](@entry_id:173145) in floating-point arithmetic  . If $\kappa_2(W^{1/2}A)$ is large (e.g., $10^8$), $\kappa_2(A^{\top}WA)$ will be on the order of $10^{16}$, which is at the limit of standard double-precision arithmetic. This makes the system computationally indistinguishable from a singular one. The process of forming the matrix product $A^{\top}WA$ can irreversibly lose information contained in the smaller singular values of $W^{1/2}A$.

**2. The Orthogonal Factorization Method**

A numerically superior approach avoids forming the normal equations altogether. It operates on the prewhitened system as described previously:
1.  Compute a factorization $W = C^{\top}C$. The Cholesky factorization $W=LL^{\top}$ is typically used, with $C=L^{\top}$.
2.  Form the transformed matrix $\tilde{A} = CA$ and vector $\tilde{b} = Cb$.
3.  Solve the standard [least squares problem](@entry_id:194621) $\min_x \|\tilde{A}x - \tilde{b}\|_2$ using a **QR factorization** of $\tilde{A}$.

This method works with the matrix $\tilde{A}$ directly, and its numerical stability is governed by $\kappa_2(\tilde{A})$, not its square. Backward error analysis shows that the [relative error](@entry_id:147538) in the computed solution from this QR-based method is typically proportional to $u\,\kappa_2(\tilde{A})$, where $u$ is the [unit roundoff](@entry_id:756332) of the machine arithmetic. In contrast, the error for the [normal equations](@entry_id:142238) method scales with $u\,\kappa_2(\tilde{A})^2$ . For this reason, the QR-based approach is generally the preferred method for its superior stability and robustness .

For problems where the matrix $A$ may be rank-deficient or nearly so, a **QR factorization with [column pivoting](@entry_id:636812) (QRCP)** should be used on $\tilde{A}$. This robust variant can reliably determine the [numerical rank](@entry_id:752818) of the problem and compute a well-behaved solution . Despite its stability issues, the [normal equations](@entry_id:142238) method can sometimes be acceptable. If the problem is known to be well-conditioned (i.e., $\kappa_2(W^{1/2}A)$ is small) and the matrix $A^{\top}WA$ has a desirable structure (e.g., sparsity) that can be exploited for a very fast Cholesky solve, it may be used for performance reasons .

The concept of **[backward error](@entry_id:746645)** formalizes numerical stability. An approximate solution $\tilde{x}$ is considered good if it is the exact solution to a nearby problem. For WLS, we can define the backward error as the smallest perturbation $(\Delta A, \Delta b)$ such that $\tilde{x}$ is an exact minimizer for the perturbed problem with data $(A+\Delta A, b+\Delta b)$. Constructing and calculating this minimal perturbation provides a quantitative measure of the quality of the computed solution $\tilde{x}$ .

#### Special Case: Semidefinite Weighting

In some scenarios, the weight matrix $W$ may be only positive semidefinite (i.e., singular), which typically occurs when some observations are to be completely ignored. In this case, the objective function $J(x) = (Ax-b)^{\top}W(Ax-b)$ is still convex, but may not be strictly convex. The Hessian matrix $H = A^{\top}WA$ will be singular if the null space of $W^{1/2}A$ is non-trivial.

Consequently, the [normal equations](@entry_id:142238) $Hx = A^{\top}Wb$ may have infinitely many solutions. The set of all minimizers forms an affine subspace of the form $x_p + \ker(H)$, where $x_p$ is any [particular solution](@entry_id:149080). This non-uniqueness arises because movements along directions in $\ker(A^{\top}WA)$ do not change the value of the [objective function](@entry_id:267263).

To obtain a unique solution, an additional criterion must be imposed. A standard choice is to select the solution with the minimum Euclidean norm, $\|x\|_2$. This unique [minimum-norm solution](@entry_id:751996) is given by the **Moore-Penrose [generalized inverse](@entry_id:749785) (MPGI)**:
$$ x^{\dagger} = (A^{\top}WA)^{\dagger} A^{\top}Wb $$
This is equivalent to imposing an additional constraint that the solution must be orthogonal to the [null space](@entry_id:151476) of $A^{\top}WA$ .

### Equality-Constrained Least Squares

We now turn to problems where the parameters $x$ must satisfy a set of [linear equality constraints](@entry_id:637994), such as $Cx=d$. This leads to the general equality-[constrained least squares](@entry_id:634563) problem.

#### KKT Conditions and Solution Methods

The general problem is to find $x \in \mathbb{R}^n$ that solves:
$$ \min_{x} \frac{1}{2} \|Ax-b\|_W^2 \quad \text{subject to} \quad Cx=d $$
where $W$ is SPD, $C \in \mathbb{R}^{p \times n}$ has full row rank, and the feasible set $\{x | Cx=d\}$ is non-empty. As this is a convex optimization problem with a strictly convex objective and affine constraints, a unique solution is guaranteed to exist.

The most fundamental approach to solving this problem is the method of **Lagrange multipliers**. We form the Lagrangian:
$$ \mathcal{L}(x, \lambda) = \frac{1}{2} (Ax-b)^{\top}W(Ax-b) + \lambda^{\top}(d - Cx) $$
Here, $\lambda \in \mathbb{R}^p$ is the vector of Lagrange multipliers. The [optimal solution](@entry_id:171456) $(x, \lambda)$ must satisfy the Karush-Kuhn-Tucker (KKT) conditions, which are obtained by setting the gradients of $\mathcal{L}$ with respect to $x$ and $\lambda$ to zero:
\begin{align*} \nabla_x \mathcal{L} = A^{\top}W(Ax-b) - C^{\top}\lambda = 0 \\ \nabla_\lambda \mathcal{L} = d - Cx = 0 \end{align*}
Rearranging these gives the symmetric but indefinite block linear system, often called the **KKT system** or saddle-point system:
$$ \begin{pmatrix} A^{\top}WA & C^{\top} \\ C & 0 \end{pmatrix} \begin{pmatrix} x \\ -\lambda \end{pmatrix} = \begin{pmatrix} A^{\top}Wb \\ -d \end{pmatrix} $$
Directly solving this $(n+p) \times (n+p)$ system is one option. However, more common are elimination methods that exploit the structure of the problem. Two primary elimination strategies exist: the [null-space method](@entry_id:636764) and the [range-space method](@entry_id:634702).

#### The Null-Space Method

The [null-space method](@entry_id:636764) transforms the constrained problem into a smaller, unconstrained one. The core idea is to parameterize the affine feasible set $\{x | Cx=d\}$. Any [feasible solution](@entry_id:634783) can be expressed as:
$$ x = x_p + Zv $$
where $x_p$ is any [particular solution](@entry_id:149080) satisfying $Cx_p=d$, and the columns of the matrix $Z \in \mathbb{R}^{n \times (n-p)}$ form a basis for the null space of $C$ (i.e., $CZ=0$). The vector $v \in \mathbb{R}^{n-p}$ freely parameterizes all possible movements away from $x_p$ that maintain feasibility.

Substituting this [parameterization](@entry_id:265163) into the WLS objective gives an unconstrained problem in terms of $v$:
$$ \min_{v} \|A(x_p + Zv) - b\|_W^2 = \min_{v} \|(AZ)v - (b - Ax_p)\|_W^2 $$
This is a WLS problem of size $m \times (n-p)$, which can be solved for $v$ using the numerically stable QR-based methods discussed earlier. Once the optimal $v^{\star}$ is found, the solution to the original problem is recovered as $x^{\star} = x_p + Zv^{\star}$ . This method is numerically robust but requires computing a basis for the [null space](@entry_id:151476) of $C$, which can be computationally intensive if $n-p$ is large.

#### The Range-Space Method

The [range-space method](@entry_id:634702), also known as the Schur complement method, is an alternative elimination strategy that is particularly effective when the number of constraints $p$ is small ($p \ll n$). Starting from the KKT system, we first solve the top block equation for $x$:
$$ x = (A^{\top}WA)^{-1}(A^{\top}Wb + C^{\top}\lambda) $$
We then substitute this expression into the constraint equation $Cx=d$:
$$ C(A^{\top}WA)^{-1}(A^{\top}Wb + C^{\top}\lambda) = d $$
Rearranging yields a linear system for the Lagrange multipliers $\lambda$:
$$ \left( C(A^{\top}WA)^{-1}C^{\top} \right) \lambda = d - C(A^{\top}WA)^{-1}A^{\top}Wb $$
The matrix $S = C(A^{\top}WA)^{-1}C^{\top}$ is the **Schur complement** of the $A^{\top}WA$ block in the KKT matrix. Under the standard assumptions that $A$ has full column rank and $C$ has full row rank, this $p \times p$ Schur complement matrix is symmetric and [positive definite](@entry_id:149459). We can solve this smaller system for $\lambda$ and then substitute back to find $x$.

Numerically, the explicit formation of $(A^{\top}WA)^{-1}$ should be avoided. Instead, to solve for $\lambda$, one typically uses factorizations of $A^{\top}WA$. For instance, if one wishes to use an iterative solver like the Conjugate Gradient method on the Schur [complement system](@entry_id:142643), matrix-vector products of the form $Sv$ can be computed "matrix-free" by performing a sequence of matrix-vector products and a solve with $A^{\top}WA$ . The [range-space method](@entry_id:634702) is efficient when $p \ll n$, but its stability can suffer if the constraint matrix $C$ is ill-conditioned, as this can lead to an ill-conditioned Schur complement $S$ .

#### A Special Case: Minimum Weighted-Norm Solutions

An important application of constrained optimization is finding the solution to an [underdetermined system](@entry_id:148553) $Ax=b$ (where $m  n$) that has the smallest norm. If we define "smallest" using a weighted norm $\|x\|_W = \sqrt{x^{\top}Wx}$ induced by an SPD matrix $W$, the problem becomes:
$$ \min_{x} x^{\top}Wx \quad \text{subject to} \quad Ax=b $$
This is a special case of the equality-constrained WLS problem where the objective matrix is $W$ and the "data matrix" in the objective is the identity. The method of Lagrange multipliers yields the KKT system:
$$ \begin{pmatrix} 2W  A^{\top} \\ A  0 \end{pmatrix} \begin{pmatrix} x \\ \lambda \end{pmatrix} = \begin{pmatrix} 0 \\ b \end{pmatrix} $$
Solving this system gives the unique minimizer $x^{\star} = W^{-1}A^{\top}(AW^{-1}A^{\top})^{-1}b$. Geometrically, the choice of $W$ redefines the notion of distance and orthogonality. The solution is the point in the feasible affine subspace $\{x | Ax=b\}$ that is "closest" to the origin, where closeness is measured in the geometry induced by $W$. Changing $W$ from, say, the identity matrix to a [diagonal matrix](@entry_id:637782) with non-uniform entries alters the shape of the [level sets](@entry_id:151155) of the objective function from spheres to ellipsoids, thereby changing which point on the feasible set is selected as the minimizer .