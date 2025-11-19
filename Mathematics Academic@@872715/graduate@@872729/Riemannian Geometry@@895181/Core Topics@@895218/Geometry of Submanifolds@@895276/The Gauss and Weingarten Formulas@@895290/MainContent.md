## Introduction
In the field of Riemannian geometry, understanding the geometry of a submanifold—a space living inside a larger, ambient space—is a central challenge. How does the curvature of the larger space and the way the submanifold is "bent" within it dictate the [submanifold](@entry_id:262388)'s own [intrinsic geometry](@entry_id:158788)? Answering this question requires a precise mathematical framework for relating the geometric structures of the ambient manifold to those of the submanifold. This is the fundamental problem addressed by the theory of submanifolds, and its cornerstone is a pair of elegant and powerful identities: the Gauss and Weingarten formulas.

This article provides a comprehensive exploration of these formulas, guiding you from their fundamental principles to their profound applications. The journey is structured into three parts. In **Principles and Mechanisms**, we will dissect the core idea of decomposing [vector fields](@entry_id:161384) into tangential and normal components, leading to the definitions of the second fundamental form and the [shape operator](@entry_id:264703). We will establish their key properties and show how they form the basis for the fundamental [structural equations](@entry_id:274644) of [submanifolds](@entry_id:159439). Next, in **Applications and Interdisciplinary Connections**, we will see this theory in action, using it to characterize classic surfaces, derive the celebrated Theorema Egregium, and explore its impact on diverse fields such as [solid mechanics](@entry_id:164042), physics, and modern geometric analysis. Finally, the **Hands-On Practices** section offers a set of guided problems, allowing you to solidify your understanding through direct computation and theoretical exploration, from basic calculations in Euclidean space to advanced concepts in higher [codimension](@entry_id:273141). Let's begin by establishing the principles that underpin this entire framework.

## Principles and Mechanisms

The study of [submanifolds](@entry_id:159439) within a larger Riemannian manifold hinges on a single, powerful idea: decomposing the geometric structures of the ambient space into components that are either tangential or normal to the [submanifold](@entry_id:262388). This decomposition allows us to understand how the intrinsic geometry of the submanifold, such as its curvature, is constrained and shaped by its [extrinsic geometry](@entry_id:262461)—the way it is embedded or immersed in the ambient space. The primary tools for this analysis are the **Gauss formula** and the **Weingarten formula**, which precisely describe the behavior of the ambient [covariant derivative](@entry_id:152476) when applied to [vector fields](@entry_id:161384) related to the [submanifold](@entry_id:262388).

### The Gauss Formula: Differentiating Tangent Fields

Let $(M, g)$ be a manifold isometrically immersed in a Riemannian manifold $(\bar{M}, \bar{g})$. For any point $p \in M$, the [tangent space](@entry_id:141028) of the ambient manifold, $T_p\bar{M}$, can be decomposed into an orthogonal [direct sum](@entry_id:156782) of the tangent space to the [submanifold](@entry_id:262388), $T_pM$, and its [orthogonal complement](@entry_id:151540), the normal space $N_pM$:
$T_p\bar{M} = T_pM \oplus N_pM$.

Consider two [vector fields](@entry_id:161384) $X$ and $Y$ that are tangent to $M$. We can extend them to be vector fields in a neighborhood of $M$ in $\bar{M}$. The covariant derivative of $Y$ with respect to $X$ in the ambient manifold, $\bar{\nabla}_X Y$, produces a vector field that is not, in general, tangent to $M$. However, at each point $p \in M$, the vector $(\bar{\nabla}_X Y)_p$ lies in $T_p\bar{M}$ and can therefore be uniquely decomposed into its tangential and normal components.

This decomposition gives rise to two fundamental objects. We define the **[induced connection](@entry_id:635081)** $\nabla$ on $M$ as the tangential projection of the ambient connection:
$$
\nabla_X Y := (\bar{\nabla}_X Y)^\top = \operatorname{pr}^\top(\bar{\nabla}_X Y)
$$
And we define the **[second fundamental form](@entry_id:161454)** $B$ as the normal projection:
$$
B(X,Y) := (\bar{\nabla}_X Y)^\perp = \operatorname{pr}^\perp(\bar{\nabla}_X Y)
$$
These definitions immediately yield the **Gauss formula**, which expresses the ambient [covariant derivative](@entry_id:152476) in terms of these new objects:
$$
\bar{\nabla}_X Y = \nabla_X Y + B(X,Y)
$$

A critical first step is to establish the nature of the [induced connection](@entry_id:635081) $\nabla$. As demonstrated in the derivation underlying [@problem_id:2997218], this connection is precisely the Levi-Civita connection of the [induced metric](@entry_id:160616) $g$ on $M$. This is proven by showing that $\nabla$ satisfies the two defining properties of a Levi-Civita connection: it is torsion-free and compatible with the metric $g$.
1.  **Torsion-freeness**: The torsion of $\nabla$ is $T(X,Y) = \nabla_X Y - \nabla_Y X - [X,Y]$. Since $\bar{\nabla}$ is torsion-free, $\bar{\nabla}_X Y - \bar{\nabla}_Y X = [X,Y]$. Projecting this identity onto the tangent bundle $TM$ yields $\nabla_X Y - \nabla_Y X = [X,Y]$, as the Lie bracket of two [tangent vector](@entry_id:264836) fields is also tangent. Thus, $T(X,Y) = 0$.
2.  **Metric Compatibility**: Metric compatibility requires $Z(g(X,Y)) = g(\nabla_Z X, Y) + g(X, \nabla_Z Y)$. Since $\bar{\nabla}$ is compatible with $\bar{g}$, we have $Z(\bar{g}(X,Y)) = \bar{g}(\bar{\nabla}_Z X, Y) + \bar{g}(X, \bar{\nabla}_Z Y)$. Substituting the Gauss formula and using the orthogonality of tangent and normal vectors shows that the terms involving the [second fundamental form](@entry_id:161454), such as $\bar{g}(B(Z,X), Y)$, vanish, leaving the desired identity for $\nabla$ and $g$.

The [second fundamental form](@entry_id:161454), $B$, captures the "acceleration" of the [submanifold](@entry_id:262388) within the ambient space. It measures how much the [tangent space](@entry_id:141028) is "twisting" in the normal directions. As a direct consequence of its definition and the properties of the Levi-Civita connection, the second fundamental form is a tensor that is symmetric in its two arguments [@problem_id:2997223].
*   **Tensoriality**: The map $B(X,Y)$ is bilinear over the ring of smooth functions $C^\infty(M)$. Linearity in the first argument, $B(fX, Y) = f B(X,Y)$, follows from the linearity of $\bar{\nabla}$ in its first argument. Linearity in the second argument, $B(X, fY) = f B(X,Y)$, follows from the Leibniz rule for $\bar{\nabla}$, noting that the term $(Xf)Y$ is tangent and thus its normal projection is zero.
*   **Symmetry**: The symmetry $B(X,Y) = B(Y,X)$ is a direct consequence of the torsion-free property of $\bar{\nabla}$. Specifically, $B(X,Y) - B(Y,X) = (\bar{\nabla}_X Y - \bar{\nabla}_Y X)^\perp = ([X,Y])^\perp$. Since the Lie bracket of two tangent vector fields is another [tangent vector](@entry_id:264836) field, its normal projection is zero, proving symmetry.

In the important special case where the ambient manifold is Euclidean space $\mathbb{R}^n$, the ambient Levi-Civita connection $\bar{\nabla}$ simplifies to the standard directional derivative of [vector fields](@entry_id:161384), where derivatives are taken component-wise. This provides a very concrete setting for calculation [@problem_id:2997189]. For example, if a surface in $\mathbb{R}^3$ is given by a [parametrization](@entry_id:272587) $r(u,v)$, the [second fundamental form](@entry_id:161454) applied to the [coordinate vector](@entry_id:153319) fields $\partial_u$ and $\partial_u$ is simply the normal component of the [second partial derivative](@entry_id:172039) vector $r_{uu}$: $B(\partial_u, \partial_u) = (r_{uu})^\perp$.

### The Weingarten Formula: Differentiating Normal Fields

Having analyzed the derivative of tangent vector fields, we now turn to the derivative of a [normal vector field](@entry_id:268853) $\xi \in \Gamma(NM)$ along a tangent direction $X \in \Gamma(TM)$. Just as before, the ambient derivative $\bar{\nabla}_X \xi$ can be decomposed into its tangential and normal parts. This decomposition defines two more key geometric objects.

The tangential component of $\bar{\nabla}_X \xi$ describes how the [normal vector](@entry_id:264185) "tilts" into the tangent space. We define the **shape operator** (or **Weingarten map**) $S_\xi: TM \to TM$ as the negative of this tangential projection:
$$
S_\xi X := -(\bar{\nabla}_X \xi)^\top
$$
The negative sign is a widely adopted convention that simplifies later formulas, particularly the Gauss equation.

The normal component of $\bar{\nabla}_X \xi$ describes the rate of change of $\xi$ within the [normal bundle](@entry_id:272447) itself. This defines the **normal connection** $\nabla^\perp$ on the [normal bundle](@entry_id:272447) $NM$:
$$
\nabla^\perp_X \xi := (\bar{\nabla}_X \xi)^\perp
$$
Combining these definitions gives the **Weingarten formula**, which is the counterpart to the Gauss formula for normal fields [@problem_id:2997225]:
$$
\bar{\nabla}_X \xi = -S_\xi X + \nabla^\perp_X \xi
$$

The true power of this formalism is revealed when we link the shape operator to the second fundamental form. By considering the derivative of the [orthogonality condition](@entry_id:168905) $\bar{g}(Y, \xi) = 0$ for a tangent field $Y$, we find a profound relationship. Using [metric compatibility](@entry_id:265910) of $\bar{\nabla}$:
$$
0 = X(\bar{g}(Y, \xi)) = \bar{g}(\bar{\nabla}_X Y, \xi) + \bar{g}(Y, \bar{\nabla}_X \xi)
$$
Substituting the Gauss and Weingarten formulas and using orthogonality, this simplifies to:
$$
\bar{g}(B(X,Y), \xi) = \bar{g}(Y, S_\xi X) = g(S_\xi X, Y)
$$
This identity is of paramount importance. It shows that the shape operator $S_\xi$ is the adjoint of the second fundamental form with respect to the metric. Since $B(X,Y)$ is symmetric in $X$ and $Y$, it follows that the [shape operator](@entry_id:264703) $S_\xi$ is a self-adjoint (or symmetric) [linear operator](@entry_id:136520) on the [tangent space](@entry_id:141028) $TM$: $g(S_\xi X, Y) = g(X, S_\xi Y)$ [@problem_id:2997223].

The normal connection $\nabla^\perp$ also has a key property: it is compatible with the metric on the [normal bundle](@entry_id:272447). That is, for any two normal fields $\xi, \eta$, we have $X(\bar{g}(\xi, \eta)) = \bar{g}(\nabla^\perp_X \xi, \eta) + \bar{g}(\xi, \nabla^\perp_X \eta)$ [@problem_id:2997225]. In the special case of a hypersurface (a [submanifold](@entry_id:262388) of codimension one), the [normal bundle](@entry_id:272447) is a one-dimensional line bundle spanned by a local unit [normal vector field](@entry_id:268853) $\nu$. In this case, the [metric compatibility condition](@entry_id:201846) on $\nu$ implies that $\bar{g}(\bar{\nabla}_X \nu, \nu) = 0$. Since $\nabla^\perp_X \nu$ is the projection of $\bar{\nabla}_X \nu$ onto the normal space spanned by $\nu$, this means $\nabla^\perp_X \nu = \bar{g}(\bar{\nabla}_X \nu, \nu)\nu = 0$. Thus, for any hypersurface, the normal connection is flat; the unit normal is always parallel with respect to the normal connection [@problem_id:2997203].

### Coordinate Representations and Calculations

For practical computations, especially for surfaces in $\mathbb{R}^3$, these concepts are expressed in [local coordinates](@entry_id:181200). Let a surface be parametrized by $X(u,v)$. The geometry is encoded in the coefficients of two quadratic forms.
*   The **[first fundamental form](@entry_id:274022)**, $I = E\,du^2 + 2F\,du\,dv + G\,dv^2$, measures lengths and angles on the surface. Its coefficients are $E = \langle X_u, X_u \rangle$, $F = \langle X_u, X_v \rangle$, and $G = \langle X_v, X_v \rangle$.
*   The **[second fundamental form](@entry_id:161454)**, $II = e\,du^2 + 2f\,du\,dv + g\,dv^2$, measures how the surface bends away from its [tangent plane](@entry_id:136914). Its coefficients are the projections of the second derivatives of the [parametrization](@entry_id:272587) onto the unit normal $n$: $e = \langle X_{uu}, n \rangle$, $f = \langle X_{uv}, n \rangle$, and $g = \langle X_{vv}, n \rangle$.

The Weingarten formula $\bar{\nabla}_X n = -S_n X$ (where we've used $\nabla^\perp_X n=0$) can be expressed in these coordinates. The derivatives of the [normal vector](@entry_id:264185), $n_u$ and $n_v$, lie in the [tangent plane](@entry_id:136914) and are therefore [linear combinations](@entry_id:154743) of $X_u$ and $X_v$. By differentiating the [orthogonality relations](@entry_id:145540) $\langle n, X_u \rangle = 0$ and $\langle n, X_v \rangle = 0$, one arrives at the **Weingarten equations**, which relate the derivatives of the normal to the basis vectors and the coefficients $e, f, g$. For example, $\langle n_u, X_u \rangle = -e$ and $\langle n_u, X_v \rangle = -f$.

These equations lead to a direct relationship between the matrix of the shape operator, $S_n$, the matrix of the first fundamental form, $\mathcal{I} = \begin{pmatrix} E  & F \\ F  & G \end{pmatrix}$, and the matrix of the second fundamental form, $\mathcal{II} = \begin{pmatrix} e  & f \\ f  & g \end{pmatrix}$. The matrix of the shape operator, often denoted $W$ or $L$, is given by [@problem_id:2997213, @problem_id:2997194]:
$$
W = \mathcal{I}^{-1} \mathcal{II} = \frac{1}{EG-F^2} \begin{pmatrix} G  & -F \\ -F  & E \end{pmatrix} \begin{pmatrix} e  & f \\ f  & g \end{pmatrix}
$$
The eigenvalues of this matrix are the **principal curvatures** of the surface, and its determinant and trace give the Gaussian and mean curvatures, respectively.

### The Structural Equations of Submanifolds

The Gauss and Weingarten formulas are not just notational conveniences; they are the building blocks for a set of fundamental equations, known as the [structural equations](@entry_id:274644), which relate the curvature of the [submanifold](@entry_id:262388) to the curvature of the ambient space. These equations—the Gauss equation, the Codazzi-Mainardi equation, and the Ricci equation—form the core of [submanifold theory](@entry_id:190701).

#### The Gauss Equation and Intrinsic Curvature

The Gauss equation relates the [intrinsic curvature](@entry_id:161701) of the submanifold $M$ to the ambient curvature and the second fundamental form. It is derived by writing the ambient Riemann tensor $\bar{R}(X,Y)Z$ and substituting the Gauss and Weingarten formulas repeatedly, then isolating the tangential components. For a surface in a flat [ambient space](@entry_id:184743) like $\mathbb{R}^3$, where $\bar{R} \equiv 0$, this procedure leads to a remarkable result for the Riemann curvature tensor $R$ of the surface [@problem_id:2997238]:
$$
\langle R(X,Y)Z, W \rangle = \langle B(X,W), B(Y,Z) \rangle - \langle B(X,Z), B(Y,W) \rangle
$$
In terms of the scalar [second fundamental form](@entry_id:161454) coefficients for an [orthonormal basis](@entry_id:147779) $\{e_1, e_2\}$, this becomes $R_{1212} = eg - f^2$.

The **Gaussian curvature** $K$ of a surface is the [sectional curvature](@entry_id:159738) of its [tangent plane](@entry_id:136914), given by $K = \frac{\langle R(e_1, e_2)e_2, e_1 \rangle}{\langle e_1, e_1 \rangle \langle e_2, e_2 \rangle - \langle e_1, e_2 \rangle^2}$. Combining this with the Gauss equation yields the celebrated formula known as the *Theorema Egregium* of Gauss:
$$
K = \frac{eg - f^2}{EG - F^2} = \det(\mathcal{I}^{-1}\mathcal{II}) = \det(S_n)
$$
This theorem is astonishing because it shows that the Gaussian curvature $K$, a purely [intrinsic property](@entry_id:273674) of the surface that can be measured by an inhabitant living within it, is completely determined by the extrinsic bending of the surface, as captured by the determinant of the [shape operator](@entry_id:264703).

The Gauss equation can be generalized to a surface embedded in an ambient space form of [constant sectional curvature](@entry_id:272200) $\kappa$. In this case, the formula for the Gaussian curvature becomes [@problem_id:2997216]:
$$
K = \kappa + \det(S_n)
$$
For example, for a sphere of radius $R$ in $\mathbb{R}^3$ ($\kappa=0$), the [shape operator](@entry_id:264703) is $S_n(X) = -\frac{1}{R} X$ (for an outward normal), so $\det(S_n) = (-\frac{1}{R})(-\frac{1}{R}) = \frac{1}{R^2}$, giving the familiar result $K = \frac{1}{R^2}$. For a cylinder of radius $R$, the [principal curvatures](@entry_id:270598) are $0$ and $-\frac{1}{R}$, so $\det(S_n)=0$, and its Gaussian curvature is $K=0$.

#### The Ricci Equation and Normal Curvature

Just as the Gauss equation describes the curvature of the [tangent bundle](@entry_id:161294), the Ricci equation describes the curvature of the [normal bundle](@entry_id:272447). The **[normal curvature](@entry_id:270966) tensor** $R^\perp$ is defined analogously to the Riemann tensor, but using the normal connection $\nabla^\perp$. By analyzing the normal projection of the ambient curvature identity $\bar{R}(X,Y)\xi$, one derives the **Ricci equation** [@problem_id:2997187]:
$$
\bar{g}(R^\perp(X,Y)\xi, \eta) = \bar{g}(\bar{R}(X,Y)\xi, \eta) + g([S_\xi, S_\eta]X, Y)
$$
This equation reveals that the curvature of the [normal bundle](@entry_id:272447) has two sources: the restriction of the ambient curvature to the [normal bundle](@entry_id:272447), and the commutator of the shape operators, $[S_\xi, S_\eta] = S_\xi S_\eta - S_\eta S_\xi$. If the shape operators for a basis of normal vectors all commute, the normal connection is flat (provided the ambient space is also flat). The non-commutativity of the shape operators is a direct measure of the "twist" or [holonomy](@entry_id:137051) within the [normal bundle](@entry_id:272447).

### The Second Fundamental Form in Higher Codimension

The concepts we have developed generalize naturally to submanifolds of higher [codimension](@entry_id:273141), i.e., for an immersion $M^n \to \bar{M}^{n+k}$ where $k > 1$. The second fundamental form $B(X,Y)$ is still a vector in the normal space, but the [normal space](@entry_id:154487) is now $k$-dimensional.

To work with $B$ in this context, it is convenient to choose a local [orthonormal frame](@entry_id:189702) $\{\xi_\alpha\}_{\alpha=1}^k$ for the [normal bundle](@entry_id:272447) $\nu(M)$. The vector $B(X,Y)$ can then be decomposed in this basis [@problem_id:2997217]:
$$
B(X,Y) = \sum_{\alpha=1}^k \bar{g}(B(X,Y), \xi_\alpha) \xi_\alpha
$$
This defines a set of $k$ **scalar second fundamental forms** $h^\alpha$, one for each normal [basis vector](@entry_id:199546):
$$
h^\alpha(X,Y) := \bar{g}(B(X,Y), \xi_\alpha)
$$
Each $h^\alpha$ is a [symmetric bilinear form](@entry_id:148281) on the [tangent space](@entry_id:141028), just as the single scalar second fundamental form was for a hypersurface. The vector-valued [second fundamental form](@entry_id:161454) $B$ can be seen as the collection of these scalar forms: $B = \sum_{\alpha=1}^k h^\alpha \otimes \xi_\alpha$.

It is crucial to recognize that this decomposition is not canonical; it depends on the choice of the orthonormal normal frame $\{\xi_\alpha\}$. If we choose a different local [orthonormal frame](@entry_id:189702) $\{\tilde{\xi}_\alpha\}$, related to the first by a smooth, pointwise rotation $R(p) \in \mathrm{SO}(k)$ such that $\tilde{\xi}_\alpha = \sum_\beta R_{\alpha\beta} \xi_\beta$, the corresponding scalar forms $\tilde{h}^\alpha$ will also transform. The transformation rule for their components $h^\alpha_{ij} = h^\alpha(e_i, e_j)$ is given by [@problem_id:2997217]:
$$
\tilde{h}^\alpha_{ij} = \sum_{\beta=1}^k R_{\alpha\beta} h^\beta_{ij}
$$
This shows that the scalar second fundamental forms mix among themselves under rotations of the normal frame. While individual $h^\alpha$s are frame-dependent, the vector-valued object $B$ and [geometric invariants](@entry_id:178611) derived from it (like the [mean curvature vector](@entry_id:199617)) are independent of this choice.