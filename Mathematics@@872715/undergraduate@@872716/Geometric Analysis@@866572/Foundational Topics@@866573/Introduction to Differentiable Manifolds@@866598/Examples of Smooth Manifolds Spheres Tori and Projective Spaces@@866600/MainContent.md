## Introduction
Smooth manifolds are a cornerstone of modern mathematics, providing a rigorous framework to study [curved spaces](@entry_id:204335) that locally resemble Euclidean space. However, moving from the abstract definition to a tangible understanding can be challenging. This article bridges that gap by focusing on the three most fundamental and illustrative examples: spheres, tori, and [projective spaces](@entry_id:157963). By dissecting these [canonical models](@entry_id:198268), we gain invaluable intuition for the core principles of differential geometry.

This article will guide you through a comprehensive exploration. The first chapter, **"Principles and Mechanisms,"** delves into the foundational constructions of these manifolds, from defining [coordinate charts](@entry_id:262338) and [smooth atlases](@entry_id:264754) to analyzing their [intrinsic geometry](@entry_id:158788) and global topology. Next, **"Applications and Interdisciplinary Connections"** will showcase the remarkable utility of these spaces, revealing their roles in physics, analysis, and algebraic topology. Finally, **"Hands-On Practices"** will allow you to solidify your understanding by applying these concepts to solve concrete geometric problems.

## Principles and Mechanisms

This chapter delves into the canonical examples that form the bedrock of manifold theory: spheres, tori, and [projective spaces](@entry_id:157963). Having established the abstract definition of a [smooth manifold](@entry_id:156564) in the preceding chapter, our focus now shifts to concrete constructions. We will explore how these spaces are defined, endowed with a smooth structure, and analyzed from both geometric and topological perspectives. Each example serves not only as an object of study in its own right but also as a testing ground for the core concepts of differential geometry, from local [coordinate charts](@entry_id:262338) to global invariants like curvature and cohomology.

### Foundational Constructions and Dimensionality

The dimension of a smooth manifold is its most basic invariant, corresponding to the number of independent parameters needed to specify a point locally. We determine the dimension by constructing explicit **[coordinate charts](@entry_id:262338)**—homeomorphisms from open subsets of the manifold to open subsets of a Euclidean space $\mathbb{R}^k$. The integer $k$ is then the dimension of the manifold.

#### Submanifolds of Euclidean Space: The Sphere $S^n$

The $n$-dimensional sphere, or **$n$-sphere**, denoted $S^n$, is arguably the most fundamental compact manifold. It is most easily defined as a **submanifold** of the $(n+1)$-dimensional Euclidean space $\mathbb{R}^{n+1}$. Specifically, the unit $n$-sphere is the set of all points at a unit distance from the origin:
$$S^n \coloneqq \{x = (x_0, x_1, \dots, x_n) \in \mathbb{R}^{n+1} \mid \sum_{i=0}^{n} x_i^2 = 1\}$$

To establish its dimension, we must show that it is locally homeomorphic to a Euclidean space. A powerful method for this is **stereographic projection**. Consider the "north pole" $N = (0, \dots, 0, 1) \in S^n$. We can define a [coordinate chart](@entry_id:263963) on the open set $U = S^n \setminus \{N\}$. The chart map $\phi: U \to \mathbb{R}^n$ sends a point $p \in U$ to the unique intersection point of the line through $N$ and $p$ with the equatorial hyperplane defined by $x_n = 0$.

A calculation shows that for a point $p=(p_0, \dots, p_n) \in U$, this map is given by:
$$\phi(p_0, \dots, p_n) = \left(\frac{p_0}{1-p_n}, \frac{p_1}{1-p_n}, \dots, \frac{p_{n-1}}{1-p_n}\right)$$
This map is a [homeomorphism](@entry_id:146933) from the punctured sphere $U$ to the entirety of $\mathbb{R}^n$. Because the neighborhood $U$ is mapped to $\mathbb{R}^n$, the dimension of the [target space](@entry_id:143180) is $n$. Therefore, the sphere $S^n$ is a [smooth manifold](@entry_id:156564) of dimension $n$. A second chart, projecting from the south pole $S=(0,\dots,0,-1)$, covers the north pole, and together these two charts form a complete atlas for $S^n$.

#### Quotient Constructions I: The Torus $T^n$

While spheres are naturally viewed as embedded in a larger space, the $n$-dimensional torus, or **$n$-torus** $T^n$, is most naturally defined as a **[quotient space](@entry_id:148218)**. We begin with the Euclidean space $\mathbb{R}^n$ and identify points that differ by an integer vector. That is, we define an [equivalence relation](@entry_id:144135) where $x \sim y$ if and only if $x - y \in \mathbb{Z}^n$. The $n$-torus is the set of equivalence classes under this relation:
$$T^n \coloneqq \mathbb{R}^n / \mathbb{Z}^n$$
The map $\pi: \mathbb{R}^n \to T^n$ that sends a point to its equivalence class is called the **canonical projection**.

To construct a [coordinate chart](@entry_id:263963), consider any point $p \in T^n$. This point is the image of some $x_0 \in \mathbb{R}^n$, so $p = [x_0]$. Let's consider a small open ball $B_{1/2}(x_0) \subset \mathbb{R}^n$ of radius $1/2$ around $x_0$. Because the radius is less than $1/2$, no two distinct points in this ball are identified under the [equivalence relation](@entry_id:144135). The restriction of the projection map $\pi$ to this ball is therefore a [bijection](@entry_id:138092) onto its image, $U = \pi(B_{1/2}(x_0))$. This map is a [homeomorphism](@entry_id:146933), and its inverse, $\phi = (\pi|_{B_{1/2}(x_0)})^{-1}: U \to B_{1/2}(x_0)$, serves as a valid [coordinate chart](@entry_id:263963). Since this chart maps a neighborhood in $T^n$ to an open set in $\mathbb{R}^n$, we conclude that the $n$-torus $T^n$ is an $n$-dimensional smooth manifold.

#### Quotient Constructions II: Projective Spaces $\mathbb{RP}^n$ and $\mathbb{CP}^n$

Projective spaces are another [fundamental class](@entry_id:158335) of manifolds defined via a quotient construction. The **[real projective space](@entry_id:149094)** $\mathbb{RP}^n$ is defined as the space of all lines through the origin in $\mathbb{R}^{n+1}$. Similarly, the **[complex projective space](@entry_id:268402)** $\mathbb{CP}^n$ is the space of all complex lines through the origin in $\mathbb{C}^{n+1}$.

Formally, $\mathbb{RP}^n$ is the quotient of $\mathbb{R}^{n+1} \setminus \{0\}$ by the equivalence relation $x \sim \lambda x$ for any non-zero real scalar $\lambda \in \mathbb{R}^*$. An [equivalence class](@entry_id:140585), representing a single line, is denoted by **[homogeneous coordinates](@entry_id:154569)** $[x_0 : x_1 : \dots : x_n]$, where not all $x_i$ are zero.

To build an atlas, we define a collection of open sets. For each $i \in \{0, \dots, n\}$, let
$$U_i = \{[x_0 : \dots : x_n] \in \mathbb{RP}^n \mid x_i \neq 0\}$$
These sets clearly cover all of $\mathbb{RP}^n$, since any point must have at least one non-zero coordinate. On each $U_i$, we can define a chart $\phi_i: U_i \to \mathbb{R}^n$. For instance, on $U_0$, any point $[x_0 : \dots : x_n]$ has a unique representative where the first coordinate is 1, namely $[1 : x_1/x_0 : \dots : x_n/x_0]$. This gives us a natural chart map:
$$\phi_0([x_0 : x_1 : \dots : x_n]) = \left(\frac{x_1}{x_0}, \frac{x_2}{x_0}, \dots, \frac{x_n}{x_0}\right)$$
This map is a [homeomorphism](@entry_id:146933) from $U_0$ onto $\mathbb{R}^n$. Since the [target space](@entry_id:143180) is $\mathbb{R}^n$, the dimension of $\mathbb{RP}^n$ is $n$.

The construction for $\mathbb{CP}^n$ is perfectly analogous. We take the quotient of $\mathbb{C}^{n+1} \setminus \{0\}$ by the relation $z \sim \lambda z$ for any non-zero complex scalar $\lambda \in \mathbb{C}^*$. We define charts $\psi_i$ on open sets $U_i = \{[z_0 : \dots : z_n] \mid z_i \neq 0\}$. The chart map $\psi_0: U_0 \to \mathbb{C}^n$ is given by:
$$\psi_0([z_0 : z_1 : \dots : z_n]) = \left(\frac{z_1}{z_0}, \frac{z_2}{z_0}, \dots, \frac{z_n}{z_0}\right)$$
This shows that $\mathbb{CP}^n$ is locally homeomorphic to $\mathbb{C}^n$. Since our goal is to determine the *real* dimension, we must recall the identification between $\mathbb{C}^n$ and $\mathbb{R}^{2n}$. Each complex coordinate $w_j = u_j + i v_j$ corresponds to two real coordinates $(u_j, v_j)$. Therefore, a chart on $\mathbb{CP}^n$ maps to an open set in $\mathbb{R}^{2n}$, establishing that $\mathbb{CP}^n$ is a [smooth manifold](@entry_id:156564) of real dimension $2n$.

### The Atlas in Detail: Smooth Structures and Transition Maps

A collection of charts that cover a manifold is called an **atlas**. For the manifold to be *smooth*, the **transition maps** between any two overlapping charts must be smooth ($C^\infty$) functions. These maps govern how the coordinate representation of a point changes as we move from one chart to another.

#### The Case of Real Projective Space $\mathbb{RP}^n$

Let's examine the atlas for $\mathbb{RP}^n$ more closely. Consider two charts, say $\phi_i$ and $\phi_k$, on their respective domains $U_i$ and $U_k$. On the overlap $U_i \cap U_k$, a point has both its $i$-th and $k$-th [homogeneous coordinates](@entry_id:154569) non-zero. Let $y = \phi_i([x])$ and $z = \phi_k([x])$. The transition map is the [composite function](@entry_id:151451) $\phi_k \circ \phi_i^{-1}$, which takes the coordinates $y$ and computes the coordinates $z$.

A direct calculation reveals the transformation rule. If $y \in \mathbb{R}^n$ are the coordinates in chart $i$, so that $y_j = x_j/x_i$ for $j \neq i$, the corresponding point in $\mathbb{RP}^n$ can be represented as $[y_1: \dots : y_{i-1} : 1 : y_{i+1} : \dots]$. To find its coordinates $z$ in chart $k$, we divide by the $k$-th component, which is $y_k$. This yields the transition functions:
$$z_j = \frac{y_j}{y_k} \quad (\text{for } j \neq i, k) \quad \text{and} \quad z_i = \frac{1}{y_k}$$
These are rational functions whose denominators are non-zero on the domain $\phi_i(U_i \cap U_k) = \{y \in \mathbb{R}^n \mid y_k \neq 0\}$. As [rational functions](@entry_id:154279) are infinitely differentiable away from their poles, the transition maps are smooth. This confirms that the standard atlas endows $\mathbb{RP}^n$ with the structure of a smooth $n$-dimensional manifold. For the special case of $\mathbb{RP}^1$, which is diffeomorphic to the circle $S^1$, the transition map between its two standard charts is simply the inversion map $t \mapsto 1/t$.

#### The Case of Complex Projective Space $\mathbb{CP}^n$

The situation for $\mathbb{CP}^n$ is entirely analogous, but with profound consequences. Following the same logic, the transition map $\psi_i \circ \psi_j^{-1}$ between two charts on $\mathbb{CP}^n$ is given by the exact same formulae, but now the variables are complex numbers.
$$w^{(i)}_k = \frac{w^{(j)}_k}{w^{(j)}_i} \quad (\text{for } k \neq i,j) \quad \text{and} \quad w^{(i)}_j = \frac{1}{w^{(j)}_i}$$
Since these functions are rational functions of [complex variables](@entry_id:175312), they are not just smooth; they are **holomorphic**. A manifold whose transition maps are all holomorphic is called a **complex manifold**. Thus, $\mathbb{CP}^n$ is the archetypal example of a compact [complex manifold](@entry_id:261516) of complex dimension $n$. This additional structure is immensely important and is not shared by its real counterpart, $\mathbb{RP}^n$, in general. For example, $\mathbb{CP}^1$ is diffeomorphic to the sphere $S^2$, while $\mathbb{RP}^1$ is diffeomorphic to the circle $S^1$.

### Embedding and Intrinsic Geometry

Manifolds can be studied intrinsically, based on their atlas structure, or extrinsically, by how they sit inside a larger [ambient space](@entry_id:184743) like $\mathbb{R}^N$. This extrinsic view gives rise to geometric concepts like curvature.

#### Immersions and Embeddings: The Torus in $\mathbb{R}^3$

A [smooth map](@entry_id:160364) $f: M \to N$ between two manifolds is called an **immersion** if its differential (or Jacobian) is injective at every point. This means that locally, the map is one-to-one. However, an immersion may have global self-intersections. An **embedding** is a map that is both an immersion and a [homeomorphism](@entry_id:146933) onto its image (with the subspace topology). This forbids self-intersections and ensures that the topology of the manifold $M$ matches the topology its image inherits from $N$. 

The standard torus provides an excellent illustration. The map $\Phi: T^2 \to \mathbb{R}^3$ that creates a [surface of revolution](@entry_id:261378), given by
$$\Phi(\theta,\phi)=\big((R+r\cos\theta)\cos\phi,\,(R+r\cos\theta)\sin\phi,\,r\sin\theta\big)$$
can be analyzed using these definitions. For this map to describe a familiar "doughnut" shape without self-intersection, we require the major radius $R$ to be greater than the minor radius $r$ ($R > r > 0$).
1.  **Immersion**: By computing the [partial derivatives](@entry_id:146280) $\frac{\partial\Phi}{\partial\theta}$ and $\frac{\partial\Phi}{\partial\phi}$, one can show their cross product is never the zero vector provided $R>r>0$. This ensures the two tangent vectors are always linearly independent, meaning the differential of $\Phi$ is injective. Thus, $\Phi$ is an immersion.
2.  **Embedding**: To be an embedding, $\Phi$ must also be a [homeomorphism](@entry_id:146933) onto its image. This requires [injectivity](@entry_id:147722). A careful analysis shows that $\Phi(\theta_1, \phi_1) = \Phi(\theta_2, \phi_2)$ if and only if $(\theta_1, \phi_1) = (\theta_2, \phi_2)$ (as points on the torus $T^2$). The map is injective. Since the domain $T^2 = S^1 \times S^1$ is compact and the codomain $\mathbb{R}^3$ is Hausdorff, any [continuous injective map](@entry_id:275991) is automatically a [homeomorphism](@entry_id:146933) onto its image.
Therefore, for $R>r>0$, the map $\Phi$ is an embedding, and its image is an **[embedded submanifold](@entry_id:273162)** of $\mathbb{R}^3$.

#### Induced Metrics: The Geometry of Curvature

When a manifold is embedded in a Euclidean space, it inherits a **Riemannian metric**, which is a way of measuring lengths and angles on the manifold itself. This is done by "pulling back" the Euclidean inner product onto the [tangent spaces](@entry_id:199137) of the submanifold. This [induced metric](@entry_id:160616) allows us to define intrinsic geometric quantities, most importantly, **curvature**.

##### Example 1: The Round Metric and Constant Curvature of $S^n$

The standard metric on $S^n$, known as the **round metric**, is the one induced by its embedding in $\mathbb{R}^{n+1}$. We can find an explicit expression for this metric in [local coordinates](@entry_id:181200). Using the inverse [stereographic projection](@entry_id:142378) chart $F: \mathbb{R}^n \to S^n$, one can compute the pullback of the Euclidean metric $g_{\text{Euc}} = \sum dP_k \otimes dP_k$. The calculation yields a remarkably simple expression for the round metric $g_{S^n}$ in stereographic coordinates $x=(x_1, \dots, x_n)$:
$$g_{S^n} = \frac{4}{(1+|x|^2)^2} \sum_{i=1}^{n} dx_i \otimes dx_i$$
This expression shows that the metric on the sphere is a scalar multiple of the Euclidean metric on $\mathbb{R}^n$. Such a metric is called **conformally flat**.

The curvature of a Riemannian manifold is captured by the **Riemann [curvature tensor](@entry_id:181383)**, $R(X,Y)Z$. For a submanifold of Euclidean space, this tensor can be computed using the **Gauss equation**, which relates it to the **second fundamental form**. For the unit sphere $S^n \subset \mathbb{R}^{n+1}$, this procedure leads to a beautiful and fundamental result:
$$R(X,Y)Z = g(Y,Z)X - g(X,Z)Y$$
From this tensor, we can compute the **sectional curvature** $K(\sigma)$, which describes the curvature of the manifold within a 2-dimensional [tangent plane](@entry_id:136914) $\sigma = \text{span}\{e_1, e_2\}$. For the unit sphere, the sectional curvature is found to be constant and equal to $+1$ for every point and every [tangent plane](@entry_id:136914). The sphere is the archetypal space of [constant positive curvature](@entry_id:268046).

##### Example 2: The Variable Curvature of the Torus $T^2$

In contrast to the sphere, the embedded torus in $\mathbb{R}^3$ has a curvature that varies from point to point. The **Gaussian curvature** (which for a 2D surface is equivalent to the sectional curvature) can be computed from the [first and second fundamental forms](@entry_id:192112) of the embedded surface. For the standard torus with major radius $R$ and minor radius $r$, the Gaussian curvature at a point corresponding to the angle $\theta$ (the angle of the circular cross-section) is given by:
$$K(\theta, \phi) = \frac{\cos\theta}{r(R+r\cos\theta)}$$
This formula reveals a rich geometric structure:
-   On the outer equator of the torus ($\theta=0$), the curvature is positive: $K = 1/(r(R+r))$. The surface is locally convex, like a sphere.
-   On the inner equator ($\theta=\pi$), the curvature is negative: $K = -1/(r(R-r))$. The surface is locally saddle-shaped.
-   On the top and bottom circles ($\theta = \pi/2, 3\pi/2$), the curvature is zero: $K=0$. The surface is locally flat in one direction, like a cylinder.
This variation in curvature makes the torus a much richer and more complex geometric object than the highly symmetric sphere.

#### The Geometry of Complex Projective Space: The Fubini-Study Metric

Complex [projective space](@entry_id:149949) $\mathbb{CP}^n$ possesses a canonical and remarkably beautiful geometric structure known as the **Fubini-Study metric**. This is an example of a **Kähler metric**, a structure that seamlessly blends Riemannian, complex, and symplectic geometry.

On a local chart $U_j \cong \mathbb{C}^n$ with coordinates $(w_1, \dots, w_n)$, this metric can be derived from a single real-valued function called the **Kähler potential**, $K$:
$$K(w_1, \dots, w_n) = \log\left(1 + \sum_{k=1}^{n} |w_k|^2\right)$$
The associated **Kähler form** $\omega_{FS}$ is a real 2-form of type (1,1) defined as $\omega_{FS} = i\partial\bar{\partial}K$. A direct computation yields its local expression:
$$\omega_{FS} = i \left( \frac{\sum_{j=1}^{n} dw_{j} \wedge d\bar{w}_{j}}{1 + \sum_{k=1}^{n} |w_{k}|^{2}} - \frac{\left(\sum_{j=1}^{n} \bar{w}_{j} dw_{j}\right) \wedge \left(\sum_{k=1}^{n} w_{k} d\bar{w}_{k}\right)}{\left(1 + \sum_{l=1}^{n} |w_{l}|^{2}\right)^{2}} \right)$$
This form has two crucial properties:
1.  **It is closed**: $d\omega_{FS} = 0$. This follows from the definition $\omega_{FS} = i\partial\bar{\partial}K$ and the identity $d = \partial + \bar{\partial}$. Since $\bar{\partial}^2=0$, we can write $\omega_{FS} = i \partial(\bar{\partial}K) = i(d-\bar{\partial})(\bar{\partial}K) = i d(\bar{\partial}K)$. Thus, $d\omega_{FS} = i d^2(\bar{\partial}K) = 0$ because $d^2=0$. This makes $(\mathbb{CP}^n, \omega_{FS})$ a [symplectic manifold](@entry_id:637770).
2.  **It is positive**: The associated Hermitian form is positive definite. This can be verified using the Cauchy-Schwarz inequality and ensures that the real part of the associated Hermitian form defines a Riemannian metric, $g_{FS}$.
The Fubini-Study metric is a fundamental object in both geometry and theoretical physics, and its existence makes $\mathbb{CP}^n$ a primary example of a compact Kähler-Einstein manifold.

### Global Topological Properties

Beyond local geometry, differential forms and algebraic topology provide powerful tools for understanding the global "shape" of a manifold—for instance, its connectivity, its holes, and its [orientability](@entry_id:149777).

#### Orientability and Integration: The Case of $\mathbb{RP}^n$

A manifold is **orientable** if it is possible to make a consistent choice of "handedness" or orientation for its tangent spaces across the entire manifold. For a connected orientable $n$-manifold, this is equivalent to the existence of a nowhere-vanishing $n$-form.

Real [projective space](@entry_id:149949) $\mathbb{RP}^n$ provides a crucial lesson in orientability. It is a standard result that $\mathbb{RP}^n$ is orientable if and only if $n$ is odd. This can be understood by considering the [covering map](@entry_id:154506) $\pi: S^n \to \mathbb{RP}^n$, where points on the sphere are identified with their antipodes, $x \sim -x$. The [antipodal map](@entry_id:151775) $A: S^n \to S^n$, given by $A(x)=-x$, has degree $\deg(A) = (-1)^{n+1}$.

Let $\omega$ be any top-degree form on $\mathbb{RP}^n$. Its pullback to the sphere, $\eta = \pi^*\omega$, must be invariant under the [antipodal map](@entry_id:151775), $A^*\eta = \eta$. However, the integral of $A^*\eta$ is related to the integral of $\eta$ by the degree of the map: $\int_{S^n} A^*\eta = \deg(A) \int_{S^n} \eta$. Combining these gives:
$$\int_{S^n} \eta = (-1)^{n+1} \int_{S^n} \eta \quad \implies \quad \left(1 - (-1)^{n+1}\right) \int_{S^n} \eta = 0$$
-   If $n$ is **even**, $n+1$ is odd, and the equation becomes $2 \int_{S^n} \eta = 0$, implying $\int_{S^n} \pi^*\omega = 0$. This is consistent with the [non-orientability](@entry_id:155097) of $\mathbb{RP}^n$ for even $n$, which precludes a well-defined notion of integral for $\omega$ itself.
-   If $n$ is **odd**, $n+1$ is even, and the equation becomes $0=0$. This places no restriction on the integral. In this case, $\mathbb{RP}^n$ is orientable, and one can show that the integral of $\omega$ is related to the integral of its pullback by $\int_{\mathbb{RP}^n}\omega = \frac{1}{2}\int_{S^n}\pi^*\omega$ (for a compatible choice of orientation).

#### De Rham Cohomology: Probing Holes

**De Rham cohomology** is a central tool that associates a sequence of vector spaces, $H^k_{\mathrm{dR}}(M)$, to a smooth manifold $M$. The dimension of $H^k_{\mathrm{dR}}(M)$, called the $k$-th Betti number $b_k$, counts the number of independent $k$-dimensional "holes" in the manifold. A non-zero cohomology group $H^k_{\mathrm{dR}}(M)$ implies the existence of closed $k$-forms that are not exact.

##### The Sphere $S^n$

Using the **Mayer-Vietoris sequence** with an [open cover](@entry_id:140020) consisting of two large hemispheres (e.g., $S^n$ minus the north pole and $S^n$ minus the south pole), one can compute the cohomology of the sphere. The result is:
$$ H^{k}_{\mathrm{dR}}(S^{n}) \cong \begin{cases} \mathbb{R}   \text{if } k=0 \text{ or } k=n \\ \{0\}   \text{otherwise} \end{cases} $$
The Betti numbers are $b_0=1$, $b_n=1$, and all others are zero. This tells us that for $n \ge 1$, the sphere is connected ($b_0=1$) and encloses a single $n$-dimensional "void" ($b_n=1$). The vanishing of the intermediate groups, $H^k_{\mathrm{dR}}(S^n)=0$ for $0  k  n$, means that spheres have no "intermediate" holes. Any closed $k$-form on $S^n$ (for $0  k  n$) is automatically exact.

##### The Torus $T^n$

The cohomology of the $n$-torus can be computed using the **Künneth formula**, which relates the cohomology of a product manifold $M \times N$ to that of its factors. Since $T^n = S^1 \times \dots \times S^1$ ($n$ times) and $H^0_{\mathrm{dR}}(S^1) \cong H^1_{\mathrm{dR}}(S^1) \cong \mathbb{R}$, the Künneth formula yields:
$$H^k_{\mathrm{dR}}(T^n) \cong \mathbb{R}^{\binom{n}{k}}$$
The $k$-th Betti number $b_k(T^n)$ is given by the binomial coefficient "n choose k". This rich structure reflects the multiple independent "loops" one can draw on a torus. For the [2-torus](@entry_id:265991) $T^2$, we have $b_0=1, b_1=2, b_2=1$, corresponding to one connected component, two independent non-contractible loops (one "longitudinally," one "latitudinally"), and one enclosed volume.

##### Real and Complex Projective Spaces

The cohomology of [projective spaces](@entry_id:157963) is more subtle. For **[real projective space](@entry_id:149094)** $\mathbb{RP}^n$ with real coefficients:
$$ H^{k}_{\mathrm{dR}}(\mathbb{RP}^n) \cong \begin{cases} \mathbb{R}  \text{if } k=0 \\ \mathbb{R}  \text{if } k=n \text{ and } n \text{ is odd} \\ \{0\}  \text{otherwise} \end{cases} $$
The vanishing of most cohomology groups reflects the complex twisting in its topology.

For **[complex projective space](@entry_id:268402)** $\mathbb{CP}^n$, the cohomology is remarkably simple and elegant. It is concentrated in even degrees:
$$ H^{k}_{\mathrm{dR}}(\mathbb{CP}^n) \cong \begin{cases} \mathbb{R}  \text{if } k \text{ is even and } 0 \le k \le 2n \\ \{0\}  \text{if } k \text{ is odd} \end{cases} $$
This structure can be understood through the lens of Kähler geometry. The powers of the Fubini-Study Kähler form $\omega_{FS}$ generate the entire [cohomology ring](@entry_id:160158). The class $[\omega_{FS}] \in H^2_{\mathrm{dR}}(\mathbb{CP}^n)$ is non-zero, and its $k$-th power, $[\omega_{FS}]^k = [\omega_{FS} \wedge \dots \wedge \omega_{FS}]$, generates the group $H^{2k}_{\mathrm{dR}}(\mathbb{CP}^n)$ for $k=1, \dots, n$.