## Introduction
In the study of geometric analysis, [smooth maps between manifolds](@entry_id:190665) serve as the primary objects of interest, relating the structure of one space to another. However, these maps can be globally complex and non-linear, making them difficult to analyze directly. The central challenge is to develop tools that can probe their local behavior in a systematic and computable way. This is achieved by linearizing the map at each point, a process that unlocks the full power of linear algebra for the study of geometry and topology.

This article introduces the fundamental machinery for this analysis: the [differential of a map](@entry_id:269524), also known as the [pushforward](@entry_id:158718), and its essential dual operation, the pullback. We will see how these tools translate the non-linear behavior of a map into a family of [linear transformations](@entry_id:149133) between tangent spaces. Across the following chapters, you will gain a comprehensive understanding of these concepts. In "Principles and Mechanisms," we will build the formal definitions of the pushforward and [pullback](@entry_id:160816) and explore their key properties. In "Applications and Interdisciplinary Connections," we will witness how these operations are used to classify maps, define submanifolds, induce geometric structures, and provide a common language for fields ranging from physics to computational science. Finally, "Hands-On Practices" will offer opportunities to solidify these ideas through concrete calculations.

## Principles and Mechanisms

In this chapter, we develop the fundamental machinery for analyzing [smooth maps between manifolds](@entry_id:190665). The central tool is the **differential** of a map, a concept that linearizes a [smooth map](@entry_id:160364) at a point, allowing the powerful tools of linear algebra to be applied to the study of geometry and topology. We will define the differential, also known as the **[pushforward](@entry_id:158718)**, and its dual operation, the **[pullback](@entry_id:160816)**. We will then explore how these mechanisms allow us to classify maps and understand their local structure, culminating in a discussion of their profound applications, such as the Inverse Function Theorem and the classification of points and maps.

### The Differential as a Linear Approximation

A [smooth map](@entry_id:160364) $F: M \to N$ between manifolds can be highly complex globally. However, locally, around any point $p \in M$, its behavior can be approximated by a linear map between the corresponding tangent spaces. This [linear map](@entry_id:201112) is the differential of $F$ at $p$.

The most intuitive way to define the differential is by considering how it acts on the velocities of curves. A tangent vector $v \in T_pM$ can be realized as the velocity vector of a smooth curve $\gamma: (-\epsilon, \epsilon) \to M$ such that $\gamma(0) = p$ and $\gamma'(0) = v$. The [smooth map](@entry_id:160364) $F$ transforms this curve on $M$ into a new curve, $F \circ \gamma$, on $N$. This new curve passes through the point $F(p)$ at $t=0$. The velocity vector of this image curve at $t=0$ is a tangent vector in $T_{F(p)}N$.

This leads to the formal definition of the **pushforward** of a vector.

**Definition (Pushforward via Curves):** Let $F: M \to N$ be a [smooth map](@entry_id:160364) and let $v \in T_pM$ be a [tangent vector](@entry_id:264836) at $p \in M$. If $\gamma$ is any smooth curve in $M$ with $\gamma(0)=p$ and $\gamma'(0)=v$, the pushforward of $v$ by $F$, denoted $F_{*p}(v)$ or $dF_p(v)$, is the tangent vector in $T_{F(p)}N$ defined by:
$$
F_{*p}(v) = (F \circ \gamma)'(0)
$$
The map $F_{*p}: T_pM \to T_{F(p)}N$ is a linear map called the **differential** (or **[pushforward](@entry_id:158718)**) of $F$ at $p$.

While this definition is geometrically intuitive, its connection to calculus becomes clearest in [local coordinates](@entry_id:181200). Let $(U, \varphi)$ be a [coordinate chart](@entry_id:263963) around $p \in M$ and $(V, \psi)$ be a chart around $F(p) \in N$. The map $F$ is represented locally by the map $G = \psi \circ F \circ \varphi^{-1}: \mathbb{R}^m \to \mathbb{R}^n$. The differential $F_{*p}$ is then represented by the Jacobian matrix of $G$ at the point $\varphi(p)$.

The Taylor expansion of $G$ at a point $x_0 = \varphi(p)$ reveals precisely why the Jacobian is the correct local representation of the differential. A first-order Taylor expansion of $G$ has the form $G(x) = G(x_0) + A(x-x_0) + r(x)$, where $A$ is the Jacobian matrix of $G$ at $x_0$ and $r(x)$ is a [remainder term](@entry_id:159839) that vanishes faster than first order, i.e., $\lim_{x \to x_0} \frac{\|r(x)\|}{\|x-x_0\|} = 0$.

If a vector $v \in T_pM$ is represented by $u \in \mathbb{R}^m$ in the chart $\varphi$, we can choose a curve $\gamma(t)$ whose coordinate representation is $x(t) = \varphi(\gamma(t)) = x_0 + tu + o(t)$. The image curve in coordinates is $y(t) = G(x(t))$. Its velocity at $t=0$, which represents $F_{*p}(v)$, is $y'(0)$. Using the Taylor expansion:
$$
y(t) = G(x(t)) = G(x_0) + A(x(t) - x_0) + r(x(t)) = G(x_0) + A(tu + o(t)) + r(x_0 + tu + o(t))
$$
Differentiating with respect to $t$ at $t=0$, the constant term $G(x_0)$ vanishes. The linear term gives $A \cdot u$. The [remainder term](@entry_id:159839) $r(x(t))$ is an $o(t)$ function, meaning its derivative at $t=0$ is zero. Thus, $y'(0) = Au$. This confirms that the [pushforward](@entry_id:158718) is captured entirely by the linear part of the map's local expansion, which is its Jacobian matrix [@problem_id:3068289].

A crucial property of the differential is its behavior under composition of maps, known as the **Chain Rule**. If $F: M \to N$ and $G: N \to P$ are [smooth maps](@entry_id:203730), then for any $p \in M$, the differential of the composition $G \circ F$ is the composition of the differentials:
$$
(G \circ F)_{*p} = G_{*F(p)} \circ F_{*p}
$$
In [local coordinates](@entry_id:181200), this corresponds to the familiar rule for the Jacobian of a [composite function](@entry_id:151451): the matrix product $J_{G \circ F}(p) = J_G(F(p)) \cdot J_F(p)$.

For example, consider the maps $F:\mathbb{R}^{2}\to\mathbb{R}^{2}$ given by $F(x,y)=(x^{2}-y, y^{2}+x)$ and $G:\mathbb{R}^{2}\to\mathbb{R}^{2}$ given by $G(u,v)=(u+v, u-v)$. To find the pushforward of the composition $(G\circ F)$ at the point $p=(1,0)$, we can compute the Jacobian matrices. The Jacobian of $F$ at $(1,0)$ is $J_F(1,0) = \begin{pmatrix} 2  -1 \\ 1  0 \end{pmatrix}$. The point $F(1,0) = (1,1)$. The Jacobian of $G$ at $(1,1)$ is $J_G(1,1) = \begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix}$. The chain rule predicts that the Jacobian of the composition at $(1,0)$ is the product of these matrices:
$$
J_{G \circ F}(1,0) = J_G(1,1) \cdot J_F(1,0) = \begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix} \begin{pmatrix} 2  -1 \\ 1  0 \end{pmatrix} = \begin{pmatrix} 3  -1 \\ 1  -1 \end{pmatrix}
$$
This result can be verified by first computing the composite map $H(x,y) = G(F(x,y)) = (x^2+y^2+x-y, x^2-y^2-x-y)$ and then calculating its Jacobian at $(1,0)$, which yields the same matrix [@problem_id:3068259].

### The Pullback: The Dual Operation

The pushforward provides a way to transport tangent vectors "forward" along a map. We now introduce a mechanism to transport dual objects—[covectors](@entry_id:157727) and [differential forms](@entry_id:146747)—"backward" against the map. This operation is the **[pullback](@entry_id:160816)**.

To define the pullback rigorously, it is useful to adopt an alternative, algebraic perspective on tangent vectors. A tangent vector $X_p \in T_pM$ can be defined as a **derivation** at $p$: a linear map $X_p: C^\infty(M) \to \mathbb{R}$ that satisfies the Leibniz rule, $X_p(fg) = f(p)X_p(g) + g(p)X_p(f)$.

From this viewpoint, the [pushforward](@entry_id:158718) $F_{*p}(X_p)$ is defined as the unique derivation on $C^\infty(N)$ at the point $F(p)$ whose action on any function $f \in C^\infty(N)$ is given by applying $X_p$ to the [composite function](@entry_id:151451) $f \circ F$:
$$
(F_{*p}(X_p))(f) := X_p(f \circ F)
$$
This definition is coordinate-free and intrinsically captures how the map $F$ transforms rates of change.

A **[covector](@entry_id:150263)** $\omega_q$ at a point $q \in N$ is a linear functional on the tangent space $T_qN$, i.e., $\omega_q: T_qN \to \mathbb{R}$. The space of all covectors at $q$ is the **[cotangent space](@entry_id:270516)** $T_q^*N$, which is the dual space of $T_qN$. A **1-form** is a smooth field of covectors.

The [pullback](@entry_id:160816) is defined by the principle of duality. Given a linear map $L: V \to W$, there is a natural **dual map** $L^*: W^* \to V^*$ defined by $(L^*\alpha)(v) = \alpha(L(v))$ for $\alpha \in W^*$ and $v \in V$. The [pullback of a 1-form](@entry_id:160530) is simply the dual map to the differential.

**Definition (Pullback of a [1-form](@entry_id:275851)):** Let $F: M \to N$ be a [smooth map](@entry_id:160364) and let $\alpha$ be a 1-form on $N$. The [pullback](@entry_id:160816) of $\alpha$ by $F$, denoted $F^*\alpha$, is a [1-form](@entry_id:275851) on $M$. At each point $p \in M$, the [covector](@entry_id:150263) $(F^*\alpha)_p \in T_p^*M$ is defined by its action on any tangent vector $X_p \in T_pM$ as follows:
$$
(F^*\alpha)_p(X_p) := \alpha_{F(p)}(F_{*p}(X_p))
$$
This definition is the cornerstone of the relationship between pushforwards and [pullbacks](@entry_id:160469) [@problem_id:3069017]. It shows that to evaluate the pulled-back form on a vector, one first pushes the vector forward and then evaluates the original form on the result. The [pullback](@entry_id:160816) operation naturally moves from the target manifold $N$ back to the source manifold $M$.

This concept extends seamlessly to higher-order differential forms. A **[k-form](@entry_id:200390)** $\omega$ on $N$ is a field of alternating multilinear maps $\omega_q: (T_qN)^k \to \mathbb{R}$. Its pullback $F^*\omega$ is a $k$-form on $M$ defined by a similar principle [@problem_id:3078555]:
$$
(F^*\omega)_p(v_1, \dots, v_k) := \omega_{F(p)}(F_{*p}(v_1), \dots, F_{*p}(v_k))
$$
for any vectors $v_1, \dots, v_k \in T_pM$.

Let's illustrate the computation of a [pullback](@entry_id:160816). Consider the map $F(x,y) = (x, xy)$ from $\mathbb{R}^2$ to $\mathbb{R}^2$. Let the target coordinates be $(u,v)$. We wish to pull back the 1-form $\alpha = u^2 dv + v du$ on the target space. We express $u, v, du, dv$ in terms of $x, y, dx, dy$:
$u = x \implies du = dx$
$v = xy \implies dv = y dx + x dy$
Substituting these into the expression for $\alpha$ gives the [pullback](@entry_id:160816) $F^*\alpha$:
$$
F^*\alpha = (x)^2(y\,dx + x\,dy) + (xy)(dx) = (x^2y + xy)dx + x^3dy
$$
To evaluate this pulled-back form at a point, say $p=(2,-1)$, on a vector $w=(1,3)$, we substitute the values:
$$
(F^*\alpha)_p(w) = ( (2^2(-1) + 2(-1)) \cdot 1) + (2^3 \cdot 3) = (-4 - 2) + 24 = 18
$$
This example shows how the abstract definition translates into a concrete calculation involving substitution and the chain rule for [differentials](@entry_id:158422) [@problem_id:3068274].

### Covariance, Contravariance, and Commutation

The relationship between pushforwards and [pullbacks](@entry_id:160469) reveals a fundamental duality in how geometric objects transform.

-   **Tangent vectors are contravariant objects.** They are "pushed forward" in the same direction as the map. Under composition of maps $M \xrightarrow{F} N \xrightarrow{G} P$, their transformations compose in the same order: $(G \circ F)_* = G_* \circ F_*$.

-   **Differential forms are covariant objects.** They are "pulled back" in the opposite direction of the map. Under the same composition $M \xrightarrow{F} N \xrightarrow{G} P$, their transformations compose in the reverse order: $(G \circ F)^* = F^* \circ G^*$.

This opposite transformation behavior is a direct consequence of the algebraic duality between the tangent and cotangent spaces.

Another key mechanism is the interaction between the [pullback](@entry_id:160816) and the [exterior derivative](@entry_id:161900), $d$. For a 0-form (a [smooth function](@entry_id:158037)) $g: N \to \mathbb{R}$, its pullback is simply the composition $F^*g = g \circ F$. Applying the exterior derivative to this function on $M$ yields the [1-form](@entry_id:275851) $d(g \circ F)$. A fundamental result, which follows directly from the [chain rule](@entry_id:147422), states that this is identical to first taking the differential of $g$ to get the [1-form](@entry_id:275851) $dg$ on $N$, and then pulling it back to $M$ [@problem_id:1546227]:
$$
d(F^*g) = F^*(dg)
$$
This is a specific instance of a more general and profoundly important theorem: **the [exterior derivative](@entry_id:161900) commutes with the pullback**. For any differential $k$-form $\omega$, we have $d(F^*\omega) = F^*(d\omega)$. This property makes the [pullback](@entry_id:160816) an essential tool in de Rham cohomology and integration theory on manifolds.

### Classifying Maps and Points via the Differential

The true power of the differential lies in its ability to classify the local behavior of a [smooth map](@entry_id:160364) based on the linear algebraic properties of $F_{*p}$.

A primary characteristic of the [linear map](@entry_id:201112) $F_{*p}: T_pM \to T_{F(p)}N$ is its **rank**. Based on the rank, we can define several crucial types of points and maps.

**Critical Points and Regular Values**
Let $\dim M = m$ and $\dim N = n$. The maximum possible rank of $F_{*p}$ is $\min(m, n)$.
-   A point $p \in M$ is a **regular point** of $F$ if $F_{*p}$ is surjective (i.e., its rank is $n$).
-   A point $p \in M$ is a **critical point** if it is not a regular point (i.e., the rank of $F_{*p}$ is less than $n$).
-   A value $y \in N$ is a **critical value** if it is the image of at least one critical point.
-   A value $y \in N$ is a **[regular value](@entry_id:188218)** if it is not a critical value.

This definition of a [regular value](@entry_id:188218) has a crucial consequence: $y$ is a [regular value](@entry_id:188218) if and only if for every $p$ in its [preimage](@entry_id:150899) $F^{-1}(y)$, the point $p$ is a regular point. This includes the case where the preimage is empty ($F^{-1}(y) = \emptyset$), which is vacuously true. For instance, for the map $h: \mathbb{R} \to \mathbb{R}$ given by $h(x) = x^2$, the value $y=-1$ has an empty preimage, making it a [regular value](@entry_id:188218). In contrast, for $f: \mathbb{R}^2 \to \mathbb{R}$ given by $f(x,y)=x^2+y^2$, the point $(0,0)$ is the only critical point. Therefore, its image, $f(0,0)=0$, is the only critical value. Any positive number $c0$ is a [regular value](@entry_id:188218) because its preimage (a circle) consists entirely of regular points [@problem_id:3068265]. The celebrated **Sard's Theorem** states that the set of critical values of a [smooth map](@entry_id:160364) has measure zero, implying that "most" values are [regular values](@entry_id:161151).

**Immersions and Submersions**
We can also classify maps based on whether the differential satisfies a rank condition at every point.
-   A [smooth map](@entry_id:160364) $F: M \to N$ is an **immersion** if $F_{*p}$ is injective for all $p \in M$. This requires $m \le n$. An immersion is a map that locally looks like an embedding, although it may have self-intersections globally (e.g., the [figure-eight curve](@entry_id:167790)).
-   A [smooth map](@entry_id:160364) $F: M \to N$ is a **[submersion](@entry_id:161795)** if $F_{*p}$ is surjective for all $p \in M$. This requires $m \ge n$. A key example is the projection map $\pi: \mathbb{R}^3 \to \mathbb{R}^2$ given by $\pi(x,y,z)=(x,y)$, which is a submersion at every point [@problem_id:3068266].

The **Preimage Theorem** (or Regular Value Theorem) states that if $y \in N$ is a [regular value](@entry_id:188218) of a [submersion](@entry_id:161795) $F$, then the preimage $F^{-1}(y)$ is a smooth [submanifold](@entry_id:262388) of $M$ of dimension $m-n$. This is one of the most powerful tools for constructing and proving the existence of [smooth manifolds](@entry_id:160799).

**Local Diffeomorphisms and the Constant Rank Theorem**
If the differential $F_{*p}$ is not just injective or surjective, but an [isomorphism](@entry_id:137127), then the map $F$ has the strongest possible local behavior. This occurs when $m=n$ and the rank is maximal.
-   The **Inverse Function Theorem** states that a [smooth map](@entry_id:160364) $F: M \to N$ is a **[local diffeomorphism](@entry_id:203529)** at $p \in M$ if and only if its differential $F_{*p}$ is a [linear isomorphism](@entry_id:270529). In [local coordinates](@entry_id:181200), this is equivalent to the Jacobian determinant being non-zero. For the map $F(x,y)=(x,xy)$, the Jacobian determinant is $x$. Thus, $F$ is a [local diffeomorphism](@entry_id:203529) everywhere except on the $y$-axis (where $x=0$), which is precisely its set of [critical points](@entry_id:144653) [@problem_id:3068274].

An even more general result is the **Constant Rank Theorem**. It states that if a map $F$ has a differential of constant rank $r$ in a neighborhood of a point, then there exist special local [coordinate systems](@entry_id:149266) in the source and target manifolds such that the map takes the [canonical form](@entry_id:140237):
$$
F(u_1, \dots, u_r, v_1, \dots, v_{m-r}) = (u_1, \dots, u_r, 0, \dots, 0)
$$
This remarkable theorem implies that, locally, every [smooth map](@entry_id:160364) of constant rank is equivalent to a standard projection onto its first $r$ coordinates followed by an inclusion into a higher-dimensional space [@problem_id:3068263]. The Submersion and Immersion Theorems are special cases of this powerful result.

### A Cautionary Note: Pushing Forward Vector Fields

While the [pullback](@entry_id:160816) of any differential form is always a well-defined operation, the same cannot be said for pushing forward an entire vector field. A common misconception is to assume that if we can push forward individual vectors, we can push forward a vector field $X$ on $M$ to a vector field $F_*X$ on $N$.

Let's attempt to define $(F_*X)_y$ at a point $y \in N$. The natural approach is to find a point $x \in M$ such that $F(x)=y$ and set $(F_*X)_y = F_{*x}(X_x)$. This procedure fails for a general [smooth map](@entry_id:160364) $F$ for two main reasons [@problem_id:3068291]:

1.  **Ambiguity from Non-Injectivity:** If $F$ is not injective, a point $y$ may have multiple preimages, say $x_1$ and $x_2$. The vectors $F_{*x_1}(X_{x_1})$ and $F_{*x_2}(X_{x_2})$ will, in general, be different. There is no canonical way to choose between them. For example, if $F: \mathbb{R} \to \mathbb{R}$ is $F(x) = x^2$ and $X$ is the constant vector field $\partial_x$, consider the point $y=1$. Its preimages are $x_1=1$ and $x_2=-1$. The [pushforward](@entry_id:158718) via $x_1=1$ gives $F_{*1}(\partial_x) = 2(1)\partial_y = 2\partial_y$, whereas the [pushforward](@entry_id:158718) via $x_2=-1$ gives $F_{*-1}(\partial_x) = 2(-1)\partial_y = -2\partial_y$. The result is ambiguous.

2.  **Undefinedness from Non-Surjectivity:** If $F$ is not surjective, there exist points $y \in N$ that are not in the image of $F$. For such a $y$, the preimage $F^{-1}(y)$ is empty, and there is no point $x$ from which to push a vector forward. The resulting field would be undefined on parts of $N$.

Consequently, the pushforward of an arbitrary smooth vector field is only well-defined and smooth when the map $F$ is a **[diffeomorphism](@entry_id:147249)**. In this case, for every $y \in N$, there is a unique [preimage](@entry_id:150899) $x = F^{-1}(y)$, resolving both ambiguity and undefinedness. This fundamental asymmetry—[pullbacks](@entry_id:160469) of forms are always defined, but pushforwards of [vector fields](@entry_id:161384) are not—is a deep feature of [differential geometry](@entry_id:145818) that underscores the distinct nature of [covariant and contravariant](@entry_id:189600) objects.