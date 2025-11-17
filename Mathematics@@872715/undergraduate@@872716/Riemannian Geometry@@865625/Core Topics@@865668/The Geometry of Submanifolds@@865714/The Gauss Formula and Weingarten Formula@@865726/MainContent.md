## Introduction
In the study of Riemannian geometry, a central challenge is to understand the geometry of a submanifold, an object living inside a larger [ambient space](@entry_id:184743). This geometry has two facets: its intrinsic properties, which can be measured by an observer confined to the [submanifold](@entry_id:262388), and its extrinsic properties, which describe how it bends and curves within the surrounding space. The fundamental problem is to find a precise mathematical dictionary that translates between these two perspectives. How is the [intrinsic curvature](@entry_id:161701) of a surface, like a sphere, related to the way it sits in three-dimensional space?

This article addresses this question by introducing two of the most powerful tools in differential geometry: the Gauss formula and the Weingarten formula. Together, they provide a complete framework for relating a submanifold's [intrinsic and extrinsic geometry](@entry_id:161677). By systematically decomposing vector derivatives, these equations reveal the deep connections between the [induced metric](@entry_id:160616), the ambient curvature, and the shape of the immersion.

Across the following chapters, you will gain a thorough understanding of this foundational theory. Chapter 1, **Principles and Mechanisms**, will derive the Gauss and Weingarten formulas from first principles, defining the crucial concepts of the second fundamental form and the shape operator. Chapter 2, **Applications and Interdisciplinary Connections**, will demonstrate how these tools are used to compute curvature, leading to profound results like Gauss's *Theorema Egregium*, and explore their role in modern [geometric analysis](@entry_id:157700). Finally, Chapter 3, **Hands-On Practices**, offers a set of guided problems to solidify your computational skills and conceptual understanding.

## Principles and Mechanisms

An isometrically [immersed submanifold](@entry_id:264923) $(M, g)$ inherits its geometric structure from the ambient Riemannian manifold $(\overline{M}, \overline{g})$. While the [induced metric](@entry_id:160616) $g$ captures the intrinsic geometry of $M$—that which can be measured without leaving the submanifold—the way $M$ sits inside $\overline{M}$ gives rise to its [extrinsic geometry](@entry_id:262461). The fundamental tools for relating these two aspects of a submanifold's geometry are the **Gauss formula** and the **Weingarten formula**. These formulas arise from a simple but powerful idea: decomposing the ambient [covariant derivative](@entry_id:152476) of vector fields into components tangent and normal to the submanifold.

### The Gauss Formula: Intrinsic Connection and Extrinsic Curvature

Let $M$ be an $m$-dimensional submanifold isometrically immersed in an $(m+k)$-dimensional Riemannian manifold $(\overline{M}, \overline{g})$. The Levi-Civita connection on the ambient manifold, denoted $\overline{\nabla}$, is a machine for differentiating [vector fields](@entry_id:161384). A natural question arises: if we take two [vector fields](@entry_id:161384), $X$ and $Y$, that are everywhere tangent to $M$, what can we say about the derivative $\overline{\nabla}_X Y$?

In general, the resulting vector field $\overline{\nabla}_X Y$ will not be tangent to $M$. At each point $p \in M$, the vector $(\overline{\nabla}_X Y)_p$ lies in the ambient [tangent space](@entry_id:141028) $T_p \overline{M}$. This space admits an [orthogonal decomposition](@entry_id:148020) $T_p \overline{M} = T_p M \oplus N_p M$, where $T_p M$ is the tangent space to $M$ and $N_p M$ is its orthogonal complement, the normal space. We can therefore decompose $\overline{\nabla}_X Y$ into its tangential and normal parts:
$$ \overline{\nabla}_X Y = (\overline{\nabla}_X Y)^{\top} + (\overline{\nabla}_X Y)^{\perp} $$
where $(\cdot)^{\top}$ denotes the orthogonal projection onto the [tangent bundle](@entry_id:161294) $TM$ and $(\cdot)^{\perp}$ denotes the orthogonal projection onto the [normal bundle](@entry_id:272447) $NM$.

This decomposition defines two fundamental objects. The tangential part is defined as the **[induced connection](@entry_id:635081)** $\nabla$ on $M$:
$$ \nabla_X Y := (\overline{\nabla}_X Y)^{\top} $$
The normal part is defined as the **second fundamental form**, a vector-valued map denoted by $B$ (or $\mathrm{II}$):
$$ B(X,Y) := (\overline{\nabla}_X Y)^{\perp} $$
Substituting these definitions yields the celebrated **Gauss formula** [@problem_id:3042719] [@problem_id:2997218]:
$$ \overline{\nabla}_X Y = \nabla_X Y + B(X,Y) $$

The Gauss formula is more than a mere definition; it contains profound geometric insights.

First, the [induced connection](@entry_id:635081) $\nabla$ is none other than the intrinsic **Levi-Civita connection** of the metric $g$ on $M$ [@problem_id:3071118] [@problem_id:2997218]. To see this, we verify that $\nabla$ is torsion-free and [metric-compatible](@entry_id:160255). Since $\overline{\nabla}$ is torsion-free, $\overline{\nabla}_X Y - \overline{\nabla}_Y X = [X,Y]$. Projecting this identity onto the [tangent bundle](@entry_id:161294) $TM$ gives:
$$ (\overline{\nabla}_X Y - \overline{\nabla}_Y X)^{\top} = ([X,Y])^{\top} $$
$$ \nabla_X Y - \nabla_Y X = [X,Y] $$
The last step holds because the Lie bracket of two [vector fields](@entry_id:161384) tangent to a [submanifold](@entry_id:262388) is also tangent to it. Thus, $\nabla$ is torsion-free. For [metric compatibility](@entry_id:265910), we use the compatibility of $\overline{\nabla}$ with $\overline{g}$:
$$ X(g(Y,Z)) = X(\overline{g}(Y,Z)) = \overline{g}(\overline{\nabla}_X Y, Z) + \overline{g}(Y, \overline{\nabla}_X Z) $$
Substituting the Gauss formula and using the orthogonality of the splitting (e.g., $\overline{g}(B(X,Y), Z) = 0$), we find:
$$ X(g(Y,Z)) = \overline{g}(\nabla_X Y, Z) + \overline{g}(Y, \nabla_X Z) = g(\nabla_X Y, Z) + g(Y, \nabla_X Z) $$
Thus, $\nabla$ is also [metric-compatible](@entry_id:160255). By the Fundamental Theorem of Riemannian Geometry, it is the unique Levi-Civita connection on $(M,g)$. This is a remarkable result: the intrinsic rule for differentiation on a [submanifold](@entry_id:262388) is precisely the tangential part of the ambient rule for differentiation. This implies that the connection $\nabla$ depends only on the [induced metric](@entry_id:160616) $g$, not on the specifics of the immersion beyond $g$ [@problem_id:2997574].

Second, the second fundamental form $B(X,Y)$ measures the failure of $\overline{\nabla}_X Y$ to be tangent to $M$. It is a measure of **extrinsic curvature**—how $M$ bends within $\overline{M}$. If $B(X,Y) = 0$ for all $X, Y$, the [submanifold](@entry_id:262388) is called **[totally geodesic](@entry_id:183906)**. In a [totally geodesic submanifold](@entry_id:191437), any geodesic of the submanifold is also a geodesic of the ambient manifold. Familiar examples include a straight line or a plane in Euclidean space $\mathbb{R}^3$, or a [great circle](@entry_id:268970) on a sphere $S^2$ [@problem_id:2997574].

Crucially, the [second fundamental form](@entry_id:161454) $B$ is a tensor. This means it is a $C^\infty(M)$-[bilinear map](@entry_id:150924) from $\Gamma(TM) \times \Gamma(TM)$ to $\Gamma(NM)$. The linearity in the first argument is straightforward. Linearity in the second argument is more subtle [@problem_id:2997223]:
$$ B(X, fY) = (\overline{\nabla}_X (fY))^{\perp} = ((Xf)Y + f \overline{\nabla}_X Y)^{\perp} = (Xf)Y^{\perp} + f(\overline{\nabla}_X Y)^{\perp} $$
Since $Y$ is a tangent vector field, its normal component $Y^{\perp}$ is zero, which eliminates the first term. This leaves $B(X, fY) = f B(X,Y)$, establishing linearity. Furthermore, $B$ is symmetric in its two arguments:
$$ B(X,Y) - B(Y,X) = (\overline{\nabla}_X Y - \overline{\nabla}_Y X)^{\perp} = ([X,Y])^{\perp} = 0 $$
The symmetry $B(X,Y) = B(Y,X)$ holds for any Riemannian submanifold and relies only on the torsion-freeness of the ambient connection, not its curvature [@problem_id:3071118] [@problem_id:2997223].

To make these concepts concrete, consider the surface $M$ in $\mathbb{R}^3$ given by the graph of $u(x,y) = \frac{1}{2}(\kappa_1 x^2 + \kappa_2 y^2)$. At the origin $p=(0,0,0)$, the tangent plane is the $xy$-plane and the [unit normal vector](@entry_id:178851) is $N=(0,0,1)$. Let the tangent vector fields corresponding to the coordinate directions be $V_1 = \partial_x$ and $V_2 = \partial_y$. A direct computation shows that at $p$, $B(V_1, V_1) = \kappa_1 N$, $B(V_2, V_2) = \kappa_2 N$, and $B(V_1, V_2) = 0$. Using the [bilinearity](@entry_id:146819) of $B$, we can compute the second fundamental form for any linear combination of these basis vectors. For example, for $X=V_1+V_2$ and $Y=V_1+2V_2$, we have:
$$ B(X,Y)|_p = B(V_1+V_2, V_1+2V_2)|_p = B(V_1,V_1) + 2B(V_1,V_2) + B(V_2,V_1) + 2B(V_2,V_2) = (\kappa_1 + 2\kappa_2)N $$
The scalar value $\langle B(X,Y), N \rangle$ at $p$ is therefore $\kappa_1 + 2\kappa_2$, illustrating how $B$ captures the curvature of the graph [@problem_id:2997218].

### The Weingarten Formula: Shape Operator and Normal Connection

Having analyzed the derivative of a tangent field, we now turn to the derivative of a normal field. Let $\xi$ be a vector field in the [normal bundle](@entry_id:272447) $NM$ and $X$ a [tangent vector](@entry_id:264836) field on $M$. The ambient derivative $\overline{\nabla}_X \xi$ can again be decomposed into its tangential and normal parts:
$$ \overline{\nabla}_X \xi = (\overline{\nabla}_X \xi)^{\top} + (\overline{\nabla}_X \xi)^{\perp} $$
This decomposition defines two more fundamental objects. The normal part defines the **normal connection** $\nabla^{\perp}$ on the bundle $NM$:
$$ \nabla^{\perp}_X \xi := (\overline{\nabla}_X \xi)^{\perp} $$
The tangential part defines the **[shape operator](@entry_id:264703)** (or **Weingarten map**) $A_{\xi}$, which is a field of endomorphisms on $TM$. By convention, a minus sign is introduced:
$$ -A_{\xi} X := (\overline{\nabla}_X \xi)^{\top} $$
Combining these gives the **Weingarten formula** [@problem_id:2997225] [@problem_id:3042719]:
$$ \overline{\nabla}_X \xi = -A_{\xi} X + \nabla^{\perp}_X \xi $$

The [shape operator](@entry_id:264703) $A_{\xi}$ and the [second fundamental form](@entry_id:161454) $B$ are intimately related. They can be seen as dual to each other via the metric. By differentiating the identity $\overline{g}(Y, \xi) = 0$ for a tangent field $Y$ and a normal field $\xi$, we obtain:
$$ 0 = X(\overline{g}(Y, \xi)) = \overline{g}(\overline{\nabla}_X Y, \xi) + \overline{g}(Y, \overline{\nabla}_X \xi) $$
Using the Gauss and Weingarten formulas and the orthogonality of the decomposition, this simplifies to the fundamental duality relation [@problem_id:2997225] [@problem_id:2997574]:
$$ \overline{g}(B(X,Y), \xi) = g(A_{\xi} X, Y) $$
Note the common but incorrect identity $\overline{g}(B(X,Y), \xi) = -g(A_{\xi} X, Y)$ differs by a sign, which stems from the definition of the [shape operator](@entry_id:264703) [@problem_id:3071118].

A critical consequence of this duality, combined with the symmetry of $B$, is that the shape operator $A_{\xi}$ is **self-adjoint** (or symmetric) with respect to the metric $g$ [@problem_id:2997223] [@problem_id:2997574]:
$$ g(A_{\xi} X, Y) = \overline{g}(B(X,Y), \xi) = \overline{g}(B(Y,X), \xi) = g(A_{\xi} Y, X) = g(X, A_{\xi} Y) $$
This is a cornerstone of [extrinsic geometry](@entry_id:262461), as it implies that at each point, the linear operator $A_{\xi}$ has real eigenvalues (the **[principal curvatures](@entry_id:270598)**) and an [orthogonal basis](@entry_id:264024) of eigenvectors (the **principal directions**).

The normal connection $\nabla^{\perp}$ defines a way to differentiate [normal vector](@entry_id:264185) fields along tangent directions, producing another [normal vector field](@entry_id:268853). A calculation shows that this connection is compatible with the metric on the [normal bundle](@entry_id:272447) [@problem_id:2997225].

### The Important Case of Hypersurfaces

The theory simplifies elegantly for [hypersurfaces](@entry_id:159491), where the [codimension](@entry_id:273141) is $k=1$. In this case, the [normal bundle](@entry_id:272447) $NM$ is a line bundle. If $M$ is orientable, we can choose a globally defined unit [normal vector field](@entry_id:268853) $N$.

A key simplification arises from differentiating the identity $\overline{g}(N,N)=1$:
$$ 0 = X(\overline{g}(N,N)) = 2\overline{g}(\overline{\nabla}_X N, N) $$
This shows that $\overline{\nabla}_X N$ is always orthogonal to $N$, which means it must be a [tangent vector](@entry_id:264836) field [@problem_id:3071118]. Consequently, its normal component is zero: $\nabla^{\perp}_X N = (\overline{\nabla}_X N)^{\perp} = 0$. The unit normal field is always parallel with respect to the normal connection [@problem_id:2997203].

The Weingarten formula for a hypersurface thus becomes simply:
$$ \overline{\nabla}_X N = -A_N X $$
Here, the [shape operator](@entry_id:264703) is often denoted simply by $S$. The [second fundamental form](@entry_id:161454) also simplifies. Since $B(X,Y)$ is a normal vector, it must be proportional to $N$:
$$ B(X,Y) = h(X,Y)N $$
The map $h$ is a scalar-valued [symmetric bilinear form](@entry_id:148281) called the **scalar [second fundamental form](@entry_id:161454)**. The duality relation now connects $h$ and $S$:
$$ h(X,Y) = \overline{g}(B(X,Y), N) = g(S X, Y) $$
This relation is often used to define the shape operator in the hypersurface setting [@problem_id:2997183].

A classic example is the unit sphere $S^m \subset \mathbb{R}^{m+1}$ with its outward-pointing unit normal $N(p)=p$. The ambient derivative in $\mathbb{R}^{m+1}$ is the standard directional derivative, so for a [tangent vector](@entry_id:264836) field $X$, we have $\overline{\nabla}_X N = X$. This immediately implies $S(X) = -X$ (i.e., $S = -\mathrm{Id}$) and consequently $h(X,Y) = g(-\mathrm{Id}(X), Y) = -g(X,Y)$ [@problem_id:3071118].

To see these concepts in action, consider a hypersurface in $\mathbb{R}^3$ given as the graph of $f(x,y) = \frac{1}{2}(ax^2+2cxy+by^2)$. At the origin, the [shape operator](@entry_id:264703) matrix in the basis $\{\partial_x, \partial_y\}$ is the Hessian of $f$, $\begin{pmatrix} a  & c \\ c  & b \end{pmatrix}$. The scalar second fundamental form entry $h(\partial_x, \partial_y)$ can be computed directly, and is found to be $c$, matching the off-diagonal entry of the [shape operator](@entry_id:264703) matrix as expected from the relation $h(X,Y) = g(SX,Y)$ [@problem_id:2997203]. Similarly, if we are given the matrix of the [shape operator](@entry_id:264703) in an [orthonormal basis](@entry_id:147779), we can use matrix multiplication to compute $h(X,Y)$ for any pair of vectors $X, Y$ [@problem_id:2997183].

### Frames, Components, and a Glimpse Beyond

In the general case of [codimension](@entry_id:273141) $k > 1$, it is often convenient to work with components. By choosing a local [orthonormal frame](@entry_id:189702) $\{e_\alpha\}_{\alpha=1}^k$ for the [normal bundle](@entry_id:272447), we can decompose the vector-valued second fundamental form $B$ into a collection of $k$ scalar-valued second fundamental forms $\{h^\alpha\}_{\alpha=1}^k$ [@problem_id:2997217]:
$$ B(X,Y) = \sum_{\alpha=1}^k h^\alpha(X,Y) e_\alpha \quad \text{where} \quad h^\alpha(X,Y) = \overline{g}(B(X,Y), e_\alpha) $$
Each $h^\alpha$ is a symmetric $(0,2)$-tensor on $M$. It is important to remember that this decomposition depends on the choice of normal frame. If we change the frame by a rotation matrix $R=(R_{\alpha\beta})$, such that $\tilde{e}_\alpha = \sum_\beta R_{\alpha\beta} e_\beta$, the components of the scalar forms transform according to $\tilde{h}^\alpha_{ij} = \sum_\beta R_{\alpha\beta} h^\beta_{ij}$ [@problem_id:2997217].

The Gauss and Weingarten formulas provide the fundamental dictionary for translating between the ambient geometry and the induced geometry of the [submanifold](@entry_id:262388). However, they are only part of the story. A given metric $g$ and [second fundamental form](@entry_id:161454) $B$ on a manifold $M$ can only arise from an [isometric immersion](@entry_id:272242) if they satisfy a set of [integrability conditions](@entry_id:158502). These are the **Gauss-Codazzi-Mainardi equations**.

These equations arise from considering the curvature tensor $\overline{R}$ of the ambient manifold. Decomposing the vector $\overline{R}(X,Y)Z$ (for tangent $X,Y,Z$) into its tangential and normal parts yields two equations:
1.  The **Gauss equation** relates the intrinsic curvature $R$ of $M$ to the ambient curvature $\overline{R}$ and the [second fundamental form](@entry_id:161454) $B$.
2.  The **Codazzi-Mainardi equation** relates the covariant derivative of $B$ to the normal component of the ambient curvature tensor:
    $$ (\tilde{\nabla}_X B)(Y,Z) - (\tilde{\nabla}_Y B)(X,Z) = (\overline{R}(X,Y)Z)^{\perp} $$
where $\tilde{\nabla}$ is the connection induced on the appropriate [tensor bundles](@entry_id:203012). This equation imposes a strong constraint on how the [extrinsic curvature](@entry_id:160405) can vary across the submanifold [@problem_id:2997574]. If the ambient space has [constant curvature](@entry_id:162122) (like Euclidean space or a sphere), then $(\overline{R}(X,Y)Z)^{\perp} = 0$, simplifying the identity. However, for a general ambient manifold, this term is non-zero and plays a crucial role, as can be explicitly calculated for submanifolds of [product spaces](@entry_id:151693) like $S^2(\kappa_1) \times S^2(\kappa_2)$ [@problem_id:2997199].