## Introduction
In the study of [differential geometry](@entry_id:145818), a central challenge is to identify "best" or most canonical maps between [curved spaces](@entry_id:204335). The theory of [harmonic maps](@entry_id:187821) offers a powerful and flexible answer, defining such maps not through rigid algebraic rules but through the elegant framework of the [calculus of variations](@entry_id:142234). These maps are critical points of a natural [energy functional](@entry_id:170311), providing a robust way to generalize fundamental concepts like geodesics (maps from a 1D domain) and minimal surfaces (isometric immersions). However, the existence, uniqueness, and regularity of [harmonic maps](@entry_id:187821) are subtle issues, deeply intertwined with the geometry—especially the curvature—of the manifolds involved.

This article provides a comprehensive exploration of the theory of [harmonic maps](@entry_id:187821), structured to guide the reader from first principles to advanced applications. The journey begins in the **"Principles and Mechanisms"** chapter, which lays the theoretical groundwork. Here, we will formally define [harmonic maps](@entry_id:187821) through the Dirichlet energy, derive their Euler-Lagrange equation (the [tension field](@entry_id:188540)), and investigate the profound influence of curvature on their stability and existence, culminating in the celebrated Eells-Sampson theorem. Following this, the **"Applications and Interdisciplinary Connections"** chapter reveals the theory's wide-reaching impact, demonstrating how [harmonic maps](@entry_id:187821) serve as a unifying tool in [complex geometry](@entry_id:159080), topology, the theory of minimal surfaces, and even the study of singular spaces. Finally, a selection of **"Hands-On Practices"** provides an opportunity to solidify these concepts through concrete problem-solving, bridging theoretical understanding with practical application.

## Principles and Mechanisms

This chapter delineates the fundamental principles governing [harmonic maps](@entry_id:187821) between Riemannian manifolds. We will establish the variational nature of [harmonic maps](@entry_id:187821), explore their defining equations and analytical foundations, and investigate the profound role that the curvature of the domain and target manifolds plays in their existence, stability, and regularity.

### The Variational Definition of Harmonic Maps

The theory of [harmonic maps](@entry_id:187821) is rooted in the calculus of variations. The central object is a measure of the total "stretching" of a map between two Riemannian manifolds, known as the Dirichlet energy.

#### The Dirichlet Energy Functional

Let $(M^m, g)$ be a compact, oriented Riemannian manifold of dimension $m$, and let $(N^n, h)$ be a complete Riemannian manifold of dimension $n$. For a [smooth map](@entry_id:160364) $u: M \to N$, its differential $du$ at a point $x \in M$ is a [linear map](@entry_id:201112) $du_x: T_xM \to T_{u(x)}N$. The metrics $g$ on $T_xM$ and $h$ on $T_{u(x)}N$ allow us to measure the magnitude of this differential.

The **energy density** of the map $u$ at a point $x \in M$ is the squared Hilbert-Schmidt norm of its differential, denoted $|du|^2_x$. It is defined as the trace of the [pullback](@entry_id:160816) of the target metric $h$ by $u$, with respect to the domain metric $g$:
$$
e(u)(x) = \frac{1}{2} |du|^2_x = \frac{1}{2} \operatorname{trace}_g(u^*h)(x).
$$
In more concrete terms, if $\{e_i\}_{i=1}^m$ is a $g$-[orthonormal basis](@entry_id:147779) for the [tangent space](@entry_id:141028) $T_xM$, the energy density is given by:
$$
e(u)(x) = \frac{1}{2} \sum_{i=1}^{m} h_{u(x)}(du_x(e_i), du_x(e_i)).
$$
The **Dirichlet energy** $E(u)$ of the map $u$ is the total energy density integrated over the entire domain manifold $M$:
$$
E(u) = \int_M e(u)(x) \, d\text{vol}_g = \frac{1}{2} \int_M |du|^2 \, d\text{vol}_g,
$$
where $d\text{vol}_g$ is the Riemannian [volume element](@entry_id:267802) on $(M,g)$. The [energy functional](@entry_id:170311) $E$ assigns a non-negative real number to each map, quantifying its overall smoothness or "stretching". Maps with lower energy are, in a geometric sense, more "economical".

#### The First Variation and the Tension Field

A **[harmonic map](@entry_id:192561)** is defined as a critical point of the Dirichlet energy functional. To make this precise, we consider a smooth one-parameter variation of a map $u$, denoted by $u_t: M \to N$, such that $u_0 = u$. The variation gives rise to a **variation vector field** $V \in \Gamma(u^*TN)$ along $u$, defined by $V(x) = \frac{d}{dt}\big|_{t=0} u_t(x)$. If $M$ has a boundary $\partial M$, we typically require the variation to be fixed at the boundary, meaning $u_t(x) = u(x)$ for all $x \in \partial M$ and all $t$.

The [first variation](@entry_id:174697) of the energy is the derivative of $E(u_t)$ at $t=0$. A standard calculation using [integration by parts](@entry_id:136350) (the divergence theorem) on manifolds yields:
$$
\frac{d}{dt}\bigg|_{t=0} E(u_t) = - \int_M h(\tau(u), V) \, d\text{vol}_g.
$$
The vector field $\tau(u) \in \Gamma(u^*TN)$ that appears in this formula is called the **[tension field](@entry_id:188540)** of the map $u$. It is the formal Euler-Lagrange operator associated with the energy functional $E$. The [tension field](@entry_id:188540) is intrinsically defined as the trace of the [second covariant derivative](@entry_id:193368) of $u$:
$$
\tau(u) = \operatorname{trace}_g(\nabla du).
$$
Here, $\nabla du$ is the [second covariant derivative](@entry_id:193368) of $u$, which is a section of the tensor bundle $T^*M \otimes T^*M \otimes u^*TN$. It is defined for [vector fields](@entry_id:161384) $X, Y$ on $M$ by $(\nabla du)(X,Y) = \nabla^{u^*TN}_X(du(Y)) - du(\nabla^M_X Y)$, where $\nabla^M$ is the Levi-Civita connection on $M$ and $\nabla^{u^*TN}$ is the connection on the [pullback bundle](@entry_id:159346) $u^*TN$ induced from the Levi-Civita connection $\nabla^N$ on $N$.

For $u$ to be a critical point of the energy, the [first variation](@entry_id:174697) must vanish for all admissible variation fields $V$. From the [first variation](@entry_id:174697) formula, this occurs if and only if the [tension field](@entry_id:188540) vanishes identically. Thus, we have our fundamental definition [@problem_id:2978885]:

**Definition:** A [smooth map](@entry_id:160364) $u: (M,g) \to (N,h)$ is **harmonic** if its [tension field](@entry_id:188540) vanishes, i.e., $\tau(u) = 0$.

#### The Analytical Framework: Sobolev Spaces and Weak Harmonic Maps

For a more robust analytical theory, particularly for proving the existence of [harmonic maps](@entry_id:187821), it is necessary to work with maps of lower regularity. The natural function space for the Dirichlet energy is the Sobolev space of maps with square-integrable first derivatives, denoted $W^{1,2}(M,N)$.

Defining such a space is non-trivial because the target $N$ is a manifold, not a linear space. The standard approach, validated by the Nash Embedding Theorem, is to isometrically embed the target manifold $(N,h)$ into a high-dimensional Euclidean space $\mathbb{R}^K$ [@problem_id:2995331]. We can then define the space $W^{1,2}(M,N)$ as the set of maps $u: M \to \mathbb{R}^K$ that are in the standard Sobolev space $W^{1,2}(M, \mathbb{R}^K)$ and whose image lies in $N$ [almost everywhere](@entry_id:146631):
$$
W^{1,2}(M,N) := \{ u \in W^{1,2}(M, \mathbb{R}^K) \mid u(x) \in N \text{ for a.e. } x \in M \}.
$$
Crucially, this definition of the space, along with the value of the energy functional $E(u)$, is independent of the particular [isometric embedding](@entry_id:152303) chosen [@problem_id:2995331]. This ensures that the theory remains intrinsic to the geometry of $M$ and $N$.

For a map $u \in W^{1,2}(M,N)$, we can no longer assume the existence of a classical [tension field](@entry_id:188540). Instead, we define a **weakly [harmonic map](@entry_id:192561)** through the [variational principle](@entry_id:145218) itself, or equivalently, through a distributional version of the Euler-Lagrange equation. A map $u \in W^{1,2}(M,N)$ is weakly harmonic if it is a critical point of $E$ with respect to variations. This is equivalent to the statement that for every smooth, compactly supported section $\phi$ of the [pullback bundle](@entry_id:159346) $u^*TN$, the following integral identity holds [@problem_id:3034979]:
$$
\int_M \langle du, \nabla \phi \rangle_{g,h} \, d\text{vol}_g = 0.
$$
This equation is the [weak formulation](@entry_id:142897) of $\tau(u)=0$. The energy functional $E$ is well-defined and weakly lower-semicontinuous on $W^{1,2}(M,N)$, properties that are essential for existence proofs via the "direct method" of the calculus of variations [@problem_id:3034979].

### Foundational Examples and Properties

To build intuition, it is useful to examine how the abstract definition of a [harmonic map](@entry_id:192561) manifests in concrete geometric situations.

#### Geodesics as Harmonic Maps

The simplest non-trivial case is when the domain is one-dimensional, such as an interval $I \subset \mathbb{R}$ or a circle $S^1$. Let $M=I$ with the standard metric $g=dt^2$. A map $u: I \to N$ is a curve in $N$. The [tension field](@entry_id:188540) simplifies to $\tau(u) = D_t u'(t)$, where $u'(t)$ is the velocity vector of the curve and $D_t$ is the covariant derivative along the curve. The condition $\tau(u)=0$ is therefore precisely the **geodesic equation**, $D_t u'(t) = 0$. Furthermore, the equation implies that the speed $|u'(t)|_h$ is constant. Thus, in one dimension, [harmonic maps](@entry_id:187821) are simply geodesics parameterized proportionally to arc length [@problem_id:2978885]. This establishes a vital connection: [harmonic maps](@entry_id:187821) are a natural generalization of geodesics to higher-dimensional domains.

#### Minimal Submanifolds as Harmonic Maps

Another fundamental connection arises when the map $u: M \to N$ is an [isometric immersion](@entry_id:272242). In this case, the image $u(M)$ is a submanifold of $N$. The [tension field](@entry_id:188540) of the immersion $u$ is directly related to a classical extrinsic geometric quantity: the **[mean curvature vector](@entry_id:199617)** $H$ of the [submanifold](@entry_id:262388) $u(M)$. The relationship is remarkably simple:
$$
\tau(u) = m H,
$$
where $m = \dim M$. Consequently, an [isometric immersion](@entry_id:272242) is a [harmonic map](@entry_id:192561) ($\tau(u)=0$) if and only if its [mean curvature vector](@entry_id:199617) vanishes ($H=0$). Submanifolds with zero mean curvature are known as **[minimal submanifolds](@entry_id:204492)**. They are [critical points](@entry_id:144653) of the volume functional. Therefore, [harmonic map](@entry_id:192561) theory contains the theory of [minimal submanifolds](@entry_id:204492) as a special case [@problem_id:2978885].

#### Conformal Invariance in Two Dimensions

A special property distinguishes two-dimensional domains. If $\dim M = 2$, the Dirichlet [energy functional](@entry_id:170311) $E(u)$ is invariant under conformal changes of the domain metric $g$. That is, if we replace $g$ with a conformally equivalent metric $\tilde{g} = e^{2\phi}g$ for any smooth function $\phi$ on $M$, the energy remains unchanged: $E_{\tilde{g}}(u) = E_g(u)$. This follows from the scaling laws for the energy density and the volume element, where for $m=2$, the scaling factors $e^{-2\phi}$ and $e^{2\phi}$ exactly cancel. This [conformal invariance](@entry_id:191867) does not hold for domain dimensions $m \ge 3$ [@problem_id:2978885]. This property is of paramount importance in complex analysis, Teichmüller theory, and theoretical physics (where it underpins 2D conformal field theories and string theory).

### The Role of Curvature I: Extrinsic Formulation and Stability

The curvature of the target manifold $N$ exerts a decisive influence on the properties of [harmonic maps](@entry_id:187821). A powerful method for analyzing this influence is to study the map from an extrinsic viewpoint.

#### The Extrinsic Decomposition of the Tension Field

By embedding the target manifold $(N,h)$ isometrically into a Euclidean space $\mathbb{R}^K$, we can relate the intrinsic [tension field](@entry_id:188540) $\tau(u)$ to the standard Laplace-Beltrami operator $\Delta_g u$ applied component-wise to the map $u: M \to \mathbb{R}^K$. The **Gauss formula** provides the link. It decomposes the ambient (flat) connection of $\mathbb{R}^K$ into a part tangent to $N$ (the connection $\nabla^N$) and a part normal to $N$ (the [second fundamental form](@entry_id:161454) $B$ of the embedding $N \hookrightarrow \mathbb{R}^K$).

This leads to a fundamental pointwise decomposition of the ambient Laplacian of the map $u$ [@problem_id:2978888]:
$$
\Delta_g u = \tau(u) + \operatorname{trace}_g(B_u(du,du)).
$$
Here, $\tau(u)$ is the intrinsic [tension field](@entry_id:188540), which is always tangent to $N$. The term $\operatorname{trace}_g(B_u(du,du))$ is the trace of the second fundamental form composed with the differential of $u$, and it is always normal to $N$. This equation thus provides an [orthogonal decomposition](@entry_id:148020) of $\Delta_g u$ into its tangential and normal components.

From this decomposition, we can see that a map $u$ is harmonic ($\tau(u)=0$) if and only if the ambient Laplacian $\Delta_g u$ is everywhere normal to the target manifold $N$ [@problem_id:2978888]. This provides an alternative, often more computable, characterization of [harmonic maps](@entry_id:187821).

For instance, if the target is the unit sphere $S^{n-1} \subset \mathbb{R}^n$, its [second fundamental form](@entry_id:161454) is $B(X,Y) = -h(X,Y)p$, where $p$ is the [position vector](@entry_id:168381) (which is also the unit normal). The trace term becomes $-\left(\sum_i h(du(e_i), du(e_i))\right)u = -|du|^2 u$. The [harmonic map equation](@entry_id:184475) $\tau(u)=0$ is then equivalent to [@problem_id:2978887] [@problem_id:2978888]:
$$
\Delta_g u + |du|^2 u = 0.
$$
Conversely, if the target $N$ is a [totally geodesic submanifold](@entry_id:191437) of $\mathbb{R}^K$ (e.g., an affine subspace), its [second fundamental form](@entry_id:161454) $B$ is zero. In this case, $\Delta_g u = \tau(u)$, and a map into $N$ is harmonic if and only if it is a harmonic function in the ambient Euclidean space, $\Delta_g u = 0$ [@problem_id:2978888].

#### Stability and the Second Variation

Harmonic maps are [critical points](@entry_id:144653) of energy, which can be local minima, maxima, or [saddle points](@entry_id:262327). The stability of a harmonic map is determined by the sign of the second variation of the energy. For a variation with field $V$, the second variation at a harmonic map $u$ defines a [quadratic form](@entry_id:153497):
$$
\frac{d^2}{dt^2}\bigg|_{t=0} E(u_t) = \int_M h(J_u(V), V) \, d\text{vol}_g.
$$
The operator $J_u$ is a self-adjoint, second-order elliptic differential operator called the **Jacobi operator** or [stability operator](@entry_id:191401). A detailed calculation reveals its form [@problem_id:3033060]:
$$
J_u(V) = \nabla^*\nabla V - \operatorname{trace}_g(R^N(V, du(\cdot))du(\cdot)).
$$
Here, $\nabla^*\nabla$ is the rough Laplacian (or Bochner Laplacian) acting on sections of $u^*TN$, and $R^N$ is the Riemann curvature tensor of the target manifold $(N,h)$. The term $\operatorname{trace}_g(R^N(V, du(\cdot))du(\cdot))$ is a zeroth-order term that depends explicitly on the target curvature and the map $u$ itself. A [harmonic map](@entry_id:192561) $u$ is **stable** if the second variation is non-negative for all variations $V$. This corresponds to the Jacobi operator $J_u$ being a non-negative operator.

### The Role of Curvature II: Existence, Uniqueness, and Regularity

The curvature term in the Jacobi operator is not merely a technicality; it is the source of the profound influence of target geometry on the entire theory.

#### The Eells-Sampson Theorem: Non-Positive Target Curvature

A case of exceptional importance is when the target manifold $(N,h)$ has [non-positive sectional curvature](@entry_id:275356) ($\sec_N \le 0$). The term in the Jacobi operator involving the curvature can be expressed in terms of the [sectional curvature](@entry_id:159738) $K_N$ of planes spanned by $V$ and $du(e_i)$. Specifically, $\langle R^N(V, du(e_i))du(e_i), V \rangle = K_N(\text{plane}) \times (\text{non-negative term})$. If $K_N \le 0$, this entire term is non-positive. The curvature term in the second variation, $-\sum_i \langle R^N(\dots) \rangle$, is therefore non-negative.

The [second variation formula](@entry_id:180586) becomes [@problem_id:2995347]:
$$
\frac{d^2}{dt^2}\bigg|_{t=0} E(u_t) = \int_M \left( |\nabla V|^2 - \sum_{i=1}^m \langle R^N(V, du(e_i))du(e_i), V \rangle \right) d\text{vol}_g \ge 0.
$$
This demonstrates that if $\sec_N \le 0$, any harmonic map is stable. In fact, a stronger result holds: the energy functional $E$ is convex along geodesic homotopies in $N$. A fundamental consequence of this convexity is that any critical point must be a global minimizer. Therefore, for a target with [non-positive sectional curvature](@entry_id:275356), **every harmonic map is a global minimizer of the energy within its homotopy class** [@problem_id:3029733]. This is a central part of the celebrated Eells-Sampson theorem, which guarantees the existence of a smooth [harmonic map](@entry_id:192561) in every homotopy class of maps from a compact manifold $M$ to a compact manifold $N$ with $\sec_N \le 0$.

This beautiful result stands in stark contrast to the case of positively curved targets. For instance, the identity map on the sphere $id: S^m \to S^m$ ($m \ge 3$) is harmonic but is known to be unstable—it is a saddle point of the energy, not a minimizer [@problem_id:2978885] [@problem_id:3029733].

#### Convexity and Estimates via the Bochner Formula

The influence of curvature can be further quantified using a **Bochner-type formula**, which computes the Laplacian of the energy density $e(u) = \frac{1}{2}|du|^2$. For a [harmonic map](@entry_id:192561) $u$, the identity is:
$$
\Delta_g e = |\nabla du|^2 + \langle \operatorname{Ric}^M, u^*h \rangle - \sum_{i,j=1}^m \langle R^N(du(e_i), du(e_j))du(e_j), du(e_i) \rangle.
$$
The first term, $|\nabla du|^2$, is non-negative. The second term depends on the Ricci curvature of the domain $M$. The third term depends on the curvature of the target $N$. If $N$ has strictly negative [sectional curvature](@entry_id:159738), say $K^N \le -a^2  0$, then the curvature term from $N$ provides a strictly positive contribution to $\Delta_g e$. For example, if $\operatorname{Ric}^M \ge 0$, we obtain a [differential inequality](@entry_id:137452) of the form [@problem_id:3025938]:
$$
\Delta_g e \ge |\nabla du|^2 + 2a^2 \sum_{1 \le i  j \le m} |du(e_i) \wedge du(e_j)|^2 \ge 0.
$$
This shows that the energy density $e$ is a [subharmonic](@entry_id:171489) function. The maximum principle then implies that $e$ cannot have an interior maximum unless it is constant. Such subharmonicity estimates are powerful tools for proving rigidity, uniqueness, and regularity of [harmonic maps](@entry_id:187821).

#### Positive Curvature and the Formation of Singularities

When the target manifold has [positive sectional curvature](@entry_id:193532), the situation changes dramatically. The Bochner formula shows that the target curvature now contributes a *negative* term to $\Delta_g e$. This term can be interpreted as a potential well that counteracts the diffusive effect of the Laplacian, creating a mechanism for energy to concentrate and form singularities.

A canonical example is the map $u: B_1(0) \subset \mathbb{R}^3 \to S^2$ given by $u(x) = x/|x|$ [@problem_id:3033106]. This map is smooth away from the origin. A direct calculation shows that its energy density is $e(u)(x) = \frac{1}{2}|du|^2 = 1/|x|^2$. The total energy in the unit ball is $E(u) = \int_{B_1} e(u)(x) \, dV = \int_{B_1} \frac{1}{|x|^2} \, dV = 4\pi$, which is finite. Thus, $u$ is in the space $W^{1,2}(B_1, S^2)$. However, $u$ is discontinuous at the origin—it has a point singularity. This map is, in fact, an energy-minimizing [harmonic map](@entry_id:192561) for its boundary values.

The existence of such singular minimizers is deeply tied to dimension. The [energy integral](@entry_id:166228) for a map with density decaying like $|x|^{-2}$ converges near the origin only if the dimension of the domain is $m > 2$. This is why such singularities are characteristic of dimensions $m \ge 3$.

The modern theory of regularity, pioneered by Schoen and Uhlenbeck, provides a precise threshold. The $\varepsilon$-regularity theorem states that a minimizing [harmonic map](@entry_id:192561) is smooth in any region where its scaled energy is sufficiently small. The map $u(x)=x/|x|$ violates this condition at the origin; its scaled energy concentrates to a specific value, $\Theta(0) = \lim_{r \to 0} r^{2-m} E(u,B_r) = 4\pi$ (for $m=3$). The stability of this singularity is a direct consequence of the positive curvature of the target sphere, which allows energy to accumulate rather than disperse [@problem_id:3033106].