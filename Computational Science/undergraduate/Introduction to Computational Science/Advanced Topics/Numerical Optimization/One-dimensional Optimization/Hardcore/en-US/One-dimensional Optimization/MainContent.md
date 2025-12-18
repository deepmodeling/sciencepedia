## Introduction
One-dimensional optimization, often called [line search](@entry_id:141607), is a foundational problem in computational science: finding the minimum of a function of a single variable. While many modern challenges involve optimizing over millions of variables, the principles of [one-dimensional search](@entry_id:172782) remain indispensable. They not only provide the building blocks for understanding more complex algorithms but also serve as critical subroutines within them. This article addresses the core question of how to efficiently and reliably find a function's minimum, particularly in common scenarios where derivative information is unavailable or untrustworthy.

Across three chapters, you will embark on a journey from theory to application. The first chapter, **Principles and Mechanisms**, will dissect the core logic of derivative-free search, deriving the elegant and robust Golden-Section Search algorithm from first principles. Next, **Applications and Interdisciplinary Connections** will reveal how this technique is a workhorse in fields ranging from machine learning to engineering design, both as a direct tuning method and as a [line search](@entry_id:141607) component in [multidimensional optimization](@entry_id:147413). Finally, **Hands-On Practices** will guide you through implementing the algorithm, preparing you to solve real-world [optimization problems](@entry_id:142739).

## Principles and Mechanisms

One-dimensional optimization, or [line search](@entry_id:141607), forms a foundational component of computational science and [numerical optimization](@entry_id:138060). It addresses the seemingly simple problem of finding the minimum of a function of a single variable, $f(x)$, within a given interval. While modern computational methods often tackle problems with millions of variables, the principles elucidated through [one-dimensional search](@entry_id:172782) are not only fundamental to understanding more complex algorithms but also serve as critical sub-problems within them. This chapter explores the principles and mechanisms of derivative-free [line search methods](@entry_id:172705), focusing on the elegant and robust Golden-Section Search algorithm.

### The Foundational Principle of Unimodality

The most robust class of one-dimensional optimization algorithms, known as **[bracketing methods](@entry_id:145720)**, relies on a single, crucial property of the objective function: **unimodality**. A function $f(x)$ is defined as **unimodal** on an interval $[a, b]$ if it possesses a single minimum in that interval. More formally, there exists a unique value $x^{\star} \in [a, b]$ such that $f(x)$ is monotonically decreasing for $x \in [a, x^{\star}]$ and monotonically increasing for $x \in [x^{\star}, b]$. This definition encompasses functions whose minimum occurs at a boundary (i.e., [monotonic functions](@entry_id:145115) on the interval) as well as those with an interior minimum.

The power of the unimodality assumption is that it allows us to shrink an interval of uncertainty without inadvertently discarding the minimizer. Consider an interval $[a, b]$ known to contain $x^{\star}$. If we evaluate the function at two distinct interior points, $x_L$ and $x_R$, such that $a  x_L  x_R  b$, we can make a definitive decision:

1.  If $f(x_L)  f(x_R)$, then the minimizer $x^{\star}$ cannot lie in the subinterval $[x_R, b]$. Why? If $x^{\star}$ were in $[x_R, b]$, then both $x_L$ and $x_R$ would have to be on the monotonically decreasing segment of the function, which would imply $f(x_L) > f(x_R)$, a contradiction. Therefore, the new, smaller interval of uncertainty must be $[a, x_R]$.

2.  If $f(x_L) \ge f(x_R)$, a symmetric argument holds. The minimizer cannot be in $[a, x_L]$, so the new interval of uncertainty becomes $[x_L, b]$.

This simple comparison logic is the engine of all bracketing search methods. However, it is critically dependent on the unimodality of $f(x)$ within the search interval. If this assumption is violated, the method can fail catastrophically. For example, attempting to minimize the function $f(x) = \sin(x)$ over an interval that spans multiple periods, such as $[0, 4\pi]$, will not succeed. Such an interval contains two minima (near $\frac{3\pi}{2}$ and $\frac{7\pi}{2}$) and is therefore not unimodal. A bracketing search initiated on this interval may incorrectly discard the subinterval containing the global minimum based on a single local comparison. It is therefore a prerequisite to ensure that the initial search interval brackets a single minimum .

### The Golden-Section Search: An Optimal Bracketing Strategy

The interval reduction logic begs a crucial question: where should we place the interior points $x_L$ and $x_R$ to achieve the most efficient search? The efficiency of a bracketing algorithm is measured by the number of function evaluations required to reduce the interval of uncertainty to a desired tolerance.

A simple approach, often called a **dichotomous search**, is to place the two points symmetrically around the midpoint of the interval, separated by a small distance $\delta$. For an interval $[a,b]$, the points would be $\frac{a+b}{2} - \delta$ and $\frac{a+b}{2} + \delta$. After the comparison, the interval is roughly halved. However, in the next iteration, the new interval has a new midpoint, and two entirely new function evaluations are required. The total number of function evaluations thus grows at twice the rate of the number of iterations .

A more intelligent strategy would be to choose the interior points such that one of them can be **reused** in the next iteration. This would reduce the computational cost to just one new function evaluation per iteration after the initial setup. Let's derive this optimal placement from first principles.

Consider a normalized interval $[0, 1]$. To maintain a consistent geometry, we choose the interior points $x_L$ and $x_R$ to have fixed fractional positions. For symmetry of interval reduction, the points should be placed symmetrically, i.e., $x_L = 1 - x_R$. Let's denote the fractional distance from the endpoints as $\rho$, so $x_R = \rho$ and $x_L = 1 - \rho$. For $x_L  x_R$, we need $\rho > \frac{1}{2}$.

Suppose our comparison finds $f(x_L) > f(x_R)$. The new interval becomes $[x_L, 1]$, which has a length of $1 - x_L = 1 - (1-\rho) = \rho$. The old point $x_R$ is contained within this new interval. The key idea is to choose $\rho$ such that the [relative position](@entry_id:274838) of the old point $x_R$ within the new interval $[x_L, 1]$ is identical to one of the original fractional positions, $1-\rho$ or $\rho$.

Let's map the new interval $[x_L, 1]$ back to $[0, 1]$. A point $z$ in $[x_L, 1]$ is mapped to $z' = \frac{z - x_L}{1-x_L}$. The old point $x_R$ is mapped to:
$$ x_R' = \frac{x_R - x_L}{1-x_L} = \frac{\rho - (1-\rho)}{\rho} = \frac{2\rho - 1}{\rho} $$
For the reuse condition, we demand that this new [relative position](@entry_id:274838) $x_R'$ be equal to one of the original symmetric positions. If we set $x_R' = \rho$, we get $2\rho-1 = \rho^2$, which is the quadratic equation:
$$ \rho^2 - 2\rho + 1 = (\rho-1)^2 = 0 $$
This gives $\rho=1$, a trivial solution corresponding to no interval reduction. The only other choice is to set the old right point $x_R$ to become the new left point, which means its new [relative position](@entry_id:274838) must be $1-\rho$:
$$ \frac{2\rho-1}{\rho} = 1-\rho \implies 2\rho-1 = \rho(1-\rho) = \rho - \rho^2 $$
Rearranging gives the celebrated equation:
$$ \rho^2 + \rho - 1 = 0 $$
The positive root of this equation is $\rho = \frac{\sqrt{5}-1}{2} \approx 0.61803$. This number is the reciprocal of the **[golden ratio](@entry_id:139097)** $\phi = \frac{1+\sqrt{5}}{2}$. The interval is reduced by this factor $\rho$ in every iteration.

This derivation gives rise to the **Golden-Section Search (GSS)** algorithm:

1.  **Initialization**: Given an interval $[a, b]$, define the constant $\rho = \frac{\sqrt{5}-1}{2}$. Calculate two interior points $x_L = b - \rho(b-a)$ and $x_R = a + \rho(b-a)$. Evaluate $f_L = f(x_L)$ and $f_R = f(x_R)$. This requires two function evaluations.
2.  **Iteration**: While the interval length $(b-a)$ is greater than a specified tolerance:
    *   If $f_L  f_R$: The new interval is $[a, x_R]$. Update $b \leftarrow x_R$. The old $x_L$ becomes the new $x_R$, so we update $x_R \leftarrow x_L$ and $f_R \leftarrow f_L$. Then, compute only one new point $x_L = b - \rho(b-a)$ and its function value $f_L = f(x_L)$.
    *   Else ($f_L \ge f_R$): The new interval is $[x_L, b]$. Update $a \leftarrow x_L$. The old $x_R$ becomes the new $x_L$, so we update $x_L \leftarrow x_R$ and $f_L \leftarrow f_R$. Then, compute only one new point $x_R = a + \rho(b-a)$ and its function value $f_R = f(x_R)$.
3.  **Termination**: The final estimate of the minimizer is the midpoint of the last interval, $\frac{a+b}{2}$.

The GSS algorithm's elegance lies in its efficiency. After initialization, it requires only one new function evaluation per iteration. This makes it significantly more efficient than a naive dichotomous search, which requires two. Although the GSS interval reduction factor ($\rho \approx 0.618$) is less aggressive than the dichotomous search's factor ($\approx 0.5$), the savings in function evaluations makes GSS the superior method for any practical problem . Furthermore, the algorithm is minimal in its memory requirements; at any given time, only the two most recent interior function values need to be stored to make the next decision .

### Properties and Invariance of the Golden-Section Search

The Golden-Section Search is not just efficient; it is also remarkably robust and possesses a fundamental geometric property that makes it widely applicable.

A key advantage of GSS is its **robustness to non-[differentiability](@entry_id:140863)**. The algorithm's logic relies only on the ordering of function values ($f(x_L)  f(x_R)$), not on their magnitude, and certainly not on their derivatives. This means GSS can be applied without modification to functions that are [continuous but not differentiable](@entry_id:261860). For instance, it can successfully navigate the "corners" of a piecewise-[smooth function](@entry_id:158037) where the derivative is discontinuous. The algorithm is blind to the smoothness of the function, asking only that it be unimodal .

Moreover, GSS exhibits **[scale invariance](@entry_id:143212)** in the [independent variable](@entry_id:146806). The placement of the interior points is based on fixed ratios of the current interval's length. This geometric construction means that the sequence of normalized interior point positions and the resulting decisions are invariant under any positive linear transformation of the coordinate system, $x \mapsto sx + t$ for $s > 0$. Consider a simple rescaling $x \mapsto sx$. The original problem seeks to minimize $f(x)$ on $[a, b]$, while the rescaled problem minimizes $g(y) = f(y/s)$ on $[sa, sb]$. The comparison at each step in the rescaled problem is $g(sc_k)$ versus $g(sd_k)$, which is identical to $f(c_k)$ versus $f(d_k)$. Since the decisions are identical at every step, the algorithm traces out the same path in a relative sense. This property is not just a theoretical curiosity; it has profound practical implications. It means the behavior of the algorithm is independent of the physical units chosen for the problem. Whether a parameter is measured in meters or millimeters, the GSS will perform the same number of iterations to achieve a given *relative* precision .

### Contextualizing Golden-Section Search: Comparison with Derivative-Based Methods

To fully appreciate the role of GSS, it is essential to compare it with methods that utilize derivative information.

#### Bisection Method on the Derivative

For a strictly convex and differentiable function, finding the unique minimizer $x^{\star}$ is equivalent to finding the unique root of its derivative, $f'(x^{\star}) = 0$. Since [strict convexity](@entry_id:193965) implies that $f'(x)$ is strictly increasing, we can use a [root-finding algorithm](@entry_id:176876) like the **[bisection method](@entry_id:140816)** on $f'(x)$. If we can find an interval $[a,b]$ where $f'(a)  0$ and $f'(b) > 0$, bisection is guaranteed to converge to $x^{\star}$.

*   **Convergence**: Bisection reduces the interval length by a factor of exactly $0.5$ per iteration, which is faster than GSS's factor of $\approx 0.618$.
*   **Requirements**: Bisection requires the ability to evaluate the first derivative, $f'(x)$.

The choice between GSS and bisection on $f'$ is a classic trade-off. If $f'(x)$ is readily available and computationally cheap, bisection is generally superior due to its faster convergence. However, in many real-world scenarios, the derivative is either analytically unavailable (e.g., $f(x)$ is a black-box simulation) or its evaluation is unreliable or noisy. In these cases, GSS is the more robust and often the only applicable choice  .

#### Newton's Method

A more powerful derivative-based approach is **Newton's method** for optimization. This method uses a local quadratic model of the function, derived from a second-order Taylor expansion around the current point $x_k$. The next point, $x_{k+1}$, is chosen as the minimum of this quadratic model, leading to the update rule:
$$ x_{k+1} = x_k - \frac{f'(x_k)}{f''(x_k)} $$
*   **Convergence**: When close to a minimum where $f''(x^{\star}) > 0$, Newton's method exhibits **quadratic convergence**, meaning the number of correct digits in the solution roughly doubles with each iteration. For a quadratic function like $f(x)=(x-2)^2$, it converges in a single step . This is vastly faster than the [linear convergence](@entry_id:163614) of GSS.
*   **Requirements and Fragility**: Newton's method requires both the first and second derivatives. Its power comes with significant fragility:
    *   It is not applicable to [non-differentiable functions](@entry_id:143443) .
    *   Its performance degrades severely if derivatives are noisy. A small error in the derivative can prevent convergence to high precision, whereas GSS, using exact function values, is unaffected .
    *   It is a local method and its convergence depends on the starting point; it provides no guarantee of finding the minimum unless started sufficiently close. GSS, as a [bracketing method](@entry_id:636790), guarantees convergence once a valid bracket is established.
    *   The update can become unstable or slow if the second derivative $f''(x)$ is near zero, which occurs in very flat regions .

In summary, GSS is a slow, steady, and highly reliable algorithm that acts as a "workhorse" for one-dimensional optimization. Derivative-based methods like Newton's method can be orders of magnitude faster but operate under much stricter assumptions about the function's smoothness and the quality of derivative information.

### Practical Considerations for Implementation

Applying GSS effectively requires addressing several practical details that arise in real-world use.

#### Bracket Initialization

The GSS algorithm assumes an initial interval $[a,b]$ that brackets the minimum is already known. But what if one only has an initial guess, $x_0$? A common strategy is to perform an **expanding search** to establish a bracket. Starting from $x_0$ with an initial step size $s_0$, one evaluates the function at $x_0$ and a neighboring point (e.g., $x_0+s_0$). If the function decreases, one continues taking steps in that direction, multiplicatively increasing the step size (e.g., by the [golden ratio](@entry_id:139097) $\phi$), until a function value is observed that is greater than the previous one. This procedure identifies a triplet of points $a  b  c$ such that $f(b)  f(a)$ and $f(b)  f(c)$, which forms a valid bracket for initiating GSS .

#### Stopping Criteria

The choice of stopping criterion is crucial. The most straightforward criterion is to terminate when the interval of uncertainty becomes sufficiently small, i.e., $b-a  \tau_x$, where $\tau_x$ is an absolute tolerance on the position of the minimizer.

An alternative is to stop when the improvement in the function value becomes negligible, i.e., $F_{k-1} - F_k  \varepsilon_f$, where $F_k$ is the best function value found after iteration $k$. While intuitive, this criterion can be dangerously misleading, especially for functions that are very flat near their minimum. For a function like $f(x) = |x-c|^{2m}$ with a large integer $m$, the function value can be extremely close to zero over a wide range of $x$ values around the minimum $c$. An optimization algorithm can enter this flat region and find that the function value barely changes from one iteration to the next, causing it to terminate prematurely long before the interval containing $x$ has been sufficiently narrowed. Therefore, a tolerance on the interval width is generally a more robust and reliable stopping criterion .

#### Handling Boundary Minima

A final consideration is the algorithm's behavior when the minimum lies at one of the boundaries of the search interval. If, for example, the function is monotonically increasing on $[a,b]$, the minimum is at $x=a$. The standard GSS will still perform its full set of iterations, slowly shrinking the interval towards the left boundary. This is inefficient.

A simple heuristic can provide substantial acceleration in such cases. At the beginning of each iteration, one can check if either of the endpoint values, $f(a)$ or $f(b)$, is smaller than both of the current interior point values. For a [unimodal function](@entry_id:143107), if $f(a)$ is less than or equal to $f(x_L)$ and $f(x_R)$, it must be the minimum. An algorithm enhanced with this **boundary-check heuristic** can terminate immediately upon identifying a boundary minimum, saving a significant number of function evaluations. The only cost is two extra function evaluations at the start of the search to get the initial values of $f(a)$ and $f(b)$ . This modification makes GSS more efficient for the special but common cases of monotonic or near-[monotonic functions](@entry_id:145115) on the interval of interest.