## Introduction
When we observe a curved surface, like the exterior of a sphere, or a complex object, like a protein molecule modeled as a surface in 3D space, we are intuitively grappling with the geometry of a [submanifold](@entry_id:262388). These objects exist within a larger, often simpler, [ambient space](@entry_id:184743) (like Euclidean space), but they possess their own unique geometric character. How is this intrinsic geometry determined by its embedding in the larger world? This article addresses this fundamental question, revealing the elegant machinery that [differential geometry](@entry_id:145818) provides to dissect the relationship between a submanifold and its parent space. We will see that the geometry of the [ambient space](@entry_id:184743) can be systematically decomposed into components that live "within" the submanifold and components that describe how it "bends" in the outside world.

The **Principles and Mechanisms** section lays the theoretical groundwork. We will start by defining the [induced metric](@entry_id:160616) and then introduce the cornerstone concept: the [induced connection](@entry_id:635081). Through the Gauss formula, we will decompose the ambient space's derivative operator into its tangential and normal parts, giving rise to the intrinsic connection and the extrinsic second fundamental form. This will culminate in the Gauss-Codazzi-Ricci equations, a set of structural formulas that form the bedrock of [submanifold theory](@entry_id:190701).

Next, the **Applications and Interdisciplinary Connections** section will put this theory to work. We will see how it explains classical results for curves and surfaces, such as the relationship between a curve's [total curvature](@entry_id:157605) and its [geodesic curvature](@entry_id:158028) on a surface. We will then explore its profound impact on modern mathematics and physics, showing how it provides the language to study area-minimizing [minimal submanifolds](@entry_id:204492) and forges connections to fields like [geometric analysis](@entry_id:157700) and string theory.

Finally, the **Hands-On Practices** section will allow you to apply these concepts directly. Through a series of guided problems, you will compute the geometric quantities for concrete examples like planes, hyperbolic paraboloids, and plane curves, solidifying your understanding of how this powerful abstract framework translates into tangible geometric insights.

## Principles and Mechanisms

Having established the fundamental concept of a submanifold, we now embark on a deeper investigation into its geometry. When a manifold $S$ resides within a larger ambient Riemannian manifold $(M,g)$, how does the geometry of $M$ impart a geometric structure to $S$? This section will systematically answer this question. We will discover that the geometry of a submanifold is a rich interplay between its own intrinsic properties and its specific manner of embedding within the [ambient space](@entry_id:184743). Our journey will culminate in a set of fundamental equations that beautifully encapsulate this relationship.

### The Induced Metric and Geometric Decomposition

Our first task is to equip the [submanifold](@entry_id:262388) with a metric. Let $(M,g)$ be a Riemannian manifold and let $S \subset M$ be a smooth [embedded submanifold](@entry_id:273162). The inclusion map $i: S \hookrightarrow M$ is, by definition, a [smooth embedding](@entry_id:637480). This implies that at each point $p \in S$, the differential map, $di_p: T_pS \to T_pM$, is an injective linear map. This crucial property allows us to identify the tangent space $T_pS$ with its image, a linear subspace of $T_pM$. Geometrically, this means we can view tangent vectors to $S$ as specific tangent vectors to $M$ that happen to be "attached" to points on $S$ and point "along" $S$ [@problem_id:3051236].

With tangent spaces of $S$ living inside the tangent spaces of $M$, it is natural to define a metric on $S$ using the ambient metric $g$. The formal mechanism for this is the **pullback** of the tensor $g$ by the inclusion map $i$. The resulting metric on $S$, denoted $g^S$ or simply $g|_S$, is called the **induced Riemannian metric**. For any two [tangent vectors](@entry_id:265494) $X, Y \in T_pS$ at a point $p \in S$, the [induced metric](@entry_id:160616) is defined as:

$g^S_p(X,Y) := g_p(di_p(X), di_p(Y))$

Since we identify $X$ with its image $di_p(X)$, this is often written less formally as $g^S_p(X,Y) = g_p(X,Y)$. This definition naturally inherits [bilinearity](@entry_id:146819) and symmetry from the ambient metric $g$. But is it positive-definite, a requirement for any Riemannian metric? The answer is yes, and the reason lies in the [injectivity](@entry_id:147722) of the differential $di_p$. For any non-[zero vector](@entry_id:156189) $X \in T_pS$, its image $di_p(X)$ is also non-zero because $di_p$ is injective. Since $g$ is a genuine metric on $M$, its value on any non-[zero vector](@entry_id:156189) is positive. Therefore, $g^S_p(X,X) = g_p(di_p(X), di_p(X)) > 0$. This confirms that $(S, g^S)$ is itself a Riemannian manifold [@problem_id:3051233].

Once $(S, g^S)$ is a Riemannian manifold in its own right, we can employ the metric to understand the local geometry. At any point $p \in S$, the tangent space of the ambient manifold, $T_pM$, can be decomposed into two orthogonal subspaces. The first is the tangent space to the submanifold, $T_pS$. The second is its orthogonal complement, the **[normal space](@entry_id:154487)** $N_pS$:

$N_pS := \{ v \in T_pM \mid g_p(v,w) = 0 \text{ for all } w \in T_pS \}$

This gives the fundamental [orthogonal decomposition](@entry_id:148020) of the ambient [tangent space](@entry_id:141028) at every point of the [submanifold](@entry_id:262388):

$T_pM = T_pS \oplus N_pS$

This decomposition is central to everything that follows. It allows us to split any vector in $T_pM$ (for $p \in S$) into a component tangent to $S$ and a component normal (orthogonal) to $S$. We denote the corresponding orthogonal projection operators as $\pi^\top: T_pM \to T_pS$ and $\pi^\perp: T_pM \to N_pS$. The union of these spaces over all points in $S$ forms the [tangent bundle](@entry_id:161294) $TS$ and the **[normal bundle](@entry_id:272447)** $NS$ [@problem_id:3051227].

### The Gauss Formula and the Induced Connection

With a metric on $S$, the Fundamental Theorem of Riemannian Geometry guarantees the existence of a unique Levi-Civita connection on $S$, which we will denote $\nabla^S$. How does this intrinsic connection relate to the Levi-Civita connection $\nabla^M$ of the ambient space?

One might naively guess that to compute $\nabla^S_X Y$ for vector fields $X, Y$ tangent to $S$, we could simply compute $\nabla^M_X Y$. However, this presents two problems. First, the operator $\nabla^M$ is defined for [vector fields](@entry_id:161384) on $M$, but $X$ and $Y$ are initially only defined on the subset $S$. Second, even if we extend $X$ and $Y$ to fields $\tilde{X}, \tilde{Y}$ on a neighborhood in $M$, the resulting vector $(\nabla^M_{\tilde{X}}\tilde{Y})_p$ at a point $p \in S$ is an element of $T_pM$ and is not, in general, tangent to $S$ (i.e., not in $T_pS$). A classic example is a great circle on a sphere $S^2 \subset \mathbb{R}^3$. A [great circle](@entry_id:268970) is a geodesic of the sphere, so its [acceleration vector](@entry_id:175748) *within the sphere's geometry* should be zero. However, viewed as a curve in $\mathbb{R}^3$, it is a circle, and its [acceleration vector](@entry_id:175748) (the standard derivative) points towards the center of the sphere—a direction normal to the sphere's surface [@problem_id:3051236].

The correct approach resolves both issues elegantly. To handle the domain issue, we recognize that $\nabla^M$ is a differential operator, requiring its arguments to be defined in an open neighborhood of a point. Thus, for vector fields $X, Y$ on $S$, we must first choose arbitrary smooth extensions $\tilde{X}, \tilde{Y}$ to a neighborhood of $S$ in $M$ [@problem_id:3051260]. We then compute $\nabla^M_{\tilde{X}}\tilde{Y}$. The resulting vector field, when restricted to $S$, can be decomposed using our [orthogonal projection](@entry_id:144168). The tangential part of this vector is defined to be the [induced connection](@entry_id:635081):

$\nabla^S_X Y := \pi^\top \left( \left. \nabla^M_{\tilde{X}}\tilde{Y} \right|_S \right)$

This cornerstone result is known as the **Gauss formula** for the [induced connection](@entry_id:635081). A crucial feature of this definition is that it is independent of the choice of extensions $\tilde{X}$ and $\tilde{Y}$ [@problem_id:3051252]. This ensures that $\nabla^S$ is a well-defined operator on $S$.

This newly defined operator $\nabla^S$ can be shown to be both torsion-free and compatible with the [induced metric](@entry_id:160616) $g^S$. By the uniqueness stated in the Fundamental Theorem of Riemannian Geometry, $\nabla^S$ is therefore precisely the Levi-Civita connection of the submanifold $(S, g^S)$ [@problem_id:3051252]. The choice of orthogonal projection is not arbitrary; it is in fact the *only* choice of projection that guarantees the resulting connection will be compatible with the [induced metric](@entry_id:160616) [@problem_id:3051264].

### Extrinsic Geometry: The Second Fundamental Form and Shape Operator

The Gauss formula tells us what to do with the tangential part of the ambient derivative. But what about the normal part we projected away? This component is not to be discarded; it measures precisely how $S$ curves within $M$.

We define the **[second fundamental form](@entry_id:161454)** of $S$, denoted $B$ (or sometimes $\mathrm{II}$), as the normal component of the ambient derivative of two tangent vector fields:

$B(X,Y) := \pi^\perp \left( \left. \nabla^M_{\tilde{X}}\tilde{Y} \right|_S \right)$

With this definition, the Gauss formula can be written as a complete decomposition of the ambient derivative:

$\nabla^M_X Y = \nabla^S_X Y + B(X,Y)$

This equation elegantly splits the way tangent fields change into an intrinsic part (the change within $S$) and an extrinsic part (the bending of $S$ in $M$) [@problem_id:3051240]. The [second fundamental form](@entry_id:161454) $B$ is a tensor that takes two [tangent vectors](@entry_id:265494) and produces a [normal vector](@entry_id:264185). A key property, which follows from the torsion-free nature of $\nabla^M$, is that $B$ is symmetric in its two arguments: $B(X,Y) = B(Y,X)$ [@problem_id:3051274]. If the [second fundamental form](@entry_id:161454) is identically zero, $B \equiv 0$, the [submanifold](@entry_id:262388) is called **[totally geodesic](@entry_id:183906)**. In such a submanifold, the ambient derivative of tangent fields is always tangent, meaning geodesics of $S$ are also geodesics of $M$.

A complementary perspective on extrinsic curvature is provided by the **[shape operator](@entry_id:264703)**, or **Weingarten map**, $A$. For each normal vector $\xi \in N_pS$, we define a [linear operator](@entry_id:136520) $A_\xi: T_pS \to T_pS$. This operator describes the "shape" of the submanifold in the direction of $\xi$. It is defined by considering how the normal field $\xi$ changes as we move along a tangential direction $X$:

$A_\xi(X) := -\pi^\top(\nabla^M_X \xi)$

The minus sign is a convention, but it is standard. The [shape operator](@entry_id:264703) and the [second fundamental form](@entry_id:161454) are intimately related. This relationship is one of the most important in [submanifold theory](@entry_id:190701):

$g(B(X,Y), \xi) = g(A_\xi(X), Y)$

This equation allows us to trade information between the normal-valued tensor $B$ and the tangent-valued operator $A_\xi$. From the symmetry of $B$, it follows directly that each shape operator $A_\xi$ is a self-adjoint (symmetric) [linear operator](@entry_id:136520) on the [tangent space](@entry_id:141028) $T_pS$: $g(A_\xi X, Y) = g(X, A_\xi Y)$ [@problem_id:3051274].

### The Normal Connection and the Weingarten Formula

We have successfully defined a connection $\nabla^S$ on the [tangent bundle](@entry_id:161294) $TS$. The same principle can be applied to define a connection on the [normal bundle](@entry_id:272447) $NS$. This **normal connection**, denoted $\nabla^\perp$, captures how normal vector fields twist and turn as we move along the [submanifold](@entry_id:262388). It is defined, analogously to the [induced connection](@entry_id:635081), by projection:

$\nabla^\perp_X \xi := \pi^\perp(\nabla^M_X \xi)$

where $X$ is a [tangent vector](@entry_id:264836) field and $\xi$ is a [normal vector field](@entry_id:268853) [@problem_id:3051227]. Just as with $\nabla^S$, this definition is independent of any choices of extension to the ambient manifold $M$ [@problem_id:3051227].

With this definition, we can now write the full decomposition of the ambient derivative of a normal field $\xi$ in a tangential direction $X$. This is the **Weingarten formula**:

$\nabla^M_X \xi = -A_\xi(X) + \nabla^\perp_X \xi$

This equation is the counterpart to the Gauss formula. The Gauss formula decomposes the derivative of *tangent* fields, while the Weingarten formula decomposes the derivative of *normal* fields [@problem_id:3051224].

The normal connection $\nabla^\perp$ has properties analogous to a Levi-Civita connection. It can be shown to be compatible with the metric $g$ restricted to the fibers of the [normal bundle](@entry_id:272447) [@problem_id:3051227]. However, the notion of torsion is not well-defined for $\nabla^\perp$, as it mixes inputs from the tangent bundle and the [normal bundle](@entry_id:272447) [@problem_id:3051227].

### The Structural Equations of Submanifold Theory

We have now assembled all the necessary components: the intrinsic connection $\nabla^S$, the extrinsic second fundamental form $B$ (and [shape operator](@entry_id:264703) $A_\xi$), and the normal connection $\nabla^\perp$. The culmination of our work is a set of equations relating the curvatures of these connections to the curvature of the ambient space. These equations, known collectively as the Gauss-Codazzi-Ricci equations, are the foundation of [submanifold geometry](@entry_id:189265).

Let $R^M$ and $R^S$ be the Riemann curvature tensors of $(M,g)$ and $(S, g^S)$ respectively, using the convention $R(X,Y)Z = \nabla_X \nabla_Y Z - \nabla_Y \nabla_X Z - \nabla_{[X,Y]}Z$.

1.  **The Gauss Equation:** This equation relates the intrinsic curvature of $S$ to the ambient curvature and the second fundamental form. It reveals how much of the [submanifold](@entry_id:262388)'s curvature is inherited from the ambient space versus how much is generated by its own embedding. For [tangent vectors](@entry_id:265494) $X,Y,Z,W \in T_pS$, the equation is:
    $g(R^S(X,Y)Z, W) = g(R^M(X,Y)Z, W) + g(B(X,W), B(Y,Z)) - g(B(X,Z), B(Y,W))$
    This remarkable formula is a generalization of Gauss's *Theorema Egregium*. It shows that the intrinsic curvature of $S$ is not simply the restriction of the ambient curvature. There is a correction term that depends quadratically on the [second fundamental form](@entry_id:161454). This term measures how the bending of the [submanifold](@entry_id:262388) in normal directions contributes to its [intrinsic curvature](@entry_id:161701) [@problem_id:3051224].

2.  **The Codazzi-Mainardi Equation:** This equation arises from considering the normal component of the ambient curvature $R^M(X,Y)Z$. It relates the covariant derivative of the second fundamental form (using the connections $\nabla^S$ and $\nabla^\perp$) to the ambient curvature. It essentially expresses a compatibility condition between the intrinsic and extrinsic geometries.

3.  **The Ricci Equation:** Just as $R^S$ describes the curvature of the tangent bundle, we can define a [curvature tensor](@entry_id:181383) $R^\perp$ for the [normal bundle](@entry_id:272447) using the normal connection $\nabla^\perp$.
    $R^\perp(X,Y)\xi = \nabla^\perp_X \nabla^\perp_Y \xi - \nabla^\perp_Y \nabla^\perp_X \xi - \nabla^\perp_{[X,Y]} \xi$
    The Ricci equation relates this [normal curvature](@entry_id:270966) to the ambient curvature and the shape operators. For [tangent vectors](@entry_id:265494) $X, Y \in T_pS$ and normal vectors $\xi, \eta \in N_pS$, it states:
    $g(R^\perp(X,Y)\xi, \eta) = g(R^M(X,Y)\xi, \eta) + g([A_\xi, A_\eta](X), Y)$
    where $[A_\xi, A_\eta] = A_\xi A_\eta - A_\eta A_\xi$ is the commutator of the shape operators. This equation shows that the curvature of the [normal bundle](@entry_id:272447) depends on the ambient curvature and the extent to which the shape operators in different normal directions fail to commute [@problem_id:3051215].

Together, the Gauss, Codazzi, and Ricci equations provide a complete description of the local geometry of a submanifold. They decompose the ambient [curvature tensor](@entry_id:181383), when restricted to the [submanifold](@entry_id:262388), into its purely tangential, mixed, and purely normal components, relating each piece to the fundamental geometric objects of the [submanifold](@entry_id:262388).