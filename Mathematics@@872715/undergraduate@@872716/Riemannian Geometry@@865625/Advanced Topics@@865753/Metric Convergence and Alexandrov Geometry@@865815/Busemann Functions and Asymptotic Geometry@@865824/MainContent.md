## Introduction
In the study of Riemannian geometry, understanding the local properties of curvature is only half the story. A central challenge is to comprehend the global, large-scale structure of a manifold—its "geometry at infinity." How do we formalize the notion of a "direction to infinity" and measure distances from it? This is the knowledge gap addressed by the Busemann function, a powerful analytical tool that translates asymptotic behavior into a concrete function on the manifold. This article provides a comprehensive introduction to this concept, designed for students of [differential geometry](@entry_id:145818). In the first chapter, "Principles and Mechanisms," we will define the Busemann function, establish its universal properties, and uncover its deeper convex nature in manifolds with nonpositive or non-negative curvature. Next, "Applications and Interdisciplinary Connections" will showcase its utility in proving profound structural results like the Cheeger-Gromoll Splitting Theorem and its connections to Lie groups and [metric geometry](@entry_id:185748). Finally, "Hands-On Practices" will offer opportunities to apply these concepts in concrete examples, solidifying your understanding of this essential geometric tool.

## Principles and Mechanisms

In this chapter, we delve into the core principles governing Busemann functions and the mechanisms through which they illuminate the large-scale geometry of Riemannian manifolds. We will begin by establishing the function's definition and its most fundamental properties, which hold in remarkable generality. We then specialize to the classical setting of manifolds with nonpositive [sectional curvature](@entry_id:159738) to uncover deeper geometric and analytic properties. Finally, we broaden our perspective to see how Busemann functions serve as coordinates for the [boundary at infinity](@entry_id:634468) and as crucial tools in the celebrated Cheeger-Gromoll Splitting Theorem.

### The Busemann Function: Definition and Universal Properties

Let $(M,g)$ be a complete Riemannian manifold, and let $d(\cdot, \cdot)$ denote the associated Riemannian distance. A **[geodesic ray](@entry_id:202351)** is a unit-speed geodesic $\gamma: [0, \infty) \to M$ that is minimizing between any two of its points; that is, $d(\gamma(s), \gamma(t)) = |t-s|$ for all $s, t \ge 0$. Such rays represent directions to infinity. To probe the geometry "at infinity" from the perspective of a point in the manifold, we can measure how the distance to a point far along a ray deviates from the parameter of the ray itself. This motivates the central definition of this chapter.

The **Busemann function** associated with a [geodesic ray](@entry_id:202351) $\gamma$ is the function $b_\gamma: M \to \mathbb{R}$ defined by the pointwise limit:
$$
b_\gamma(x) = \lim_{t\to\infty} \big( d(x, \gamma(t)) - t \big)
$$
This function, named after Herbert Busemann, can be thought of as a "signed distance" to the point at infinity defined by the ray $\gamma$. Note that some authors define the Busemann function with the opposite sign; our choice is motivated by properties that will soon become apparent.

A primary question is whether this limit is always well-defined. Indeed, the existence of the Busemann function is a universal property for any complete Riemannian manifold, independent of its curvature. To establish this, consider the function $f_x(t) = d(x, \gamma(t)) - t$ for a fixed point $x \in M$. Let $t_2 > t_1 \ge 0$. By the [triangle inequality](@entry_id:143750), we have:
$$
d(x, \gamma(t_2)) \le d(x, \gamma(t_1)) + d(\gamma(t_1), \gamma(t_2))
$$
Since $\gamma$ is a unit-speed ray, $d(\gamma(t_1), \gamma(t_2)) = t_2 - t_1$. Substituting and rearranging gives:
$$
d(x, \gamma(t_2)) - t_2 \le d(x, \gamma(t_1)) - t_1
$$
This shows that the function $t \mapsto f_x(t)$ is monotonically non-increasing. To guarantee convergence, we also need a lower bound. Applying the [triangle inequality](@entry_id:143750) to the points $x$, $\gamma(0)$, and $\gamma(t)$:
$$
d(\gamma(0), \gamma(t)) \le d(\gamma(0), x) + d(x, \gamma(t))
$$
Since $d(\gamma(0), \gamma(t)) = t$, this becomes $t \le d(x, \gamma(0)) + d(x, \gamma(t))$, which rearranges to:
$$
d(x, \gamma(t)) - t \ge -d(x, \gamma(0))
$$
The function $f_x(t)$ is bounded below by the constant $-d(x, \gamma(0))$. A monotonically non-increasing function that is bounded below must converge to a finite limit. Therefore, $b_\gamma(x)$ exists for every $x \in M$ [@problem_id:3038491] [@problem_id:2969267].

The Busemann function also possesses a fundamental regularity property that is independent of curvature: it is always a **1-Lipschitz function**. This means that for any two points $x, y \in M$, the inequality $|b_\gamma(x) - b_\gamma(y)| \le d(x,y)$ holds. The proof is another straightforward application of the triangle inequality. For any $t \ge 0$:
$$
d(x, \gamma(t)) \le d(x,y) + d(y, \gamma(t))
$$
Subtracting $t$ from both sides and taking the limit as $t \to \infty$ yields:
$$
b_\gamma(x) \le d(x,y) + b_\gamma(y) \quad \implies \quad b_\gamma(x) - b_\gamma(y) \le d(x,y)
$$
By swapping the roles of $x$ and $y$, we obtain $b_\gamma(y) - b_\gamma(x) \le d(x,y)$. Together, these two inequalities confirm the 1-Lipschitz condition [@problem_id:3038491] [@problem_id:2969267] [@problem_id:3038494] [@problem_id:2969266].

To gain intuition for the Busemann function, it is instructive to evaluate it on the generating ray itself. For any $s \ge 0$, let's compute $b_\gamma(\gamma(s))$. By definition, and since we can assume $t > s$ in the limit:
$$
b_\gamma(\gamma(s)) = \lim_{t\to\infty} \big( d(\gamma(s), \gamma(t)) - t \big) = \lim_{t\to\infty} \big( (t-s) - t \big) = -s
$$
This simple but crucial result shows that the Busemann function linearly parameterizes the ray $\gamma$, decreasing with unit speed as we travel along it [@problem_id:3038491] [@problem_id:3038494]. Two rays $\gamma_1$ and $\gamma_2$ are said to be **asymptotic** if the distance between them remains bounded, i.e., $\sup_{t \ge 0} d(\gamma_1(t), \gamma_2(t))  \infty$. It can be shown that two rays are asymptotic if and only if their corresponding Busemann functions differ by a constant value across the entire manifold [@problem_id:2969267]. This establishes the Busemann function as a canonical object associated not just with a single ray, but with an entire [asymptotic equivalence](@entry_id:273818) class of rays—a point on the "[boundary at infinity](@entry_id:634468)."

### Busemann Functions on Hadamard Manifolds

While Busemann functions are universally defined, their geometric character is most profoundly revealed in spaces with nonpositive [sectional curvature](@entry_id:159738). A **Hadamard manifold** (or Cartan-Hadamard manifold) is a complete, simply connected Riemannian manifold with [sectional curvature](@entry_id:159738) $K \le 0$ everywhere. These spaces are also known as **CAT(0) spaces** and serve as nonlinear generalizations of Euclidean space.

#### Convexity of the Busemann Function

The most important property of Busemann functions on Hadamard manifolds is that they are **convex**. A function $f: M \to \mathbb{R}$ is convex if its restriction to any geodesic is a convex function in the classical one-dimensional sense. That is, for any geodesic $\sigma$, the function $s \mapsto f(\sigma(s))$ is convex.

The proof of this fact elegantly combines two fundamental principles. First, a key feature of Hadamard manifolds is that for any fixed point $p \in M$, the [distance function](@entry_id:136611) $x \mapsto d(p,x)$ is convex. Second, the pointwise limit of a sequence of [convex functions](@entry_id:143075) is itself convex. Recall that the Busemann function is the limit of the functions $f_t(x) = d(x, \gamma(t)) - t$. For each fixed $t$, the function $x \mapsto d(x, \gamma(t))$ is the distance from the fixed point $\gamma(t)$, and is therefore convex. Adding the constant $-t$ preserves [convexity](@entry_id:138568). Thus, $b_\gamma$ is the [pointwise limit](@entry_id:193549) of a family of [convex functions](@entry_id:143075), and is consequently convex itself [@problem_id:3038491] [@problem_id:3038494] [@problem_id:3075466].

#### Geometric Consequences: Horospheres and Horoballs

The [convexity](@entry_id:138568) of Busemann functions has profound geometric implications for their level and [sublevel sets](@entry_id:636882).

*   A **[horosphere](@entry_id:191600)** centered at the point at infinity $[\gamma]$ is a level set of the Busemann function, $H_c = \{ x \in M \mid b_\gamma(x) = c \}$.
*   A **horoball** is a [sublevel set](@entry_id:172753), either open ($B_c = \{ x \in M \mid b_\gamma(x)  c \}$) or closed ($\bar{B}_c = \{ x \in M \mid b_\gamma(x) \le c \}$).

In Euclidean space $\mathbb{R}^n$, if $\gamma(t) = t v$ for a [unit vector](@entry_id:150575) $v$, the Busemann function is $b_\gamma(x) = -\langle x, v \rangle$. The horospheres are [hyperplanes](@entry_id:268044) orthogonal to $v$, and the horoballs are open or closed half-spaces.

A direct consequence of the [convexity](@entry_id:138568) of $b_\gamma$ is that all its [sublevel sets](@entry_id:636882) are **geodesically convex**. This means that for any two points in a closed horoball $\bar{B}_c$, the unique [minimizing geodesic](@entry_id:197967) segment connecting them is entirely contained within $\bar{B}_c$ [@problem_id:3038494].

However, one must be cautious not to overextend the analogy with Euclidean space.
1.  **Horoballs are generally unbounded.** In the Euclidean example, a half-space is clearly unbounded. This holds true in general Hadamard manifolds [@problem_id:3038494].
2.  **Horospheres are not [totally geodesic](@entry_id:183906) in general.** A hypersurface is [totally geodesic](@entry_id:183906) if any geodesic starting tangent to it remains within it. While this is true for [hyperplanes](@entry_id:268044) in $\mathbb{R}^n$, it fails in negatively curved spaces. In hyperbolic space $\mathbb{H}^n$, horospheres have constant [geodesic curvature](@entry_id:158028) 1 (for $K=-1$), whereas [totally geodesic](@entry_id:183906) [hypersurfaces](@entry_id:159491) have [geodesic curvature](@entry_id:158028) 0. This distinction is a crucial feature of negatively curved geometry [@problem_id:3038491] [@problem_id:2969266].

#### Differential Properties and Regularity

The [convexity](@entry_id:138568) of Busemann functions also determines their differential properties. On a Hadamard manifold, a Busemann function is always of class $C^1$. Its [gradient field](@entry_id:275893), $\nabla b_\gamma$, is well-defined and has a remarkable property: its norm is everywhere equal to 1.
$$
|\nabla b_\gamma(x)| = 1 \quad \text{for all } x \in M
$$
This can be proven by considering the directional derivative along the unique [geodesic ray](@entry_id:202351) from $x$ that is asymptotic to $\gamma$ [@problem_id:2969266] [@problem_id:2969252].

As a convex function, its Hessian, where defined, must be [positive semi-definite](@entry_id:262808): $\mathrm{Hess}\, b_\gamma \ge 0$. The Laplacian, $\Delta b_\gamma = \mathrm{tr}(\mathrm{Hess}\, b_\gamma)$, must therefore be non-negative. A function with a non-negative Laplacian is called **[subharmonic](@entry_id:171489)**. Thus, Busemann functions on Hadamard manifolds are [subharmonic](@entry_id:171489) [@problem_id:3075466].

While $C^1$ regularity is guaranteed, Busemann functions are not always $C^2$ smooth on a general Hadamard manifold [@problem_id:2969267] [@problem_id:3075466]. The failure of smoothness occurs at points that form an "asymptotic [cut locus](@entry_id:161337)." At such a point $x$, there is more than one [geodesic ray](@entry_id:202351) starting from $x$ that is asymptotic to $\gamma$. This corresponds to the initial velocity vectors of [minimizing geodesics](@entry_id:637576) from $x$ to $\gamma(t)$ having multiple [accumulation points](@entry_id:177089) as $t \to \infty$. Since the gradient $\nabla b_\gamma(x)$ is the limit of these velocity vectors (with a sign change), its value becomes ill-defined, leading to a "crease" or "ridge" in the function where it is not differentiable [@problem_id:3067334]. This behavior is prevented in manifolds where geodesics are forced to diverge, such as those with strictly negative curvature. It can, however, occur in manifolds that contain "flat strips," which are regions isometric to $\mathbb{R} \times [a,b]$ [@problem_id:3075466].

#### Quantitative Properties under Negative Curvature

If we strengthen the curvature hypothesis from $K \le 0$ to a strictly negative upper bound, $K \le -\kappa^2  0$ for some constant $\kappa > 0$, the properties of Busemann functions become even more rigid and quantitative.

Under this stricter condition, Busemann functions are guaranteed to be smooth (at least $C^2$ if the metric is sufficiently regular). The Hessian is not just [positive semi-definite](@entry_id:262808), but strictly [positive definite](@entry_id:149459) on the directions orthogonal to the gradient. The only null direction for the Hessian is the gradient direction itself:
$$
\ker(\mathrm{Hess}\, b_\gamma|_x) = \mathrm{span}\{\nabla b_\gamma(x)\}
$$
This reflects the fact that $b_\gamma$ changes linearly along the asymptotic [geodesic flow](@entry_id:270369) defined by $-\nabla b_\gamma$, but is strictly convex in all orthogonal directions [@problem_id:2969252].

This strict positivity can be quantified. The Hessian, which measures the second fundamental form of the horospheres, is bounded below: for any vector $V$ orthogonal to $\nabla b_\gamma$, we have $\mathrm{Hess}\, b_\gamma(V,V) \ge \kappa |V|^2$. Summing over an orthonormal basis gives a lower bound on the Laplacian, a result known as the **Laplacian [comparison theorem](@entry_id:637672)**:
$$
\Delta b_\gamma \ge (n-1)\kappa
$$
In the model space of [constant sectional curvature](@entry_id:272200) $K = -\kappa^2$ (hyperbolic space $\mathbb{H}^n_{-\kappa^2}$), these inequalities become equalities [@problem_id:2969252]. The Hessian and Laplacian are given by explicit formulas:
$$
\mathrm{Hess}\, b_\gamma = \kappa(g - db_\gamma \otimes db_\gamma) \quad \text{and} \quad \Delta b_\gamma = (n-1)\kappa
$$
Here, $db_\gamma \otimes db_\gamma$ is the tensor product of the 1-form $db_\gamma$ with itself. These formulas provide a powerful computational tool and a benchmark for comparison in more general [negatively curved manifolds](@entry_id:195581) [@problem_id:2969252] [@problem_id:2969266].

### The Asymptotic Viewpoint: The Boundary at Infinity

Busemann functions provide not just a tool for studying the interior of a manifold, but also a way to formalize and analyze its "[boundary at infinity](@entry_id:634468)."

#### Horofunctions and the Gromov Compactification

The idea can be placed in a more general context. For any proper [metric space](@entry_id:145912) $M$ (a space where closed balls are compact), one can define an embedding into a space of functions. Fix a basepoint $o \in M$. The map $\Phi: M \to C(M)/\mathbb{R}$ given by
$$
\Phi(x) = [y \mapsto d(x,y) - d(x,o)]
$$
is an injective embedding of $M$ into the [space of continuous functions](@entry_id:150395) on $M$ modulo constant functions [@problem_id:2969248]. The closure of the image, $\overline{\Phi(M)}$, is a [compact space](@entry_id:149800) known as the **horofunction [compactification](@entry_id:150518)** of $M$. The boundary points, $\partial_h M = \overline{\Phi(M)} \setminus \Phi(M)$, are represented by functions called **horofunctions**. Each horofunction arises as a limit of the normalized distance functions $y \mapsto d(x_n, y) - d(x_n, o)$ for some sequence $x_n$ that diverges to infinity [@problem_id:2969248].

For a Hadamard manifold, this abstract construction has a concrete [geometric realization](@entry_id:265700). A fundamental theorem states that the horofunction boundary $\partial_h M$ is naturally homeomorphic to the **visual boundary** $\partial_\infty M$, which is the set of [asymptotic equivalence](@entry_id:273818) classes of geodesic rays. Moreover, every horofunction is precisely a Busemann function for some [geodesic ray](@entry_id:202351) [@problem_id:2969248].

#### Horoballs and the Boundary Topology

This identification allows us to use Busemann functions to describe the topology of the [boundary at infinity](@entry_id:634468). The standard **cone topology** on $\partial_\infty M$ is one where two rays are "close" if their initial segments stay close for a long time. It turns out that this topology can also be described using horoballs.

For a point $\xi \in \partial_\infty M$ and $R > 0$, define a "neighborhood" in the boundary:
$$
U_R(\xi) = \{ \eta \in \partial_\infty M \mid \text{the ray } \gamma_\eta \text{ eventually enters and stays in the horoball } B_R(\xi) \}
$$
where $B_R(\xi) = \{x \in M \mid b_\xi(x)  -R \}$. The behavior of these sets depends critically on the curvature.

If the manifold has a "flat strip" (e.g., Euclidean space $\mathbb{R}^n$ or a product like $\mathbb{H}^n \times \mathbb{R}$), then $U_R(\xi)$ is a large, fixed set (a hemisphere in the case of $\mathbb{R}^n$) that does not shrink as $R \to \infty$. In this case, these sets do not form a basis for the topology [@problem_id:2978397].

However, if the manifold has no flat strips—a property known as the **[visibility axiom](@entry_id:190181)**, which holds if $K \le -\kappa^2  0$—then the situation is different. For any two distinct points $\xi, \eta \in \partial_\infty M$, their corresponding rays diverge sufficiently fast such that for any deep enough horoball around $\xi$, the ray $\gamma_\eta$ will not enter it. This means the sets $U_R(\xi)$ shrink to the single point $\{\xi\}$ as $R \to \infty$, and the family $\{U_R(\xi)\}_{R>0}$ forms a [neighborhood basis](@entry_id:148053) for the cone topology at $\xi$. In this way, Busemann functions provide the very [coordinate charts](@entry_id:262338) used to define the structure of the [boundary at infinity](@entry_id:634468) [@problem_id:2978397].

### Generalization to Non-negative Ricci Curvature and the Splitting Theorem

The theory of Busemann functions extends powerfully beyond the realm of nonpositive [sectional curvature](@entry_id:159738) to manifolds satisfying a weaker condition on the **Ricci curvature**, $\mathrm{Ric} \ge 0$. On a complete manifold with non-negative Ricci curvature, Busemann functions are still convex [@problem_id:3025625]. This is a much deeper result, whose proof relies on the Hessian [comparison theorem](@entry_id:637672) for the distance function, which states that under $\mathrm{Ric} \ge 0$, $\mathrm{Hess}\, d_p \le \frac{1}{d_p} g$ in a certain sense. This implies that the functions $f_t(x) = t - d(x,\gamma(t))$ are "almost convex" for large $t$, and their limit $b_\gamma$ is convex [@problem_id:3025625].

The true power of this generalization is revealed in the context of the **Cheeger-Gromoll Splitting Theorem**. This theorem states that any complete Riemannian manifold with $\mathrm{Ric} \ge 0$ that contains a **line** (a geodesic $\alpha: \mathbb{R} \to M$ that is minimizing between any two of its points) must split as an isometric product $M \cong N \times \mathbb{R}$, where $N$ is a manifold with $\mathrm{Ric} \ge 0$.

Busemann functions are the key to the proof. A line $\alpha$ gives rise to two opposing geodesic rays, $\alpha^+$ and $\alpha^-$. One can define the corresponding Busemann functions $b_{\alpha^+}$ and $b_{\alpha^-}$. A crucial calculation shows that both functions are affine when restricted to the line itself, and their sum, $b_{\alpha^+} + b_{\alpha^-}$, is constant everywhere on the manifold $M$ [@problem_id:3025625]. It can be further shown that these Busemann functions are in fact smooth. The function $b_{\alpha^+}$ (or $b_{\alpha^-}$) serves as a global [height function](@entry_id:271993) whose level sets are the leaves of the [foliation](@entry_id:160209) that gives the splitting of $M$ into $N \times \mathbb{R}$. In this way, Busemann functions transform a local geometric condition (the existence of a single line) into a global topological and metric conclusion (the splitting of the entire manifold).