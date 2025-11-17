## Introduction
The study of [partial differential equations](@entry_id:143134) (PDEs) on [curved spaces](@entry_id:204335) is a central pursuit in modern mathematics and physics, yet it presents a fundamental challenge: how do we analyze functions and their derivatives on a space without a global coordinate system? The answer lies at the powerful intersection of [differential geometry](@entry_id:145818) and functional analysis, in the form of Sobolev embedding theorems on manifolds. These theorems provide the essential toolkit for making sense of "weak" solutions to PDEs and understanding their qualitative properties, bridging the gap between abstract analytic data and concrete geometric behavior. This article provides a comprehensive introduction to this vital theory.

We will begin in the **Principles and Mechanisms** chapter by building the necessary foundations. You will learn how to define Sobolev spaces on a Riemannian manifold, both through a practical local-to-global construction and an intrinsic geometric definition. We will then state and outline the proofs for the main Sobolev embedding theorems and their crucial refinements, such as the Rellich-Kondrachov [compactness theorem](@entry_id:148512) and the Moser-Trudinger inequality.

Next, in the **Applications and Interdisciplinary Connections** chapter, we will see these theorems in action. You will discover how they are used to establish the smoothness of solutions to PDEs, to prove fundamental results in [spectral geometry](@entry_id:186460), and to tackle famous challenges in geometric analysis like the Yamabe problem.

Finally, the **Hands-On Practices** section will offer opportunities to solidify your understanding by working through concrete problems, exploring how these powerful analytic tools are applied to specific geometric settings like the sphere and the torus.

## Principles and Mechanisms

### Foundational Structures: Geometry and Analysis

The study of Sobolev embedding theorems on manifolds lies at the confluence of [differential geometry](@entry_id:145818) and [functional analysis](@entry_id:146220). To embark on this study, we must first establish our geometric stage and our analytic tools.

#### The Geometric Arena: Smooth Riemannian Manifolds

The natural setting for [geometric analysis](@entry_id:157700) is a **[smooth manifold](@entry_id:156564)**. A [smooth manifold](@entry_id:156564) $M$ of dimension $n$ is a topological space that is Hausdorff, second-countable, and locally resembles Euclidean space $\mathbb{R}^n$. This local resemblance is formalized through an atlas of [coordinate charts](@entry_id:262338), which are homeomorphisms from open sets of $M$ to open sets in $\mathbb{R}^n$. Crucially, for a *smooth* manifold, the transition maps between any two overlapping charts are required to be infinitely differentiable ($C^\infty$). This [compatibility condition](@entry_id:171102) ensures that the concept of [differentiability](@entry_id:140863) for functions on the manifold is well-defined, independent of the choice of coordinates.

While the [smooth structure](@entry_id:159394) allows for calculus, it does not inherently provide a way to measure lengths, angles, or volumes. This geometric structure is introduced by a **Riemannian metric**, denoted by $g$. A Riemannian metric is a smooth field of inner products on the tangent spaces of the manifold. That is, for each point $x \in M$, the metric provides a [bilinear map](@entry_id:150924) $g_x: T_x M \times T_x M \to \mathbb{R}$ that is symmetric and positive-definite. The smoothness of the metric ensures that as we move from point to point on the manifold, these inner products vary in a $C^\infty$ manner [@problem_id:3063214].

This structure is fundamental. The inner product $g_x$ allows us to define the length of a tangent vector $v \in T_x M$ as $\|v\|_{g_x} = \sqrt{g_x(v,v)}$. From this, we can measure the lengths of curves, define distances, and, importantly for our purposes, define pointwise norms of vector and [tensor fields](@entry_id:190170). The metric also induces a canonical [volume element](@entry_id:267802), denoted $dV_g$, which provides a consistent way to integrate functions over the manifold. Together, the pointwise norms and the volume measure are the essential ingredients for building function spaces on $M$.

#### The Analytic Framework: Sobolev Spaces in Euclidean Space

Before defining [function spaces](@entry_id:143478) on manifolds, we must first understand their counterparts in the simpler setting of Euclidean space. Classical [function spaces](@entry_id:143478) like $C^k(\Omega)$, the space of $k$-times continuously differentiable functions on an open set $\Omega \subset \mathbb{R}^n$, are often too restrictive for the study of [partial differential equations](@entry_id:143134) (PDEs), as solutions may not possess classical derivatives. Sobolev spaces provide a powerful extension by defining derivatives in a "weak" sense.

Let $u$ be a [locally integrable function](@entry_id:175678) on $\Omega$. We say that a function $v \in L^1_{\text{loc}}(\Omega)$ is the **weak $\alpha$-th partial derivative** of $u$, denoted $v = D^\alpha u$, if it satisfies the following identity for all [test functions](@entry_id:166589) $\varphi \in C_c^\infty(\Omega)$ ([smooth functions](@entry_id:138942) with [compact support](@entry_id:276214) in $\Omega$):
$$
\int_\Omega u \, D^\alpha \varphi \, dx = (-1)^{|\alpha|} \int_\Omega v \, \varphi \, dx
$$
This definition is motivated by the [integration by parts](@entry_id:136350) formula, which holds for smooth functions. The key insight is that the left-hand side is well-defined even if $u$ is not differentiable, allowing us to transfer the derivatives from the (potentially non-smooth) function $u$ to the infinitely smooth test function $\varphi$.

With this concept, we can define the **Sobolev space** $W^{k,p}(\Omega)$ for an integer $k \ge 0$ and $1 \le p \le \infty$. It consists of all functions $u \in L^p(\Omega)$ such that for every multi-index $\alpha$ with order $|\alpha| \le k$, the [weak derivative](@entry_id:138481) $D^\alpha u$ exists and also belongs to $L^p(\Omega)$ [@problem_id:3063242]. This space is a Banach space when equipped with a norm that controls the function and all its [weak derivatives](@entry_id:189356) up to order $k$, such as:
$$
\|u\|_{W^{k,p}(\Omega)} = \left( \sum_{|\alpha| \le k} \|D^\alpha u\|_{L^p(\Omega)}^p \right)^{1/p}
$$
These spaces are the fundamental building blocks for the theory of Sobolev embeddings on manifolds.

### Constructing Sobolev Spaces on Manifolds

The primary challenge in generalizing Sobolev spaces to a manifold $M$ is the absence of a global coordinate system. How can we speak of partial derivatives in a coordinate-free way? The solution lies in a "local-to-global" construction that patches together local, Euclidean-based definitions.

#### The Local-to-Global Approach via Partitions of Unity

For a [compact manifold](@entry_id:158804) $M$, we can find a finite atlas of [coordinate charts](@entry_id:262338) $\{(U_i, \varphi_i)\}_{i=1}^N$ that covers $M$. We can also construct a **smooth partition of unity** $\{\chi_i\}_{i=1}^N$ subordinate to this cover. This is a collection of [smooth functions](@entry_id:138942) $\chi_i: M \to \mathbb{R}$ such that:
1.  $0 \le \chi_i(x) \le 1$ for all $x \in M$.
2.  The support of each $\chi_i$ is contained in the corresponding chart domain $U_i$.
3.  $\sum_{i=1}^N \chi_i(x) = 1$ for all $x \in M$.

This tool allows us to decompose any function $u$ on $M$ into a finite sum $u = \sum_{i=1}^N \chi_i u$, where each piece $\chi_i u$ is supported within a single [coordinate chart](@entry_id:263963) $U_i$. We can then define the Sobolev space $W^{k,p}(M)$ as the set of functions $u \in L^p(M)$ for which the norm
$$
\|u\|_{\text{charts}} := \left( \sum_{i=1}^N \|(\chi_i u) \circ \varphi_i^{-1}\|_{W^{k,p}(\varphi_i(U_i))}^p \right)^{1/p}
$$
is finite. Here, $(\chi_i u) \circ \varphi_i^{-1}$ is the representation of the function piece in the [local coordinates](@entry_id:181200) of the chart $\varphi_i(U_i) \subset \mathbb{R}^n$, and its $W^{k,p}$ norm is the standard Euclidean Sobolev norm.

A crucial theorem states that for a compact manifold, any two choices of finite atlas and subordinate [partition of unity](@entry_id:141893) produce [equivalent norms](@entry_id:268877). This means that while the value of the norm depends on the specific choice of charts, the set of functions with finite norm does not. Consequently, the space $W^{k,p}(M)$ is well-defined as a Banach space, independent of the construction details [@problem_id:3063231].

#### The Intrinsic Definition

The chart-based construction, while practical, may seem artificial. Fortunately, the Riemannian metric $g$ allows for an equivalent, intrinsically geometric definition. The metric gives rise to a canonical **covariant derivative**, or connection, denoted $\nabla$, which is a coordinate-invariant way to differentiate vector fields. This can be extended to define iterated covariant derivatives $\nabla^j u$ of a function $u$. Using the pointwise norm $|\cdot|_g$ and the volume form $dV_g$ induced by the metric, we can define an intrinsic Sobolev norm:
$$
\|u\|_{W^{k,p}(M,g)} = \left( \sum_{j=0}^k \int_M |\nabla^j u|_g^p \, dV_g \right)^{1/p}
$$
On a compact manifold, this intrinsic norm is equivalent to any norm constructed using charts and [partitions of unity](@entry_id:152644) [@problem_id:3063231]. This equivalence confirms that Sobolev spaces on manifolds are natural objects, deeply tied to the underlying geometry.

### The Sobolev Embedding Theorems on Manifolds

The "smoothness" of a function in a Sobolev space is determined by the interplay of its [differentiability](@entry_id:140863) order $k$, its integrability exponent $p$, and the dimension of the space $n$. Sobolev embedding theorems make this relationship precise by establishing when one Sobolev space is continuously included in another. An embedding $W^{k,p}(M) \hookrightarrow W^{m,q}(M)$ signifies that any function with $k$ [weak derivatives](@entry_id:189356) in $L^p$ is guaranteed to have $m$ [weak derivatives](@entry_id:189356) in $L^q$, and this relationship is continuous (i.e., bounded).

#### Statement and Proof Mechanism

The fundamental Sobolev [embedding theorem](@entry_id:150872) on a compact $n$-dimensional Riemannian manifold $M$ states the following:

**Theorem:** Let $k, m$ be integers with $k > m \ge 0$, and let $1 \le p,q \le \infty$. If the parameters satisfy the condition
$$
k - m \ge \frac{n}{p} - \frac{n}{q}
$$
then there is a continuous embedding $W^{k,p}(M) \hookrightarrow W^{m,q}(M)$ [@problem_id:3063226, @problem_id:3063227].

The proof of this theorem is a quintessential example of a local-to-global argument in [geometric analysis](@entry_id:157700), reducing the problem on the manifold to the known case on Euclidean space [@problem_id:3063201]. The strategy unfolds as follows:

1.  **Decomposition:** Take a function $f \in W^{k,p}(M)$ and decompose it using a finite [partition of unity](@entry_id:141893), $f = \sum_{i=1}^N \psi_i f$. Each $\psi_i f$ is supported in a [coordinate chart](@entry_id:263963) $U_i$.

2.  **Pullback to Charts:** For each piece, consider its coordinate representation $f_i = (\psi_i f) \circ \varphi_i^{-1}$, which is a function with [compact support](@entry_id:276214) in an open set $\varphi_i(U_i) \subset \mathbb{R}^n$.

3.  **Apply Euclidean Embedding:** Apply the known Euclidean Sobolev [embedding theorem](@entry_id:150872) to each $f_i$. This yields a local estimate of the form $\|f_i\|_{W^{m,q}(\mathbb{R}^n)} \le C_i \|f_i\|_{W^{k,p}(\mathbb{R}^n)}$.

4.  **Globalization:** Sum these local estimates. To control the global norm $\|f\|_{W^{m,q}(M)}$ by the sum of the local norms, we must carefully handle the overlaps between the supports of the [partition of unity](@entry_id:141893) functions. This requires the [partition of unity](@entry_id:141893) to have **bounded overlap**: there must be a uniform integer bound $L$ on the number of functions $\psi_i$ that are non-zero at any given point [@problem_id:3063241]. With bounded overlap and the finiteness of the atlas (a consequence of compactness), the local estimates can be summed to produce a global inequality $\|f\|_{W^{m,q}(M)} \le C \|f\|_{W^{k,p}(M)}$, establishing the continuous embedding.

This elegant argument demonstrates how geometric tools (atlases, [partitions of unity](@entry_id:152644)) allow us to leverage the full power of Euclidean analysis to prove deep results on [curved spaces](@entry_id:204335).

### Refinements and Special Cases

The general [embedding theorem](@entry_id:150872) has several crucial refinements that are central to its application in geometry and PDEs.

#### Compactness: The Rellich-Kondrachov Theorem

A much stronger property than a continuous embedding is a **[compact embedding](@entry_id:263276)**. An embedding $X \hookrightarrow Y$ is compact if it maps [bounded sets](@entry_id:157754) in $X$ to pre-compact sets in $Y$ (sets whose closure is compact). This means that any bounded sequence in $X$ has a subsequence that converges in the norm of $Y$. This property is invaluable for existence proofs in the calculus of variations and PDE theory.

The celebrated **Rellich-Kondrachov theorem** provides the condition for compactness. On a [compact manifold](@entry_id:158804), the Sobolev embedding is compact if the inequality relating the parameters is strict:

**Theorem (Rellich-Kondrachov on Manifolds):** The embedding $W^{k,p}(M) \hookrightarrow W^{m,q}(M)$ is **compact** if $k > m$ and
$$
k - m > \frac{n}{p} - \frac{n}{q}
$$
The most frequently used cases are for embeddings into spaces of functions ($m=0$):
*   If $1 \le p  n$, the embedding $W^{1,p}(M) \hookrightarrow L^q(M)$ is compact for all $q$ in the range $1 \le q  p^*$, where $p^* = \frac{np}{n-p}$ is the critical Sobolev exponent [@problem_id:3063205].
*   If $p=n$, the embedding $W^{1,n}(M) \hookrightarrow L^q(M)$ is compact for all finite $q \ge 1$ [@problem_id:3063205].

In the critical case where $k-m = n/p - n/q$, the embedding is continuous but famously *not* compact.

#### The Borderline Case $p=n$: The Moser-Trudinger Inequality

The case $p=n$ is particularly subtle. The scaling of the Sobolev inequality suggests that for $p=n$, one might expect an embedding of $W^{1,n}(M)$ into $L^\infty(M)$, the space of essentially bounded functions. However, this is false. One can construct a sequence of functions on $M$ that are uniformly bounded in the $W^{1,n}(M)$ norm but whose $L^\infty$ norms blow up to infinity. Such a [counterexample](@entry_id:148660) can be built by transplanting a sequence of logarithmically-peaked functions into a local [coordinate chart](@entry_id:263963), demonstrating the failure of the embedding [@problem_id:3063230].

The correct, sharp replacement for the failed embedding into $L^\infty$ is the **Moser-Trudinger inequality**. It reveals that while functions in $W^{1,n}(M)$ may be unbounded, their growth is controlled: they have exponential integrability.

**Theorem (Moser-Trudinger on Manifolds):** Let $(M,g)$ be a compact $n$-dimensional Riemannian manifold. There exist constants $\alpha > 0$ and $C > 0$ such that for any function $u \in W^{1,n}(M)$ with $\|\nabla u\|_{L^n(M)} \le 1$ and [zero mean](@entry_id:271600) value, the following inequality holds:
$$
\int_M \exp\left(\alpha \, |u|^{\frac{n}{n-1}}\right) \, dV_g \le C
$$
This result is sharp. There is a universal constant $\alpha_n = n \omega_{n-1}^{1/(n-1)}$ (where $\omega_{n-1}$ is the volume of the unit $(n-1)$-sphere) such that the inequality holds for all $\alpha \le \alpha_n$, but fails for any $\alpha > \alpha_n$. The sharpness on manifolds is a consequence of the local nature of the extremal functions, which can be replicated in a [coordinate chart](@entry_id:263963) on any manifold [@problem_id:3063230].

### Beyond the Compact Setting: The Role of Bounded Geometry

The local-to-global arguments described above rely heavily on the compactness of the manifold, which guarantees the existence of a finite atlas and simplifies control over constants. On [non-compact manifolds](@entry_id:262738), new difficulties arise. An atlas must be countable, leading to infinite sums, and geometric properties can vary wildly across the manifold, meaning there may be no uniform control over the constants in local Sobolev estimates.

To extend the theory to [non-compact manifolds](@entry_id:262738), one needs to impose conditions on the geometry to ensure a sufficient degree of uniformity. The key concept is **[bounded geometry](@entry_id:189959)**. A complete Riemannian manifold $(M,g)$ is said to have [bounded geometry](@entry_id:189959) if:
1.  Its [injectivity radius](@entry_id:192335) is uniformly bounded below by a positive constant: $\mathrm{inj}_g(M) \ge i_0 > 0$.
2.  Its Riemann curvature tensor and all of its covariant derivatives are uniformly bounded in norm across the manifold.

These conditions ensure that the manifold is "uniformly regular" at all scales. The lower bound on the injectivity radius allows one to cover any part of the manifold with normal [coordinate charts](@entry_id:262338) of a uniform size. The [curvature bounds](@entry_id:200421) guarantee that within these charts, the metric coefficients are uniformly equivalent to the Euclidean metric, and their derivatives are uniformly controlled.

Under the assumption of [bounded geometry](@entry_id:189959), the local-to-global proof mechanism can be resurrected. One can construct a partition of unity with uniformly bounded derivatives and overlap, and the constants in the local Sobolev estimates become uniform across the manifold. This allows one to prove that the Euclidean Sobolev embeddings carry over to [non-compact manifolds](@entry_id:262738) with [bounded geometry](@entry_id:189959), with embedding constants that are uniform on any precompact region [@problem_id:3063246]. This illustrates how controlling the geometry is essential for establishing global analytic properties.