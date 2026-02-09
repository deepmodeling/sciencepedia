## Introduction
In the landscape of differential geometry, Riemannian submersions stand out as a powerful tool for relating the geometry of a manifold to that of a lower-dimensional one. These maps serve as a geometric refinement of the topological notion of a fiber bundle, providing a precise framework for understanding how a space can be "built" out of a base space and a collection of fibers. The central challenge addressed by this theory is quantifying the exact geometric relationship between the "total space," the "base space," and the fibers, particularly concerning fundamental properties like geodesics and curvature. By imposing a specific compatibility condition between the metrics of the involved manifolds, the theory of Riemannian submersions provides elegant and computable answers.

This article will guide you through the foundational aspects and applications of this essential concept. In the first chapter, **Principles and Mechanisms**, we will establish the core definitions, including the crucial decomposition of tangent spaces into vertical and horizontal components, and introduce O'Neill's tensors, the primary tools for measuring the geometry of a submersion. Following this, the **Applications and Interdisciplinary Connections** chapter will explore canonical examples like the Hopf fibration, demonstrate the computational power of the curvature formulas, and highlight connections to Lie theory and geometric analysis. Finally, the **Hands-On Practices** section will provide you with the opportunity to apply these theoretical insights to concrete problems, solidifying your understanding of how Riemannian submersions work in practice.

## Principles and Mechanisms

In this chapter, we delve into the core principles that govern Riemannian submersions. We will dissect the fundamental geometric structure they impose on a manifold and introduce the primary mechanisms and tools used to analyze their properties. Our exploration will begin with the defining characteristics of a Riemannian submersion, move to the geometric significance of its constituent parts, and culminate in an examination of its profound effect on curvature.

### The Fundamental Decomposition: Vertical and Horizontal Spaces

A smooth map $\pi:(M,g) \to (B,h)$ between two Riemannian manifolds is first and foremost a **smooth submersion**. This is a differential-topological requirement, meaning the differential $d\pi_p: T_pM \to T_{\pi(p)}B$ is a surjective linear map at every point $p \in M$. This condition ensures that the pre-image of any point $b \in B$, called the **fiber** $\pi^{-1}(b)$, is a smooth, regularly embedded submanifold of $M$. The tangent space to this fiber at $p$ is precisely the kernel of the differential, $T_p(\pi^{-1}(\pi(p))) = \ker d\pi_p$. This subspace of $T_pM$ is called the **vertical space**, denoted $\mathcal{V}_p$.

The purely topological structure of a submersion does not, however, imply any relationship between the metrics $g$ and $h$. The defining feature of a **Riemannian submersion** is the introduction of a specific metric compatibility condition. This condition elegantly connects the geometry of the total space $(M,g)$ with that of the base space $(B,h)$.

At each point $p \in M$, the Riemannian metric $g$ provides an inner product on the tangent space $T_pM$. This allows us to define the **horizontal space**, denoted $\mathcal{H}_p$, as the orthogonal complement of the vertical space: $\mathcal{H}_p = (\mathcal{V}_p)^\perp$. This gives a $g$-orthogonal direct sum decomposition of each tangent space: $T_pM = \mathcal{V}_p \oplus \mathcal{H}_p$.

The crucial metric condition for a Riemannian submersion is that the differential $d\pi_p$, when restricted to the horizontal space, must be a linear isometry.

**Definition:** A smooth submersion $\pi:(M,g) \to (B,h)$ is a **Riemannian submersion** if for every $p \in M$, the restriction of its differential to the horizontal space, $d\pi_p|_{\mathcal{H}_p}: \mathcal{H}_p \to T_{\pi(p)}B$, is a linear isometry. This means for all horizontal vectors $X, Y \in \mathcal{H}_p$, the following equality holds:
$$
h_{\pi(p)}(d\pi_p(X), d\pi_p(Y)) = g_p(X, Y)
$$
This condition is a strong constraint. It is not a local isometry on the entire tangent space $T_pM$, as any non-zero vertical vector $V \in \mathcal{V}_p$ has positive length $g_p(V,V) > 0$ but is mapped to the zero vector in $T_{\pi(p)}B$, whose length is $h(0,0)=0$ [@problem_id:3064122].

Furthermore, given a smooth submersion $\pi: (M,g) \to B$, it is not always possible to find a metric $h$ on $B$ that turns $\pi$ into a Riemannian submersion. Conversely, given metrics $g$ on $M$ and $h$ on $B$, a smooth submersion $\pi$ between them may not be Riemannian. The existence of a horizontal distribution with the required isometry property depends on the compatibility of the metrics. For instance, consider the submersion $\pi: (\mathbb{R}^2, g_{euc}) \to (\mathbb{R}, h_c)$ where $\pi(x,y)=x$, $g_{euc}$ is the standard Euclidean metric, and $h_c = c \,dx^2$ for a constant $c>0$. For any potential horizontal vector $X=a\,\partial_x+b\,\partial_y$, the isometry condition requires $g(X,X) = a^2+b^2$ to equal $h_c(d\pi(X), d\pi(X)) = c a^2$. This simplifies to $b^2 = (c-1)a^2$. If $0  c  1$, the right-hand side is negative, which is impossible for a real vector. Thus, for such metrics, no horizontal distribution can satisfy the isometry property, and $\pi$ cannot be a Riemannian submersion [@problem_id:3064145].

The decomposition of the tangent bundle $TM$ into the **vertical distribution** $\mathcal{V}$ and the **horizontal distribution** $\mathcal{H}$ is the foundational structure of a Riemannian submersion. An immediate consequence of this structure is a relationship between the lengths of curves. For any smooth curve $\gamma(t)$ in $M$, its tangent vector $\dot{\gamma}(t)$ can be decomposed into vertical and horizontal components, $\dot{\gamma}(t) = \dot{\gamma}^{\mathcal{V}}(t) + \dot{\gamma}^{\mathcal{H}}(t)$. The differential $d\pi$ annihilates the vertical part, so the velocity of the projected curve $\pi \circ \gamma$ is $d\pi(\dot{\gamma}) = d\pi(\dot{\gamma}^{\mathcal{H}})$. Using the isometry property and orthogonality, we find:
$$
g(\dot{\gamma}, \dot{\gamma}) = g(\dot{\gamma}^{\mathcal{V}}, \dot{\gamma}^{\mathcal{V}}) + g(\dot{\gamma}^{\mathcal{H}}, \dot{\gamma}^{\mathcal{H}}) = \|\dot{\gamma}^{\mathcal{V}}\|_g^2 + h(d\pi(\dot{\gamma}^{\mathcal{H}}), d\pi(\dot{\gamma}^{\mathcal{H}})) = \|\dot{\gamma}^{\mathcal{V}}\|_g^2 + \|d\pi(\dot{\gamma})\|_h^2
$$
This implies that $\|\dot{\gamma}\|_g^2 \ge \|d\pi(\dot{\gamma})\|_h^2$, meaning a Riemannian submersion is distance-decreasing. Equality holds if and only if the vertical component of the velocity vanishes, i.e., if the curve $\gamma$ is everywhere horizontal. Such a curve is called a **horizontal curve** [@problem_id:3064127].

### Foliations, Fields, and Forms

The structure of a Riemannian submersion is intimately related to the theory of foliations. A distribution on a manifold is **integrable** if it is tangent to a family of submanifolds that "slice" or foliate the manifold. By the Frobenius theorem, a distribution is integrable if and only if it is closed under the Lie bracket.

The vertical distribution $\mathcal{V} = \ker d\pi$ is always integrable. To see this, let $V_1, V_2$ be two vertical vector fields. Their defining property is that $d\pi(V_1)=0$ and $d\pi(V_2)=0$. The differential of their Lie bracket is given by $d\pi([V_1, V_2]) = [d\pi(V_1), d\pi(V_2)] = [0,0] = 0$. Thus, $[V_1, V_2]$ is also a vertical vector field. The maximal integral manifolds of this integrable distribution are precisely the fibers of the submersion, $\pi^{-1}(b)$. This structure is called a **foliation by fibers** [@problem_id:3064127] [@problem_id:3064120].

In stark contrast, the horizontal distribution $\mathcal{H}$ is generally **not integrable**. The failure of $\mathcal{H}$ to be closed under the Lie bracket is a crucial feature that encodes geometric information. We will see that this non-integrability is directly responsible for differences in curvature between the total space and the base space. A simple example where $\mathcal{H}$ is integrable is a trivial product manifold $M = B \times F$ with a product metric, where $\pi$ is the projection onto $B$. However, in many fundamental examples, $\mathcal{H}$ is not integrable. For instance, in the **Hopf fibration** $\pi: S^3 \to S^2$, the Lie bracket of two horizontal vector fields can have a non-zero vertical component, demonstrating non-integrability [@problem_id:3064124].

To work with the geometry of the base space from the perspective of the total space, it is useful to identify vector fields and differential forms on $M$ that correspond to objects on $B$.

A vector field $X$ on $M$ is called a **basic vector field** if it is both horizontal and projectable, meaning it is $\pi$-related to a vector field on $B$. That is, there exists a vector field $\bar{X}$ on $B$ such that $d\pi(X) = \bar{X} \circ \pi$. For every vector field $\bar{X}$ on the base $B$, there exists a unique basic vector field $X$ on $M$ that projects to it. This $X$ is called the **horizontal lift** of $\bar{X}$. At each point $p \in M$, $X_p$ is the unique vector in $\mathcal{H}_p$ such that $d\pi_p(X_p) = \bar{X}_{\pi(p)}$. This uniqueness is guaranteed because $d\pi_p|_{\mathcal{H}_p}$ is an isomorphism. This establishes a one-to-one correspondence between vector fields on $B$ and basic vector fields on $M$ [@problem_id:3064104].

Similarly, a differential $k$-form $\alpha$ on $M$ is called a **basic form** if it is the pullback of a form from the base, i.e., $\alpha = \pi^*\beta$ for some unique $k$-form $\beta$ on $B$. Basic forms have a useful intrinsic characterization: a form $\alpha$ is basic if and only if it is horizontal (it vanishes when any of its arguments is a vertical vector, $i_V\alpha=0$) and it is invariant along the fibers (its Lie derivative with respect to any vertical vector field is zero, $\mathcal{L}_V\alpha=0$). Using Cartan's formula, $\mathcal{L}_V\alpha = i_Vd\alpha + d(i_V\alpha)$, this second condition becomes equivalent to $i_V(d\alpha)=0$ for a horizontal form [@problem_id:3064120].

### O'Neill's Tensors: The Tools of Measurement

To quantify the geometric properties of a Riemannian submersion, Barrett O'Neill introduced two fundamental tensors, denoted $T$ and $A$. These tensors capture the interaction between the covariant derivative $\nabla$ of $(M,g)$ and the vertical-horizontal decomposition. They are defined by taking the covariant derivative of two vector fields of a specific type (vertical or horizontal) and projecting the result onto the other distribution [@problem_id:2989132].

The **tensor T** is defined for any two vertical vector fields $U,V$ as:
$$
T_U V = (\nabla_U V)^{\mathcal{H}}
$$
This tensor measures the horizontal component of the acceleration of a curve within a fiber. Geometrically, $T$ is nothing but the **second fundamental form** of the fibers. A fiber is a **totally geodesic** submanifold—meaning any geodesic of the fiber is also a geodesic of the ambient space $M$—if and only if its second fundamental form vanishes identically. Therefore, the fibers of a Riemannian submersion are totally geodesic if and only if $T \equiv 0$ [@problem_id:2989132].

A related concept is that of a minimal submanifold. The **mean curvature vector** of a fiber is the trace of its second fundamental form, $H = \sum_{i} T_{U_i}U_i$, where $\{U_i\}$ is a local orthonormal frame for the vertical space. A fiber is a **minimal submanifold** if and only if its mean curvature vector vanishes, $H=0$ [@problem_id:3064107]. Since being totally geodesic ($T \equiv 0$) implies being minimal ($H=0$), but not vice-versa, we see that fibers can be minimal without being totally geodesic.

The **tensor A** is defined for any two horizontal vector fields $X,Y$ as:
$$
A_X Y = (\nabla_X Y)^{\mathcal{V}}
$$
This tensor measures the vertical component that arises when we take the covariant derivative of one horizontal field with respect to another. It is directly related to the integrability of the horizontal distribution. Using the torsion-free property of the Levi-Civita connection, $[X,Y] = \nabla_X Y - \nabla_Y X$, and projecting onto the vertical distribution, we find:
$$
[X,Y]^{\mathcal{V}} = (\nabla_X Y)^{\mathcal{V}} - (\nabla_Y X)^{\mathcal{V}} = A_X Y - A_Y X
$$
This equation shows that the horizontal distribution $\mathcal{H}$ is integrable (i.e., $[X,Y]^{\mathcal{V}}=0$ for all horizontal $X,Y$) if and only if the tensor $A$ is symmetric. For many applications, $A$ is skew-symmetric, in which case non-integrability is equivalent to $A \not\equiv 0$. The tensor $A$ is thus a direct measure of the "twisting" of the fibers, or the non-integrability of the horizontal distribution [@problem_id:2989132].

### Curvature and the Hopf Fibration

The true power of O'Neill's tensors becomes apparent when we study curvature. A fundamental property of Riemannian submersions is that **horizontal geodesics of the total space project to geodesics of the base space** [@problem_id:3064127] [@problem_id:3064120]. This can be shown using the key formula relating the connection $\nabla$ on $M$ to the connection $\nabla^B$ on $B$. For any basic vector fields $X,Y$ on $M$ lifting $\bar{X}, \bar{Y}$ on $B$, we have:
$$
d\pi((\nabla_X Y)^{\mathcal{H}}) = \nabla^B_{\bar{X}} \bar{Y}
$$
If $\gamma$ is a horizontal geodesic in $M$, its tangent vector field $X=\dot{\gamma}$ satisfies $\nabla_X X = 0$. Since $X$ is horizontal, $(\nabla_X X)^{\mathcal{H}}=0$. Applying the formula, we see that the acceleration of the projected curve $\pi\circ\gamma$ is zero, so it is a geodesic [@problem_id:2989132].

The relationship between the sectional curvatures is given by **O'Neill's curvature formula**. For an orthonormal pair of horizontal vectors $X, Y$ at a point $p \in M$, the sectional curvature $K_B$ of the base space is related to the sectional curvature $K_M$ of the total space by:
$$
K_B(d\pi(X), d\pi(Y)) = K_M(X, Y) + 3\|A_X Y\|_g^2
$$
This formula is remarkable. It shows that the curvature of the base space is the curvature of the horizontal section in the total space *plus* a non-negative term that depends on the non-integrability of the horizontal distribution. The twisting of the fibers, measured by the tensor $A$, always acts to increase the curvature of the base space relative to the total space.

The canonical example illustrating this principle is the **Hopf fibration**, $\pi: S^3 \to S^2$ [@problem_id:3060977]. Here, the total space $S^3$ can be endowed with its standard round metric of constant sectional curvature $K_M = 1$. The base space $S^2$ is given the metric that makes $\pi$ a Riemannian submersion. This induced metric gives $S^2$ a constant sectional curvature of $K_B = 4$. O'Neill's formula perfectly explains this four-fold increase in curvature. For any horizontal orthonormal pair $X,Y$ on $S^3$, the structure of the Lie group $\mathrm{SU}(2) \cong S^3$ dictates that the Lie bracket $[X,Y]$ has a vertical component of length 2. This gives $\|A_XY\|^2 = \|\frac{1}{2}[X,Y]^{\mathcal{V}}\|^2 = 1$. Plugging this into the formula yields:
$$
K_B = K_M + 3\|A_X Y\|^2 = 1 + 3(1) = 4
$$
This demonstrates how the non-trivial fibration structure, with its non-integrable horizontal distribution, enriches the geometry of the base manifold.

### Broader Context: Quotients of Group Actions

A principal source of Riemannian submersions is the quotient of a manifold by an isometric group action. Let a compact Lie group $G$ act smoothly, properly, and isometrically on a Riemannian manifold $(M,g)$.

If the action is **free** (meaning the isotropy group $G_p = \{g \in G \mid g \cdot p = p\}$ is trivial for every point $p$), then the orbit space $M/G$ is a smooth manifold, and the projection map $\pi: M \to M/G$ is a Riemannian submersion when $M/G$ is endowed with the unique quotient metric. The fibers of this submersion are the orbits of the group action.

However, if the action is **not free**, the situation changes dramatically [@problem_id:3064150]. The quotient space $M/G$ is generally not a smooth manifold but a more complex object called an **orbifold** or a stratified space. Points in $M/G$ that correspond to orbits with non-trivial isotropy groups are **singular points**. Near such a point, the local structure of $M/G$ is a cone-like singularity.

A classic example is the action of the circle group $S^1$ on the sphere $S^2$ by rotation about the z-axis. The orbits are circles of latitude, except for the north and south poles, which are fixed points. The isotropy group at the poles is the entire group $S^1$. The quotient space $S^2/S^1$ is homeomorphic to the interval $[-1,1]$, which is a manifold with boundary. The projection map $\pi(x,y,z)=z$ fails to be a submersion at the poles, as its differential vanishes there. Because the target space $M/G$ fails to be a smooth manifold, the global projection $\pi: M \to M/G$ cannot be a Riemannian submersion in the standard sense [@problem_id:3064150]. The theory can be extended to these singular settings, but it marks the boundary of the classical theory of Riemannian submersions and the beginning of the theory of singular Riemannian foliations.