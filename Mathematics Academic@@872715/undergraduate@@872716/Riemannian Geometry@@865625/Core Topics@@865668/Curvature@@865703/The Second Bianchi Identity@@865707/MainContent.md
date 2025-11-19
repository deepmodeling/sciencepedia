## Introduction
The Riemann [curvature tensor](@entry_id:181383) offers a powerful way to measure the geometry of a curved space, but its algebraic properties at a single point only tell part of the story. A deeper understanding requires knowing how curvature itself changes from one point to another. This leads us to one of the most profound structural laws in differential geometry: the second Bianchi identity. This identity is not just a mathematical curiosity; it is a cornerstone of Riemannian geometry and a linchpin of modern theoretical physics, most famously providing the geometric foundation for Albert Einstein's theory of general relativity.

This article bridges the gap between the static definition of curvature and its dynamic behavior. We will explore the differential constraints that curvature must obey, revealing a deep and elegant law governing the structure of space. You will learn how this identity arises, what it means geometrically, and how its consequences echo across vast domains of science. Over the next three chapters, we will first uncover the fundamental principles and mechanisms behind the identity. We will then explore its far-reaching applications in pure [geometry and physics](@entry_id:265497). Finally, you will have the opportunity to solidify your understanding through a series of hands-on practices.

## Principles and Mechanisms

Having introduced the fundamental concepts of Riemannian geometry, we now delve into one of the most profound and consequential identities satisfied by the Riemann [curvature tensor](@entry_id:181383): the second Bianchi identity. This identity is not merely an algebraic curiosity; it is a differential relation that constrains how curvature can vary across a manifold. Understanding its principles and the mechanisms from which it arises provides deep insight into the geometric structure of space and is foundational to modern physics, particularly general relativity.

### The Covariant Derivative of the Curvature Tensor

Before stating the identity itself, we must first establish a clear understanding of what it means to differentiate the [curvature tensor](@entry_id:181383). This requires extending the notion of the covariant derivative to arbitrary [tensor fields](@entry_id:190170).

#### Recap: The Riemann Curvature Tensor

Recall that on a Riemannian manifold $(M,g)$, the Levi-Civita connection $\nabla$ provides a canonical way to differentiate vector fields. The **Riemann [curvature tensor](@entry_id:181383)**, denoted $R$, measures the [non-commutativity](@entry_id:153545) of second covariant derivatives. For any smooth vector fields $X, Y, Z$, it is defined as the $(1,3)$-tensor given by:
$$
R(X,Y)Z = \nabla_X \nabla_Y Z - \nabla_Y \nabla_X Z - \nabla_{[X,Y]} Z
$$
where $[X,Y]$ is the Lie bracket of [vector fields](@entry_id:161384) [@problem_id:3077207, 3003092, 3077235]. The term $-\nabla_{[X,Y]}Z$ is crucial; without it, the expression would not be a tensor (i.e., it would not be $C^\infty(M)$-linear in $X$ and $Y$). Geometrically, the [curvature tensor](@entry_id:181383) measures the failure of parallel transport to be path-independent. Specifically, the infinitesimal change in a vector $W$ when parallel-transported around a small parallelogram spanned by vectors $X$ and $Y$ is given by $R(X,Y)W$ [@problem_id:3077202].

#### Extending the Covariant Derivative

The power of [tensor calculus](@entry_id:161423) lies in its coordinate-independent language. To maintain this, we cannot simply differentiate the components of a tensor. Instead, the [covariant derivative](@entry_id:152476) $\nabla$ is extended from vector fields to any [tensor field](@entry_id:266532) of type $(r,s)$ by imposing a set of natural axioms [@problem_id:3077231]. This extension is uniquely determined by requiring that for any vector field $X$:

1.  On scalar functions $f$, $\nabla_X f$ is the directional derivative, $X(f)$.
2.  On [vector fields](@entry_id:161384), it is the given connection $\nabla_X Y$.
3.  It obeys the **Leibniz rule** (or derivation property) with respect to the tensor product $\otimes$:
    $$
    \nabla_X(T \otimes S) = (\nabla_X T) \otimes S + T \otimes (\nabla_X S)
    $$
4.  It commutes with all natural contractions (e.g., tracing, or evaluating a [covector](@entry_id:150263) on a vector).

From these rules, we can derive the action of $\nabla_X$ on any tensor. For instance, to find the [covariant derivative](@entry_id:152476) of a $1$-form $\alpha$, we consider its contraction with a vector field $Z$, which is the scalar function $\alpha(Z)$. Applying the Leibniz rule and [commutativity](@entry_id:140240) with contraction yields:
$$
X(\alpha(Z)) = \nabla_X(\alpha(Z)) = C(\nabla_X(\alpha \otimes Z)) = C((\nabla_X \alpha)\otimes Z + \alpha \otimes (\nabla_X Z)) = (\nabla_X \alpha)(Z) + \alpha(\nabla_X Z)
$$
Rearranging this gives the definition of the covariant derivative of a $1$-form:
$$
(\nabla_X \alpha)(Z) = X(\alpha(Z)) - \alpha(\nabla_X Z)
$$

#### Defining $\nabla R$

Applying this machinery to the Riemann curvature tensor $R$, viewed as a $(1,3)$-tensor, allows us to define its [covariant derivative](@entry_id:152476), $\nabla R$, which is a $(1,4)$-tensor. For a direction $X$, the tensor $(\nabla_X R)$ is given by the Leibniz rule [@problem_id:3077211, 3077235]:
$$
(\nabla_X R)(Y,Z)W = \nabla_X(R(Y,Z)W) - R(\nabla_X Y, Z)W - R(Y, \nabla_X Z)W - R(Y,Z)\nabla_X W
$$
This expression captures the rate of change of the [curvature operator](@entry_id:198006) as one moves along the direction of $X$, correctly accounting for the variation of the input vector fields. It represents the first-order change in the infinitesimal holonomy $R(Y,Z)W$ along an [integral curve](@entry_id:276251) of $X$ [@problem_id:3077211].

In a local coordinate system $\{x^i\}$, this abstract definition translates into a concrete formula involving Christoffel symbols $\Gamma^k_{ij}$. The components of the [covariant derivative](@entry_id:152476) of the $(0,4)$ version of the curvature tensor, $R_{ijkl} = g(R(\partial_i,\partial_j)\partial_k, \partial_l)$, are given by [@problem_id:3003091]:
$$
\nabla_m R_{ijkl} = \partial_m R_{ijkl} - \Gamma^p_{im} R_{pjkl} - \Gamma^p_{jm} R_{ipkl} - \Gamma^p_{km} R_{ijpl} - \Gamma^p_{lm} R_{ijkp}
$$
Here, $\partial_m$ is the partial derivative with respect to the coordinate $x^m$, and the $\Gamma$ terms are corrections that ensure the entire object transforms as a tensor.

### The Second Bianchi Identity

With the definition of $\nabla R$ in hand, we can now state the second Bianchi identity. It establishes a fundamental relationship among the covariant derivatives of the [curvature tensor](@entry_id:181383) in different directions.

#### Statement of the Identity

The **second Bianchi identity** (also known as the differential Bianchi identity) asserts that the cyclic sum of the covariant derivative of the [curvature tensor](@entry_id:181383) over its first three arguments vanishes. In operator form, this is written as [@problem_id:3077235]:
$$
\operatorname{cyc}_{X,Y,Z}\,(\nabla_X R)(Y,Z)W = 0
$$
where the cyclic sum notation means:
$$
(\nabla_X R)(Y,Z)W + (\nabla_Y R)(Z,X)W + (\nabla_Z R)(X,Y)W = 0
$$
This identity holds for all [vector fields](@entry_id:161384) $X,Y,Z,W$. In [index notation](@entry_id:191923), this is expressed as [@problem_id:3077225]:
$$
\nabla_i R_{jk\ell m} + \nabla_j R_{ki\ell m} + \nabla_k R_{ij\ell m} = 0
$$
This is a differential identity, relating the values of curvature and its first derivatives at a point. This distinguishes it fundamentally from the **first Bianchi identity**, $R(X,Y)Z + R(Y,Z)X + R(Z,X)Y = 0$ (or $R_{ijkl}+R_{iklj}+R_{iljk}=0$ in [index form](@entry_id:183467)), which is a purely algebraic, pointwise symmetry of the tensor itself [@problem_id:3077225].

#### Geometric Interpretation: The Boundary of a Boundary

The second Bianchi identity has a profound geometric meaning, which can be understood by considering [parallel transport](@entry_id:160671) around an infinitesimal 3-dimensional cube [@problem_id:3077202, 3077211].

1.  The holonomy (change in a vector after [parallel transport](@entry_id:160671)) around an infinitesimal parallelogram with sides $\epsilon X, \epsilon Y$ is approximately given by the operator $I + \epsilon^2 R(X,Y)$.
2.  Consider an infinitesimal cube with sides $\epsilon X, \epsilon Y, \epsilon Z$. The boundary of this cube consists of six faces.
3.  The [holonomy](@entry_id:137051) around the "bottom" face in the $XY$-plane is $H_{XY} \approx I + \epsilon^2 R(X,Y)$. The [holonomy](@entry_id:137051) around the "top" face, displaced by $\epsilon Z$, depends on the curvature at that new point. The change in curvature is described by the covariant derivative, so the [holonomy](@entry_id:137051) on the top face is approximately $H'_{XY} \approx I + \epsilon^2(R(X,Y) + \epsilon(\nabla_Z R)(X,Y))$.
4.  The combined contribution from this pair of opposite faces to the total holonomy around the cube's boundary is approximately $H'_{XY} \circ H_{XY}^{-1} \approx I + \epsilon^3 (\nabla_Z R)(X,Y)$. The quadratic terms cancel, leaving a cubic term representing the change in holonomy.
5.  Summing the contributions from all three pairs of faces gives the total deviation from identity for the [holonomy](@entry_id:137051) around the cube's entire boundary:
    $$
    H_{cube} - I \approx \epsilon^3 \left[ (\nabla_X R)(Y,Z) + (\nabla_Y R)(Z,X) + (\nabla_Z R)(X,Y) \right]
    $$
A fundamental geometric principle states that the [holonomy](@entry_id:137051) around the boundary of a 3-cell has no cubic term. Therefore, the coefficient of $\epsilon^3$ must vanish. This gives exactly the second Bianchi identity. This interpretation reveals the identity as a manifestation of the topological principle that "the [boundary of a boundary is zero](@entry_id:269907)", often expressed in homology theory as $\partial^2=0$.

### Mechanisms and Consequences

The second Bianchi identity is not an accidental property but a deep consequence of the definitions of [connection and curvature](@entry_id:158520). It also leads to one of the most important equations in physics.

#### Algebraic Origin

The identity can be derived formally from the definitions. The proof relies on the **Jacobi identity** for operators, applied to the [covariant derivative](@entry_id:152476) operators $\nabla_X, \nabla_Y, \nabla_Z$ [@problem_id:3077235, 3077211]:
$$
[[\nabla_X, \nabla_Y], \nabla_Z] + [[\nabla_Y, \nabla_Z], \nabla_X] + [[\nabla_Z, \nabla_X], \nabla_Y] = 0
$$
By substituting the definition of curvature, $[ \nabla_X, \nabla_Y ]W = R(X,Y)W + \nabla_{[X,Y]}W$, and making use of the Jacobi identity for the Lie bracket of vector fields, this operator identity algebraically reduces to the second Bianchi identity. This derivation reveals that the identity is guaranteed for any connection that is **torsion-free**, meaning $T(X,Y) = \nabla_X Y - \nabla_Y X - [X,Y] = 0$. Since the Levi-Civita connection is torsion-free by definition, it must satisfy the second Bianchi identity. For a general connection with torsion $T$, the identity becomes $\operatorname{cyc}_{X,Y,Z}\,(\nabla_X R)(Y,Z) = \operatorname{cyc}_{X,Y,Z}\,R(T(X,Y),Z)$ [@problem_id:3077211].

It is critical to distinguish the second Bianchi identity from the much stronger condition $\nabla R = 0$. The Bianchi identity holds on *every* Riemannian manifold, whereas $\nabla R = 0$ defines a very special class of manifolds known as *[locally symmetric spaces](@entry_id:637873)* (e.g., Euclidean space, spheres) [@problem_id:3003092]. Furthermore, in dimension 2, the identity becomes a [tautology](@entry_id:143929) due to the linear dependence of any three vectors and provides no geometric constraint [@problem_id:3077211]. This is why certain theorems relying on this identity, like Schur's Lemma, require dimension $n \ge 3$.

#### Advanced Formulation and the Contracted Identity

A particularly elegant perspective comes from the language of exterior [differential forms](@entry_id:146747) [@problem_id:3003083, 3003087]. If the connection is represented by a matrix of [1-forms](@entry_id:157984) $\omega$, and the curvature by a matrix of [2-forms](@entry_id:188008) $\Omega$ through Cartan's structure equation $\Omega = d\omega + \omega \wedge \omega$, then the second Bianchi identity takes the remarkably compact form:
$$
d^{\nabla}\Omega = 0
$$
where $d^{\nabla}$ is the exterior covariant derivative. This equation, $d^{\nabla}\Omega = d\Omega + [\omega, \Omega] = 0$, can be shown to follow formally from the definition of $\Omega$ and the property $d^2=0$. This proves that the identity is an intrinsic structural feature of any connection, regardless of torsion.

The most celebrated application of the second Bianchi identity arises from its contracted form. By contracting the indices of $\nabla_i R_{jk\ell m} + \dots = 0$ twice, one arrives at a new identity involving the **Ricci tensor** ($\mathrm{Ric}_{ij} = R^k{}_{ikj}$) and the **[scalar curvature](@entry_id:157547)** ($R = g^{ij}\mathrm{Ric}_{ij}$). This **contracted Bianchi identity** states that the **Einstein tensor**, $G_{ij} = \mathrm{Ric}_{ij} - \frac{1}{2}R g_{ij}$, is [divergence-free](@entry_id:190991) [@problem_id:3077225]:
$$
\nabla^i G_{ij} = 0
$$
This conservation law is the mathematical backbone of Einstein's field equations in general relativity, where it ensures that the geometric side of the equation ($G_{ij}$) is compatible with the physical side (the stress-energy tensor $T_{ij}$), which is also conserved ($\nabla^i T_{ij} = 0$). The second Bianchi identity is thus not only a cornerstone of [differential geometry](@entry_id:145818) but a linchpin of [modern cosmology](@entry_id:752086) and physics.