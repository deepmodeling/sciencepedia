## Introduction
In the study of [differential geometry](@entry_id:145818), we seek to understand the structure of smooth manifolds and the relationships between them. While any [smooth map](@entry_id:160364) preserves the local [differentiable structure](@entry_id:273538), this is often too general a notion. To capture more precise geometric relationships, we need to consider specific classes of maps. A central question arises: how can we formalize the idea of one manifold residing inside another, potentially with self-intersections or complex global behavior, while still maintaining a well-behaved local structure? This leads us to the concept of **immersions**, which precisely describe maps that are local embeddings but may have non-trivial global properties.

This article provides a comprehensive exploration of immersions and their images, known as immersed [submanifolds](@entry_id:159439). Across three chapters, you will build a robust understanding of this fundamental topic.
- The **"Principles and Mechanisms"** chapter will introduce the formal definition of an immersion based on the injectivity of its differential, explore methods for verifying the immersion condition, and critically distinguish immersions from embeddings through illustrative examples of self-intersection and [topological pathologies](@entry_id:158838).
- The **"Applications and Interdisciplinary Connections"** chapter will demonstrate the power of immersions, showing how they are used to define the geometry of curves and surfaces, reveal deep connections between topology and geometry, and provide the foundation for advanced concepts in Riemannian geometry, [symplectic geometry](@entry_id:160783), and dynamical systems.
- Finally, the **"Hands-On Practices"** section will offer guided problems to solidify your understanding, moving from basic verification exercises to more nuanced explorations of the properties that define immersions.

We will begin by establishing the core principles of immersions, laying the groundwork for understanding their profound role in modern geometry.

## Principles and Mechanisms

In our study of [smooth manifolds](@entry_id:160799), we are fundamentally interested in the relationships between them, which are captured by [smooth maps](@entry_id:203730). While any [smooth map](@entry_id:160364) preserves the local [differentiable structure](@entry_id:273538), certain classes of maps impose stronger geometric constraints. This chapter focuses on one such class: **immersions**. An immersion is, intuitively, a map that locally behaves like a well-behaved inclusion of one space into another, without any "creasing" or "crushing" of the domain.

### The Definition of an Immersion

Let $M$ and $N$ be smooth manifolds of dimensions $m$ and $n$ respectively, and let $f: M \to N$ be a [smooth map](@entry_id:160364). At any point $p \in M$, the map $f$ induces a [linear transformation](@entry_id:143080) between the [tangent spaces](@entry_id:199137), called the **differential** (or [pushforward](@entry_id:158718)) of $f$ at $p$, denoted by $df_p: T_pM \to T_{f(p)}N$.

A [smooth map](@entry_id:160364) $f: M \to N$ is defined as an **immersion** if its differential $df_p$ is an injective (one-to-one) linear map for every point $p \in M$.

The requirement of an injective differential has a profound and immediate consequence rooted in linear algebra. For a linear map between [finite-dimensional vector spaces](@entry_id:265491) to be injective, the dimension of the domain cannot exceed the dimension of the codomain. Applying this to the differential $df_p$, we arrive at a necessary condition for any immersion to exist:

$\dim(T_pM) \le \dim(T_{f(p)}N)$, which implies $\dim(M) \le \dim(N)$.

If $m > n$, it is impossible for the [linear map](@entry_id:201112) $df_p: T_pM \to T_{f(p)}N$ to be injective, as the kernel must be non-trivial. Therefore, no [smooth map](@entry_id:160364) from a higher-dimensional manifold to a lower-dimensional one can be an immersion. For example, consider a map from a 3-dimensional space to a 2-dimensional one, such as $f: \mathbb{R}^3 \to S^1 \times \mathbb{R}$. Here, $\dim(\mathbb{R}^3) = 3$ and $\dim(S^1 \times \mathbb{R}) = \dim(S^1) + \dim(\mathbb{R}) = 1 + 1 = 2$. Since $3 > 2$, the differential $df_p: T_p\mathbb{R}^3 \to T_{f(p)}(S^1 \times \mathbb{R})$ is a [linear map](@entry_id:201112) from a 3D space to a 2D space and can never be injective. Consequently, no such map can be an immersion [@problem_id:1645241].

### Verifying the Immersion Condition

In practice, we often work in [local coordinates](@entry_id:181200). Let $U \subseteq \mathbb{R}^m$ and $V \subseteq \mathbb{R}^n$ be open sets, and let a map $f: U \to V$ be given by coordinate functions $f(x_1, \dots, x_m) = (y_1, \dots, y_n)$. The differential $df_p$ is represented by the **Jacobian matrix**, an $n \times m$ matrix of [partial derivatives](@entry_id:146280):
$$
(df_p)_{ij} = \frac{\partial y_i}{\partial x_j}(p)
$$
The injectivity of $df_p$ is equivalent to its [matrix representation](@entry_id:143451) having a rank equal to the dimension of the domain, i.e., $\text{rank}(df_p) = m$. Points $p$ where this condition fails are known as **[singular points](@entry_id:266699)** of the map.

#### Immersed Curves

The simplest case is a smooth curve, which is a map $\gamma: I \to \mathbb{R}^n$ from an open interval $I \subset \mathbb{R}$. Here, the domain is 1-dimensional, so the Jacobian is an $n \times 1$ column vector, which is simply the velocity vector $\gamma'(t)$. The immersion condition $\text{rank}(d\gamma_t) = 1$ simplifies to the requirement that the velocity vector $\gamma'(t)$ is never the zero vector for all $t \in I$. A point where $\gamma'(t) = 0$ is a singular point; the curve momentarily "stops" and fails to be an immersion.

For example, consider a family of [helical curves](@entry_id:265354) in $\mathbb{R}^3$ given by $\gamma(t) = (a \cos(t) + b \cos(2t), a \sin(t) + b \sin(2t), ct)$ [@problem_id:1645223]. The velocity vector is $\gamma'(t) = (-a \sin(t) - 2b \sin(2t), a \cos(t) + 2b \cos(2t), c)$. The squared speed is $\|\gamma'(t)\|^2 = (-a \sin(t) - 2b \sin(2t))^2 + (a \cos(t) + 2b \cos(2t))^2 + c^2$. A careful expansion and simplification of the first two terms yields $a^2 + 4b^2 + 4ab \cos(t)$. Thus, $\|\gamma'(t)\|^2 = a^2 + 4b^2 + 4ab \cos(t) + c^2$. For the curve to fail as an immersion, we need $\|\gamma'(t)\|^2 = 0$ for some $t$. If $c \neq 0$, then $c^2 > 0$, and the speed can never be zero. A failure can only occur if $c=0$. In this case, we need $a^2 + 4b^2 + 4ab \cos(t) = 0$. For this equation to have a real solution for $t$, the value of $\cos(t)$ must be in $[-1, 1]$. An analysis reveals this is possible if and only if $a = \pm 2b$. For instance, with parameters $(a=4, b=-2, c=0)$, we have $a = -2b$, and the curve fails to be an immersion.

#### Immersed Surfaces and Higher Dimensions

For a map from a higher-dimensional domain, like a surface parameterized by $\Phi: U \subset \mathbb{R}^2 \to \mathbb{R}^3$, the Jacobian is a $3 \times 2$ matrix. To verify the immersion condition, we must check that its rank is 2 everywhere. This is equivalent to checking that its two column vectors are [linearly independent](@entry_id:148207). A practical way to do this is to check that at least one of the $2 \times 2$ minors of the Jacobian has a non-zero determinant.

Let's examine the map $\Phi(u, v) = (u^3 - 3u, v^3 - 3v, uv)$ [@problem_id:1645244]. Its Jacobian matrix is:
$$
D\Phi(u,v) = \begin{pmatrix} 3u^2 - 3 & 0 \\ 0 & 3v^2 - 3 \\ v & u \end{pmatrix}
$$
The map fails to be an immersion at $(u,v)$ if the rank of this matrix is less than 2, which means both columns are linearly dependent. This occurs if and only if all $2 \times 2$ minors are zero. The three minors are:
1. $M_{12} = (3u^2 - 3)(3v^2 - 3) = 9(u^2-1)(v^2-1)$
2. $M_{13} = u(3u^2 - 3) = 3u(u^2-1)$
3. $M_{23} = -v(3v^2-3) = -3v(v^2-1)$

For all three to be zero, we must have either $u^2=1$ or $v^2=1$. If $u^2=1$, then $M_{12}=0$ and $M_{13}=0$. For $M_{23}$ to be zero, we need either $v=0$ or $v^2=1$. This gives singular points at $(\pm 1, 0)$ and $(\pm 1, \pm 1)$. By symmetry, if $v^2=1$, we get [singular points](@entry_id:266699) at $(0, \pm 1)$ and $(\pm 1, \pm 1)$. The full set of singular points is therefore $(\pm 1, 0), (0, \pm 1), (\pm 1, 1), (\pm 1, -1)$. At all other points in $\mathbb{R}^2$, the map is an immersion.

An important class of immersions comes from the graphs of smooth functions. If $h: U \subset \mathbb{R}^m \to \mathbb{R}^k$ is a smooth function, its graph can be described by the map $F: U \to \mathbb{R}^{m+k}$ given by $F(\mathbf{x}) = (\mathbf{x}, h(\mathbf{x}))$. The Jacobian matrix of $F$ has a distinctive block structure:
$$
dF_\mathbf{x} = \begin{pmatrix} I_m \\ J_h(\mathbf{x}) \end{pmatrix}
$$
where $I_m$ is the $m \times m$ identity matrix and $J_h$ is the $k \times m$ Jacobian of $h$. Because of the identity block on top, the $m$ columns of this matrix are guaranteed to be linearly independent. Therefore, the rank of $dF_\mathbf{x}$ is always $m$, and the graph of any smooth function is always an immersion [@problem_id:1645210]. We can also verify this using the **Gram matrix**, $G = (dF)^T(dF)$. The map is an immersion if and only if $\det(G) \neq 0$. For a graph map, $G = I_m + (J_h)^T J_h$. This matrix is always [positive definite](@entry_id:149459), and its determinant is always strictly positive, providing another confirmation that graph maps are immersions.

### Algebraic Properties of Immersions

Immersions behave predictably under standard operations on maps, which makes them a robust structural concept in differential geometry.

#### Immersions and Local Diffeomorphisms

When the domain and [codomain](@entry_id:139336) have the same dimension ($m=n$), the Jacobian matrix of a map $f: M^m \to N^m$ is a square matrix. In this case, the condition that $df_p$ is injective is equivalent to it being invertible. By the Inverse Function Theorem, an invertible differential at a point $p$ is precisely the condition for $f$ to be a **[local diffeomorphism](@entry_id:203529)** at $p$. Thus, for maps between manifolds of the same dimension, the concepts of immersion and [local diffeomorphism](@entry_id:203529) are identical. For instance, the map $f: \mathbb{R}^2 \to \mathbb{R}^2$ given in complex notation by $f(z) = z^3$ where $z=u+iv$ has a Jacobian determinant equal to $9(u^2+v^2)^2$ [@problem_id:1645238]. This determinant is non-zero everywhere except at the origin $(0,0)$. Consequently, the map is both an immersion and a [local diffeomorphism](@entry_id:203529) on $\mathbb{R}^2 \setminus \{(0,0)\}$.

#### Composition and Products

Immersions are closed under composition. If $f: M \to N$ and $g: N \to P$ are immersions, then their composition $g \circ f: M \to P$ is also an immersion. This follows directly from the [chain rule](@entry_id:147422) for differentials: $d(g \circ f)_p = dg_{f(p)} \circ df_p$. The composition of two injective [linear maps](@entry_id:185132) is itself injective. Since $df_p$ and $dg_{f(p)}$ are injective for all $p$, so is their composition, guaranteeing that $g \circ f$ is an immersion [@problem_id:1645224].

Furthermore, immersions are closed under the formation of product maps. If $f: M \to N$ and $g: P \to Q$ are immersions, then the product map $f \times g: M \times P \to N \times Q$, defined by $(f \times g)(p,q) = (f(p), g(q))$, is always an immersion [@problem_id:1645251]. The [tangent space](@entry_id:141028) of a product manifold is the direct sum of the tangent spaces of its factors, e.g., $T_{(p,q)}(M \times P) \cong T_pM \oplus T_qP$. The differential of the product map acts accordingly:
$$
d(f \times g)_{(p,q)}(v, w) = (df_p(v), dg_q(w)) \quad \text{for } v \in T_pM, w \in T_qP
$$
To check for injectivity, suppose $d(f \times g)_{(p,q)}(v, w) = (0, 0)$. This implies $df_p(v) = 0$ and $dg_q(w) = 0$. Since $f$ and $g$ are immersions, their [differentials](@entry_id:158422) are injective, so we must have $v=0$ and $w=0$. Therefore, $(v,w)=(0,0)$, proving that $d(f \times g)_{(p,q)}$ is injective. This property holds universally, with no additional conditions required on $f$ or $g$.

### Immersed Submanifolds and Embeddings

The image of an immersion $f: M \to N$, denoted $f(M)$, is called an **[immersed submanifold](@entry_id:264923)** of $N$. The **Immersion Theorem** states that for any point $p \in M$, there exist local [coordinate charts](@entry_id:262338) around $p$ and $f(p)$ such that the map $f$ takes the simple form $(x_1, \dots, x_m) \mapsto (x_1, \dots, x_m, 0, \dots, 0)$. This confirms our intuition that an immersion locally "lays down" a copy of the domain manifold inside the [codomain](@entry_id:139336).

However, the global picture can be much more complex. While an immersion is locally injective, it may not be globally injective. This leads to the crucial distinction between an immersion and an **embedding**. A [smooth map](@entry_id:160364) $f: M \to N$ is an embedding if it is an immersion that is also a [homeomorphism](@entry_id:146933) onto its image, $f(M)$ (where the image is given the subspace topology from $N$). Being a [homeomorphism](@entry_id:146933) requires two things:
1. The map $f$ must be injective (one-to-one) on its entire domain.
2. The inverse map $f^{-1}: f(M) \to M$ must be continuous.

An immersion can fail to be an embedding in two fundamental ways.

#### Failure of Global Injectivity: Self-Intersections

An immersion might be locally one-to-one but fail to be globally so, causing its image to intersect itself. A classic example is the parameterization of a Klein bottle in $\mathbb{R}^3$, which can be given by a map $\phi: \mathbb{R}^2 \to \mathbb{R}^3$ [@problem_id:1645240]. While a detailed calculation shows the Jacobian has rank 2 everywhere (so it is an immersion), the map is not injective. For instance, points $(u,v)$ and $(u+2\pi, -v)$ in the domain map to the same point in $\mathbb{R}^3$. This lack of global [injectivity](@entry_id:147722) means the surface must pass through itself.

A simpler example is a curve in the plane, $\gamma: \mathbb{R} \to \mathbb{R}^2$. Even if its velocity is never zero, it can cross its own path. Consider the curve $\gamma(t) = (A \sin(\omega t), B \exp(-t^2/\lambda^2))$ [@problem_id:1645226]. The map is an immersion for positive constants $A, B, \omega, \lambda$. However, the $y$-coordinate is an [even function](@entry_id:164802) of $t$, so $y(t)=y(-t)$ for all $t$. A self-intersection occurs if $x(t_1) = x(t_2)$ and $y(t_1) = y(t_2)$ for $t_1 \neq t_2$. Choosing $t_2 = -t_1$ for some $t_1 \neq 0$ satisfies the $y$-condition. The $x$-condition becomes $A \sin(\omega t_1) = A \sin(-\omega t_1) = -A \sin(\omega t_1)$, which holds if $\sin(\omega t_1) = 0$. This occurs for $t_1 = k\pi/\omega$ for any non-zero integer $k$. Thus, the curve has infinitely many self-intersection points at $\gamma(\pm k\pi/\omega)$, all lying on the $y$-axis. The map is an immersion, but it is not an embedding.

#### Failure of Homeomorphism: Topological Pathologies

More subtly, an immersion can be injective but still fail to be an embedding. This occurs if the topology of the image does not match the topology of the domain. Specifically, the inverse map $f^{-1}: f(M) \to M$ is not continuous.

The quintessential example is the "irrational winding line on a torus" [@problem_id:1645228]. Let the torus be $T^2 = S^1 \times S^1$, and consider the map $\alpha: \mathbb{R} \to T^2$ defined by $\alpha(t) = (e^{it}, e^{i\sqrt{2}t})$.
1.  **Immersion:** The derivative is $\alpha'(t) = (ie^{it}, i\sqrt{2}e^{i\sqrt{2}t})$. Its squared norm is $\| \alpha'(t) \|^2 = |i|^2 + |i\sqrt{2}|^2 = 1+2=3$. Since the derivative is never zero, $\alpha$ is an immersion.
2.  **Injectivity:** The map is injective. If $\alpha(t_1) = \alpha(t_2)$, then $t_1-t_2 = 2\pi k_1$ and $\sqrt{2}(t_1-t_2) = 2\pi k_2$ for integers $k_1, k_2$. This would imply $\sqrt{2} = k_2/k_1$, which is impossible for non-zero integers since $\sqrt{2}$ is irrational. Thus $t_1=t_2$.

Despite being an injective immersion, $\alpha$ is not an embedding. The reason lies in the topology of its image, $\text{Im}(\alpha)$. It is a famous result that because the frequency ratio $\sqrt{2}$ is irrational, the image of $\alpha$ is a **dense** subset of the torus $T^2$. This means the curve winds around the torus, eventually passing arbitrarily close to every single point on it.

The denseness of the image prevents the inverse map $\alpha^{-1}: \text{Im}(\alpha) \to \mathbb{R}$ from being continuous. To see this, consider the point $p_0 = \alpha(0) = (1,1)$ in the image. If $\alpha^{-1}$ were continuous, any sequence of image points $p_n = \alpha(t_n)$ converging to $p_0$ would require the preimages $t_n$ to converge to $t_0 = \alpha^{-1}(p_0) = 0$. However, because the image is dense, we can find a sequence of points $p_n$ that converges to $p_0$ but whose preimages $t_n$ tend to infinity. For example, due to the irrationality of $\sqrt{2}$, it is possible to find a sequence of times $t_n \to \infty$ for which $\alpha(t_n)$ gets arbitrarily close to $\alpha(0)$. Since the preimages $t_n$ do not converge to $0$, the map $\alpha^{-1}$ is not continuous. The topology of the image is more complex than that of the real line it came from; [open intervals](@entry_id:157577) in $\mathbb{R}$ do not necessarily map to open sets in the subspace topology of the image.

In summary, an immersion provides a local model for a [submanifold](@entry_id:262388), but global properties like injectivity and topological compatibility are required to promote it to an embedding, which corresponds to our more intuitive notion of a [submanifold](@entry_id:262388) without self-intersections or strange topological behavior.