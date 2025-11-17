## Introduction
Harmonic maps are a central object of study in [geometric analysis](@entry_id:157700), representing a natural generalization of harmonic functions to the setting of maps between curved spaces. Defined as [critical points](@entry_id:144653) of a geometric energy functional, they represent maps that are "optimal" or least distorting in a certain sense. A fundamental challenge, however, is to understand their behavior. The equation they satisfy—the [harmonic map equation](@entry_id:184475)—is a complex system of [nonlinear partial differential equations](@entry_id:168847). To extract meaningful geometric information, one needs a tool that directly connects the analytical properties of the map to the underlying geometry of the domain and target manifolds.

This is precisely the role of the Bochner formula, a powerful identity that serves as a cornerstone of the field. By relating the Laplacian of the map's energy density to the curvature tensors of the manifolds, the formula transforms the difficult analytical problem into a study of a [differential inequality](@entry_id:137452), making it amenable to powerful techniques like the maximum principle. This article provides a comprehensive exploration of this vital tool. In the first chapter, **"Principles and Mechanisms,"** we will derive the Bochner formula from first principles, starting with the energy of a map and the definition of a [harmonic map](@entry_id:192561). In the second chapter, **"Applications and Interdisciplinary Connections,"** we will witness the formula in action, exploring how it leads to profound [rigidity theorems](@entry_id:198222), proves the existence of [harmonic maps](@entry_id:187821), and explains the structure of their singularities. Finally, **"Hands-On Practices"** will offer a set of guided problems to solidify your understanding of these fundamental concepts.

## Principles and Mechanisms

In this chapter, we delve into the core principles and mechanisms underpinning the theory of [harmonic maps](@entry_id:187821). We will begin by defining the energy of a map, which provides a natural way to quantify its geometric "distortion." We will then use [variational principles](@entry_id:198028) to define [harmonic maps](@entry_id:187821) as the critical points of this energy functional. The central result of the chapter is the Bochner formula, a powerful identity that relates the analytical properties of a harmonic map to the underlying geometry of the domain and target manifolds. Finally, we will explore the profound consequences of this formula, which include fundamental [rigidity theorems](@entry_id:198222) and the basis for powerful analytical estimates.

### Energy Density and the Energy Functional

A [smooth map](@entry_id:160364) $u: (M,g) \to (N,h)$ between two Riemannian manifolds transfers geometric information from the domain $(M,g)$ to the target $(N,h)$. A fundamental question is how to quantify the "stretch" or "distortion" introduced by the map at each point. The natural object that captures this information is the differential of the map, $du$, which at each point $p \in M$ is a [linear map](@entry_id:201112) $du_p: T_pM \to T_{u(p)}N$.

To measure the magnitude of this linear map, we use the metrics $g$ on $M$ and $h$ on $N$. The squared norm of the differential at a point $p$, denoted $|du|_p^2$, is defined by choosing a $g$-[orthonormal basis](@entry_id:147779) $\{e_i\}_{i=1}^m$ for the tangent space $T_pM$ and summing the squared lengths of the images of these basis vectors in $T_{u(p)}N$. Specifically:

$$
|du|^2 = \sum_{i=1}^m h\big(du(e_i), du(e_i)\big)
$$

This quantity, known as the Hilbert-Schmidt norm squared of the differential, is independent of the choice of [orthonormal basis](@entry_id:147779). An alternative and equivalent perspective is to consider the pullback of the metric $h$ by the map $u$, denoted $u^*h$. This is a symmetric 2-tensor on $M$ defined by $(u^*h)(X,Y) = h(du(X), du(Y))$ for any vector fields $X, Y$ on $M$. The squared norm of the differential is then simply the trace of this [pullback](@entry_id:160816) tensor with respect to the domain metric $g$: $|du|^2 = \operatorname{trace}_g(u^*h)$.

From this pointwise measure of distortion, we define the **energy density** of the map $u$ as:

$$
e(u) = \frac{1}{2}|du|^2
$$

The factor of $\frac{1}{2}$ is a standard convention chosen to simplify the resulting Euler-Lagrange equations, which we will encounter shortly. The total **energy** of the map $u$ is then obtained by integrating this density over the entire domain manifold $M$ with respect to its volume measure $d\mu_g$. [@problem_id:3025931]

$$
E(u) = \int_M e(u) \,d\mu_g = \frac{1}{2} \int_M |du|^2 \,d\mu_g
$$

This energy functional, often called the Dirichlet energy, is a central object in geometric analysis. It provides a global measure of the map's smoothness and stretch.

### Harmonic Maps as Critical Points of Energy

Maps that are "optimal" in some sense are often [critical points](@entry_id:144653) of a functional. In our context, we are interested in maps that are [critical points](@entry_id:144653) of the energy functional $E(u)$. To find these, we consider a smooth one-parameter variation of the map $u$, denoted $u_t$, where $u_0 = u$. The variational vector field is given by $V = \frac{d}{dt}\big|_{t=0} u_t$, which is a section of the [pullback](@entry_id:160816) tangent bundle $u^*TN$.

The [first variation](@entry_id:174697) of the energy is the derivative of $E(u_t)$ with respect to $t$ at $t=0$. A standard calculation involving [integration by parts](@entry_id:136350) (or the divergence theorem) on the manifold $M$ reveals that:

$$
\frac{d}{dt}\bigg|_{t=0} E(u_t) = - \int_M \langle \tau(u), V \rangle_h \,d\mu_g
$$

Here, $\tau(u)$ is a vector field along the map $u$ (i.e., a section of $u^*TN$) known as the **[tension field](@entry_id:188540)**. This [first variation](@entry_id:174697) formula shows that the [tension field](@entry_id:188540) is the negative $L^2$-gradient of the energy functional. The [tension field](@entry_id:188540) has an explicit formula in terms of the covariant derivative of the differential, $\nabla du$:

$$
\tau(u) = \operatorname{trace}_g(\nabla du)
$$

A map $u$ is a critical point of the energy functional if the [first variation](@entry_id:174697) is zero for all compactly supported variations $V$. This occurs precisely when the [tension field](@entry_id:188540) vanishes identically. We thus arrive at the definition of a harmonic map. [@problem_id:3025952]

**Definition:** A [smooth map](@entry_id:160364) $u: (M,g) \to (N,h)$ is called a **harmonic map** if its [tension field](@entry_id:188540) is zero everywhere, i.e., $\tau(u) = 0$.

In the simplest case where the target manifold is Euclidean space $(N,h) = (\mathbb{R}^k, \delta)$, where $\delta$ is the standard flat metric, the covariant derivative $\nabla^N$ is just the standard directional derivative. The [tension field](@entry_id:188540) for a map $u = (u^1, \dots, u^k)$ simplifies to the action of the Laplace-Beltrami operator of $(M,g)$ on each component function:

$$
\tau(u)^\alpha = \Delta_M u^\alpha, \quad \text{for } \alpha=1, \dots, k
$$

Therefore, a map into Euclidean space is harmonic if and only if its component functions are harmonic functions on $M$. In this sense, [harmonic maps](@entry_id:187821) are a natural generalization of harmonic functions to the setting of maps between curved manifolds. [@problem_id:3025952, @problem_id:3066151, @problem_id:3066125]

### The Geometric Toolkit: Connections and Curvature

To understand the [tension field](@entry_id:188540) and to proceed with a deeper analysis of [harmonic maps](@entry_id:187821), we must first formalize the tools of differentiation on manifolds.

The **Levi-Civita connection**, denoted $\nabla$, is the canonical way to differentiate [vector fields](@entry_id:161384) on a Riemannian manifold $(M,g)$. It is defined by two fundamental properties: it is **[metric-compatible](@entry_id:160255)**, meaning $\nabla g = 0$, and it is **torsion-free**. The fundamental theorem of Riemannian geometry guarantees that for any Riemannian manifold, there exists a unique connection satisfying these two properties. [@problem_id:3066114]

While the connection allows us to define derivatives, the order of differentiation matters on a curved space. The failure of second covariant derivatives to commute is measured by the **Riemann curvature tensor**. For vector fields $X, Y, Z$ on $M$, it is defined as:

$$
R^M(X,Y)Z = \nabla_X \nabla_Y Z - \nabla_Y \nabla_X Z - \nabla_{[X,Y]}Z
$$

This tensor encodes the [intrinsic curvature](@entry_id:161701) of the manifold. By taking a trace of the Riemann tensor, we obtain a coarser but still crucial measure of curvature, the **Ricci [curvature tensor](@entry_id:181383)**, $\operatorname{Ric}^M$. With the convention for $R^M$ given above, the Ricci tensor is defined by tracing over the first and fourth slots:

$$
\operatorname{Ric}^M(X,Y) = \operatorname{trace} \big(Z \mapsto R^M(Z,X)Y \big) = \sum_{i=1}^m g(R^M(e_i,X)Y, e_i)
$$

where $\{e_i\}$ is a local [orthonormal frame](@entry_id:189702). These curvature tensors of both the domain and target manifolds are the essential ingredients in the Bochner formula. [@problem_id:3066143]

### The Bochner Formula for Harmonic Maps

The central principle connecting the analytic nature of a [harmonic map](@entry_id:192561) to the geometry of the manifolds is the **Bochner formula**. This formula arises from computing the Laplacian of the energy density, $\Delta e(u)$. For a harmonic map, where $\tau(u)=0$, this computation yields a remarkable identity. The calculation involves applying the Laplacian, using the product rule for covariant derivatives, and then applying a commutation formula for second derivatives (a Weitzenböck formula), which is where the curvature terms appear.

The resulting formula, often called the Eells-Sampson Bochner formula, is:
$$
\frac{1}{2}\Delta |du|^2 = |\nabla du|^2 + \sum_{i=1}^m h\big(du(\operatorname{Ric}^M(e_i)), du(e_i)\big) - \sum_{i,j=1}^m h\big(R^N(du(e_i),du(e_j))du(e_i), du(e_j)\big)
$$
where $\{e_i\}$ is a local [orthonormal frame](@entry_id:189702) on $M$, $\operatorname{Ric}^M$ is the Ricci tensor of $M$ (viewed as an endomorphism), and $R^N$ is the Riemann [curvature tensor](@entry_id:181383) of $N$. [@problem_id:3066164]

Let us analyze the geometric meaning of each term on the right-hand side. [@problem_id:3066170]

1.  **$|\nabla du|^2$**: This is the squared norm of the [second covariant derivative](@entry_id:193368) of $u$. As a squared norm, this term is always non-negative, $|\nabla du|^2 \ge 0$. It measures the failure of the differential $du$ to be parallel. A map for which $\nabla du = 0$ is called **[totally geodesic](@entry_id:183906)**; such maps send geodesics to geodesics. Thus, this term quantifies how far the harmonic map $u$ deviates from being [totally geodesic](@entry_id:183906).

2.  **The Domain Curvature Term**: The term $\sum_{i} h(du(\operatorname{Ric}^M e_i), du(e_i))$ couples the Ricci curvature of the domain with the map itself. It arises from the commutation of covariant derivatives acting on $du$, specifically from the $R^M$ part of the Ricci identity. [@problem_id:3066108] If the domain has positive Ricci curvature in directions where the map is stretching, this term will contribute positively to $\Delta e(u)$.

3.  **The Target Curvature Term**: The final term, $-\sum_{i,j} h(R^N(du(e_i),du(e_j))du(e_i), du(e_j))$, involves the full Riemann curvature tensor of the target manifold. It originates from the curvature of the pullback connection on the bundle $u^*TN$, which is identical to the [pullback](@entry_id:160816) of the target's curvature, $R^N$. [@problem_id:3066081] The sign of this term is crucial. The expression $h(R^N(X,Y)X,Y)$ is directly related to the sectional curvature $K_N$ of the plane spanned by $X$ and $Y$. If the target manifold $(N,h)$ has [non-positive sectional curvature](@entry_id:275356) ($K_N \le 0$), then $h(R^N(X,Y)X,Y) \le 0$ for all $X,Y$. Because of the negative sign in the Bochner formula, the overall contribution from the target curvature is non-negative under this condition.

### Consequences: Rigidity and Gradient Estimates

The Bochner formula is not merely a complex identity; it is a powerful machine for translating geometric assumptions into deep analytical results about [harmonic maps](@entry_id:187821). [@problem_id:3066125] Its primary use is in deriving [rigidity theorems](@entry_id:198222) and *a priori* estimates.

Let us consider a [harmonic map](@entry_id:192561) $u: (M,g) \to (N,h)$ where $(M,g)$ is a compact manifold without boundary. Suppose we make two favorable geometric assumptions:
*   The domain $(M,g)$ has non-negative Ricci curvature, $\operatorname{Ric}^M \ge 0$.
*   The target $(N,h)$ has [non-positive sectional curvature](@entry_id:275356), $K_N \le 0$.

Under these assumptions, let's re-examine the Bochner formula:
$$
\frac{1}{2}\Delta |du|^2 = \underbrace{|\nabla du|^2}_{\ge 0} + \underbrace{\sum_{i} h\big(du(\operatorname{Ric}^M e_i), du(e_i)\big)}_{\ge 0 \text{ since } \operatorname{Ric}^M \ge 0} - \underbrace{\sum_{i,j} h\big(R^N(du(e_i),du(e_j))du(e_i), du(e_j)\big)}_{\le 0 \text{ since } K_N \le 0}
$$

The combination of these signs leads to the inequality:
$$
\Delta e(u) = \Delta \left(\frac{1}{2}|du|^2\right) \ge 0
$$

This means that the energy density $e(u)$ is a **[subharmonic](@entry_id:171489) function** on the [compact manifold](@entry_id:158804) $M$. By the [weak maximum principle](@entry_id:191971) (or by integrating over $M$ and using the divergence theorem), a [subharmonic](@entry_id:171489) function on a compact manifold without boundary must be constant. Therefore, $e(u) = C$ for some constant $C \ge 0$.

If $e(u)$ is constant, its Laplacian must be zero, so $\Delta e(u) = 0$. Since the right-hand side of the Bochner formula is a sum of three non-negative terms, their sum can be zero only if each term is individually zero. In particular, we must have $|\nabla du|^2 = 0$, which implies that the map $u$ is [totally geodesic](@entry_id:183906). This is a powerful rigidity result: any [harmonic map](@entry_id:192561) from a compact manifold with non-negative Ricci curvature to a manifold with [non-positive sectional curvature](@entry_id:275356) must be [totally geodesic](@entry_id:183906). [@problem_id:3066151, @problem_id:3066125]

Furthermore, if the Ricci curvature of the domain is strictly positive at some point, $\operatorname{Ric}^M > 0$, then the term $\sum_{i} h(du(\operatorname{Ric}^M e_i), du(e_i))$ can only be zero if $du=0$ at that point. Since the energy density is constant, this forces $du=0$ everywhere, meaning $u$ must be a constant map.

This line of reasoning, known as the **Bochner technique**, is a cornerstone of modern [geometric analysis](@entry_id:157700). While we have focused on rigidity results for compact domains, the same formula serves as the starting point for deriving local [gradient estimates](@entry_id:189587) for [harmonic maps](@entry_id:187821) on complete, [non-compact manifolds](@entry_id:262738), a famous result of S. T. Yau. [@problem_id:3066125] In all its applications, the Bochner formula provides an indispensable bridge between the geometry of spaces and the analysis of maps between them.