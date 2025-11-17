## Introduction
Harmonic maps are a central object of study in [geometric analysis](@entry_id:157700), representing [critical points](@entry_id:144653) of an [energy functional](@entry_id:170311) that measures the "stretching" between two Riemannian manifolds. While the concept is intuitive, a deeper understanding requires powerful analytical machinery to connect the properties of these maps to the underlying geometry of the spaces involved. The Bochner formula for [harmonic maps](@entry_id:187821) provides this crucial link, establishing a profound identity that has become a cornerstone of the field. This article serves as a comprehensive guide to this essential tool. The first chapter, **Principles and Mechanisms**, meticulously derives the formula from first principles, starting with the variational framework of energy and the [tension field](@entry_id:188540), and culminating in the full Bochner-Weitzenböck identity. The second chapter, **Applications and Interdisciplinary Connections**, explores the far-reaching consequences of this formula, from proving the landmark Eells-Sampson [existence theorem](@entry_id:158097) to establishing rigidity results and probing the [topology of manifolds](@entry_id:267834). Finally, the **Hands-On Practices** section provides guided exercises to solidify your understanding by applying the formula in concrete geometric settings. We begin by laying the analytical foundation upon which these powerful applications are built.

## Principles and Mechanisms

In the preceding chapter, we introduced the concept of [harmonic maps](@entry_id:187821) as a natural generalization of geodesics to higher-dimensional domains. These maps represent a state of minimal "stretching" or distortion between two Riemannian manifolds. To move beyond this intuitive picture and into the analytical heart of the theory, we must formalize this notion of minimality and derive the equations that govern such maps. This chapter is dedicated to developing the fundamental principles and mechanisms that form the bedrock of modern [geometric analysis](@entry_id:157700), culminating in the celebrated Bochner formula for [harmonic maps](@entry_id:187821). This formula, a powerful identity relating the map's energy to the curvature of the manifolds, is the engine behind many of the deepest results in the field.

### The Variational Framework: Energy and the Tension Field

The most natural way to quantify the "stretching" of a map $f:(M,g) \to (N,h)$ between Riemannian manifolds is to measure the magnitude of its differential, $df$. At each point $p \in M$, the differential $df_p: T_pM \to T_{f(p)}N$ is a [linear map](@entry_id:201112) between tangent spaces. The metrics $g$ and $h$ induce a natural inner product on this space of linear maps, allowing us to define the squared norm of the differential, denoted $|df|^2$.

For a local $g$-[orthonormal frame](@entry_id:189702) $\{e_i\}_{i=1}^m$ of the [tangent bundle](@entry_id:161294) $TM$, the squared norm is computed by summing the squared lengths of the images of the basis vectors:
$$
|df|^2 = \sum_{i=1}^m h\big(df(e_i), df(e_i)\big)
$$
This quantity is independent of the choice of [orthonormal frame](@entry_id:189702). An equivalent and often useful formulation involves the **[pullback metric](@entry_id:161465)** $f^*h$, a symmetric 2-tensor on $M$ defined by $(f^*h)(X,Y) = h(df(X), df(Y))$ for any [vector fields](@entry_id:161384) $X, Y$ on $M$. The squared norm of the differential is precisely the trace of this [pullback metric](@entry_id:161465) with respect to the domain metric $g$: $|df|^2 = \operatorname{trace}_g(f^*h)$.

We define the **energy density** of the map $f$ as the scalar function $e(f)$ on $M$ given by half this squared norm. The conventional factor of $\frac{1}{2}$ serves to simplify the resulting variational equations.
$$
e(f) := \frac{1}{2}|df|^2 = \frac{1}{2}\operatorname{trace}_g(f^*h)
$$
The total **Dirichlet energy** of the map $f$ is then obtained by integrating this density over the entire domain manifold $M$ with respect to its volume measure $d\mu_g$ [@problem_id:3025931].
$$
E(f) := \int_M e(f) \,d\mu_g = \frac{1}{2}\int_M |df|^2 \,d\mu_g
$$
A map is considered **harmonic** if it is a critical point of this [energy functional](@entry_id:170311) $E(f)$ with respect to suitable variations. To make this precise, consider a smooth one-parameter family of maps $f_t: M \to N$, where $t \in (-\epsilon, \epsilon)$, such that $f_0 = f$. The infinitesimal change of the map at $t=0$ is captured by the **variational vector field** $V \in \Gamma(f^*TN)$, defined by $V(p) = \frac{d}{dt}\big|_{t=0} f_t(p)$. If we require that the variation is compactly supported in the interior of $M$, we ensure that the map is fixed on the boundary (if any) and far away.

The map $f$ is a critical point of the energy if the [first variation](@entry_id:174697) vanishes for all such compactly supported variations: $\frac{d}{dt}\big|_{t=0} E(f_t) = 0$. A fundamental calculation, involving [differentiation under the integral sign](@entry_id:158299) and integration by parts (via the Divergence Theorem), reveals that the [first variation of energy](@entry_id:635793) is given by a simple and elegant formula [@problem_id:3025947]:
$$
\frac{d}{dt}\bigg|_{t=0} E(f_t) = - \int_M \langle \tau(f), V \rangle_h \,d\mu_g
$$
The section $\tau(f) \in \Gamma(f^*TN)$ appearing in this formula is known as the **[tension field](@entry_id:188540)** of the map $f$. The vanishing of the [first variation](@entry_id:174697) for all compactly supported sections $V$ is, by the fundamental lemma of the calculus of variations, equivalent to the vanishing of the [tension field](@entry_id:188540) itself. Therefore, we arrive at the Euler-Lagrange equation for the [energy functional](@entry_id:170311):
$$
f \text{ is harmonic } \iff \tau(f) \equiv 0
$$
The [first variation](@entry_id:174697) formula also gives the [tension field](@entry_id:188540) a powerful geometric interpretation: $\tau(f)$ is the negative **$L^2$-gradient** of the [energy functional](@entry_id:170311) $E$. That is, $\operatorname{grad}_{L^2} E(f) = -\tau(f)$ [@problem_id:3025952]. This perspective frames the search for [harmonic maps](@entry_id:187821) as finding the zeros of a [gradient flow](@entry_id:173722), which is the idea behind the [harmonic map heat flow](@entry_id:200511) method, a key existence technique pioneered by Eells and Sampson.

### The Analytical Structure of the Tension Field

To proceed with a deeper analysis, we need an explicit formula for the [tension field](@entry_id:188540) $\tau(f)$ in terms of [differential operators](@entry_id:275037). This requires the machinery of connections on [vector bundles](@entry_id:159617). The differential $df$ maps vectors in $TM$ to vectors in $TN$. As the base point $p \in M$ varies, the [target space](@entry_id:143180) $T_{f(p)}N$ also varies. The natural geometric object to house the vectors $df(X)$ is the **[pullback bundle](@entry_id:159346)** $f^*TN \to M$. The fiber of this bundle over a point $p \in M$ is precisely the tangent space $T_{f(p)}N$ of the target manifold at the image point $f(p)$ [@problem_id:3025940].

A connection $\nabla^N$ on the tangent bundle $TN$ induces a **[pullback](@entry_id:160816) connection** on $f^*TN$, which we will denote simply by $\nabla$. This connection tells us how to differentiate sections of $f^*TN$ along [vector fields](@entry_id:161384) on $M$. Given a vector field $X \in \Gamma(TM)$ and a section $W \in \Gamma(f^*TN)$, the covariant derivative $\nabla_X W$ is defined by differentiating an arbitrary local extension of $W$ on $N$ in the direction of $df(X)$ using the connection $\nabla^N$.

With this apparatus, we can view the differential $df$ as a section of the tensor product bundle $T^*M \otimes f^*TN$. Its [covariant derivative](@entry_id:152476), $\nabla df$, is a section of $T^*M \otimes T^*M \otimes f^*TN$, often called the **[second fundamental form](@entry_id:161454)** of the map $f$. For vector fields $X, Y \in \Gamma(TM)$, it is defined by the familiar Leibniz rule for a tensor product connection:
$$
(\nabla df)(X,Y) = \nabla_X(df(Y)) - df(\nabla^M_X Y)
$$
where $\nabla^M$ is the Levi-Civita connection on $(M,g)$ [@problem_id:3025940]. The [tension field](@entry_id:188540) $\tau(f)$ is then defined as the trace of this second fundamental form with respect to the metric $g$ [@problem_id:3025952].
$$
\tau(f) := \operatorname{trace}_g(\nabla df) = \sum_{i=1}^m (\nabla df)(e_i, e_i)
$$
where $\{e_i\}$ is any local $g$-[orthonormal frame](@entry_id:189702) for $TM$.

This intrinsic definition reveals the [tension field](@entry_id:188540) as a second-order [differential operator](@entry_id:202628). In the special case where the target manifold is Euclidean space $(N,h) = (\mathbb{R}^k, g_{euc})$, the connection $\nabla^N$ is the standard [directional derivative](@entry_id:143430), and its Christoffel symbols vanish. The expression for the [tension field](@entry_id:188540) then simplifies dramatically. If $f = (f^1, \dots, f^k)$ are the component functions of the map in Cartesian coordinates, the [tension field](@entry_id:188540)'s components are given by the action of the Laplace-Beltrami operator on $M$:
$$
\tau(f)^\alpha = \Delta_M f^\alpha \quad \text{for } \alpha=1, \dots, k
$$
In this case, the [harmonic map equation](@entry_id:184475) $\tau(f)=0$ becomes the familiar system of linear [elliptic partial differential equations](@entry_id:141811) $\Delta_M f^\alpha = 0$ for each component. For a general curved target $N$, the presence of the Christoffel symbols of $h$ makes the [harmonic map equation](@entry_id:184475) a system of *nonlinear* second-order PDEs.

### The Bochner-Weitzenböck Formula for Maps

The [first variation](@entry_id:174697) identifies [harmonic maps](@entry_id:187821). The second variation, which involves studying the Laplacian of the energy density $\Delta e(f)$, is crucial for determining stability and proving regularity. The calculation of $\Delta e(f)$ leads to a celebrated identity known as the **Bochner formula** (or Bochner-Weitzenböck formula) for maps. This formula is a cornerstone of [geometric analysis](@entry_id:157700), as it beautifully intertwines the analytical properties of the map with the geometry of the domain and target manifolds.

The derivation begins with the fundamental identity relating the Laplacian of the squared norm of any section $\sigma$ of a [vector bundle](@entry_id:157593) to the norm of its covariant derivative and the connection Laplacian $\Delta_c \sigma = \operatorname{tr}_g(\nabla^2 \sigma) = -\nabla^*\nabla\sigma$:
$$
\frac{1}{2}\Delta |\sigma|^2 = |\nabla \sigma|^2 + \langle \Delta_c \sigma, \sigma \rangle
$$
Applying this to our section $\sigma = du$ for a map $u: M \to N$, we get:
$$
\frac{1}{2}\Delta |du|^2 = |\nabla du|^2 + \langle \Delta_c du, du \rangle
$$
The problem is now reduced to finding an explicit expression for the connection Laplacian term $\langle \Delta_c du, du \rangle$. This is achieved via a **Weitzenböck formula**, which decomposes the connection Laplacian using the Ricci identity for [commutators](@entry_id:158878) of covariant derivatives. This identity is precisely where curvature enters the picture.

The commutation of covariant derivatives on the bundle $T^*M \otimes u^{-1}TN$ introduces curvature from both the domain $M$ and the target $N$.
1.  **Target Curvature**: The curvature of the pullback connection on $u^*TN$ is directly related to the curvature of $N$. For vector fields $X, Y \in \Gamma(TM)$, the [curvature operator](@entry_id:198006) is given by $R^{u^*TN}(X,Y) = R^N(du(X), du(Y))$, where $R^N$ is the Riemann [curvature tensor](@entry_id:181383) of $(N,h)$ [@problem_id:3025944].
2.  **Domain Curvature**: The connection on the $T^*M$ factor involves the curvature of $M$, and its contribution to the final formula appears in the form of the Ricci tensor, $\operatorname{Ric}^M$.

A detailed calculation, which relies on separating the connection Laplacian $\Delta_c$ from the Hodge Laplacian $\Delta_H$ [@problem_id:3025946], yields the following Weitzenböck identity for the differential $du$:
$$
\Delta_c du = \nabla \tau(u) + du \circ \operatorname{Ric}^M - \mathcal{R}^N(du)
$$
where $\tau(u)$ is the [tension field](@entry_id:188540), $du \circ \operatorname{Ric}^M$ denotes the action of the Ricci tensor of $M$ on the $T^*M$ part of $du$, and $\mathcal{R}^N(du)$ is a term involving the Riemann curvature of $N$. In an [orthonormal frame](@entry_id:189702) $\{e_i\}$, these curvature terms act on a vector $X$ as:
$$
(du \circ \operatorname{Ric}^M)(X) = du(\operatorname{Ric}^M(X))
$$
$$
\mathcal{R}^N(du)(X) = \sum_{j=1}^m R^N(du(e_j), du(X))du(e_j)
$$
Substituting this decomposition of $\Delta_c du$ back into the expression for $\frac{1}{2}\Delta |du|^2$ yields the complete Bochner formula for a [smooth map](@entry_id:160364) $u:(M,g) \to (N,h)$ [@problem_id:3035000] [@problem_id:3033004]:
$$
\frac{1}{2}\Delta |du|^2 = |\nabla du|^2 + \langle \nabla \tau(u), du \rangle + \langle du(\operatorname{Ric}^M(\cdot)), du(\cdot) \rangle_h - \sum_{i,j=1}^m \langle R^N(du(e_i), du(e_j))du(e_j), du(e_i) \rangle_h
$$
This formula is a profound statement about the interplay between analysis and geometry. The left-hand side is analytical (the Laplacian of the energy density), while the right-hand side is a sum of four distinct terms, each with a clear geometric or analytical meaning:
-   $|\nabla du|^2$: The squared norm of the [second fundamental form](@entry_id:161454). This is always non-negative.
-   $\langle \nabla \tau(u), du \rangle$: A term coupling the map to its [tension field](@entry_id:188540).
-   $\langle du(\operatorname{Ric}^M(\cdot)), du(\cdot) \rangle_h$: The contribution from the domain's Ricci curvature.
-   $-\sum_{i,j} \langle R^N(\dots) \rangle$: The contribution from the target's Riemann curvature.

### Interpreting and Applying the Bochner Formula

The power of the Bochner formula lies in its application to [harmonic maps](@entry_id:187821) and its interpretation under various curvature assumptions.

#### The Harmonic Map Case

If the map $f: M \to N$ is harmonic, then by definition its [tension field](@entry_id:188540) $\tau(f)$ is zero. Consequently, the term $\langle \nabla \tau(f), df \rangle$ vanishes, and the Bochner identity simplifies to its most famous form:
$$
\frac{1}{2}\Delta |df|^2 = |\nabla df|^2 + \langle df(\operatorname{Ric}^M(\cdot)), df(\cdot) \rangle_h - \sum_{i,j=1}^m \langle R^N(df(e_i), df(e_j))df(e_j), df(e_i) \rangle_h
$$
This identity is a second-order elliptic [differential inequality](@entry_id:137452) for the energy density $|df|^2$. If the right-hand side is non-negative, which occurs for instance if $\operatorname{Ric}^M \ge 0$ and $N$ has [non-positive sectional curvature](@entry_id:275356), then $\Delta |df|^2 \ge 0$. This means $|df|^2$ is a [subharmonic](@entry_id:171489) function, and by the maximum principle, it must be constant if $M$ is compact. This is the key argument in many foundational theorems.

#### Specialization to Constant Target Curvature

The target curvature term is often cumbersome. However, in the important case where the target manifold $(N,h)$ has **[constant sectional curvature](@entry_id:272200)** $K$, it simplifies beautifully. The identity for such a manifold is
$$
\langle R^{N}(U,V)W,Z\rangle_{h} = K\big(\langle U,W\rangle_{h}\langle V,Z\rangle_{h} - \langle U,Z\rangle_{h}\langle V,W\rangle_{h}\big)
$$
Substituting this into the curvature sum and using the **Gram matrix** of the differential, $G_{ij} = \langle df(e_i), df(e_j) \rangle_h$, the entire term becomes a simple algebraic expression involving the trace and Hilbert-Schmidt norm of $G$ [@problem_id:3025930]:
$$
-\sum_{i,j=1}^m \langle R^N(df(e_i), df(e_j))df(e_j), df(e_i) \rangle_h = K\left((\operatorname{tr}G)^2 - \|G\|_{HS}^2\right)
$$
Since $\operatorname{tr}G = |df|^2$, the Bochner formula for a [harmonic map](@entry_id:192561) into a target of [constant sectional curvature](@entry_id:272200) $K$ becomes:
$$
\frac{1}{2}\Delta |df|^2 = |\nabla df|^2 + \langle df(\operatorname{Ric}^M(\cdot)), df(\cdot) \rangle_h + K\left(|df|^4 - \|G\|_{HS}^2\right)
$$
This explicit form is particularly useful for studying maps into spheres, hyperbolic spaces, and Euclidean spaces.

#### A Note on Conventions

When consulting different textbooks and research papers, one must be vigilant about sign conventions for the Riemann curvature tensor. The convention used throughout this text is
$$
R(X,Y)Z = \nabla_X \nabla_Y Z - \nabla_Y \nabla_X Z - \nabla_{[X,Y]}Z \quad (\text{Convention I})
$$
Another common choice is $R^\#(X,Y)Z = -R(X,Y)Z$ (Convention II). The Bochner formula, being a geometric identity, must remain valid regardless of notational choices. A consequence of this is that the sign of the target curvature term in the final formula depends on the convention used [@problem_id:3025933]. Under Convention I, as derived above, the general target curvature term enters with a negative sign: $-\sum \langle R^N(\dots)\rangle$. If one were to use Convention II for the target curvature, this term would appear with a positive sign: $+\sum \langle R^{\#N}(\dots)\rangle$. Being aware of this dependence is essential for correctly applying results from different sources.

In summary, the Bochner formula is a powerful analytical tool that provides a quantitative link between the energy of a map and the geometry of the spaces it connects. It is the primary mechanism for deriving [a priori estimates](@entry_id:186098), proving regularity, and establishing [existence theorems](@entry_id:261096) for [harmonic maps](@entry_id:187821), making it a central pillar of geometric analysis.