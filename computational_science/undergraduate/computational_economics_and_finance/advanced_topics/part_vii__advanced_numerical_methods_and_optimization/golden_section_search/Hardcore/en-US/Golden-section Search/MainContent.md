## Introduction
Optimization is a fundamental pillar of [computational economics](@entry_id:140923) and finance, where finding the best possible outcome under a given set of constraints is a constant objective. While many classical [optimization techniques](@entry_id:635438) rely on calculus, a significant class of real-world problems involves objective functions that are non-differentiable, computationally expensive to evaluate, or available only as a "black box" through simulation. This gap necessitates robust and efficient **[derivative-free optimization](@entry_id:137673)** methods. The Golden-section search stands out as one of the most elegant and foundational algorithms in this category.

This article provides a deep dive into the Golden-section search, guiding you from its theoretical underpinnings to its practical applications. The first chapter, **Principles and Mechanisms**, will deconstruct the algorithm, explaining the critical concept of unimodality and the mathematical reasoning that makes the golden ratio the optimal choice for interval reduction. Next, **Applications and Interdisciplinary Connections** will showcase the method's versatility, exploring its use in solving problems in finance, economics, machine learning, and engineering. Finally, the **Hands-On Practices** section will offer concrete programming exercises to solidify your understanding and allow you to implement the algorithm in practical scenarios.

## Principles and Mechanisms

In the preceding chapter, we introduced the broad challenge of optimization in economics and finance. We now transition from the conceptual overview to the specific mechanics of a foundational algorithm. Many optimization problems, particularly those emerging from complex simulations or dealing with non-analytical objective functions, cannot be solved using methods that rely on derivatives. For these scenarios, we must turn to **[derivative-free optimization](@entry_id:137673)** techniques. This chapter delves into the principles of one of the most elegant and efficient of these methods: the Golden-section Search. We will build the algorithm from first principles, understand the mathematical reasoning behind its design, and explore its performance characteristics and practical limitations.

### The Prerequisite of Unimodality

The core strategy of many one-dimensional derivative-free methods is to find a minimum by iteratively shrinking an interval that is guaranteed to contain it. This "bracketing" approach is only valid under a key assumption about the function's shape within the search interval: **unimodality**.

A function $f(x)$ is said to be **strictly unimodal** on an interval $[a, b]$ if it possesses a single unique minimizer, $x^{\star}$, within that interval, and is strictly decreasing for all $x \in [a, x^{\star})$ and strictly increasing for all $x \in (x^{\star}, b]$. Visually, this corresponds to a function shape with a single valley. This property is crucial because it allows us to make definitive conclusions about where the minimum *cannot* be. If we evaluate the function at two interior points, $c$ and $d$, where $a  c  d  b$, a comparison of their values, $f(c)$ and $f(d)$, allows us to discard a portion of the interval. For instance, if we find that $f(c)  f(d)$, the unimodality assumption ensures that the minimum cannot lie in the subinterval $(d, b]$, allowing us to shrink our search space to the new interval $[a, d]$.

The unimodality assumption is not merely a theoretical convenience. It holds for any strictly [convex function](@entry_id:143191), which is a common and important class of functions in [economic modeling](@entry_id:144051). For instance, when Golden-section search is used as a **line search** sub-problem within a larger [multidimensional optimization](@entry_id:147413) algorithm like the Conjugate Gradient method, the objective is to minimize a function of a single variable $\alpha$, given by $\phi_k(\alpha) = f(\mathbf{x}_k + \alpha\mathbf{p}_k)$. If the main objective function $f(\mathbf{x})$ is strictly convex, the resulting one-dimensional function $\phi_k(\alpha)$ is also strictly convex and therefore unimodal, justifying the use of a method like Golden-section search .

However, if this core assumption is violated—for example, if a function has two distinct local minima within the initial search interval—the guarantees of the [search algorithm](@entry_id:173381) are voided. The algorithm itself will not fail in a computational sense; it will continue to shrink the interval based on its mechanical rules. Yet, it may "silently" discard the region containing the true [global minimum](@entry_id:165977) based on an early comparison, ultimately converging to a merely local minimum. The algorithm has no intrinsic diagnostic to detect non-unimodality; the interval will continue to shrink predictably, giving no outward sign that its fundamental premise has been violated . This underscores the importance of ensuring the unimodality condition holds, often by first using a bracketing routine to identify a suitable starting interval .

A notable strength of the Golden-section search is that it does *not* require the function to be differentiable. Its logic relies solely on comparing function values. This means it can be successfully applied to continuous functions that have "kinks" or "corners," such as $f(x) = |x^2 - c|$, as long as the search is restricted to an interval on which the function is unimodal. For example, on the interval $[0, u]$ with $u > \sqrt{c}$, the function $f(x)=|x^2-c|$ is unimodal with its minimum at the non-differentiable point $x=\sqrt{c}$, and Golden-section search will correctly converge to it .

### The Golden-Section Search: An Optimal Bracketing Strategy

Having established the importance of unimodality, we now construct the algorithm. Our goal is to devise a bracketing strategy that is as efficient as possible, where efficiency is measured by the number of function evaluations required to narrow the interval of uncertainty to a desired width. Since function evaluations can be computationally expensive—for example, when each evaluation involves running a complex economic simulation—minimizing their number is paramount .

Let our current interval of uncertainty be $[a, b]$, with length $L = b - a$. We introduce two interior test points, $c$ and $d$, where $a  c  d  b$. We evaluate $f(c)$ and $f(d)$ and apply the update rule for minimization:
- If $f(c)  f(d)$, the new interval becomes $[a, d]$.
- If $f(d) \le f(c)$, the new interval becomes $[c, b]$.

The key question is: where should we place $c$ and $d$? A naive choice, such as placing them to trisect the interval, is possible. However, the true genius of the Golden-section search lies in placing the points in such a way that one of the interior points from the current iteration can be reused in the next, thereby requiring only **one new function evaluation** per iteration after the first.

Let's formalize this. Suppose we want the new interval to have a length of $kL$ for some fixed reduction factor $k \in (0.5, 1)$, regardless of the outcome. To achieve this, the points must be placed symmetrically. For an interval normalized to $[0, 1]$, the new interval must be $[0, k]$ or $[1-k, 1]$. This forces the test points to be at $x_1 = 1-k$ and $x_2 = k$.

Now, consider the case where the new interval becomes $[0, k]$. The old test point that remains is $x_1 = 1-k$. For this point to be reusable in the new interval, its position relative to the new interval must match one of the required test point proportions. That is, the old point $x_1$ must become the new $x_1'$ or $x_2'$. This leads to a geometric condition on the reduction factor $k$: for reuse to be possible in both reduction scenarios, $k$ must satisfy the quadratic equation $k^2 + k - 1 = 0$ .

Solving for the positive root of this equation gives:
$$ k = \frac{-1 + \sqrt{1^2 - 4(1)(-1)}}{2} = \frac{\sqrt{5}-1}{2} \approx 0.618034 $$
This special number is the reciprocal of the **[golden ratio](@entry_id:139097)**, $\phi = \frac{1+\sqrt{5}}{2} \approx 1.618034$. Thus, the Golden-section search is not just an arbitrary algorithm; it is the unique bracketing search strategy that achieves a constant interval reduction while requiring only one new function evaluation per iteration. Any other choice of a fixed reduction factor $k$ (for instance, placing one point at the midpoint) breaks the geometric [self-similarity](@entry_id:144952) and would necessitate two new function evaluations in the worst case, making the search less efficient  .

#### The Algorithm in Practice

Let's summarize the procedure for minimizing a [unimodal function](@entry_id:143107) $f(x)$ on an initial interval $[a_0, b_0]$.

1.  **Initialization**: Define the golden ratio factor $\rho = \frac{\sqrt{5}-1}{2}$. Set the current interval $[a, b] = [a_0, b_0]$. Calculate two initial interior points:
    $$ c = b - \rho(b - a) $$
    $$ d = a + \rho(b - a) $$
    Evaluate the function at these two points, $f(c)$ and $f(d)$.

2.  **Iteration**: Repeat the following until the interval width $(b-a)$ is smaller than a desired tolerance:
    - If $f(c)  f(d)$: The new interval is $[a, d]$. Set $b \leftarrow d$. The old point $c$ becomes the new $d$. We only need to compute one new point: $d \leftarrow c$, and $c \leftarrow b - \rho(b-a)$. Evaluate the new $f(c)$.
    - If $f(d) \le f(c)$: The new interval is $[c, b]$. Set $a \leftarrow c$. The old point $d$ becomes the new $c$. We only need to compute one new point: $c \leftarrow d$, and $d \leftarrow a + \rho(b-a)$. Evaluate the new $f(d)$.

3.  **Termination**: The final interval $[a, b]$ brackets the minimizer. An estimate of the minimizer $x^{\star}$ is often given by the midpoint of this final interval, $\frac{a+b}{2}$.

To solve a maximization problem for a function $\eta(x)$, one can simply apply the minimization algorithm to the function $g(x) = -\eta(x)$ .

**Illustrative Example:**
Let's apply three iterations of GSS to maximize the function $\eta(\alpha)$ from problem  on the interval $[1.5, 3.0]$. This is equivalent to minimizing $f(\alpha) = -\eta(\alpha)$. The update rule for maximization states that if $\eta(c) > \eta(d)$, the new interval is $[a, d]$; otherwise, it is $[c, b]$. Let $\rho = (\sqrt{5}-1)/2 \approx 0.618$.

-   **Iteration 1**:
    -   $[a_0, b_0] = [1.5, 3.0]$. Length is $1.5$.
    -   $c_1 = 3.0 - \rho(1.5) \approx 2.073$, $d_1 = 1.5 + \rho(1.5) \approx 2.427$.
    -   Evaluations give $\eta(c_1) \approx 1.058$ and $\eta(d_1) \approx 1.063$.
    -   Since $\eta(d_1) > \eta(c_1)$, the new interval is $[a_1, b_1] = [c_1, b_0] = [2.073, 3.0]$.

-   **Iteration 2**:
    -   $[a_1, b_1] = [2.073, 3.0]$. Length is $0.927$.
    -   The old $d_1$ becomes the new $c_2$. So, $c_2 = 2.427$. We only compute $d_2 = a_1 + \rho(b_1 - a_1) \approx 2.646$.
    -   We reuse $\eta(c_2) = \eta(d_1) \approx 1.063$. We compute $\eta(d_2) \approx 0.916$.
    -   Since $\eta(c_2) > \eta(d_2)$, the new interval is $[a_2, b_2] = [a_1, d_2] = [2.073, 2.646]$.

-   **Iteration 3**:
    -   $[a_2, b_2] = [2.073, 2.646]$. Length is $0.573$.
    -   The old $c_2$ becomes the new $d_3$. So $d_3 = 2.427$. We compute $c_3 = b_2 - \rho(b_2 - a_2) \approx 2.292$.
    -   We reuse $\eta(d_3) = \eta(c_2) \approx 1.063$. We compute $\eta(c_3) \approx 1.096$.
    -   Since $\eta(c_3) > \eta(d_3)$, the new interval is $[a_3, b_3] = [a_2, d_3] = [2.073, 2.427]$.

The midpoint of the final interval $[2.073, 2.427]$ is approximately $2.250$, which is our estimate for the optimal parameter $\alpha$.

### Performance Analysis and Comparisons

The efficiency of an algorithm is best understood by analyzing its convergence rate and comparing it to alternatives.

The Golden-section search exhibits **[linear convergence](@entry_id:163614)**. This means the error (represented by the interval length) decreases by a constant factor, $\rho \approx 0.618$, at each iteration. Consequently, the number of function evaluations, $N$, required to reduce an initial interval of length $L_0$ to a final width of $\epsilon$ scales logarithmically with the required precision: $N \propto \ln(L_0 / \epsilon)$.

-   **GSS vs. Uniform Sampling**: A naive approach might be to simply evaluate the function at $N$ evenly spaced points across the interval (a grid or uniform search). To guarantee a final uncertainty interval of length $\epsilon$, this method requires a number of evaluations that scales linearly with the precision, $N \propto L_0 / \epsilon$. The logarithmic scaling of GSS versus the [linear scaling](@entry_id:197235) of uniform sampling means that for high-precision requirements (very small $\epsilon$), GSS is orders of magnitude more efficient. In a scenario where function evaluations are costly, this difference is critical .

-   **GSS vs. Trisection Search**: A more plausible alternative is the **Trisection Search**, where at each step, the interval is divided into three equal parts by two interior points. After comparison, two-thirds of the interval is retained. While the reduction factor of $2/3 \approx 0.667$ seems comparable to GSS's $0.618$, trisection search cannot reuse function evaluations and thus requires two new evaluations per iteration. When a fair comparison is made on a per-evaluation basis, GSS is demonstrably superior. The interval reduction per *evaluation* for GSS is $\rho \approx 0.618$, while for trisection it is $\sqrt{2/3} \approx 0.816$. Since a smaller factor indicates faster convergence, GSS is the more efficient algorithm. Asymptotically, trisection requires about $2.37$ times more function evaluations than GSS to achieve the same tolerance .

### Practical Implementation and Advanced Considerations

Beyond the core algorithm, several practical issues arise during implementation.

#### Choice of Termination Criterion

How do we decide when to stop the search? Two common criteria are:
1.  **Interval-length criterion**: Stop when the interval width $|b-a|$ is less than a tolerance $\epsilon$.
2.  **Function-value criterion**: Stop when the difference in function values at the endpoints, $|f(b) - f(a)|$, is less than a tolerance $\delta$.

For Golden-section search, the interval-length criterion is almost always preferred due to its robustness. The number of iterations required to meet this criterion is predictable and depends only on the initial interval width and $\epsilon$, not on the function's specific shape. It directly guarantees a certain precision in the *location* of the minimum, $x^{\star}$ .

The function-value criterion, however, can be unreliable, especially for functions with a very **flat minimum**. In such cases, a very large change in the input $x$ can result in a minuscule change in the output $f(x)$. The search might terminate because $|f(b)-f(a)|$ is small, while the interval $[a,b]$ itself is still very wide, leading to poor accuracy in locating $x^{\star}$. To make the function-value criterion safe for a function whose local behavior is like $|x-x^{\star}|^p$ (where large $p$ indicates flatness), the tolerance $\delta$ must be chosen to be on the order of $\epsilon^p$, which requires prior knowledge about the function's shape .

#### Role in Multidimensional Optimization

While powerful for one-dimensional problems, GSS often serves as a component within more complex algorithms for [multidimensional optimization](@entry_id:147413). For example, many methods iterate via $\mathbf{x}_{k+1} = \mathbf{x}_k + \alpha_k \mathbf{p}_k$, where $\mathbf{p}_k$ is a search direction and $\alpha_k$ is a step length found by solving the one-dimensional [line search](@entry_id:141607) problem: $\min_{\alpha} f(\mathbf{x}_k + \alpha \mathbf{p}_k)$. GSS is a candidate for solving this sub-problem.

However, using GSS in this context involves trade-offs. Its derivative-free nature is an advantage, but because it provides an *inexact* solution to the [line search](@entry_id:141607) (up to a tolerance), it can disrupt theoretical properties of the parent algorithm. For instance, the Conjugate Gradient method's celebrated property of terminating in at most $n$ steps for a quadratic function in $\mathbb{R}^n$ relies on an [exact line search](@entry_id:170557). Using GSS with a finite tolerance breaks this guarantee . Furthermore, more advanced [line search strategies](@entry_id:636391) are designed to satisfy specific gradient-based criteria, such as the **Wolfe conditions**, which ensure both [sufficient decrease](@entry_id:174293) in the function value and progress away from steep regions. As a derivative-free method, GSS cannot check or enforce these conditions .

In summary, the Golden-section search is a powerful, elegant, and optimally efficient algorithm for [one-dimensional optimization](@entry_id:635076) of unimodal functions without derivatives. Its strength lies in its simplicity, robustness, and minimal data requirements—relying only on the ordinal comparison of function values. Understanding its underlying principles, from the necessity of unimodality to the geometric optimality of the golden ratio, provides a solid foundation for tackling a wide range of optimization challenges in [computational economics](@entry_id:140923) and finance.