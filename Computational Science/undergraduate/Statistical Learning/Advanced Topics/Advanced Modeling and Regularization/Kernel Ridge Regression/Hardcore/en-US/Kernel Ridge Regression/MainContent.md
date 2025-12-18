## Introduction
Kernel Ridge Regression (KRR) stands as a cornerstone of modern [statistical learning](@entry_id:269475), offering a powerful and principled framework for modeling complex, non-linear relationships in data. While linear models are fundamental, they often fall short when faced with the intricate patterns inherent in real-world phenomena. KRR elegantly addresses this gap by generalizing linear [ridge regression](@entry_id:140984) to arbitrarily complex function classes, providing a robust method that balances data fidelity with model complexity to prevent [overfitting](@entry_id:139093) and enhance generalization. This article serves as a comprehensive guide to understanding and applying KRR, from its theoretical underpinnings to its diverse practical implementations.

To build a thorough understanding, we will journey through three distinct chapters. First, in **"Principles and Mechanisms,"** we will dissect the mathematical heart of KRR, exploring the famous "kernel trick," the spectral nature of regularization, and the method's deep connections to broader mathematical and statistical concepts. Next, **"Applications and Interdisciplinary Connections"** will showcase the remarkable versatility of KRR, demonstrating how thoughtful kernel design enables its use in fields ranging from computational biology to physics and allows it to tackle unstructured data like graphs and sequences. Finally, **"Hands-On Practices"** will transition from theory to application, presenting targeted problems that challenge you to implement KRR, analyze its properties, and confront practical issues like numerical stability, solidifying your command of this essential machine learning tool.

## Principles and Mechanisms

This chapter delves into the core principles and mechanisms of Kernel Ridge Regression (KRR). We transition from the conceptual overview provided in the introduction to a rigorous examination of the method's mathematical foundations, its connections to other statistical frameworks, and the practical implications of its design. We will dissect the "kernel trick," analyze the role of regularization from a spectral viewpoint, explore the behavior of the model in modern overparameterized regimes, and connect KRR to the broader theories of Gaussian processes and Tikhonov regularization.

### From Linear Ridge Regression to the Kernel Trick

Kernel Ridge Regression can be understood as an elegant generalization of linear [ridge regression](@entry_id:140984). Recall that linear [ridge regression](@entry_id:140984) seeks to find a weight vector $w$ that minimizes the sum of squared errors on a [training set](@entry_id:636396), while penalizing the magnitude of the weights to prevent [overfitting](@entry_id:139093). When we believe the relationship between inputs and outputs is nonlinear, a common strategy is to first map the input data $x \in \mathcal{X}$ into a higher-dimensional (and possibly infinite-dimensional) feature space $\mathcal{H}$ via a feature map $\phi: \mathcal{X} \to \mathcal{H}$. In this feature space, we can then perform linear [ridge regression](@entry_id:140984).

The [objective function](@entry_id:267263) for [ridge regression](@entry_id:140984) in the feature space $\mathcal{H}$ is to find a linear function $f(x) = \langle w, \phi(x) \rangle_{\mathcal{H}}$ by minimizing the following functional over the weight vector $w \in \mathcal{H}$:
$$
J(w) = \frac{1}{n}\sum_{i=1}^n (y_i - \langle w, \phi(x_i) \rangle_{\mathcal{H}})^2 + \lambda \|w\|_{\mathcal{H}}^2
$$
Here, $\lambda > 0$ is the [regularization parameter](@entry_id:162917) that controls the trade-off between fitting the data and maintaining a small norm for the weight vector $w$. A crucial insight, formalized by the **Representer Theorem**, states that the optimal weight vector $w^*$ for this problem must lie in the linear span of the feature vectors of the training data. That is, $w^*$ can be expressed as a linear combination of the feature representations of the training points:
$$
w^* = \sum_{i=1}^n \alpha_i \phi(x_i)
$$
for some scalar coefficients $\alpha_i \in \mathbb{R}$. Intuitively, any component of $w$ that is orthogonal to this span would not affect the model's predictions on the training data (and thus would not change the loss term), but it would increase the regularization penalty $\|w\|_{\mathcal{H}}^2$. Therefore, an [optimal solution](@entry_id:171456) cannot have such a component.

Substituting this form of $w^*$ back into our prediction function $f(x)$ yields:
$$
f(x) = \langle w^*, \phi(x) \rangle_{\mathcal{H}} = \left\langle \sum_{i=1}^n \alpha_i \phi(x_i), \phi(x) \right\rangle_{\mathcal{H}} = \sum_{i=1}^n \alpha_i \langle \phi(x_i), \phi(x) \rangle_{\mathcal{H}}
$$
This expression reveals a remarkable property. The prediction at any point $x$ depends only on the inner products between the feature vectors. This motivates the definition of a **kernel function** $k(x, x')$ as the inner product in the feature space:
$$
k(x, x') = \langle \phi(x), \phi(x') \rangle_{\mathcal{H}}
$$
Using the kernel, the prediction function becomes $f(x) = \sum_{i=1}^n \alpha_i k(x_i, x)$. This formulation allows us to compute the predictions without ever explicitly defining or computing the feature map $\phi(x)$, which could be computationally infeasible or even impossible if $\mathcal{H}$ is infinite-dimensional. This powerful idea is known as the **kernel trick**.

The problem now shifts to finding the optimal coefficients $\alpha = (\alpha_1, \dots, \alpha_n)^\top$. By substituting the kernel representation into the original objective function, we can express the entire optimization problem in terms of $\alpha$ and the kernel function. Let $K$ be the $n \times n$ symmetric Gram matrix with entries $K_{ij} = k(x_i, x_j)$. The vector of predictions on the training data is given by $(K\alpha)_i = \sum_{j=1}^n k(x_i, x_j) \alpha_j = f(x_i)$, and the squared norm of the function is $\|f\|_{\mathcal{H}}^2 = \alpha^\top K \alpha$. The objective function becomes a quadratic function of $\alpha$:
$$
J(\alpha) = \frac{1}{n} \|y - K\alpha\|_2^2 + \lambda \alpha^\top K \alpha
$$
Setting the gradient with respect to $\alpha$ to zero yields the linear system of equations:
$$
(K + n\lambda I)\alpha = y
$$
where $I$ is the $n \times n$ identity matrix. Since $K$ is [positive semi-definite](@entry_id:262808) and $\lambda > 0$, the matrix $(K + n\lambda I)$ is invertible, yielding a unique solution $\alpha = (K + n\lambda I)^{-1}y$.

This entire framework, from defining a linear model in a high-dimensional feature space to solving a finite-dimensional linear system involving only the kernel matrix, constitutes Kernel Ridge Regression. Its practical implementation, however, has significant computational costs. The primary bottlenecks for a standard, exact solver are :
*   **Training Time**: Constructing the $n \times n$ matrix $K$ requires $\mathcal{O}(n^2)$ kernel evaluations. Solving the linear system for $\alpha$ typically requires $\mathcal{O}(n^3)$ time using methods like Cholesky factorization.
*   **Training Memory**: Storing the dense Gram matrix $K$ requires $\mathcal{O}(n^2)$ memory.
*   **Prediction Time**: To make a prediction for a new point $x_{new}$, one must compute $f(x_{new}) = \sum_{i=1}^n \alpha_i k(x_i, x_{new})$, which involves $\mathcal{O}(n)$ kernel evaluations.

These scaling properties make KRR computationally demanding for very large datasets, motivating research into approximation methods.

### A Spectral View of Regularization

The solution to KRR, $\hat{y} = K\alpha = K(K+\lambda' I)^{-1}y$ (where $\lambda' = n\lambda$ for the formulation above), defines a linear mapping from the observed responses $y$ to the fitted values $\hat{y}$. This mapping is encapsulated by the **[smoother matrix](@entry_id:754980)** (or [hat matrix](@entry_id:174084)) $S_{\lambda'} = K(K+\lambda' I)^{-1}$. To gain a deeper understanding of how regularization works, it is instructive to analyze this matrix through the lens of the [spectral decomposition](@entry_id:148809) of the kernel matrix $K$.

Since $K$ is a real, symmetric, and [positive semi-definite matrix](@entry_id:155265), it admits an [eigendecomposition](@entry_id:181333) $K = U\Lambda U^\top$, where $U$ is an orthogonal matrix whose columns are the eigenvectors of $K$, and $\Lambda$ is a diagonal matrix containing the corresponding non-negative eigenvalues $\lambda_1, \dots, \lambda_n$. We can express the [smoother matrix](@entry_id:754980) in this [eigenbasis](@entry_id:151409):
$$
S_{\lambda'} = (U\Lambda U^\top)(U\Lambda U^\top + \lambda'I)^{-1} = U\Lambda U^\top (U(\Lambda + \lambda'I)U^\top)^{-1} = U\Lambda(\Lambda + \lambda'I)^{-1}U^\top
$$
The matrix $\Lambda(\Lambda + \lambda'I)^{-1}$ is diagonal, with entries $\frac{\lambda_j}{\lambda_j + \lambda'}$. This provides a clear picture of the regularization mechanism: KRR projects the data vector $y$ onto the [orthonormal basis of eigenvectors](@entry_id:180262) of $K$ (as $U^\top y$), shrinks the resulting coefficients, and then transforms back to the original basis. The shrinkage factor for the $j$-th component is $\frac{\lambda_j}{\lambda_j + \lambda'}$.

This factor is always between 0 and 1. For directions corresponding to large eigenvalues $\lambda_j \gg \lambda'$, the shrinkage factor is close to 1, meaning the data's projection onto these directions is largely preserved. These directions represent stable patterns in the data where the kernel exhibits high variance. Conversely, for directions with small eigenvalues $\lambda_j \ll \lambda'$, the shrinkage factor is close to 0, effectively filtering out these components. These directions correspond to noisy or unstable patterns. Thus, the [regularization parameter](@entry_id:162917) $\lambda'$ sets a threshold for what the model considers signal versus noise in the [spectral domain](@entry_id:755169).

A useful summary statistic for the complexity of the fitted model is the **[effective degrees of freedom](@entry_id:161063)**, defined as the trace of the [smoother matrix](@entry_id:754980), $\mathrm{tr}(S_{\lambda'})$. Using the [spectral decomposition](@entry_id:148809) and the cyclic property of the trace, we find :
$$
\mathrm{tr}(S_{\lambda'}) = \mathrm{tr}\left(U\Lambda(\Lambda + \lambda'I)^{-1}U^\top\right) = \mathrm{tr}\left(\Lambda(\Lambda + \lambda'I)^{-1}\right) = \sum_{j=1}^n \frac{\lambda_j}{\lambda_j + \lambda'}
$$
Each term in the sum can be interpreted as the "degree of freedom" used for the $j$-th eigen-direction. For example, if we have $n=3$ training points and the kernel matrix has eigenvalues $\lambda_1=9, \lambda_2=3, \lambda_3=1$, setting the regularization parameter to $\lambda'=3$ results in [effective degrees of freedom](@entry_id:161063) of:
$$
\mathrm{tr}(S_{3}) = \frac{9}{9+3} + \frac{3}{3+3} + \frac{1}{1+3} = \frac{3}{4} + \frac{1}{2} + \frac{1}{4} = 1.5
$$
This value, between 0 and $n=3$, provides a measure of the model's flexibility, accounting for the regularization-induced shrinkage.

### The Ridgeless Limit, Interpolation, and Overparameterization

A topic of great interest in modern machine learning is the behavior of models in the "ridgeless" limit, i.e., as the regularization parameter $\lambda \to 0$. This regime corresponds to fitting the training data as closely as possible, often leading to exact interpolation where $f(x_i) = y_i$ for all training points.

The vector of KRR predictions on the [training set](@entry_id:636396) is $\hat{y} = K(K+\lambda' I)^{-1}y$. In the limit $\lambda' \to 0$, the behavior of this expression depends critically on whether the Gram matrix $K$ is invertible. Using the spectral decomposition $K=U\Lambda U^\top$, the limiting predictions can be written as $\hat{y} \to U \Sigma_{lim} U^\top y$, where $\Sigma_{lim}$ is a [diagonal matrix](@entry_id:637782) with entries that are 1 if $\lambda_j > 0$ and 0 if $\lambda_j = 0$. This limiting matrix is precisely the orthogonal projection operator onto the range (or [column space](@entry_id:150809)) of $K$, denoted $P_{\mathrm{range}(K)}$. Therefore, we find a general result:
$$
\lim_{\lambda \to 0} \hat{y} = P_{\mathrm{range}(K)} y
$$
This means that in the [ridgeless limit](@entry_id:635503), KRR provides a perfect interpolation of the training data (i.e., $\hat{y} = y$) if and only if the target vector $y$ lies within the range of the Gram matrix $K$ .

We can analyze this behavior in two distinct regimes:

**1. Invertible Gram Matrix ($K$ is full rank)**: This scenario occurs when the kernel function and the data points $\{x_i\}$ are such that the matrix $K$ is invertible. A common case is when using a strictly [positive definite](@entry_id:149459) kernel (like the Gaussian kernel) with distinct input points. In the context of finite-dimensional [feature maps](@entry_id:637719) $\phi: \mathcal{X} \to \mathbb{R}^d$, this occurs in the "underparameterized" or wide data regime where the number of data points is less than the feature dimension ($n  d$) and the feature vectors $\{\phi(x_i)\}_{i=1}^n$ are linearly independent .
In this case, $\mathrm{range}(K) = \mathbb{R}^n$, so any target vector $y$ can be interpolated. The limit solution is given by coefficients $\alpha_0 = K^{-1}y$, and the predictions are $\hat{y} = K\alpha_0 = y$. Furthermore, this interpolating solution is unique and possesses the smallest possible RKHS norm among all functions in $\mathcal{H}$ that pass through the training points. The norm of this minimum-norm interpolant is given by:
$$
\|f_0\|_{\mathcal{H}}^2 = \alpha_0^\top K \alpha_0 = (y^\top K^{-1}) K (K^{-1}y) = y^\top K^{-1} y
$$
This norm will be small and the solution well-behaved if the matrix $K$ is well-conditioned, meaning its [smallest eigenvalue](@entry_id:177333) is bounded away from zero.

**2. Singular Gram Matrix ($K$ is rank-deficient)**: This scenario is typical in "overparameterized" settings where the effective number of features is smaller than the number of data points ($d  n$). It also arises whenever there are linear dependencies in the data, such as having duplicated input points . For instance, if $x_1 = x_2$, the first two rows (and columns) of $K$ will be identical, making it singular. The regularization term $\lambda' I$ is crucial here, as it "shifts" the eigenvalues of $K$ by $\lambda'$, ensuring that $K+\lambda' I$ is invertible and the problem remains well-posed.
In the [ridgeless limit](@entry_id:635503) $\lambda \to 0$, interpolation is only possible for the special subset of target vectors $y$ that lie in the range of the singular matrix $K$. If this condition is met, KRR again converges to the minimum-norm interpolating solution. The norm of this solution is now given by $\|f_0\|_{\mathcal{H}}^2 = y^\top K^\dagger y$, where $K^\dagger$ is the **Moore-Penrose [pseudoinverse](@entry_id:140762)** of $K$ . The [pseudoinverse](@entry_id:140762) effectively inverts $K$ on its range and acts as zero on its [null space](@entry_id:151476). The magnitude of this norm depends on the alignment of $y$ with the eigenvectors of $K$; the norm will be smaller if the energy of $y$ is concentrated in directions corresponding to large eigenvalues of $K$.

### Broader Perspectives on Kernel Ridge Regression

The principles of KRR are deeply connected to other major frameworks in machine learning and [applied mathematics](@entry_id:170283), which provide both probabilistic and functional-analytic interpretations of the method.

#### Connection to Gaussian Processes

A powerful perspective on KRR comes from the theory of **Gaussian Processes (GPs)**, which provides a Bayesian, probabilistic approach to regression. In a GP model, we place a [prior distribution](@entry_id:141376) over functions. Specifically, we assume the true underlying function $f$ is drawn from a GP, written $f \sim \mathcal{GP}(0, k)$, meaning that for any collection of points $x_1, \dots, x_n$, the vector of function values $(f(x_1), \dots, f(x_n))$ follows a multivariate Gaussian distribution with a [zero mean](@entry_id:271600) and a covariance matrix given by the kernel matrix $K$. The observations are then modeled as noisy realizations of the function, $y_i = f(x_i) + \varepsilon_i$, where the noise $\varepsilon_i$ is typically assumed to be [independent and identically distributed](@entry_id:169067) Gaussian, $\varepsilon_i \sim \mathcal{N}(0, \sigma^2)$.

Given the training data, Bayesian inference allows us to compute the posterior distribution over the function value $f(x_\star)$ at a new test point $x_\star$. This posterior is also Gaussian. Its mean, which serves as the optimal point prediction, can be shown to be :
$$
\mathbb{E}[f(x_\star) | y] = k_\star^\top (K + \sigma^2 I)^{-1} y
$$
where $k_\star$ is the vector of kernel evaluations between the test point $x_\star$ and each training point $x_i$.

Remarkably, this expression for the GP posterior mean is identical to the KRR predictor $f(x_\star) = k_\star^\top (K + \lambda I)^{-1} y$, provided we identify the KRR [regularization parameter](@entry_id:162917) $\lambda$ with the noise variance $\sigma^2$ in the GP model. (Note: this specific correspondence $\lambda = \sigma^2$ holds when the KRR loss is the sum of squared errors, $\sum(y_i-f(x_i))^2$; if an average loss $\frac{1}{n}\sum(y_i-f(x_i))^2$ is used, the correspondence becomes $n\lambda = \sigma^2$). This profound connection establishes KRR as a non-[probabilistic method](@entry_id:197501) that yields the same point predictions as a fully Bayesian GP model. It provides a principled interpretation of the regularization parameter $\lambda$ as representing our assumption about the level of noise in the data. The GP framework also provides a posterior variance, which quantifies the uncertainty in its predictions—a feature not inherently present in the standard KRR formulation.

#### Connection to Tikhonov Regularization in Hilbert Spaces

KRR can also be viewed as a specific instance of a more general mathematical tool: **Tikhonov regularization** for solving [linear inverse problems](@entry_id:751313) in Hilbert spaces. Many problems in science and engineering can be formulated as finding an unknown function or signal $f$ from a set of indirect measurements $g$. This can be modeled as solving the operator equation $Af = g$, where $A$ is a [linear operator](@entry_id:136520). Often, this problem is ill-posed (e.g., a solution may not exist, not be unique, or be highly sensitive to noise in $g$).

Tikhonov regularization seeks a stable solution by minimizing a penalized objective:
$$
\min_{f \in \mathcal{H}} \|Af - g\|_{\mathbb{R}^m}^2 + \lambda \|f\|_{\mathcal{H}}^2
$$
where $\mathcal{H}$ is a Hilbert space of functions, $A: \mathcal{H} \to \mathbb{R}^m$ is a [bounded linear operator](@entry_id:139516) representing the measurement process, $g \in \mathbb{R}^m$ is the vector of measurements, and $\lambda \|f\|_{\mathcal{H}}^2$ is a penalty on the complexity of the solution.

A generalized [representer theorem](@entry_id:637872) shows that the solution to this problem, $f_\lambda$, lies in the range of the adjoint operator $A^*$. Specifically, $f_\lambda$ can be written as a [linear combination](@entry_id:155091) of a set of basis functions $\{h_i = A^*e_i\}_{i=1}^m$, where $\{e_i\}$ is the standard basis for $\mathbb{R}^m$ .

Standard KRR is recovered as a special case where the Hilbert space $\mathcal{H}$ is an RKHS and the operator $A$ is the **evaluation operator**, which maps a function $f$ to the vector of its values at the training points: $Af = (f(x_1), \dots, f(x_n))^\top$. In this setting, the adjoint operator maps the $i$-th basis vector $e_i$ to the kernel function centered at the $i$-th data point, $A^*e_i = k(x_i, \cdot)$. The solution thus lies in the span of $\{k(x_i, \cdot)\}_{i=1}^n$, recovering the standard form of the KRR solution. This perspective situates KRR within a vast and powerful mathematical framework for solving [ill-posed problems](@entry_id:182873), providing access to a rich body of theoretical results.

### Advanced Topics and Practical Considerations

We conclude by addressing several advanced topics that are crucial for the robust application and theoretical understanding of KRR.

#### Handling Intercepts and Global Shifts

The basic KRR formulation finds a function $f \in \mathcal{H}$ that passes through the origin in feature space, meaning it has no explicit intercept or bias term. In practice, it is often desirable to fit a model of the form $f(x) + b$. One elegant way to achieve this within the kernel framework is to modify the kernel. Consider the modified kernel $k_c(x, x') = k(x, x') + c$ for some constant $c  0$. Using this kernel is equivalent to augmenting the original [feature map](@entry_id:634540) $\phi(x)$ with an additional constant feature of value $\sqrt{c}$. This implicitly introduces an intercept term $b$ into the model, but this intercept is itself regularized with a penalty proportional to $b^2/c$.

As we take the limit $c \to \infty$, the penalty on the intercept vanishes, and the model converges to KRR with an explicit, unpenalized intercept . This limiting model has the desirable property that if the target values $y$ are shifted by a constant $\delta$, the fitted values $\hat{y}$ are also shifted by the same constant $\delta$. Using a large but finite $c$ is a common and effective practical strategy for incorporating a near-unpenalized intercept.

#### Indefinite Kernels

The theory of KRR is built upon the assumption that the [kernel function](@entry_id:145324) $k(x,x')$ is [positive semi-definite](@entry_id:262808) (a Mercer kernel), which guarantees that the Gram matrix $K$ is [positive semi-definite](@entry_id:262808) and corresponds to an inner product in some feature space. However, in some applications, one might construct a symmetric similarity matrix $K$ that is not [positive semi-definite](@entry_id:262808)—it has negative eigenvalues. Such an indefinite "kernel" does not correspond to a valid RKHS norm.

While the primal optimization problem loses its [convexity](@entry_id:138568), the dual linear system $(K + \lambda I)\alpha = y$ can often still be solved. This system has a unique solution as long as $\lambda$ is not equal to the negative of any of the eigenvalues of $K$ . To restore a proper connection to a well-posed statistical model, one can "repair" the [indefinite matrix](@entry_id:634961) $K$. Two common approaches are:
1.  **Spectral Clipping**: Perform an [eigendecomposition](@entry_id:181333) of $K=U\Lambda U^\top$ and create a new matrix $K_+ = U \max(\Lambda, 0) U^\top$ by setting all negative eigenvalues to zero. This new matrix $K_+$ is the closest [positive semi-definite matrix](@entry_id:155265) to $K$ in the Frobenius norm.
2.  **Diagonal Shift**: Add a multiple of the identity, $K_\delta = K + \delta I$, choosing $\delta$ large enough to shift all eigenvalues to be non-negative (i.e., $\delta  -\lambda_{\min}(K)$). This is equivalent to simply increasing the overall regularization parameter.

These corrections modify the problem but ensure the resulting model is a valid KRR estimator based on a true [positive semi-definite kernel](@entry_id:273817).

#### Consistency and Learning Rates

Finally, a fundamental theoretical question is: under what conditions does the KRR estimator $\hat{f}$ converge to the true underlying function $f^*$ as the number of data points $n$ increases? The answer lies in the field of [statistical learning theory](@entry_id:274291), which analyzes the trade-off between bias ([approximation error](@entry_id:138265)) and variance (sample error).

The total expected error can be decomposed as:
$$
\mathbb{E}[\|\hat{f}_\lambda - f^*\|_{L^2}^2] = \underbrace{\|f_\lambda - f^*\|_{L^2}^2}_{\text{Approximation Error}} + \underbrace{\mathbb{E}[\|\hat{f}_\lambda - f_\lambda\|_{L^2}^2]}_{\text{Sample Error}}
$$
where $f_\lambda$ is the ideal, noise-free KRR solution that would be obtained with infinite data. The approximation error measures how well the best function in our regularized model class can approximate the true function $f^*$. It decreases as $\lambda \to 0$. The sample error measures the variability of our estimator due to the finite training sample. It increases as $\lambda \to 0$.

The convergence of KRR depends on choosing a sequence of regularization parameters $\lambda_n$ that balances this trade-off. For the error to go to zero, we need $\lambda_n \to 0$ and $n\lambda_n \to \infty$ as $n \to \infty$. More precise results, known as **learning rates**, can be derived under smoothness assumptions on the true function $f^*$. For instance, if $f^*$ is assumed to have a certain degree of smoothness $r$ (formalized by a "source condition"), then the optimal choice of the regularization parameter that minimizes the [error bound](@entry_id:161921) behaves like $\lambda_n \propto n^{-\frac{1}{2r+1}}$. This leads to a convergence rate where the expected error decreases as $\mathcal{O}(n^{-\frac{2r}{2r+1}})$ . This demonstrates that KRR is not just a practical algorithm but also a principled estimation procedure with strong theoretical guarantees, whose performance depends jointly on the amount of data, the choice of regularization, and the intrinsic complexity of the function being learned. A related concept is **[algorithmic stability](@entry_id:147637)**, which ensures that small perturbations to the [training set](@entry_id:636396) (like changing one data point) lead to only small changes in the learned function. This property, which can be formally bounded , is key to ensuring that the model generalizes well from the training data to unseen data.