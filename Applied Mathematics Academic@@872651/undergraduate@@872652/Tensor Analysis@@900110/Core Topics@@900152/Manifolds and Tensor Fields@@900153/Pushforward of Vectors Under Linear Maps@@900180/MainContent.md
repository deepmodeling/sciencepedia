## Introduction
When we study transformations between spaces, we often focus on where points are mapped. However, in science and engineering, we must also consider how directional quantities, such as velocity or force, are transformed. If a robotic arm moves its joints, how does that translate to the velocity of its gripper? If a material deforms, how does a vector embedded within it change? The mathematical framework for answering these questions is built around a concept known as the **[pushforward](@entry_id:158718)**. It provides a rigorous and systematic method for "pushing" [tangent vectors](@entry_id:265494) from a source space to a [target space](@entry_id:143180), addressing the knowledge gap between mapping points and transforming the vector information associated with them.

This article provides a comprehensive introduction to the pushforward, structured to build your understanding from foundational principles to practical applications.
- In **Principles and Mechanisms**, we will formally define the [pushforward](@entry_id:158718), first examining its simple and intuitive behavior under linear and affine maps, and then generalizing to nonlinear maps through the use of the Jacobian matrix.
- The next chapter, **Applications and Interdisciplinary Connections**, will demonstrate the broad utility of the [pushforward](@entry_id:158718) in diverse fields such as physics, robotics, and continuum mechanics, revealing it as a unifying concept for analyzing transformations.
- Finally, **Hands-On Practices** will guide you through targeted exercises to solidify your computational skills and deepen your conceptual grasp of the material.

## Principles and Mechanisms

In our study of transformations between spaces, we are interested not only in where points are mapped, but also in how directional information at those points is transformed. If we imagine a [smooth map](@entry_id:160364) $f$ from a space $M$ to a space $N$, and a particle moving along a path in $M$, its velocity vector describes the instantaneous direction and speed of its motion. The map $f$ transports this particle to a new path in $N$, which will have its own velocity vector. The **[pushforward](@entry_id:158718)** is the mathematical operation that directly relates the original velocity vector to the new one. It provides a systematic way to "push forward" [tangent vectors](@entry_id:265494) from one space to another.

### Defining the Pushforward: Transforming Velocities

Let us formalize this intuitive idea. Consider a [smooth map](@entry_id:160364) $f: M \to N$ between two manifolds (for instance, Euclidean spaces like $\mathbb{R}^n$). A **[tangent vector](@entry_id:264836)** $v$ at a point $p \in M$ can be understood as the velocity of some curve $\gamma: (-\epsilon, \epsilon) \to M$ that passes through $p$ at $t=0$, such that $\gamma(0) = p$ and its velocity vector $\gamma'(0) = v$.

The map $f$ takes the curve $\gamma(t)$ in $M$ and creates a new curve, the composite curve $f \circ \gamma$, in $N$. This new curve passes through the point $f(p)$ at $t=0$. The velocity vector of this new curve at $t=0$ is, by definition, the pushforward of the original vector $v$ by the map $f$. We denote the [pushforward](@entry_id:158718) of $v$ by $f_*(v)$ or, more precisely, $(f_*)_p(v)$ to emphasize its dependence on the point $p$.

Formally, the [pushforward](@entry_id:158718) $(f_*)_p(v)$ is a [tangent vector](@entry_id:264836) in the [tangent space](@entry_id:141028) at $f(p)$, denoted $T_{f(p)}N$, and is defined as:
$$
(f_*)_p(v) = \frac{d}{dt}\bigg|_{t=0} (f \circ \gamma)(t)
$$
A fundamental property of this definition is that the result is independent of the specific curve $\gamma$ chosen, so long as it satisfies the conditions $\gamma(0)=p$ and $\gamma'(0)=v$. Any two such curves will yield the same pushforward vector, making the operation well-defined.

### The Case of Linear and Affine Maps

The structure of the pushforward becomes particularly clear when the map itself is linear. Consider a [linear map](@entry_id:201112) $L: \mathbb{R}^n \to \mathbb{R}^m$. Let $v \in T_p\mathbb{R}^n$ be a tangent vector at a point $p \in \mathbb{R}^n$. We can represent $v$ using the simple curve $\gamma(t) = p + tv$. This curve satisfies $\gamma(0)=p$ and $\gamma'(0)=v$.

To find the pushforward $L_*(v)$, we first form the composite curve $L \circ \gamma$:
$$
(L \circ \gamma)(t) = L(p + tv)
$$
Because $L$ is a linear map, it distributes over addition and scalar multiplication:
$$
L(p + tv) = L(p) + tL(v)
$$
Now, we compute the velocity of this new curve by differentiating with respect to $t$:
$$
\frac{d}{dt} (L(p) + tL(v)) = L(v)
$$
The result, $L(v)$, is a constant vector. Evaluating at $t=0$ gives us the pushforward: $L_*(v) = L(v)$.

This reveals a profound simplification: **for a linear map, the pushforward operation is identical to the [linear map](@entry_id:201112) itself acting on the vector**. The [pushforward](@entry_id:158718) map, $L_*$, is independent of the point $p$ at which the tangent vector is based. For example, if we have a linear map $L: \mathbb{R}^2 \to \mathbb{R}^3$ given by $L(x_1, x_2) = (x_1 + 2x_2, 3x_1 - x_2, 4x_1)$ and a [tangent vector](@entry_id:264836) with components $(2, -3)$ at the point $p=(1,1)$, the [pushforward](@entry_id:158718) is simply the result of applying $L$ to the vector's components: $L(2, -3) = (2 + 2(-3), 3(2) - (-3), 4(2)) = (-4, 9, 8)$. This can be verified by explicitly using the curve definition, which yields the same result [@problem_id:1534563].

This principle extends directly to **affine maps**, which are of the form $f(\mathbf{x}) = A\mathbf{x} + \mathbf{b}$, where $A$ is a [linear transformation](@entry_id:143080) (a matrix) and $\mathbf{b}$ is a constant translation vector. Following the same procedure with a curve $\gamma(t) = p + tv$:
$$
(f \circ \gamma)(t) = A(p+tv) + \mathbf{b} = A(p) + tA(v) + \mathbf{b}
$$
When we differentiate with respect to $t$, the constant terms $A(p)$ and $\mathbf{b}$ vanish:
$$
\frac{d}{dt} (A(p) + tA(v) + \mathbf{b}) = A(v)
$$
Thus, for an affine map, the pushforward $(f_*)_p(v)$ is just $A(v)$. The translational part $\mathbf{b}$ and the point of application $p$ have no effect on the transformation of the vector. The pushforward is determined entirely by the linear part of the map [@problem_id:1534585].

The concept is not limited to Euclidean spaces. Consider the vector space $V$ of all $2 \times 2$ matrices and the [linear map](@entry_id:201112) $f: V \to V$ defined by transposition, $f(A) = A^T$. The pushforward of a tangent vector $B \in T_A V \cong V$ is found to be $(f_*)_A(B) = B^T$. Once again, the [pushforward](@entry_id:158718) is simply the [linear map](@entry_id:201112) itself, independent of the point $A$ [@problem_id:1534551].

### Generalization to Nonlinear Maps: The Jacobian Matrix

For a general nonlinear [smooth map](@entry_id:160364) $f: \mathbb{R}^n \to \mathbb{R}^m$, the situation is more complex but follows the same core idea. The pushforward $(f_*)_p$ can no longer be the map $f$ itself, but it still acts as a linear transformation on tangent vectors. It is, in fact, the **[best linear approximation](@entry_id:164642)** of the map's action on vectors in the infinitesimal neighborhood of the point $p$. This linear approximation is given by the **Jacobian matrix** of the map.

Let the map $f$ be given by component functions $f(\mathbf{x}) = (y_1(\mathbf{x}), \dots, y_m(\mathbf{x}))$, where $\mathbf{x} = (x_1, \dots, x_n)$. Let a [tangent vector](@entry_id:264836) $v$ at $p$ have components $(v_1, \dots, v_n)$. The components of the pushforward vector $w = (f_*)_p(v)$ are given by the [multivariable chain rule](@entry_id:146671):
$$
w_j = \sum_{i=1}^{n} \frac{\partial y_j}{\partial x_i}\bigg|_{p} v_i
$$
This relationship can be expressed in matrix form:
$$
\begin{pmatrix} w_1 \\ \vdots \\ w_m \end{pmatrix} = \begin{pmatrix} \frac{\partial y_1}{\partial x_1}  \cdots  \frac{\partial y_1}{\partial x_n} \\ \vdots  \ddots  \vdots \\ \frac{\partial y_m}{\partial x_1}  \cdots  \frac{\partial y_m}{\partial x_n} \end{pmatrix}_p \begin{pmatrix} v_1 \\ \vdots \\ v_n \end{pmatrix}
$$
The matrix of [partial derivatives](@entry_id:146280), evaluated at the point $p$, is the Jacobian matrix of $f$ at $p$, denoted $J_f(p)$ or $Df|_p$. So, the action of the [pushforward](@entry_id:158718) on the components of a vector is simply multiplication by the Jacobian matrix: $[(f_*)_p(v)] = J_f(p) [v]$.

A crucial distinction from the linear case emerges: for a nonlinear map, the Jacobian matrix $J_f(p)$ typically depends on the point $p$. This means **the pushforward transformation itself changes from point to point**.

For instance, consider the map $f(x,y) = (\exp(x)\cos(y), \exp(x)\sin(y))$, which transforms Cartesian coordinates to a version of polar coordinates [@problem_id:1534554]. Its Jacobian matrix is:
$$
J_f(x,y) = \begin{pmatrix} \exp(x)\cos(y)  -\exp(x)\sin(y) \\ \exp(x)\sin(y)  \exp(x)\cos(y) \end{pmatrix}
$$
The pushforward of a vector $(a,b)$ at a point $(x_0, y_0)$ will depend explicitly on $x_0$ and $y_0$. Similarly, for a map like $f(u,v) = (v\cos u, v\sin u, v)$ which maps a plane to a cone, the [pushforward](@entry_id:158718) of a vector at $(u_0, v_0)$ depends on these coordinates [@problem_id:1534559]. The point-dependence is made especially clear in a map like $f(x,y) = (x, y/x)$; the [pushforward](@entry_id:158718) of a vector $(A, B)$ at $(x_0, y_0)$ results in a new vector whose second component, $-A(y_0/x_0^2) + B/x_0$, is a function of the point $(x_0, y_0)$ [@problem_id:1534566].

### Fundamental Properties of the Pushforward

The pushforward operation adheres to several essential algebraic rules that make it a cornerstone of [differential geometry](@entry_id:145818).

#### The Chain Rule
If we have a sequence of [smooth maps](@entry_id:203730), say $M \xrightarrow{f} N \xrightarrow{g} P$, we can either compose the maps first to get $g \circ f$ and then compute the pushforward, or we can compute the pushforward of each map and compose the resulting [linear transformations](@entry_id:149133). The [chain rule for pushforwards](@entry_id:199545) states that these two procedures give the same result:
$$
(g \circ f)_* = g_* \circ f_*
$$
This property is sometimes called the "[functoriality](@entry_id:150069)" of the [pushforward](@entry_id:158718). Intuitively, it means that transforming a velocity vector first by $f$ and then by $g$ is identical to transforming it by the single composite map $g \circ f$. In terms of Jacobians, this corresponds to the [chain rule](@entry_id:147422) for [multivariable calculus](@entry_id:147547): $J_{g \circ f}(p) = J_g(f(p)) \cdot J_f(p)$. This can be verified with simple [linear maps](@entry_id:185132), such as composing a scaling and a rotation [@problem_id:1534573].

#### Inverse Maps
A powerful consequence of the [chain rule](@entry_id:147422) applies to invertible maps, or **diffeomorphisms**. If a map $f: M \to N$ is a [diffeomorphism](@entry_id:147249) with inverse $f^{-1}: N \to M$, their composition is the identity map: $f^{-1} \circ f = \text{id}_M$. Applying the [pushforward](@entry_id:158718) [chain rule](@entry_id:147422) gives:
$$
(f^{-1} \circ f)_* = (f^{-1})_* \circ f_* = (\text{id}_M)_*
$$
The pushforward of the identity map is just the [identity transformation](@entry_id:264671) on the [tangent space](@entry_id:141028). Therefore, $(f^{-1})_* \circ f_* = \text{Id}$, which implies that the pushforward of the inverse map is the inverse of the original [pushforward](@entry_id:158718) map:
$$
(f^{-1})_* = (f_*)^{-1}
$$
This means that the Jacobian matrix of an inverse map is the inverse of the Jacobian matrix of the original map: $J_{f^{-1}}(f(p)) = [J_f(p)]^{-1}$. This provides a practical method for finding the pushforward of an inverse map without needing to find the analytical expression for the inverse map itself [@problem_id:1534579].

### Geometric Interpretation: The Kernel
For any given point $p$, the [pushforward](@entry_id:158718) $(f_*)_p: T_pM \to T_{f(p)}N$ is a [linear map](@entry_id:201112) between two vector spaces. Like any [linear map](@entry_id:201112), it has a **kernel** (or null space), which is the set of all vectors in the domain that are mapped to the [zero vector](@entry_id:156189) in the [codomain](@entry_id:139336):
$$
\text{ker}((f_*)_p) = \{ v \in T_pM \mid (f_*)_p(v) = 0 \}
$$
What is the geometric meaning of a vector being in the kernel? If $v \in \text{ker}((f_*)_p)$, it means that a curve moving with velocity $v$ is mapped by $f$ to a curve whose velocity at the point $f(p)$ is zero. The map $f$ "crushes" or "annihilates" motion in the direction of $v$.

Consider the projection map $\pi: \mathbb{R}^3 \to \mathbb{R}^2$ given by $\pi(x, y, z) = (x+z, y-z)$. This is a linear map, so its [pushforward](@entry_id:158718) is represented by its constant Jacobian matrix. The kernel of this [pushforward](@entry_id:158718) consists of all vectors $(v_1, v_2, v_3)$ such that $v_1+v_3=0$ and $v_2-v_3=0$. Solving this system shows that the kernel is a one-dimensional subspace spanned by the vector $(-1, 1, 1)$ [@problem_id:1534530]. This vector represents the direction in $\mathbb{R}^3$ along which all points are projected to the same point in $\mathbb{R}^2$. The kernel of the pushforward thus identifies the "fibers" of the projection—the directions that are lost in the mapping process. The dimension of this kernel is a measure of the "information" lost by the map at that point. If the kernel is trivial (contains only the zero vector), the map is an **immersion** at that point, meaning it preserves all local directional information.