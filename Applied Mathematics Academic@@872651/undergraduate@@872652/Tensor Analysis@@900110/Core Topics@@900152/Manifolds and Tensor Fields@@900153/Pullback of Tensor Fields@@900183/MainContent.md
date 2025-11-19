## Introduction
When studying smooth manifolds, a fundamental challenge is to understand how a map $\Phi: M \to N$ allows us to compare the geometry of two different spaces. How can we use the structure on the target manifold $N$ to define a corresponding structure on the source manifold $M$? The **pullback of [tensor fields](@entry_id:190170)** provides a powerful and elegant answer to this question. It is a systematic procedure for transporting covariant geometric objects—such as functions, [differential forms](@entry_id:146747), and metric tensors—backward, from the target to the source, against the direction of the map itself. This article provides a comprehensive introduction to this essential tool of [differential geometry](@entry_id:145818). In the first chapter, **Principles and Mechanisms**, we will construct the [pullback](@entry_id:160816) from the ground up, exploring its formal definition and the crucial role of the differential map. Next, **Applications and Interdisciplinary Connections** will showcase the [pullback](@entry_id:160816)'s immense utility, from inducing the metric on a surface to formalizing the [change of variables](@entry_id:141386) in integration and identifying symmetries in physical systems. Finally, **Hands-On Practices** will offer a set of curated problems to reinforce these concepts through practical computation and conceptual analysis.

## Principles and Mechanisms

In the study of manifolds, we often encounter [smooth maps](@entry_id:203730) between them. A central question is how these maps allow us to relate geometric and [algebraic structures](@entry_id:139459) defined on one manifold to those on another. The primary tool for this is the **[pullback](@entry_id:160816)**, an operation that takes [tensor fields](@entry_id:190170) on the target manifold and transports them "backward" to create corresponding [tensor fields](@entry_id:190170) on the source manifold. This chapter elucidates the principles and mechanisms governing the [pullback](@entry_id:160816) operation, establishing its definition, properties, and limitations.

### The Conceptual Foundation: Pushing Forward and Pulling Back

Consider a [smooth map](@entry_id:160364) $\Phi: M \to N$ between two manifolds $M$ and $N$. For any point $p \in M$, there is a naturally associated [linear map](@entry_id:201112) between the [tangent spaces](@entry_id:199137), called the **differential** of $\Phi$ at $p$, denoted $d\Phi_p: T_pM \to T_{\Phi(p)}N$. This map, also known as the **[pushforward](@entry_id:158718)** of tangent vectors, describes the [local linear approximation](@entry_id:263289) of $\Phi$ at $p$. It tells us how tangent vectors at $p$ (representing infinitesimal displacements on $M$) are transformed into tangent vectors at the image point $\Phi(p)$ on $N$.

The key insight is that while the differential map pushes vectors *forward* (from $M$ to $N$), it provides the precise mechanism needed to pull *back* objects that act on vectors. This is the essence of duality. Covariant tensors, by their very nature as multilinear maps on [tangent spaces](@entry_id:199137), are perfectly suited for this backward transport. The pullback operation, $\Phi^*$, is defined precisely to exploit this relationship.

### Pullback of Covariant Tensor Fields

The definition of the [pullback](@entry_id:160816) is most naturally introduced by considering tensors of increasing rank.

#### The Simplest Case: Scalar Fields (Type (0,0))

A [scalar field](@entry_id:154310) on a manifold $N$ is a function $f: N \to \mathbb{R}$. From the perspective of [tensor analysis](@entry_id:184019), it is a tensor field of type $(0,0)$, meaning it takes [zero vector](@entry_id:156189) arguments. To pull back such a field via a map $\Phi: M \to N$, we require a function on $M$ whose value at any point $p \in M$ is determined by the value of $f$ at the corresponding point $\Phi(p) \in N$. The most natural definition is simple [function composition](@entry_id:144881).

The **[pullback](@entry_id:160816) of a [scalar field](@entry_id:154310)** $f$ is a scalar field $\Phi^*f$ on $M$ defined by:
$$ (\Phi^*f)(p) = f(\Phi(p)) $$
This operation is a direct generalization of [function composition](@entry_id:144881) familiar from elementary calculus. For instance, if we have a map $\Phi: \mathbb{R} \to \mathbb{R}^2$ given by $t \mapsto (x(t), y(t))$ and a [scalar field](@entry_id:154310) $f(x,y)$ on $\mathbb{R}^2$, the pullback is simply the [composite function](@entry_id:151451) $(\Phi^*f)(t) = f(x(t), y(t))$. [@problem_id:1533949]

#### The Archetype: One-Forms (Type (0,1))

A one-form (or [covector field](@entry_id:186855)) $\omega$ on $N$ assigns to each point $q \in N$ a [linear functional](@entry_id:144884) $\omega_q: T_qN \to \mathbb{R}$. To define its [pullback](@entry_id:160816) $\Phi^*\omega$ on $M$, we must define a one-form $(\Phi^*\omega)_p$ at each point $p \in M$. This new one-form must be a linear functional on the [tangent space](@entry_id:141028) $T_pM$.

Given a tangent vector $X_p \in T_pM$, we can use the differential to push it forward to a [tangent vector](@entry_id:264836) $d\Phi_p(X_p) \in T_{\Phi(p)}N$. Now we have a vector at the point $\Phi(p)$, where the original one-form $\omega$ is defined. We can simply evaluate $\omega_{\Phi(p)}$ on this pushed-forward vector. This gives the definition of the **[pullback of a one-form](@entry_id:263669)**:
$$ (\Phi^*\omega)_p(X_p) := \omega_{\Phi(p)}(d\Phi_p(X_p)) $$
This definition can be viewed as pre-composing the [linear map](@entry_id:201112) $\omega_{\Phi(p)}$ with the linear map $d\Phi_p$. This process is always well-defined for any [smooth map](@entry_id:160364) $\Phi$.

In [local coordinates](@entry_id:181200), this definition translates into a straightforward computational recipe. Let $M$ have coordinates $u^i$ and $N$ have coordinates $x^j$. The map $\Phi$ is given by functions $x^j(u^1, \dots, u^m)$. A [one-form](@entry_id:276716) on $N$ is written as $\omega = \sum_j A_j(x) dx^j$. The pullback $\Phi^*\omega$ is found by applying two rules:
1.  Pull back the coefficient functions: $A_j \mapsto A_j \circ \Phi$.
2.  Pull back the basis [one-forms](@entry_id:270392) $dx^j$: $dx^j \mapsto d(x^j \circ \Phi) = \sum_i \frac{\partial x^j}{\partial u^i} du^i$.

Combining these gives:
$$ \Phi^*\omega = \sum_j (A_j \circ \Phi) \left( \sum_i \frac{\partial x^j}{\partial u^i} du^i \right) = \sum_i \left( \sum_j (A_j \circ \Phi) \frac{\partial x^j}{\partial u^i} \right) du^i $$
For example, to pull back the one-form $\omega = y^2 \, dx + z \, dy - xz \, dz$ on $\mathbb{R}^3$ via the [parameterization](@entry_id:265163) of a parabolic cylinder $\Phi: \mathbb{R}^2 \to \mathbb{R}^3$ given by $(u,v) \mapsto (u, u^2, v)$, we substitute $x=u$, $y=u^2$, $z=v$ into the coefficients and replace $dx, dy, dz$ with their [total differentials](@entry_id:171747) $du, d(u^2)=2u\,du, dv$ respectively. [@problem_id:1533955]

#### General Covariant Tensors (Type (0,k))

The logic extends seamlessly to any purely [covariant tensor](@entry_id:198677) field. A tensor field $T$ of type $(0,k)$ on $N$ is a [multilinear map](@entry_id:274221) at each point $q \in N$ that takes $k$ tangent vectors from $T_qN$ and returns a real number. The **pullback of a (0,k)-tensor** $T$ is defined by feeding the original tensor with pushed-forward vectors:
$$ (\Phi^*T)_p(X_{1,p}, \dots, X_{k,p}) := T_{\Phi(p)}(d\Phi_p(X_{1,p}), \dots, d\Phi_p(X_{k,p})) $$
where $X_{1,p}, \dots, X_{k,p}$ are any $k$ tangent vectors in $T_pM$.

A preeminent application of this principle is the **[induced metric](@entry_id:160616)**. If $(N, g)$ is a Riemannian manifold, where $g$ is a type $(0,2)$ metric tensor, any [smooth map](@entry_id:160364) $\Phi: M \to N$ (often an immersion or embedding) induces a metric tensor $\Phi^*g$ on $M$. This [pullback metric](@entry_id:161465) allows us to measure lengths and angles on $M$ as inherited from the ambient space $N$.

For example, consider the Euclidean metric $g = dx^2 + dy^2 + dz^2$ on $\mathbb{R}^3$. We can pull this back to the surface of a cylinder of radius $R$ via the [parameterization](@entry_id:265163) $\Phi(\theta, h) = (R\cos\theta, R\sin\theta, h)$. The resulting metric on the cylinder's surface is $\Phi^*g = R^2 d\theta^2 + dh^2$, which correctly describes its flat geometry—the geometry of a rolled-up plane. [@problem_id:1533951] This [induced metric](@entry_id:160616) can then be used to compute geometric quantities, such as the length of a vector field defined on the manifold $M$. [@problem_id:1533953]

### The Asymmetry: Why Contravariant Tensors Do Not Pull Back

A natural question arises: can we define a [pullback](@entry_id:160816) for a contravariant tensor, such as a vector field (type (1,0))? Let's attempt to construct a pullback $(\Phi^*Y)_p \in T_pM$ for a vector field $Y$ on $N$. At point $p \in M$, we have access to the vector $Y_{\Phi(p)} \in T_{\Phi(p)}N$. To define a vector in $T_pM$, we would need a canonical map from $T_{\Phi(p)}N$ to $T_pM$. The differential $d\Phi_p$ goes in the opposite direction.

There is no general, natural way to reverse the differential map. An inverse $(d\Phi_p)^{-1}: T_{\Phi(p)}N \to T_pM$ exists if and only if $d\Phi_p$ is a [linear isomorphism](@entry_id:270529). This requires not only that $\dim M = \dim N$ but also that the map $\Phi$ is a [local diffeomorphism](@entry_id:203529). For a general [smooth map](@entry_id:160364), no such canonical backward map exists.

This reveals a fundamental asymmetry rooted in the directionality of the differential map [@problem_id:2992311]:
-   **Covariant tensors** (like [one-forms](@entry_id:270392) and metrics) are "receiving" objects; they take vectors as input. They can be pulled back because we can feed them with vectors that have been pushed forward.
-   **Contravariant tensors** (like [vector fields](@entry_id:161384)) are "donating" objects. They cannot be pulled back because there is no natural way to transport them backward against the flow of the differential.

It is crucial to distinguish the [pullback](@entry_id:160816) of a vector field (which is generally not possible) from the **[pushforward](@entry_id:158718) of a vector field**. Given a vector field $X$ on $M$, we can define a map $p \mapsto d\Phi_p(X_p)$. This assigns a vector in $T_{\Phi(p)}N$ to each point $p \in M$. However, this is not a vector field *on N* unless $\Phi$ is a diffeomorphism. If $\Phi$ is not surjective, points in $N$ outside the image of $\Phi$ are not assigned a vector. If $\Phi$ is not injective, a point in $N$ may be the image of multiple points in $M$, leading to an ambiguous or multi-valued assignment. Thus, the pushforward generally produces a vector field *along the map* $\Phi$, not on the manifold $N$.

### Pullback of Mixed Tensors: The Diffeomorphism Case

The restriction on pulling back contravariant components is lifted in the special but important case where the map $F: M \to N$ is a **[diffeomorphism](@entry_id:147249)**. A diffeomorphism is a smooth, invertible map whose inverse is also smooth. This guarantees that for every $p \in M$, the differential $dF_p: T_pM \to T_{F(p)}N$ is a [linear isomorphism](@entry_id:270529), and its inverse $(dF_p)^{-1}: T_{F(p)}N \to T_pM$ is well-defined.

With this inverse map in hand, we can define the pullback of any [tensor field](@entry_id:266532) of type $(r,s)$. For a [mixed tensor](@entry_id:182079) of type $(1,1)$, such as $P$, which can be viewed as a linear operator $P_q: T_qN \to T_qN$ at each point, the [pullback](@entry_id:160816) $(F^*P)_p$ is defined as the operator on $T_pM$ that makes the following diagram commute: first push a vector from $T_pM$ to $T_{F(p)}N$, apply $P_{F(p)}$, then pull the result back to $T_pM$. This is expressed by the similarity transformation formula:
$$ (F^*P)_p(X_p) = (dF_p)^{-1} ( P_{F(p)}(dF_p(X_p)) ) $$
In matrix terms, if $[dF]$, $[(dF)^{-1}]$, and $[P]$ are the [matrix representations](@entry_id:146025) of the operators in chosen bases, the matrix of the pullback tensor is given by $[F^*P] = [(dF)^{-1}] [P] [dF]$. This is precisely the change-of-basis formula for a linear operator, reinforcing the interpretation that the [pullback](@entry_id:160816) re-expresses the tensor in the "new" coordinate system defined by the map $F$. [@problem_id:1533935]

### Fundamental Properties of the Pullback

The pullback operation is not just a definition; it adheres to a set of powerful algebraic rules that make it a cornerstone of differential geometry.

#### Linearity
The pullback is a [linear operator](@entry_id:136520) on the space of [tensor fields](@entry_id:190170). For any two [tensor fields](@entry_id:190170) $T_1, T_2$ of the same type on $N$ and any constant $c \in \mathbb{R}$:
$$ \Phi^*(T_1 + T_2) = \Phi^*T_1 + \Phi^*T_2 \quad \text{and} \quad \Phi^*(cT_1) = c(\Phi^*T_1) $$
This property follows directly from the linearity of the definitions. For example, computing $\Phi^*(\alpha + \beta)$ for two [one-forms](@entry_id:270392) involves pulling back each term separately and adding the results. [@problem_id:1533932]

#### Identity Map
Pulling back a [tensor field](@entry_id:266532) $T$ on a manifold $M$ by the identity map $id: M \to M$ leaves the tensor unchanged:
$$ id^*T = T $$
This is because for the identity map, $id(p) = p$ and the differential $d(id)_p$ is simply the identity map on the [tangent space](@entry_id:141028) $T_pM$. Substituting these into the [pullback](@entry_id:160816) formula, $(\Phi^*T)_p(X_1, \dots) = T_{\Phi(p)}(d\Phi_p(X_1), \dots)$, immediately returns the original action of the tensor $T_p$. [@problem_id:1533966]

#### Composition (Functoriality)
The [pullback](@entry_id:160816) respects map composition. If we have a sequence of [smooth maps](@entry_id:203730) $L \xrightarrow{G} M \xrightarrow{F} N$, the [pullback](@entry_id:160816) by the composite map $H = F \circ G$ is equivalent to pulling back sequentially:
$$ (F \circ G)^*T = G^*(F^*T) $$
This "[chain rule](@entry_id:147422)" for [pullbacks](@entry_id:160469) is a direct consequence of the chain rule for differentials, $d(F \circ G)_p = dF_{G(p)} \circ dG_p$. It ensures that transforming geometric objects along a composite path is a consistent process. [@problem_id:1533986]

#### Commutation with the Exterior Derivative
One of the most profound properties connects the [pullback](@entry_id:160816) to [differential calculus](@entry_id:175024) on manifolds. The [pullback](@entry_id:160816) operator commutes with the exterior derivative operator $d$. For any [scalar field](@entry_id:154310) $f$ on $N$:
$$ \Phi^*(df) = d(\Phi^*f) $$
This states that it does not matter whether we first compute the differential one-form $df$ on $N$ and then pull it back to $M$, or if we first pull back the scalar field $f$ to $M$ and then compute its differential. The result is the same one-form on $M$. This property is fundamental to the theory of [integration on manifolds](@entry_id:156150) and is a key ingredient in proofs of Stokes' theorem. Its validity can be verified by direct computation on both sides of the equation. [@problem_id:1533954]

In summary, the pullback is a systematic and powerful mechanism for transporting [covariant tensor](@entry_id:198677) fields from a target manifold to a source manifold. Governed by the differential map, its definition is both geometrically intuitive and algebraically robust, providing a foundational language for comparing and relating geometric structures across different spaces.