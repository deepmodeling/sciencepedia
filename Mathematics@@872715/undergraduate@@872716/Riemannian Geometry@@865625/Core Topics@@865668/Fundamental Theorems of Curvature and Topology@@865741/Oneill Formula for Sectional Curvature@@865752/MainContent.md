## Introduction
In [differential geometry](@entry_id:145818), Riemannian [submersions](@entry_id:159709) offer a powerful method for deconstructing [complex manifolds](@entry_id:159076) into simpler, lower-dimensional components: a base space and a collection of fibers. This decomposition is fundamental to understanding the geometry of many important spaces, from the [projective spaces](@entry_id:157963) of algebra to the extra dimensions of theoretical physics. A central question that arises is how the curvature—the ultimate measure of a manifold's local geometry—of the total space relates to the curvatures of its constituent parts. Simply put, how does the "twisting" of the fibers over the base influence the overall geometry?

This article addresses this question by providing a comprehensive exploration of the O'Neill formulas for [sectional curvature](@entry_id:159738). These formulas serve as the definitive bridge connecting the geometry of the total space, the base, and the fibers. We will see how the interaction between the horizontal and vertical geometry is captured by two fundamental objects, the O'Neill tensors, and how these tensors directly enter the curvature equations.

This exploration is structured into three chapters. The first, **Principles and Mechanisms**, will lay the theoretical groundwork by defining the [horizontal and vertical distributions](@entry_id:637120), introducing the O'Neill tensors, and deriving the main curvature formulas. The second chapter, **Applications and Interdisciplinary Connections**, will showcase the utility of these formulas through canonical examples like the Hopf [fibration](@entry_id:162085) and warped products, and explore their significance in fields such as geometric analysis and Kaluza-Klein theory. Finally, **Hands-On Practices** offers a series of guided problems to solidify your computational skills and geometric intuition. By the end, you will have a robust understanding of how to analyze and compute curvature in the rich setting of a Riemannian [submersion](@entry_id:161795).

## Principles and Mechanisms

A Riemannian [submersion](@entry_id:161795) $\pi: (M,g) \to (B, \bar{g})$ provides a rich geometric structure by relating a "total space" $M$ to a "base space" $B$. Central to this structure is the [orthogonal decomposition](@entry_id:148020) of the [tangent space](@entry_id:141028) at any point $p \in M$ into vertical and horizontal subspaces, $T_pM = \mathcal{V}_p \oplus \mathcal{H}_p$. The **vertical space** $\mathcal{V}_p = \ker(d\pi_p)$ is the [tangent space](@entry_id:141028) to the fiber $\pi^{-1}(\pi(p))$, while the **horizontal space** $\mathcal{H}_p = \mathcal{V}_p^{\perp}$ is its orthogonal complement. A defining feature of a Riemannian [submersion](@entry_id:161795) is that the differential $d\pi_p$ restricts to a linear [isometry](@entry_id:150881) from the horizontal space $\mathcal{H}_p$ onto the tangent space of the base $T_{\pi(p)}B$.

This isometric relationship is the foundation for comparing the curvature of $M$ with that of $B$. For any orthonormal pair of horizontal vectors $\{X, Y\}$ in $\mathcal{H}_p$, their images $\{d\pi_p X, d\pi_p Y\}$ form an orthonormal pair in $T_{\pi(p)}B$. Orthonormal vectors are necessarily [linearly independent](@entry_id:148207), which ensures that they span a well-defined 2-plane. Consequently, the sectional curvature of the base, $K^B(d\pi_p X, d\pi_p Y)$, is always well-defined, making a comparison with the [sectional curvature](@entry_id:159738) $K^M(X,Y)$ in the total space a meaningful endeavor [@problem_id:3060965]. The goal of this chapter is to detail the precise relationships between these curvatures, a task accomplished through the formulas developed by Barrett O'Neill.

### Decomposing the Connection: The O'Neill Tensors

The key to unlocking the relationship between the curvatures of $M$, $B$, and the fibers of $\pi$ lies in analyzing the Levi-Civita connection $\nabla$ of the total space $(M,g)$. While the [tangent bundle](@entry_id:161294) $TM$ splits neatly into an orthogonal sum $\mathcal{H} \oplus \mathcal{V}$, the connection $\nabla$ does not, in general, preserve this splitting. The manner in which it fails to do so encodes the essential geometric information about the submersion. This strategy of decomposing the connection is the central mechanism for all subsequent analysis [@problem_id:3060953].

We decompose the covariant derivative of a vector field by projecting its components onto the [horizontal and vertical distributions](@entry_id:637120). This process gives rise to two fundamental tensors, known as the **O'Neill tensors**, typically denoted by $A$ and $T$.

For [vector fields](@entry_id:161384) $X, Y$ that are everywhere horizontal, the [covariant derivative](@entry_id:152476) $\nabla_X Y$ is not necessarily horizontal. Its vertical part defines the first O'Neill tensor:
**Definition (The A-Tensor):** For horizontal [vector fields](@entry_id:161384) $X, Y$, the tensor $A$ is defined by
$$ A_X Y := (\nabla_X Y)^{\mathcal{V}} $$
where $(\cdot)^{\mathcal{V}}$ denotes the [orthogonal projection](@entry_id:144168) onto the vertical distribution $\mathcal{V}$.

Similarly, for vector fields $U, V$ that are everywhere vertical, the covariant derivative $\nabla_U V$ is not necessarily vertical. Its horizontal part defines the second O'Neill tensor:
**Definition (The T-Tensor):** For vertical [vector fields](@entry_id:161384) $U, V$, the tensor $T$ is defined by
$$ T_U V := (\nabla_U V)^{\mathcal{H}} $$
where $(\cdot)^{\mathcal{H}}$ denotes the orthogonal projection onto the [horizontal distribution](@entry_id:196663) $\mathcal{H}$.

These tensors quantify the "mixing" of the [horizontal and vertical distributions](@entry_id:637120) by the Levi-Civita connection. Their geometric significance becomes clear when we consider the simplest possible case of a Riemannian [submersion](@entry_id:161795).

### The Baseline Case: Riemannian Products

Consider a Riemannian product manifold $(M,g)$, where $M = B \times F$ and the metric is a direct sum $g = g_B \oplus g_F$. The natural projection $\pi: B \times F \to B$ is a canonical example of a Riemannian [submersion](@entry_id:161795). In this case, the [horizontal distribution](@entry_id:196663) $\mathcal{H}$ corresponds to the [tangent spaces](@entry_id:199137) of $B$, and the vertical distribution $\mathcal{V}$ corresponds to the tangent spaces of $F$.

A fundamental property of the Levi-Civita connection on a Riemannian product is that it completely preserves the product structure. Specifically, for horizontal vector fields $X, Y$ and vertical vector fields $U, V$:
1.  $\nabla_X Y$ is horizontal.
2.  $\nabla_U V$ is vertical.
3.  $\nabla_X U = \nabla_U X = 0$.

From these properties, it immediately follows that the O'Neill tensors vanish identically:
-   $A_X Y = (\nabla_X Y)^{\mathcal{V}} = 0$ since $\nabla_X Y$ is purely horizontal.
-   $T_U V = (\nabla_U V)^{\mathcal{H}} = 0$ since $\nabla_U V$ is purely vertical.

This vanishing has profound geometric consequences. Since $T \equiv 0$, the fibers $\{b\} \times F$ are **[totally geodesic submanifolds](@entry_id:637049)** of $M$. Since $A \equiv 0$, the [horizontal distribution](@entry_id:196663) $\mathcal{H}$ is **integrable**, meaning it is closed under the Lie bracket. The local integral [submanifolds](@entry_id:159439) for $\mathcal{H}$ are slices of the form $B \times \{f\}$.

In this simplified setting where $A \equiv 0$ and $T \equiv 0$, the curvature of the product space relates to the curvatures of its factors in the most straightforward way [@problem_id:3060961]:
-   **Horizontal Curvature:** $K^M(X,Y) = K^B(d\pi X, d\pi Y)$
-   **Vertical Curvature:** $K^M(U,V) = K^F(U,V)$
-   **Mixed Curvature:** $K^M(X,U) = 0$

This product case serves as our baseline. The O'Neill tensors, therefore, measure the deviation of a general Riemannian [submersion](@entry_id:161795) from being a simple Riemannian product.

### Geometric Interpretation of the O'Neill Tensors

In a general Riemannian [submersion](@entry_id:161795), the tensors $A$ and $T$ are the obstructions to the local geometry being a product.

The tensor $A$ is intrinsically linked to the integrability of the [horizontal distribution](@entry_id:196663). For any two horizontal vector fields $X$ and $Y$, the vertical part of their Lie bracket is given by $[X,Y]^{\mathcal{V}} = A_X Y - A_Y X$. By the Frobenius theorem, the distribution $\mathcal{H}$ is integrable if and only if $[X,Y]$ is horizontal for all horizontal $X,Y$. This is equivalent to $A_X Y = A_Y X$. However, a crucial property for **basic** horizontal [vector fields](@entry_id:161384) (those that are $\pi$-related to [vector fields](@entry_id:161384) on the base) is that $A$ is skew-symmetric: $A_X Y = -A_Y X$ [@problem_id:3060968]. Thus, for a [submersion](@entry_id:161795) defined by basic fields, $\mathcal{H}$ is integrable if and only if $A \equiv 0$.

The tensor $T$ has an equally clear geometric interpretation. A fiber $F = \pi^{-1}(b)$ is a [submanifold](@entry_id:262388) of $M$. Its [second fundamental form](@entry_id:161454), $\mathrm{II}(U,V)$, which measures the failure of the fiber to be [totally geodesic](@entry_id:183906), is defined as the component of $\nabla_U V$ normal to the fiber. Since the [normal space](@entry_id:154487) to the vertical fiber is the horizontal space, we have $\mathrm{II}(U,V) = (\nabla_U V)^{\mathcal{H}}$. This is precisely the definition of the O'Neill tensor $T_U V$ [@problem_id:3060952] [@problem_id:3060982]. Therefore:
-   The fibers of a Riemannian submersion are **[totally geodesic](@entry_id:183906)** if and only if the O'Neill tensor **$T \equiv 0$** [@problem_id:3060956].

The conditions $A \equiv 0$ and $T \equiv 0$ are independent. For example, in the famous Hopf [fibration](@entry_id:162085) $\pi: S^3 \to S^2$, the fibers are great circles, which are [totally geodesic](@entry_id:183906), so $T \equiv 0$. However, the [horizontal distribution](@entry_id:196663) is not integrable, so $A \not\equiv 0$. Conversely, one can construct [submersions](@entry_id:159709) where $\mathcal{H}$ is integrable ($A \equiv 0$) but the fibers are not [totally geodesic](@entry_id:183906) ($T \not\equiv 0$).

This leads to a profound unifying principle known as the de Rham Decomposition Theorem. If both distributions $\mathcal{H}$ and $\mathcal{V}$ are integrable and their geometry does not mix (i.e., they are parallel with respect to $\nabla$), then the manifold decomposes. For a Riemannian submersion, this translates to the conditions $A \equiv 0$ and $T \equiv 0$. If both O'Neill tensors vanish, $(M,g)$ is locally isometric to a Riemannian product of an open set in the base and a piece of a fiber [@problem_id:3060957].

### The O'Neill Curvature Formulas

With a clear understanding of the tensors $A$ and $T$, we can now state and interpret the main formulas relating the sectional curvatures.

#### Curvature of Horizontal Planes

For a 2-plane spanned by an orthonormal pair of **horizontal** vectors $\{X, Y\}$ at a point $p \in M$, the sectional curvature $K^M(X,Y)$ is given by:

$$ K^M(X,Y) = K^B(d\pi_p X, d\pi_p Y) - 3 \|A_X Y\|^2 $$

This is O'Neill's first fundamental formula. The term $\|A_X Y\|^2$ is always non-negative. This formula reveals that the non-integrability of the [horizontal distribution](@entry_id:196663) ($A \not\equiv 0$) always **decreases** the sectional curvature of horizontal planes in the total space relative to the corresponding plane in the base space.

A detailed derivation involves substituting the decomposed connection into the definition of the Riemann tensor, $R^M(X,Y)Y = \nabla_X \nabla_Y Y - \nabla_Y \nabla_X Y - \nabla_{[X,Y]} Y$, and taking the inner product with $X$ [@problem_id:3060980]. The terms involving the horizontal parts of the connection assemble to give the base curvature $K^B$, while the terms involving the vertical "leakage" encoded by $A$ combine, using the skew-symmetry of $A$ for basic fields, to produce the correction term $-3\|A_X Y\|^2$ [@problem_id:3060968].

Alternatively, we can express the base curvature in terms of the total space curvature:

$$ K^B(d\pi_p X, d\pi_p Y) = K^M(X,Y) + 3 \|A_X Y\|^2 $$

This form emphasizes that the non-integrability of the [horizontal distribution](@entry_id:196663) **increases** the curvature of the base space. The "twisting" of the fibers adds positive curvature to the base.

#### Curvature of Vertical Planes

For a 2-plane spanned by an orthonormal pair of **vertical** vectors $\{U, V\}$, the relationship is governed by the Gauss equation of [submanifold theory](@entry_id:190701), with the tensor $T$ playing the role of the [second fundamental form](@entry_id:161454) of the fiber. The formula is:

$$ K^M(U,V) = K^F(U,V) + \|T_U V\|^2 - \langle T_U U, T_V V \rangle $$

where $K^F(U,V)$ is the intrinsic [sectional curvature](@entry_id:159738) of the fiber. The effect of the [extrinsic curvature](@entry_id:160405) of the fiber (measured by $T$) is more complex than in the horizontal case [@problem_id:3060970].

- The term $\|T_U V\|^2$ is non-negative and tends to **increase** $K^M$ relative to $K^F$.
- The term $-\langle T_U U, T_V V \rangle$ can be positive, negative, or zero, depending on the geometry. It often tends to **decrease** $K^M$ relative to $K^F$.

The total effect depends on the competition between these two terms. The [sectional curvature](@entry_id:159738) of the total space is less than that of the fiber, $K^M  K^F$, precisely when $\langle T_U U, T_V V \rangle > \|T_U V\|^2$. A direct and important consequence is that if the fibers are [totally geodesic](@entry_id:183906) ($T \equiv 0$), then the curvature formula simplifies to an equality: $K^M(U,V) = K^F(U,V)$ [@problem_id:3060956].

#### Curvature of Mixed Planes

For a "mixed" plane spanned by an orthonormal pair consisting of a horizontal vector $X$ and a vertical vector $U$, the sectional curvature $K^M(X,U)$ measures the interaction between the two distributions. The formula can be expressed in terms of the O'Neill tensors, but the most important conceptual point is its value in the baseline case. As established for a Riemannian product where $A \equiv 0$ and $T \equiv 0$, the curvature of any mixed plane is identically zero: $K^M(X,U)=0$ [@problem_id:3060961] [@problem_id:3060957]. Thus, non-zero mixed curvature is a direct consequence of the non-triviality of the O'Neill tensors.

### A Canonical Example: The Hopf Fibration

The Hopf [fibration](@entry_id:162085) provides a beautiful and concrete illustration of these principles. Consider the submersion $\pi: S^3 \to S^2$, where $S^3$ is equipped with its standard metric of [constant sectional curvature](@entry_id:272200) $K^{S^3}=1$. The metric induced on $S^2$ is such that $\pi$ becomes a Riemannian submersion.

The total space $S^3$ can be identified with the Lie group $\mathrm{SU}(2)$. We can choose a global [orthonormal frame](@entry_id:189702) $\{E_1, E_2, E_3\}$ of [left-invariant vector fields](@entry_id:637116) such that at every point, $\mathcal{H} = \mathrm{span}\{E_1, E_2\}$ and $\mathcal{V} = \mathrm{span}\{E_3\}$. The Lie algebra structure of $\mathfrak{su}(2)$ dictates the [commutation relations](@entry_id:136780), a standard choice being $[E_1, E_2] = 2E_3$.

Let's apply our framework [@problem_id:3060977]:
1.  **Fiber Geometry**: The fibers of the Hopf [fibration](@entry_id:162085) are great circles in $S^3$. Great circles are geodesics, so the fibers are [totally geodesic submanifolds](@entry_id:637049). This immediately implies that the O'Neill tensor $T \equiv 0$.
2.  **Horizontal Geometry**: We can compute the A-tensor. For a [bi-invariant metric](@entry_id:184842) on a Lie group, the Levi-Civita connection is given by $\nabla_X Y = \frac{1}{2}[X,Y]$ for [left-invariant vector fields](@entry_id:637116) $X, Y$. Applying this, we get $A_{E_1} E_2 = (\nabla_{E_1} E_2)^{\mathcal{V}} = (\frac{1}{2}[E_1, E_2])^{\mathcal{V}} = (\frac{1}{2}(2E_3))^{\mathcal{V}} = E_3$.
3.  **Curvature Calculation**: Since $A_{E_1}E_2 = E_3 \neq 0$, the [horizontal distribution](@entry_id:196663) is not integrable. We can now use O'Neill's formula to find the curvature of the base space $S^2$. Let $\bar{X} = d\pi E_1$ and $\bar{Y} = d\pi E_2$ be an orthonormal basis for a tangent plane on $S^2$.
    $$ K^{S^2}(\bar{X}, \bar{Y}) = K^{S^3}(E_1, E_2) + 3 \|A_{E_1} E_2\|^2 $$
    We know the curvature of $S^3$ is $K^{S^3}(E_1, E_2) = 1$. We just calculated $A_{E_1}E_2 = E_3$, and since $\{E_i\}$ is an [orthonormal frame](@entry_id:189702), $\|E_3\|^2=1$. Plugging these values in:
    $$ K^{S^2} = 1 + 3(1)^2 = 4 $$
This remarkable result shows that the standard metric on $S^2$ induced by the Hopf [fibration](@entry_id:162085) has a [constant sectional curvature](@entry_id:272200) of 4. The [positive curvature](@entry_id:269220) is enhanced precisely because of the "twisting" of the $S^3$ fibers, a geometric feature captured perfectly by the non-vanishing of the O'Neill tensor $A$.