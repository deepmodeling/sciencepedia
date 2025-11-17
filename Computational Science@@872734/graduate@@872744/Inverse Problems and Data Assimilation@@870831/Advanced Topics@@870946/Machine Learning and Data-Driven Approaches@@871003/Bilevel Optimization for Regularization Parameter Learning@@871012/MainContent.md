## Introduction
The selection of regularization parameters is a critical and often challenging step in solving [inverse problems](@entry_id:143129) and building machine learning models. A poorly chosen parameter can lead to models that either fail to capture the underlying structure of the data or overfit to noise. While manual tuning and [grid search](@entry_id:636526) are common, they are often heuristic, computationally expensive, and lack a rigorous theoretical foundation. This article addresses this gap by presenting a systematic and powerful alternative: [bilevel optimization](@entry_id:637138) for automatically learning regularization parameters from data.

This approach reframes hyperparameter selection as a nested optimization problem, where an outer problem seeks to optimize for generalization performance on a validation set, while an inner problem solves for the model parameters on a training set. Over the following chapters, you will gain a comprehensive understanding of this elegant framework. We will begin in "Principles and Mechanisms" by deriving the mathematical machinery, including the [hypergradient](@entry_id:750478), that powers this method. Next, "Applications and Interdisciplinary Connections" will showcase its versatility across a vast landscape of scientific and engineering challenges, from medical imaging to weather forecasting. Finally, "Hands-On Practices" will provide concrete exercises to translate theory into practical coding skills. By the end, you will be equipped to apply [bilevel optimization](@entry_id:637138) to enhance the robustness and performance of your own models.

## Principles and Mechanisms

This chapter delves into the core principles and mechanisms underpinning the learning of regularization parameters via [bilevel optimization](@entry_id:637138). We will transition from the conceptual framework to the mathematical machinery required for its implementation, exploring both theoretical foundations and practical computational strategies. Our focus will be on deriving the essential tool for this process—the **[hypergradient](@entry_id:750478)**—and understanding its computation in various settings.

### The Bilevel Optimization Framework

The automatic selection of hyperparameters, such as the regularization parameter in an [inverse problem](@entry_id:634767), represents a classic challenge in statistical modeling and machine learning. A naive choice might involve tuning the parameter to minimize the error on the same data used for [model fitting](@entry_id:265652). However, this approach inevitably leads to **[overfitting](@entry_id:139093)** the hyperparameter, typically by selecting a value that under-regularizes the model, thereby fitting the noise in the training data too closely.

A more principled approach is to formulate the task as a **[bilevel optimization](@entry_id:637138) problem**. This framework formalizes the idea of tuning hyperparameters based on their out-of-sample performance. It consists of two nested optimization problems: an **inner problem** (or lower-level problem) and an **outer problem** (or upper-level problem).

*   The **inner problem** corresponds to the standard model-fitting process. For a *fixed* value of a hyperparameter $\lambda$, we solve for the model parameters that best fit the **training data**.
*   The **outer problem** aims to find the optimal hyperparameter $\lambda$ by minimizing a loss function that evaluates the performance of the inner solution on an independent **validation dataset**.

Let's formalize this for a typical linear [inverse problem](@entry_id:634767). Suppose we have a set of training observations $y_{\mathrm{tr}}$ and a set of validation observations $y_{\mathrm{val}}$. For a given [regularization parameter](@entry_id:162917) $\lambda$, the inner problem seeks an estimate $u_{\lambda}$ by solving a Tikhonov-regularized objective:
$$
u_{\lambda} \in \arg\min_{u \in \mathbb{R}^{n}} \left( \frac{1}{2} \left\| A u - y_{\mathrm{tr}} \right\|_{R^{-1}}^{2} + \frac{\lambda}{2} \left\| L u \right\|_{2}^{2} \right).
$$
Here, $A$ is the forward operator, $L$ is a regularization operator, and the term $\| \cdot \|_{R^{-1}}^2$ denotes the squared Mahalanobis distance, which is statistically appropriate for Gaussian noise with covariance $R$. The solution $u_{\lambda}$ is implicitly a function of the hyperparameter $\lambda$.

The outer problem then seeks to minimize a validation loss, which measures how well $u_{\lambda}$ generalizes to data it has not seen during training. This loss is computed using the validation data $y_{\mathrm{val}}$:
$$
\min_{\lambda > 0} \ J(\lambda) := \frac{1}{2} \left\| A u_{\lambda} - y_{\mathrm{val}} \right\|_{R^{-1}}^{2}.
$$
The complete, well-posed bilevel formulation combines these two levels, ensuring that the hyperparameter is chosen to optimize for generalization, not just for training fit [@problem_id:3368777]. This structure is fundamental and prevents the [data leakage](@entry_id:260649) that would occur if validation data were used to determine the state estimate $u$ directly.

### The Lower-Level Problem: Well-Posedness and Solution

Before we can optimize the outer objective, we must ensure that the inner problem is well-behaved. Specifically, for any given $\lambda$ in the search space, does a solution $u_{\lambda}$ exist, and is it unique? The uniqueness of $u_{\lambda}$ is critical, as it allows us to treat the solution as a [well-defined function](@entry_id:146846) of $\lambda$, a prerequisite for differentiation.

The lower-level objective for Tikhonov regularization is a quadratic function of $u$:
$$
J_{\text{inner}}(u; \lambda) = \frac{1}{2} u^T (A^T A + \lambda L^T L) u - y_{\mathrm{tr}}^T A u + \frac{1}{2} y_{\mathrm{tr}}^T y_{\mathrm{tr}}.
$$
A unique minimizer for this unconstrained convex program exists if and only if the objective is strictly convex, which in turn requires its Hessian matrix to be [positive definite](@entry_id:149459). The Hessian of $J_{\text{inner}}$ with respect to $u$ is given by:
$$
H_{\lambda} = A^T A + \lambda L^T L.
$$
For $H_{\lambda}$ to be positive definite, the quadratic form $u^T H_{\lambda} u$ must be strictly positive for any non-zero vector $u$. Let's examine this form:
$$
u^T H_{\lambda} u = u^T A^T A u + \lambda u^T L^T L u = \|A u\|_2^2 + \lambda \|L u\|_2^2.
$$
Since both terms are non-negative, their sum can only be zero if both terms are individually zero. For $\lambda > 0$, this requires that $\|A u\|_2^2 = 0$ and $\|L u\|_2^2 = 0$, which means $u$ must belong to the null space of $A$ and the null space of $L$ simultaneously. To prevent any non-[zero vector](@entry_id:156189) $u$ from making the [quadratic form](@entry_id:153497) zero, we must impose the condition that the intersection of these null spaces contains only the [zero vector](@entry_id:156189):
$$
\mathcal{N}(A) \cap \mathcal{N}(L) = \{0\}.
$$
This is the fundamental condition for the [existence and uniqueness](@entry_id:263101) of the Tikhonov-regularized solution for any $\lambda > 0$. If this condition holds, the Hessian $H_{\lambda}$ is invertible, and we can find the unique solution $u_{\lambda}$ by setting the gradient of the inner objective to zero, which yields the familiar **normal equations**:
$$
(A^T A + \lambda L^T L) u_{\lambda} = A^T y_{\mathrm{tr}}.
$$
The explicit solution is then given by:
$$
u_{\lambda}(y_{\mathrm{tr}}) = (A^T A + \lambda L^T L)^{-1} A^T y_{\mathrm{tr}}.
$$
This expression makes explicit the dependence of the inner solution on the hyperparameter $\lambda$ and forms the basis for computing the [hypergradient](@entry_id:750478) [@problem_id:3368767].

### Computing the Hypergradient via Implicit Differentiation

To solve the outer problem $\min_{\lambda} J(\lambda)$ using [gradient-based methods](@entry_id:749986), we need to compute the derivative $\frac{\mathrm{d}J}{\mathrm{d}\lambda}$, often termed the **[hypergradient](@entry_id:750478)**. This is the derivative of the outer loss with respect to a hyperparameter of the inner problem. Since $J(\lambda)$ depends on $\lambda$ through the inner solution $u_{\lambda}$, we can apply the [chain rule](@entry_id:147422):
$$
\frac{\mathrm{d}J}{\mathrm{d}\lambda} = \left(\frac{\partial J}{\partial u_{\lambda}}\right)^{\top} \frac{\mathrm{d}u_{\lambda}}{\mathrm{d}\lambda}.
$$
The first term, $\frac{\partial J}{\partial u_{\lambda}}$, is simply the gradient of the outer loss with respect to the model parameters, evaluated at the solution $u_{\lambda}$. For a standard validation loss $J(\lambda) = \frac{1}{2}\|A_{\mathrm{val}} u_{\lambda} - y_{\mathrm{val}}\|_2^2$, this gradient is $A_{\mathrm{val}}^{\top}(A_{\mathrm{val}} u_{\lambda} - y_{\mathrm{val}})$.

The second term, $\frac{\mathrm{d}u_{\lambda}}{\mathrm{d}\lambda}$, is the sensitivity of the inner solution to a change in the hyperparameter. It is the key quantity we need to find. A naive approach would be to differentiate the explicit solution $u_{\lambda} = H_{\lambda}^{-1} A^T y_{\mathrm{tr}}$, but this requires differentiating a matrix inverse, which can be cumbersome. A more elegant and general approach is **[implicit differentiation](@entry_id:137929)**.

We start with the [normal equations](@entry_id:142238), which define $u_{\lambda}$ implicitly:
$$
(A^{\top}A + \lambda L^{\top}L) u_{\lambda} = A^{\top}y_{\mathrm{tr}}.
$$
Since this identity holds for all $\lambda$ in a neighborhood, we can differentiate the entire equation with respect to $\lambda$. Applying the product rule to the left-hand side yields:
$$
\frac{\mathrm{d}}{\mathrm{d}\lambda}(A^{\top}A + \lambda L^{\top}L) u_{\lambda} + (A^{\top}A + \lambda L^{\top}L) \frac{\mathrm{d}u_{\lambda}}{\mathrm{d}\lambda} = 0.
$$
The derivative of the matrix term is simply $L^{\top}L$. Rearranging to solve for the sensitivity $\frac{\mathrm{d}u_{\lambda}}{\mathrm{d}\lambda}$, we get:
$$
(A^{\top}A + \lambda L^{\top}L) \frac{\mathrm{d}u_{\lambda}}{\mathrm{d}\lambda} = - (L^{\top}L) u_{\lambda}.
$$
Since the matrix $H_{\lambda} = A^{\top}A + \lambda L^{\top}L$ is invertible, we can pre-multiply by its inverse:
$$
\frac{\mathrm{d}u_{\lambda}}{\mathrm{d}\lambda} = - (A^{\top}A + \lambda L^{\top}L)^{-1} (L^{\top}L) u_{\lambda}.
$$
This expression reveals how the inner solution $u_{\lambda}$ changes in response to an infinitesimal change in $\lambda$. Notice that computing this sensitivity requires solving a linear system with the same Hessian matrix $H_{\lambda}$ from the inner problem.

Finally, combining the parts, we obtain the full expression for the [hypergradient](@entry_id:750478) [@problem_id:3368776] [@problem_id:3368828]:
$$
\frac{\mathrm{d}J}{\mathrm{d}\lambda} = - \underbrace{\left(A_{\mathrm{val}} u_{\lambda} - y_{\mathrm{val}}\right)^{\top} A_{\mathrm{val}}}_{\left(\frac{\partial J}{\partial u_{\lambda}}\right)^{\top}} \underbrace{(A^{\top}A + \lambda L^{\top}L)^{-1} (L^{\top}L) u_{\lambda}}_{-\frac{\mathrm{d}u_{\lambda}}{\mathrm{d}\lambda}}.
$$

#### An Illustrative Calculation

To solidify these concepts, consider a concrete example [@problem_id:3368813]. Let $A = \begin{pmatrix} 1  1 \\ 0  1 \end{pmatrix}$, $L = \begin{pmatrix} 1  0 \\ 0  2 \end{pmatrix}$, and $B = \begin{pmatrix} 2  0 \\ 0  1 \end{pmatrix}$ be the validation operator. The training data is $y = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$ and validation data is $y_{\mathrm{val}} = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$. We wish to evaluate the [hypergradient](@entry_id:750478) $\frac{\mathrm{d}J}{\mathrm{d}\lambda}$ at $\lambda = 1$.

1.  **Solve for the inner solution $u_1$**: We first solve $(A^T A + 1 \cdot L^T L) u_1 = A^T y$.
    *   $A^T A = \begin{pmatrix} 1  1 \\ 1  2 \end{pmatrix}$, $L^T L = \begin{pmatrix} 1  0 \\ 0  4 \end{pmatrix}$.
    *   The Hessian is $H(1) = A^T A + L^T L = \begin{pmatrix} 2  1 \\ 1  6 \end{pmatrix}$.
    *   The right-hand side is $A^T y = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$.
    *   Solving $H(1) u_1 = A^T y$ gives $u_1 = H(1)^{-1} A^T y = \frac{1}{11} \begin{pmatrix} 6  -1 \\ -1  2 \end{pmatrix} \begin{pmatrix} 1 \\ 1 \end{pmatrix} = \frac{1}{11} \begin{pmatrix} 5 \\ 1 \end{pmatrix}$.

2.  **Compute the [hypergradient](@entry_id:750478)**: Now we plug $u_1$ and $\lambda=1$ into the [hypergradient](@entry_id:750478) formula $\frac{\mathrm{d}J}{\mathrm{d}\lambda} = - (B u_{1} - y_{\mathrm{val}})^T B (A^T A + L^T L)^{-1} L^T L u_{1}$.
    *   Validation residual: $B u_1 - y_{\mathrm{val}} = \frac{1}{11}\begin{pmatrix} 10 \\ 1 \end{pmatrix} - \begin{pmatrix} 0 \\ 1 \end{pmatrix} = \frac{10}{11}\begin{pmatrix} 1 \\ -1 \end{pmatrix}$.
    *   Gradient of outer loss: $(B u_1 - y_{\mathrm{val}})^T B = \frac{10}{11} \begin{pmatrix} 2  -1 \end{pmatrix}$.
    *   Sensitivity term: $H(1)^{-1} (L^T L u_1) = \frac{1}{11} \begin{pmatrix} 6  -1 \\ -1  2 \end{pmatrix} \left( \begin{pmatrix} 1  0 \\ 0  4 \end{pmatrix} \frac{1}{11} \begin{pmatrix} 5 \\ 1 \end{pmatrix} \right) = \frac{1}{121} \begin{pmatrix} 26 \\ 3 \end{pmatrix}$.
    *   Putting it all together: $\frac{\mathrm{d}J}{\mathrm{d}\lambda}|_{\lambda=1} = - \left( \frac{10}{11} \begin{pmatrix} 2  -1 \end{pmatrix} \right) \left( \frac{1}{121} \begin{pmatrix} 26 \\ 3 \end{pmatrix} \right) = -\frac{10}{1331}(52 - 3) = -\frac{490}{1331}$.

This negative value indicates that at $\lambda=1$, increasing the [regularization parameter](@entry_id:162917) would decrease the validation loss, suggesting we should move towards a larger $\lambda$.

#### An Analytical Solution in a Scalar Case

In some simple cases, we can use the [hypergradient](@entry_id:750478) to find a [closed-form solution](@entry_id:270799) for the optimal $\lambda$. Consider a scalar problem where we estimate $x \in \mathbb{R}$ from a measurement $y \in \mathbb{R}$ using the model $y = x + \text{noise}$. The Tikhonov-regularized estimate is $x^{\star}(\lambda) = \arg\min_x \frac{1}{2}(x - y)^2 + \frac{\lambda}{2} x^2$. The solution is explicitly $x^{\star}(\lambda) = \frac{y}{1+\lambda}$.

The outer problem is to minimize the validation loss $J(\lambda) = \frac{1}{2}(x^{\star}(\lambda) - z)^2$, where $z$ is a validation target. To find the optimal $\lambda$, we set the [hypergradient](@entry_id:750478) to zero:
$$
\frac{\mathrm{d}J}{\mathrm{d}\lambda} = (x^{\star}(\lambda) - z) \frac{\mathrm{d}x^{\star}}{\mathrm{d}\lambda} = 0.
$$
From the explicit solution, $\frac{\mathrm{d}x^{\star}}{\mathrm{d}\lambda} = -\frac{y}{(1+\lambda)^2}$. The derivative is zero if either $y=0$ (a trivial case) or if $x^{\star}(\lambda) - z = 0$. This second condition is highly intuitive: the optimal $\lambda$ is one that makes the regularized estimate match the validation target.
$$
x^{\star}(\lambda) = z \implies \frac{y}{1+\lambda} = z \implies \lambda^{\star} = \frac{y}{z} - 1.
$$
Since $\lambda$ must be non-negative, the solution is only valid if $y/z \ge 1$. If $y/z  1$, the derivative $\frac{\mathrm{d}J}{\mathrm{d}\lambda}$ is positive for all $\lambda \ge 0$, meaning the minimum occurs at the boundary, $\lambda^{\star}=0$. The complete solution is therefore $\lambda^{\star} = \max(0, \frac{y}{z} - 1)$. For instance, if the training data is $y=3$ and the validation target is $z=2$, the optimal [regularization parameter](@entry_id:162917) is $\lambda^{\star} = \frac{3}{2} - 1 = \frac{1}{2}$ [@problem_id:3368794]. This simple example beautifully illustrates the core principle of bilevel learning: finding the hyperparameter that makes the model generalize best to unseen data.

### Extensions to Nonsmooth Regularization

The [implicit differentiation](@entry_id:137929) technique is not limited to smooth regularizers like Tikhonov. It can be extended to nonsmooth problems, such as those involving the $\ell_1$-norm (LASSO), which is widely used for promoting sparsity. Consider the LASSO inner problem:
$$
x^{*}(\lambda) \in \operatorname*{arg\,min}_{x \in \mathbb{R}^{n}} \frac{1}{2}\|A x - y\|_{2}^{2} + \lambda \|x\|_{1}.
$$
The challenge here is that the solution map $x^*(\lambda)$ is not continuously differentiable everywhere. However, under certain regularity conditions, it is piecewise differentiable. Specifically, if the set of non-zero components of the solution, known as the **active set** $S = \{i : x_i^*(\lambda) \neq 0\}$, remains constant in a neighborhood of some $\lambda_0$, then the problem becomes locally smooth on that active set.

The optimality condition for LASSO is given by the Karush-Kuhn-Tucker (KKT) conditions:
$$
A^{\top}(A x^{*} - y) + \lambda s = 0,
$$
where $s$ is a [subgradient](@entry_id:142710) of the $\ell_1$-norm at $x^*$. For components in the active set ($i \in S$), $s_i = \mathrm{sign}(x_i^*)$, which is locally constant. For components in the inactive set ($i \notin S$), $x_i^*=0$.

By focusing only on the equations corresponding to the active set $S$, we can write a system that is locally smooth in $\lambda$:
$$
A_S^{\top} (A_S x_S^*(\lambda) - y) + \lambda s_S = 0,
$$
where the subscript $S$ denotes restriction to the columns or entries in the active set. This equation now looks very similar to the smooth Tikhonov case. We can differentiate it with respect to $\lambda$ (assuming $s_S$ is constant) to find the sensitivity of the active components:
$$
A_S^{\top} A_S \frac{\mathrm{d}x_S^*}{\mathrm{d}\lambda} + s_S = 0 \implies \frac{\mathrm{d}x_S^*}{\mathrm{d}\lambda} = -(A_S^{\top}A_S)^{-1} s_S.
$$
The derivatives of the inactive components are zero. The [hypergradient](@entry_id:750478) is then computed using the [chain rule](@entry_id:147422), summing only over the active set:
$$
\frac{\mathrm{d}J}{\mathrm{d}\lambda} = \left(\frac{\partial J}{\partial x_S^*}\right)^{\top} \frac{\mathrm{d}x_S^*}{\mathrm{d}\lambda} = - \left(\big[B^{\top}(B x^{*} - y_{\mathrm{val}})\big]_S\right)^{\top} (A_S^{\top}A_S)^{-1} s_S.
$$
This powerful result shows that even for nonsmooth problems, we can compute hypergradients by identifying the local [smooth manifold](@entry_id:156564) on which the solution lies and applying [implicit differentiation](@entry_id:137929) there [@problem_id:3368775].

### Computational Strategies for Hypergradient Calculation

While [implicit differentiation](@entry_id:137929) provides an exact formula for the [hypergradient](@entry_id:750478), its computation involves solving a linear system with the Hessian matrix, e.g., $H_{\lambda} v = w$. For large-scale problems, this can be computationally expensive, especially since it must be done at every step of the outer optimization for $\lambda$.

An alternative strategy arises when the inner problem is solved with an iterative algorithm, such as the Iterative Shrinkage-Thresholding Algorithm (ISTA) or gradient descent. The solution $x^*(\lambda)$ is the fixed point of an iteration map $T$, i.e., $x^*(\lambda) = T(x^*(\lambda); \lambda)$. The sensitivity $\frac{\mathrm{d}x^*}{\mathrm{d}\lambda}$ can be expressed using a Neumann series:
$$
\frac{\mathrm{d}x^*}{\mathrm{d}\lambda} = (I - J_T)^{-1} \partial_{\lambda} T = \left( \sum_{k=0}^{\infty} J_T^k \right) \partial_{\lambda} T,
$$
where $J_T = \frac{\partial T}{\partial x}$ is the Jacobian of the map $T$ with respect to $x$, and $\partial_{\lambda} T$ is the partial derivative with respect to $\lambda$.

This formulation suggests two main computational approaches [@problem_id:3368764]:

1.  **Implicit Differentiation**: This involves computing $\frac{\mathrm{d}x^*}{\mathrm{d}\lambda}$ by solving the linear system $(I - J_T)v = \partial_{\lambda} T$. This is mathematically equivalent to differentiating the [normal equations](@entry_id:142238). It is exact but requires a linear system solve.

2.  **Truncated Backpropagation**: This method approximates the infinite Neumann series by a finite sum of $K$ terms. This is equivalent to unrolling the iterative solver for $K$ steps and then applying [reverse-mode automatic differentiation](@entry_id:634526) ([backpropagation](@entry_id:142012)) through this unrolled computation graph. This approach avoids an explicit linear system solve but introduces a bias, as it neglects the tail of the series.

The bias of the truncated [hypergradient](@entry_id:750478) $g_K(\lambda)$ after $K$ steps can be bounded. If the [iterative map](@entry_id:274839) $T$ is a contraction with rate $q = \|J_T\|_2  1$, the error decreases geometrically:
$$
|g_K(\lambda) - g(\lambda)| \le \|\nabla_x \ell(x^*) \|_2 \|\partial_{\lambda} T(x^*; \lambda)\|_2 \frac{q^{K+1}}{1-q}.
$$
This bound allows for an adaptive [stopping rule](@entry_id:755483): for a desired tolerance $\varepsilon$, one can choose the number of unrolling steps $K$ large enough to guarantee that the [approximation error](@entry_id:138265) is below $\varepsilon$. This provides a practical trade-off between computational cost and accuracy, making [hypergradient](@entry_id:750478) computation feasible for very large-scale models where exact Hessian-based methods are prohibitive.

### Alternative Perspectives and Objectives

The bilevel framework is versatile and connects to several other important concepts in [statistical learning](@entry_id:269475).

From a **Bayesian perspective**, Tikhonov regularization is equivalent to finding the Maximum A Posteriori (MAP) estimate of $x$ under a Gaussian prior. In this view, learning the hyperparameter $\lambda$ can be framed as an **Empirical Bayes** procedure, where $\lambda$ is chosen to maximize the [marginal likelihood](@entry_id:191889) or "evidence" of the data, $p(y | \lambda)$. For linear-Gaussian models, it can be shown that the negative log-marginal likelihood is given by:
$$
- \log p(y \mid \lambda) = J(x_\lambda, \lambda) + \frac{1}{2} \log \det (Q_{\lambda}) - \frac{n}{2} \log \lambda + c,
$$
where $J(x_\lambda, \lambda)$ is the minimized value of the inner objective and $Q_\lambda$ is the posterior [precision matrix](@entry_id:264481). Optimizing this objective provides another principled way to select $\lambda$. It is also worth noting that this evidence function is generally non-convex in $\lambda$, making its optimization challenging [@problem_id:3368780].

Furthermore, the choice of the outer objective itself is a modeling decision. While we have focused on a simple validation loss, other criteria are also common [@problem_id:3368837]:

*   **Predictive Risk**: The true expected squared [prediction error](@entry_id:753692), $\mathbb{E}[ \| A x_{\lambda}(y) - A x_{\star} \|_2^2 ]$, is the ideal but unobservable target.
*   **Stein’s Unbiased Risk Estimate (SURE)**: For Gaussian noise, SURE provides an unbiased, data-driven estimate of the predictive risk without requiring a separate validation set.
*   **Cross-Validation (CV)**: Methods like Leave-One-Out CV (LOOCV) provide a nearly unbiased estimate of predictive risk and are more broadly applicable to non-Gaussian noise.

While these criteria have different finite-sample properties, it is a foundational result in statistical theory that under suitable conditions (e.g., in a well-behaved asymptotic regime), they are often equivalent. Minimizing any of them leads to the selection of the same asymptotically optimal [regularization parameter](@entry_id:162917). This provides theoretical justification for using these practical, data-driven criteria as surrogates for the ideal but unknowable predictive risk.