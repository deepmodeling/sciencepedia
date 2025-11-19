## Introduction
Riemannian [submersions](@entry_id:159709) offer a powerful lens through which to analyze the intricate geometry of a manifold by decomposing it into a simpler base space and a collection of fibers. This technique is central to modern differential geometry, providing a bridge between spaces of different dimensions. However, this decomposition raises a critical question: how can we precisely relate the geometric properties, particularly the curvature, of the total space to the geometries of its constituent parts? The answer lies in a set of elegant and profound equations developed by Barrett O'Neill, which form the bedrock of [submersion](@entry_id:161795) theory.

This article provides a systematic exploration of this framework. The first chapter, "Principles and Mechanisms," will introduce the foundational concepts, including the vertical and horizontal distributions, the fundamental O'Neill tensors that measure the 'twist' of the submersion, and the celebrated curvature formulas that connect them all. The second chapter, "Applications and Interdisciplinary Connections," will showcase the theory's power by using it to compute curvature on symmetric spaces, construct new metrics, analyze the phenomenon of [manifold collapse](@entry_id:637039), and forge links to fields like geometric analysis and mathematical physics. Finally, "Hands-On Practices" will offer opportunities to solidify this understanding through targeted problems. This journey begins by dissecting the essential machinery that makes Riemannian [submersions](@entry_id:159709) a cornerstone of geometric investigation.

## Principles and Mechanisms

A Riemannian submersion provides a powerful framework for dissecting the geometry of a manifold by projecting it onto a lower-dimensional space. This process allows us to relate the curvatures and connections of the total space, the base space, and the fibers of the [submersion](@entry_id:161795). The key to this relationship lies in a set of fundamental equations and tensors, primarily developed by Barrett O'Neill, which encode the interaction between the vertical and horizontal geometry.

### The Vertical and Horizontal Distributions

Let $\pi: (M, g) \to (B, h)$ be a **Riemannian submersion**. This means that $\pi$ is a smooth [submersion](@entry_id:161795) between Riemannian manifolds, and for each point $p \in M$, the differential $d\pi_p$ maps the orthogonal complement of its kernel onto the [tangent space](@entry_id:141028) of the base isometrically.

This geometric structure induces a [canonical decomposition](@entry_id:634116) of the tangent bundle of $M$. At each point $p \in M$, the tangent space $T_p M$ splits into two orthogonal subspaces:

1.  The **vertical space** $\mathcal{V}_p$, which is the [tangent space](@entry_id:141028) to the fiber $\pi^{-1}(\pi(p))$. Equivalently, the vertical space is the kernel of the differential, $\mathcal{V}_p = \ker(d\pi_p)$. The collection of all such spaces forms the **vertical distribution** $\mathcal{V}$.

2.  The **horizontal space** $\mathcal{H}_p$, defined as the [orthogonal complement](@entry_id:151540) of the vertical space within $T_p M$, i.e., $\mathcal{H}_p = (\mathcal{V}_p)^\perp$. The collection of these spaces forms the **[horizontal distribution](@entry_id:196663)** $\mathcal{H}$.

Thus, we have an orthogonal [direct sum decomposition](@entry_id:263004) $TM = \mathcal{V} \oplus \mathcal{H}$. Any vector field $E$ on $M$ can be uniquely decomposed into its vertical and horizontal components, denoted $E = E^{\mathcal{V}} + E^{\mathcal{H}}$. The defining property of a Riemannian [submersion](@entry_id:161795) is that for any two horizontal vectors $X_p, Y_p \in \mathcal{H}_p$, the following isometry condition holds:
$$
h_{\pi(p)}(d\pi_p(X_p), d\pi_p(Y_p)) = g_p(X_p, Y_p)
$$
This condition ensures that the metric on the base space is precisely the one inherited from the horizontal geometry of the total space.

A vector field $X$ on $M$ is called **basic** if it is everywhere horizontal and is $\pi$-related to a vector field on the base. That is, there exists a vector field $\bar{X}$ on $B$ such that $d\pi(X) = \bar{X} \circ \pi$. Basic [vector fields](@entry_id:161384) serve as the essential link for comparing geometric quantities between $M$ and $B$.

### The Fundamental Tensors of a Submersion

The Levi-Civita connection $\nabla$ on $(M,g)$ generally does not preserve the vertical and horizontal distributions. The failure to do so is measured by two fundamental [tensor fields](@entry_id:190170), known as the **O'Neill tensors**, denoted $A$ and $T$.

Let $X, Y$ be horizontal vector fields and $U, V$ be vertical [vector fields](@entry_id:161384). The tensors $A$ and $T$ are defined by:

-   $A_X Y = (\nabla_X Y)^{\mathcal{V}}$
-   $T_U V = (\nabla_U V)^{\mathcal{H}}$

The tensor $A$ measures how the [covariant derivative](@entry_id:152476) of two horizontal fields can produce a vertical component. The tensor $T$ measures how the [covariant derivative](@entry_id:152476) of two vertical fields can produce a horizontal component.

These definitions can be extended to all vector fields $E, F$ on $M$ by first projecting the inputs onto their respective distributions [@problem_id:2989132]:
$$
A(E,F) := A(E^{\mathcal{H}}, F^{\mathcal{H}}) \qquad T(E,F) := T(E^{\mathcal{V}}, F^{\mathcal{V}})
$$
This convention immediately implies that if one of the arguments of $A$ is vertical or one of the arguments of $T$ is horizontal, the result is zero. For example, for a horizontal field $X$ and a vertical field $U$, we have $U^{\mathcal{H}} = 0$ and $X^{\mathcal{V}} = 0$, which from the [bilinearity](@entry_id:146819) of the base tensors leads to $A_X U = 0$ and $T_U X = 0$ [@problem_id:2989132].

These tensors possess fundamental symmetries and anti-symmetries that are direct consequences of the torsion-free property of the Levi-Civita connection, $\nabla_E F - \nabla_F E = [E,F]$.

For any vertical fields $U, V$, their Lie bracket $[U,V]$ is also a vertical field. This is because $d\pi([U,V]) = [d\pi(U), d\pi(V)] = [0,0] = 0$. Using the torsion-free property, we have $[U,V]^\mathcal{H} = (\nabla_U V)^\mathcal{H} - (\nabla_V U)^\mathcal{H}$. Since $[U,V]$ is vertical, its horizontal projection is zero. This gives:
$$
0 = T_U V - T_V U
$$
This shows that the tensor **$T$ is symmetric**.

For horizontal fields $X, Y$, the Lie bracket $[X,Y]$ is not necessarily horizontal. Its vertical component is given by:
$$
[X,Y]^\mathcal{V} = (\nabla_X Y)^\mathcal{V} - (\nabla_Y X)^\mathcal{V} = A_X Y - A_Y X
$$
This crucial formula reveals that the **skew-symmetric part of $A$ measures the vertical component of the Lie bracket of horizontal fields** [@problem_id:2989132] [@problem_id:2974964].

### Geometric Interpretation of A and T

The tensors $A$ and $T$ are not mere algebraic objects; they encode deep geometric information about the submersion.

The tensor $T$ is identical to the **second fundamental form of the fibers**. A [submanifold](@entry_id:262388) is **[totally geodesic](@entry_id:183906)** if any geodesic starting tangent to it remains within it. This is equivalent to its [second fundamental form](@entry_id:161454) being identically zero. For the fibers of a [submersion](@entry_id:161795), this means that for any two vertical vector fields $U, V$, the [covariant derivative](@entry_id:152476) $\nabla_U V$ must remain vertical. This is equivalent to the condition that its horizontal component, $(\nabla_U V)^\mathcal{H}$, vanishes. Therefore, **the fibers of a Riemannian [submersion](@entry_id:161795) are [totally geodesic](@entry_id:183906) if and only if $T \equiv 0$** [@problem_id:2989132] [@problem_id:2974964]. An important example where this occurs is the projection from the unit tangent bundle of a surface to the surface itself, when equipped with the Sasaki metric [@problem_id:2989139].

The tensor $A$ measures the failure of the [horizontal distribution](@entry_id:196663) to be **integrable**. By the Frobenius theorem, a distribution is integrable if and only if it is closed under the Lie bracket. For the [horizontal distribution](@entry_id:196663) $\mathcal{H}$, this means that for any two horizontal fields $X, Y$, their Lie bracket $[X,Y]$ must also be horizontal. This is equivalent to $[X,Y]^\mathcal{V} = 0$. From the formula above, this condition is equivalent to $A_X Y = A_Y X$. Therefore, **the [horizontal distribution](@entry_id:196663) is integrable if and only if the tensor $A$ is symmetric** [@problem_id:2974964]. If $\mathcal{H}$ is not integrable, geodesics that start horizontally may develop vertical components. When $A \equiv 0$, the [horizontal distribution](@entry_id:196663) is not only integrable but also [totally geodesic](@entry_id:183906).

Many important Riemannian [submersions](@entry_id:159709), such as [principal bundles](@entry_id:160029) with non-flat connections, feature a non-integrable [horizontal distribution](@entry_id:196663). For instance, the Heisenberg group provides a canonical example. By defining a [left-invariant metric](@entry_id:637439) on a compact quotient of the Heisenberg group, we can construct a principal circle bundle over a flat 2-torus, $\pi: M \to T^2$. The structure equations for the Lie algebra can be used to show that the Lie bracket of the horizontal basis fields $E_1, E_2$ has a non-zero vertical component, $[E_1, E_2] = nU$, where $U$ is the vertical field. This directly implies a non-zero, [skew-symmetric tensor](@entry_id:199349) $A$ [@problem_id:2989135]. A direct calculation using the Koszul formula shows that $A_{E_1} E_2 = \frac{n}{2} U$.

### The Submersion and the Levi-Civita Connection

A cornerstone of the theory is the relationship between the Levi-Civita connection $\nabla$ on the total space $M$ and the Levi-Civita connection $\nabla^B$ on the base space $B$. For any two basic [vector fields](@entry_id:161384) $X, Y$ on $M$, which are lifts of fields $\bar{X}, \bar{Y}$ on $B$, the horizontal part of their covariant derivative projects precisely to the covariant derivative of the base fields:
$$
d\pi((\nabla_X Y)^{\mathcal{H}}) = \nabla^B_{\bar{X}} \bar{Y}
$$
This identity, sometimes called the **Gauss equation** for [submersions](@entry_id:159709), can be proven by showing that the connection on $B$ defined by the left-hand side is both torsion-free and [metric-compatible](@entry_id:160255), and thus must coincide with the unique Levi-Civita connection $\nabla^B$ [@problem_id:2989132] [@problem_id:2974964]. This formula confirms that the geometry of the base space is not arbitrary, but is intrinsically determined by the horizontal geometry of the total space.

With this, we can write a full decomposition of the covariant derivative. For horizontal fields $X, Y$ and vertical fields $U, V$:
-   $\nabla_X Y = (\nabla_X Y)^{\mathcal{H}} + A_X Y$
-   $\nabla_U V = T_U V + (\nabla_U V)^{\mathcal{V}}$
-   $\nabla_X U = (\nabla_X U)^{\mathcal{H}} + (\nabla_X U)^{\mathcal{V}}$
-   $\nabla_U X = (\nabla_U X)^{\mathcal{H}} + (\nabla_U X)^{\mathcal{V}}$

The cross-terms $\nabla_X U$ and $\nabla_U X$ can also be related to the tensors $A$ and $T$. For instance, one can show that for a horizontal field $X$ and vertical field $U$, $g((\nabla_X U)^{\mathcal{H}}, Y) = -g(U, A_X Y)$ for any horizontal $Y$.

### O'Neill's Curvature Formulas

The most celebrated results of the theory are O'Neill's formulas, which express the [sectional curvature](@entry_id:159738) of the total space $(M,g)$ in terms of the curvature of the base space, the fibers, and the tensors $A$ and $T$.

Let us consider a 2-plane in $T_p M$. We have three cases:

1.  **Horizontal Plane:** Let $\{X, Y\}$ be an orthonormal basis for a horizontal plane in $T_p M$. Let $\{\bar{X}, \bar{Y}\}$ be the corresponding [orthonormal basis](@entry_id:147779) for a plane in $T_{\pi(p)} B$. The sectional curvatures are related by:
    $$
    K_M(X, Y) = K_B(\bar{X}, \bar{Y}) - 3\|A_X Y\|_g^2
    $$
    This formula is remarkable. It shows that the curvature of the total space is always less than or equal to the curvature of the base space. The non-integrability of the [horizontal distribution](@entry_id:196663), quantified by $\|A_X Y\|^2$, pulls the curvature down. Conversely, it implies that the base space can have significantly higher curvature than the total space.

    A classic illustration is the **Hopf fibration** $\pi: S^3 \to S^2 \cong \mathbb{C}P^1$. The total space $S^3$ with its standard round metric has [constant sectional curvature](@entry_id:272200) $K_{S^3}=1$. The base space $\mathbb{C}P^1$ inherits a metric that makes this map a Riemannian submersion. By choosing a convenient point and computing the term $\|A_X Y\|^2$ for a horizontal plane, one finds that $\|A_X Y\|^2=1$. Plugging this into O'Neill's formula gives:
    $$
    K_{\mathbb{C}P^1} = K_{S^3}(X,Y) + 3\|A_X Y\|^2 = 1 + 3(1) = 4
    $$
    Thus, the [complex projective line](@entry_id:276948) has [constant sectional curvature](@entry_id:272200) 4, a result beautifully derived from the geometry of the 3-sphere [@problem_id:1661486]. A similar calculation for the [submersion](@entry_id:161795) $\pi: US^2 \to S^2$ shows that for a horizontal plane spanned by $\{v^h, w^h\}$, the curvature is $K_{US^2}(v^h, w^h) = K_{S^2}(v,w) - 3\|A_{v^h} w^h}\|^2 = 1 - 3(\frac{1}{4}) = \frac{1}{4}$ [@problem_id:2989139].

2.  **Vertical Plane:** Let $\{U, V\}$ be an orthonormal basis for a vertical plane. The sectional curvature is given by:
    $$
    K_M(U, V) = K_{\text{fiber}}(U, V) - \|T_U V\|_g^2
    $$
    Here, $K_{\text{fiber}}(U,V)$ is the intrinsic [sectional curvature](@entry_id:159738) of the fiber itself. This shows that the [extrinsic curvature](@entry_id:160405) of the fibers, measured by $T$, also pulls down the curvature of the total space. If the fibers are [totally geodesic](@entry_id:183906) ($T \equiv 0$), then $K_M(U,V) = K_{\text{fiber}}(U,V)$.

3.  **Mixed Plane:** For an orthonormal pair consisting of a horizontal vector $X$ and a vertical vector $U$, the formula is:
    $$
    K_M(X, U) = g(\nabla_U(A_X X), U) - \|(\nabla_U X)^{\mathcal{H}}\|^2
    $$
    This formula shows how the curvature of mixed planes depends on the covariant derivatives of the fundamental tensors.

### Application: Collapsing Manifolds with Bounded Curvature

O'Neill's formulas are a critical tool in the study of **collapsing manifolds**, a central topic in modern geometry. Consider an effective isometric action of a torus $T^k$ on a closed manifold $(M^n, g)$. We can attempt to "collapse" $M$ onto its [orbit space](@entry_id:148658) $M/T^k$ by shrinking the orbits. This is modeled by introducing a family of metrics $g_\epsilon = \epsilon^2 g^{\text{vert}} + g^{\text{hor}}$, where $g^{\text{vert}}$ is the metric restricted to the vertical distribution (tangent to orbits) and $g^{\text{hor}}$ is the metric on its horizontal complement. As $\epsilon \to 0$, the diameter of the orbits shrinks to zero. A key question is whether the [sectional curvature](@entry_id:159738) remains uniformly bounded during this process.

O'Neill's formulas provide the answer. In the setting of a free torus action, $\pi: M \to B=M/T^k$ is a principal $T^k$-bundle. If we assume the fibers are [totally geodesic](@entry_id:183906) ($T=0$), the curvature formulas for the metric $g_\epsilon$ become [@problem_id:2971421]:
-   $K_{g_\epsilon}(X, Y) = K_B(\bar{X}, \bar{Y}) - 3\epsilon^2\|A_X Y\|_g^2$
-   $K_{g_\epsilon}(U/\epsilon, V/\epsilon) = K_{\text{fiber}}(U,V)$
-   $K_{g_\epsilon}(X, U/\epsilon) = K_g(X,U)$

Since the original manifold is compact, all terms on the right-hand sides are bounded. As $\epsilon \to 0$, the [sectional curvature](@entry_id:159738) of $(M, g_\epsilon)$ remains uniformly bounded. The manifold $(M, g_\epsilon)$ collapses with [bounded curvature](@entry_id:183139) to the smooth base manifold $(B, h)$ in the Gromov-Hausdorff sense.

The situation is drastically different if the torus action has **singular strata**, i.e., orbits where the [stabilizer subgroup](@entry_id:137216) is non-trivial. In this case, the [orbit space](@entry_id:148658) $B=M/T^k$ is not a [smooth manifold](@entry_id:156564) but an Alexandrov space with conical singularities. A naive scaling $g_\epsilon$ as above would cause curvature to blow up near the singular strata. However, [bounded curvature](@entry_id:183139) collapse is still achievable through a more sophisticated modification of the metric near the singularities. The resulting Gromov-Hausdorff limit is the singular [orbit space](@entry_id:148658) $B$, which serves as a foundational example of an Alexandrov space arising from a geometric construction [@problem_id:2971421]. This illustrates the profound utility of Riemannian submersion theory in understanding the structure of both smooth and singular geometric spaces.