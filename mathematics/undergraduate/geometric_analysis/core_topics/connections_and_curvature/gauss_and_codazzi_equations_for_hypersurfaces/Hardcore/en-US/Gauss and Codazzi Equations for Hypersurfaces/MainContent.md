## Introduction
The study of geometry often involves understanding how one object sits inside another. For a surface or a higher-dimensional object, known as a hypersurface, embedded in a larger ambient space, two distinct geometries emerge: the *intrinsic* geometry, which can be measured entirely from within the surface, and the *extrinsic* geometry, which describes how it bends and curves in the surrounding space. A fundamental question in differential geometry is how these two perspectives are related. What are the mathematical laws that connect the internal metric of a hypersurface to its external shape? This question reveals a deep and elegant structure at the heart of manifold theory.

This article addresses this central problem by developing the foundational equations of hypersurface theory: the Gauss and Codazzi equations. These equations act as the essential compatibility conditions that must be satisfied by any immersion. We will explore how they arise naturally from the decomposition of the ambient space's connection and how they encapsulate the intricate relationship between curvature, shape, and embedding.

Over the next three sections, you will gain a comprehensive understanding of this cornerstone of geometry. In "Principles and Mechanisms," we will derive the Gauss and Codazzi equations from first principles and discuss the powerful Fundamental Theorem of Hypersurfaces, which shows these equations are the complete set of local conditions for an immersion. Following this, "Applications and Interdisciplinary Connections" will demonstrate the profound impact of these equations, from the classical Theorema Egregium to their critical role as constraint equations in Einstein's theory of general relativity. Finally, "Hands-On Practices" will provide an opportunity to solidify these concepts through concrete calculations and problem-solving. We begin by building the essential machinery needed to analyze the geometry of an immersed hypersurface.

## Principles and Mechanisms

This chapter delves into the core principles that govern the geometry of hypersurfaces. Having established the foundational concepts in the introduction, we now develop the essential machinery for analyzing how a hypersurface $S$ sits inside an ambient Riemannian manifold $(M, g)$. The central theme is the relationship between the *intrinsic* geometry of the hypersurface, determined solely by its own metric, and its *extrinsic* geometry, which describes its shape and curvature as seen from the ambient space. This relationship is encoded in a set of fundamental equations, the Gauss and Codazzi equations, which act as compatibility conditions. Ultimately, we will see that these equations are so fundamental that they are not just consequences of an immersion; they are sufficient conditions for constructing an immersion with prescribed geometric properties.

Throughout this chapter, we let $(M, g)$ be a smooth $(n+1)$-dimensional Riemannian manifold with Levi-Civita connection $\bar{\nabla}$, and $i: S \to M$ be a smooth immersion of an $n$-dimensional manifold $S$, which we call a hypersurface. We denote the induced metric on $S$ by $g_S$ and its Levi-Civita connection by $\nabla$. For vector fields $X, Y, Z$ on $S$, the Riemann curvature tensor is defined by the convention $R(X,Y)Z = \nabla_X \nabla_Y Z - \nabla_Y \nabla_X Z - \nabla_{[X,Y]} Z$. Ambient quantities will be denoted with an overbar, such as $\bar{R}$ for the curvature of $M$.

### Geometric Preliminaries: The Tangent-Normal Decomposition

To study the geometry of the hypersurface $S$ within the ambient manifold $M$, our first task is to describe the relationship between their tangent spaces. At any point $p \in S$, the differential of the immersion, $di_p: T_pS \to T_{i(p)}M$, is an injective linear map. This allows us to identify the tangent space $T_pS$ with its image, an $n$-dimensional subspace of the $(n+1)$-dimensional tangent space $T_{i(p)}M$.

The ambient metric $g$ provides an inner product on each tangent space of $M$. This allows us to define the **normal space** to $S$ at $p$, denoted $N_pS$, as the orthogonal complement of $T_pS$ within $T_{i(p)}M$:
$$
N_pS = \{v \in T_{i(p)}M \mid g(v, w) = 0 \text{ for all } w \in T_pS \}
$$
Since $S$ is a hypersurface (codimension one), each normal space $N_pS$ is a one-dimensional vector space. At every point $p \in S$, we have an orthogonal decomposition of the ambient tangent space:
$$
T_{i(p)}M = T_pS \oplus N_pS
$$
This decomposition is fundamental to everything that follows.

A crucial tool for extrinsic geometry is a **unit normal vector field** $\nu$, which is a smooth choice of a unit-length vector $\nu(p) \in N_pS$ at each point $p \in S$. The existence of such a global, smooth, non-vanishing field is not guaranteed. It exists if and only if the normal line bundle $NS = \bigsqcup_{p \in S} N_pS$ is a trivial bundle. Geometrically, this means the hypersurface is **two-sided**; one can consistently define an "inside" and "outside". For instance, a Möbius strip embedded in $\mathbb{R}^3$ is one-sided and does not admit a global unit normal field.

The existence of $\nu$ is also related to orientability. If the ambient manifold $M$ is orientable, then $S$ admits a global unit normal field if and only if $S$ itself is orientable [@problem_id:3049783]. In our subsequent discussions, we will typically assume we are working on a region of $S$ that admits a smooth unit normal field $\nu$, which we refer to as an oriented hypersurface.

### Decomposing the Ambient Connection

The key to relating the intrinsic and extrinsic geometry of $S$ lies in analyzing the ambient Levi-Civita connection $\bar{\nabla}$. If $X$ and $Y$ are vector fields tangent to $S$, the covariant derivative $\bar{\nabla}_X Y$ is a vector field along $S$, but it is not necessarily tangent to $S$. For example, if you walk along a great circle (a geodesic) on a sphere in $\mathbb{R}^3$, your acceleration vector points towards the center of the sphere, normal to the surface.

Using the tangent-normal decomposition, we can split $\bar{\nabla}_X Y$ into its tangential and normal components:
$$
\bar{\nabla}_X Y = (\bar{\nabla}_X Y)^{\top} + (\bar{\nabla}_X Y)^{\perp}
$$
where $(\cdot)^{\top}$ denotes the orthogonal projection onto $TS$ and $(\cdot)^{\perp}$ denotes the orthogonal projection onto $NS$.

The tangential component defines a connection on $S$, which turns out to be precisely the Levi-Civita connection $\nabla$ of the induced metric $g_S$:
$$
\nabla_X Y := (\bar{\nabla}_X Y)^{\top}
$$
The normal component must be parallel to the unit normal vector $\nu$. We can therefore write it as $h(X,Y)\nu$ for some scalar function $h(X,Y)$. This function, which measures the extent to which $\bar{\nabla}_X Y$ fails to be tangent to $S$, is of paramount importance. It is called the **second fundamental form** of the hypersurface. By definition, we have:
$$
h(X,Y) = g(\bar{\nabla}_X Y, \nu)
$$
Combining these definitions gives the celebrated **Gauss formula**:
$$
\bar{\nabla}_X Y = \nabla_X Y + h(X,Y)\nu
$$
This equation is the first bridge between the intrinsic geometry of $S$ (captured by $\nabla$) and its extrinsic geometry (captured by $h$) [@problem_id:3049769]. The second fundamental form $h$ is a symmetric bilinear form on the tangent space. Its symmetry, $h(X,Y) = h(Y,X)$, is a direct consequence of the torsion-free property of the ambient connection $\bar{\nabla}$.

### The Shape Operator and the Weingarten Formula

The Gauss formula describes what happens to tangent vectors. To complete the picture, we must also describe what happens to the normal vector as we differentiate it along tangent directions. Differentiating the identity $g(\nu, \nu) = 1$ along a tangent vector field $X$ yields:
$$
0 = X(g(\nu,\nu)) = g(\bar{\nabla}_X \nu, \nu) + g(\nu, \bar{\nabla}_X \nu) = 2g(\bar{\nabla}_X \nu, \nu)
$$
This shows that the vector $\bar{\nabla}_X \nu$ is orthogonal to $\nu$. Since the normal space is one-dimensional, this implies that $\bar{\nabla}_X \nu$ must be a tangent vector. It lies in $T_pS$ for every $p \in S$.

This observation gives rise to the **shape operator** (or Weingarten map), which is a $(1,1)$-tensor field $A$ on $S$ that describes the change in the normal vector. It is defined by the **Weingarten formula**:
$$
AX = -\bar{\nabla}_X \nu
$$
The shape operator measures the "shape" of the hypersurface. For example, on a sphere, it is proportional to the identity map, indicating that the surface curves equally in all directions. The minus sign is a common convention that simplifies the relationship between $A$ and $h$.

To see this relationship, we differentiate the identity $g(Y, \nu) = 0$ along $X$:
$$
0 = X(g(Y,\nu)) = g(\bar{\nabla}_X Y, \nu) + g(Y, \bar{\nabla}_X \nu)
$$
The first term is exactly $h(X,Y)$. The second term involves the shape operator. Substituting the definitions gives:
$$
h(X,Y) + g(Y, -AX) = 0 \quad \implies \quad h(X,Y) = g(Y, AX)
$$
Since the metric $g$ is symmetric, we have the fundamental link between the second fundamental form and the shape operator:
$$
h(X,Y) = g(AX, Y)
$$
This relation shows that the shape operator $A$ is a self-adjoint (or symmetric) operator on the tangent space with respect to the induced metric $g_S$. Its eigenvalues are the **principal curvatures** of the hypersurface, and its eigenvectors give the corresponding **principal directions**.

### The Fundamental Equations of Compatibility

We now arrive at the central results of this chapter. The Gauss formula and the Weingarten formula decompose the first derivatives of vector fields. A natural step is to consider second derivatives, which leads to curvature. By applying these formulas to the definition of the ambient Riemann curvature tensor $\bar{R}$, we can decompose $\bar{R}$ and in doing so, we find two profound compatibility conditions that link the intrinsic and extrinsic geometry. These are the Gauss and Codazzi equations [@problem_id:3049763].

#### The Gauss Equation: The Origin of Intrinsic Curvature

Let $X, Y, Z, W$ be vector fields tangent to $S$. The Gauss equation arises from considering the tangential component of the ambient curvature operator $\bar{R}(X,Y)Z$. A detailed calculation involving repeated application of the Gauss and Weingarten formulas reveals that the intrinsic curvature tensor $R^S$ of the hypersurface is related to the ambient curvature $\bar{R}$ and the second fundamental form $h$ by the following equation:
$$
g_S(R^S(X,Y)Z, W) = g(\bar{R}(X,Y)Z, W) + h(X,Z)h(Y,W) - h(Y,Z)h(X,W)
$$
This is the **Gauss equation**. It is a cornerstone of geometry, famously leading Gauss to his *Theorema Egregium* for surfaces in $\mathbb{R}^3$. In that special case, the ambient space is flat, so $\bar{R}=0$, and the equation simplifies to show that the intrinsic curvature (the Gaussian curvature) is determined entirely by the second fundamental form: $K = \det(A)$.

The Gauss equation provides a profound insight: the intrinsic curvature of a submanifold is not simply the restriction of the ambient curvature. It is a combination of the ambient curvature and a term that is purely extrinsic, determined by how the surface bends via its second fundamental form [@problem_id:3049781].

A subtle but important question arises here. The second fundamental form $h$ and the shape operator $A$ both depend on the choice of the unit normal $\nu$; replacing $\nu$ with $-\nu$ reverses their signs. How can the intrinsic curvature $R^S$, which depends only on the metric $g_S$, be related to them? The answer lies in the structure of the Gauss equation. The second fundamental form appears quadratically, in products like $h(X,Z)h(Y,W)$. When we flip the sign of $\nu$, $h$ becomes $-h$, but the product $(-h)(X,Z)(-h)(Y,W)$ remains unchanged. Thus, the right-hand side of the Gauss equation is independent of the choice of normal, resolving the apparent paradox and beautifully demonstrating the consistency of the geometric framework [@problem_id:3049771].

#### The Codazzi Equation: Constraining the Extrinsic Curvature

The Gauss equation comes from the tangential component of the ambient curvature. The normal component yields the second fundamental equation of compatibility, known as the **Codazzi-Mainardi equation**, or simply the **Codazzi equation**. This equation relates the normal component of the ambient curvature to the covariant derivative of the second fundamental form.

First, we must define the covariant derivative of the tensor $h$. As $h$ is a $(0,2)$-tensor field on $S$, its covariant derivative with respect to the induced connection $\nabla$ is given by:
$$
(\nabla_X h)(Y,Z) = X(h(Y,Z)) - h(\nabla_X Y, Z) - h(Y, \nabla_X Z)
$$
This measures the rate of change of the second fundamental form as we move in the direction $X$ on the hypersurface.

The Codazzi equation is derived by computing the normal component of $\bar{R}(X,Y)Z$, which is $g(\bar{R}(X,Y)Z, \nu)$. Another careful calculation shows that this quantity is related to the covariant derivatives of $h$ as follows:
$$
g(\bar{R}(X,Y)Z, \nu) = (\nabla_X h)(Y,Z) - (\nabla_Y h)(X,Z)
$$
This equation implies that the tensor $(\nabla_X h)(Y,Z)$ is symmetric in the variables $X$ and $Y$. It provides a constraint on how the second fundamental form can vary across the hypersurface. In a flat ambient space ($\bar{R}=0$), the equation simplifies to $(\nabla_X h)(Y,Z) = (\nabla_Y h)(X,Z)$, which in local coordinates becomes the classical condition $h_{ij;k} = h_{ik;j}$ [@problem_id:3049747] [@problem_id:3049737].

### The Fundamental Theorem of Hypersurfaces

We have seen that any immersed hypersurface must satisfy the Gauss and Codazzi equations. A profound question, answered by the Fundamental Theorem of Hypersurfaces, is whether the converse is true. That is, if we are given a Riemannian metric $g_S$ and a symmetric $(0,2)$-tensor $h$ on a manifold $S$, can we find an immersion of $S$ into an ambient space (e.g., Euclidean space $\mathbb{R}^{n+1}$) such that $g_S$ and $h$ are its first and second fundamental forms?

The answer is yes, provided that $g_S$ and $h$ satisfy the Gauss and Codazzi equations, and with a topological condition on $S$.

#### Existence and Uniqueness

**The Fundamental Theorem of Hypersurfaces** states that if $(S, g_S)$ is a simply connected $n$-dimensional Riemannian manifold, and $h$ is a smooth symmetric $(0,2)$-tensor field on $S$ such that the pair $(g_S, h)$ satisfies the Gauss and Codazzi equations for an ambient space of constant curvature $\kappa$, then there exists an isometric immersion $F: S \to X^{n+1}(\kappa)$ into the $(n+1)$-dimensional space form of constant curvature $\kappa$. Furthermore, this immersion is unique up to a rigid motion (an isometry) of the ambient space $X^{n+1}(\kappa)$ [@problem_id:3049773].

This theorem is a pillar of geometry, showing that the Gauss and Codazzi equations are the complete set of local conditions for a metric and a shape tensor to be realized by a hypersurface.

#### The Mechanism: Integrability of Structure Equations

The proof of this theorem reveals why the Gauss and Codazzi equations play this central role. The construction of the immersion $F$ is recast as solving a system of first-order partial differential equations for a "moving frame" that is adapted to the hypersurface. This frame consists of the position vector $F(p)$ and an orthonormal basis for $T_{F(p)}M$ composed of tangent vectors and the normal vector.

The system of PDEs describes how this frame changes from point to point, governed by a connection whose components are built from the given data $(g_S, h)$. The **Gauss and Codazzi equations are precisely the integrability conditions** for this system of PDEs. In the language of modern geometry, they ensure that the constructed connection is flat (i.e., has zero curvature). The Frobenius Integrability Theorem then guarantees that, on a local neighborhood, this system has a unique solution for any given initial position and orientation of the frame. This solution gives the desired local immersion [@problem_id:3049766].

#### The Role of Topology: Monodromy

The theorem's hypothesis that $S$ must be **simply connected** is essential for global uniqueness. On a simply connected manifold, the flatness of the connection ensures that parallel transport is path-independent. This allows one to integrate the local solutions into a single, well-defined global immersion, which is unique up to the choice of the initial frame (a rigid motion).

If $S$ is not simply connected (for example, a torus), path-dependence can arise. Parallel transporting a frame around a non-contractible loop may result in a different frame. This phenomenon is called **monodromy** or **holonomy**, and it is captured by a homomorphism $\rho: \pi_1(S) \to \mathrm{Isom}(X)$, where $\pi_1(S)$ is the fundamental group of $S$ and $\mathrm{Isom}(X)$ is the isometry group of the ambient space $X$.

In this case, an immersion of $S$ may only exist if its lift to the universal cover $\tilde{S}$ is equivariant with respect to such a monodromy representation. The data $(g_S, h)$ determines a class of possible monodromy representations, but different representations within this class can lead to distinct, non-congruent immersions of $S$ into $X$. Therefore, for a non-simply connected manifold, specifying the immersion uniquely requires specifying not only the local data $(g_S, h)$ but also the global monodromy representation $\rho$ [@problem_id:3049758]. This reveals a beautiful interplay between the local differential geometry encoded by the Gauss-Codazzi equations and the global topology of the manifold.