## Introduction
Iterative [optimization algorithms](@entry_id:147840) are the engines of modern computational science, progressively refining solutions to complex problems. However, this iterative process raises a critical question: when is a solution "good enough"? Without a clear answer, an algorithm might stop too soon, yielding a poor result, or run indefinitely, wasting valuable resources. This is the domain of **stopping criteria and tolerances**—the set of rules that governs when to terminate an optimization process. Crafting effective stopping criteria is a nuanced art, requiring a deep understanding of both [optimization theory](@entry_id:144639) and practical application.

This article provides a comprehensive guide to this crucial topic. We will begin in the section **Principles and Mechanisms** by dissecting the fundamental building blocks of stopping criteria, from simple gradient norms to advanced measures for constrained and non-smooth problems, and examining their pitfalls in settings like [ill-conditioned problems](@entry_id:137067). The section **Applications and Interdisciplinary Connections** will then bridge theory and practice, exploring how these criteria are adapted for sophisticated algorithms and applied in fields like machine learning and engineering, where tolerances are tied to statistical generalization and physical reality. Finally, the **Hands-On Practices** section will offer a chance to implement and test these concepts, solidifying your understanding by building robust solvers for practical challenges. By the end, you will be equipped to design and interpret stopping criteria that are not just numerically sound, but meaningfully aligned with your specific optimization goals.

## Principles and Mechanisms

Iterative optimization algorithms are the workhorses of modern science and engineering, generating sequences of improving approximations to a problem's solution. A foundational question in their practical application is determining when to terminate the process. An algorithm, if left unchecked, would run indefinitely. We therefore require a set of well-defined rules, known as **stopping criteria** (or termination criteria), to halt the iteration and accept the current iterate as a satisfactory solution. The design of these criteria is a delicate balance. A criterion that is too lenient may cause premature termination, yielding a low-quality approximation far from the true optimum. Conversely, a criterion that is too stringent may lead to excessive and unnecessary computation for negligible gains in accuracy. This chapter elucidates the core principles and mechanisms behind modern stopping criteria, moving from the simplest cases to more complex and realistic optimization settings.

### Criteria for Unconstrained Smooth Optimization

For an unconstrained problem of minimizing a [smooth function](@entry_id:158037) $f: \mathbb{R}^n \to \mathbb{R}$, the [first-order necessary condition](@entry_id:175546) for a point $x^*$ to be a local minimizer is that it must be a stationary point, meaning the gradient is zero: $\nabla f(x^*) = 0$. Since [numerical algorithms](@entry_id:752770) operate with finite precision, we cannot expect to find a point where the gradient is exactly zero. Instead, a practical stopping criterion seeks to identify an iterate $x_k$ where the gradient is "small enough."

#### Measures of Stationarity

The most direct translation of the optimality condition is to monitor the magnitude of the [gradient vector](@entry_id:141180). A common choice for this is the Euclidean norm, leading to the **absolute gradient norm criterion**:
$$
\|\nabla f(x_k)\| \le \varepsilon_{\text{abs}}
$$
where $\varepsilon_{\text{abs}} > 0$ is a user-defined absolute tolerance. While simple and intuitive, this criterion harbors significant pitfalls.

First, it is sensitive to the scaling of the function $f(x)$. If we were to replace $f(x)$ with $g(x) = c f(x)$ for some positive constant $c$, the gradient would become $\nabla g(x) = c \nabla f(x)$. The stopping test for $g(x)$ would be $\|c \nabla f(x_k)\| \le \varepsilon_{\text{abs}}$, which is equivalent to $\|\nabla f(x_k)\| \le \varepsilon_{\text{abs}}/c$. This means that simply rescaling the objective function changes the effective tolerance, breaking the consistency of the criterion.

Second, and more critically, a small gradient norm does not necessarily imply that the iterate is close to the true minimum, either in function value or in position. This issue is particularly acute for **ill-conditioned** problems, where the function's landscape features long, flat valleys. Consider a strictly convex quadratic function $f(x) = \frac{1}{2} x^\top Q x - b^\top x$. The unique minimizer is $x^* = Q^{-1}b$. The suboptimality, or error in function value, can be expressed in terms of the gradient $\nabla f(x) = Qx - b$:
$$
f(x) - f(x^*) = \frac{1}{2} (x - x^*)^\top Q (x - x^*) = \frac{1}{2} \nabla f(x)^\top Q^{-1} \nabla f(x)
$$
The magnitude of this suboptimality depends not just on the size of the gradient, $\|\nabla f(x)\|$, but on the interaction between the gradient vector and the inverse Hessian, $Q^{-1}$. The worst-case suboptimality for a given gradient norm $\|\nabla f(x)\| \le \varepsilon$ occurs when the gradient aligns with the eigenvector of $Q^{-1}$ corresponding to its largest eigenvalue, $\lambda_{\max}(Q^{-1})$. This eigenvalue is the reciprocal of the smallest eigenvalue of $Q$, $\lambda_{\min}(Q)$. Thus, the maximum possible suboptimality is bounded by $\frac{1}{2} \varepsilon^2 \lambda_{\max}(Q^{-1})$.

For example, in a hypothetical scenario with an extremely ill-conditioned Hessian $Q = \text{diag}(10^{-6}, 10^2)$, the largest eigenvalue of its inverse is $\lambda_{\max}(Q^{-1}) = 10^6$. If an algorithm stops when $\|\nabla f(x_k)\|_2 \le 10^{-3}$, the suboptimality could be as large as $\frac{1}{2} (10^{-3})^2 (10^6) = 0.5$. An apparently small gradient can mask a very large error in the function value, rendering the absolute gradient norm criterion unreliable for [ill-conditioned problems](@entry_id:137067) [@problem_id:3187908].

To mitigate sensitivity to the overall scale of the problem, a **relative gradient norm criterion** is often used:
$$
\|\nabla f(x_k)\| \le \varepsilon_{\text{rel}} \|\nabla f(x_0)\|
$$
This condition terminates the algorithm when the gradient norm has been reduced by a certain fraction relative to its initial value. It is inherently [scale-invariant](@entry_id:178566) with respect to the function $f(x)$. However, it can be problematic if $\|\nabla f(x_0)\|$ is either exceptionally large (requiring an excessive number of iterations) or exceptionally small (causing premature termination).

A robust and widely adopted practice is to use a **mixed absolute-relative criterion**:
$$
\|\nabla f(x_k)\| \le \varepsilon_{\text{abs}} + \varepsilon_{\text{rel}} \|\nabla f(x_0)\|
$$
This criterion inherits the best of both worlds. The relative term provides [scale-invariance](@entry_id:160225) and ensures progress on problems with large initial gradients, while the absolute term prevents the algorithm from running indefinitely when the initial gradient is very small and ensures termination to a fixed level of stationarity [@problem_id:3187951]. It is important to recognize, however, that the presence of the $\varepsilon_{\text{abs}} > 0$ term means this mixed test is not strictly [scale-invariant](@entry_id:178566). True [scale-invariance](@entry_id:160225) is achieved only if $\varepsilon_{\text{abs}} = 0$.

Furthermore, if the function $f$ possesses stronger properties, such as being $\mu$-strongly convex, satisfying a stopping criterion can provide explicit guarantees on the quality of the solution. For a $\mu$-strongly convex function, we have the bounds:
$$
\|x_k - x^*\| \le \frac{1}{\mu} \|\nabla f(x_k)\| \quad \text{and} \quad f(x_k) - f(x^*) \le \frac{1}{2\mu} \|\nabla f(x_k)\|^2
$$
If the mixed stopping criterion is met, we can directly bound the distance to the optimum and the suboptimality:
$$
\|x_k - x^*\| \le \frac{1}{\mu} (\varepsilon_{\text{abs}} + \varepsilon_{\text{rel}} \|\nabla f(x_0)\|)
$$
$$
f(x_k) - f(x^*) \le \frac{1}{2\mu} (\varepsilon_{\text{abs}} + \varepsilon_{\text{rel}} \|\nabla f(x_0)\|)^2
$$
These relationships are fundamental, as they translate a heuristic stopping tolerance into a rigorous, quantitative certificate of solution quality [@problem_id:3187951].

### Criteria Based on Progress

An alternative class of stopping criteria is based not on an explicit measure of optimality, but on the observed progress of the algorithm from one iteration to the next. These criteria are appealing for their simplicity and universality, as they do not require gradient information.

Common progress-based criteria include monitoring the absolute change in the iterates, $\|x_{k+1} - x_k\| \le \varepsilon_x$, or the absolute change in the function value, $|f(x_{k+1}) - f(x_k)| \le \varepsilon_f$. To make these criteria robust to the scale of the solution vector, it is often better to use a relative measure. For instance, a **relative change in iterates criterion** checks if
$$
\frac{\|x_{k+1} - x_k\|}{\|x_{k+1}\|} \le \varepsilon_x \quad \text{or, to avoid division by zero,} \quad \frac{\|x_{k+1} - x_k\|}{\max\{1, \|x_{k+1}\|\}} \le \varepsilon_x
$$
The norm used can be any standard [vector norm](@entry_id:143228), such as the [infinity norm](@entry_id:268861), $\|\cdot\|_\infty$. A numerical example might involve iterates $x^{(k)} = (3.451, -1.234, 5.802)^\top$ and $x^{(k+1)} = (3.486, -1.201, 5.845)^\top$. The [infinity norm](@entry_id:268861) of the difference is $\|x^{(k+1)} - x^{(k)}\|_\infty = \max\{0.035, 0.033, 0.043\} = 0.043$, while $\|x^{(k+1)}\|_\infty = 5.845$. The relative change is $0.043 / 5.845 \approx 7.36 \times 10^{-3}$. This value would then be compared against a tolerance to decide whether to stop [@problem_id:2182360].

While intuitive, progress-based criteria must be used with extreme caution. Their fundamental flaw is that **stagnation does not imply convergence**. An algorithm can slow to a crawl, taking infinitesimally small steps, while still being very far from the true minimum. This is a common behavior for algorithms encountering ill-conditioned landscapes.

Consider a hypothetical sequence converging slowly to a known solution $x^*=2$, such as $x_k = 2 + 0.8^k$. The true [absolute error](@entry_id:139354) is $|x_k - x^*| = 0.8^k$. The absolute change between successive iterates is $|x_k - x_{k-1}| = |(2+0.8^k) - (2+0.8^{k-1})| = 0.2 \times 0.8^{k-1}$. For a tolerance of $\varepsilon = 0.05$, the criterion based on successive change, $|x_k - x_{k-1}| \le 0.05$, is met at iteration $k=8$. However, at this point, the true error is $|x_8 - x^*| = 0.8^8 \approx 0.168$, which is more than three times the desired tolerance. The criterion based on true error, $|x_k - x^*| \le 0.05$, is not met until iteration $k=14$ [@problem_id:2206870]. This example starkly illustrates the danger of relying solely on progress-based criteria. They are best used as a secondary check or a safeguard against infinite loops, in conjunction with a primary criterion based on a measure of optimality.

### Handling Heterogeneous Scales and Geometry

Many real-world [optimization problems](@entry_id:142739) involve variables with different physical units or vastly different numerical scales. For example, one variable might represent a pressure in Pascals, while another represents a temperature in Kelvin. In such cases, standard [vector norms](@entry_id:140649), which treat all components equally, become physically meaningless and numerically fragile.

#### Scaling and Non-Dimensionalization

Applying a norm to a vector of mixed units, such as one containing meters and millimeters, is a dimensionally inconsistent operation akin to "adding apples and oranges." A robust stopping criterion must first render all quantities dimensionless before combining or comparing them. This is achieved through **scaling**.

For an equality-constrained problem where we must check both constraint feasibility, $\|c(x_k)\|$, and Lagrangian [stationarity](@entry_id:143776), $\|\nabla_x \mathcal{L}(x_k, \lambda_k)\|$, a principled approach is to use diagonal scaling matrices. Suppose the constraint vector $c(x)$ has components with units of length (e.g., meters) and the [gradient vector](@entry_id:141180) $\nabla_x \mathcal{L}$ has components with units of inverse length. A proper method would involve scaling matrices, say $W_c$ and $W_x$, that non-dimensionalize each component before a norm is taken. For instance, if a [characteristic length](@entry_id:265857) scale for the problem is $L_{char} = 1$ meter, we could define $W_c = \text{diag}(1/L_{char}, \dots)$ and $W_x = \text{diag}(L_{char}, \dots)$. The criteria would then become:
$$
\|W_c c(x_k)\|_\infty \le \varepsilon_c \quad \text{and} \quad \|W_x \nabla_x \mathcal{L}(x_k, \lambda_k)\|_\infty \le \varepsilon_g
$$
This ensures that the test is invariant to the choice of physical units (e.g., meters vs. millimeters) and that the dimensionless tolerances $\varepsilon_c$ and $\varepsilon_g$ are applied to quantities of a comparable scale [@problem_id:3187859].

A related idea for unconstrained problems is to define a [scaling matrix](@entry_id:188350) that adapts to the current iterate $x_k$. A criterion of the form
$$
\|D(x_k)^{-1} \nabla f(x_k)\| \le \varepsilon
$$
where $D(x_k) = \text{diag}(\max\{1, |x_{k,i}|\})$ is a [diagonal matrix](@entry_id:637782) of component-wise magnitudes, attempts to measure a relative [stationarity](@entry_id:143776) for components of $x_k$ that are large, while defaulting to an absolute measure for components near zero [@problem_id:3187890]. While such criteria are improvements, achieving perfect invariance to general rescalings of variables remains a challenging theoretical and practical issue.

#### Preconditioned Criteria

Advanced [optimization algorithms](@entry_id:147840), such as [preconditioned conjugate gradient](@entry_id:753672) or quasi-Newton methods, often use a [symmetric positive definite](@entry_id:139466) **preconditioner** matrix $M$ to reshape the geometry of the problem space. The search direction is computed as $p_k = -M^{-1} \nabla f(x_k)$. This can be interpreted as performing a [steepest descent](@entry_id:141858) step in a new geometry defined by the inner product $\langle u, v \rangle_M = u^\top M v$.

In this preconditioned space, the natural way to measure the size of the gradient (a dual vector) is via the corresponding [dual norm](@entry_id:263611), which is given by:
$$
\|\nabla f(x_k)\|_{M^{-1}} = \sqrt{\nabla f(x_k)^\top M^{-1} \nabla f(x_k)} = \|M^{-1/2} \nabla f(x_k)\|
$$
where $M^{-1/2}$ is the [symmetric square](@entry_id:137676) root of $M^{-1}$. This leads to the **preconditioned stopping criterion**:
$$
\|M^{-1/2} \nabla f(x_k)\| \le \varepsilon_M
$$
This criterion is consistent with the geometry of the algorithm and is invariant under the change of variables $y = M^{1/2}x$. If $M$ is chosen well (e.g., as a diagonal [scaling matrix](@entry_id:188350) or an approximation of the Hessian), this test provides a much more reliable measure of proximity to the optimum than the unscaled Euclidean norm.

The choice between the Euclidean test $\|\nabla f(x_k)\| \le \varepsilon$ and the preconditioned test $\|M^{-1/2} \nabla f(x_k)\| \le \varepsilon_M$ involves a fundamental trade-off.
- The **preconditioned test** is preferable when the algorithm's behavior is tied to the geometry of $M$ and when variables have heterogeneous scales that $M$ is designed to correct.
- The **Euclidean test** is preferable when one needs a universal, algorithm-independent measure of [stationarity](@entry_id:143776) that can be compared across different methods or different [preconditioners](@entry_id:753679) [@problem_id:3187949].

### Criteria for Constrained and Non-Smooth Optimization

When [optimization problems](@entry_id:142739) involve constraints or non-differentiable terms, the simple condition $\nabla f(x^*) = 0$ no longer holds. The stopping criteria must be adapted to reflect the appropriate first-order [optimality conditions](@entry_id:634091) for these more complex settings.

#### Problems with Simple Constraints

For a problem with bound constraints, $\min f(x)$ subject to $l \le x \le u$, a point $x^*$ is stationary if the gradient component $\nabla_i f(x^*)$ is zero for any component $x_i^*$ in the interior of its bounds, non-negative if $x_i^* = l_i$, and non-positive if $x_i^* = u_i$. This complex logical condition can be captured by a single continuous vector quantity, the **projected gradient**. For a given step size $\alpha > 0$, the projected gradient mapping is defined as:
$$
\mathbf{g}_\alpha(x) = \frac{1}{\alpha} \left( x - \Pi_{[l,u]}(x - \alpha \nabla f(x)) \right)
$$
where $\Pi_{[l,u]}(\cdot)$ is the [projection operator](@entry_id:143175) onto the feasible box. A point $x$ is stationary if and only if $\mathbf{g}_\alpha(x) = 0$. This provides a natural stopping criterion for projected-[gradient-based methods](@entry_id:749986):
$$
\|\mathbf{g}_{\alpha_k}(x_k)\| \le \varepsilon
$$
where $\alpha_k$ is the step size used in the algorithm. A related stationarity measure, often used independently of the algorithm's step size, fixes $\alpha=1$ in the definition of the mapping [@problem_id:3187933].

#### Composite Non-Smooth Problems

Many modern problems take the composite form $\min F(x) = f(x) + g(x)$, where $f$ is smooth and $g$ is convex but possibly non-smooth (e.g., the $\ell_1$-norm used in LASSO). The [first-order optimality condition](@entry_id:634945) is a set inclusion: $0 \in \nabla f(x^*) + \partial g(x^*)$, where $\partial g$ is the subdifferential of $g$.

For these problems, stopping based on $\|\nabla f(x_k)\| \le \varepsilon$ is incorrect, as a solution does not require the gradient of the smooth part to be zero. The proper generalization of the gradient is the **proximal-gradient mapping**:
$$
G_\alpha(x) := \frac{1}{\alpha} \left( x - \operatorname{prox}_{\alpha g}(x - \alpha \nabla f(x)) \right)
$$
where $\operatorname{prox}_{\alpha g}$ is the [proximal operator](@entry_id:169061) of $g$. This mapping has the crucial property that $G_\alpha(x) = 0$ if and only if $x$ satisfies the [first-order optimality condition](@entry_id:634945). It therefore serves as a valid and consistent measure of [stationarity](@entry_id:143776). The appropriate stopping criterion is:
$$
\|G_\alpha(x_k)\| \le \varepsilon
$$
Importantly, in the special case where the non-smooth part is absent ($g(x) \equiv 0$), the [proximal operator](@entry_id:169061) becomes the [identity mapping](@entry_id:634191), and $G_\alpha(x)$ simplifies to exactly $\nabla f(x)$. Thus, this criterion correctly reduces to the standard gradient norm test for smooth problems [@problem_id:3187901].

#### General Constrained Problems and Interior-Point Methods

For general nonlinear programs with equality and [inequality constraints](@entry_id:176084), optimality is characterized by the Karush-Kuhn-Tucker (KKT) conditions. These conditions comprise multiple parts: primal feasibility (constraints are satisfied), [dual feasibility](@entry_id:167750) (conditions on the Lagrangian multipliers), and complementarity (a condition linking primal variables and dual [slack variables](@entry_id:268374)). A reliable stopping criterion must monitor progress toward satisfying all parts of the KKT conditions.

A particularly sophisticated example is found in **[primal-dual interior-point methods](@entry_id:637906) (IPMs)** for linear programming. These algorithms maintain primal iterates $x$, dual iterates $y$, and dual [slack variables](@entry_id:268374) $s$. Termination is based on satisfying three conditions simultaneously:
1.  **Primal Feasibility:** The norm of the primal residual, $\|r_{\text{pri}}\| = \|Ax - b\|$, must be small.
2.  **Dual Feasibility:** The norm of the dual residual, $\|r_{\text{dual}}\| = \|A^\top y + s - c\|$, must be small.
3.  **Complementarity:** The average complementarity gap, $\mu_{\text{comp}} = x^\top s / n$, must be small.

A typical [stopping rule](@entry_id:755483) is:
$$
\|r_{\text{pri}}\| \le \varepsilon_{\text{feas}}, \quad \|r_{\text{dual}}\| \le \varepsilon_{\text{feas}}, \quad \text{and} \quad \mu_{\text{comp}} \le \varepsilon_{\mu}
$$
These algorithms are guided by a **barrier parameter** $\mu$, which is gradually driven to zero. The logic for updating $\mu$ is intertwined with the stopping criteria. Robust IPMs will only decrease $\mu$ when the iterate is sufficiently "central," meaning the feasibility residuals are small relative to the current complementarity gap. This ensures stable progress towards a solution that satisfies all three KKT conditions [@problem_id:3187939].

### Summary and Practical Recommendations

The design and application of stopping criteria are a crucial component of numerical optimization, requiring a deep understanding of both the underlying theory and the practical characteristics of the problem at hand. We can distill the preceding principles into a set of practical recommendations:

-   **No Single Criterion is Foolproof:** Relying on a single, simplistic criterion is dangerous. A small change in iterates does not guarantee proximity to a solution, and a small gradient does not guarantee a small error in function value, especially in ill-conditioned or poorly scaled problems.

-   **Use a Combination of Criteria:** A robust implementation should always include a limit on the maximum number of iterations to prevent infinite loops. The primary [stopping rule](@entry_id:755483) should be based on a measure of optimality (e.g., a scaled norm of the gradient or its appropriate generalization). This can be supplemented with a progress-based criterion to detect stagnation.

-   **Prioritize Optimality-Based Measures:** The most reliable criteria are those that approximate the problem's first-order [optimality conditions](@entry_id:634091). For unconstrained smooth problems, this is $\|\nabla f(x_k)\|$; for constrained or non-smooth problems, this involves generalized measures like the projected gradient or proximal-gradient mapping.

-   **Respect Scaling and Geometry:** Always be mindful of the scale and units of your problem variables. Non-dimensionalize or use properly scaled norms to ensure your criteria are meaningful and robust. If using a preconditioned algorithm, consider a stopping test consistent with the algorithm's induced geometry.

-   **Choose Tolerances Wisely:** The choice of tolerance values ($\varepsilon$) is problem-dependent and reflects the desired trade-off between solution accuracy and computational resources. There is no universal "correct" value; it must be determined based on the application's requirements.

Ultimately, a stopping criterion is a sophisticated heuristic. Its effectiveness hinges on its ability to faithfully reflect the mathematical structure of the optimization problem and the geometric intuition of the algorithm designed to solve it.