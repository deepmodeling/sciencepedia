## Introduction
In the world of optimization, [convex functions](@entry_id:143075) are the gold standard. Their unique property—that any local minimum is also a global minimum—transforms potentially intractable problems into solvable ones. But in practice, we rarely deal with simple, textbook [convex functions](@entry_id:143075). Real-world models in finance, engineering, and machine learning are complex constructions. This raises a critical question: how can we confidently determine if a complex function is convex, or better yet, how can we build one from the ground up while guaranteeing its [convexity](@entry_id:138568)?

This article provides the answer by exploring the "calculus" of [convex functions](@entry_id:143075)—a set of powerful rules and operations that preserve [convexity](@entry_id:138568). By mastering these tools, you gain the ability to systematically analyze and construct sophisticated optimization models.

Across three chapters, you will embark on a comprehensive journey. First, in **Principles and Mechanisms**, we will lay the foundation, detailing the core algebraic and compositional operations that serve as the building blocks for [convex functions](@entry_id:143075). Next, in **Applications and Interdisciplinary Connections**, we will see these principles in action, demonstrating how they enable tractable formulations in fields from signal processing and machine learning to [financial risk management](@entry_id:138248). Finally, **Hands-On Practices** will allow you to solidify your understanding by applying these concepts to solve concrete analytical problems. Let's begin by exploring the fundamental operations that preserve [convexity](@entry_id:138568).

## Principles and Mechanisms

In the study of optimization, [convex functions](@entry_id:143075) hold a place of paramount importance. Their defining characteristic—that the chord connecting any two points on their graph lies on or above the graph itself—ensures that any [local minimum](@entry_id:143537) is also a global minimum. This property simplifies the search for optimal solutions immensely. While the previous chapter introduced the fundamental definition and properties of [convex functions](@entry_id:143075), our focus here is on construction and recognition. How can we build complex [convex functions](@entry_id:143075) from simpler ones? And how can we determine if a given function is convex?

This chapter explores the key **operations that preserve [convexity](@entry_id:138568)**. Understanding these operations is a practical skill, enabling us to decompose a complicated optimization problem into a series of [convexity](@entry_id:138568)-preserving steps, thereby certifying the convexity of the objective function and constraints. We will proceed from foundational algebraic operations to more advanced constructions involving composition, partial minimization, and the deep interplay between [convex sets](@entry_id:155617) and [convex functions](@entry_id:143075).

### Foundational Operations: Sums, Scaling, and Supremum

The simplest and most common way to build new [convex functions](@entry_id:143075) is through algebraic combination. The fundamental operations of scaling and addition, when applied correctly, are guaranteed to preserve convexity.

A function $f: \mathbb{R}^n \to \mathbb{R}$ is convex if for all $x, y \in \mathbb{R}^n$ and for all $\theta \in [0, 1]$, the inequality $f(\theta x + (1-\theta)y) \le \theta f(x) + (1-\theta)f(y)$ holds. This definition is the bedrock upon which we will build.

#### Non-negative Weighted Sums

Let us consider a collection of [convex functions](@entry_id:143075) $f_1, f_2, \dots, f_m$ and a set of non-negative weights $w_1, w_2, \dots, w_m \ge 0$. The function formed by their non-negative weighted sum, $f(x) = \sum_{i=1}^m w_i f_i(x)$, is also convex.

To see why, we apply the definition of convexity. For any $x, y \in \mathbb{R}^n$ and $\theta \in [0, 1]$:
$$
f(\theta x + (1-\theta)y) = \sum_{i=1}^m w_i f_i(\theta x + (1-\theta)y)
$$
Since each $f_i$ is convex, we have $f_i(\theta x + (1-\theta)y) \le \theta f_i(x) + (1-\theta)f_i(y)$. Because each weight $w_i$ is non-negative, we can multiply both sides of this inequality by $w_i$ without changing its direction:
$$
w_i f_i(\theta x + (1-\theta)y) \le w_i (\theta f_i(x) + (1-\theta)f_i(y)) = \theta w_i f_i(x) + (1-\theta) w_i f_i(y)
$$
Summing these inequalities over all $i$ from $1$ to $m$ gives:
$$
\sum_{i=1}^m w_i f_i(\theta x + (1-\theta)y) \le \sum_{i=1}^m (\theta w_i f_i(x) + (1-\theta) w_i f_i(y))
$$
By rearranging the terms on the right-hand side, we get:
$$
f(\theta x + (1-\theta)y) \le \theta \left(\sum_{i=1}^m w_i f_i(x)\right) + (1-\theta) \left(\sum_{i=1}^m w_i f_i(y)\right) = \theta f(x) + (1-\theta)f(y)
$$
This proves that $f(x)$ is convex. This principle covers several common cases:
*   **Sum:** The sum of two or more [convex functions](@entry_id:143075) (where all $w_i = 1$) is convex.
*   **Positive Scaling:** A positive multiple of a convex function (where $m=1$ and $w_1 > 0$) is convex.

It is crucial that the weights be non-negative. If some weights are negative, [convexity](@entry_id:138568) is not guaranteed. For instance, consider the [convex functions](@entry_id:143075) $\phi_1(t)=t^2$ and $\phi_2(t)=t^2$ with weights $w_1=1$ and $w_2=-1$. Then a function of the form $f(x) = w_1 \phi_1(x) + w_2 \phi_2(2x)$ becomes $f(x) = 1 \cdot x^2 - 1 \cdot (2x)^2 = -3x^2$, which is a strictly [concave function](@entry_id:144403) .

A powerful extension of the non-negative sum is the **expectation** operator. If a [loss function](@entry_id:136784) $\ell(x, \xi)$ is convex in the decision variable $x \in \mathbb{R}^n$ for every possible realization of a random variable $\xi$, then its expected value, $f(x) = \mathbb{E}[\ell(x, \xi)]$, is also convex in $x$. The expectation is essentially a continuous analogue of a weighted sum, where the probability density or [mass function](@entry_id:158970) provides the non-negative weights. This is a cornerstone of [stochastic optimization](@entry_id:178938) .

#### Pointwise Supremum

Another fundamental building block is the **[pointwise supremum](@entry_id:635105)** (or maximum for a finite collection). If $\{f_i\}_{i \in I}$ is any collection (finite or infinite) of [convex functions](@entry_id:143075), then the function defined by their [pointwise supremum](@entry_id:635105),
$$
f(x) = \sup_{i \in I} f_i(x)
$$
is also a [convex function](@entry_id:143191).

The proof is elegant. For each $i \in I$, since $f_i$ is convex:
$$
f_i(\theta x + (1-\theta)y) \le \theta f_i(x) + (1-\theta)f_i(y)
$$
By the definition of the supremum, $f_i(x) \le \sup_{j \in I} f_j(x) = f(x)$ and $f_i(y) \le \sup_{j \in I} f_j(y) = f(y)$. Substituting these into the right-hand side of the inequality, we find:
$$
f_i(\theta x + (1-\theta)y) \le \theta f(x) + (1-\theta)f(y)
$$
This inequality holds for *every* function $f_i$ in the collection. Since the right-hand side is a constant upper bound for all $f_i(\theta x + (1-\theta)y)$, it must also be an upper bound for their [supremum](@entry_id:140512):
$$
f(\theta x + (1-\theta)y) = \sup_{i \in I} f_i(\theta x + (1-\theta)y) \le \theta f(x) + (1-\theta)f(y)
$$
This confirms that $f(x)$ is convex. A common application of this principle is in defining piecewise-linear [convex functions](@entry_id:143075) as the maximum of a set of affine functions, $f(x) = \max_{i=1,\dots,m} (a_i^\top x + b_i)$, since every [affine function](@entry_id:635019) is convex . Taking the supremum is a robust operation; adding or removing functions from the collection still results in a [convex function](@entry_id:143191).

In direct contrast, the **pointwise infimum** of [convex functions](@entry_id:143075) does *not* generally preserve convexity. For example, the function $h(x) = \inf\{x, -x\} = -|x|$ is the infimum of two affine (and thus convex) functions, yet it is a [concave function](@entry_id:144403) . Similarly, for a random loss $\ell(x,\xi)$ convex in $x$, the "best-case" function $f(x)=\inf_{\xi} \ell(x,\xi)$ is generally not convex .

### Operations Involving Composition

Composition provides a powerful way to generate new [convex functions](@entry_id:143075), but the rules are more subtle than for simple algebraic combinations.

#### Composition with an Affine Map

One of the most useful and straightforward composition rules involves an inner [affine function](@entry_id:635019). If $f: \mathbb{R}^m \to \mathbb{R}$ is a [convex function](@entry_id:143191), and $A \in \mathbb{R}^{m \times n}$ and $b \in \mathbb{R}^m$ define an [affine mapping](@entry_id:746332) from $\mathbb{R}^n$ to $\mathbb{R}^m$, then the composite function $g(x) = f(Ax+b)$ is convex on $\mathbb{R}^n$.

The proof follows directly from the definitions. Let $x, y \in \mathbb{R}^n$ and $\theta \in [0,1]$.
$$
g(\theta x + (1-\theta)y) = f(A(\theta x + (1-\theta)y) + b)
$$
Because the mapping $z \mapsto Az+b$ is affine, it preserves convex combinations:
$$
A(\theta x + (1-\theta)y) + b = \theta(Ax+b) + (1-\theta)(Ay+b)
$$
Substituting this into the expression for $g$ and using the [convexity](@entry_id:138568) of $f$:
$$
g(\theta x + (1-\theta)y) = f(\theta(Ax+b) + (1-\theta)(Ay+b)) \le \theta f(Ax+b) + (1-\theta)f(Ay+b) = \theta g(x) + (1-\theta)g(y)
$$
This confirms that $g(x)$ is convex  . This rule is broadly applicable, for instance, showing that if $\phi(t)$ is a convex function of a scalar $t$, then $f(x) = \phi(a^\top x)$ is a [convex function](@entry_id:143191) of the vector $x$ .

#### Composition with Scalar Functions

When the outer function is a scalar function, we have another important rule. Let $h: \mathbb{R} \to \mathbb{R}$ and $f: \mathbb{R}^n \to \mathbb{R}$. The composition $g(x) = h(f(x))$ is convex if:
1.  $f$ is a [convex function](@entry_id:143191), and
2.  $h$ is a convex and **non-decreasing** function.

Let's trace the proof. From the convexity of $f$, we know $f(\theta x + (1-\theta)y) \le \theta f(x) + (1-\theta)f(y)$. Since $h$ is non-decreasing, we can apply it to both sides of this inequality without changing the direction:
$$
h(f(\theta x + (1-\theta)y)) \le h(\theta f(x) + (1-\theta)f(y))
$$
Now, because $h$ is also convex, we can apply its convexity definition to the right-hand side:
$$
h(\theta f(x) + (1-\theta)f(y)) \le \theta h(f(x)) + (1-\theta)h(f(y))
$$
Combining these two steps, we get $g(\theta x + (1-\theta)y) \le \theta g(x) + (1-\theta)g(y)$, proving the [convexity](@entry_id:138568) of the composition  . The non-decreasing condition on the outer function $h$ is essential.

#### A Note on General Vector Composition

The rules for vector composition, where $g(x) = f(\sigma(x))$ for $f: \mathbb{R}^m \to \mathbb{R}$ and $\sigma: \mathbb{R}^n \to \mathbb{R}^m$, are significantly more complex. Even if $f$ is convex and each component of $\sigma$ is convex, the composition $g$ is not guaranteed to be convex. A full analysis requires examining the Hessian of the [composite function](@entry_id:151451) using the [multivariate chain rule](@entry_id:635606). For a twice-differentiable composition, the Hessian is given by:
$$
\nabla^2 g(x) = J_{\sigma}(x)^\top \nabla^2 f(\sigma(x)) J_{\sigma}(x) + \sum_{i=1}^m \frac{\partial f}{\partial z_i}(\sigma(x)) H_{\sigma_i}(x)
$$
where $J_{\sigma}$ is the Jacobian of $\sigma$ and $H_{\sigma_i}$ is the Hessian of its $i$-th component. Convexity of $g$ requires this entire matrix to be positive semidefinite. The second term can be indefinite and destroy convexity, even when $f$ is convex. A well-known example is the composition of a linear function $f(z)=z_1$ with the [softmax function](@entry_id:143376) $\sigma(x)$. While $f$ is convex, the resulting function $g(x) = \sigma_1(x)$ is not convex, demonstrating the subtlety of vector composition .

### Advanced Constructions

Beyond basic algebra and composition, several more advanced operations that preserve convexity are indispensable in modern optimization.

#### Partial Minimization

A remarkably powerful principle is that of **partial minimization**. If a function $f(x, y)$ of two variables $x \in \mathbb{R}^n$ and $y \in \mathbb{R}^m$ is jointly convex, then the function $g(x)$ obtained by minimizing $f$ over $y$,
$$
g(x) = \inf_{y \in \mathbb{R}^m} f(x, y)
$$
is a convex function of $x$. Geometrically, this operation corresponds to projecting the (convex) epigraph of $f$ onto a lower-dimensional space, which preserves the convexity of the set. This principle has profound applications.

One such application is the **Moreau envelope**. For a proper, lower semicontinuous, convex function $f$, its Moreau envelope is defined as:
$$
e_\lambda f(x) = \inf_{y \in \mathbb{R}^n} \left\{ f(y) + \frac{1}{2\lambda} \|x-y\|^2 \right\}
$$
This fits the partial minimization framework, as the function inside the [infimum](@entry_id:140118), $F(x,y) = f(y) + \frac{1}{2\lambda}\|x-y\|^2$, can be shown to be jointly convex in $(x,y)$. Therefore, the Moreau envelope $e_\lambda f(x)$ is always a [convex function](@entry_id:143191), provided the original function $f$ is convex . The Moreau envelope is a central tool in [proximal algorithms](@entry_id:174451), acting as a smoothing operator that yields a continuously differentiable approximation to $f$. It always lies below the original function, $e_\lambda f(x) \le f(x)$, and converges to $f(x)$ as the parameter $\lambda \to 0$ .

Another critical application is the **Conditional Value at Risk (CVaR)**, a [coherent risk measure](@entry_id:137862) used widely in finance and engineering. For a random loss $\ell(x, \xi)$ that is convex in $x$, its CVaR at level $\alpha \in (0,1)$ is also convex in $x$. This is because CVaR has a variational representation that is an instance of partial minimization:
$$
\mathrm{CVaR}_\alpha(\ell(x,\xi)) = \inf_{t \in \mathbb{R}} \left( t + \frac{1}{1-\alpha} \mathbb{E}[\max\{0, \ell(x, \xi) - t\}] \right)
$$
The expression inside the [infimum](@entry_id:140118) can be proven to be jointly convex in $(x,t)$ by applying the foundational rules: $\ell(x,\xi)-t$ is convex; $\max\{0,\cdot\}$ is convex and non-decreasing; expectation preserves convexity; and adding the [convex function](@entry_id:143191) $t$ preserves [convexity](@entry_id:138568). Since CVaR is the partial [infimum](@entry_id:140118) of a jointly [convex function](@entry_id:143191), it is convex .

#### From Convex Sets to Convex Functions

The relationship between [convex sets](@entry_id:155617) and [convex functions](@entry_id:143075) is bidirectional. We can define [convex functions](@entry_id:143075) based on the geometry of [convex sets](@entry_id:155617).

A fundamental connection is through **[sublevel sets](@entry_id:636882)**. A function $f$ is convex if and only if its $\alpha$-[sublevel sets](@entry_id:636882), defined as $S_\alpha = \{x \in \mathbb{R}^n \mid f(x) \le \alpha\}$, are convex for every $\alpha \in \mathbb{R}$. Proving that a [convex function](@entry_id:143191) has convex [sublevel sets](@entry_id:636882) is straightforward. If $x, y \in S_\alpha$, then $f(x) \le \alpha$ and $f(y) \le \alpha$. By convexity of $f$, for any $\theta \in [0,1]$,
$$
f(\theta x + (1-\theta)y) \le \theta f(x) + (1-\theta)f(y) \le \theta\alpha + (1-\theta)\alpha = \alpha
$$
This shows that the point $\theta x + (1-\theta)y$ is also in $S_\alpha$, so the [sublevel set](@entry_id:172753) is convex .

We can also construct a convex function directly from a [convex set](@entry_id:268368). Given a nonempty, convex, and [absorbing set](@entry_id:276794) $C \subset \mathbb{R}^n$ (where absorbing means that for any point $x$, a scaled version of $C$ contains it), we can define its **Minkowski functional** or **[gauge function](@entry_id:749731)**:
$$
\gamma_C(x) := \inf\{\lambda > 0 : x \in \lambda C\}
$$
This function measures how much the set $C$ must be "scaled up" to contain the point $x$. One can prove that for a convex set $C$, this functional satisfies two key properties:
1.  **Non-negative Homogeneity:** $\gamma_C(\alpha x) = \alpha \gamma_C(x)$ for all $\alpha \ge 0$.
2.  **Subadditivity (Triangle Inequality):** $\gamma_C(x+y) \le \gamma_C(x) + \gamma_C(y)$.

A function with these two properties is known as a [sublinear functional](@entry_id:143368), and every [sublinear functional](@entry_id:143368) is convex. This is easily shown:
$$
\gamma_C(\theta x + (1-\theta)y) \le \gamma_C(\theta x) + \gamma_C((1-\theta)y) = \theta \gamma_C(x) + (1-\theta)\gamma_C(y)
$$
Thus, the [gauge function](@entry_id:749731) provides a canonical way to derive a convex function that encodes the geometry of a convex set .

### A Cautionary Note: Operations That Fail to Preserve Convexity

It is just as important to recognize operations that do not preserve convexity. Common mistakes often involve assuming that all "simple" operations do.
*   **Product:** The product of two [convex functions](@entry_id:143075) is not generally convex. For example, $f_1(x) = x^2$ and $f_2(x) = x^2$ are convex, but their product $f(x)=x^4$ is also convex. However, $g_1(x)=(x-1)^2$ and $g_2(x)=(x+1)^2$ are convex, but their product $g(x)=(x^2-1)^2$ is not.
*   **Division and Reciprocals:** The ratio of [convex functions](@entry_id:143075) is not convex. The special case of the harmonic mean of [convex functions](@entry_id:143075), $H(x) = (\sum 1/f_i(x))^{-1}$, is also not guaranteed to be convex. In some specific instances, algebraic simplification might lead to a convex result, but this is an exception, not the rule .
*   **Quantiles (Value-at-Risk):** Unlike CVaR, the $\alpha$-quantile (also known as Value-at-Risk or VaR) of a random loss does not preserve convexity. A simple example with a discrete two-point distribution for $\xi$ can show that the quantile of $\ell(x,\xi)$ can be non-convex even when $\ell(x,\xi)$ is convex in $x$ for both outcomes . This distinction is of utmost importance in risk management and [stochastic programming](@entry_id:168183).

By mastering this calculus of [convex functions](@entry_id:143075), one gains the ability to systematically verify the [convexity](@entry_id:138568) of complex models, a critical step in formulating well-behaved and solvable [optimization problems](@entry_id:142739).