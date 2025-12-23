## Introduction
The [fixed-point iteration method](@entry_id:168837) is a cornerstone of [numerical analysis](@entry_id:142637), offering an elegant and powerful approach for solving a wide variety of equations. At its core, the method transforms the often-difficult task of finding a root into a more intuitive process of finding a "fixed point" where a function's input equals its output. This iterative technique provides a unifying framework that underpins many sophisticated algorithms across science and engineering. The central challenge, however, lies in understanding when and why this iterative process succeeds. The critical questions are: how do we choose the right transformation, and under what conditions can we guarantee that our sequence of approximations will converge to the correct solution?

This article provides a thorough exploration of the [fixed-point iteration method](@entry_id:168837), structured to build a robust understanding from foundational theory to practical application. In the first chapter, **Principles and Mechanisms**, we will dissect the core concepts of fixed points, convergence criteria based on the derivative, and the rigorous guarantees provided by the Fixed-Point Theorem. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the method's remarkable versatility by showing how it is applied to solve [linear systems](@entry_id:147850), optimize machine learning algorithms, and model equilibrium in fields from economics to quantum chemistry. Finally, the **Hands-On Practices** chapter will offer targeted problems designed to solidify your comprehension and allow you to apply these principles to concrete examples.

## Principles and Mechanisms

The [fixed-point iteration method](@entry_id:168837) is a fundamental concept in numerical analysis, providing a powerful and versatile framework for solving a vast range of equations. The core idea is elegantly simple: to find a root of an equation, we transform it into a form where the variable is isolated on one side. This transformation recasts the problem of root-finding into a problem of finding a "fixed point" of a function.

### The Fixed-Point Concept

Given an equation that we wish to solve for a variable $x$, say $f(x) = 0$, we can often rearrange it algebraically into the form:

$$x = g(x)$$

A value $x^*$ that satisfies this equation, i.e., $x^* = g(x^*)$, is called a **fixed point** of the function $g$. Graphically, a fixed point is the x-coordinate of a point where the graph of the function $y = g(x)$ intersects the line $y=x$.

Once the problem is in this form, we can devise an iterative scheme. We begin with an initial guess, $x_0$, and generate a sequence of approximations using the recurrence relation:

$$x_{n+1} = g(x_n), \quad \text{for } n = 0, 1, 2, \dots$$

If this sequence $\{x_n\}$ converges to a limit, say $x^*$, and the function $g$ is continuous, then this limit must be a fixed point. This is because taking the limit of both sides of the recurrence gives:

$$\lim_{n\to\infty} x_{n+1} = \lim_{n\to\infty} g(x_n)$$

$$x^* = g\left(\lim_{n\to\infty} x_n\right) = g(x^*)$$

The crucial question, which forms the central theme of this chapter, is: under what conditions does this sequence actually converge?

### Local Convergence and the Role of the Derivative

To build our intuition, let us consider a simple yet illustrative model. Imagine a [chemical reactor](@entry_id:204463) where a substance's concentration, $C_n$, is measured after each cycle $n$. In each cycle, the concentration first decreases by a fraction $\alpha$ and is then increased by a constant amount $\beta$. The evolution of the concentration can be described by the affine iteration :

$$C_{n+1} = (1-\alpha)C_n + \beta$$

This is a [fixed-point iteration](@entry_id:137769) with the function $g(C) = (1-\alpha)C + \beta$. The fixed point, or steady-state concentration $C^*$, is found by setting $C^* = g(C^*)$, which yields $C^* = (1-\alpha)C^* + \beta$, so $\alpha C^* = \beta$, and finally $C^* = \frac{\beta}{\alpha}$.

To understand convergence, let's examine the error, $e_n = C_n - C^*$. The error at the next step is:

$$e_{n+1} = C_{n+1} - C^* = \left((1-\alpha)C_n + \beta\right) - C^*$$

Substituting $\beta = \alpha C^*$ and $C_n = e_n + C^*$:

$$e_{n+1} = (1-\alpha)(e_n + C^*) + \alpha C^* - C^* = (1-\alpha)e_n + (1-\alpha)C^* + \alpha C^* - C^* = (1-\alpha)e_n$$

From the relationship $e_{n+1} = (1-\alpha)e_n$, we can see that the error is multiplied by the factor $(1-\alpha)$ at each step. By induction, $e_n = (1-\alpha)^n e_0$. The sequence of errors will converge to zero if and only if $|1-\alpha|  1$.

This simple linear example reveals a profound principle: the convergence of a [fixed-point iteration](@entry_id:137769) near a fixed point is governed by the "slope" of the function $g$ at that point. We can generalize this by considering the [error propagation](@entry_id:136644) for an arbitrary function $g$. Let $x^*$ be a fixed point, and let $e_n = x_n - x^*$. Then:

$$e_{n+1} = x_{n+1} - x^* = g(x_n) - g(x^*) = g(x^* + e_n) - g(x^*)$$

If $g$ is differentiable, the Mean Value Theorem states that there exists a point $\xi_n$ between $x_n$ and $x^*$ such that:

$$g(x_n) - g(x^*) = g'(\xi_n)(x_n - x^*) = g'(\xi_n)e_n$$

Thus, the error propagates according to $|e_{n+1}| = |g'(\xi_n)||e_n|$. As $x_n$ approaches $x^*$, $\xi_n$ also approaches $x^*$. The behavior of the iteration is therefore determined by the magnitude of the derivative at the fixed point, $|g'(x^*)|$. This leads to a fundamental classification of fixed points :

-   A fixed point $x^*$ is **attracting** if $|g'(x^*)|  1$. If the initial guess $x_0$ is sufficiently close to $x^*$, the sequence $\{x_n\}$ will converge to $x^*$.
-   A fixed point $x^*$ is **repelling** if $|g'(x^*)| > 1$. The iteration will move away from $x^*$, even if started very close to it (unless $x_0 = x^*$ exactly). The error is amplified at each step .
-   A fixed point $x^*$ is **neutral** (or **indifferent**) if $|g'(x^*)| = 1$. The convergence behavior cannot be determined from the first derivative alone; a more detailed analysis is required.

For instance, consider the function $g(x) = \frac{2x}{1+x^2}$ . The fixed points are the solutions to $x = \frac{2x}{1+x^2}$, which are $x = 0, 1, -1$. The derivative is $g'(x) = \frac{2(1-x^2)}{(1+x^2)^2}$. Evaluating at the fixed points:
-   At $x=0$, $|g'(0)| = |2| > 1$, so $x=0$ is a [repelling fixed point](@entry_id:189650).
-   At $x=1$, $|g'(1)| = |0|  1$, so $x=1$ is an attracting fixed point.
-   At $x=-1$, $|g'(-1)| = |0|  1$, so $x=-1$ is also an attracting fixed point.

### Qualitative Behavior: Monotonic vs. Oscillatory Convergence

Within the realm of attracting fixed points, where $|g'(x^*)|  1$, the *sign* of the derivative determines the qualitative nature of the convergence. The approximate error relation $e_{n+1} \approx g'(x^*)e_n$ is key.

If **$0 \le g'(x^*)  1$**, the error $e_{n+1}$ will have the same sign as $e_n$. This means if an iterate $x_n$ is greater than $x^*$, the next iterate $x_{n+1}$ will also be greater than $x^*$ (but closer). The sequence approaches the fixed point from one side, a behavior known as **monotonic convergence**.

If **$-1  g'(x^*)  0$**, the error $e_{n+1}$ will have the opposite sign of $e_n$. If $x_n$ is greater than $x^*$, $x_{n+1}$ will be less than $x^*$, and vice-versa. The iterates jump back and forth across the fixed point as they home in on it. This is called **oscillatory convergence** or spiral convergence.

A classic example of oscillatory convergence is the search for the Dottie number, the unique real solution to $x = \cos(x)$ . The iteration is $x_{n+1} = \cos(x_n)$. Let the fixed point be $x^*$. The derivative is $g'(x) = -\sin(x)$. Since the fixed point $x^*$ lies in the interval $(0, 1)$, $\sin(x^*)$ is positive, meaning $g'(x^*) = -\sin(x^*)$ is negative. Furthermore, since $x^* \in (0, 1)$, we know $\sin(x^*)  \sin(1)  1$. Therefore, we have $-1  g'(x^*)  0$, which correctly predicts that the iterates will spiral in towards the Dottie number.

### Guaranteed Convergence: The Fixed-Point Theorem

Local convergence analysis tells us what happens if we start "sufficiently close" to a fixed point. But what if we need a guarantee of convergence from *any* starting point within a specified interval? The **Fixed-Point Theorem** (also known as the Contraction Mapping Theorem) provides a set of stronger conditions for such a guarantee.

**Theorem (Fixed-Point Theorem):** Let $g$ be a function defined on a closed interval $I = [a, b]$. If $g$ satisfies the following two conditions:
1.  **Self-Mapping Property:** $g$ maps the interval $I$ into itself. That is, for every $x \in I$, the value $g(x)$ is also in $I$.
2.  **Contraction Property:** $g$ is a contraction on $I$. That is, there exists a constant $k$ with $0 \le k  1$ such that for all $x, y \in I$, $|g(x) - g(y)| \le k|x - y|$. If $g$ is differentiable, this condition is satisfied if $|g'(x)| \le k  1$ for all $x \in I$.

If these conditions hold, then:
(a) There exists a unique fixed point $x^*$ in the interval $I$.
(b) For any initial guess $x_0 \in I$, the sequence $x_{n+1} = g(x_n)$ is guaranteed to converge to $x^*$.

To apply this theorem, we must verify both conditions. Consider an engineer trying to find the equilibrium temperature $T$ for a thermistor, which must lie in the interval $[1, 2]$ and solves the equation $T^4 - T = 3$. This is rearranged into the fixed-point form $T = (T+3)^{1/4}$. Let $g(T) = (T+3)^{1/4}$ and $I = [1, 2]$ .

1.  **Verify Self-Mapping**: We must check if $g([1, 2]) \subseteq [1, 2]$. Since $g'(T) = \frac{1}{4}(T+3)^{-3/4} > 0$, the function $g(T)$ is increasing. We only need to check the endpoints. $g(1) = 4^{1/4} = \sqrt{2} \approx 1.414$ and $g(2) = 5^{1/4} \approx 1.495$. Since $[1.414, 1.495] \subset [1, 2]$, the self-mapping condition holds. This verification is sometimes more subtle, as for $g(x) = 1 + \frac{1}{1+x}$ on $[1,2]$, where $g'(x)  0$ and the image interval is $[g(2), g(1)] = [4/3, 3/2]$, which is also a subset of $[1,2]$ .

2.  **Verify Contraction**: We check the derivative on the interval. For $T \in [1, 2]$, the derivative $g'(T) = \frac{1}{4(T+3)^{3/4}}$ is a decreasing function. Its maximum value occurs at $T=1$, which is $g'(1) = \frac{1}{4(4)^{3/4}} = \frac{1}{4 \cdot 2\sqrt{2}} = \frac{1}{8\sqrt{2}} \approx 0.088  1$. So we can take $k = \frac{1}{8\sqrt{2}}$, and the contraction condition holds.

Since both conditions are satisfied, the theorem guarantees that the iteration $T_{n+1} = (T_{n}+3)^{1/4}$ will converge to the unique equilibrium temperature for any starting guess in $[1, 2]$.

### The Rate and Order of Convergence

When an iteration converges, the next natural question is: how fast? The **[rate of convergence](@entry_id:146534)** quantifies this.

If $|g'(x^*)| = L$ where $0  L  1$, the convergence is **linear**. In this case, the error is reduced by a roughly constant factor $L$ at each step: $|e_{n+1}| \approx L |e_n|$. A direct consequence is that the number of correct decimal places in the approximation increases by a fixed amount per iteration. We can use the more rigorous [error bound](@entry_id:161921) $|e_n| \le L^n |e_0|$ to estimate the number of iterations $N$ required to achieve a certain accuracy. For instance, to reduce the initial error by a factor of $10^5$ with a contraction constant $L=0.4$, we solve $L^N \le 10^{-5}$, which gives $N \ge \frac{\ln(10^{-5})}{\ln(0.4)} \approx 12.57$. Thus, 13 iterations are required .

A much faster convergence occurs when $g'(x^*) = 0$. In this case, the [linear approximation](@entry_id:146101) of the error is zero, and we must turn to a higher-order Taylor expansion around the fixed point $x^*$:

$$e_{n+1} = g(x_n) - g(x^*) = g(x^*+e_n) - g(x^*) = g'(x^*)e_n + \frac{g''(x^*)}{2!}e_n^2 + \frac{g'''(x^*)}{3!}e_n^3 + \dots$$

If $g'(x^*) = 0$ but $g''(x^*) \neq 0$, the [dominant term](@entry_id:167418) in the error becomes:

$$e_{n+1} \approx \frac{g''(x^*)}{2} e_n^2$$

This is called **quadratic convergence**. The error at each step is proportional to the square of the previous error. This means that the number of correct significant digits roughly doubles with each iteration, a dramatic improvement over [linear convergence](@entry_id:163614). The premier example of a quadratically convergent method is **Newton's method** for solving $f(x)=0$. Its iteration function is $g(x) = x - \frac{f(x)}{f'(x)}$. The derivative is $g'(x) = \frac{f(x)f''(x)}{(f'(x))^2}$. At a [simple root](@entry_id:635422) $r$ where $f(r)=0$ and $f'(r) \neq 0$, we immediately see that $g'(r)=0$. This is the reason for Newton's method's celebrated speed .

This concept can be generalized. An iterative method has **[order of convergence](@entry_id:146394) $m$** if:

$$|e_{n+1}| \approx C|e_n|^m \quad \text{for some } C > 0$$

This occurs if $g'(x^*) = g''(x^*) = \dots = g^{(m-1)}(x^*) = 0$, but $g^{(m)}(x^*) \neq 0$. By carefully designing the iteration function $g(x)$, one can achieve even higher orders of convergence. For example, in designing an algorithm to find the cube root of $A$, one might propose an iteration family like $x_{n+1} = x_n \left( \frac{x_n^3 + \alpha A}{\beta x_n^3 + A} \right)$. By choosing the parameters $\alpha$ and $\beta$ to make successive derivatives of the iteration function vanish at the fixed point $p=A^{1/3}$, one can achieve [cubic convergence](@entry_id:168106) ($m=3$) .

### Special Cases and Practical Considerations

The elegant theory of [fixed-point iteration](@entry_id:137769) has some important subtleties.

**Neutral Fixed Points:** When $|g'(x^*)| = 1$, the linear analysis fails. The convergence behavior depends on the higher-order terms in the Taylor expansion. Consider the iteration $x_{n+1} = x_n^2 - x_n + 1$ . The unique fixed point is $x^*=1$. The derivative is $g'(x) = 2x - 1$, so $g'(1)=1$. A detailed analysis of the error, $e_{n+1} = x_{n+1}-1 = (x_n-1)^2 = e_n^2$, reveals that if we start with $x_0 \in (0,1)$, the error is negative and approaches zero. If $x_0=0$ or $x_0=1$, it converges. However, if $x_0 > 1$, the error is positive and grows at each step, leading to divergence. The set of starting points for which the iteration converges (the **basin of attraction**) is the interval $[0,1]$, a much more delicate situation than for a standard attracting fixed point.

**Numerical Stability:** In practice, computers use finite-precision floating-point arithmetic. This introduces a small round-off error in every calculation. For a convergent iteration $x_{n+1} = g(x_n)$, the computed sequence $\hat{x}_n$ will not converge perfectly to $x^*$. Let's model the computed step as $\hat{x}_{n+1} \approx g(\hat{x}_n) + \delta_n$, where $\delta_n$ is the [computational error](@entry_id:142122), bounded by machine epsilon, $\epsilon_{mach}$. For a convergent scheme with contraction factor $L=|g'(x^*)|$, the [error propagation](@entry_id:136644) becomes $|e_{n+1}| \approx L|e_n| + \epsilon_{mach}$. After many iterations, the term $L|e_n|$ will shrink, but it will be balanced by the constant introduction of new error $\epsilon_{mach}$. The error will stabilize when $|e_n|$ reaches a point where $|e_n| \approx L|e_n| + \epsilon_{mach}$, which implies a terminal error magnitude of $|e| \approx \frac{\epsilon_{mach}}{1-L}$. This means the iteration converges not to a point, but to a "[numerical stability](@entry_id:146550) interval" around the true fixed point, whose size is determined by both the machine precision and the contraction factor of the method . A method with a smaller contraction factor (i.e., $L$ closer to 0) will have better numerical stability and a smaller terminal error interval.