## Introduction
The geometry of a submanifold is not defined in isolation; it is deeply intertwined with the geometry of the larger space in which it resides. In Riemannian geometry, understanding this relationship is a central challenge. How does the curvature of an ambient manifold influence the [intrinsic curvature](@entry_id:161701) of a [submanifold](@entry_id:262388)? How can we measure the way a submanifold 'bends' or 'twists' within its surroundings? This article addresses these fundamental questions by introducing the core concepts of [extrinsic geometry](@entry_id:262461). We will develop the essential machinery—the [second fundamental form](@entry_id:161454) and the shape operator—to precisely quantify the [extrinsic curvature](@entry_id:160405) of an immersion. These tools allow us to define and explore two canonical classes of [submanifolds](@entry_id:159439): [totally geodesic submanifolds](@entry_id:637049), which are extrinsically 'flat', and totally [umbilic submanifolds](@entry_id:637677), which curve isotropically at every point.

Across three chapters, this article will guide you from foundational theory to practical application. The first chapter, **Principles and Mechanisms**, establishes the definitions of the second fundamental form, the [shape operator](@entry_id:264703), and the fundamental equations of Gauss, Codazzi, and Ricci. The second chapter, **Applications and Interdisciplinary Connections**, explores the profound role these [submanifolds](@entry_id:159439) play in geometric analysis, general relativity, and Kähler geometry. Finally, the **Hands-On Practices** section provides concrete problems to solidify your understanding of these abstract concepts. By the end, you will have a robust framework for analyzing the geometry of submanifolds.

## Principles and Mechanisms

The geometry of an [immersed submanifold](@entry_id:264923) is intricately linked to the geometry of the [ambient space](@entry_id:184743). Understanding this relationship requires a set of tools to decompose the ambient curvature into components intrinsic and extrinsic to the [submanifold](@entry_id:262388). This chapter develops the foundational machinery of [extrinsic geometry](@entry_id:262461)—the [second fundamental form](@entry_id:161454) and the shape operator—and uses it to define and explore two canonical classes of submanifolds: [totally geodesic](@entry_id:183906) and totally [umbilic submanifolds](@entry_id:637677).

### The Second Fundamental Form and the Gauss Formula

Consider an [isometric immersion](@entry_id:272242) $i: (N^m, g) \hookrightarrow (M^n, \bar{g})$. At each point $p \in N$, the tangent space of the ambient manifold $M$ decomposes into an orthogonal direct sum of the tangent space to the [submanifold](@entry_id:262388) $N$ and its orthogonal complement, the [normal space](@entry_id:154487) $\nu_p N$. This decomposition extends to a bundle decomposition over $N$: $TM|_N = TN \oplus \nu$. The [vector bundle](@entry_id:157593) $\nu$ is called the **[normal bundle](@entry_id:272447)**. It is crucial to recognize that this decomposition is fundamentally **extrinsic**; it depends on how $N$ is situated within $M$ and cannot be defined from the [intrinsic geometry](@entry_id:158788) of $(N,g)$ alone [@problem_id:3005512].

The key to relating the geometries of $N$ and $M$ lies in comparing their respective Levi-Civita connections, $\nabla$ on $N$ and $\bar{\nabla}$ on $M$. For any two [vector fields](@entry_id:161384) $X, Y$ tangent to $N$, the ambient covariant derivative $\bar{\nabla}_X Y$ is a vector field along $N$ which, in general, has both a tangential and a normal component. The celebrated **Gauss formula** provides this decomposition:
$$
\bar{\nabla}_X Y = (\bar{\nabla}_X Y)^\top + (\bar{\nabla}_X Y)^\perp
$$
where $(\cdot)^\top$ and $(\cdot)^\perp$ denote the orthogonal projections onto $TN$ and $\nu$, respectively.

This equation serves as a definition for two fundamental objects. The tangential component is defined as the **[induced connection](@entry_id:635081)** on $N$, which can be proven to be the unique Levi-Civita connection $\nabla$ compatible with the [induced metric](@entry_id:160616) $g$. The normal component is a [tensor field](@entry_id:266532) that quantifies the failure of $N$ to be "flat" within $M$. This is the **second fundamental form**, denoted by $B$:
$$
B(X,Y) := (\bar{\nabla}_X Y)^\perp
$$
With these definitions, the Gauss formula is written as:
$$
\bar{\nabla}_X Y = \nabla_X Y + B(X,Y)
$$
The [second fundamental form](@entry_id:161454) $B$ is a symmetric, [bilinear map](@entry_id:150924) on $T_p N$ for each $p \in N$, with values in the normal space $\nu_p N$. Its symmetry, $B(X,Y) = B(Y,X)$, is a direct consequence of the torsion-free property of the ambient connection $\bar{\nabla}$, since $B(X,Y) - B(Y,X) = (\bar{\nabla}_X Y - \bar{\nabla}_Y X)^\perp = ([X,Y])^\perp = 0$, as the Lie bracket of two [vector fields](@entry_id:161384) tangent to a submanifold is also tangent to it.

Geometrically, $B(X,X)$ represents the initial [acceleration vector](@entry_id:175748) of a geodesic in $M$ that starts at $p$ with velocity $X$. If $B(X,X) \neq 0$, this geodesic immediately begins to curve away from the tangent space $T_p N$. A distribution of tangent planes $D \subset TM$ is called **autoparallel** if $\bar{\nabla}_X Y$ remains in $D$ for any vector fields $X,Y$ tangent to $D$. From the Gauss formula, we see that the tangent bundle $TN$ is an autoparallel distribution if and only if its [second fundamental form](@entry_id:161454) vanishes identically [@problem_id:3005525].

### The Shape Operator and the Weingarten Formula

A dual perspective on extrinsic curvature is obtained by examining how the [normal spaces](@entry_id:154073) themselves vary as we move along the submanifold. For a vector field $X$ tangent to $N$ and a [normal vector field](@entry_id:268853) $\xi$ along $N$, the ambient derivative $\bar{\nabla}_X \xi$ can likewise be decomposed into its tangential and normal parts. This decomposition gives rise to the **Weingarten formula**:
$$
\bar{\nabla}_X \xi = -A_\xi X + \nabla^\perp_X \xi
$$
Here, $A_\xi X = -(\bar{\nabla}_X \xi)^\top$ defines the **shape operator** (or **Weingarten map**) $A_\xi$, which is an endomorphism of the tangent bundle $TN$. The term $\nabla^\perp_X \xi = (\bar{\nabla}_X \xi)^\perp$ defines the **normal connection**, a connection on the [normal bundle](@entry_id:272447) $\nu$.

The shape operator $A_\xi$ measures the tangential component of the rate of change of the normal field $\xi$ in the direction of $X$. It describes how the tangent space of $N$ must "bend" to accommodate the change in the normal direction.

The second fundamental form and the [shape operator](@entry_id:264703) are not independent but are linked by a crucial identity. Since $\bar{g}$ is parallel with respect to $\bar{\nabla}$, for $X,Y \in \Gamma(TN)$ and $\xi \in \Gamma(\nu)$, we have:
$$
0 = X(\bar{g}(Y, \xi)) = \bar{g}(\bar{\nabla}_X Y, \xi) + \bar{g}(Y, \bar{\nabla}_X \xi)
$$
Substituting the Gauss and Weingarten formulas, and using the orthogonality of tangential and normal vectors, this simplifies to:
$$
\bar{g}(B(X,Y), \xi) = \bar{g}(Y, A_\xi X) = g(A_\xi X, Y)
$$
This fundamental relationship shows that $A_\xi$ is a self-adjoint endomorphism of $(T_p N, g_p)$ for each $p \in N$ and each $\xi \in \nu_p$. It establishes the shape operator as the algebraic dual to the [second fundamental form](@entry_id:161454) [@problem_id:3005512].

### Ideal Submanifolds: Totally Geodesic and Totally Umbilic

Submanifolds are classified based on the structure of their second fundamental form. The two simplest and most important classes are those where $B$ is either identically zero or is as "isotropic" as possible.

#### Totally Geodesic Submanifolds

A submanifold $(N,g)$ is **[totally geodesic](@entry_id:183906)** in $(M, \bar{g})$ if its second fundamental form vanishes identically, $B \equiv 0$. This condition has several profound and equivalent characterizations:

1.  $B(X,Y) = 0$ for all $X,Y \in \Gamma(TN)$.
2.  The [shape operator](@entry_id:264703) $A_\xi = 0$ for all normal vector fields $\xi$. This follows directly from the duality $g(A_\xi X, Y) = \bar{g}(B(X,Y), \xi)$ [@problem_id:3005525].
3.  Any geodesic of $N$ (with respect to $\nabla$) is also a geodesic of $M$ (with respect to $\bar{\nabla}$). This is because for a geodesic $\gamma(t)$ in $N$, its acceleration in $N$ is $\nabla_{\gamma'} \gamma' = 0$. Its acceleration in $M$ is $\bar{\nabla}_{\gamma'} \gamma' = \nabla_{\gamma'} \gamma' + B(\gamma', \gamma')$. This vanishes if and only if $B(\gamma', \gamma')=0$. If this holds for all geodesics, it implies $B \equiv 0$.

Totally geodesic [submanifolds](@entry_id:159439) are, in a sense, the "flattest" possible [embeddings](@entry_id:158103). They inherit their geometry directly from the ambient space. Classic examples include lines and affine subspaces in Euclidean space, and great spheres within a larger sphere.

#### Totally Umbilic Submanifolds

A more general and equally important class of submanifolds consists of those where the second fundamental form is as isotropic as possible at each point. This means that $B(X,Y)$ should only depend on the metric pairing $g(X,Y)$, not on the specific directions of $X$ and $Y$. This leads to the definition of a **totally umbilic** [submanifold](@entry_id:262388), for which there exists a [normal vector field](@entry_id:268853) $H_{umb}$ such that for all $X,Y \in \Gamma(TN)$:
$$
B(X,Y) = g(X,Y) H_{umb}
$$
This special [normal vector field](@entry_id:268853) $H_{umb}$ is known as the **[mean curvature vector](@entry_id:199617)**, a name justified by taking the trace of the second fundamental form. Let $\{e_i\}_{i=1}^m$ be a local [orthonormal basis](@entry_id:147779) for $TN$. The trace is
$$
\mathrm{tr}_g B = \sum_{i=1}^m B(e_i, e_i) = \sum_{i=1}^m g(e_i, e_i) H_{umb} = \sum_{i=1}^m H_{umb} = m H_{umb}
$$
Thus, the vector $H_{umb}$ is indeed the [mean curvature vector](@entry_id:199617), often defined as $H = \frac{1}{m}\mathrm{tr}_g B$ [@problem_id:3005506] [@problem_id:3005513]. A submanifold is totally umbilic if and only if its [second fundamental form](@entry_id:161454) is given by $B(X,Y) = g(X,Y) H$.

The totally umbilic condition has an elegant equivalent formulation in terms of shape operators. Using the duality relation:
$$
g(A_\xi X, Y) = \bar{g}(B(X,Y), \xi) = \bar{g}(g(X,Y)H, \xi) = g(X,Y)\bar{g}(H, \xi)
$$
This implies that for any normal field $\xi$, the [shape operator](@entry_id:264703) is a scalar multiple of the identity map:
$$
A_\xi = \bar{g}(H, \xi) \mathrm{Id}_{TN}
$$
This property is particularly simple in the case of a **hypersurface** ([codimension](@entry_id:273141) one), where the [normal bundle](@entry_id:272447) is spanned by a single unit normal field $\nu$. In this case, any normal vector is proportional to $\nu$, and the [mean curvature vector](@entry_id:199617) is $H = \lambda \nu$ for some function $\lambda$. The shape operator $A := A_\nu$ is simply $A = \lambda \mathrm{Id}_{TN}$, meaning all [principal curvatures](@entry_id:270598) are equal to $\lambda$ [@problem_id:3005506].

The relationship between these two classes is clear: a [submanifold](@entry_id:262388) is [totally geodesic](@entry_id:183906) if and only if it is totally umbilic with a vanishing [mean curvature vector](@entry_id:199617) ($H \equiv 0$) [@problem_id:3005506] [@problem_id:3005513]. The archetypal example of a [totally umbilic submanifold](@entry_id:192464) that is not [totally geodesic](@entry_id:183906) is a sphere $S^{n-1}(r)$ in Euclidean space $\mathbb{R}^n$.

A more intricate example is provided by the geometry of warped products [@problem_id:3005508]. Consider the manifold $M = \mathbb{R} \times_f S^n$ with metric $\bar{g} = dt^2 + f(t)^2 g_{S^n}$, where $f(t) = \exp(kt)$ for some constant $k \neq 0$. A fiber $N = \{t_0\} \times S^n$ is a hypersurface with unit normal field $\partial_t$. A direct computation using the Koszul formula shows its second fundamental form is $B(X,Y) = -k \, g(X,Y) \partial_t$, where $g$ is the [induced metric](@entry_id:160616) on the fiber. This is a perfect instance of the totally umbilic condition, with [mean curvature vector](@entry_id:199617) $H = -k \partial_t$. The [submanifold](@entry_id:262388) is totally umbilic but not [totally geodesic](@entry_id:183906). The squared norm of its [second fundamental form](@entry_id:161454), $|B|^2 = \sum_{i,j=1}^n \bar{g}(B(e_i,e_j), B(e_i,e_j))$, is a constant value $nk^2$.

### The Fundamental Equations of Submanifold Theory

The interplay between [intrinsic curvature](@entry_id:161701) (of $N$), [extrinsic curvature](@entry_id:160405) (of $N$ in $M$), and ambient curvature (of $M$) is governed by a set of three fundamental equations named after Gauss, Codazzi, and Ricci.

#### The Gauss Equation

The **Gauss equation** relates the Riemann [curvature tensor](@entry_id:181383) $R$ of the submanifold to the ambient curvature tensor $\bar{R}$ and the second fundamental form. For a hypersurface with [shape operator](@entry_id:264703) $S$, it takes the form:
$$
\bar{g}(R(X,Y)Z, W) = \bar{g}(\bar{R}(X,Y)Z, W) + g(SY, Z)g(SX, W) - g(SX, Z)g(SY, W)
$$
This equation provides a powerful way to compute the [intrinsic curvature](@entry_id:161701) of a submanifold. For instance, consider a totally umbilic hypersurface $M^m$ in a [space form](@entry_id:203017) $\overline{M}^{m+1}$ of [constant sectional curvature](@entry_id:272200) $\kappa$. The umbilic condition $S=\lambda \mathrm{Id}$ and the structure of $\bar{R}$ simplify the Gauss equation dramatically, yielding that the [sectional curvature](@entry_id:159738) $K_M$ of $M$ is constant and given by:
$$
K_M = \kappa + \lambda^2 = \kappa + |H|^2
$$
Here $|H|$ is the magnitude of the [mean curvature vector](@entry_id:199617). This beautiful result [@problem_id:3005504] shows that such a [submanifold](@entry_id:262388) is itself a space of [constant curvature](@entry_id:162122), with its curvature being a sum of the ambient curvature and the squared [extrinsic curvature](@entry_id:160405).

#### The Ricci Equation

While the Gauss equation concerns the tangent bundle, the **Ricci equation** describes the curvature of the [normal bundle](@entry_id:272447). The [curvature tensor](@entry_id:181383) $R^\perp$ of the normal connection $\nabla^\perp$ is related to the ambient curvature and the commutator of the shape operators:
$$
\langle R^\perp(X,Y)\xi, \eta \rangle = \langle \bar{R}(X,Y)\xi, \eta \rangle + g( [A_\xi, A_\eta]X, Y )
$$
where $[A_\xi, A_\eta] = A_\xi A_\eta - A_\eta A_\xi$ is the commutator [@problem_id:3005517]. This equation reveals that the [normal curvature](@entry_id:270966) has two sources: the restriction of the ambient curvature to the [normal bundle](@entry_id:272447), and the non-commutativity of the shape operators.

For a [totally umbilic submanifold](@entry_id:192464), we have seen that $A_\xi = \langle H, \xi \rangle \mathrm{Id}$, which implies that all shape operators are scalar multiples of the identity. They therefore commute: $[A_\xi, A_\eta]=0$ for all $\xi, \eta$. In this case, the Ricci equation simplifies to:
$$
\langle R^\perp(X,Y)\xi, \eta \rangle = \langle \bar{R}(X,Y)\xi, \eta \rangle
$$
This means the [normal curvature](@entry_id:270966) of a [totally umbilic submanifold](@entry_id:192464) is completely determined by the ambient curvature. A significant consequence is that if the [ambient space](@entry_id:184743) is flat ($\bar{R} \equiv 0$), such as Euclidean space, then the normal connection of any [totally umbilic submanifold](@entry_id:192464) must also be flat ($R^\perp \equiv 0$) [@problem_id:3005517].

### Advanced Examples and Constraints

The concepts of [totally geodesic](@entry_id:183906) and totally [umbilic submanifolds](@entry_id:637677) find application and exhibit rich behavior in more structured settings.

#### Rigidity in Product Manifolds

The totally umbilic condition is highly restrictive, a fact starkly illustrated by considering product [submanifolds](@entry_id:159439) [@problem_id:3005529]. Let $N_1 \subset M_1$ and $N_2 \subset M_2$ be submanifolds. For their product $N_1 \times N_2$ to be totally umbilic in the product manifold $M_1 \times M_2$, a careful analysis of the second fundamental form shows that this is only possible under very specific circumstances. If neither $N_1$ nor $N_2$ is a single point (i.e., $\dim N_1 > 0$ and $\dim N_2 > 0$), then $N_1 \times N_2$ is totally umbilic if and only if both $N_1$ and $N_2$ are [totally geodesic](@entry_id:183906). In essence, any "bending" (non-zero [second fundamental form](@entry_id:161454)) in one factor is incompatible with the uniform [isotropy](@entry_id:159159) demanded by the umbilic condition across the product structure. The only exception is the degenerate case where one factor, say $N_2$, is a point; then $N_1 \times \{p_2\}$ is totally umbilic in $M_1 \times M_2$ if and only if $N_1$ is totally umbilic in $M_1$.

#### Constraints in Kähler Geometry

The presence of additional geometric structure, such as a complex structure, can impose even stronger constraints. Let $(\tilde{M}, \tilde{g}, J)$ be a Kähler manifold, meaning $\tilde{\nabla}J=0$. Let $N \subset \tilde{M}$ be a **complex submanifold**, i.e., $J(T_p N) = T_p N$ for all $p \in N$.

The condition $\tilde{\nabla}J = 0$ forces the [second fundamental form](@entry_id:161454) $B$ of $N$ to satisfy two remarkable identities:
1.  $B(X, JY) = J(B(X,Y))$
2.  $B(JX, JY) = -B(X,Y)$

From the second identity, one can prove a foundational theorem in Kähler geometry: **every complex [submanifold](@entry_id:262388) of a Kähler manifold is a [minimal submanifold](@entry_id:200568)** ($H \equiv 0$). The proof involves taking the trace of $B$ over a special [orthonormal basis](@entry_id:147779) adapted to the [complex structure](@entry_id:269128), where the terms cancel out in pairs [@problem_id:3005523].

This theorem has a powerful corollary: **A complex [submanifold](@entry_id:262388) of a Kähler manifold is totally umbilic if and only if it is [totally geodesic](@entry_id:183906).** This is because if it is totally umbilic, its second fundamental form must be $B(X,Y) = g(X,Y)H$. Since $H$ must be zero, it follows that $B \equiv 0$. This stands in stark contrast to the real setting, where spheres provide a rich family of non-geodesic, totally [umbilic submanifolds](@entry_id:637677). In the complex world, such objects are forbidden. This rigidity implies that for any complex submanifold, the intrinsic [holomorphic sectional curvature](@entry_id:634709) is directly inherited from the [ambient space](@entry_id:184743) if and only if the [submanifold](@entry_id:262388) is [totally geodesic](@entry_id:183906) [@problem_id:3005523].