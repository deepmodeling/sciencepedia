## Introduction
How do we perform calculus on a curved surface? While a Riemannian metric allows us to measure lengths and angles within a single tangent space, it doesn't tell us how to compare vectors from different points or how to define the acceleration of a curve. This requires a rule for differentiation, known as a connection. However, a manifold can be equipped with infinitely many connections, creating a fundamental problem: which one is the "correct" one for the geometry?

This article delves into the solution provided by one of the most foundational results in the field: the Fundamental Theorem of Riemannian Geometry. It establishes that for any given metric, there is one and only one connection that is perfectly in tune with the geometry.

- In **Principles and Mechanisms**, we will formally define an [affine connection](@entry_id:160152) and introduce the two natural conditions it must satisfy—[metric compatibility](@entry_id:265910) and torsion-freeness. We will then prove the Fundamental Theorem, showing how these conditions uniquely determine the canonical Levi-Civita connection.

- In **Applications and Interdisciplinary Connections**, we will put this theorem to work. You will learn how the Levi-Civita connection is used to calculate Christoffel symbols, define geodesics and curvature, and serve as the mathematical language for theories in continuum mechanics and general relativity.

- Finally, in **Hands-On Practices**, you will have the opportunity to solidify your understanding by working through concrete examples, from calculating Christoffel symbols for various metrics to verifying the properties of the connection.

By the end of this article, you will understand not only what the Levi-Civita connection is, but why its unique existence is the cornerstone of calculus on curved manifolds.

## Principles and Mechanisms

In the preceding chapter, we introduced the fundamental objects of study in Riemannian geometry: a smooth manifold $M$ equipped with a Riemannian metric $g$. The metric provides a way to measure lengths and angles within each [tangent space](@entry_id:141028) $T_pM$. However, to perform calculus on the manifold—to compare vectors in different [tangent spaces](@entry_id:199137) and to define concepts like acceleration—we need an additional structure: a way to differentiate [vector fields](@entry_id:161384). This structure is provided by an **[affine connection](@entry_id:160152)**. This chapter will explore the properties of connections, leading to the central theorem that endows every Riemannian manifold with a single, canonical connection uniquely determined by its metric.

### The Nature of an Affine Connection

An [affine connection](@entry_id:160152) is a rule for differentiating a vector field with respect to another vector field. More formally, a **linear (or affine) connection** on the tangent bundle $TM$ is a map $\nabla: \Gamma(TM) \times \Gamma(TM) \to \Gamma(TM)$, denoted by $(X,Y) \mapsto \nabla_X Y$, that satisfies a specific set of axioms. For any vector fields $X, Y, Z \in \Gamma(TM)$ and any smooth function $f \in C^{\infty}(M)$, these axioms are [@problem_id:3070971]:

1.  **$C^{\infty}(M)$-linearity in the first argument:** $\nabla_{fX+Y}Z = f\nabla_X Z + \nabla_Y Z$.
2.  **$\mathbb{R}$-linearity (Additivity) in the second argument:** $\nabla_X(Y+Z) = \nabla_X Y + \nabla_X Z$.
3.  **Leibniz Rule in the second argument:** $\nabla_X(fY) = (Xf)Y + f\nabla_X Y$.

The first property, linearity over [smooth functions](@entry_id:138942) in $X$, implies that the value of $\nabla_X Y$ at a point $p$, denoted $(\nabla_X Y)(p)$, depends only on the tangent vector $X(p)$ and not on the behavior of the vector field $X$ in a neighborhood of $p$. This is a crucial locality property.

However, the third property—the Leibniz rule—reveals something profound about the nature of a connection. The presence of the derivative term $(Xf)Y$ means that the operator $Y \mapsto \nabla_X Y$ is **not** $C^{\infty}(M)$-linear. If it were, the rule would simply be $\nabla_X(fY) = f\nabla_X Y$. This non-tensorial behavior is the defining characteristic of a connection. While a Riemannian metric $g$ is a $(0,2)$-tensor field, satisfying the property $g(fX, hY) = fh g(X,Y)$, a connection $\nabla$ is not a tensor field at all [@problem_id:3070973]. The value $(\nabla_X Y)(p)$ depends not only on the vectors $X(p)$ and $Y(p)$ but also on the first-order derivatives of the components of $Y$ at $p$.

Despite this, there is a deep relationship between connections and tensors. Consider two distinct connections on $M$, say $\nabla^{(1)}$ and $\nabla^{(2)}$. Let us define a new map $D$ representing their difference: $D(X,Y) = \nabla^{(1)}_X Y - \nabla^{(2)}_X Y$. We can investigate the properties of this difference map. It is straightforward to show that $D$ is $C^{\infty}(M)$-linear in both of its arguments. For instance, in the second argument:
$$
D(X, fY) = \nabla^{(1)}_X(fY) - \nabla^{(2)}_X(fY) = \left( (Xf)Y + f\nabla^{(1)}_X Y \right) - \left( (Xf)Y + f\nabla^{(2)}_X Y \right) = f D(X,Y)
$$
The non-tensorial derivative terms $(Xf)Y$ cancel perfectly. Since $D$ is $C^{\infty}(M)$-bilinear and maps two vector fields to a vector field, it is, by definition, a [tensor field](@entry_id:266532) of type $(1,2)$ [@problem_id:3070973], [@problem_id:3070979]. This implies that the set of all affine connections on a manifold is an **affine space** modeled on the vector space of $(1,2)$-[tensor fields](@entry_id:190170). Stating that two connections $\nabla^{(1)}$ and $\nabla^{(2)}$ are equal is equivalent to stating that their difference tensor $D$ is the zero tensor everywhere on $M$. This provides a precise meaning for the "uniqueness" of a connection.

### The Canonical Choice: Torsion-Freeness and Metric Compatibility

The axioms for an [affine connection](@entry_id:160152) are purely algebraic and do not reference the metric structure of a Riemannian manifold. On any given manifold, there are infinitely many possible connections. The central goal of Riemannian geometry is to single out one that is perfectly adapted to the geometry defined by the metric $g$. This is achieved by imposing two additional, natural conditions.

#### Metric Compatibility

A connection $\nabla$ is said to be **compatible with the metric** $g$ if the metric is covariantly constant. This means that for any vector field $X$, the [covariant derivative of the metric tensor](@entry_id:198162) in the direction of $X$ is zero: $\nabla_X g = 0$. Using the product rule for [covariant differentiation](@entry_id:263981), this condition is equivalent to the following identity holding for all vector fields $X, Y, Z \in \Gamma(TM)$ [@problem_id:3070995]:
$$
X(g(Y,Z)) = g(\nabla_X Y, Z) + g(Y, \nabla_X Z)
$$
This condition has a beautiful geometric interpretation. It means that the geometry of [tangent vectors](@entry_id:265494)—their lengths and the angles between them—is preserved under **[parallel transport](@entry_id:160671)**. A vector field $V$ is said to be parallel-transported along a curve $\gamma(t)$ if its [covariant derivative](@entry_id:152476) along the curve's [tangent vector](@entry_id:264836) $\dot{\gamma}$ is zero, i.e., $\nabla_{\dot{\gamma}} V = 0$. If we take two [vector fields](@entry_id:161384), $V(t)$ and $W(t)$, that are both parallel-transported along $\gamma$, the [metric compatibility condition](@entry_id:201846) allows us to calculate the rate of change of their inner product:
$$
\frac{d}{dt} g(V(t), W(t)) = g(\nabla_{\dot{\gamma}} V, W) + g(V, \nabla_{\dot{\gamma}} W) = g(0, W) + g(V, 0) = 0
$$
The inner product $g(V(t), W(t))$ is constant along the curve [@problem_id:1550523], [@problem_id:3071004]. Thus, a [metric-compatible connection](@entry_id:194538) ensures that parallel transport is an isometry between tangent spaces.

In a local coordinate system $\{x^i\}$, this condition can be written as $\nabla_k g_{ij} = 0$. Expanding the [covariant derivative](@entry_id:152476) gives an expression for the partial derivatives of the metric components in terms of the [connection coefficients](@entry_id:157618), or **Christoffel symbols**, $\Gamma^k_{ij}$ [@problem_id:1550530]:
$$
\partial_k g_{ij} = \Gamma^l_{ki} g_{lj} + \Gamma^l_{kj} g_{il}
$$

#### Torsion-Freeness

The second condition relates the connection to the Lie bracket of vector fields, an intrinsic operation on any manifold. The **[torsion tensor](@entry_id:204137)** of a connection $\nabla$ is the $(1,2)$-[tensor field](@entry_id:266532) $T$ defined by:
$$
T(X,Y) = \nabla_X Y - \nabla_Y X - [X,Y]
$$
A connection is said to be **torsion-free** if its [torsion tensor](@entry_id:204137) vanishes identically, i.e., $T(X,Y)=0$ for all $X, Y$. This condition simplifies to the symmetric-looking relation $\nabla_X Y - \nabla_Y X = [X,Y]$.

In a local coordinate system, the Lie bracket of [coordinate basis](@entry_id:270149) vectors is zero: $[\partial_i, \partial_j] = 0$. The components of the [torsion tensor](@entry_id:204137) in this basis are therefore given by $T^k_{ij} = \Gamma^k_{ij} - \Gamma^k_{ji}$. Thus, the torsion-free condition is equivalent to the statement that the Christoffel symbols are symmetric in their lower two indices [@problem_id:1550551]:
$$
\Gamma^k_{ij} = \Gamma^k_{ji}
$$
This condition implies that the infinitesimal parallelograms used to define the covariant derivative close up, which corresponds to a more "natural" form of differentiation.

### The Fundamental Theorem of Riemannian Geometry

We are now equipped to state the most important result in the foundations of Riemannian geometry. It asserts that the two conditions of [metric compatibility](@entry_id:265910) and torsion-freeness are not only natural but also precisely sufficient to single out a unique connection from the infinite set of possibilities.

**The Fundamental Theorem of Riemannian Geometry:** *For any Riemannian manifold $(M,g)$, there exists a unique [affine connection](@entry_id:160152) $\nabla$ that is both [metric-compatible](@entry_id:160255) and torsion-free.*

This unique connection is called the **Levi-Civita connection** of the metric $g$ [@problem_id:3070995]. This theorem is profound: it establishes a canonical and intrinsic way to perform [differential calculus](@entry_id:175024) on any Riemannian manifold, using only the structure provided by the metric itself.

### The Koszul Formula: Proof of Existence and Uniqueness

The proof of the fundamental theorem is constructive and provides an explicit formula for the Levi-Civita connection. This formula, known as the **Koszul formula**, demonstrates both uniqueness and existence in a single, elegant stroke. The derivation relies on skillfully manipulating the two defining conditions.

Let's assume a connection $\nabla$ exists that is both [metric-compatible](@entry_id:160255) and torsion-free. We write down the metric-compatibility identity for three cyclic [permutations](@entry_id:147130) of vector fields $X, Y, Z$:
1. $X(g(Y,Z)) = g(\nabla_X Y, Z) + g(Y, \nabla_X Z)$
2. $Y(g(Z,X)) = g(\nabla_Y Z, X) + g(Z, \nabla_Y X)$
3. $Z(g(X,Y)) = g(\nabla_Z X, Y) + g(X, \nabla_Z Y)$

By forming the linear combination $(1) + (2) - (3)$ and strategically applying the torsion-free condition (e.g., $\nabla_Y X = \nabla_X Y - [X,Y]$) to rearrange terms, we can isolate the term $g(\nabla_X Y, Z)$. After careful algebraic simplification, we arrive at the Koszul formula [@problem_id:2996994]:
$$
2g(\nabla_X Y, Z) = X(g(Y,Z)) + Y(g(Z,X)) - Z(g(X,Y)) + g([X,Y],Z) + g([Z,X],Y) - g([Y,Z],X)
$$
This formula is the heart of the theorem.

**Uniqueness:** The right-hand side of the Koszul formula depends only on the metric $g$ and the Lie bracket of [vector fields](@entry_id:161384)—structures that are given on the manifold, independent of any choice of connection. This means that for any connection satisfying the two hypotheses, the scalar quantity $g(\nabla_X Y, Z)$ is uniquely determined for all possible [vector fields](@entry_id:161384) $Z$. Because the metric $g$ is non-degenerate, it defines an inner product on each tangent space. By the Riesz [representation theorem](@entry_id:275118), if the inner product of a vector $v$ with every other vector is uniquely determined, then the vector $v$ itself is uniquely determined. In our case, the vector is $\nabla_X Y$. Thus, any connection satisfying the conditions must be given by this formula, proving **uniqueness**. [@problem_id:2996994]

**Existence:** To prove existence, one simply turns the argument around. We can *define* an operator $\nabla_X Y$ via the Koszul formula. One must then perform the rigorous check that this operator, so defined, satisfies all the axioms of an [affine connection](@entry_id:160152) and is indeed [metric-compatible](@entry_id:160255) and torsion-free. Since all components of the formula ([vector fields as derivations](@entry_id:636698), the metric, the Lie bracket) are intrinsic and coordinate-free, the resulting connection is also intrinsically defined. [@problem_id:2996994]

In [local coordinates](@entry_id:181200), setting $X=\partial_i$, $Y=\partial_j$, and $Z=\partial_k$, and noting that $[\partial_i, \partial_j] = 0$, the Koszul formula simplifies significantly and leads to an explicit formula for the Christoffel symbols in terms of the derivatives of the metric components [@problem_id:1550530]:
$$
\Gamma^k_{ij} = \frac{1}{2} g^{kl} \left( \frac{\partial g_{jl}}{\partial x^i} + \frac{\partial g_{il}}{\partial x^j} - \frac{\partial g_{ij}}{\partial x^l} \right)
$$
where $g^{kl}$ are the components of the [inverse metric tensor](@entry_id:275529). This shows concretely how the connection is "soldered" to the metric.

### Necessity of the Conditions

The fundamental theorem's power lies in its delicate balance of conditions. Dropping either torsion-freeness or metric-compatibility destroys uniqueness, opening the door to an infinite family of connections. We can illustrate this by constructing explicit counterexamples [@problem_id:3070984]. Let $\nabla$ be the Levi-Civita connection on a Riemannian manifold $(M,g)$, and consider a new connection $\nabla'$ defined by $\nabla'_X Y = \nabla_X Y + A(X,Y)$, where $A$ is a non-zero $(1,2)$-tensor.

- **If only [metric compatibility](@entry_id:265910) is required:** There exist many connections that are [metric-compatible](@entry_id:160255) but have torsion. For example, on Euclidean space $(\mathbb{R}^n, g_{\text{eucl}})$, the tensor $A(X,Y) = g(V,X)JY$, where $V$ is a constant vector and $J$ is a constant skew-[symmetric operator](@entry_id:275833), gives rise to a new connection $\nabla' = \nabla + A$ that is [metric-compatible](@entry_id:160255) but not torsion-free. This demonstrates that [metric compatibility](@entry_id:265910) alone is not enough to ensure uniqueness.

- **If only torsion-freeness is required:** Similarly, there are many torsion-free connections that fail to be [metric-compatible](@entry_id:160255). An important class of such connections arises in projective geometry. A tensor of the form $A(X,Y) = \alpha(X)Y + \alpha(Y)X$, where $\alpha$ is a non-zero 1-form, is symmetric in $X$ and $Y$. The resulting connection $\nabla' = \nabla+A$ is therefore torsion-free. However, one can verify that it is not [metric-compatible](@entry_id:160255).

These examples underscore that it is the precise conjunction of both hypotheses that uniquely determines the Levi-Civita connection.

### Geometric Consequences of the Levi-Civita Connection

The existence of a canonical connection has profound implications, allowing us to define fundamental geometric concepts in an intrinsic way.

**Geodesics:** The Levi-Civita connection gives a canonical notion of a "straight line" on a curved manifold. A **geodesic** is a curve $\gamma(t)$ whose [tangent vector](@entry_id:264836) is parallel-transported along itself: $\nabla_{\dot{\gamma}} \dot{\gamma} = 0$. In [local coordinates](@entry_id:181200), this becomes a system of second-order [ordinary differential equations](@entry_id:147024). The standard existence and uniqueness theorems for ODEs then guarantee that for any point $p \in M$ and any [initial velocity](@entry_id:171759) $v \in T_pM$, there exists a unique geodesic starting at $p$ with that velocity, at least for a short time [@problem_id:3071004]. It is crucial to note, however, that while geodesics are *locally* the shortest path between two points, they are not necessarily globally length-minimizing. For example, on a sphere, traveling the "long way" around a [great circle](@entry_id:268970) is a geodesic path but is clearly not the shortest route.

**Riemannian Normal Coordinates:** The existence of geodesics allows for the construction of a very special local coordinate system around any point $p \in M$, known as **Riemannian [normal coordinates](@entry_id:143194)**. These coordinates are constructed by identifying a neighborhood of $p$ in $M$ with a neighborhood of the origin in its [tangent space](@entry_id:141028) $T_pM$ via the [exponential map](@entry_id:137184). In this coordinate system, two remarkable properties hold [@problem_id:3071004]:
1. Geodesics passing through $p$ are represented as straight lines passing through the origin.
2. All Christoffel symbols of the Levi-Civita connection vanish at the point $p$: $\Gamma^k_{ij}(p)=0$.

This means that at any point, we can choose coordinates such that the effects of curvature on first derivatives disappear. In this sense, every Riemannian manifold is "infinitesimally Euclidean." This is an invaluable tool for both computation and conceptual arguments.

**Curvature and Holonomy:** While we can make the [connection coefficients](@entry_id:157618) vanish at a single point, we generally cannot make them vanish in a whole neighborhood. The obstruction to doing so is **curvature**. A direct manifestation of curvature is **[holonomy](@entry_id:137051)**. Although [parallel transport](@entry_id:160671) preserves lengths and angles, transporting a vector around a closed loop does not, in general, return the vector to its original state. The transformation the vector undergoes is an [isometry](@entry_id:150881) of the [tangent space](@entry_id:141028), and the set of all such transformations forms the **holonomy group** of the connection. The [holonomy group](@entry_id:160097) is trivial if and only if the manifold is flat (zero curvature). The fact that [parallel transport](@entry_id:160671) around a loop is not the identity map is a direct measure of how the manifold is curved [@problem_id:3071004]. This concept of curvature, which is defined in terms of the Levi-Civita connection, will be the central topic of the next chapter.