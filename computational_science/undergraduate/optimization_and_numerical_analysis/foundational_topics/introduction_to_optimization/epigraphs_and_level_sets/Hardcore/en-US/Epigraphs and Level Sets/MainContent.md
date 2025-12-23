## Introduction
In the world of optimization, success often hinges on our ability to understand the structure of functions. While algebraic formulas provide a precise description, a geometric perspective can unlock deeper insights into a function's behavior, revealing the pathways to its optimal points. This article introduces two fundamental geometric tools—[epigraphs](@entry_id:173713) and level sets—that transform functions into tangible shapes, making abstract properties like [convexity](@entry_id:138568) intuitive and analyzable. By moving from pure algebra to geometry, we bridge a critical knowledge gap, gaining a more powerful language to describe and solve optimization problems.

## Principles and Mechanisms

In the study of optimization, we are fundamentally concerned with the behavior of functions—identifying where they reach their lowest or highest values. While algebraic manipulation is a powerful tool, a geometric perspective often provides deeper insight into a function's structure and the nature of its optimal points. This chapter introduces two fundamental geometric constructs—the epigraph and the [level set](@entry_id:637056)—that serve as powerful visual and analytical tools for understanding and classifying functions, particularly in the context of [convexity](@entry_id:138568) and the existence of optima.

### Defining the Geometric Landscape: Epigraphs and Sublevel Sets

To analyze a function geometrically, we must first learn how to represent it as a set in space. The epigraph and [sublevel sets](@entry_id:636882) are two primary ways to achieve this, each offering a unique perspective on the function's properties.

#### The Epigraph: A View From Above

The most intuitive representation of a function $f: \mathbb{R}^n \to \mathbb{R}$ is its graph, the set of points $(\mathbf{x}, f(\mathbf{x}))$. However, for optimization, it is often more useful to consider the set of all points that lie *on or above* the graph. This set is called the **epigraph** of the function.

Formally, the [epigraph of a function](@entry_id:637750) $f$ with domain $\text{dom}(f) \subseteq \mathbb{R}^n$ is a set in the higher-dimensional space $\mathbb{R}^{n+1}$, defined as:
$$
\text{epi}(f) = \{(\mathbf{x}, t) \in \mathbb{R}^n \times \mathbb{R} \mid \mathbf{x} \in \text{dom}(f), t \ge f(\mathbf{x}) \}
$$
The term "epigraph" comes from the Greek *epi* for "above" or "over" and *graph*. It is the "supergraph" of the function, encompassing the function's surface and the entire region of space vertically above it.

Consider the function $f(x,y) = x^4 + y^2$ defined on $\mathbb{R}^2$. Its epigraph is the set of points $(x, y, z)$ in $\mathbb{R}^3$ that satisfy the inequality $z \ge x^4 + y^2$. This set captures the bowl-like shape of the function's graph and fills it, extending infinitely upwards .

The geometry of the epigraph can reveal the essence of a function. A particularly illustrative example is the **Euclidean norm** in two dimensions, $f(\mathbf{x}) = \|\mathbf{x}\|_2 = \sqrt{x_1^2 + x_2^2}$ for $\mathbf{x} = (x_1, x_2) \in \mathbb{R}^2$. Its epigraph is the set of points $(x_1, x_2, t) \in \mathbb{R}^3$ satisfying $t \ge \sqrt{x_1^2 + x_2^2}$. Since the norm is always non-negative, this inequality implies $t \ge 0$. If we square both sides, we get $t^2 \ge x_1^2 + x_2^2$. This inequality describes a solid, upward-pointing right circular cone with its apex at the origin. The epigraph of the Euclidean norm is thus a familiar geometric shape .

Even for the simplest of functions, the epigraph provides a clear geometric picture. For a [constant function](@entry_id:152060) $f(\mathbf{x}) = c$ for all $\mathbf{x} \in \mathbb{R}^n$, its epigraph is the set $\{(\mathbf{x}, t) \in \mathbb{R}^n \times \mathbb{R} \mid t \ge c\}$. This describes a **closed half-space** in $\mathbb{R}^{n+1}$, consisting of all points whose $(n+1)$-th coordinate is at least $c$ .

#### Sublevel and Level Sets: Slicing the Domain

While the epigraph lives in a higher-dimensional space, **[sublevel sets](@entry_id:636882)** provide a way to visualize a function's structure within its own domain, $\mathbb{R}^n$. An $\alpha$-[sublevel set](@entry_id:172753), for some scalar value $\alpha$, is the collection of all points in the domain where the function's value is less than or equal to $\alpha$.

Formally, the **$\alpha$-[sublevel set](@entry_id:172753)** of a function $f: \mathbb{R}^n \to \mathbb{R}$ is defined as:
$$
S_\alpha = \{\mathbf{x} \in \text{dom}(f) \mid f(\mathbf{x}) \le \alpha \}
$$
Similarly, one can define the **$\alpha$-superlevel set** as $\{\mathbf{x} \mid f(\mathbf{x}) \ge \alpha\}$ and the **$\alpha$-[level set](@entry_id:637056)** as $\{\mathbf{x} \mid f(\mathbf{x}) = \alpha\}$. Level sets are the familiar contour lines seen on [topographic maps](@entry_id:202940). For optimization, the [sublevel sets](@entry_id:636882) are of primary interest, as they represent regions of the domain where the function value is "good" (i.e., low, in a minimization context).

Consider a practical example from manufacturing, where the cost to produce $x_1$ units of Component A and $x_2$ units of Component B is given by a linear [cost function](@entry_id:138681) $f(x_1, x_2) = 4x_1 + 7x_2$. If the company has a daily budget of $350$ currency units, the management is interested in the set of all production plans $(x_1, x_2)$ that meet this budget. This set is precisely the $350$-[sublevel set](@entry_id:172753) of the [cost function](@entry_id:138681):
$$
S_{350} = \{(x_1, x_2) \mid 4x_1 + 7x_2 \le 350, x_1 \ge 0, x_2 \ge 0 \}
$$
This set is a triangular region in the first quadrant of the plane, a simple example of a **closed half-plane** intersected with the non-negative quadrant. Any production plan within this region, such as $(70, 10)$ or $(35, 30)$, is feasible, while a plan outside it, such as $(50, 22)$, is not .

The character of [sublevel sets](@entry_id:636882) can vary dramatically depending on the value of $\alpha$. Returning to the constant function $f(\mathbf{x}) = c$, the condition for its $\beta$-[sublevel set](@entry_id:172753) is simply $c \le \beta$. If this condition is true (i.e., $\beta \ge c$), then *every* point $\mathbf{x} \in \mathbb{R}^n$ is in the [sublevel set](@entry_id:172753), so $S_\beta = \mathbb{R}^n$. If the condition is false (i.e., $\beta  c$), then *no* point can satisfy it, and the [sublevel set](@entry_id:172753) is the empty set, $S_\beta = \emptyset$ .

### The Bridge Between Geometry and Algebra

Epigraphs and [sublevel sets](@entry_id:636882) are not independent concepts; they are intimately related. The [sublevel sets](@entry_id:636882) of a function can be derived directly from its epigraph through a simple geometric procedure of slicing and projection.

Imagine the [epigraph of a function](@entry_id:637750) $f: \mathbb{R}^n \to \mathbb{R}$ as a solid object in $\mathbb{R}^{n+1}$. To find the $\alpha$-[sublevel set](@entry_id:172753), we perform two steps:
1.  **Slice:** Intersect the epigraph, $\text{epi}(f)$, with the horizontal [hyperplane](@entry_id:636937) defined by $t = \alpha$. This intersection consists of all points $(\mathbf{x}, \alpha)$ such that $\alpha \ge f(\mathbf{x})$.
2.  **Project:** Project this resulting set down onto the domain space $\mathbb{R}^n$. This projection simply discards the last coordinate, collecting all the points $\mathbf{x}$ that satisfy the inequality from the first step.

Let's illustrate this with the function $f(x) = x^2$ for a level $\alpha > 0$. The epigraph is the set $\{(x,y) \mid y \ge x^2\}$.
1.  **Slice:** We intersect this set with the horizontal line $y=\alpha$. This gives the set of points $S = \{(x, \alpha) \mid \alpha \ge x^2\}$. Since $\alpha > 0$, this inequality is equivalent to $-\sqrt{\alpha} \le x \le \sqrt{\alpha}$. Thus, $S$ is a horizontal line segment from $(-\sqrt{\alpha}, \alpha)$ to $(\sqrt{\alpha}, \alpha)$.
2.  **Project:** Projecting this line segment onto the x-axis gives the set of x-coordinates, which is the closed interval $[-\sqrt{\alpha}, \sqrt{\alpha}]$. This is precisely the $\alpha$-[sublevel set](@entry_id:172753) of $f(x) = x^2$ .

This procedure provides a powerful geometric intuition: the [sublevel sets](@entry_id:636882) of a function are the "shadows" cast by horizontal slices of its epigraph.

### The Cornerstone of Optimization: Convexity

The concepts of [epigraphs](@entry_id:173713) and [sublevel sets](@entry_id:636882) are most powerful when connected to **[convexity](@entry_id:138568)**, a central theme in optimization. A set is **convex** if the line segment connecting any two points in the set lies entirely within the set. A function is **convex** if the line segment connecting two points on its graph always lies on or above the graph itself.

This geometric definition of a [convex function](@entry_id:143191) leads to a profound and elegant connection with its epigraph.

**A function is convex if and only if its epigraph is a [convex set](@entry_id:268368).**

This statement, often called the **epigraph criterion for convexity**, is a cornerstone of convex analysis. It transforms the abstract algebraic inequality of function convexity, $f(\lambda \mathbf{x}_1 + (1-\lambda) \mathbf{x}_2) \le \lambda f(\mathbf{x}_1) + (1-\lambda) f(\mathbf{x}_2)$, into a simple, verifiable geometric property of a set.

To see why this is true, consider two points $( \mathbf{x}_1, t_1)$ and $(\mathbf{x}_2, t_2)$ in the epigraph of a convex function $f$. This means $t_1 \ge f(\mathbf{x}_1)$ and $t_2 \ge f(\mathbf{x}_2)$. A point on the line segment connecting them is $(\lambda \mathbf{x}_1 + (1-\lambda) \mathbf{x}_2, \lambda t_1 + (1-\lambda) t_2)$ for some $\lambda \in [0,1]$. For this point to be in the epigraph, its vertical coordinate must be greater than or equal to the function's value at its horizontal coordinate:
$$
\lambda t_1 + (1-\lambda) t_2 \ge f(\lambda \mathbf{x}_1 + (1-\lambda) \mathbf{x}_2)
$$
Because $t_1 \ge f(\mathbf{x}_1)$ and $t_2 \ge f(\mathbf{x}_2)$, we have $\lambda t_1 + (1-\lambda) t_2 \ge \lambda f(\mathbf{x}_1) + (1-\lambda) f(\mathbf{x}_2)$. The [convexity](@entry_id:138568) of $f$ ensures that $\lambda f(\mathbf{x}_1) + (1-\lambda) f(\mathbf{x}_2) \ge f(\lambda \mathbf{x}_1 + (1-\lambda) \mathbf{x}_2)$. Chaining these inequalities confirms that the line segment is indeed in the epigraph.

This criterion allows us to prove the convexity of functions by analyzing their [epigraphs](@entry_id:173713), and vice versa. For example, the function $g(x_1, x_2) = x_1^2 + |x_2|$ can be shown to be convex because it is the sum of two [convex functions](@entry_id:143075), $f_1(x_1, x_2) = x_1^2$ and $f_2(x_1, x_2) = |x_2|$. By the epigraph criterion, its epigraph, $\text{epi}(g)$, must therefore be a [convex set](@entry_id:268368) in $\mathbb{R}^3$ . Similarly, the function $f(x) = 1/x$ on the domain $x > 0$ has a second derivative $f''(x) = 2/x^3$, which is strictly positive for all $x > 0$. By the [second-derivative test](@entry_id:160504), the function is convex. Consequently, we can immediately conclude that its epigraph is a convex set without needing to analyze the set's geometry directly .

The epigraph criterion also provides a powerful mechanism for understanding how operations on functions affect their convexity. Consider the function $h(\mathbf{x}) = \max(f_1(\mathbf{x}), f_2(\mathbf{x}))$, the pointwise maximum of two functions. A point $(\mathbf{x}, t)$ is in the epigraph of $h$ if and only if $t \ge h(\mathbf{x})$, which is equivalent to $t \ge \max(f_1(\mathbf{x}), f_2(\mathbf{x}))$. This in turn is true if and only if $t \ge f_1(\mathbf{x})$ *and* $t \ge f_2(\mathbf{x})$. This is precisely the condition that $(\mathbf{x}, t)$ must be in $\text{epi}(f_1)$ and also in $\text{epi}(f_2)$. Therefore, we arrive at the elegant result:
$$
\text{epi}(\max(f_1, f_2)) = \text{epi}(f_1) \cap \text{epi}(f_2)
$$
This result has a crucial implication: since the intersection of any number of [convex sets](@entry_id:155617) is always convex, the pointwise maximum of [convex functions](@entry_id:143075) is always a [convex function](@entry_id:143191). This allows us to build complex [convex functions](@entry_id:143075) from simpler ones .

### Beyond Convexity: Quasiconvexity and Compactness

While [convexity](@entry_id:138568) is a desirable property, it is sometimes too restrictive. There are important classes of non-[convex functions](@entry_id:143075) that still possess favorable geometric properties useful in optimization.

#### Quasiconvexity and Sublevel Sets

A convex function has the property that all of its [sublevel sets](@entry_id:636882) are [convex sets](@entry_id:155617). However, the converse is not true. This observation leads to a broader class of functions. A function is called **quasiconvex** if all of its [sublevel sets](@entry_id:636882) are convex.

Every [convex function](@entry_id:143191) is quasiconvex, but not every [quasiconvex function](@entry_id:177407) is convex.
Consider the function $f(x) = \sqrt{|x|}$. This function is not convex. For instance, the midpoint of the chord connecting $(1,1)$ and $(-1,1)$ is $(0,1)$, but the function value at the midpoint is $f(0)=0$, which is below the chord, violating the definition of convexity. However, its $\alpha$-[sublevel sets](@entry_id:636882) for $\alpha \ge 0$ are of the form $S_\alpha = \{x \mid \sqrt{|x|} \le \alpha\}$, which simplifies to $\{x \mid |x| \le \alpha^2\}$, or the interval $[-\alpha^2, \alpha^2]$. Since all [sublevel sets](@entry_id:636882) are intervals (or the [empty set](@entry_id:261946) for $\alpha  0$), they are all convex. Thus, $f(x) = \sqrt{|x|}$ is quasiconvex but not convex. Another example is $f(x) = x^3$, which is not convex, but its [sublevel sets](@entry_id:636882) are rays of the form $(-\infty, \sqrt[3]{\alpha}]$, which are convex . Quasiconvex functions are important because for such functions, a local minimum is not necessarily a global minimum, but specialized optimization algorithms can still find global solutions efficiently.

#### Coercivity and Compactness of Sublevel Sets

The ultimate goal of many [optimization problems](@entry_id:142739) is to prove the existence of a minimizer. Sublevel sets are central to this goal. The **Extreme Value Theorem** states that a continuous function on a **compact** set (a set that is both closed and bounded) is guaranteed to attain its minimum and maximum values on that set.

If we can show that the search for a minimum can be restricted to a compact [sublevel set](@entry_id:172753), then the existence of a solution is guaranteed. But how can we ensure a [sublevel set](@entry_id:172753) is compact? This requires an additional property on the function, known as **coercivity**.

A function $f: \mathbb{R}^n \to \mathbb{R}$ is **coercive** if its value tends to infinity as the norm of its input tends to infinity. Formally, $\lim_{\|\mathbf{x}\| \to \infty} f(\mathbf{x}) = \infty$. This means that far away from the origin, the function values are very large.

Now, consider a function $f$ that is both continuous and coercive.
-   Because $f$ is continuous, the preimage of a closed set is closed. The set $(-\infty, \alpha]$ is a [closed set](@entry_id:136446) in $\mathbb{R}$. Therefore, the [sublevel set](@entry_id:172753) $S_\alpha = f^{-1}((-\infty, \alpha])$ must be a **closed** set.
-   Because $f$ is coercive, the [sublevel sets](@entry_id:636882) must be **bounded**. If a [sublevel set](@entry_id:172753) $S_\alpha$ were unbounded, one could find a sequence of points $\mathbf{x}_k \in S_\alpha$ with $\|\mathbf{x}_k\| \to \infty$. But coercivity would imply $f(\mathbf{x}_k) \to \infty$. This contradicts the fact that $f(\mathbf{x}_k) \le \alpha$ for all points in the [sublevel set](@entry_id:172753). Therefore, $S_\alpha$ must be bounded.

Since any non-empty [sublevel set](@entry_id:172753) of a continuous, [coercive function](@entry_id:636735) is both closed and bounded, it is **compact** by the Heine-Borel theorem. This is a profound result: for any such function, a global minimizer is guaranteed to exist, as it must be the minimum of the function over any non-empty (and thus compact) [sublevel set](@entry_id:172753) .

In conclusion, [epigraphs](@entry_id:173713) and [sublevel sets](@entry_id:636882) are far more than mere geometric curiosities. They are the language through which we can understand, classify, and analyze the structure of functions, forming the essential bridge between the algebraic formulation of optimization problems and the geometric intuition required to solve them.