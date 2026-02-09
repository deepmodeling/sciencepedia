## Introduction
The study of smooth manifolds is fundamentally concerned with understanding the relationships between them, which are encoded by smooth maps. While continuity offers a basic framework, the differentiable structure of manifolds allows for a far deeper analysis. This is achieved by examining the local linear behavior of a map through its differential, whose properties provide a powerful tool for classifying mappings and the geometric structures they induce. A central question is how to use these local properties to understand the global structure of a map and its image. This article addresses this by providing a comprehensive framework for classifying smooth maps, revealing how local injectivity or surjectivity of the differential leads to profound global geometric consequences.

Across three chapters, this article will guide you through this essential area of differential geometry. First, in **"Principles and Mechanisms"**, we will establish the foundational theory, defining immersions, submersions, and embeddings based on the rank of the differential and exploring their local structure via the Constant Rank Theorem. Next, **"Applications and Interdisciplinary Connections"** will demonstrate the power of these concepts, showing how they are used to construct new manifolds, realize abstract ones in Euclidean space, and link the geometries of different spaces through fibrations and curvature relations. Finally, **"Hands-On Practices"** will provide concrete exercises to solidify your understanding of these theoretical tools, bridging the gap between abstract definitions and practical computation.

## Principles and Mechanisms

In the study of smooth manifolds, a central theme is understanding how one manifold can be mapped into another. While continuity provides a baseline for such mappings, the smooth structure allows for a far more refined analysis. The key to this analysis lies in the local linear approximation of a smooth map, known as its differential. The properties of this differential at each point—specifically, its rank—provide a powerful lens through which we can classify maps and understand the geometric structures they create. This chapter will dissect the fundamental principles governing smooth maps, focusing on the pivotal concepts of immersions, submersions, and embeddings.

### The Differential as a Local Litmus Test

Let $M$ and $N$ be smooth manifolds of dimensions $m$ and $n$, respectively, and let $f: M \to N$ be a smooth map. For any point $p \in M$, the **differential** of $f$ at $p$ is a linear map between the tangent spaces, $df_p: T_pM \to T_{f(p)}N$. This map encapsulates the complete first-order behavior of $f$ in a neighborhood of $p$. The most important invariant of this linear map is its **rank**, the dimension of its image.

While the differential $df_p$ is an abstract, coordinate-free object, its rank can be computed using local coordinates. Let $(U, \varphi)$ be a chart around $p$ and $(V, \psi)$ be a chart around $f(p)$. The map $f$ has a local coordinate representation $\tilde{f} = \psi \circ f \circ \varphi^{-1}: \mathbb{R}^m \to \mathbb{R}^n$. The matrix representation of $df_p$ with respect to the bases induced by these charts is the familiar **Jacobian matrix** of $\tilde{f}$ evaluated at $\varphi(p)$, denoted $D\tilde{f}(\varphi(p))$. The rank of the linear map $df_p$ is precisely the rank of this matrix [@problem_id:3051016].

A crucial question is whether this rank depends on the chosen coordinate systems. If it did, it would not be an intrinsic property of the map $f$ itself. Fortunately, the rank is independent of the choice of charts. If we choose different charts, say $(U', \varphi')$ and $(V', \psi')$, the new Jacobian matrix is related to the old one by multiplication with the Jacobian matrices of the transition maps. Since transition maps are diffeomorphisms, their Jacobians are invertible matrices. A fundamental result from linear algebra states that multiplying a matrix by invertible matrices on the left or right does not change its rank. Therefore, the rank of the differential is a well-defined, intrinsic property of the smooth map at each point, providing a robust foundation for classifying maps based on their local behavior [@problem_id:3051016].

### A Taxonomy of Smooth Maps: Immersions and Submersions

The rank of the differential $df_p$ can range from $0$ to $\min(m, n)$. We are particularly interested in cases where the rank is maximal at every point, which gives rise to two fundamental classes of maps.

An **immersion** is a smooth map $f: M \to N$ whose differential $df_p$ is **injective** at every point $p \in M$. For a linear map to be injective, the dimension of the domain cannot exceed the dimension of the codomain, so a necessary condition for an immersion is $m \le n$. Injectivity of $df_p$ means that its kernel is trivial, and by the rank-nullity theorem, its rank must equal the dimension of the domain, i.e., $\mathrm{rank}(df_p) = m$.

A **submersion** is a smooth map $f: M \to N$ whose differential $df_p$ is **surjective** at every point $p \in M$. For a linear map to be surjective, the dimension of the domain must be at least the dimension of the codomain, so a necessary condition for a submersion is $m \ge n$. Surjectivity of $df_p$ means its image is the entire codomain tangent space, so its rank must equal the dimension of the codomain, i.e., $\mathrm{rank}(df_p) = n$.

It is essential to distinguish these properties. Consider the projection map $\pi: \mathbb{R}^2 \to \mathbb{R}$ given by $\pi(x,y) = x$. The Jacobian matrix is $\begin{pmatrix} 1 & 0 \end{pmatrix}$, which has rank $1$. Since the target dimension is $n=1$, the differential is surjective everywhere, and $\pi$ is a submersion. However, the domain dimension is $m=2$. A linear map from a 2-dimensional space to a 1-dimensional space cannot be injective, so $\pi$ is not an immersion [@problem_id:3066018].

Conversely, an immersion is not necessarily a submersion. In the special case where $\dim M = \dim N$, a linear map is injective if and only if it is surjective. Therefore, a smooth map $f: M \to N$ with $\dim M = \dim N$ is an immersion if and only if it is a submersion. By the Inverse Function Theorem, such a map is a **local diffeomorphism**.

### Local Normal Forms: The Constant Rank Theorem

The definitions of immersions and submersions impose a condition on the rank of the differential at *every* point. This constancy of rank is extremely powerful. The **Constant Rank Theorem** states that if a smooth map has constant rank $r$ in a neighborhood of a point, then it can be represented in a particularly simple form in suitable local coordinates.

For an **immersion** $f: M^m \to N^n$, the rank is constantly $m$. The Constant Rank Theorem implies that for any $p \in M$, there exist charts around $p$ and $f(p)$ in which $f$ takes the form of a standard inclusion of $\mathbb{R}^m$ into $\mathbb{R}^n$:
$$
(x_1, \dots, x_m) \mapsto (x_1, \dots, x_m, 0, \dots, 0)
$$
This is the **Immersion Theorem**. It tells us that, locally, every immersion "looks like" the inclusion of a plane into a higher-dimensional space. An immediate consequence is that an immersion is a local embedding; that is, for a sufficiently small neighborhood $U$ of any point, the restriction $f|_U$ is an embedding [@problem_id:3052939].

For a **submersion** $f: M^m \to N^n$, the rank is constantly $n$. The Constant Rank Theorem implies that for any $p \in M$, there exist charts around $p$ and $f(p)$ in which $f$ takes the form of a standard projection:
$$
(x_1, \dots, x_m) \mapsto (x_1, \dots, x_n)
$$
This is the **Submersion Theorem**. It tells us that, locally, every submersion "looks like" a projection from a higher-dimensional space onto a lower-dimensional one [@problem_id:3052939]. This local picture is the foundation for the theory of fibrations.

### From Local to Global: Injective Immersions and Embeddings

The local picture of an immersion is deceptively simple. Globally, immersions can exhibit complex behavior. They are not necessarily injective. For example, the map $f: \mathbb{R} \to \mathbb{R}^2$ given by $f(t) = (\sin t, \sin 2t)$ is an immersion because its derivative $f'(t) = (\cos t, 2\cos 2t)$ never vanishes. However, it is not injective, as $f(0) = f(\pi) = (0,0)$. Its image is a figure-eight curve that crosses itself at the origin [@problem_id:3066018, @problem_id:2980336]. Similarly, the covering map $\gamma: \mathbb{R} \to S^1$ given by $\gamma(t) = (\cos t, \sin t)$ is an immersion, but it is periodic and thus highly non-injective [@problem_id:3066018].

This leads to a crucial distinction between an immersion and an embedding. A smooth map $f: M \to N$ is a **smooth embedding** if it is an immersion and also a **homeomorphism** onto its image $f(M)$ (where $f(M)$ is given the subspace topology from $N$) [@problem_id:3050997]. A homeomorphism is a continuous bijection with a continuous inverse.

For an immersion to be an embedding, it must first be injective. But injectivity alone is not sufficient. Consider the map $f: \mathbb{R} \to \mathbb{T}^2 = S^1 \times S^1$ given by $f(t) = (e^{2\pi i t}, e^{2\pi i \alpha t})$, where $\alpha$ is an irrational number. This is an injective immersion. However, its image is a dense winding line on the torus. The map is not a homeomorphism onto its image because the inverse map is not continuous. We can find points in the image that are very close together, but whose preimages in $\mathbb{R}$ are very far apart. This pathology prevents the subspace topology on the image from matching the topology of the domain $\mathbb{R}$ [@problem_id:3050997].

When does an injective immersion become an embedding? A powerful theorem provides a sufficient condition: **an injective immersion from a compact manifold is always an embedding**. If $M$ is compact, any continuous bijection from $M$ to a Hausdorff space (like $f(M)$) is automatically a homeomorphism. This means that for compact domains, the pathological behavior of the irrational torus winding cannot occur [@problem_id:3050997].

The image of an embedding is called an **embedded submanifold**. Its topology is simply the one it inherits as a subspace of the ambient manifold $N$. For example, the unit sphere $S^2$ is an embedded submanifold of $\mathbb{R}^3$. In contrast, the image of an immersion is an **immersed submanifold**. Its topology is the one transferred from the domain via the map, which can be finer (have more open sets) than the subspace topology if the map is not an embedding. The figure-eight curve is an immersed, but not embedded, submanifold of $\mathbb{R}^2$.

### Constructing Submanifolds via the Preimage Theorem

While embeddings provide a direct way to define submanifolds, one of the most powerful methods for constructing them arises from submersions. This method is encapsulated in the Preimage Theorem.

First, we must define the key terms. A point $p \in M$ is a **critical point** of $f: M \to N$ if the differential $df_p$ is not surjective. A point $y \in N$ is a **critical value** if it is the image of some critical point, i.e., $y \in f(\text{Crit}(f))$.

Conversely, a point $y \in N$ is a **regular value** of $f$ if $df_p$ is surjective for **every** point $p$ in the preimage $f^{-1}(y)$. It is crucial to note the universal quantifier "for every"; if even one point in the preimage is critical, $y$ is not a regular value. An important subtlety is that if the preimage $f^{-1}(y)$ is empty, the condition is vacuously satisfied, and $y$ is a regular value by definition [@problem_id:3052936] [@problem_id:3079608].

With these definitions, we can state the **Preimage Theorem** (also known as the Regular Value Theorem):

> If $y \in N$ is a regular value of a smooth map $f: M^m \to N^n$, then the preimage $f^{-1}(y)$ is a properly embedded submanifold of $M$ of dimension $m-n$.

Furthermore, the tangent space to this submanifold at a point $p \in f^{-1}(y)$ is given precisely by the kernel of the differential:
$$
T_p(f^{-1}(y)) = \ker(df_p)
$$
This theorem is a cornerstone of differential topology. It allows us to define manifolds implicitly. For example, the unit sphere $S^{n-1} \subset \mathbb{R}^n$ can be defined as the preimage $f^{-1}(1)$ for the function $f: \mathbb{R}^n \to \mathbb{R}$ given by $f(x) = \|x\|^2 = x_1^2 + \dots + x_n^2$. The differential is $df_x = (2x_1, \dots, 2x_n)$, which is surjective (non-zero) for all $x \neq 0$. Since all points in the preimage of $1$ are non-zero, $1$ is a regular value, and $S^{n-1}$ is guaranteed to be an $(n-1)$-dimensional submanifold of $\mathbb{R}^n$.

The connection to submersions is now clear. If $f: M \to N$ is a submersion, then $df_p$ is surjective for *all* $p \in M$. This immediately implies that *every* point $y \in N$ is a regular value. As a direct consequence of the Preimage Theorem, for any submersion $f$, every fiber (preimage) $f^{-1}(y)$ is an embedded submanifold of $M$ of dimension $m-n$ [@problem_id:3052939].

### The Genericity of Regularity: Sard's Theorem

The Preimage Theorem is powerful, but it relies on finding a regular value. How can we be sure that such values exist? **Sard's Theorem** provides a profound answer: for a sufficiently smooth map, the set of critical values is "small" in the codomain.

More precisely, Sard's Theorem states:
> Let $f: M^m \to N^n$ be a map of class $C^k$. If $k > \max\{m-n, 0\}$, then the set of critical values of $f$ has Lebesgue measure zero in $N$.

A set of measure zero is negligible; for instance, it contains no open sets. This means its complement—the set of regular values—is a set of full measure and is therefore dense in $N$. In practical terms, this tells us that regular values are abundant. No matter where you look in the target manifold, there is a regular value nearby. This ensures that the Preimage Theorem is not a vacuous statement but a widely applicable tool [@problem_id:3052923]. The differentiability requirement is sharp; the theorem can fail if the map is not smooth enough.

### Geometric Enhancement: Riemannian Submersions

The concepts discussed so far belong to the realm of differential topology, relying only on the smooth structure of the manifolds. When the manifolds are endowed with Riemannian metrics, we can introduce more geometric structure.

A **Riemannian submersion** is a map $f: (M,g) \to (N,h)$ between Riemannian manifolds that is not only a smooth submersion, but also respects the metrics in a specific way. For a submersion, at each point $p \in M$, the tangent space $T_pM$ decomposes into an orthogonal direct sum of two subspaces:
1.  The **vertical distribution** $\mathcal{V}_p = \ker(df_p)$, which is the tangent space to the fiber $f^{-1}(f(p))$.
2.  The **horizontal distribution** $\mathcal{H}_p = (\mathcal{V}_p)^{\perp}$, its orthogonal complement with respect to the metric $g$.

The differential $df_p$ annihilates the vertical space. The key condition for a Riemannian submersion is that when restricted to the horizontal space, the differential must be a **linear isometry**. That is, for any two vectors $u, v \in \mathcal{H}_p$:
$$
h_{f(p)}(df_p(u), df_p(v)) = g_p(u, v)
$$
This means the map preserves lengths and angles of horizontal vectors. A Riemannian submersion provides a geometric decomposition of the manifold $M$ into a family of fibers (the preimages) and a "base space" $N$, where the geometry is linked in this precise isometric way. This concept is fundamental in many areas of geometry and physics, including the study of principal bundles and Kaluza-Klein theory [@problem_id:3051005].