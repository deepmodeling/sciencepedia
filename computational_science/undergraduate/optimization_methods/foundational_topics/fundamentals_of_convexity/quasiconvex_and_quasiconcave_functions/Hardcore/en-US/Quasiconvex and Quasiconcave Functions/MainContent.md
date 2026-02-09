## Introduction
In the world of optimization, convexity is a cornerstone property that guarantees efficient and reliable solutions. However, many practical problems in science, engineering, and economics do not fit this strict mold, presenting objectives that are non-convex and seemingly difficult to solve globally. This article tackles this challenge by introducing quasiconvex and quasiconcave functions—a powerful generalization of convexity that retains the crucial property of enabling efficient global optimization. By relaxing the definition of convexity while preserving the structure of its level sets, quasiconvexity opens the door to solving a much wider class of real-world problems.

This article will guide you through the theory and application of this essential concept. In the first chapter, **Principles and Mechanisms**, we will explore the formal definitions of quasiconvexity, its key properties, and the bisection method that makes its optimization tractable. Next, in **Applications and Interdisciplinary Connections**, we will demonstrate how these functions appear in diverse fields, from fractional programming in engineering to fairness models in economics. Finally, **Hands-On Practices** will offer an opportunity to apply these concepts to concrete problems. We begin by delving into the fundamental principles that define quasiconvex functions and set them apart from their convex counterparts.

## Principles and Mechanisms

This chapter delves into the principles and mechanisms of a class of functions that generalize the concept of convexity: quasiconvex and quasiconcave functions. While not all desirable properties of convex functions are retained, quasiconvexity preserves a crucial feature: the ability to find a global minimum efficiently. We will explore the formal definitions, key characterizations, and the powerful optimization framework that makes these functions central to many fields of science and engineering.

### The Essence of Quasiconvexity: Convex Sublevel Sets

The geometric intuition behind a convex function is that its epigraph—the set of points lying on or above its graph—is a convex set. This implies that a line segment connecting any two points on the function's graph must lie on or above the graph itself. Quasiconvexity relaxes this requirement.

A function $f: D \to \mathbb{R}$ defined on a convex domain $D \subseteq \mathbb{R}^n$ is **quasiconvex** if for every real number $\alpha$, its $\alpha$-sublevel set, defined as:

$$
S_{\alpha} = \{ x \in D \mid f(x) \le \alpha \}
$$

is a convex set.

Intuitively, this means that for any "height" $\alpha$, all points whose function values are at or below that height form a single, connected "blob" without any holes or separate pieces. This definition is less restrictive than convexity. Every convex function is quasiconvex, because the sublevel sets of a convex function are always convex. However, the converse is not true.

A powerful illustration of this distinction is the function $f(x) = \sqrt{\|x\|}$ for $x \in \mathbb{R}^n$, where $\| \cdot \|$ is the Euclidean norm [@problem_id:3170826]. Let's analyze its sublevel sets. For any $\alpha \in \mathbb{R}$, the set $S_{\alpha}$ is $\{x \in \mathbb{R}^n \mid \sqrt{\|x\|} \le \alpha\}$.
- If $\alpha  0$, the set is empty, which is convex.
- If $\alpha \ge 0$, the inequality is equivalent to $\|x\| \le \alpha^2$. This describes a closed ball centered at the origin with radius $\alpha^2$. A ball is a convex set.
Since all sublevel sets of $f(x) = \sqrt{\|x\|}$ are convex, the function is, by definition, quasiconvex.

However, this function is not convex. To see this, we can test the fundamental inequality for convex functions, $f(\theta x_1 + (1-\theta)x_2) \le \theta f(x_1) + (1-\theta)f(x_2)$. Let's choose $x_1 = e_1$ (the first standard basis vector), $x_2=0$, and $\theta = 1/2$.
- The left-hand side is $f(\frac{1}{2}e_1 + \frac{1}{2}\cdot 0) = f(\frac{1}{2}e_1) = \sqrt{\|\frac{1}{2}e_1\|} = \sqrt{1/2} = 1/\sqrt{2}$.
- The right-hand side is $\frac{1}{2}f(e_1) + \frac{1}{2}f(0) = \frac{1}{2}\sqrt{\|e_1\|} + \frac{1}{2}\sqrt{\|0\|} = \frac{1}{2}\sqrt{1} + 0 = 1/2$.
The inequality $1/\sqrt{2} \le 1/2$ is false. Therefore, the function is not convex. This demonstrates that quasiconvexity is a strictly broader class than convexity. The epigraph of this function is not a convex set, even though its sublevel sets are [@problem_id:3170826].

The counterpart to quasiconvexity is **quasiconcavity**. A function $f$ is quasiconcave if $-f$ is quasiconvex. This is equivalent to all its **superlevel sets**, $\{x \in D \mid f(x) \ge \alpha\}$, being convex. A function that is both quasiconvex and quasiconcave is called **quasilinear**.

For example, the function $f(x) = \min_{i=1,\dots,m} a_i^\top x$ is quasiconcave [@problem_id:3170750]. Its $\alpha$-superlevel set is $\{x \mid \min_i a_i^\top x \ge \alpha\}$, which can be written as $\{x \mid a_i^\top x \ge \alpha \text{ for all } i\}$. This set is an intersection of half-spaces, which is a convex polyhedron, and thus a convex set.

### Alternative Characterizations and Properties

Beyond the sublevel set definition, several equivalent characterizations provide deeper insight and practical tools for working with quasiconvex functions.

#### The Quasiconvexity Inequality

An alternative definition states that a function $f$ is quasiconvex if for any $x_1, x_2$ in its domain and any $\theta \in [0,1]$, the following inequality holds:

$$
f(\theta x_1 + (1-\theta)x_2) \le \max\{f(x_1), f(x_2)\}
$$

This means the value of the function on any line segment does not exceed the maximum of its values at the segment's endpoints. Similarly, a function $f$ is quasiconcave if:

$$
f(\theta x_1 + (1-\theta)x_2) \ge \min\{f(x_1), f(x_2)\}
$$

#### The Line-Search Characterization

A particularly useful property is that a function is quasiconvex if and only if its restriction to any line is quasiconvex [@problem_id:3170743]. For a function $g: \mathbb{R} \to \mathbb{R}$, being quasiconvex is equivalent to its sublevel sets being intervals. Therefore, to test if $f: \mathbb{R}^n \to \mathbb{R}$ is quasiconvex, one can check whether the single-variable function $g(t) = f(x+tv)$ is quasiconvex for all choices of point $x$ and direction $v$.

Let's apply this test to a few functions on $\mathbb{R}^2$ [@problem_id:3170743]:
- **$f(x,y) = x^3$**: The restriction to any line is $g(t) = (x_0+tv_x)^3$. This is a monotonic function of $t$ (or constant if $v_x=0$). The sublevel sets of any monotonic function are rays or the entire line, which are intervals. Thus, $f(x,y)=x^3$ is quasiconvex.
- **$f(x,y) = \max\{x,y\}$**: The restriction is $g(t) = \max\{x_0+tv_x, y_0+tv_y\}$. This is the maximum of two affine functions, which is always a convex function. Since every convex function is quasiconvex, $f(x,y)=\max\{x,y\}$ is quasiconvex.
- **$f(x,y) = \min\{x,y\}$**: This function is not quasiconvex. Consider the line $x=t, y=-t$. The restriction is $g(t) = \min\{t, -t\} = -|t|$. The sublevel set for $\alpha=-1$ is $\{t \mid -|t| \le -1\}$, or $|t| \ge 1$. This set is $(-\infty, -1] \cup 1, \infty)$, which is not an interval.
- **$f(x,y) = \sin(x)+y^2$**: This is not quasiconvex. Restricting to the x-axis ($y=0$) gives $g(t) = \sin(t)$. The [sublevel set $\{t \mid \sin(t) \le 0\}$ is a union of disjoint intervals like $[\pi, 2\pi], [3\pi, 4\pi]$, etc., which is not connected.

#### First-Order Condition for Differentiable Functions

For a differentiable function $f$, there is a powerful first-order condition for quasiconvexity. A differentiable function $f$ is quasiconvex if and only if for all $x, y$ in its domain:

$$
f(y) \le f(x) \implies \nabla f(x)^\top (y-x) \le 0
$$

This condition has a clear geometric interpretation: if you are at a point $x$, any direction vector $(y-x)$ that points towards a "lower or equal" point $y$ must form a non-acute (obtuse or right) angle with the gradient vector $\nabla f(x)$.

Consider the function $f(x) = \ln(1+\|x\|_2)$, which is quasiconvex [@problem_id:3170780]. For any $x \ne 0$, its gradient is $\nabla f(x) = \frac{x}{(1+\|x\|_2)\|x\|_2}$. The condition becomes: if $\|y\|_2 \le \|x\|_2$, then $\frac{x^\top (y-x)}{(1+\|x\|_2)\|x\|_2} \le 0$. Since the denominator is positive, this simplifies to checking if $x^\top y \le \|x\|_2^2$. By the Cauchy-Schwarz inequality, $x^\top y \le \|x\|_2 \|y\|_2$. And since $\|y\|_2 \le \|x\|_2$, we have $\|x\|_2 \|y\|_2 \le \|x\|_2^2$. The condition holds, confirming quasiconvexity. The supremum of the directional derivative towards any point in the sublevel set is precisely zero, which is achieved by moving towards $y=x$.

#### Strict Quasiconvexity and Uniqueness of Minima

A key property of convex optimization is that any local minimum is also a global minimum. This property extends to quasiconvex optimization *under certain conditions*. A related concept is **strict quasiconvexity**. A function $f$ is strictly quasiconvex if for any distinct $x,y$ and any $t \in (0,1)$:

$$
f(t x + (1-t)y)  \max\{f(x), f(y)\}
$$

This strict inequality forbids "flat" segments in the function's graph that are not at the global minimum. For a strictly quasiconvex function, a local minimum is always a global minimum, and this minimum is unique. For a general quasiconvex function, the set of global minimizers is a convex set.

However, for a function that is quasiconvex but not strictly quasiconvex, it may possess local minima that are not global. More commonly in well-behaved examples, this non-strictness leads to a non-unique set of global minimizers.

Consider the function $f(x) = \max\{0, |x|-1\}$ on the interval $X=[-3,3]$ [@problem_id:3170753]. This function is continuous and quasiconvex. However, it is not strictly quasiconvex because for any two points $x,y$ in $[-1,1]$, we have $f(x)=f(y)=0$, and any point between them also has a function value of 0, violating the strict inequality. The minimum value of this function is $0$, and it is achieved for all $x \in [-1,1]$. The set of minimizers is the interval $[-1,1]$, not a single point. This is a direct consequence of the "flat" region where the function attains its minimum. Another example is $f(x)=\max\{x,0\}$ on $[-3,3]$, whose minimum value of 0 is achieved on the entire interval $[-3,0]$.

### Operations That Preserve Quasiconvexity

Understanding how quasiconvexity behaves under standard operations is crucial for identifying quasiconvex problems.

1.  **Non-decreasing Composition**: If $g: \mathbb{R}^n \to \mathbb{R}$ is quasiconvex and $\phi: \mathbb{R} \to \mathbb{R}$ is non-decreasing, then the composite function $f(x) = \phi(g(x))$ is quasiconvex. This can be seen by examining the sublevel sets of $f$. The set $\{x \mid \phi(g(x)) \le \alpha\}$ is equivalent to $\{x \mid g(x) \in Y_\alpha\}$, where $Y_\alpha = \{y \mid \phi(y) \le \alpha\}$. Because $\phi$ is non-decreasing, $Y_\alpha$ is an interval (e.g., $(-\infty, c]$). The set $\{x \mid g(x) \le c\}$ is just a sublevel set of the quasiconvex function $g$, and is therefore convex. A simple but important application is that if $\phi$ is non-decreasing, then $f(x) = \phi(a^\top x)$ is quasiconvex, because $a^\top x$ is a convex function [@problem_id:3170812].

2.  **Pointwise Maximum**: The pointwise maximum of a set of quasiconvex functions, $f(x) = \max_{i=1,\dots,m} f_i(x)$, is also quasiconvex. This follows because the $\alpha$-sublevel set of $f$ is the intersection of the $\alpha$-sublevel sets of the individual functions $f_i$: $S_\alpha = \bigcap_{i=1}^m \{x \mid f_i(x) \le \alpha\}$. Since each set in the intersection is convex (by the quasiconvexity of $f_i$) and the intersection of convex sets is convex, $S_\alpha$ is convex. This property is powerful. For example, in robust design, we might model a worst-case objective as $f(x) = \max_i \phi_i(g_i(x))$ where each $g_i$ is a convex performance metric and $\phi_i$ is a non-decreasing scaling function. Our results show that this composite function is quasiconvex [@problem_id:3170734].

3.  **Operations That Do Not Preserve Quasiconvexity**: It is critical to note that not all operations that preserve convexity also preserve quasiconvexity. For instance, the sum of two quasiconvex functions is not necessarily quasiconvex. A more surprising result is that the **product** of two non-negative quasiconvex functions need not be quasiconvex. A simple counterexample on $\mathbb{R}$ is given by $f(x) = \sqrt{|x|}$ and $g(x) = \sqrt{|x-1|}$, both of which are quasiconvex. Their product is $h(x) = \sqrt{|x(x-1)|}$. The sublevel set $\{x \mid h(x) \le t\}$ is $\{x \mid |x(x-1)| \le t^2\}$. If we choose $t$ small enough (e.g., $t=1/4$), this sublevel set becomes the union of two disjoint intervals, which is not a convex set. This shows that $h(x)$ is not quasiconvex [@problem_id:3170775].

### The Core Mechanism: Optimization via Convex Feasibility

The primary reason quasiconvex functions are so important in optimization is that, despite their added generality, they can be minimized globally using an efficient, systematic procedure. This procedure transforms the optimization problem into a series of convex feasibility problems.

Consider the optimization problem:
$$
p^* = \min_{x \in C} f(x)
$$
where $f$ is a quasiconvex function and $C$ is a convex set. The optimal value $p^*$ is the smallest value $t$ for which the sublevel set $S_t = \{x \in C \mid f(x) \le t\}$ is non-empty. This observation is the key.

This allows us to find $p^*$ using a **bisection search** on the value of the function. Suppose we have an initial interval $[l, u]$ that is known to contain $p^*$. The algorithm is as follows:

1.  Set a test value $t = (l+u)/2$.
2.  Solve the **convex feasibility problem**: find a point $x$ that satisfies $x \in C$ and $f(x) \le t$. This is equivalent to determining if the convex set $S_t$ is empty.
3.  If a feasible point is found, it means an objective value of $t$ (or lower) is achievable. We can therefore update our search interval by setting the new upper bound $u=t$.
4.  If no such point exists, it means the optimal value must be greater than $t$. We update our search interval by setting the new lower bound $l=t$.
5.  Repeat until the interval $[u-l]$ is sufficiently small.

The power of this method hinges on our ability to efficiently solve the feasibility problem in step 2. This is possible if the inequality $f(x) \le t$ can be represented by a set of constraints recognized by modern convex optimization solvers.

A prominent class of such functions are fractional functions, which often appear in signal processing, finance, and engineering design. Consider a function of the form:
$$
f(x) = \frac{\|Ax-b\|_2}{c^\top x + d}
$$
where the domain is restricted to a convex set where $c^\top x + d > 0$ [@problem_id:3170749] [@problem_id:3170836]. This function is quasiconvex. The feasibility check requires finding an $x$ such that $f(x) \le t$. Since the denominator is positive, we can rearrange this to:
$$
\|Ax-b\|_2 \le t(c^\top x + d)
$$
This is a **Second-Order Cone (SOC)** constraint. Problems involving SOC constraints and linear constraints are known as **Second-Order Cone Programs (SOCPs)**, and can be solved with extreme efficiency. Therefore, minimizing such a fractional objective becomes a sequence of SOCP feasibility checks. This method connects the abstract theory of quasiconvexity directly to the practical power of modern computational optimization.

For instance, finding the minimum of $f(x_1, x_2) = \frac{\sqrt{x_1^2 + x_2^2}}{2+x_1}$ subject to $x_1 \ge 1$ can be done by bisection, where each step involves solving for an $(x_1, x_2)$ satisfying $x_1 \ge 1$ and $\|x\|_2 \le t(2+x_1)$ [@problem_id:3170836]. In a similar vein, the maximization of a quasiconcave function, like $f(x) = \min_i a_i^\top x$, can be found by finding the largest $t$ for which the convex set $\{x \mid x \in C, a_i^\top x \ge t \text{ for all } i\}$ is feasible [@problem_id:3170750].

This bisection method based on convex feasibility is the central mechanism that makes quasiconvex optimization a tractable and powerful extension of the convex optimization paradigm.