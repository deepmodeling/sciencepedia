## Introduction
Optimization is a cornerstone of science and engineering, but what happens when the function you need to optimize is a "black box"? In countless real-world scenarios—from tuning complex machine learning models to calibrating climate simulators—the derivatives essential for traditional [optimization methods](@entry_id:164468) are unavailable or prohibitively expensive to compute. This knowledge gap creates a significant challenge: how can we navigate vast, unknown landscapes to find an [optimal solution](@entry_id:171456) efficiently?

Model-based [derivative-free optimization](@entry_id:137673) (DFO) provides a powerful and principled answer. Instead of relying on gradients, these algorithms intelligently construct a local, simplified approximation—a surrogate model—of the true function using a limited number of sample evaluations. By performing optimization steps on this cheaper model within a carefully managed "trust region," DFO methods can make steady progress toward a solution, even in the face of noise, constraints, and high evaluation costs.

This article will guide you through the theory and practice of these sophisticated techniques. In the first chapter, **Principles and Mechanisms**, you will learn the core concepts, from building polynomial and radial basis function models to managing the trust-region feedback loop. Next, **Applications and Interdisciplinary Connections** will showcase the versatility of DFO in solving complex problems across machine learning, engineering, and economics. Finally, **Hands-On Practices** will provide you with concrete exercises to solidify your understanding and apply these methods to practical scenarios.

## Principles and Mechanisms

Model-based [derivative-free optimization](@entry_id:137673) (DFO) methods represent a powerful class of algorithms for solving optimization problems where the derivatives of the objective function are unavailable or impractical to compute. These methods operate on a simple yet profound principle: if the true [objective function](@entry_id:267263) $f(x)$ is too complex or expensive to work with directly, one should approximate it with a simpler, cheaper **[surrogate model](@entry_id:146376)** $m(x)$ and perform optimization steps based on this model. The entire process is managed within a **trust region**, a localized domain where the surrogate is believed to be a faithful approximation of the true function. This chapter elucidates the core principles and mechanisms that govern the construction of these models and the logic of the trust-region framework.

### The Core Idea: Surrogate Models in a Trust Region

At each iteration $k$, a model-based DFO algorithm focuses on a region around the current best point, or iterate, $x_k$. This region, typically a ball of radius $\Delta_k > 0$ centered at $x_k$, is the trust region. Within this region, the algorithm constructs a surrogate model $m_k(s)$ that approximates the behavior of the true function $f(x_k + s)$ for steps $s$ such that $\|s\| \le \Delta_k$.

The iterative process follows a logical loop:
1.  **Model Construction**: Build or update a local surrogate model $m_k(s)$ using values of $f$ evaluated at a set of sample points.
2.  **Step Calculation**: Solve a [trust-region subproblem](@entry_id:168153), which involves finding a step $s_k$ that minimizes the model $m_k(s)$ within the bounds of the trust region: $s_k \approx \arg\min_{\|s\| \le \Delta_k} m_k(s)$.
3.  **Step Evaluation**: The proposed step is evaluated by computing the true function value at the new point, $f(x_k + s_k)$. The algorithm assesses the quality of the step by comparing the *actual reduction* in the [objective function](@entry_id:267263) to the *predicted reduction* by the model.
4.  **Update**: Based on the agreement between the model's prediction and the actual outcome, the algorithm decides whether to accept the new point (i.e., set $x_{k+1} = x_k + s_k$) and how to adjust the trust-region radius $\Delta_k$ for the next iteration. A good prediction may lead to an expansion of the trust region, while a poor prediction necessitates shrinking it.

This [iterative refinement](@entry_id:167032) of model and trust region is the engine that drives the optimization forward, balancing the goal of making progress (exploitation) with the need to maintain an accurate model (exploration).

### Constructing Surrogate Models

The effectiveness of a model-based method hinges on the quality of its surrogate model. While various types of models exist, polynomial functions are the most common starting point due to their simplicity and well-understood properties.

#### Polynomial Interpolation Models

An interpolation model is one that is required to exactly match the known function values at a set of points. For a quadratic model in one dimension, $m(x) = ax^2 + bx + c$, we need to determine three coefficients $(a, b, c)$. This can be achieved by evaluating the true function $f(x)$ at three distinct points $(x_1, x_2, x_3)$ and solving the system of linear equations that arises from the interpolation conditions $m(x_i) = f(x_i)$ for $i=1, 2, 3$.

For instance, to construct a quadratic model that passes through the points $(-1, 4.5)$, $(0.5, 1.0)$, and $(2, 6.0)$, we would solve the system:
$$
\begin{align*}
a(-1)^2 + b(-1) + c = 4.5 \\
a(0.5)^2 + b(0.5) + c = 1.0 \\
a(2)^2 + b(2) + c = 6.0
\end{align*}
$$
Solving this system yields the unique coefficients for the local model [@problem_id:2166488]. This process generalizes to higher dimensions. A linear model in $\mathbb{R}^n$, $m(x) = c + g^T x$, has $n+1$ parameters (the scalar $c$ and the $n$ components of the [gradient vector](@entry_id:141180) $g$), and thus generally requires $n+1$ interpolation points to be uniquely determined. A full quadratic model, $m(s) = c + g^T s + \frac{1}{2} s^T B s$, has $1 + n + \frac{n(n+1)}{2}$ coefficients.

A critical requirement for this process to succeed is that the set of interpolation points must be **well-poised**. This is a geometric condition ensuring that the system of linear equations for the model coefficients has a unique solution. If the set is not well-poised (or is *ill-poised*), the model is not uniquely determined.

Consider constructing a linear model $m(x) = c + g^T x$ in $\mathbb{R}^3$ using four points $\{y_0, y_1, y_2, y_3\}$. From the properties of a linear model, we know that for any two points $y_i$ and $y_j$, the difference in model values is $m(y_i) - m(y_j) = g^T(y_i - y_j)$. Since the model interpolates the function, this implies $f(y_i) - f(y_j) = g^T(y_i - y_j)$. This gives us a system of equations to find the model gradient $g$. If, for example, the four points $y_0, y_1, y_2, y_3$ happen to lie on the same plane (i.e., they are coplanar), the displacement vectors $\{y_1-y_0, y_2-y_0, y_3-y_0\}$ will also be coplanar and cannot span $\mathbb{R}^3$. Consequently, they cannot uniquely determine all three components of the [gradient vector](@entry_id:141180) $g$. Specifically, the component of $g$ normal to the plane containing the points will be undetermined. In such cases, the model is ambiguous, and an [optimization algorithm](@entry_id:142787) relying on it may stall or fail [@problem_id:2166511]. Ensuring the poisedness of the interpolation set is a fundamental task in managing the model.

#### Beyond Polynomials: Radial Basis Function (RBF) Models

While polynomials are a workhorse, other model classes offer greater flexibility. **Radial Basis Functions (RBFs)** are a powerful alternative, constructing a model of the form $s(x) = \sum_{j=1}^N w_j \phi(\|x - x_j\|)$, where $\{x_j\}$ are the centers (often the interpolation points themselves), $\phi$ is a kernel function (e.g., cubic $\phi(r)=r^3$, or Gaussian $\phi(r)=\exp(-(r/\varepsilon)^2)$), and $w_j$ are weights determined by the interpolation conditions.

A sophisticated DFO algorithm might maintain a *portfolio* of candidate models, such as several RBF models with different kernels or different parameters (like the shape parameter $\varepsilon$ in the Gaussian kernel). At each iteration, it must select the best model from this portfolio. For expensive functions, this selection must be done without additional function evaluations. **Leave-one-out cross-validation (LOO-CV)** is a robust technique for this, but a naive implementation is prohibitively expensive. Fortunately, for RBF interpolants, a computational shortcut exists that allows the LOO-CV errors to be calculated efficiently from the inverse of a single interpolation matrix, making this a viable strategy for practical DFO [@problem_id:3153318].

### The Trust-Region Mechanism: Managing the Model and Step

The trust region is the mechanism that controls the interaction between the model and the true function. Its radius, $\Delta_k$, is a dynamic parameter that reflects the algorithm's confidence in its current surrogate model.

#### The Basic Feedback Loop: Step Acceptance and Radius Update

The core idea of the trust-region feedback loop can be understood even without a sophisticated model. Consider a simple **compass search** or **[pattern search](@entry_id:170858)** algorithm. At iteration $k$, it probes a fixed set of directions around the current point $x_k$ at a distance of $\Delta_k$. If any of these trial points yield a strict decrease in the function value, the iteration is a **success**. The algorithm moves to the best new point and, being confident, might expand the trust region for the next iteration: $\Delta_{k+1} = \gamma \Delta_k$ for some expansion factor $\gamma > 1$. If none of the trial points yield an improvement, the iteration is a **failure**. The algorithm stays at $x_k$ and, acknowledging that its search radius was too large, contracts the trust region: $\Delta_{k+1} = \beta \Delta_k$ for some contraction factor $0  \beta  1$.

The choice of $\gamma$ and $\beta$ balances convergence speed and stability. Aggressive parameters (large $\gamma$, small $\beta$) can lead to rapid progress on [simple functions](@entry_id:137521) but may cause instability on more complex landscapes, like the narrow, curving valley of the Rosenbrock function [@problem_id:3117671]. This simple success/failure logic forms the basis of the more refined model-based approach.

#### The Model-Based Approach: The $\rho$ Ratio

In a model-based framework, the decision to accept a step and update the radius is guided by a more quantitative measure of model quality. We define two key quantities:
-   **Actual Reduction**: $\text{ared}_k = f(x_k) - f(x_k + s_k)$, the true improvement achieved by the step $s_k$.
-   **Predicted Reduction**: $\text{pred}_k = m_k(0) - m_k(s_k)$, the improvement predicted by the model.

The agreement between model and function is measured by their ratio, conventionally denoted by $\rho_k$:
$$
\rho_k = \frac{\text{ared}_k}{\text{pred}_k}
$$
The value of $\rho_k$ dictates the algorithm's actions, typically governed by two thresholds, $0  \eta_1  \eta_2  1$.

1.  **Excellent Agreement ($\rho_k  \eta_2$)**: The actual reduction is a large fraction of, or even exceeds, the predicted reduction. The step is accepted ($x_{k+1} = x_k + s_k$), and confidence in the model is high. The trust region is expanded: $\Delta_{k+1} = \gamma_{\text{inc}} \Delta_k$ with $\gamma_{\text{inc}}  1$.
2.  **Acceptable Agreement ($\eta_1 \le \rho_k \le \eta_2$)**: The step provides a [sufficient decrease](@entry_id:174293), though not as much as predicted. The step is accepted ($x_{k+1} = x_k + s_k$), but confidence in the model is neutral. The trust region radius is often kept the same: $\Delta_{k+1} = \Delta_k$.
3.  **Poor Agreement ($\rho_k \le \eta_1$)**: The actual reduction is negligible or the function value even increased. The model has proven to be a poor predictor at the current scale. The step is rejected ($x_{k+1} = x_k$), and the trust region must be shrunk: $\Delta_{k+1} = \gamma_{\text{dec}} \Delta_k$ with $\gamma_{\text{dec}} \in (0, 1)$ [@problem_id:3153333].

While the $\rho_k$ ratio is a powerful tool, it must be interpreted with care. It measures the *agreement* between the model and the function for a given step, but it does not guarantee the absolute quality of the model. It is possible to construct pathological cases where a model exhibits severe bias—for example, by vastly underestimating both the local gradient and curvature of the true function. Such a "timid" model may predict a very small decrease (`pred`), while the true function yields a much larger one (`ared`). The resulting ratio $\rho_k = \text{ared} / \text{pred}$ can be very large, falsely signaling an excellent model. An algorithm blindly trusting this large $\rho_k$ would expand the trust region, extending its reliance on what is actually a very poor model, potentially hindering convergence [@problem_id:3153333].

### Advanced Topics and Practical Considerations

Building a robust DFO solver requires addressing several practical challenges, from handling noisy data to intelligently managing and improving the [surrogate model](@entry_id:146376) over time.

#### Handling Noisy Function Evaluations

When function evaluations are contaminated with noise, i.e., we observe $y_i = f(x_i) + \epsilon_i$, where $\epsilon_i$ is a random error term, the modeling strategy must adapt. Interpolation-based models, which force $m(x_i) = y_i$, become highly problematic as they will fit the noise in the data. This phenomenon, known as **overfitting**, results in a model with high parameter variance that generalizes poorly.

A more robust approach is to use **regression-based models**. By using more points than are strictly necessary to define the model (e.g., $N  p$ points, where $p$ is the number of model parameters), we can find the parameters $\beta$ that minimize the [sum of squared errors](@entry_id:149299), $\|\Phi\beta - y\|_2^2$. This least-squares fit averages out the noise instead of interpolating it.

A principled criterion for choosing between interpolation and regression can be derived from statistical theory. The covariance of the estimated model parameters $\hat{\beta}$ is given by $\text{Cov}(\hat{\beta}) = \sigma^2 (\Phi^T \Phi)^{-1}$, where $\sigma^2$ is the noise variance and $\Phi$ is the design matrix. A useful scalar measure of total [parameter uncertainty](@entry_id:753163) is the sum of the parameter variances, $V = \text{trace}(\text{Cov}(\hat{\beta})) = \sigma^2 \text{trace}((\Phi^T \Phi)^{-1})$. By estimating the noise variance $\sigma^2$ (e.g., from replicate evaluations) and computing the trace term for both a candidate interpolation set and a regression set, an algorithm can choose the strategy that minimizes this total variance, leading to a more stable and reliable model [@problem_id:3153280].

The sampling strategy itself is also critical under noise. Consider building a 1D quadratic model with a limited budget of new evaluations. One must decide between repeating evaluations at existing points or sampling new locations. To estimate curvature (the quadratic term), the model requires information from at least three distinct locations. Sampling a new point at $x=-\Delta$ when points at $x=0$ and $x=+\Delta$ already exist is essential for this. Any remaining budget can then be used for replicate samples (e.g., at the center $x=0$) to reduce the overall variance of the parameter estimates by averaging out noise [@problem_id:3153321].

#### Model Management and Failsafes

Even in a noise-free setting, interpolation can produce unreliable models. For a quadratic model $m_k(s) = f(x_k) + g_k^T s + \frac{1}{2} s^T B_k s$, the Hessian matrix $B_k$ may exhibit large [negative curvature](@entry_id:159335) (i.e., have large negative eigenvalues). This can cause the model to predict an enormous decrease within the trust region that is not matched by the true function.

A simple check for $\lambda_{\min}(B_k)  0$ is too sensitive. A more sophisticated criterion is needed to decide if the curvature is "dangerously" negative. The effect of the quadratic term should be compared to the effect of the linear term. A principled condition for unreliability arises by comparing the maximum possible curvature-induced reduction, $-\frac{1}{2} \Delta_k^2 \lambda_{\min}(B_k)$, to the scale of the linear reduction, $\|g_k\| \Delta_k$. This leads to a scaled check: declare the Hessian unreliable if $\lambda_{\min}(B_k) \le -\eta \frac{2 \|g_k\|}{\Delta_k}$ for some threshold $\eta  0$.

However, this structural check should be combined with empirical evidence of failure. The most robust approach is to trigger a failsafe only when the Hessian is structurally suspect *and* the model has proven inaccurate on the current step, i.e., $\rho_k$ is small. When such unreliability is detected, the algorithm can temporarily switch to a simpler, more robust step, such as the gradient-only **Cauchy step**, $s_k^{\text{grad}} = - \frac{\Delta_k}{\|g_k\|} g_k$, which ignores the suspect Hessian $B_k$ entirely [@problem_id:3153257].

#### Intelligent Sampling: Balancing Exploration and Exploitation

Beyond just maintaining a well-poised set, advanced algorithms aim to *intelligently* improve the model by carefully selecting where to sample next. This involves balancing two competing objectives:
-   **Exploitation**: Sampling at the point that the current model predicts is the best, i.e., minimizing $m_k(s)$.
-   **Exploration**: Sampling at a point where the model is most uncertain, thereby improving its overall accuracy.

This trade-off can be formalized using an **[acquisition function](@entry_id:168889)**. For Gaussian Process (GP) models, a common choice is the **Lower Confidence Bound (LCB)**, which seeks to minimize $m_k(s) - \kappa_k \sigma_k(s)$, where $m_k(s)$ is the predicted mean and $\sigma_k(s)$ is the posterior standard deviation (a [measure of uncertainty](@entry_id:152963)). The parameter $\kappa_k  0$ controls the trade-off. This criterion favors points that either have a low predicted value or high uncertainty. Similar principles can be applied to polynomial models by constructing an [uncertainty measure](@entry_id:270603) based on the Lagrange polynomials associated with the interpolation set. Formulating the next point selection as the optimization of such an [acquisition function](@entry_id:168889) provides a principled mechanism for active model improvement [@problem_id:3153347].

#### Termination Criteria

Finally, a robust DFO method needs a reliable rule for when to stop. Relying on a single condition, like a small trust-region radius, is insufficient, as this can occur simply because the model is persistently poor. A principled termination criterion should confirm that two conditions are met: first, that an approximate optimum has been found, and second, that the information used to make this assessment is trustworthy.

This leads to a multi-part criterion that must be satisfied simultaneously:
1.  **Approximate Optimality**: The norm of the model gradient, $\|\nabla m_k(0)\|$, which serves as our estimate for the true gradient $\|\nabla f(x_k)\|$, must be small: $\|\nabla m_k(0)\| \le \varepsilon_g$.
2.  **Local Convergence**: The trust-region radius must be small, $\Delta_k \le \varepsilon_\Delta$, indicating that the search has been localized to a small region.
3.  **Model Fidelity**: The model must have demonstrated consistent and high-quality agreement with the true function. This can be verified by checking that $|\rho_j - 1| \le \varepsilon_\rho$ for a recent history of iterations, e.g., for $j = k-L+1, \dots, k$.

Only when all three conditions are met can the algorithm confidently terminate, declaring that it has found an approximate [stationary point](@entry_id:164360) and that its assessment is based on a reliable local model [@problem_id:3153342].