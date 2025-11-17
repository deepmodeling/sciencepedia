## Introduction
Dynamic models are the cornerstone of modern economic analysis, finance, and numerous other scientific fields. They allow us to study the evolution of systems over time, from capital accumulation in an economy to the trajectory of a spacecraft. However, the models that most accurately capture real-world complexity—featuring nonlinearities, uncertainty, and high dimensionality—rarely have a closed-form, analytical solution. Their behavior is instead defined by intractable [functional equations](@entry_id:199663), such as the Bellman or Euler equations, which poses a significant computational challenge. How can we solve for the optimal policies and value functions that are the key outputs of these models?

Projection methods offer a powerful and versatile answer to this question. This class of numerical techniques transforms the infinite-dimensional problem of finding an unknown function into a manageable, finite-dimensional problem of finding a set of coefficients for a well-chosen approximation. This article serves as a comprehensive guide to understanding and implementing these methods. It is structured to build your expertise from the ground up across three chapters.

First, **Principles and Mechanisms** will deconstruct the core theory, explaining how to approximate functions, set up the collocation system, and choose essential building blocks like basis functions and approximation domains. Next, **Applications and Interdisciplinary Connections** will broaden the horizon, showcasing how these methods solve pressing problems in economics—from models with frictions to agent-based learning—and connect to parallel concepts like Reduced-Order Modeling in engineering and physics. Finally, **Hands-On Practices** will provide opportunities to apply this knowledge, guiding you through coding and validating solutions for canonical economic models. By the end, you will have a robust framework for tackling a wide array of complex dynamic problems.

## Principles and Mechanisms

Projection methods constitute a powerful class of numerical techniques for solving the [functional equations](@entry_id:199663) that arise from dynamic economic models. Unlike methods that discretize the state space and solve for the unknown function at each grid point, [projection methods](@entry_id:147401) seek to find an approximate solution that is valid over a continuous domain. This is achieved by "projecting" the infinite-dimensional problem of finding a function onto a finite-dimensional problem of finding a set of parameters for a chosen approximating function. This chapter elucidates the core principles and mechanisms of these methods, from foundational concepts to advanced practical considerations.

### From Functional Equations to Finite-Dimensional Systems

Dynamic [optimization problems](@entry_id:142739), whether framed in discrete or continuous time, are typically characterized by a [functional equation](@entry_id:176587), such as a Bellman equation or a Hamilton-Jacobi-Bellman equation. The solution to this equation is an unknown function, such as a **[value function](@entry_id:144750)** $V(\cdot)$ or a **[policy function](@entry_id:136948)** $g(\cdot)$ that maps states to controls. For example, in a standard neoclassical growth model, the Bellman equation is:

$$
V(k) = \max_{c, k'} \{u(c) + \beta V(k')\} \quad \text{s.t.} \quad c+k' = f(k)
$$

The solution to this problem is the value function $V(k)$ and the associated optimal [policy function](@entry_id:136948) for next-period capital, $k' = g(k)$. The core challenge is that these functions are infinite-dimensional objects. Projection methods address this by postulating that the unknown function can be well-approximated by a parameterized function from a known family. This approximation, denoted $\hat{g}(k; \theta)$, is typically a linear combination of pre-selected **basis functions** $\phi_j(k)$:

$$
g(k) \approx \hat{g}(k; \theta) = \sum_{j=1}^{N} \theta_j \phi_j(k)
$$

Here, $\theta = (\theta_1, \dots, \theta_N)$ is a finite-dimensional vector of coefficients. The problem is thus transformed from finding an unknown function $g(k)$ to finding the optimal $N$-dimensional vector $\theta$.

Once an approximate functional form is chosen, we must define what makes a particular parameter vector $\theta$ "best." This is done by measuring how well the approximate solution satisfies the original functional equation. Substituting $\hat{g}(k; \theta)$ into the governing equation (e.g., the Bellman or Euler equation) yields a **residual function**, $R(k; \theta)$, which is nonzero when the approximation is not exact.

The projection step involves choosing $\theta$ to make this residual "small." The most common approach is **collocation**, which forces the residual to be exactly zero at a predetermined, finite set of $N$ points in the state space, known as **collocation nodes** $\{k_i\}_{i=1}^N$. This procedure generates a system of $N$ equations in $N$ unknown coefficients:

$$
R(k_i; \theta) = 0, \quad \text{for } i = 1, \dots, N
$$

Solving this system yields the coefficient vector $\theta^\star$ that defines the approximate solution.

### Value Function vs. Euler Equation Projection

There are two primary approaches to implementing [projection methods](@entry_id:147401), distinguished by the [functional equation](@entry_id:176587) they target.

#### Projection on the Bellman Equation (Value Function Iteration)

One approach is to approximate the value function, $V(k) \approx \hat{V}(k; \theta) = \sum_{j=1}^N \theta_j \phi_j(k)$. The coefficients $\theta$ are found by iterating on the Bellman operator. At each iteration, one solves for an updated set of coefficients $\theta^{(n+1)}$ that satisfy the Bellman equation at the collocation nodes, given the current approximation $\hat{V}(k; \theta^{(n)})$ for the [continuation value](@entry_id:140769):

$$
\hat{V}(k_i; \theta^{(n+1)}) = \max_{k'} \{u(f(k_i) - k') + \beta \hat{V}(k'; \theta^{(n)})\} \quad \text{for } i = 1, \dots, N
$$

This method, often called [value function iteration](@entry_id:140921) (VFI) with approximation, can be computationally demanding. Each iteration requires solving $N$ separate optimization problems to handle the maximization on the right-hand side. Furthermore, while the Bellman operator is a contraction mapping for the true value function, this property does not guarantee rapid convergence for the coefficient vector $\theta$.

#### Projection on the Euler Equation

A more direct and often more efficient approach is to approximate the [policy function](@entry_id:136948) $g(k)$ and collocate on the intertemporal **Euler equation**. The Euler equation is a [first-order necessary condition](@entry_id:175546) for optimality that relates marginal utility across adjacent periods. For the neoclassical growth model, it is:

$$
u'(c) = \beta \mathbb{E}[u'(c')(f'(k') + 1 - \delta)]
$$

Here, $c = f(k) - g(k)$ and $c' = f(g(k)) - g(g(k))$. The key advantage is that the Euler equation is a direct equation for the [policy function](@entry_id:136948) $g(k)$, bypassing the need to approximate the value function.

The procedure, as demonstrated in the context of a deterministic growth model [@problem_id:2422853], is as follows:
1.  **Parameterize the Policy:** Define an approximate [policy function](@entry_id:136948) $\hat{g}(k; \theta)$. For example, one could parameterize the consumption function $c(k; \theta)$ or, to ensure feasibility, the saving rate.
2.  **Form the Residual:** For any state $k$ and parameter vector $\theta$, the policy implies current consumption $c$, next-period capital $k'$, and next-period consumption $c'$. These can be plugged into the Euler equation to form a residual, often expressed in normalized form:
    $$
    R(k; \theta) = 1 - \frac{\beta u'(c')(f'(k') + 1 - \delta)}{u'(c)}
    $$
3.  **Collocate and Solve:** Set up the system of $N$ nonlinear equations $R(k_i; \theta) = 0$ at the chosen collocation nodes $\{k_i\}_{i=1}^N$. This system is then solved for $\theta$ using a [numerical root-finding](@entry_id:168513) algorithm.

As a direct comparison shows [@problem_id:2422765], Euler Equation Projection (EEP) is typically significantly faster than VFI. EEP requires solving a single system of nonlinear equations once, whereas VFI requires an outer loop of Bellman iterations, each containing an inner loop of costly optimization problems. Moreover, by construction, EEP delivers an Euler equation residual of zero (up to numerical tolerance) at the collocation nodes, which is the specific metric of economic accuracy often used. The [policy function](@entry_id:136948) derived from VFI does not generally satisfy this property due to [approximation error](@entry_id:138265) in the [value function](@entry_id:144750)'s derivative.

### The Essential Building Blocks

The success of any [projection method](@entry_id:144836) hinges on a series of crucial design choices. These choices are not independent; they interact to determine the accuracy, stability, and efficiency of the entire procedure.

#### Choice of Basis Functions

The basis functions $\{\phi_j(k)\}$ are the foundation of the approximation. The ideal basis can represent the true, unknown function with high accuracy using a small number of terms ($N$).

A seemingly simple choice is the **monomial basis**, $\{1, k, k^2, \dots, k^{N-1}\}$. However, this is a notoriously poor choice for all but the lowest-degree approximations. As the degree increases, the basis functions become nearly linearly dependent on any given interval. This leads to a collocation matrix that is extremely **ill-conditioned**, a problem that grows exponentially with the degree. Solving the resulting linear algebra problems becomes numerically unstable, making it impossible to find reliable coefficients [@problem_id:2422813].

A far superior choice for functions on a compact interval is a basis of **orthogonal polynomials**, such as **Chebyshev polynomials**. These polynomials are defined on the interval $[-1, 1]$ and possess properties that make them ideal for approximation. While the collocation matrix is not strictly orthogonal, it is extremely well-conditioned, especially when paired with a judicious choice of collocation nodes. The condition number grows only logarithmically with the degree, allowing for stable and accurate high-degree polynomial approximations [@problem_id:2422813]. To use these polynomials, it is essential to first perform an affine transformation of the model's state variable from its natural domain $[k_{\min}, k_{\max}]$ to the Chebyshev domain $[-1, 1]$. Failing to do so destroys the beneficial properties of the basis and leads to severe [ill-conditioning](@entry_id:138674) [@problem_id:2422813] [@problem_id:2422786].

For problems with an inherently [periodic structure](@entry_id:262445), such as models with seasonal cycles, neither monomials nor Chebyshev polynomials are the most natural choice. Instead, a **Fourier basis** of [sine and cosine functions](@entry_id:172140) is superior. A truncated Fourier series is inherently periodic, automatically satisfying boundary conditions that would need to be explicitly enforced with a polynomial basis. This makes them more efficient and elegant for such problems [@problem_id:2422828]. Furthermore, differentiation is transformed into a simple algebraic multiplication of the coefficients in the frequency domain, a key advantage for computational efficiency [@problem_id:2422828].

#### Choice of Domain and Nodes

The **approximation domain**, $[k_{\min}, k_{\max}]$, must be chosen with care. This domain should encompass the region of the state space where the system is expected to operate, known as the **ergodic set**. If the domain is chosen too narrowly, the simulated state may frequently exit it. When this happens, the method breaks down. To evaluate the expectation in the Euler equation, the algorithm needs to evaluate the [policy function](@entry_id:136948) at a future state $k'$ which may lie outside $[k_{\min}, k_{\max}]$. The behavior of polynomial approximations outside their defined interval is uncontrolled and often wildly inaccurate (extrapolation error). This invalidates the accuracy of the entire solution, even for states inside the domain, and leads to biased results if one simulates the model. Practical "fixes" like clipping the state to the boundary simply mean that one is simulating a different, distorted economic model [@problem_id:2422806].

The choice of **collocation nodes** is also critical and is tightly linked to the choice of basis. For a Chebyshev polynomial basis, selecting the nodes to be the roots or extrema of a higher-order Chebyshev polynomial (e.g., Chebyshev-Gauss or Chebyshev-Gauss-Lobatto nodes) is the standard and optimal approach. This choice minimizes [interpolation error](@entry_id:139425) and, as noted, helps ensure the collocation matrix is well-conditioned [@problem_id:2422813].

#### Handling Higher Dimensions: The Curse of Dimensionality

When models feature multiple state variables ($d > 1$), the most straightforward approach is to build a grid using a **[tensor product](@entry_id:140694)** of one-dimensional node sets. If each dimension uses $m$ nodes, the total number of collocation nodes becomes $m^d$. This exponential growth in computational cost with dimension is known as the **curse of dimensionality**, and it renders tensor-product methods infeasible for $d \ge 4$ or $5$.

For such problems, **sparse grid** methods provide a powerful remedy. A sparse grid, constructed using the Smolyak algorithm, is a specific combination of smaller tensor-product grids at different levels of resolution. It achieves a given approximation accuracy with far fewer points than a full tensor grid. For a target one-dimensional resolution $m$, the number of points on a standard sparse grid scales as $O(m (\log m)^{d-1})$ instead of $O(m^d)$. This dramatic reduction in computational cost makes it possible to solve moderately high-dimensional problems that would be completely intractable with tensor grids [@problem_id:2422831].

### Implementation: Solvers and Accuracy

After setting up the collocation system $R(\theta) = 0$, one must solve it. Since the residual function is typically nonlinear, this requires an iterative [root-finding algorithm](@entry_id:176876).

Common choices include **Newton's method** and **quasi-Newton methods** like Broyden's method. Newton's method offers fast (quadratic) local convergence but requires the computation of the Jacobian matrix $\partial R / \partial \theta$ at each iteration, which can be analytically complex or computationally expensive. Broyden's method avoids this by building up an approximation to the Jacobian using only information from the residual evaluations. It converges more slowly (superlinearly) but can be faster overall if the cost of evaluating the true Jacobian is very high [@problem_id:2422778].

A critical practical challenge is that these solvers are generally guaranteed to converge only if the initial guess, $\theta^{(0)}$, is sufficiently close to the true solution $\theta^\star$. A poor initial guess can cause the solver to diverge or, more commonly, to propose a step that violates an economic constraint, such as non-negativity of consumption or capital. For instance, an initial guess might imply a consumption level so high that next-period capital becomes negative, causing the algorithm to fail when it attempts to evaluate the [policy function](@entry_id:136948) at this undefined state [@problem_id:2422786]. Robust implementations therefore require good initial guesses (e.g., based on the model's steady state [@problem_id:2422853]) and "globalization" strategies like [backtracking line search](@entry_id:166118) or imposing explicit bounds to ensure iterates remain in an economically feasible region [@problem_id:2422786].

Finally, since the result is an approximation, its accuracy must be verified. The standard practice is to compute the Euler equation residual on a very fine **validation grid** of points that is independent of the collocation nodes. The maximum absolute residual on this grid (the [supremum norm](@entry_id:145717)) serves as a robust measure of the solution's economic error. A small sup-norm indicates that the approximate policy nearly satisfies the optimality condition across the entire domain [@problem_id:2422853].

### Advanced Considerations

The performance of [projection methods](@entry_id:147401) is also deeply intertwined with the economic structure of the model itself. For example, in models with CRRA utility, the curvature parameter $\sigma$ (the coefficient of relative [risk aversion](@entry_id:137406)) has a profound impact on numerical difficulty. A higher $\sigma$ implies a stronger desire for [consumption smoothing](@entry_id:145557), which often leads to a true [policy function](@entry_id:136948) that is highly curved. It also makes the marginal utility function $u'(c) = c^{-\sigma}$ extremely sensitive to small errors in consumption, especially where consumption is low. Together, these effects mean that problems with high $\sigma$ are more nonlinear and harder to approximate accurately. They may require higher-degree polynomial bases, a denser concentration of collocation nodes in low-consumption regions, or more sophisticated solver strategies to achieve convergence [@problem_id:2422787].

Furthermore, in stochastic models, solving the system requires computing an expectation in the Euler residual, which is done via numerical quadrature. The accuracy of this integration is another key component of the overall error. The choice of the number of quadrature nodes ($M$) relative to the number of basis functions ($N$) is a non-trivial resource allocation problem. For a fixed computational budget, there is an optimal balance between improving the [function approximation](@entry_id:141329) (increasing $N$) and improving the integral approximation (increasing $M$). The guiding principle is to balance the sources of error, choosing $N$ and $M$ such that the approximation error and [quadrature error](@entry_id:753905) decay at the same rate as the computational budget grows [@problem_id:2422777]. This ensures that no single source of error becomes the bottleneck to achieving a more accurate solution.