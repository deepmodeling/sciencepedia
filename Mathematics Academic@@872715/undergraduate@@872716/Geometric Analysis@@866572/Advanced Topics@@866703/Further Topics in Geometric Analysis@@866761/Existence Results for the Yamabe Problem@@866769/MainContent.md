## Introduction
The quest for [canonical metrics](@entry_id:266957) on Riemannian manifolds is a central theme in modern geometry. One of the most celebrated achievements in this area is the solution to the Yamabe problem, which asks a fundamental question: can every smooth, closed Riemannian manifold be conformally deformed to have [constant scalar curvature](@entry_id:186408)? This problem sits at the crossroads of [conformal geometry](@entry_id:186351), [nonlinear analysis](@entry_id:168236), and the [calculus of variations](@entry_id:142234), and its resolution represents a triumph of [geometric analysis](@entry_id:157700). The article addresses the challenge of proving the existence of such a metric, a task complicated by profound analytical difficulties related to [scale invariance](@entry_id:143212) and a loss of compactness.

This article will guide you through the complete story of the Yamabe problem's solution. In "Principles and Mechanisms," we will translate the geometric question into the analytical framework of the Yamabe equation, explore the variational approach used to solve it, and dissect the celebrated three-part proof by Trudinger, Aubin, and Schoen. Following this, "Applications and Interdisciplinary Connections" will reveal the far-reaching consequences of this result, from classifying manifolds and uncovering [topological obstructions](@entry_id:634492) to its deep connections with general relativity. Finally, "Hands-On Practices" will provide concrete exercises to apply these concepts, solidifying your understanding of this landmark theorem.

## Principles and Mechanisms

The existence of a Riemannian metric with [constant scalar curvature](@entry_id:186408) within a given conformal class, known as the Yamabe problem, represents a landmark achievement in [geometric analysis](@entry_id:157700). Its solution is a rich interplay between [conformal geometry](@entry_id:186351), the [calculus of variations](@entry_id:142234), and the theory of [nonlinear partial differential equations](@entry_id:168847). This chapter elucidates the core principles and mechanisms that underpin the problem's formulation and its eventual resolution. We will transition from the geometric statement of the problem to its analytical formulation, explore the [variational methods](@entry_id:163656) used to tackle it, diagnose the profound analytical difficulties that arise, and finally, outline the celebrated proof of existence.

### From Conformal Geometry to the Yamabe Equation

The Yamabe problem is fundamentally a question in [conformal geometry](@entry_id:186351). On a closed, smooth Riemannian manifold $(M, g)$ of dimension $n \ge 3$, the set of all metrics that are pointwise rescalings of $g$ forms a **conformal class**, denoted $[g]$. Any metric $\tilde{g} \in [g]$ can be written as $\tilde{g} = f \cdot g$ for some smooth, positive function $f$ on $M$. For reasons of [conformal covariance](@entry_id:189180) that will become apparent, it is conventional to write this relationship as:
$$
\tilde{g} = u^{\frac{4}{n-2}} g
$$
where $u$ is a smooth, strictly positive function. For $\tilde{g}$ to be a well-defined, smooth Riemannian metric, the function $u$ must belong to $C^\infty(M)$ and satisfy $u(p) > 0$ for all $p \in M$. Smoothness of $u$ is necessary to ensure the coefficient function $u^{\frac{4}{n-2}}$ is smooth, and strict positivity is required for the metric tensor to remain [positive definite](@entry_id:149459) at every point [@problem_id:3048135].

The central question of the Yamabe problem is: does every conformal class $[g]$ on a closed manifold contain a metric with [constant scalar curvature](@entry_id:186408)? To translate this geometric question into an analytical one, we must understand how the [scalar curvature](@entry_id:157547) transforms under such a conformal change. This transformation law is most elegantly expressed through a special differential operator known as the **conformal Laplacian**.

For a metric $g$, the conformal Laplacian $L_g$ is defined as:
$$
L_g \phi = -a_n \Delta_g \phi + R_g \phi
$$
where $\phi$ is a [smooth function](@entry_id:158037), $\Delta_g$ is the Laplace–Beltrami operator (defined with the sign convention that its eigenvalues are non-negative), $R_g$ is the scalar curvature of $g$, and $a_n$ is the dimensional constant $a_n = \frac{4(n-1)}{n-2}$.

The significance of this operator lies in its remarkable transformation property. If $\tilde{g} = u^{\frac{4}{n-2}} g$, then the scalar curvature of the new metric, $R_{\tilde{g}}$, is related to the original geometry via $L_g$ by the following fundamental formula [@problem_id:3048189]:
$$
R_{\tilde{g}} = u^{-\frac{n+2}{n-2}} (L_g u)
$$
This formula is the linchpin of the entire problem. It connects the scalar curvature of the new metric $\tilde{g}$ to an operation on the conformal factor $u$ with respect to the old metric $g$. The problem of finding a metric $\tilde{g}$ with [constant scalar curvature](@entry_id:186408), say $R_{\tilde{g}} = \lambda$ for some constant $\lambda \in \mathbb{R}$, is now equivalent to finding a smooth positive function $u$ that solves [@problem_id:3048116]:
$$
\lambda = u^{-\frac{n+2}{n-2}} (L_g u)
$$
Multiplying by $u^{\frac{n+2}{n-2}}$, we arrive at the celebrated **Yamabe equation**:
$$
L_g u = \lambda u^{\frac{n+2}{n-2}}
$$
This is a semilinear elliptic [partial differential equation](@entry_id:141332) for the unknown function $u$. The existence of a [constant scalar curvature](@entry_id:186408) metric in the conformal class $[g]$ is thereby reduced to the existence of a positive, smooth solution to this PDE.

### The Variational Formulation

Solving a nonlinear PDE like the Yamabe equation directly is a formidable task. A powerful alternative is the **[calculus of variations](@entry_id:142234)**, which seeks solutions as critical points (e.g., minimizers) of an associated energy functional. The structure of the Yamabe equation suggests a natural candidate for such a functional.

We define the **Yamabe functional** $Q_g(u)$ for any non-zero function $u$ in the Sobolev space $H^1(M)$ (the completion of [smooth functions](@entry_id:138942) under the norm involving both the function and its gradient in $L^2$) as follows:
$$
Q_g(u) = \frac{\int_M u (L_g u) \,dV_g}{\left(\int_M |u|^{\frac{2n}{n-2}} \,dV_g\right)^{\frac{n-2}{n}}} = \frac{\int_M \left(a_n |\nabla_g u|^2 + R_g u^2\right) \,dV_g}{\left(\int_M |u|^{\frac{2n}{n-2}} \,dV_g\right)^{\frac{n-2}{n}}}
$$
The second equality follows from [integration by parts](@entry_id:136350). A formal calculation shows that the Euler-Lagrange equation for this functional is precisely the Yamabe equation, where the constant $\lambda$ appears as a Lagrange multiplier. Therefore, a minimizer of $Q_g(u)$ yields a solution to our problem.

The [infimum](@entry_id:140118) of this functional over the entire conformal class is a geometric invariant called the **Yamabe constant**, denoted $Y(M, [g])$:
$$
Y(M, [g]) = \inf_{u \in H^1(M) \setminus \{0\}} Q_g(u)
$$
This functional and its [infimum](@entry_id:140118) have two crucial properties [@problem_id:3048169]:
1.  **Homogeneity:** The functional is homogeneous of degree 0, meaning $Q_g(tu) = Q_g(u)$ for any scalar $t>0$. This allows us to restrict the minimization problem to the constraint manifold of functions satisfying $\int_M |u|^{\frac{2n}{n-2}} \,dV_g = 1$.
2.  **Conformal Invariance:** The value of the Yamabe constant $Y(M, [g])$ depends only on the conformal class $[g]$, not on the specific choice of representative metric $g$ used to compute it. This confirms it is a true geometric invariant.

The sign of $Y(M, [g])$ partitions the problem into three distinct cases, corresponding to the sign of the first eigenvalue $\lambda_1(L_g)$ of the conformal Laplacian. The cases where $Y(M, [g]) \le 0$ are analytically simpler. The primary challenge arises in the positive case, $Y(M, [g]) > 0$, which is our main focus [@problem_id:3048189] [@problem_id:3048169]. To solve the problem here, one must prove that the [infimum](@entry_id:140118) $Y(M, [g])$ is achieved by some smooth positive function $u$.

### The Analytical Obstacle: Lack of Compactness

The standard strategy for proving the existence of a minimizer is the **direct method in the [calculus of variations](@entry_id:142234)**. One takes a minimizing sequence $\{u_k\}$, i.e., a sequence such that $Q_g(u_k) \to Y(M, [g])$, and attempts to extract a convergent subsequence whose limit is the desired minimizer. This method hinges on a property called **compactness**.

The Yamabe functional involves two norms: the $H^1$ norm in the numerator and the $L^p$ norm in the denominator, where $p = \frac{2n}{n-2}$. According to the **Sobolev [embedding theorem](@entry_id:150872)** on a compact $n$-manifold ($n \ge 3$), the space $H^1(M)$ embeds continuously into $L^q(M)$ for all $1 \le q \le \frac{2n}{n-2}$. Furthermore, by the Rellich-Kondrachov theorem, this embedding is **compact** for any exponent $q  \frac{2n}{n-2}$.

The exponent $p = \frac{2n}{n-2}$ is known as the **critical Sobolev exponent**. At this precise exponent, the embedding $H^1(M) \hookrightarrow L^{\frac{2n}{n-2}}(M)$ ceases to be compact [@problem_id:3048163]. This lack of compactness is the central analytical difficulty of the Yamabe problem. It means that a sequence $\{u_k\}$ that is bounded in $H^1(M)$ is not guaranteed to have a subsequence that converges strongly in $L^{\frac{2n}{n-2}}(M)$.

For a minimizing sequence $\{u_k\}$ normalized such that $\int_M |u_k|^{\frac{2n}{n-2}} \,dV_g = 1$, we can always find a weak limit $u$. However, due to the lack of compactness, we can only conclude that $\int_M |u|^{\frac{2n}{n-2}} \,dV_g \le 1$. It is possible for the "mass" of the $L^{\frac{2n}{n-2}}$-norm to be lost in the weak limit, for example if $u \equiv 0$ or if the inequality is strict. In such a scenario, the direct method fails, as the limit function does not satisfy the constraint and is not a minimizer [@problem_id:3048166].

The geometric origin of this failure is **scale invariance**. On Euclidean space $\mathbb{R}^n$, the homogeneous Sobolev [seminorm](@entry_id:264573) $\|\nabla f\|_{L^2(\mathbb{R}^n)}$ and the critical norm $\|f\|_{L^{\frac{2n}{n-2}}(\mathbb{R}^n)}$ exhibit the same behavior under the [scaling transformation](@entry_id:166413) $f(x) \mapsto \lambda^{\frac{n-2}{2}} f(\lambda x)$. This invariance allows for the existence of functions, known as **bubbles**, that can be arbitrarily concentrated at a point while keeping these two norms constant. When such profiles are transplanted onto a manifold, they generate minimizing sequences that concentrate their energy at one or more points. This phenomenon of **concentration** or **bubbling** is the manifestation of the lack of compactness [@problem_id:3048178].

### The Path to Existence: A Trilogy of Results

The resolution of the Yamabe problem is a triumphal story of modern geometry, unfolding in three main acts, associated with the work of Neil Trudinger, Thierry Aubin, and Richard Schoen [@problem_id:3048133].

#### Act I: Trudinger's Dichotomy

Neil Trudinger's foundational work established a crucial dichotomy. He demonstrated that the [bubbling phenomenon](@entry_id:183569) is not arbitrary; it is tied to a [specific energy](@entry_id:271007) level. By analyzing a concentrating sequence, one finds that its Yamabe quotient $Q_g(u_k)$ must approach the Yamabe constant of the standard round sphere, $Y(S^n, [g_{\text{round}}])$. This value represents the best constant for the critical Sobolev inequality on $\mathbb{R}^n$.

This leads to Trudinger's criterion: if the Yamabe invariant of the manifold is strictly less than that of the sphere,
$$
Y(M, [g])  Y(S^n, [g_{\text{round}}])
$$
then a minimizing sequence cannot lose mass to bubbles. The energy level is simply too low for a bubble to form. In this case, compactness is restored for the minimizing sequence, and the existence of a smooth, positive minimizer is guaranteed [@problem_id:3048119]. The Yamabe problem was thus reduced to verifying this strict inequality.

#### Act II: Aubin's Inequality

The next major breakthrough came from Thierry Aubin. His strategy was to test the strict inequality directly. First, by constructing ingenious [test functions](@entry_id:166589) that mimic the behavior of bubbles, he proved the universal inequality [@problem_id:3048124]:
$$
Y(M, [g]) \le Y(S^n, [g_{\text{round}}])
$$
for any [compact manifold](@entry_id:158804) $(M,g)$. This showed that the round sphere is maximal in terms of its Yamabe invariant.

Aubin then performed a more refined [asymptotic analysis](@entry_id:160416) of these [test functions](@entry_id:166589). The expansion of the Yamabe functional for a highly concentrated [test function](@entry_id:178872) includes terms that depend on the local geometry of the manifold, such as the Weyl tensor and the [scalar curvature](@entry_id:157547). He showed that if the manifold $(M,g)$ is not locally conformally flat and its dimension is $n \ge 6$, these geometric terms force the Yamabe quotient of the test functions to lie strictly below $Y(S^n, [g_{\text{round}}])$, thus proving the strict inequality. This solved the Yamabe problem for a vast class of manifolds, but left open the cases of low dimensions ($n=3, 4, 5$) and locally conformally flat manifolds.

#### Act III: Schoen's Completion and the Positive Mass Theorem

The final, and most difficult, cases were resolved by Richard Schoen. His work addressed the critical threshold where $Y(M, [g]) = Y(S^n, [g_{\text{round}}])$. He showed, by contradiction, that this equality can only hold if $(M,g)$ is conformally equivalent to the standard sphere (in which case a solution trivially exists).

Schoen's proof is a profound application of ideas from mathematical general relativity. He argued that if a minimizing sequence were to bubble at a point $p$, a "blow-up" analysis of the geometry near $p$ would produce a complete, [asymptotically flat manifold](@entry_id:181302) with non-negative [scalar curvature](@entry_id:157547). A key invariant of such a manifold is its ADM mass. Schoen, building on joint work with S.-T. Yau, related this mass to the geometry of the original manifold $(M,g)$ through its Green's function for the conformal Laplacian. He then invoked the **Positive Mass Theorem**, a deep result stating that the ADM mass of such a manifold is non-negative, and is zero if and only if the manifold is isometric to Euclidean space. Schoen's analysis showed that a bubbling sequence on a manifold not conformal to the sphere would lead to a contradiction with this theorem. This ruled out the possibility of bubbling in all remaining non-trivial cases [@problem_id:3048148].

With Schoen's work, the proof was complete. For any closed Riemannian manifold $(M,g)$ of dimension $n \ge 3$, one of two situations must occur:
1.  The manifold is conformally equivalent to the standard sphere, in which case a [constant scalar curvature](@entry_id:186408) metric already exists in its conformal class.
2.  The manifold is not conformally equivalent to the standard sphere, in which case the strict inequality $Y(M, [g])  Y(S^n, [g_{\text{round}}])$ holds. By Trudinger's criterion, a minimizer for the Yamabe functional exists, yielding a solution to the Yamabe problem.

In every case, a metric of [constant scalar curvature](@entry_id:186408) is guaranteed to exist.