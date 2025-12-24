## Introduction
In the modern study of mechanics, physics, and engineering, the language of [differential geometry](@entry_id:145818) provides a powerful, coordinate-independent framework for describing complex systems. Central to this language are two dual operations: the **[pushforward](@entry_id:158718)** and the **[pullback](@entry_id:160816)**. These tools address the fundamental problem of how to consistently transform physical and geometric quantities—such as velocities, forces, and fields—when a system changes its configuration or is viewed in a different coordinate system. By providing a rigorous method for transporting objects like vectors and [differential forms](@entry_id:146747) between manifolds, they form the bedrock upon which the elegant theories of [geometric mechanics](@entry_id:169959) are built.

This article provides a comprehensive exploration of these essential operations. You will learn:
- **Principles and Mechanisms:** The formal definitions of the [pushforward](@entry_id:158718) for [tangent vectors](@entry_id:265494) and the pullback for [differential forms](@entry_id:146747), leading to their role in defining dynamics through Lie derivatives and their profound implications in Hamiltonian mechanics, such as the preservation of symplectic structure.
- **Applications and Interdisciplinary Connections:** How these abstract concepts are applied to solve concrete problems in diverse fields, from deriving stress tensor relationships in continuum mechanics and defining symmetries in general relativity to enabling robust algorithms in computational science and [image analysis](@entry_id:914766).
- **Hands-On Practices:** A series of targeted problems designed to solidify your understanding of how to compute and apply pushforwards and [pullbacks](@entry_id:160469) in practical scenarios involving transformations of [vector fields](@entry_id:161384) and canonical maps.

## Principles and Mechanisms

The [geometric formulation of mechanics](@entry_id:202980) relies on a set of powerful, coordinate-independent tools for describing transformations and dynamics on [smooth manifolds](@entry_id:160799). Central to this framework are the dual operations of **[pushforward](@entry_id:158718)** and **[pullback](@entry_id:160816)**. The [pushforward](@entry_id:158718) describes how geometric objects like [tangent vectors](@entry_id:265494) are transported *forward* by a map, in the same direction as the map itself. Conversely, the pullback describes how objects like functions and [differential forms](@entry_id:146747) are transported *backward*, against the direction of the map. This chapter elucidates the principles and mechanisms of these operations, building from their fundamental definitions to their profound applications in the description of Hamiltonian flows, symmetries, and conserved quantities.

### The Fundamental Duality: Pushforwards and Pullbacks

Let us consider two [smooth manifolds](@entry_id:160799), $M$ and $N$, and a [smooth map](@entry_id:160364) $F: M \to N$. This map provides the stage upon which we define our core operations.

#### The Pushforward of Tangent Vectors

At each point $p \in M$, the map $F$ induces a [linear transformation](@entry_id:143080) between the corresponding [tangent spaces](@entry_id:199137). This is known as the **differential**, **[tangent map](@entry_id:203492)**, or **[pushforward](@entry_id:158718)** of $F$ at $p$, denoted $dF_p: T_p M \to T_{F(p)} N$. Its action on a tangent vector $v \in T_p M$ can be defined by how the vector acts on [smooth functions](@entry_id:138942). For any smooth real-valued function $g$ defined on a neighborhood of $F(p)$ in $N$, the new vector $dF_p(v)$ acts on $g$ as:
$$
(dF_p(v))(g) = v(g \circ F)
$$
This definition elegantly captures the idea that the pushed-forward vector's rate of change on $g$ at $F(p)$ is the same as the original vector's rate of change on the "pulled-back" function $g \circ F$ at $p$.

While this definition is abstract and coordinate-free, in practical applications we often work in [local coordinates](@entry_id:181200). Let $(U, \phi)$ be a chart around $p \in M$ with coordinates $x^i$, and $(V, \psi)$ be a chart around $F(p) \in N$ with coordinates $y^j$. In these coordinates, the map $F$ is represented by a function $\hat{F} = \psi \circ F \circ \phi^{-1}$ from an open set in $\mathbb{R}^{\dim M}$ to an open set in $\mathbb{R}^{\dim N}$. The linear map $dF_p$ is then represented by the familiar **Jacobian matrix** of this coordinate representation, evaluated at the point $\phi(p)$ :
$$
[dF_p] = D(\psi \circ F \circ \phi^{-1})\big(\phi(p)\big)
$$
The entry in the $j$-th row and $i$-th column of this matrix is $\frac{\partial \hat{F}^j}{\partial x^i}(\phi(p))$. It is crucial to remember that while the [linear map](@entry_id:201112) $dF_p$ is an intrinsic geometric object, its [matrix representation](@entry_id:143451) depends explicitly on the choice of [coordinate charts](@entry_id:262338). If one changes the charts, the matrix transforms according to the [chain rule](@entry_id:147422), involving the Jacobians of the coordinate transition maps .

#### The Pullback of Differential Forms

The dual operation to the [pushforward](@entry_id:158718) is the **[pullback](@entry_id:160816)**. While the [pushforward](@entry_id:158718) acts on contravariant objects like [tangent vectors](@entry_id:265494), the pullback acts on covariant objects like [differential forms](@entry_id:146747). Given a differential $k$-form $\alpha \in \Omega^k(N)$, its [pullback](@entry_id:160816) by $F$ is a $k$-form $F^*\alpha \in \Omega^k(M)$. The definition is constructed such that the pairing between forms and vectors is preserved in a natural way.

At a point $p \in M$, the value of the pulled-back form, $(F^*\alpha)_p$, is an alternating [multilinear map](@entry_id:274221) on the [tangent space](@entry_id:141028) $T_pM$. To define its action on a set of $k$ vectors $v_1, \dots, v_k \in T_pM$, we first "push" these vectors forward to the [tangent space](@entry_id:141028) $T_{F(p)}N$ using the differential $dF_p$. Then, we evaluate the original form $\alpha$ at the point $F(p)$ on these pushed-forward vectors . This yields the defining formula:
$$
(F^*\alpha)_p(v_1, \dots, v_k) = \alpha_{F(p)}(dF_p(v_1), \dots, dF_p(v_k))
$$
This definition elegantly illustrates the duality: to pull a form back from $N$ to $M$, one feeds it vectors that have been pushed forward from $M$ to $N$.

The [pullback](@entry_id:160816) operator has several crucial algebraic properties that make it a cornerstone of differential geometry. It commutes with the [exterior derivative](@entry_id:161900), $F^*(d\alpha) = d(F^*\alpha)$, a property known as the **[naturality](@entry_id:270302) of the exterior derivative**. It also distributes over the [wedge product](@entry_id:147029), $F^*(\alpha \wedge \beta) = (F^*\alpha) \wedge (F^*\beta)$ . These properties ensure that the pullback is a homomorphism of differential graded algebras, preserving the fundamental structures on the space of forms.

### Dynamics and Infinitesimal Transformations

The concepts of [pushforward](@entry_id:158718) and pullback are not limited to static maps; they are essential for describing dynamics and continuous transformations generated by [vector fields](@entry_id:161384).

#### The Pushforward of Vector Fields

While the differential $dF_p$ pushes forward individual [tangent vectors](@entry_id:265494) for any [smooth map](@entry_id:160364) $F$, pushing forward an entire vector field $X \in \mathfrak{X}(M)$ to obtain a new vector field on $N$ is more restrictive. It requires that the map $F$ be a **diffeomorphism** (a smooth, invertible map with a smooth inverse). This ensures that each point $q \in N$ has a unique [preimage](@entry_id:150899) $p = F^{-1}(q) \in M$, allowing us to define the vector at $q$ unambiguously.

For a diffeomorphism $F: M \to N$, the **[pushforward](@entry_id:158718) vector field** $F_*X$ on $N$ is defined such that the vector at point $F(p) \in N$ is the [pushforward](@entry_id:158718) of the vector $X_p$ from $M$ :
$$
(F_*X)_{F(p)} = dF_p(X_p)
$$
The most important consequence of this definition is its effect on dynamics. If $\gamma(t)$ is an [integral curve](@entry_id:276251) of the vector field $X$ (i.e., $\dot{\gamma}(t) = X_{\gamma(t)}$), then the transformed curve $F(\gamma(t))$ is an [integral curve](@entry_id:276251) of the pushed-forward vector field $F_*X$. In essence, a [diffeomorphism](@entry_id:147249) maps the flow of one vector field to the flow of its [pushforward](@entry_id:158718) .

#### The Lie Derivative

Instead of a single transformation, consider a continuous family of transformations generated by the **flow** of a vector field $X$. The flow is a one-parameter family of diffeomorphisms, $\phi_t: M \to M$, satisfying $\frac{d}{dt}\phi_t(p) = X(\phi_t(p))$. The **Lie derivative** with respect to $X$, denoted $\mathcal{L}_X$, measures the infinitesimal rate of change of a [tensor field](@entry_id:266532) (like a differential form $\alpha$) as it is dragged along by this flow. It is defined as the derivative of the pullback at time $t=0$ :
$$
\mathcal{L}_X \alpha = \left.\frac{d}{dt}\right|_{t=0} (\phi_t)^*\alpha
$$
This definition implies that for a small time $t$, the [pullback of a form](@entry_id:275358) can be approximated by the first-order Taylor expansion $(\phi_t)^*\alpha \approx \alpha + t (\mathcal{L}_X \alpha)$ . A [tensor field](@entry_id:266532) is said to be *invariant* under the flow of $X$ if its Lie derivative vanishes, $\mathcal{L}_X \alpha = 0$.

While the definition via flows is intuitive, for computations, **Cartan's magic formula** provides a powerful alternative that does not require solving for the flow explicitly. It relates the Lie derivative to the exterior derivative $d$ and the [interior product](@entry_id:158127) $\iota_X$:
$$
\mathcal{L}_X \alpha = d(\iota_X \alpha) + \iota_X(d\alpha)
$$
This formula is an indispensable tool throughout [geometric mechanics](@entry_id:169959).

### Applications in Hamiltonian Mechanics

The true power of these geometric operations becomes apparent when applied to the [symplectic framework](@entry_id:1132750) of Hamiltonian mechanics.

#### Symplectomorphisms and Hamiltonian Flows

A **symplectic manifold** is a pair $(M, \omega)$ where $M$ is an even-dimensional manifold and $\omega$ is a symplectic form—a closed ($d\omega=0$) and non-degenerate 2-form. The form $\omega$ provides a way to pair [tangent vectors](@entry_id:265494) at each point, and a central question in mechanics is what transformations preserve this structure.

A **[symplectomorphism](@entry_id:1132764)** is a diffeomorphism $F: (M, \omega_M) \to (N, \omega_N)$ that preserves the symplectic structure. The precise meaning of this preservation is captured by the [pullback](@entry_id:160816): $F^*\omega_N = \omega_M$ . Pointwise, this means that for any $x \in M$ and any two [tangent vectors](@entry_id:265494) $v, w \in T_x M$, the pairing of the original vectors by $\omega_M$ is identical to the pairing of the pushed-forward vectors by $\omega_N$ :
$$
\omega_M(x)(v,w) = \omega_N(F(x))(dF_x v, dF_x w)
$$
This implies that the differential $dF_x$ is a linear symplectomorphism between [tangent spaces](@entry_id:199137). In special [local coordinates](@entry_id:181200) known as Darboux coordinates, where $\omega$ has a standard [matrix representation](@entry_id:143451) $J = \begin{pmatrix} 0 & I_n \\ -I_n & 0 \end{pmatrix}$, the Jacobian matrix $M$ of a [symplectomorphism](@entry_id:1132764) satisfies the algebraic condition $M^T J M = J$. A key consequence of this is that the determinant of a symplectic map is always $+1$, meaning symplectomorphisms are volume-preserving and orientation-preserving , .

A profound result connects Hamiltonian dynamics to this [symmetry group](@entry_id:138562). For any Hamiltonian function $H$, the associated **Hamiltonian vector field** $X_H$ is defined by the relation $\iota_{X_H}\omega = dH$. Using Cartan's formula, one can show that the Lie derivative of the symplectic form along any Hamiltonian vector field is zero :
$$
\mathcal{L}_{X_H} \omega = d(\iota_{X_H}\omega) + \iota_{X_H}(d\omega) = d(dH) + \iota_{X_H}(0) = 0
$$
Since $\mathcal{L}_{X_H}\omega=0$, the form $\omega$ is invariant under the flow $\phi_t$ of $X_H$. This means that $(\phi_t)^*\omega = \omega$ for all $t$. In other words, **the flow generated by any Hamiltonian vector field consists entirely of symplectomorphisms**. This is the geometric heart of Hamiltonian mechanics: the dynamics it generates automatically preserves the fundamental structure of the phase space.

#### Consequences of Symplectic Symmetry

The interplay between symplectomorphisms and Hamiltonian [vector fields](@entry_id:161384) leads to further important results. When a system is transformed by a [symplectomorphism](@entry_id:1132764) $F: M \to M$, the Hamiltonian [vector fields](@entry_id:161384) themselves transform according to a specific rule. If $X_H$ is the Hamiltonian vector field for a function $H$, its [pushforward](@entry_id:158718) $F_*X_H$ is also a Hamiltonian vector field, but for the transformed Hamiltonian $H \circ F^{-1}$ , :
$$
F_* X_H = X_{H \circ F^{-1}}
$$
An equivalent and often useful form of this identity is $F_*(X_{H \circ F}) = X_H$ , . This relationship is crucial for understanding how symmetries of a system relate to conserved quantities.

Furthermore, because symplectomorphisms preserve the 2-form $\omega$, they also preserve its powers. On a $2n$-dimensional symplectic manifold, the top-degree form $\mu = \frac{1}{n!} \omega^n = \frac{1}{n!} (\omega \wedge \dots \wedge \omega)$ is a [volume form](@entry_id:161784), known as the **Liouville [volume form](@entry_id:161784)**. Since the pullback respects [scalar multiplication](@entry_id:155971) and wedge products, for any symplectomorphism $F$, we have :
$$
F^*\mu = F^*\left(\frac{1}{n!}\omega^n\right) = \frac{1}{n!}(F^*\omega)^n = \frac{1}{n!}\omega^n = \mu
$$
This proves **Liouville's theorem**: symplectomorphisms preserve the canonical phase space volume. Since Hamiltonian flows are sequences of symplectomorphisms, this means that the volume of any region of phase space is conserved as it evolves under Hamiltonian dynamics.

### Advanced Structures and Applications

The [pushforward](@entry_id:158718) and pullback operations are not just descriptive tools; they are constitutive elements in the definition of more advanced structures that bridge different formalisms and uncover deep properties of mechanical systems.

#### The Legendre Transform and Canonical Forms

Classical mechanics can be formulated on the tangent bundle $TQ$ (the space of positions and velocities) in the Lagrangian framework, or on [the cotangent bundle](@entry_id:185138) $T^*Q$ (the space of positions and momenta) in the Hamiltonian framework. The bridge between these two pictures is the **Legendre transform**. For a regular Lagrangian $L: TQ \to \mathbb{R}$, the Legendre transform is a map $\mathbb{F}L: TQ \to T^*Q$ that, in local coordinates $(q^i, \dot{q}^i)$, defines the momenta $p_i$ as $p_i = \frac{\partial L}{\partial \dot{q}^i}$.

The cotangent bundle $T^*Q$ is endowed with a special structure, the **canonical 1-form** $\theta$ (also called the tautological or Liouville [1-form](@entry_id:275851)), which in local coordinates $(q^i, p_i)$ is given by $\theta = p_i dq^i$. The [canonical symplectic form](@entry_id:180641) is then $\omega = -d\theta$. The [pullback](@entry_id:160816) operation provides the crucial link between the Lagrangian and its associated Hamiltonian structure. The [pullback](@entry_id:160816) of the canonical 1-form by the Legendre transform yields a 1-form on $TQ$ whose coordinate expression is fundamental :
$$
\mathbb{F}L^* \theta = \frac{\partial L}{\partial \dot{q}^i} dq^i
$$
This beautiful relation encapsulates the transition from velocity phase space to momentum phase space, with the pullback acting as the formal mechanism for translating the canonical structure of $T^*Q$ back to $TQ$.

#### Momentum Maps for Hamiltonian Group Actions

When a Lie group $G$ acts on a symplectic manifold $(M, \omega)$ by symplectomorphisms, and this action has an additional structure, we call it a Hamiltonian action. This structure is encoded in a **momentum map** $J: M \to \mathfrak{g}^*$, where $\mathfrak{g}^*$ is the dual of the Lie algebra of $G$. The momentum map assigns a "conserved quantity" to each symmetry generator. For each element $\xi \in \mathfrak{g}$, its associated fundamental vector field $\xi_M$ on $M$ is Hamiltonian, and its Hamiltonian function is given by the pairing of the momentum map's value with $\xi$ :
$$
d\langle J, \xi \rangle = \iota_{\xi_M} \omega
$$
This defining equation can be recast in the language of [pullbacks](@entry_id:160469). The right-hand side, $\iota_{\xi_M} \omega$, can be viewed as a section of [the cotangent bundle](@entry_id:185138) $T^*M$. Using the canonical [1-form](@entry_id:275851) $\theta_{\text{can}}$ on $T^*M$, this 1-form is precisely the pullback of $\theta_{\text{can}}$ by this section. This provides an elegant, albeit abstract, reformulation of the momentum map condition . The existence of such a map is the statement of Noether's theorem in the language of geometric mechanics: symmetries give rise to conserved quantities (the components of the momentum map).

#### Symplectic Reduction

As a final illustration of the power of these concepts, we consider the **Marsden-Weinstein reduction theorem**. This theorem provides a systematic way to construct a new, smaller symplectic manifold from a larger one that possesses a Hamiltonian group action. It is the geometric procedure for "modding out" by a symmetry.

Given a Hamiltonian $G$-action with momentum map $J$, one selects a value $\mu \in \mathfrak{g}^*$ for the conserved quantity. Under certain technical conditions (that $\mu$ is a [regular value](@entry_id:188218) and the action of the [isotropy subgroup](@entry_id:200360) $G_\mu$ on the [level set](@entry_id:637056) $J^{-1}(\mu)$ is free and proper), the theorem states that the [quotient space](@entry_id:148218) $M_\mu = J^{-1}(\mu)/G_\mu$ is itself a smooth symplectic manifold, called the [reduced phase space](@entry_id:165136) .

The core of the theorem lies in how the new symplectic form $\omega_\mu$ on the reduced space $M_\mu$ is defined. It is the unique 2-form satisfying the following relation involving [pullbacks](@entry_id:160469):
$$
\pi^* \omega_\mu = i^* \omega
$$
Here, $i: J^{-1}(\mu) \hookrightarrow M$ is the inclusion of the [level set](@entry_id:637056) into the original manifold, and $\pi: J^{-1}(\mu) \to M_\mu$ is the projection onto the [quotient space](@entry_id:148218). This single equation is a masterpiece of geometric construction. The form $\omega$ on the large space $M$ is first pulled back by $i$ to the constraint [submanifold](@entry_id:262388) $J^{-1}(\mu)$, resulting in a (degenerate) 2-form $i^*\omega$. The theorem guarantees that this form's degeneracy is precisely along the directions that are quotiented out by $\pi$. Thus, there is a unique [non-degenerate form](@entry_id:150307) $\omega_\mu$ on the base space $M_\mu$ that, when pulled back by $\pi$, reproduces $i^*\omega$. This procedure is the foundation for studying systems with symmetry, from the motion of a rigid body to the equations of gauge theories in physics.

In summary, the [pushforward](@entry_id:158718) and pullback are far more than notational conveniences. They are the fundamental operators that allow us to compare, transform, and relate geometric structures across manifolds, forming the very language used to express the principles of dynamics, symmetry, and reduction in modern geometric mechanics.