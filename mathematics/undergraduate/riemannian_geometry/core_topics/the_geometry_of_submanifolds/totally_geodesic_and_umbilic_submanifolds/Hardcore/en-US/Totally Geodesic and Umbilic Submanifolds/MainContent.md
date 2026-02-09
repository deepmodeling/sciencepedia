## Introduction
In the study of Riemannian geometry, understanding how submanifolds exist within larger, ambient spaces is a central theme. A key challenge lies in distinguishing a submanifold's intrinsic geometry—the properties an observer confined to it would measure—from its extrinsic geometry, which describes how it curves and bends in its surroundings. This article provides a comprehensive introduction to two fundamental classes of submanifolds where this relationship is simplest and most profound: totally geodesic and totally umbilic submanifolds. In "Principles and Mechanisms," we will develop the essential tools, such as the second fundamental form and the shape operator, that quantify extrinsic curvature. The "Applications and Interdisciplinary Connections" section will then showcase the far-reaching importance of these concepts, from foundational examples in space forms to their role in topology and general relativity. Finally, "Hands-On Practices" will guide you through concrete calculations to solidify your understanding. We begin by decomposing the ambient geometry to isolate the principles that govern how a submanifold is embedded.

## Principles and Mechanisms

In our study of a submanifold $(M, g)$ within an ambient Riemannian manifold $(\bar{M}, \bar{g})$, our primary goal is to understand how the geometry of $M$ is influenced by its embedding in $\bar{M}$. The central principle is that the ambient Levi-Civita connection $\bar{\nabla}$ provides a tool to measure how $M$ "bends" or "curves" within its surroundings. By decomposing the action of $\bar{\nabla}$ on vector fields associated with $M$, we can isolate the intrinsic geometric properties of $M$ from its extrinsic properties. This decomposition gives rise to a set of fundamental equations and geometric quantities that form the bedrock of submanifold theory.

### Decomposing the Ambient Connection: The Fundamental Formulas

Let $i: M \hookrightarrow \bar{M}$ be an isometric immersion. This means the metric $g$ on $M$ is induced from the ambient metric $\bar{g}$ via pullback. For any vector fields $X, Y$ tangent to $M$, their inner product is given by $g(X,Y) = \bar{g}(X,Y)$, where we identify $X$ and $Y$ with their images under the differential of the immersion.

At each point $p \in M$, the tangent space of the ambient manifold splits into an orthogonal direct sum of the tangent space to $M$ and its orthogonal complement, the normal space $N_p M$ (or $T_p^\perp M$):
$$
T_p\bar{M} = T_pM \oplus N_pM
$$
This allows us to decompose any vector field $V$ along $M$ into its tangential component $V^\top \in \Gamma(TM)$ and its normal component $V^\perp \in \Gamma(NM)$.

#### The Induced Connection and the Second Fundamental Form

The key insight is to apply this decomposition to the ambient covariant derivative of vector fields tangent to $M$. Let $X$ and $Y$ be smooth vector fields on $M$. While $X$ and $Y$ are tangent to $M$ at every point, their covariant derivative $\bar{\nabla}_X Y$ in the ambient manifold is not, in general, tangent to $M$. The deviation from the tangent space is a direct measure of the extrinsic curvature of $M$.

We decompose $\bar{\nabla}_X Y$ into its tangential and normal components:
$$
\bar{\nabla}_X Y = (\bar{\nabla}_X Y)^\top + (\bar{\nabla}_X Y)^\perp
$$
Each component is given a special name and significance:

1.  The tangential component defines a connection on $M$, which we denote by $\nabla$. That is, $\nabla_X Y := (\bar{\nabla}_X Y)^\top$. A foundational result in Riemannian geometry, sometimes called the **Theorem of Gauss**, states that this induced connection $\nabla$ is precisely the unique Levi-Civita connection of the induced metric $(M, g)$. It is torsion-free and compatible with the metric $g$.

2.  The normal component is a normal-bundle-valued symmetric $(0,2)$-tensor called the **second fundamental form**, denoted $\mathrm{II}$. That is, $\mathrm{II}(X,Y) := (\bar{\nabla}_X Y)^\perp$. This tensor quantifies how $M$ is curving within $\bar{M}$. Its symmetry, $\mathrm{II}(X,Y) = \mathrm{II}(Y,X)$, is a direct consequence of the torsion-free property of the ambient connection $\bar{\nabla}$.

Combining these definitions, we arrive at the **Gauss formula**, one of the most fundamental equations in the theory of submanifolds:
$$
\bar{\nabla}_X Y = \nabla_X Y + \mathrm{II}(X,Y)
$$
This equation beautifully separates the ambient derivative into an intrinsic part (the Levi-Civita connection of $M$) and an extrinsic part (the second fundamental form).

#### The Shape Operator and the Normal Connection

We can perform a similar decomposition for the ambient derivative of a normal vector field. Let $\eta$ be a smooth section of the normal bundle $NM$ and $X$ be a tangent vector field on $M$. The ambient derivative $\bar{\nabla}_X \eta$ can also be decomposed into its tangential and normal parts:
$$
\bar{\nabla}_X \eta = (\bar{\nabla}_X \eta)^\top + (\bar{\nabla}_X \eta)^\perp
$$
These components also have special names:

1.  The tangential component defines the **shape operator** (or **Weingarten map**). For a given normal field $\eta$, the shape operator $S_\eta$ is an endomorphism of the tangent bundle, $S_\eta: \Gamma(TM) \to \Gamma(TM)$, defined by the relation $S_\eta X := -(\bar{\nabla}_X \eta)^\top$. The negative sign is a convention that ensures desirable properties, as we will see.

2.  The normal component defines the **normal connection**, a connection on the normal bundle $NM$, denoted by $\nabla^\perp$. It is defined as $\nabla^\perp_X \eta := (\bar{\nabla}_X \eta)^\perp$. This connection is compatible with the metric $\bar{g}$ restricted to the fibers of the normal bundle.

These definitions yield the **Weingarten equation**:
$$
\bar{\nabla}_X \eta = -S_\eta X + \nabla^\perp_X \eta
$$
The shape operator and the second fundamental form are not independent; they are dual to each other. By differentiating the identity $\bar{g}(Y, \eta) = 0$ for a tangent field $Y$ and normal field $\eta$, one can establish the crucial link:
$$
g(S_\eta X, Y) = \bar{g}(\mathrm{II}(X,Y), \eta)
$$
This identity holds for all tangent fields $X, Y$ and normal fields $\eta$. From this, and the symmetry of $\mathrm{II}$, it immediately follows that the shape operator $S_\eta$ is a self-adjoint operator on the tangent space $T_pM$ for every normal vector $\eta_p \in N_pM$. That is, $g(S_\eta X, Y) = g(X, S_\eta Y)$.

### Special Geometries I: Totally Geodesic Submanifolds

The simplest possible extrinsic geometry a submanifold can have is no extrinsic curvature at all. This special class of submanifolds is fundamental to geometry.

#### Definition and Geometric Intuition

A submanifold $M$ is said to be **totally geodesic** if its second fundamental form vanishes identically, $\mathrm{II} \equiv 0$. This condition has several powerful and equivalent formulations:

-   From the Gauss formula, $\mathrm{II} \equiv 0$ is equivalent to the condition that for any tangent vector fields $X, Y$ on $M$, the ambient derivative $\bar{\nabla}_X Y$ is itself a tangent vector field. In this case, $\bar{\nabla}_X Y = \nabla_X Y$. The ambient connection, when restricted to acting on vector fields of $M$, coincides with the intrinsic connection of $M$.
-   From the duality with the shape operator, $\mathrm{II} \equiv 0$ is equivalent to the condition that the shape operator $S_\eta$ is the zero operator for every normal vector field $\eta$.

Intuitively, a totally geodesic submanifold is one that is "flat" relative to the ambient space. Familiar examples include a straight line or a plane in Euclidean space $\mathbb{R}^3$, and any great sphere $S^k$ inside a larger sphere $S^n$.

#### The Geodesic Property

The name "totally geodesic" is justified by the behavior of geodesics. A curve $\gamma$ in $M$ is a geodesic of $M$ if its acceleration vector with respect to the intrinsic connection vanishes, i.e., $\nabla_{\dot{\gamma}} \dot{\gamma} = 0$. Similarly, it is a geodesic of $\bar{M}$ if $\bar{\nabla}_{\dot{\gamma}} \dot{\gamma} = 0$.

If $M$ is totally geodesic, then for the velocity field $\dot{\gamma}$ of any curve in $M$, we have $\bar{\nabla}_{\dot{\gamma}} \dot{\gamma} = \nabla_{\dot{\gamma}} \dot{\gamma}$. This means that $\nabla_{\dot{\gamma}} \dot{\gamma} = 0$ if and only if $\bar{\nabla}_{\dot{\gamma}} \dot{\gamma} = 0$. Therefore, **a curve in a totally geodesic submanifold is a geodesic of the submanifold if and only if it is a geodesic of the ambient space.**

This property extends further. Consider a geodesic $\gamma$ of the ambient space $\bar{M}$ that starts at a point $p \in M$ with an initial velocity $v \in T_pM$ that is tangent to $M$. Does this geodesic remain within $M$? For a totally geodesic submanifold, the answer is yes. This can be seen by an argument from the uniqueness of solutions to ordinary differential equations. Let $\tilde{\gamma}$ be the unique geodesic of $M$ starting at $p$ with velocity $v$. Since $M$ is totally geodesic, $\tilde{\gamma}$ is also a geodesic of $\bar{M}$. By the uniqueness of geodesics in $\bar{M}$ with given initial data, the ambient geodesic $\gamma$ must coincide with $\tilde{\gamma}$. Since $\tilde{\gamma}$ lies entirely in $M$ by its construction, $\gamma$ must also lie entirely in $M$. This is the sense in which such submanifolds are "totally" geodesic.

### Special Geometries II: Totally Umbilic Submanifolds

After the "flat" case of totally geodesic submanifolds, the next simplest and most symmetric case is that of totally umbilic submanifolds. These are submanifolds whose extrinsic curvature is the same in all directions at a given point.

#### Isotropy of Curvature and the Umbilic Condition

To build intuition, consider a hypersurface $M^{n-1} \subset \bar{M}^n$ with a chosen unit normal vector field $\nu$. The **normal curvature** at a point $p \in M$ in a tangent direction $v \in T_pM$ is the number $k_n(v) = \bar{g}(\mathrm{II}(v,v), \nu)/g(v,v)$. It measures how much the surface bends in the direction of $\nu$.

A point $p$ is called an **umbilic point** if this normal curvature $k_n(v)$ is independent of the direction $v$. If $k_n(v) = k_0$ for all unit vectors $v$, then by polarization, the second fundamental form must be proportional to the metric: $\mathrm{II}_p(X,Y) = k_0 g(X,Y) \nu$.

This idea generalizes to arbitrary codimension. A submanifold $M \subset \bar{M}$ is defined as **totally umbilic** if its second fundamental form is everywhere proportional to the metric tensor. That is, there exists a smooth normal vector field $H$ along $M$ such that for all tangent vector fields $X, Y$:
$$
\mathrm{II}(X,Y) = g(X,Y)H
$$
This vector field $H$ is necessarily the mean curvature vector, as we will see shortly. The archetypal example of a totally umbilic submanifold is a standard sphere $S^n(r)$ in Euclidean space $\mathbb{R}^{n+1}$. A plane is also totally umbilic, being the special case where $H=0$.

#### The Role of the Shape Operator

The umbilic condition has a clean and powerful interpretation in terms of the shape operator. If $M$ is totally umbilic, we can substitute its definition into the duality relation:
$$
g(S_\eta X, Y) = \bar{g}(\mathrm{II}(X,Y), \eta) = \bar{g}(g(X,Y)H, \eta) = g(X,Y) \bar{g}(H, \eta)
$$
Since this holds for all $Y$, we must have $S_\eta X = \bar{g}(H, \eta)X$. This means that for any normal vector $\eta$, the shape operator $S_\eta$ is simply a scalar multiple of the identity operator:
$$
S_\eta = \bar{g}(H, \eta) \mathrm{Id}
$$
This is an equivalent characterization of a totally umbilic submanifold. Since the eigenvalues of the shape operator are the principal curvatures, this implies that for a totally umbilic submanifold, all principal curvatures in any given normal direction are equal. This confirms our intuition that these submanifolds are "isotropic" with respect to their extrinsic curvature.

### Mean Curvature and Minimal Submanifolds

#### The Mean Curvature Vector

For any submanifold, we can average the second fundamental form to define a single vector that captures the "mean" extrinsic curvature at a point. The **mean curvature vector** $H$ is defined as the trace of the second fundamental form with respect to the metric $g$. If $\{e_1, \dots, e_m\}$ is a local orthonormal frame for $TM$, then
$$
H = \frac{1}{m} \sum_{i=1}^m \mathrm{II}(e_i, e_i)
$$
where $m = \dim M$. A submanifold with $H \equiv 0$ is called a **minimal submanifold**. This name arises from the fact that such submanifolds are (locally) critical points for the volume functional.

The mean curvature vector is intimately related to the trace of the shape operators. One can show that for any normal vector field $\xi$, $\text{tr}(S_\xi) = m \bar{g}(H, \xi)$. This implies that a submanifold is minimal if and only if the trace of its shape operator in every normal direction is zero.

#### Distinguishing Minimal, Umbilic, and Totally Geodesic Submanifolds

These concepts are related in a strict hierarchy, and it is crucial to understand the distinctions.

1.  **Totally Geodesic vs. Minimal**: If a submanifold is totally geodesic, then $\mathrm{II} \equiv 0$. It follows directly from the definition of the mean curvature vector that $H \equiv 0$. Thus, every totally geodesic submanifold is minimal. The converse is not true. A minimal submanifold only requires the *trace* of $\mathrm{II}$ to vanish, not the full tensor. The catenoid and helicoid in $\mathbb{R}^3$ are classic examples of minimal surfaces ($H=0$) that are not totally geodesic ($\mathrm{II} \neq 0$).

2.  **Totally Umbilic vs. Minimal**: If a submanifold is totally umbilic, its second fundamental form is given by $\mathrm{II}(X,Y) = g(X,Y)H$. In this special case, the condition $H \equiv 0$ immediately implies that $\mathrm{II}(X,Y)=0$ for all $X,Y$. Therefore, for a totally umbilic submanifold, being minimal is equivalent to being totally geodesic.

3.  **Constant Mean Curvature (CMC) vs. Totally Umbilic**: A surface with constant mean curvature (CMC) is one where $\|H\|$ is constant. This is a much weaker condition than being totally umbilic. The umbilic condition specifies the entire tensor $\mathrm{II}(X,Y) = g(X,Y)H$, whereas the CMC condition only constrains the trace of $\mathrm{II}$. For instance, a right circular cylinder in $\mathbb{R}^3$ has constant mean curvature, but its principal curvatures are $k_1 = 1/R$ and $k_2=0$, so it is not umbilic. More dynamic examples are the non-compact Delaunay surfaces of revolution in $\mathbb{R}^3$ (unduloids and nodoids), which have non-zero constant mean curvature but unequal and non-constant principal curvatures, making them clear counterexamples to the notion that CMC implies umbilic.

### The Gauss Equation: Relating Intrinsic and Extrinsic Curvature

We have seen how the Gauss formula relates the connections $\nabla$ and $\bar{\nabla}$. The culmination of this theory is a formula that relates their respective curvature tensors, $R^M$ and $R^{\bar{M}}$. This result is known as the **Gauss equation**.

#### The Curvature Formula

For any four vector fields $X, Y, Z, W$ tangent to $M$, the Gauss equation relates the intrinsic Riemann curvature tensor of $M$ to the ambient curvature tensor and the second fundamental form:
$$
R^M(X,Y,Z,W) = R^{\bar{M}}(X,Y,Z,W) + \bar{g}(\mathrm{II}(X,W), \mathrm{II}(Y,Z)) - \bar{g}(\mathrm{II}(X,Z), \mathrm{II}(Y,W))
$$
Here, $R^M(X,Y,Z,W) = g(R^M(X,Y)Z, W)$ and $R^{\bar{M}}(X,Y,Z,W) = \bar{g}(\bar{R}(X,Y)Z, W)$ are the $(0,4)$ curvature tensors.

This remarkable equation shows that the intrinsic curvature of a submanifold is not simply the restriction of the ambient curvature. There is an additional contribution that depends quadratically on the second fundamental form. This term represents the contribution of the extrinsic bending of $M$ to its intrinsic curvature. This is a profound generalization of Gauss's Theorema Egregium, which corresponds to the case where $M$ is a surface in $\bar{M}=\mathbb{R}^3$ (where $R^{\bar{M}}=0$).

#### Geometric Consequences

The Gauss equation provides deep insights when applied to our special classes of submanifolds.

-   If $M$ is **totally geodesic**, then $\mathrm{II} \equiv 0$. The extrinsic curvature terms in the Gauss equation vanish, and we are left with:
    $$
    R^M(X,Y,Z,W) = R^{\bar{M}}(X,Y,Z,W)
    $$
    This means the intrinsic curvature of a totally geodesic submanifold is simply the restriction of the ambient curvature tensor to its tangent spaces.

-   If $M$ is **totally umbilic**, so that $\mathrm{II}(X,Y) = g(X,Y)H$, the extrinsic term in the Gauss equation simplifies significantly:
    $$
    \bar{g}(\mathrm{II}(X,W), \mathrm{II}(Y,Z)) - \bar{g}(\mathrm{II}(X,Z), \mathrm{II}(Y,W)) = \|H\|^2 \big( g(X,W)g(Y,Z) - g(X,Z)g(Y,W) \big)
    $$
    The sectional curvature $K_M(\sigma)$ of a plane $\sigma = \text{span}\{X,Y\}$ in $T_pM$ (where $\{X,Y\}$ is an orthonormal basis) is then given by:
    $$
    K_M(\sigma) = K_{\bar{M}}(\sigma) + \|H\|^2
    $$
    This provides a powerful result: if the ambient manifold $\bar{M}$ has constant sectional curvature $C$, then any totally umbilic submanifold $M$ also has constant sectional curvature, equal to $C + \|H\|^2$. For the classic example of a sphere $S^2(r)$ in flat Euclidean space $\mathbb{R}^3$, we have $C=0$ and $\|H\|^2 = (1/r)^2$, yielding the well-known intrinsic sectional curvature of $1/r^2$.