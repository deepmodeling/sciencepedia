## Introduction
To perform calculus on [curved spaces](@entry_id:204335) like manifolds, we must move beyond intuitive geometric notions and establish a rigorous algebraic framework. The concepts of vector spaces and their subspaces, cornerstones of linear algebra, provide this essential foundation. This article addresses the fundamental challenge of defining vectors and their properties intrinsically, without relying on an embedding in a higher-dimensional Euclidean space. By treating vectors as operators on functions, we can build the entire machinery of differential geometry from the ground up. In the following chapters, you will learn how this abstract approach yields powerful tools. "Principles and Mechanisms" establishes the core algebraic definitions, introducing the tangent space as a space of derivations and exploring how subspaces manifest in [submanifolds](@entry_id:159439) and Lie groups. "Applications and Interdisciplinary Connections" demonstrates the utility of these concepts in modeling geometric constraints, physical symmetries, and solutions to differential equations across various scientific fields. Finally, "Hands-On Practices" offers a set of targeted exercises to solidify your understanding of these crucial structures. We begin by constructing the most fundamental object: the tangent space at a single point.

## Principles and Mechanisms

Having introduced the foundational concept of a [smooth manifold](@entry_id:156564), we now turn our attention to the rich algebraic structures that these geometric objects support. At the heart of differential geometry lies the ability to perform calculus on curved spaces. This requires a rigorous notion of vectors, which serve as the basis for defining derivatives, and more complex objects like vector fields and [differential forms](@entry_id:146747). This chapter will establish the algebraic framework of [vector spaces](@entry_id:136837) and subspaces as they manifest on manifolds, moving from the local structure at a single point to global structures defined over the entire manifold.

### The Tangent Space: Vectors as Derivations

In elementary calculus, a tangent vector to a curve in Euclidean space is visualized as an arrow with a specific direction and magnitude. On an abstract manifold, which may not be embedded in a higher-dimensional Euclidean space, this intuitive picture is insufficient. We need an intrinsic definition. The key insight is to define a tangent vector by what it *does*: it measures the rate of change of functions in a particular direction. This operational perspective leads to the algebraic definition of a [tangent vector](@entry_id:264836) as a **derivation**.

A derivation at a point $p$ on a manifold $M$ is a [linear map](@entry_id:201112) $D$ from the ring of smooth real-valued functions on $M$, denoted $C^\infty(M)$, to the real numbers, $D: C^\infty(M) \to \mathbb{R}$. This map must satisfy the **Leibniz rule** (or product rule) for any two functions $f, g \in C^\infty(M)$:
$$D(fg) = f(p)D(g) + g(p)D(f)$$
The set of all such derivations at the point $p$ is called the **tangent space** to $M$ at $p$, and is denoted $T_pM$.

This definition elegantly captures the essence of a [directional derivative](@entry_id:143430). The linearity condition ensures that derivatives behave as expected with sums and scalar multiples of functions. The Leibniz rule is the crucial property that distinguishes derivatives from other [linear maps](@entry_id:185132). Let's demonstrate that this set of derivations naturally forms a vector space.

Let $D_1$ and $D_2$ be two derivations in $T_pM$, and let $c \in \mathbb{R}$ be a scalar.
-   **Addition:** We define their sum $(D_1 + D_2)$ by its action on a function $f$: $(D_1 + D_2)(f) = D_1(f) + D_2(f)$. This sum is clearly linear. Let's check the Leibniz rule:
    \begin{align*}
    (D_1+D_2)(fg) = D_1(fg) + D_2(fg) \\
    = \left( f(p)D_1(g) + g(p)D_1(f) \right) + \left( f(p)D_2(g) + g(p)D_2(f) \right) \\
    = f(p)(D_1(g) + D_2(g)) + g(p)(D_1(f) + D_2(f)) \\
    = f(p)(D_1+D_2)(g) + g(p)(D_1+D_2)(f)
    \end{align*}
    Thus, $D_1 + D_2$ is also a derivation at $p$.
-   **Scalar Multiplication:** We define the scalar multiple $(cD_1)$ by $(cD_1)(f) = cD_1(f)$. This is also linear. Checking the Leibniz rule:
    \begin{align*}
    (cD_1)(fg) = c(D_1(fg)) \\
    = c(f(p)D_1(g) + g(p)D_1(f)) \\
    = f(p)(cD_1(g)) + g(p)(cD_1(f)) \\
    = f(p)(cD_1)(g) + g(p)(cD_1)(f)
    \end{align*}
    Thus, $cD_1$ is also a derivation at $p$.
-   **Zero Vector:** The zero map, which sends every function to $0$, trivially satisfies linearity and the Leibniz rule and serves as the zero vector in $T_pM$.

Since the set of derivations at $p$ is closed under addition and [scalar multiplication](@entry_id:155971) and contains a zero element, $T_pM$ is a real vector space. For an $n$-dimensional manifold, if we introduce a local coordinate system $(x^1, \dots, x^n)$ around $p$, the partial derivative operators $\{\frac{\partial}{\partial x^1}|_p, \dots, \frac{\partial}{\partial x^n}|_p\}$ form a basis for $T_pM$. Consequently, the dimension of the tangent space is equal to the dimension of the manifold: $\dim(T_pM) = n$.

It is instructive to examine operators that fail the Leibniz rule. Consider an operator of the form $L = D_0 + c E_p$, where $D_0$ is a genuine derivation, $E_p$ is the [evaluation map](@entry_id:149774) $E_p(f) = f(p)$, and $c$ is a real constant. Applying $L$ to a product $fg$ gives:
$$L(fg) = D_0(fg) + c E_p(fg) = f(p)D_0(g) + g(p)D_0(f) + c f(p)g(p)$$
The right-hand side of the Leibniz rule for $L$ would be:
$$f(p)L(g) + g(p)L(f) = f(p)(D_0(g) + c g(p)) + g(p)(D_0(f) + c f(p)) = f(p)D_0(g) + g(p)D_0(f) + 2c f(p)g(p)$$
For $L$ to be a derivation, these two expressions must be equal for all functions $f$ and $g$. This requires $c f(p)g(p) = 2c f(p)g(p)$, which simplifies to $c f(p)g(p) = 0$. Since we can always choose functions for which $f(p) \neq 0$ and $g(p) \neq 0$, this equality can only hold universally if $c=0$. This confirms that a [linear operator](@entry_id:136520) is a derivation if and only if it has no "evaluation part". This is a precise way of saying that derivations only care about the infinitesimal behavior of a function at a point, not its actual value there [@problem_id:1688880].

### Vector Subspaces in Geometry

The concept of a [vector subspace](@entry_id:151815)—a subset of a vector space that is itself a vector space under the inherited operations—is ubiquitous in differential geometry. A subset $S$ of a vector space $V$ is a subspace if it contains the zero vector, is closed under [vector addition](@entry_id:155045), and is closed under [scalar multiplication](@entry_id:155971).

A common misconception is that the union of two subspaces is also a subspace. A simple geometric example illustrates why this is not true. Consider the [tangent space](@entry_id:141028) $T_p\mathbb{R}^2$ with basis vectors $\partial_x|_p$ and $\partial_y|_p$. Let $S_1$ be the one-dimensional subspace spanned by $\partial_x|_p$ (the "x-axis" in the [tangent space](@entry_id:141028)) and $S_2$ be the subspace spanned by $\partial_y|_p$ (the "y-axis"). The vector $v_1 = \partial_x|_p$ is in their union $S_1 \cup S_2$, and the vector $v_2 = \partial_y|_p$ is also in $S_1 \cup S_2$. However, their sum, $v_1+v_2 = \partial_x|_p + \partial_y|_p$, is not a scalar multiple of $\partial_x|_p$ nor of $\partial_y|_p$. Therefore, $v_1+v_2$ is not in $S_1 \cup S_2$, violating the [closure under addition](@entry_id:151632) requirement. Thus, the union of subspaces is not, in general, a subspace [@problem_id:1688869].

#### Tangent Spaces of Submanifolds

One of the most important sources of subspaces is the geometry of submanifolds. If $S$ is an $m$-dimensional [submanifold](@entry_id:262388) of an $n$-dimensional manifold $M$ (with $m \le n$), then for any point $p \in S$, the [tangent space](@entry_id:141028) $T_pS$ can be naturally viewed as an $m$-dimensional [vector subspace](@entry_id:151815) of $T_pM$.

Consider a plane $P$ in $\mathbb{R}^3$ defined by $ax+by+cz=d$. This plane is a 2-dimensional [submanifold](@entry_id:262388) of $\mathbb{R}^3$. The tangent space $T_p\mathbb{R}^3$ at any point $p$ can be identified with $\mathbb{R}^3$ itself. A vector $v = (v_x, v_y, v_z) \in T_p\mathbb{R}^3$ is tangent to the plane $P$ if it is orthogonal to the plane's [normal vector](@entry_id:264185) $N = (a, b, c)$. This condition is $N \cdot v = av_x + bv_y + cv_z = 0$. The set of all such vectors $v$ forms the [tangent space](@entry_id:141028) $T_pP$. This set clearly contains the zero vector and is closed under addition and scalar multiplication, making it a 2-dimensional subspace of $T_p\mathbb{R}^3$ [@problem_id:1688853].

Another canonical example is the unit circle $S^1$ as a [submanifold](@entry_id:262388) of the plane $\mathbb{R}^2$. At any point $p = (\cos\theta, \sin\theta)$ on the circle, the tangent space $T_pS^1$ is the 1-dimensional line passing through the origin of the [tangent plane](@entry_id:136914) and perpendicular to the position vector of $p$. A basis for this subspace is given by the velocity vector of a curve parameterizing the circle, such as $v_p = (-\sin\theta, \cos\theta)$. This is a 1-dimensional subspace of $T_p\mathbb{R}^2 \cong \mathbb{R}^2$. The formal map that embeds $T_pS^1$ into $T_p\mathbb{R}^2$ is the **[pushforward](@entry_id:158718)** of the inclusion map $i: S^1 \to \mathbb{R}^2$, which confirms that the image of $T_pS^1$ is precisely this 1-dimensional subspace [@problem_id:1688875].

#### Tangent Spaces to Lie Groups

Matrix Lie groups, such as the [special linear group](@entry_id:139538) $SL(n, \mathbb{R})$ of $n \times n$ matrices with determinant 1, are manifolds whose elements are matrices. The ambient space is the vector space of all $n \times n$ real matrices, $M_n(\mathbb{R})$. The tangent space to $SL(n, \mathbb{R})$ at the identity matrix $I$ is a [vector subspace](@entry_id:151815) of $M_n(\mathbb{R})$. A matrix $X \in M_n(\mathbb{R})$ is in this tangent space, denoted $T_I SL(n, \mathbb{R})$, if it is the velocity vector $C'(0)$ of a smooth curve $C(t)$ in $SL(n, \mathbb{R})$ with $C(0)=I$.

The condition $C(t) \in SL(n, \mathbb{R})$ means $\det(C(t)) = 1$ for all $t$. Differentiating this with respect to $t$ and evaluating at $t=0$ gives a condition on $X$. Using Jacobi's formula for the derivative of a determinant,
$$ \frac{d}{dt}\det(C(t)) = \det(C(t)) \text{tr}\left(C(t)^{-1} C'(t)\right) $$
At $t=0$, this becomes:
$$ 0 = \det(I) \text{tr}\left(I^{-1} C'(0)\right) = 1 \cdot \text{tr}(X) $$
Thus, any tangent vector to $SL(n, \mathbb{R})$ at the identity must be a traceless matrix. Conversely, any traceless matrix can be shown to be such a tangent vector. The set of all traceless $n \times n$ matrices, denoted $\mathfrak{sl}(n, \mathbb{R})$, is easily shown to be a [vector subspace](@entry_id:151815) of $M_n(\mathbb{R})$. Therefore, $T_I SL(n, \mathbb{R}) = \mathfrak{sl}(n, \mathbb{R})$ [@problem_id:1688856].

### Vector Spaces of Fields

We can generalize from vectors at a single point to fields defined over the entire manifold. A **smooth vector field** $X$ on a manifold $M$ is a smooth assignment of a [tangent vector](@entry_id:264836) $X_p \in T_pM$ to each point $p \in M$. The set of all smooth [vector fields](@entry_id:161384) on $M$ is denoted $\mathfrak{X}(M)$. This set forms an infinite-dimensional vector space over $\mathbb{R}$, with addition and scalar multiplication defined pointwise:
$$ (X+Y)_p = X_p + Y_p \quad \text{and} \quad (cX)_p = cX_p $$

Within this vast space, many geometrically significant subsets form vector subspaces.

-   **Constant Vector Fields:** On $\mathbb{R}^n$, a constant vector field is one that assigns the same vector $\vec{c} \in \mathbb{R}^n$ to every point. The set $\mathcal{C}_n$ of all constant vector fields is a subspace of $\mathfrak{X}(\mathbb{R}^n)$. An isomorphism exists between $\mathcal{C}_n$ and $\mathbb{R}^n$ itself, as each constant field is uniquely determined by its constant vector value. If $\{e_1, \dots, e_n\}$ is the standard basis for $\mathbb{R}^n$, then the constant [vector fields](@entry_id:161384) $\{E_1, \dots, E_n\}$ where $E_i(p) = e_i$ for all $p$ form a basis for $\mathcal{C}_n$. Thus, the dimension of this subspace is $n$ [@problem_id:1688886].

-   **Killing Vector Fields:** A Killing vector field on a Riemannian manifold $(M, g)$ is a vector field $X$ that preserves the metric tensor $g$ under the flow it generates. This corresponds to an [infinitesimal isometry](@entry_id:634668) (a symmetry) of the space. The mathematical condition is that the Lie derivative of the metric with respect to $X$ is zero: $L_X g = 0$. The Lie derivative operator $X \mapsto L_X g$ is a [linear map](@entry_id:201112) from $\mathfrak{X}(M)$ to the space of symmetric $(0,2)$-tensors. The set of all Killing vector fields is precisely the kernel of this [linear map](@entry_id:201112). Since the kernel of any [linear operator](@entry_id:136520) is a [vector subspace](@entry_id:151815), the set of Killing vector fields forms a [vector subspace](@entry_id:151815) of $\mathfrak{X}(M)$ [@problem_id:1688882].

-   **Differential Forms:** Similar structures exist for [differential forms](@entry_id:146747). The set of all smooth $k$-forms on $M$, denoted $\Omega^k(M)$, is a real vector space. The [exterior derivative](@entry_id:161900) $d: \Omega^k(M) \to \Omega^{k+1}(M)$ is a [linear operator](@entry_id:136520).
    -   The set of **closed $k$-forms**, $Z^k(M)$, are those for which $d\omega = 0$. This set is the kernel of $d$, $\ker(d)$, and is therefore a [vector subspace](@entry_id:151815) of $\Omega^k(M)$ [@problem_id:1688859].
    -   The set of **exact $k$-forms**, $B^k(M)$, are those for which $\omega = d\alpha$ for some $(k-1)$-form $\alpha$. This set is the image of the map $d: \Omega^{k-1}(M) \to \Omega^k(M)$, $\text{Im}(d)$. The [image of a linear map](@entry_id:204818) is also a [vector subspace](@entry_id:151815) [@problem_id:1688863].
    -   Not all geometrically defined sets of forms are subspaces. A condition may be non-linear. For example, the condition $\omega \wedge d\omega = 0$ is not preserved under addition, and so the set of [1-forms](@entry_id:157984) satisfying it is not a subspace [@problem_id:1688859].

### A Deeper Look: Vector Spaces versus Modules

While we have established that $\mathfrak{X}(M)$ is a vector space over the real numbers $\mathbb{R}$, it possesses a richer structure. We can multiply a vector field $X$ by a [smooth function](@entry_id:158037) $f \in C^\infty(M)$ to obtain a new vector field $fX$, defined pointwise by $(fX)_p = f(p)X_p$. Since $C^\infty(M)$ is a ring, this operation makes $\mathfrak{X}(M)$ a **module** over the ring of smooth functions.

This distinction is crucial. A [vector subspace](@entry_id:151815) of $\mathfrak{X}(M)$ is closed under multiplication by real numbers (constants), but a **submodule** must be closed under multiplication by *any* [smooth function](@entry_id:158037). As an example, consider the subspace $\mathcal{C}_2$ of constant [vector fields](@entry_id:161384) on $\mathbb{R}^2$. Let $X_c = 2\frac{\partial}{\partial x} + 3\frac{\partial}{\partial y}$ be a field in $\mathcal{C}_2$. If we multiply this by a non-constant function, such as $f(x,y) = x$, the resulting vector field is $Y = fX_c = 2x\frac{\partial}{\partial x} + 3x\frac{\partial}{\partial y}$. The components of this new field depend on $x$, so it is not a constant vector field. Thus, $Y \notin \mathcal{C}_2$. This demonstrates that while $\mathcal{C}_2$ is a [vector subspace](@entry_id:151815) of $\mathfrak{X}(\mathbb{R}^2)$, it is not a submodule [@problem_id:1688897]. This highlights that the algebraic properties of geometric objects can be subtle, depending on whether we consider scalars to be real numbers or the entire ring of [smooth functions](@entry_id:138942). This module structure is fundamental to more advanced topics like connections and [tensor analysis](@entry_id:184019).

This exploration of vector spaces and subspaces provides the essential algebraic language for describing local and global geometric structures. From the definition of a single [tangent vector](@entry_id:264836) to spaces of fields that encode the symmetries of a manifold, the principles of linear algebra are an indispensable tool in the study of [differential geometry](@entry_id:145818).