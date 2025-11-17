## Introduction
In the landscape of differential geometry, the concept of a submanifold is of paramount importance, providing a framework for studying geometric objects that reside within larger, ambient spaces. From the elegant curve of a [soap film](@entry_id:267628) to the trajectory of a satellite in curved spacetime, submanifolds offer a precise mathematical language to describe a vast array of physical and abstract structures. The central challenge this article addresses is understanding and quantifying the intricate relationship between a submanifold's own intrinsic geometry and the extrinsic way it is embedded in its surroundings.

This article is structured to guide you from foundational theory to practical application. In the first chapter, **Principles and Mechanisms**, we will construct the essential machinery of [submanifold theory](@entry_id:190701), starting with rigorous definitions via immersions and the Regular Value Theorem, and developing key analytical tools like the fundamental forms and the [shape operator](@entry_id:264703). Building on this, the second chapter, **Applications and Interdisciplinary Connections**, will showcase the profound impact of these ideas, demonstrating how they provide critical insights into classical geometry, minimal surfaces, general relativity, and modern control theory. Finally, the **Hands-On Practices** section will allow you to solidify your understanding by actively engaging with and solving concrete problems, bridging the gap between abstract concepts and computational mastery.

## Principles and Mechanisms

Having introduced the foundational concept of a smooth manifold, we now turn our attention to one of the most fruitful areas of [differential geometry](@entry_id:145818): the study of submanifolds. A submanifold is, informally, a manifold that resides inside a larger ambient manifold. The central theme of this chapter is to understand how the geometry of the [ambient space](@entry_id:184743) constrains and defines the geometry of the [submanifold](@entry_id:262388). We will develop the essential machinery—the fundamental forms and [structural equations](@entry_id:274644)—that allows us to precisely quantify this relationship, bridging the gap between the submanifold's intrinsic properties and its extrinsic embedding.

### Defining Submanifolds: Parametric and Implicit Approaches

There are two primary, complementary methods for constructing and defining submanifolds. The first is a parametric approach, which views a [submanifold](@entry_id:262388) as the image of a sufficiently "nice" map from a model manifold. The second is an implicit approach, which characterizes a [submanifold](@entry_id:262388) as the solution set to a system of equations, known as a [level set](@entry_id:637056).

#### Immersions and Embeddings

The parametric approach begins with the notion of an **immersion**. A [smooth map](@entry_id:160364) $f: M \to N$ between smooth manifolds is called an **immersion** if its differential, $df_p: T_pM \to T_{f(p)}N$, is an injective linear map for every point $p \in M$. This condition ensures that, on an infinitesimal level, the map $f$ does not collapse tangent vectors. The Rank-Nullity Theorem implies that for an immersion to exist, we must have $\dim(M) \le \dim(N)$. The image $f(M)$ of an immersion, equipped with the [smooth structure](@entry_id:159394) inherited from $M$ that makes $f: M \to f(M)$ a diffeomorphism, is called an **[immersed submanifold](@entry_id:264923)**.

An immersion guarantees that the map is locally an embedding, but it does not preclude global self-intersections or other [topological pathologies](@entry_id:158838). A stronger, and more geometrically well-behaved, notion is that of an **embedding**. An immersion $f: M \to N$ is an **embedding** if it is also a [homeomorphism](@entry_id:146933) onto its image $f(M)$, where the image is endowed with the subspace topology inherited from the ambient manifold $N$. An **[embedded submanifold](@entry_id:273162)** is the image of an embedding.

The crucial distinction between an immersed and an [embedded submanifold](@entry_id:273162) is topological. For an embedding, the topology on the [submanifold](@entry_id:262388) induced via the map $f$ coincides with the topology it inherits as a subspace of $N$. This is not necessarily true for an immersion. An immersion can fail to be an embedding in two primary ways: it might not be injective (leading to self-intersections), or it might be injective but fail to be a homeomorphism onto its image (e.g., if the image of an open set in $M$ is not open in the subspace topology of $f(M)$).

A classic illustration of this distinction is provided by comparing a simple [paraboloid](@entry_id:264713) with a [figure-eight curve](@entry_id:167790) in $\mathbb{R}^3$ [@problem_id:2980336].
-   Consider the surface $S$ in $\mathbb{R}^3$ given as the graph of the function $z = x^2 + y^2$. It can be parameterized by the map $F: \mathbb{R}^2 \to \mathbb{R}^3$ defined by $F(x,y) = (x, y, x^2+y^2)$. The differential of this map has rank 2 everywhere, so $F$ is an immersion. Furthermore, $F$ is an [injective map](@entry_id:262763), and its inverse, the projection $(x,y,z) \mapsto (x,y)$, is continuous. Thus, $F$ is a [homeomorphism](@entry_id:146933) onto its image. Consequently, the paraboloid $S$ is an [embedded submanifold](@entry_id:273162) of $\mathbb{R}^3$.

-   In contrast, consider the curve in $\mathbb{R}^3$ parameterized by $\gamma: S^1 \to \mathbb{R}^3$ given by $\gamma(t) = (\sin(t), \sin(2t), 0)$. The velocity vector $\gamma'(t) = (\cos(t), 2\cos(2t), 0)$ is never zero, so $\gamma$ is an immersion. However, the map is not injective; for instance, $\gamma(0) = \gamma(\pi) = (0,0,0)$. This self-intersection at the origin means $\gamma$ cannot be a homeomorphism onto its image. The resulting [figure-eight curve](@entry_id:167790) is therefore an immersed, but not embedded, [submanifold](@entry_id:262388) of $\mathbb{R}^3$.

#### The Regular Value Theorem

The implicit approach provides a powerful method for identifying submanifolds without constructing an explicit parameterization. It relies on the concept of [regular values](@entry_id:161151). Let $f: M^m \to N^n$ be a [smooth map](@entry_id:160364) between manifolds of dimensions $m$ and $n$.

A point $p \in M$ is a **regular point** of $f$ if the differential $df_p: T_pM \to T_{f(p)}N$ is surjective. A point that is not regular is called a **critical point**. A point $q \in N$ is a **[regular value](@entry_id:188218)** if its entire preimage $f^{-1}(q) = \{p \in M \mid f(p)=q\}$ consists only of regular points. If the preimage is empty, $q$ is also considered a [regular value](@entry_id:188218). Any point in the image of $f$ that is not a [regular value](@entry_id:188218) is a **critical value**.

The fundamental result connecting these ideas is the **Regular Value Theorem** (also known as the Preimage Theorem), a direct consequence of the Implicit Function Theorem [@problem_id:2980347].

**Theorem (Regular Value Theorem):** Let $f: M^m \to N^n$ be a [smooth map](@entry_id:160364). If $q \in N$ is a [regular value](@entry_id:188218) of $f$, then the [level set](@entry_id:637056) $f^{-1}(q)$ is a properly [embedded submanifold](@entry_id:273162) of $M$ of dimension $m-n$. Furthermore, the tangent space to this [submanifold](@entry_id:262388) at any point $p \in f^{-1}(q)$ is given by the kernel of the differential: $T_p(f^{-1}(q)) = \ker(df_p)$.

This theorem is immensely practical. To show that a subset $S \subset M$ is an [embedded submanifold](@entry_id:273162), one need only find a [smooth function](@entry_id:158037) $f: M \to N$ for which $S$ is the level set of a [regular value](@entry_id:188218).

Let's consider some examples in $\mathbb{R}^3$ where $M = \mathbb{R}^3$ and $N = \mathbb{R}$ [@problem_id:1662503].
-   **Hyperboloid of One Sheet:** Let $S_A$ be the set defined by $x^2 + y^2 - z^2 = 1$. This is the level set $F^{-1}(0)$ for the function $F(x,y,z) = x^2 + y^2 - z^2 - 1$. The differential of $F$ is represented by its gradient, $\nabla F = (2x, 2y, -2z)$. This gradient is zero only at the origin $(0,0,0)$. However, the origin does not lie on the surface $S_A$, since $0^2+0^2-0^2 = 0 \neq 1$. Therefore, every point in the preimage $F^{-1}(0)$ is a regular point. This means $0$ is a [regular value](@entry_id:188218) of $F$, and by the Regular Value Theorem, the [hyperboloid](@entry_id:170736) $S_A$ is a smooth [embedded submanifold](@entry_id:273162) of $\mathbb{R}^3$ of dimension $3-1 = 2$.

-   **Cone:** Let $S_B$ be the set defined by $x^2 + y^2 - z^2 = 0$. This is the [level set](@entry_id:637056) $F^{-1}(0)$ for $F(x,y,z) = x^2 + y^2 - z^2$. The gradient is again $\nabla F = (2x, 2y, -2z)$, which is zero at the origin $(0,0,0)$. The origin satisfies the equation $0^2+0^2-0^2=0$, so it lies on the surface $S_B$. Thus, the origin is a critical point within the [level set](@entry_id:637056), making $0$ a critical value. The theorem does not apply, and indeed, the cone is not a [smooth manifold](@entry_id:156564) due to the singularity at its apex.

-   **Disjoint Union of Spheres:** Let $S_C$ be the set defined by $(x^2+y^2+z^2-5)(x^2+y^2+z^2-10)=0$. This is the union of a sphere of radius $\sqrt{5}$ and a sphere of radius $\sqrt{10}$. Let $F(x,y,z) = (x^2+y^2+z^2-5)(x^2+y^2+z^2-10)$. One can compute its gradient and show that it never vanishes on the set $F=0$. Thus, $0$ is a [regular value](@entry_id:188218), and $S_C$ is a smooth 2-dimensional [submanifold](@entry_id:262388), consisting of two [connected components](@entry_id:141881).

### The Fundamental Forms: Probing Extrinsic Geometry

Once a [submanifold](@entry_id:262388) is defined, we can investigate its geometry. When a Riemannian metric $\bar{g}$ is present on the ambient manifold $\bar{M}$, it naturally induces a geometric structure on any submanifold $M \subset \bar{M}$. The study of this induced structure is the domain of [extrinsic geometry](@entry_id:262461).

#### The Induced Metric (First Fundamental Form)

An immersion $f: M \to \bar{M}$ allows us to pull back the metric $\bar{g}$ from the ambient space to define a metric $g$ on $M$. This **[induced metric](@entry_id:160616)**, also known as the **[first fundamental form](@entry_id:274022)**, is defined by:
$$
g_p(X, Y) = \bar{g}_{f(p)}(df_p(X), df_p(Y))
$$
for any [tangent vectors](@entry_id:265494) $X, Y \in T_pM$. If $f$ is an immersion, the injectivity of $df_p$ ensures that $g$ is non-degenerate, making $(M,g)$ a Riemannian manifold in its own right. An immersion that preserves the metric in this way, i.e., $g$ is the given metric on $M$, is called an **[isometric immersion](@entry_id:272242)**.

In [local coordinates](@entry_id:181200) $(u^1, \dots, u^m)$ on $M$, a [parameterization](@entry_id:265163) is given by $F(u^1, \dots, u^m)$. The [tangent vectors](@entry_id:265494) $\partial_i = \frac{\partial F}{\partial u^i}$ form a basis for the tangent space. The components of the [induced metric](@entry_id:160616) tensor are then computed by taking inner products of these basis vectors in the ambient space:
$$
g_{ij} = \bar{g}(\partial_i, \partial_j)
$$
For instance, consider a [2-torus](@entry_id:265991) embedded in $\mathbb{R}^4$ with the standard Euclidean metric, parameterized by $F(\theta, \phi)$ [@problem_id:1029256]. The tangent vectors are $\partial_\theta F$ and $\partial_\phi F$. The components of the [induced metric](@entry_id:160616) are $g_{\theta\theta} = \langle \partial_\theta F, \partial_\theta F \rangle$, $g_{\phi\phi} = \langle \partial_\phi F, \partial_\phi F \rangle$, and $g_{\theta\phi} = \langle \partial_\theta F, \partial_\phi F \rangle$. These components capture the complete intrinsic geometry of the torus at the level of lengths and angles.

#### Decomposing Covariant Derivatives: The Gauss and Weingarten Formulas

The key to relating the [intrinsic geometry](@entry_id:158788) of a submanifold to its extrinsic embedding lies in decomposing the ambient [covariant derivative](@entry_id:152476). Let $(M,g)$ be a submanifold of a Riemannian manifold $(\bar{M}, \bar{g})$. For each point $p \in M$, the tangent space of the ambient manifold splits into an orthogonal [direct sum](@entry_id:156782):
$$
T_p\bar{M} = T_pM \oplus (T_pM)^\perp
$$
The space $(T_pM)^\perp$ is the **normal space** at $p$, and the collection of all [normal spaces](@entry_id:154073) forms the **[normal bundle](@entry_id:272447)**, denoted $\nu(M)$ or $T^\perp M$.

Now, let $X$ and $Y$ be vector fields tangent to $M$. We can extend them to vector fields on an [open neighborhood](@entry_id:268496) in $\bar{M}$ and compute the ambient [covariant derivative](@entry_id:152476) $\bar{\nabla}_X Y$. The resulting vector field, evaluated at points on $M$, will not generally be tangent to $M$. We can decompose it into its tangential and normal components [@problem_id:3005525]:
$$
\bar{\nabla}_X Y = (\bar{\nabla}_X Y)^\top + (\bar{\nabla}_X Y)^\perp
$$
This decomposition defines two fundamental objects. The tangential part defines a [torsion-free connection](@entry_id:181337) on $M$, which can be shown to be its unique Levi-Civita connection $\nabla$. The normal part defines a symmetric, [bilinear map](@entry_id:150924) called the **[second fundamental form](@entry_id:161454)**, $B: TM \times TM \to T^\perp M$. This leads to the **Gauss formula**:
$$
\bar{\nabla}_X Y = \nabla_X Y + B(X,Y)
$$
The [second fundamental form](@entry_id:161454) $B(X,Y)$ measures the failure of the submanifold to be "flat" within the [ambient space](@entry_id:184743). If $B \equiv 0$, the [submanifold](@entry_id:262388) is called **[totally geodesic](@entry_id:183906)**. In a [totally geodesic submanifold](@entry_id:191437), the ambient derivative of tangent fields remains tangent. This implies that any geodesic of the [submanifold](@entry_id:262388) is also a geodesic of the ambient manifold. The property that $TM$ is an **autoparallel** distribution (i.e., $\bar{\nabla}_X Y$ is tangent to $M$ for all $X,Y$ tangent to $M$) is precisely the condition that $M$ is [totally geodesic](@entry_id:183906) [@problem_id:3005525].

Similarly, we can analyze the derivative of a [normal vector field](@entry_id:268853) $\xi \in \Gamma(T^\perp M)$ in a tangent direction $X$. The vector field $\bar{\nabla}_X \xi$ also splits into tangential and normal components. This decomposition is described by the **Weingarten formula**:
$$
\bar{\nabla}_X \xi = -A_\xi X + \nabla^\perp_X \xi
$$
Here, $A_\xi X = -(\bar{\nabla}_X \xi)^\top$ is the tangential part, defining the **[shape operator](@entry_id:264703)** (or Weingarten map) $A_\xi: TM \to TM$ associated with the [normal vector](@entry_id:264185) $\xi$. The normal part, $\nabla^\perp_X \xi = (\bar{\nabla}_X \xi)^\perp$, defines the **normal connection** $\nabla^\perp$ on the [normal bundle](@entry_id:272447).

#### The Second Fundamental Form and the Shape Operator

The second fundamental form and the [shape operator](@entry_id:264703) are intimately related. By using the property that $\bar{\nabla}$ is compatible with the metric $\bar{g}$, one can derive the following fundamental identity:
$$
\bar{g}(B(X,Y), \xi) = g(A_\xi X, Y)
$$
Since $B(X,Y)$ is symmetric in $X$ and $Y$, this identity implies that each [shape operator](@entry_id:264703) $A_\xi$ is a self-adjoint (symmetric) endomorphism of the [tangent space](@entry_id:141028): $g(A_\xi X, Y) = g(X, A_\xi Y)$. The eigenvalues of the [shape operator](@entry_id:264703) are called the **principal curvatures**, and its eigenvectors are the **principal directions**.

For a hypersurface (a submanifold of [codimension](@entry_id:273141) 1), there are only two choices for a unit [normal vector field](@entry_id:268853), $\nu$ and $-\nu$. The shape operator is typically defined with respect to one of these, say $S \equiv A_\nu$. Its determinant, $\det(S)$, is the **Gaussian curvature**, and its normalized trace, $\frac{1}{m}\mathrm{tr}(S)$, is the **mean curvature**.

As a concrete example, consider a surface in $\mathbb{R}^3$ given as the [graph of a function](@entry_id:159270) $z = f(x,y)$ [@problem_id:1029260]. With respect to the basis $\{\partial_x, \partial_y\}$ for the [tangent space](@entry_id:141028), the matrices of the first fundamental form ($I$) and second fundamental form ($II$) can be calculated. The matrix of the shape operator is then $S = I^{-1}II$. At a point where the [tangent plane](@entry_id:136914) is horizontal (e.g., if $f_x=f_y=0$), the [first fundamental form](@entry_id:274022) is the identity matrix, and the matrix of the shape operator is simply the Hessian matrix of $f$ (up to a normalization factor). For the surface $f(x, y) = a \exp(b x^2 + c y^2) + d xy$, at the origin $(0,0)$, we have $f_x(0,0)=f_y(0,0)=0$. The [shape operator](@entry_id:264703) matrix becomes $$S = \begin{pmatrix} 2ab & d \\ d & 2ac \end{pmatrix}$$, and the Gaussian curvature is $K = \det(S) = 4a^2bc - d^2$.

#### Extrinsic Curvature Invariants: Mean Curvature

While the shape operator $A_\xi$ depends on a choice of [normal vector](@entry_id:264185) $\xi$, we can construct invariants that are intrinsic to the immersion. The most important of these is the **[mean curvature vector](@entry_id:199617)**. For an immersion $f:M^m \to \bar{M}$, the [mean curvature vector](@entry_id:199617) $H$ is the normalized trace of the [second fundamental form](@entry_id:161454) with respect to the metric $g$:
$$
H = \frac{1}{m} \mathrm{tr}_g(B) = \frac{1}{m} \sum_{i=1}^m B(e_i, e_i)
$$
where $\{e_i\}_{i=1}^m$ is any local [orthonormal frame](@entry_id:189702) for $TM$ [@problem_id:2984391].

This definition has two crucial properties. First, $H$ is a [normal vector field](@entry_id:268853) because each $B(e_i, e_i)$ is a normal vector by definition, and the [normal bundle](@entry_id:272447) is closed under linear combinations. Second, the definition of $H$ is independent of the choice of [orthonormal frame](@entry_id:189702). A change of [orthonormal frame](@entry_id:189702) corresponds to an [orthogonal transformation](@entry_id:155650), and the trace of a [bilinear form](@entry_id:140194) is invariant under such transformations. Thus, the [mean curvature vector](@entry_id:199617) is a well-defined geometric invariant of the immersion.

A [submanifold](@entry_id:262388) is called **minimal** if its [mean curvature vector](@entry_id:199617) vanishes identically, $H \equiv 0$. Minimal surfaces are, in a sense, the "tightest" possible immersions of a manifold, locally minimizing surface area. A generalization of [totally geodesic submanifolds](@entry_id:637049) is the class of **totally umbilic** submanifolds. A submanifold is totally umbilic if its [second fundamental form](@entry_id:161454) is proportional to the metric tensor at every point, i.e., $B(X,Y) = g(X,Y)H$ for all [tangent vectors](@entry_id:265494) $X,Y$, where $H$ is the [mean curvature vector](@entry_id:199617) [@problem_id:3005525]. This is equivalent to the condition that for any [normal vector](@entry_id:264185) $\xi$, the shape operator $A_\xi$ is a multiple of the identity map: $A_\xi = \lambda_\xi \mathrm{Id}$. The standard sphere in Euclidean space is a paradigmatic example of a [totally umbilic submanifold](@entry_id:192464).

### The Fundamental Equations of Immersion Theory

The machinery of the Gauss and Weingarten formulas leads to a set of profound [structural equations](@entry_id:274644) that link the curvature of the ambient manifold, the [intrinsic curvature](@entry_id:161701) of the [submanifold](@entry_id:262388), and its extrinsic curvature as measured by the [second fundamental form](@entry_id:161454). These are known as the Gauss, Codazzi, and Ricci equations.

#### The Gauss Equation: From Extrinsic Bending to Intrinsic Curvature

The Gauss equation relates the Riemann [curvature tensor](@entry_id:181383) $R$ of the submanifold to the ambient [curvature tensor](@entry_id:181383) $\bar{R}$ and the second fundamental form. For tangent vectors $X, Y, Z, W \in TM$, it reads:
$$
\bar{g}(\bar{R}(X,Y)Z, W) = g(R(X,Y)Z, W) + \bar{g}(B(X,Z), B(Y,W)) - \bar{g}(B(X,W), B(Y,Z))
$$
This remarkable equation shows that the intrinsic curvature $R$ of the [submanifold](@entry_id:262388) is not independent but is determined by the ambient curvature and the way the submanifold is embedded (via $B$). In the special case where the ambient manifold is Euclidean space ($\bar{R} \equiv 0$), the equation simplifies and is often called the *Theorema Egregium* of Gauss. It reveals that the intrinsic curvature is determined entirely by the second fundamental form.

A spectacular application of the Gauss equation is the calculation of the curvature of the unit $n$-sphere $S^n$ embedded in $\mathbb{R}^{n+1}$ [@problem_id:2980342]. For $S^n \subset \mathbb{R}^{n+1}$, the outward unit normal is $\nu(p) = p$. The [shape operator](@entry_id:264703) is found to be $S(X) = -X$, i.e., $S = -\mathrm{Id}$. The second fundamental form is thus $II(X,Y) = g(S(X), Y) = -g(X,Y)$. Inserting this into the Gauss equation for a hypersurface in Euclidean space, $g(R(X,Y)Y,X) = II(X,X)II(Y,Y) - II(X,Y)^2$, for an orthonormal pair $\{X,Y\}$, we get:
$$
K(\sigma) = g(R(X,Y)Y,X) = (-g(X,X))(-g(Y,Y)) - (-g(X,Y))^2 = (-1)(-1) - 0^2 = 1
$$
This demonstrates that the unit $n$-sphere is a space of [constant sectional curvature](@entry_id:272200) $K=+1$. From this, one can deduce that its [scalar curvature](@entry_id:157547) is $\mathrm{Scal} = n(n-1)$.

#### The Codazzi Equation: A Constraint on Extrinsic Geometry

While the Gauss equation constrains the tangential part of the ambient curvature, the Codazzi equation (or Codazzi-Mainardi equation) constrains its normal part. It relates the covariant derivative of the second fundamental form to the ambient curvature:
$$
(\bar{R}(X,Y)Z)^\perp = (\nabla_X B)(Y,Z) - (\nabla_Y B)(X,Z)
$$
where $(\nabla_X B)(Y,Z) = \nabla^\perp_X(B(Y,Z)) - B(\nabla_X Y, Z) - B(Y, \nabla_X Z)$ is the [covariant derivative](@entry_id:152476) of $B$. If the [ambient space](@entry_id:184743) is Euclidean ($\bar{R}=0$), the equation simplifies to $(\nabla_X B)(Y,Z) = (\nabla_Y B)(X,Z)$, indicating that the tensor $\nabla B$ is symmetric in its first two slots. This equation acts as a compatibility condition, restricting the possible extrinsic geometries a submanifold can possess. For [surfaces of revolution](@entry_id:178960) in $\mathbb{R}^3$, the Codazzi-Mainardi equations yield differential equations relating the principal curvatures. For the special case of Delaunay surfaces, which have [constant mean curvature](@entry_id:194008), these equations can be solved explicitly [@problem_id:1029128].

#### The Ricci Equation: Curvature of the Normal Bundle

For submanifolds with codimension greater than one, there is a third fundamental equation: the Ricci equation. It describes the curvature $R^\perp$ of the normal connection $\nabla^\perp$ in terms of the ambient curvature and the shape operators. For tangent fields $X, Y$ and normal fields $\xi, \eta$, the Ricci equation is:
$$
\bar{g}(R^\perp(X,Y)\xi, \eta) = \bar{g}(\bar{R}(X,Y)\xi, \eta) + g([A_\xi, A_\eta]X, Y)
$$
where $[A_\xi, A_\eta] = A_\xi A_\eta - A_\eta A_\xi$ is the commutator of the shape operators [@problem_id:2980323]. This equation shows that the curvature of the [normal bundle](@entry_id:272447) has two sources: the ambient curvature restricted to the [normal bundle](@entry_id:272447), and the [non-commutativity](@entry_id:153545) of the shape operators. If the shape operators for different normal directions commute, the normal connection's curvature is simply the restriction of the ambient curvature. The commutator term $[A_\xi, A_\eta]$ thus measures the "extrinsic twist" of the [normal bundle](@entry_id:272447), a phenomenon that has no analogue for [hypersurfaces](@entry_id:159491).

Together, the Gauss, Codazzi, and Ricci equations form the structural foundation of [submanifold theory](@entry_id:190701). They demonstrate that the geometry of a submanifold is a rich interplay between its intrinsic structure and the manner of its immersion into an [ambient space](@entry_id:184743).