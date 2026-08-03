## Introduction
In the study of differential geometry, we model curved spaces as manifolds, each point of which possesses a flat tangent space representing all possible "velocities" or directional derivatives. A fundamental question arises: when we have a smooth map from one manifold to another, how does it transform these tangent vectors? How can we mathematically describe the way a particle's velocity on a surface is affected by a projection or transformation of that surface?

This knowledge gap is bridged by a crucial concept known as the **pushforward**, also called the tangent map or differential. The pushforward provides a rigorous way to "push" a tangent vector from a source manifold to a target manifold. It is the best linear approximation of the map at a given point, acting on vectors. This article will guide you through this fundamental concept, equipping you with the tools to understand and apply it. In **Principles and Mechanisms**, we will establish the formal definitions of the pushforward and its concrete representation as the Jacobian matrix. Following this, **Applications and Interdisciplinary Connections** will showcase its power in diverse fields like physics, engineering, and Lie theory. Finally, **Hands-On Practices** will provide targeted exercises to solidify your computational and geometric understanding of the pushforward.

## Principles and Mechanisms

In our study of manifolds, we have established that at each point $p$ on a manifold $M$, there exists a vector space of tangent vectors, $T_p M$. These vectors represent infinitesimal displacements or velocities of curves passing through $p$. A central question in differential geometry is how a smooth map between two manifolds, $F: M \to N$, affects these tangent vectors. The answer lies in a fundamental construction known as the **pushforward**. The pushforward, also called the differential or tangent map, provides a canonical way to "push" a tangent vector from the source manifold's tangent space to the target manifold's tangent space. It is, in essence, the best linear approximation of the map $F$ at a point, applied to tangent vectors.

### Formal Definitions of the Pushforward

The concept of the pushforward can be formalized in several equivalent ways. Each definition provides a unique perspective on its nature and utility. We will explore the two most common definitions: one based on curves and another based on the action of vectors on functions.

#### The Velocity Vector of a Transformed Curve

Perhaps the most intuitive way to understand the pushforward is by considering its effect on the velocity vectors of curves. A tangent vector $v \in T_p M$ can always be realized as the velocity vector of some smooth curve $\gamma: (-\epsilon, \epsilon) \to M$ such that $\gamma(0) = p$ and the derivative of the curve with respect to its parameter $t$, evaluated at $t=0$, is $v$. We write this as $\gamma'(0) = v$.

Given a smooth map $F: M \to N$, we can apply this map to the entire curve $\gamma(t)$ to obtain a new curve, $\sigma(t) = F(\gamma(t))$, which lies in the manifold $N$. This new curve passes through the point $F(p)$ at $t=0$. The velocity vector of this transformed curve at $t=0$ is a tangent vector in the tangent space $T_{F(p)}N$. We define this new velocity vector to be the pushforward of $v$.

Formally, the **pushforward** of a vector $v \in T_p M$ under a map $F: M \to N$, denoted $(F_*)_p(v)$ or simply $F_*(v)$, is defined as:
$$
(F_*)_p(v) = \frac{d}{dt}\bigg|_{t=0} (F \circ \gamma)(t)
$$
where $\gamma(t)$ is any smooth curve in $M$ satisfying $\gamma(0) = p$ and $\gamma'(0) = v$.

A crucial aspect of this definition is that the resulting vector $(F_*)_p(v)$ is independent of the particular choice of curve $\gamma(t)$ used to represent $v$. Any two curves, say $\gamma_1(t)$ and $\gamma_2(t)$, that satisfy the conditions $\gamma_1(0) = \gamma_2(0) = p$ and $\gamma_1'(0) = \gamma_2'(0) = v$ will yield the same pushforward vector. In local coordinates, this independence can be verified using the chain rule, which shows that the result only depends on the first derivative of the curve at $t=0$, which is the vector $v$ itself [@problem_id:1534290]. This definition beautifully captures the idea that the pushforward transforms the "velocity" of a path in $M$ into the corresponding "velocity" of the image path in $N$.

#### Action on Functions and the Duality with Pullbacks

An alternative, more abstract definition arises from the interpretation of tangent vectors as derivations on smooth functions. Recall that a tangent vector $v \in T_p M$ can be viewed as a linear operator that takes a smooth real-valued function $g: M \to \mathbb{R}$ and returns its directional derivative at $p$ along $v$, a real number denoted $v[g]$.

The pushforward vector, $(F_*)_p(v)$, should be an element of $T_{F(p)}N$, and therefore it must be capable of acting on smooth functions defined on $N$. Let $h: N \to \mathbb{R}$ be a smooth function. How should $(F_*)_p(v)$ act on $h$? The only way for the vector $v \in T_p M$ to interact with the function $h$ is to first "pull back" $h$ to the manifold $M$. The composition $h \circ F$ is a smooth function from $M$ to $\mathbb{R}$. Since $v$ is a derivation at $p \in M$, it can act on this composite function. This leads to our second definition.

The pushforward vector $(F_*)_p(v) \in T_{F(p)}N$ is the unique tangent vector whose action on any smooth function $h: N \to \mathbb{R}$ is given by:
$$
((F_*)_p(v))[h] = v[h \circ F]
$$
This definition elegantly connects the pushforward with the **pullback** of functions, denoted $F^*h = h \circ F$. The equation can be rewritten as $(F_*v)[h] = v[F^*h]$.

A special and important case arises when the target manifold $N$ is the real line $\mathbb{R}$ itself, so we have a function $F: M \to \mathbb{R}$. The tangent space at any point $F(p) \in \mathbb{R}$ can be identified with $\mathbb{R}$, with the basis vector being $\frac{d}{dt}|_{F(p)}$. The pushforward $F_*(v)$ is therefore just a number times this basis vector. This number is precisely the directional derivative of $F$ along $v$, which is $v[F]$ [@problem_id:1534294]. In this context, the definition becomes $(F_*(v)) = v[F] \frac{d}{dt}|_{F(p)}$, which directly identifies the pushforward with the action of the vector on the function itself.

### The Pushforward in Local Coordinates: The Jacobian Matrix

While the formal definitions are conceptually vital, for practical computations we almost always work in local coordinates. In this setting, the pushforward reveals itself to be a familiar operation from multivariable calculus: multiplication by the Jacobian matrix.

Let $F: M \to N$ be a smooth map between an $n$-dimensional manifold $M$ and an $m$-dimensional manifold $N$. Let $p \in M$ and choose a coordinate chart $(U, \phi)$ around $p$ with coordinates $(x^1, \dots, x^n)$, and a chart $(V, \psi)$ around $F(p)$ with coordinates $(y^1, \dots, y^m)$. In these coordinates, the map $F$ can be expressed by $m$ component functions:
$$
y^j = F^j(x^1, \dots, x^n), \quad \text{for } j=1, \dots, m
$$
A tangent vector $v \in T_p M$ can be written in the coordinate basis as $v = \sum_{i=1}^n v^i \frac{\partial}{\partial x^i}\big|_p$. Its pushforward, $(F_*)_p(v) \in T_{F(p)}N$, will have components in the target coordinate basis: $(F_*)_p(v) = \sum_{j=1}^m w^j \frac{\partial}{\partial y^j}\big|_{F(p)}$. Our goal is to find the relationship between the components $w^j$ and $v^i$.

Using the action-on-functions definition, let's have the pushforward vector act on a coordinate function $y^k$ on $N$.
$$
w^k = ((F_*)_p(v))[y^k] = v[y^k \circ F] = v[F^k]
$$
Substituting the component form of $v$, we get:
$$
w^k = \left(\sum_{i=1}^n v^i \frac{\partial}{\partial x^i}\bigg|_p\right)[F^k] = \sum_{i=1}^n v^i \frac{\partial F^k}{\partial x^i}\bigg|_p
$$
This equation reveals the transformation rule for the components. In matrix form, this is:
$$
\begin{pmatrix} w^1 \\ w^2 \\ \vdots \\ w^m \end{pmatrix} = \begin{pmatrix}
\frac{\partial y^1}{\partial x^1} & \frac{\partial y^1}{\partial x^2} & \cdots & \frac{\partial y^1}{\partial x^n} \\
\frac{\partial y^2}{\partial x^1} & \frac{\partial y^2}{\partial x^2} & \cdots & \frac{\partial y^2}{\partial x^n} \\
\vdots & \vdots & \ddots & \vdots \\
\frac{\partial y^m}{\partial x^1} & \frac{\partial y^m}{\partial x^2} & \cdots & \frac{\partial y^m}{\partial x^n}
\end{pmatrix}_{p}
\begin{pmatrix} v^1 \\ v^2 \\ \vdots \\ v^n \end{pmatrix}
$$
The $m \times n$ matrix of partial derivatives is the **Jacobian matrix** of the map $F$ at the point $p$, denoted $(J_F)_p$ or $DF_p$. Thus, in local coordinates, the pushforward operation is simply the multiplication of a vector's components by the Jacobian matrix.

#### Illustrative Examples

Let's ground this concept with a few examples.

- **Linear Transformations:** Consider a linear transformation $L: \mathbb{R}^n \to \mathbb{R}^m$. Such a map is given by $y^j = \sum_i A^j_i x^i$ for some constant matrix $A$. The partial derivatives are $\frac{\partial y^j}{\partial x^i} = A^j_i$, so the Jacobian matrix $J_L$ is simply the matrix $A$ itself, and it is constant for all points $p \in \mathbb{R}^n$. Thus, for a linear map, the pushforward is the linear map itself, acting on the vector components [@problem_id:1534305]. For instance, if $L: \mathbb{R}^3 \to \mathbb{R}^2$ is given by $L(x, y, z) = (4x - 2z, 3y + x)$, its Jacobian matrix is $\begin{pmatrix} 4 & 0 & -2 \\ 1 & 3 & 0 \end{pmatrix}$. The pushforward of a vector $v_p$ with components $(5, -1, 2)$ is found by matrix multiplication:
$$
\begin{pmatrix} 4 & 0 & -2 \\ 1 & 3 & 0 \end{pmatrix} \begin{pmatrix} 5 \\ -1 \\ 2 \end{pmatrix} = \begin{pmatrix} 16 \\ 2 \end{pmatrix}
$$
The resulting vector has components $(16, 2)$ in the target tangent space.

- **Non-Linear Maps:** The power of the Jacobian formulation becomes more apparent with non-linear maps, where the matrix itself depends on the point $p$. Consider a map $\Phi: \mathbb{R}^2 \to \mathbb{R}^3$ given by $\Phi(u, v) = (u \cos v, u \sin v, u^2)$, which parameterizes a paraboloid [@problem_id:1534277]. The Jacobian matrix is:
$$
J_{\Phi}(u,v) = \begin{pmatrix} \frac{\partial x}{\partial u} & \frac{\partial x}{\partial v} \\ \frac{\partial y}{\partial u} & \frac{\partial y}{\partial v} \\ \frac{\partial z}{\partial u} & \frac{\partial z}{\partial v} \end{pmatrix} = \begin{pmatrix} \cos v & -u \sin v \\ \sin v & u \cos v \\ 2u & 0 \end{pmatrix}
$$
To push forward a vector $V_P = 3 \frac{\partial}{\partial u} - 2 \frac{\partial}{\partial v}$ at the point $P=(u_0, v_0) = (2, \pi/4)$, we first evaluate the Jacobian at $P$:
$$
(J_{\Phi})_P = \begin{pmatrix} \sqrt{2}/2 & -\sqrt{2} \\ \sqrt{2}/2 & \sqrt{2} \\ 4 & 0 \end{pmatrix}
$$
Then, we multiply this matrix by the component vector of $V_P$, which is $\begin{pmatrix} 3 \\ -2 \end{pmatrix}$:
$$
(\Phi_*)_P(V_P) = \begin{pmatrix} \sqrt{2}/2 & -\sqrt{2} \\ \sqrt{2}/2 & \sqrt{2} \\ 4 & 0 \end{pmatrix} \begin{pmatrix} 3 \\ -2 \end{pmatrix} = \begin{pmatrix} \frac{3\sqrt{2}}{2} + 2\sqrt{2} \\ \frac{3\sqrt{2}}{2} - 2\sqrt{2} \\ 12 \end{pmatrix} = \begin{pmatrix} \frac{7\sqrt{2}}{2} \\ -\frac{\sqrt{2}}{2} \\ 12 \end{pmatrix}
$$
The resulting vector resides in the tangent space of $\mathbb{R}^3$ at the point $\Phi(P)$.

- **Projections:** Maps can reduce dimensionality, and the pushforward reflects this. Consider the canonical projection $\Phi: \mathbb{R}^3 \to \mathbb{R}^2$ given by $\Phi(x, y, z) = (x, y)$ [@problem_id:1534282]. The Jacobian is a constant $2 \times 3$ matrix:
$$
J_{\Phi} = \begin{pmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \end{pmatrix}
$$
When this acts on a vector with components $(v_x, v_y, v_z)$, the result is $\begin{pmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \end{pmatrix} \begin{pmatrix} v_x \\ v_y \\ v_z \end{pmatrix} = \begin{pmatrix} v_x \\ v_y \end{pmatrix}$. The pushforward simply extracts the first two components, effectively discarding any information about the vector's component in the $z$-direction.

### Core Properties of the Pushforward

The pushforward inherits several fundamental properties from its definition as the linearization of a smooth map.

- **Linearity:** For a fixed point $p \in M$, the map $(F_*)_p: T_p M \to T_{F(p)} N$ is a linear transformation between vector spaces. This means for any vectors $v, w \in T_p M$ and scalars $a, b \in \mathbb{R}$, we have $(F_*)_p(av + bw) = a(F_*)_p(v) + b(F_*)_p(w)$. This is immediately obvious from the Jacobian matrix representation.

- **The Chain Rule for Manifolds:** One of the most important properties is how the pushforward behaves under composition of maps. If $F: M \to N$ and $G: N \to P$ are smooth maps, then the composite map $G \circ F: M \to P$ is also smooth. The pushforward of this composite map is the composition of the individual pushforwards:
$$
((G \circ F)_*)_p = (G_*)_{F(p)} \circ (F_*)_p
$$
In terms of Jacobian matrices, this is a restatement of the multivariable chain rule: $J_{G \circ F}(p) = J_G(F(p)) \cdot J_F(p)$. This property ensures that our notion of differentiation on manifolds is consistent and compositional [@problem_id:1666517].

- **Behavior under Invertible Maps:** If a map $F: M \to N$ is a **diffeomorphism** (i.e., it is smooth, bijective, and has a smooth inverse $F^{-1}: N \to M$), then its pushforward $(F_*)_p: T_p M \to T_{F(p)} N$ is a vector space isomorphism for every $p \in M$. This means it is an invertible linear map. The pushforward of the inverse map, $((F^{-1})_*)_{F(p)}$, is the inverse of the original pushforward map:
$$
((F^{-1})_*)_{F(p)} = ((F_*)_p)^{-1}
$$
In terms of Jacobian matrices, this means $J_{F^{-1}}(F(p)) = (J_F(p))^{-1}$. This property is immensely useful, as it allows us to transform tangent vectors back and forth between diffeomorphic manifolds without loss of information [@problem_id:1534263].

### Geometric Interpretation: The Kernel of the Pushforward

Since $(F_*)_p$ is a linear map between vector spaces, we can analyze it using the tools of linear algebra, specifically by examining its kernel and image.

The **kernel** of the pushforward at a point $p$, denoted $\ker((F_*)_p)$, is the set of all tangent vectors $v \in T_p M$ that are mapped to the zero vector in $T_{F(p)}N$:
$$
\ker((F_*)_p) = \{ v \in T_p M \mid (F_*)_p(v) = 0 \}
$$
Geometrically, the kernel consists of vectors representing directions of infinitesimal motion at $p$ that are "invisible" to the map $F$. If you move an infinitesimal distance along such a vector, the image point $F(p)$ does not move (to first order).

For a map $F: \mathbb{R}^n \to \mathbb{R}^m$, finding the kernel of the pushforward is equivalent to finding the null space of the Jacobian matrix $J_F$. For example, with the projection map $\Phi(x, y, z) = (x, y)$ [@problem_id:1534282], the Jacobian is $\begin{pmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \end{pmatrix}$. A vector $(v_x, v_y, v_z)$ is in the kernel if its pushforward $(v_x, v_y)$ is zero, which implies $v_x=0$ and $v_y=0$. Thus, the kernel is spanned by the vector $\frac{\partial}{\partial z}$, representing the direction that is projected away.

When the target is $\mathbb{R}$, as in a function $F: M \to \mathbb{R}$, the condition for a vector $v$ to be in the kernel of $F_*$ is $F_*(v) = 0$. This is equivalent to stating that the directional derivative of $F$ in the direction $v$ is zero: $v[F] = 0$. In Euclidean space, this is the condition $\nabla F \cdot v = 0$. This means the kernel of $F_*$ at a point $p$ is the tangent space to the level set of $F$ passing through $p$ [@problem_id:1534308].

The kernel is a vector subspace of $T_pM$, and its dimension can be found using the rank-nullity theorem. A basis for this subspace can be found by solving the linear system $J_F \cdot v = 0$ for the components of $v$ [@problem_id:1534274]. The dimension of the kernel provides crucial information about the local behavior of the map, indicating directions of "collapse" or information loss. This concept is central to the definitions of immersions and submersions and is a cornerstone of the interplay between analysis and geometry on manifolds.