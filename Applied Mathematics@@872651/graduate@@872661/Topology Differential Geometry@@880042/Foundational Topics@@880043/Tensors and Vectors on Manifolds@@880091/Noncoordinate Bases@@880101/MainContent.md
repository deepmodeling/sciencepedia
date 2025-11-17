## Introduction
In differential geometry and theoretical physics, the description of geometric objects is often tied to a chosen coordinate system. While coordinate bases are computationally convenient, they are inherently rigid and often fail to capture the natural symmetries of a physical system or the perspective of a local observer. This limitation necessitates a more powerful and flexible framework: the theory of noncoordinate bases, also known as frames or anholonomic bases. These bases are not derived from a single [coordinate chart](@entry_id:263963), allowing them to adapt to rotating reference systems, local physical symmetries, or the intrinsic geometry of a curved space.

This article delves into the essential formalism of noncoordinate bases, bridging the gap between abstract theory and practical application. It addresses the fundamental problem of how to perform calculus and analyze geometry when the basis vectors themselves vary in a complex, non-integrable way. By mastering this machinery, you will gain a deeper understanding of the distinction between intrinsic geometric properties and their representation, unlocking a powerful toolkit for tackling advanced problems.

The following chapters will guide you through this topic systematically. First, **Principles and Mechanisms** will introduce the core concepts, including frames and [coframes](@entry_id:637284), Lie brackets, [structure functions](@entry_id:161908), and [connection coefficients](@entry_id:157618). Next, **Applications and Interdisciplinary Connections** will demonstrate the power of these tools in fields like Riemannian geometry, general relativity, and the study of Lie groups. Finally, **Hands-On Practices** will provide targeted problems to solidify your computational skills and conceptual understanding.

## Principles and Mechanisms

In the study of [differential geometry](@entry_id:145818), our description of geometric quantities—such as vectors, [one-forms](@entry_id:270392), and tensors—is fundamentally tied to a choice of basis. While coordinate bases, derived directly from a local coordinate system, are algebraically simple and computationally convenient, they are not always the most natural or insightful choice for describing physical or geometric phenomena. For instance, an observer's local measurement apparatus might be rotating or moving in a way that does not align with any fixed coordinate grid. This necessitates a more general formalism: that of **noncoordinate bases**, also known as **frames** or **anholonomic bases**. This chapter will develop the principles and mechanisms governing the use of these more flexible frames.

### Frames and Coframes: The Language of Local Observers

A **[coordinate basis](@entry_id:270149)** on an $n$-dimensional manifold, associated with coordinates $\{x^i\}$, consists of the set of vector fields $\{\partial_1, \partial_2, \dots, \partial_n\}$, where $\partial_i = \partial / \partial x^i$. A key property of these [vector fields](@entry_id:161384) is that they are derived from the [gradient operator](@entry_id:275922) along specific coordinate directions.

We generalize this by defining a **frame** (or **noncoordinate basis**) as any set of $n$ [vector fields](@entry_id:161384) $\{e_1, e_2, \dots, e_n\}$ that are [linearly independent](@entry_id:148207) at every point in some open region of the manifold. These [vector fields](@entry_id:161384) serve as a basis for the [tangent space](@entry_id:141028) at each point, but they need not be derivable from any single coordinate system.

Since $\{e_a\}$ forms a basis, any vector field $V$ can be expressed as a linear combination of these frame vectors: $V = v^a e_a$, where the coefficients $v^a$ are scalar functions on the manifold. This includes the [coordinate basis](@entry_id:270149) vectors themselves. The process of changing from a [coordinate basis](@entry_id:270149) to a noncoordinate basis is a fundamental algebraic task.

Consider, for example, a frame on $\mathbb{R}^3$ defined by the [vector fields](@entry_id:161384) [@problem_id:999536]:
$$
\begin{aligned}
e_1 = \partial_y + z\partial_x \\
e_2 = \partial_z + x\partial_y \\
e_3 = \partial_x + y\partial_z
\end{aligned}
$$
Suppose we wish to express the [coordinate vector](@entry_id:153319) field $V = \partial_y$ in this frame. We seek coefficient functions $c_1, c_2, c_3$ such that $\partial_y = c_1 e_1 + c_2 e_2 + c_3 e_3$. Substituting the definitions of the frame vectors yields:
$$
\partial_y = c_1(\partial_y + z\partial_x) + c_2(\partial_z + x\partial_y) + c_3(\partial_x + y\partial_z)
$$
By collecting the terms for each [coordinate basis](@entry_id:270149) vector, we obtain:
$$
\partial_y = (c_1 z + c_3)\partial_x + (c_1 + c_2 x)\partial_y + (c_2 + c_3 y)\partial_z
$$
For this equality to hold, the coefficients of the [coordinate basis](@entry_id:270149) vectors must match on both sides. This leads to a system of linear algebraic equations for the functions $c_a(x,y,z)$:
$$
\begin{cases}
c_1 z + c_3 = 0 \\
c_1 + c_2 x = 1 \\
c_2 + c_3 y = 0
\end{cases}
$$
Solving this system reveals the component functions. For instance, from the first two equations we find $c_3 = -c_1 z$ and from the third we get $c_2 = -c_3 y = c_1 yz$. Substituting this into the second equation gives $c_1 + (c_1 yz)x = 1$, which implies $c_1(1 + xyz) = 1$. This yields $c_1 = \frac{1}{1+xyz}$, and consequently, $c_2 = \frac{yz}{1+xyz}$ and $c_3 = \frac{-z}{1+xyz}$. This example illustrates that the components of a simple vector field can become non-trivial functions when expressed in a noncoordinate basis, reflecting the relationship between the two bases.

Associated with any [vector basis](@entry_id:191419) is a [dual basis](@entry_id:145076) for the [cotangent space](@entry_id:270516). For a frame $\{e_a\}$, the [dual basis](@entry_id:145076) is the **coframe** $\{\theta^a\}$, a set of [1-forms](@entry_id:157984) defined by the duality condition:
$$
\theta^a(e_b) = \delta^a_b
$$
where $\delta^a_b$ is the Kronecker delta. Just as we expressed vector fields in the new basis, we can express the coframe [1-forms](@entry_id:157984) in terms of the coordinate [dual basis](@entry_id:145076) $\{dx^i\}$.

Let's find the coframe for a simple noncoordinate basis on $\mathbb{R}^3$ given by [@problem_id:999546]:
$$
e_1 = \partial_x + \partial_y, \quad e_2 = \partial_y + \partial_z, \quad e_3 = \partial_z + \partial_x
$$
To find $\theta^1$, we write it as a general [linear combination](@entry_id:155091) of the coordinate 1-forms: $\theta^1 = a\,dx + b\,dy + c\,dz$, where $a,b,c$ are functions to be determined (in this case, they will be constants). We then apply the duality conditions:
$$
\theta^1(e_1) = (a\,dx + b\,dy + c\,dz)(\partial_x + \partial_y) = a \cdot 1 + b \cdot 1 + c \cdot 0 = a+b = 1
$$
$$
\theta^1(e_2) = (a\,dx + b\,dy + c\,dz)(\partial_y + \partial_z) = a \cdot 0 + b \cdot 1 + c \cdot 1 = b+c = 0
$$
$$
\theta^1(e_3) = (a\,dx + b\,dy + c\,dz)(\partial_z + \partial_x) = a \cdot 1 + b \cdot 0 + c \cdot 1 = a+c = 0
$$
This gives a system of three [linear equations](@entry_id:151487) for three unknowns. Solving this system yields $a=1/2$, $b=1/2$, and $c=-1/2$. Therefore, the first [dual basis](@entry_id:145076) 1-form is:
$$
\theta^1 = \frac{1}{2}dx + \frac{1}{2}dy - \frac{1}{2}dz
$$
The other coframe forms, $\theta^2$ and $\theta^3$, can be found analogously.

### Geometric Objects in a Noncoordinate Basis

The components of any [tensor field](@entry_id:266532) will transform when changing to a noncoordinate basis. Let us consider the metric tensor, $g$. In a [coordinate basis](@entry_id:270149) $\{\partial_i\}$, its components are $g_{ij} = g(\partial_i, \partial_j)$. In a frame $\{e_a\}$, the components are given by $\tilde{g}_{ab} = g(e_a, e_b)$.

A key insight afforded by noncoordinate bases is the distinction between the [intrinsic geometry](@entry_id:158788) of the manifold and the representation of that geometry in a particular basis. For example, the Euclidean plane is intrinsically flat. In Cartesian coordinates $(x,y)$, the metric is $g=dx \otimes dx + dy \otimes dy$, and its components form the identity matrix: $g(\partial_i, \partial_j) = \delta_{ij}$. The simplicity of these components reflects the alignment of the basis with the flat geometry.

However, if we choose a noncoordinate basis, the metric components can appear more complex. Consider the standard Euclidean metric on $\mathbb{R}^3$ and the frame [@problem_id:999626]:
$$
e_1 = \partial_x + y\partial_z, \quad e_2 = \partial_y + z\partial_x, \quad e_3 = \partial_z + x\partial_y
$$
Let's compute the metric component $\tilde{g}_{12} = g(e_1, e_2)$. Using the [bilinearity](@entry_id:146819) of the metric and the fact that the Cartesian [coordinate basis](@entry_id:270149) is orthonormal, i.e., $g(\partial_i, \partial_j) = \delta_{ij}$:
$$
\begin{aligned}
\tilde{g}_{12} = g(\partial_x + y\partial_z, \partial_y + z\partial_x) \\
= g(\partial_x, \partial_y) + z\,g(\partial_x, \partial_x) + y\,g(\partial_z, \partial_y) + yz\,g(\partial_z, \partial_x) \\
= 0 + z(1) + y(0) + yz(0) \\
= z
\end{aligned}
$$
The result is that the metric component $\tilde{g}_{12}$ is not constant and is non-zero. The metric tensor now has off-diagonal components that vary with position, such as $\tilde{g}_{12}(x,y,z) = z$. This does not mean the space has become curved; it is still the same flat Euclidean space. It simply means our chosen basis vectors are not orthogonal to each other and their relationship changes from point to point.

### The Signature of Non-[integrability](@entry_id:142415): Lie Brackets and Structure Functions

The most profound difference between coordinate and noncoordinate bases lies in their [commutation relations](@entry_id:136780). For any [coordinate basis](@entry_id:270149), the Lie bracket of any two basis vectors vanishes:
$$
[\partial_i, \partial_j] = \partial_i \partial_j - \partial_j \partial_i = 0
$$
This property, a consequence of the equality of [mixed partial derivatives](@entry_id:139334) on [smooth functions](@entry_id:138942) ($X(Y(f)) - Y(X(f))$), is the analytical expression of the geometric idea that coordinate lines form an integrable grid.

In general, the vector fields of a noncoordinate basis do not commute: $[e_a, e_b] \neq 0$. The **Lie bracket** $[X,Y]$ of two [vector fields](@entry_id:161384) measures the infinitesimal failure of the flows generated by $X$ and $Y$ to commute. For a noncoordinate basis, its non-vanishing Lie brackets signify that the basis fields do not mesh together to form a coordinate system. For this reason, such bases are also called **anholonomic**.

Since the Lie bracket $[e_a, e_b]$ is itself a vector field, it can be expanded in the frame $\{e_c\}$:
$$
[e_a, e_b] = C^c_{ab} e_c
$$
The coefficients $C^c_{ab}(x)$ are scalar functions on the manifold known as the **[structure functions](@entry_id:161908)** or **structure coefficients** of the frame. They are antisymmetric in their lower indices, $C^c_{ab} = -C^c_{ba}$, and they encode the fundamental geometric properties of the chosen frame. If all [structure functions](@entry_id:161908) vanish, the frame is integrable and is, at least locally, a [coordinate basis](@entry_id:270149) (a result known as the Frobenius Integration Theorem).

To compute the [structure functions](@entry_id:161908), one first calculates the Lie bracket, typically using the coordinate representation. For two vector fields $X = X^i \partial_i$ and $Y = Y^j \partial_j$, the Lie bracket is given by:
$$
[X, Y] = \left( X(Y^k) - Y(X^k) \right) \partial_k = \left( X^i \frac{\partial Y^k}{\partial x^i} - Y^i \frac{\partial X^k}{\partial x^i} \right) \partial_k
$$
As a first step, consider the frame on $\mathbb{R}^2$ given by $e_1 = \partial_x$ and $e_2 = x\partial_x + \partial_y$ [@problem_id:999508]. The Lie bracket is:
$$
[e_1, e_2] = [\partial_x, x\partial_x + \partial_y] = [\partial_x, x\partial_x] + [\partial_x, \partial_y]
$$
Using the identity $[fX, gY] = fg[X,Y] + f(Xg)Y - g(Yf)X$, and noting $[\partial_x, \partial_x]=0$ and $[\partial_x, \partial_y]=0$:
$$
[\partial_x, x\partial_x] = (\partial_x x)\partial_x = 1 \cdot \partial_x = \partial_x
$$
Thus, $[e_1, e_2] = \partial_x$. Since $e_1 = \partial_x$, we have $[e_1, e_2] = e_1$. Comparing this to the definition $[e_1, e_2] = C^k_{12} e_k$, we can immediately read off the [structure functions](@entry_id:161908): $C^1_{12} = 1$ and $C^2_{12} = 0$.

In more complex cases, the resulting Lie bracket must be re-expressed in the noncoordinate basis. For the basis on $\mathbb{R}^3$ given by $e_1 = \partial_x + \alpha y \partial_z$, $e_2 = \partial_y - \alpha x \partial_z$, and $e_3 = x \partial_y - y \partial_x + \beta(x^2+y^2)\partial_z$ [@problem_id:999575], the Lie bracket $[e_1, e_2]$ is found to be $-2\alpha \partial_z$ in the [coordinate basis](@entry_id:270149). To find the structure function $C^3_{12}$, we must express $\partial_z$ in the $\{e_a\}$ basis. This involves solving another [system of linear equations](@entry_id:140416), which ultimately shows that $[e_1, e_2]$ has a non-zero component along $e_3$, giving a non-trivial structure function $C^3_{12} = -\frac{2\alpha}{(\alpha+\beta)(x^2+y^2)}$.

The calculation of Lie brackets is not restricted to Cartesian coordinates. In the Euclidean plane with [polar coordinates](@entry_id:159425) $(r, \phi)$, consider the [rotating frame](@entry_id:155637) [@problem_id:999563]:
$$
E_1 = \cos(\alpha\phi) \partial_r - \frac{\sin(\alpha\phi)}{r} \partial_\phi, \quad E_2 = \sin(\alpha\phi) \partial_r + \frac{\cos(\alpha\phi)}{r} \partial_\phi
$$
A careful application of the Lie bracket formula in polar coordinates reveals, for instance, that the $\partial_\phi$ component of the bracket $[E_1, E_2]$ is $[E_1, E_2]^\phi = \frac{\alpha-1}{r^2}$. This non-vanishing result again confirms the anholonomic nature of the frame.

### Cartan's Structure Equations and the Connection

The calculation of [structure functions](@entry_id:161908) via coordinate-based Lie bracket formulas can be cumbersome. The formalism of [differential forms](@entry_id:146747), developed by Élie Cartan, provides a more elegant and powerful approach. The entire set of [commutation relations](@entry_id:136780) for a frame can be encoded in **Cartan's first structure equation**:
$$
d\theta^c = -\frac{1}{2} C^c_{ab} \theta^a \wedge \theta^b
$$
Here, $d\theta^c$ is the exterior derivative of the coframe [1-form](@entry_id:275851) $\theta^c$, and $\wedge$ denotes the wedge product. This equation provides a direct method for computing [structure functions](@entry_id:161908) by calculating the exterior derivatives of the coframe forms. For example, if we were to compute $d\theta^2$ for a given coframe, we could read off the [structure functions](@entry_id:161908) $C^2_{13}$, $C^2_{21}$, etc., as the coefficients of the $\theta^1 \wedge \theta^3$, $\theta^2 \wedge \theta^1$ terms [@problem_id:999697].

Beyond algebraic properties, we are interested in performing [calculus on manifolds](@entry_id:270207), which requires a notion of [covariant differentiation](@entry_id:263981), specified by a connection $\nabla$. In a noncoordinate basis, the action of the connection on the basis vectors themselves defines the **[connection coefficients](@entry_id:157618)** $\Gamma^k_{ij}$ (analogous to Christoffel symbols):
$$
\nabla_{e_i} e_j = \Gamma^k_{ij} e_k
$$
A crucial point is that even in a [flat space](@entry_id:204618) where the connection is notionally "trivial," the [connection coefficients](@entry_id:157618) in a noncoordinate basis can be non-zero. This is because the coefficients must account for the way the basis vectors themselves vary from point to point.

Consider again the flat Euclidean plane with the frame $e_1 = \partial_x, e_2 = x\partial_x + \partial_y$ [@problem_id:999651]. The Levi-Civita connection $\nabla$ in Cartesian coordinates is simply component-wise differentiation: $\nabla_X Y = (X(Y^x))\partial_x + (X(Y^y))\partial_y$. Let's compute $\nabla_{e_2} e_2$:
$$
\begin{aligned}
\nabla_{e_2} e_2 = \nabla_{x\partial_x + \partial_y} (x\partial_x + \partial_y) \\
= ( (x\partial_x + \partial_y)(x) )\partial_x + ( (x\partial_x + \partial_y)(1) )\partial_y \\
= (x \cdot 1 + 0)\partial_x + (0)\partial_y \\
= x \partial_x
\end{aligned}
$$
Since $e_1 = \partial_x$, we have $\nabla_{e_2} e_2 = x e_1$. Comparing this with the definition $\nabla_{e_2} e_2 = \Gamma^k_{22} e_k = \Gamma^1_{22} e_1 + \Gamma^2_{22} e_2$, we see immediately that $\Gamma^1_{22} = x$ and $\Gamma^2_{22} = 0$. The [connection coefficient](@entry_id:261760) $\Gamma^1_{22}$ is non-zero because $e_2$ "changes" in the direction of $e_2$ in a way that has a component along $e_1$.

For the Levi-Civita connection, the [connection coefficients](@entry_id:157618) can be found from the metric components and the [structure functions](@entry_id:161908) using the **Koszul formula**. For a frame $\{e_a\}$, the formula is:
$$
2g(\nabla_{e_a} e_b, e_c) = e_a(g_{bc}) + e_b(g_{ac}) - e_c(g_{ab}) - g([e_a, e_b], e_c) + g([e_a, e_c], e_b) + g([e_b, e_c], e_a)
$$
where $g_{ab} = g(e_a, e_b)$. This formula explicitly shows the two sources of non-zero [connection coefficients](@entry_id:157618): the changing of metric components in the frame ($e_a(g_{bc})$ terms) and the [non-commutativity](@entry_id:153545) of the frame itself ($g([e_a, e_b], e_c)$ terms). The calculation of a term like $g([e_1, e_2], e_2)$ [@problem_id:999508] is a direct input into this fundamental formula.

### Applications in Physics and Lie Groups

Noncoordinate bases are not merely a mathematical curiosity; they are essential tools in theoretical physics and the study of Lie groups.

A particularly important case is a **left-invariant frame** on a Lie group. These are frames whose [vector fields](@entry_id:161384) are unchanged by the group's left-multiplication operation. For such a frame, the [structure functions](@entry_id:161908) $C^c_{ab}$ become constants, known as the **structure constants** of the group's Lie algebra. For instance, the Lie group $SU(2)$ can be viewed as a 3-manifold. It admits a left-invariant [orthonormal frame](@entry_id:189702) $\{e_a\}$ whose structure constants are given by the Levi-Civita symbol, $[e_a, e_b] = \epsilon_{abd} e_d$ [@problem_id:999511] [@problem_id:999560]. For such frames, calculations often simplify dramatically. The trace of the Killing form, a canonical [symmetric bilinear form](@entry_id:148281) on any Lie algebra, can be computed directly from these constants [@problem_id:999560].

The concept of **torsion** is also clarified by the use of noncoordinate bases. The [torsion tensor](@entry_id:204137) of a connection $\nabla$ is defined as
$$
T(X,Y) = \nabla_X Y - \nabla_Y X - [X,Y]
$$
In a frame $\{e_a\}$, its components are $T^k_{ij} = \Gamma^k_{ij} - \Gamma^k_{ji} - C^k_{ij}$. The Levi-Civita connection is, by definition, torsion-free, which imposes the condition that the antisymmetric part of its [connection coefficients](@entry_id:157618) must exactly match the [structure functions](@entry_id:161908): $\Gamma^k_{ij} - \Gamma^k_{ji} = C^k_{ij}$.

In theories like Einstein-Cartan gravity or in the study of [material defects](@entry_id:159283), connections with non-zero torsion are considered. Suppose one starts with the torsion-free Levi-Civita connection $\nabla$ and defines a new connection $\tilde{\nabla}$ by adding a [tensor field](@entry_id:266532) $K$: $\tilde{\nabla}_X Y = \nabla_X Y + K(X,Y)$ [@problem_id:999511]. The components of the new connection are $\tilde{\Gamma}^d_{ab} = \Gamma^d_{ab} + K^d_{ab}$. The torsion of this new connection is then:
$$
\begin{aligned}
\tilde{T}^d_{ab} = \tilde{\Gamma}^d_{ab} - \tilde{\Gamma}^d_{ba} - C^d_{ab} \\
= (\Gamma^d_{ab} + K^d_{ab}) - (\Gamma^d_{ba} + K^d_{ba}) - C^d_{ab} \\
= (\Gamma^d_{ab} - \Gamma^d_{ba} - C^d_{ab}) + (K^d_{ab} - K^d_{ba})
\end{aligned}
$$
Since $\nabla$ is torsion-free, the term in the first parenthesis vanishes, leaving $\tilde{T}^d_{ab} = K^d_{ab} - K^d_{ba}$. The torsion of the modified connection is simply the antisymmetric part of the added tensor $K$. This elegant result demonstrates how the machinery of frames, [structure functions](@entry_id:161908), and connections provides a clear and powerful language for describing complex geometric structures.