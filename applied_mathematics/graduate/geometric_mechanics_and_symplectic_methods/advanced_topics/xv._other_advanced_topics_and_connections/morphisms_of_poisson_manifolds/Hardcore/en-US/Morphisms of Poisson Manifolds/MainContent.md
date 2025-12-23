## Introduction
Poisson manifolds provide a powerful generalization of the symplectic structures used in classical Hamiltonian mechanics, allowing for the description of a wider class of physical systems, including those with symmetries and constraints. Within this rich geometric framework, a fundamental question arises: how do we relate different Poisson spaces in a way that respects their intrinsic structure? The answer lies in the concept of a **Poisson morphism**, a map that preserves the Poisson bracket. These morphisms are not merely mathematical curiosities; they are the essential language for describing [canonical transformations](@entry_id:178165), symmetries, conserved quantities, and the process of system simplification through reduction.

This article provides a detailed exploration of Poisson morphisms, from their foundational definitions to their far-reaching applications. It aims to bridge the gap between the abstract theory and its practical significance in mechanics and computation. The discussion is structured to build a cohesive understanding across three core chapters.
*   **Principles and Mechanisms** will establish the fundamental characterizations of Poisson maps, explore key examples like Lie-Poisson morphisms and [momentum maps](@entry_id:178341), and detail their profound role in the theory of Poisson reduction.
*   **Applications and Interdisciplinary Connections** will demonstrate how these principles serve as a unifying thread connecting classical mechanics, symmetry analysis, the design of structure-preserving [numerical algorithms](@entry_id:752770), and the global theory of quantization.
*   **Hands-On Practices** will offer a series of guided problems designed to solidify theoretical understanding through concrete calculations involving Lie algebroids, Dirac morphisms, and the mechanics of reduction.

## Principles and Mechanisms

This chapter delves into the principles and mechanisms governing morphisms between Poisson manifolds. Having established the foundational concepts of Poisson geometry in the introduction, we now explore the structure-preserving maps that connect different Poisson spaces. These maps, known as Poisson morphisms, are central to understanding the relationships between physical systems, the process of reduction, and the classification of Poisson structures themselves. We will begin by establishing the fundamental characterizations of Poisson maps, then explore their role in key examples and applications, culminating in a discussion of their generalizations within the broader frameworks of Dirac geometry and canonical relations.

### Fundamental Characterizations of Poisson Morphisms

The most natural starting point for defining a morphism between two [algebraic structures](@entry_id:139459) is to require the preservation of the defining operation. For Poisson manifolds, this operation is the Poisson bracket on the algebra of smooth functions.

A [smooth map](@entry_id:160364) $F: (M, \pi_M) \to (N, \pi_N)$ between two Poisson manifolds is called a **Poisson map** (or Poisson morphism) if it preserves the Poisson bracket structure. This means that for any pair of [smooth functions](@entry_id:138942) $\varphi, \psi \in C^\infty(N)$, the Poisson bracket of their [pullbacks](@entry_id:160469) to $M$ is equal to the pullback of their Poisson bracket on $N$. Formally, this is expressed as:
$$
\{\varphi \circ F, \psi \circ F\}_M = \{\varphi, \psi\}_N \circ F
$$
This definition elegantly captures the preservation of the algebraic structure. However, to work effectively with Poisson maps in geometric contexts, it is essential to translate this functional definition into equivalent conditions on the underlying geometric objects—the Poisson bivectors and their associated bundle maps.

Let us expand the defining equation at a point $m \in M$. The left-hand side is given by the bivector $\pi_M$:
$$
\{\varphi \circ F, \psi \circ F\}_M(m) = \pi_M(m)(d(\varphi \circ F)_m, d(\psi \circ F)_m)
$$
Using the [chain rule](@entry_id:147422) for [differentials](@entry_id:158422), $d(\varphi \circ F)_m = dF_m^*(d\varphi_{F(m)})$, where $dF_m^*: T_{F(m)}^*N \to T_m^*M$ is the pullback map on [covectors](@entry_id:157727). The expression becomes:
$$
\pi_M(m)(dF_m^*(d\varphi_{F(m)}), dF_m^*(d\psi_{F(m)}))
$$
The right-hand side of the defining equation is:
$$
\{\varphi, \psi\}_N(F(m)) = \pi_N(F(m))(d\varphi_{F(m)}, d\psi_{F(m)})
$$
Since this equality must hold for arbitrary functions $\varphi, \psi$, it must hold for any pair of [covectors](@entry_id:157727) at $F(m)$, as any covector can be realized as the differential of some function. Letting $\alpha = d\varphi_{F(m)}$ and $\beta = d\psi_{F(m)}$, we arrive at the condition that for all $\alpha, \beta \in T_{F(m)}^*N$:
$$
\pi_M(m)(dF_m^*(\alpha), dF_m^*(\beta)) = \pi_N(F(m))(\alpha, \beta)
$$
This equation provides two powerful geometric characterizations of a Poisson map .

First, we can express this in terms of the [pushforward](@entry_id:158718) of the bivector field. The [pushforward](@entry_id:158718) of the [bivector](@entry_id:204759) $\pi_M$ by the map $F$, denoted $F_*\pi_M$, is defined by the relation above. The condition for $F$ to be a Poisson map is that this [pushforward](@entry_id:158718) [bivector](@entry_id:204759) must agree with the bivector $\pi_N$ on the image of $F$. This is often written as:
$$
(F_* \pi_M)|_{F(M)} = \pi_N|_{F(M)}
$$
More explicitly, this means that for every $m \in M$, $(\Lambda^2 dF_m)(\pi_M(m)) = \pi_N(F(m))$, where $\Lambda^2 dF_m$ is the [induced map](@entry_id:271712) on bivectors. This equality implies that the [bivector](@entry_id:204759) $\pi_N(F(m))$ must lie in the image of $\Lambda^2 dF_m$, which is the space of bivectors tangent to the image [submanifold](@entry_id:262388) $F(M)$ (assuming $F$ is an immersion).

Second, we can formulate the condition in terms of the **anchor maps** $\pi_M^\sharp: T^*M \to TM$ and $\pi_N^\sharp: T^*N \to TN$. Recall that the anchor map is defined by the relation $\langle \beta, \pi_X^\sharp(\alpha) \rangle = \pi_X(\alpha, \beta)$ for [covectors](@entry_id:157727) $\alpha, \beta$ on a Poisson manifold $(X, \pi_X)$. By manipulating the fundamental equality, we find that it is equivalent to the following identity of [linear maps](@entry_id:185132) from $T_{F(m)}^*N$ to $T_{F(m)}N$:
$$
dF_m \circ \pi_M^\sharp(m) \circ dF_m^* = \pi_N^\sharp(F(m))
$$
This compact relation, stating that the anchor maps are intertwined by the differential of $F$ and its dual, is an extremely useful characterization, particularly in the context of reduction theory and Lie algebroids.

A crucial special case concerns maps between symplectic manifolds. If $(M, \omega_M)$ and $(N, \omega_N)$ are symplectic, their Poisson bivectors are the inverses of the [symplectic forms](@entry_id:165896), $\pi_M = \omega_M^{-1}$ and $\pi_N = \omega_N^{-1}$. A [diffeomorphism](@entry_id:147249) $F: M \to N$ is a **symplectomorphism** if it preserves the symplectic form, i.e., $F^*\omega_N = \omega_M$. It is a fundamental theorem that a diffeomorphism between two [symplectic manifolds](@entry_id:161608) is a Poisson map if and only if it is a [symplectomorphism](@entry_id:1132764). Such maps are sometimes called **Poisson diffeomorphisms**.

### Important Classes of Poisson Morphisms

#### Lie-Poisson Morphisms

A canonical and historically significant class of Poisson manifolds arises from the structure of Lie algebras. For any finite-dimensional Lie algebra $(\mathfrak{g}, [\cdot,\cdot]_\mathfrak{g})$, its [dual vector space](@entry_id:193439) $\mathfrak{g}^*$ is endowed with a natural Poisson structure, known as the **Lie-Poisson structure**. The Poisson bracket of two smooth functions $f, g \in C^\infty(\mathfrak{g}^*)$ is defined at a point $\mu \in \mathfrak{g}^*$ as:
$$
\{f, g\}_{\mathfrak{g}}(\mu) = \langle \mu, [df_\mu, dg_\mu]_\mathfrak{g} \rangle
$$
where $df_\mu$ and $dg_\mu$ are the [differentials](@entry_id:158422) of the functions at $\mu$, identified as elements of $(\mathfrak{g}^*)^* \cong \mathfrak{g}$, and $\langle \cdot, \cdot \rangle$ is the natural pairing between $\mathfrak{g}^*$ and $\mathfrak{g}$.

Now, consider two Lie algebras, $\mathfrak{g}$ and $\mathfrak{h}$, and a Lie algebra homomorphism $\phi: \mathfrak{g} \to \mathfrak{h}$. This algebraic map induces a geometric map between their corresponding Lie-Poisson manifolds. The dual map $\phi^*: \mathfrak{h}^* \to \mathfrak{g}^*$ is a linear map defined by $(\phi^*\nu)(X) = \nu(\phi(X))$ for $\nu \in \mathfrak{h}^*$ and $X \in \mathfrak{g}$. A direct calculation, using the fact that $\phi$ preserves the Lie bracket, shows that $\phi^*$ is a Poisson map . This establishes a beautiful correspondence: homomorphisms of Lie algebras give rise to Poisson morphisms of the associated Lie-Poisson manifolds.

Functions that Poisson-commute with all other functions are called **Casimir functions**. On a Lie-Poisson manifold $\mathfrak{g}^*$, a function $C$ is a Casimir if and only if it is constant on the coadjoint orbits of the corresponding Lie group $G$. The [pullback](@entry_id:160816) of a Casimir function on the target manifold of a Poisson map is not always a Casimir on the domain, but it Poisson-commutes with the pullback of any other function. For $C \circ \phi^*$ to be a Casimir on $\mathfrak{h}^*$, it must commute with *all* functions on $\mathfrak{h}^*$, a condition that is guaranteed if the map $\phi^*$ is a surjective [submersion](@entry_id:161795), which in turn is equivalent to the original Lie algebra homomorphism $\phi$ being injective.

#### Momentum Maps as Poisson Morphisms

In mechanics, symmetries of a system are described by [group actions](@entry_id:268812), and conserved quantities are encoded in [momentum maps](@entry_id:178341). In the modern picture of Poisson geometry, this framework is generalized to the setting of Lie groupoids. A **symplectic groupoid** $(\Gamma, \Omega) \rightrightarrows (P, \pi)$ is a Lie groupoid $\Gamma$ over a base manifold $P$ (the space of objects), where $\Gamma$ is equipped with a symplectic form $\Omega$ that is compatible with the groupoid multiplication. Every symplectic groupoid has a Poisson manifold as its base, and it serves as a global object that "integrates" the infinitesimal structure of the Poisson manifold.

When a symplectic groupoid acts on a symplectic manifold $(X, \omega_X)$, the action is governed by a **moment map** $J: X \to P$. This map generalizes the notion of the momentum map for Lie [group actions](@entry_id:268812). A fundamental theorem states that if the groupoid action is symplectic, then the moment map $J: (X, \omega_X) \to (P, \pi)$ is a Poisson map . This provides a vast class of physically and geometrically significant examples of Poisson morphisms. For instance, the identity map on a Lie-Poisson manifold $\mathfrak{so}(3)^*$ can be viewed as the moment map for the action of the symplectic groupoid $T^*SO(3)$ on $\mathfrak{so}(3)^*$, and is therefore trivially a Poisson map. This implies that the Poisson bracket on $\mathfrak{so}(3)^*$ is consistent with this more general framework. A direct calculation confirms this, and also shows that functions of the Casimir invariant, such as those depending only on $|\mu|^2$ for $\mu \in \mathfrak{so}(3)^* \cong \mathbb{R}^3$, have a vanishing Poisson bracket with any other function, as expected .

### Poisson Morphisms and Reduction Theory

One of the most profound roles of Poisson morphisms is in the theory of reduction, which provides a systematic way to simplify complex systems by exploiting symmetries. The central idea is to "quotient out" the symmetries to obtain a simpler, reduced system.

#### The Problem of Quotients and Poisson Submersions

A naive attempt to define a Poisson structure on a quotient space $N = M/{\sim}$ by "pushing forward" the bivector $\pi_M$ from a Poisson manifold $(M, \pi_M)$ via a projection map $F: M \to N$ generally fails. If the map $F$ is not injective, a point $y \in N$ may have multiple preimages, say $x_1, x_2 \in M$. The [pushforward](@entry_id:158718) bivector at $y$ would be $(dF)_{x_1}(\pi_M(x_1))$ or $(dF)_{x_2}(\pi_M(x_2))$, and there is no guarantee these values are the same .

The correct notion that enables such a quotient procedure is that of a **Poisson [submersion](@entry_id:161795)**. A surjective [submersion](@entry_id:161795) $F: (M, \pi_M) \to (N, \pi_N)$ is a Poisson [submersion](@entry_id:161795) if it is a Poisson map. In this case, the Poisson structure $\pi_N$ on the quotient is uniquely determined by the requirement that $F$ be a Poisson map. This condition is equivalent to the bivector $\pi_M$ being projectable with respect to $F$.

#### Dirac and Poisson Reduction

The general theory of Poisson reduction provides a mechanism for constructing such [quotient spaces](@entry_id:274314). Let $(M, \pi)$ be a Poisson manifold and $C \subset M$ be a **[coisotropic submanifold](@entry_id:1122621)**. This geometric condition is defined as $\pi^\sharp(TC^\circ) \subset TC$, where $TC^\circ$ is the conormal bundle of $C$. This condition ensures that the distribution $\mathcal{F} = \pi^\sharp(TC^\circ)$, known as the **characteristic distribution**, is tangent to $C$. The Jacobi identity for $\pi$ implies that $\mathcal{F}$ is integrable. If the leaf space $M_{\text{red}} = C/\mathcal{F}$ is a [smooth manifold](@entry_id:156564), then it inherits a unique Poisson structure $\pi_{\text{red}}$ such that the quotient projection $q: C \to M_{\text{red}}$ becomes a Poisson [submersion](@entry_id:161795) (in a generalized sense) .

This process can be elegantly described using the language of **Dirac structures**. A Dirac structure is a subbundle of $TM \oplus T^*M$ that generalizes both Poisson and presymplectic structures. The reduction of a [coisotropic submanifold](@entry_id:1122621) corresponds to a well-defined forward image operation on Dirac structures, which yields the Dirac structure (and thus the Poisson structure) on the reduced space .

A classic application is **Marsden-Weinstein reduction**. Here, one starts with a symplectic manifold $(M, \omega)$ with a Hamiltonian $G$-action and an [equivariant momentum map](@entry_id:1124631) $J: M \to \mathfrak{g}^*$. The [level set](@entry_id:637056) $C = J^{-1}(0)$ is a [coisotropic submanifold](@entry_id:1122621). The characteristic [foliation](@entry_id:160209) on $C$ corresponds to the action of the group $G$. The reduced space is the [orbit space](@entry_id:148658) $M_{\text{red}} = C/G$. The fundamental result is that $M_{\text{red}}$ inherits a unique symplectic (and thus Poisson) structure $\omega_{\text{red}}$ such that the diagram involving the inclusion $i: C \hookrightarrow M$ and the projection $\pi: C \to M_{\text{red}}$ is compatible. This compatibility, which relates the brackets of functions on $M$ to brackets on $M_{\text{red}}$, is precisely what makes the projection a Poisson map in this context .

#### The Lie Algebroid Perspective on Reduction

The interplay between Poisson maps and reduction can be viewed through the powerful lens of Lie algebroids. The cotangent bundle $T^*M$ of a Poisson manifold $(M, \pi_M)$ has a natural Lie algebroid structure, with the anchor map being $\pi_M^\sharp: T^*M \to TM$. From this perspective, a map $F: M \to N$ is a Poisson map if and only if the pair $(F, F^*)$, where $F^*$ is the pullback on [1-forms](@entry_id:157984), defines a morphism of Lie algebroids from $(T^*N, \pi_N^\sharp)$ to $(T^*M, \pi_M^\sharp)$.

Furthermore, a [coisotropic submanifold](@entry_id:1122621) $C \subset M$ is one whose conormal bundle $\nu_C^* = TC^\circ$ is a Lie subalgebroid of $T^*M|_C$. The central theorem of Poisson reduction can then be elegantly restated: if $F: M \to N$ is a Poisson map that is transverse to a [coisotropic submanifold](@entry_id:1122621) $S \subset N$, then its [preimage](@entry_id:150899) $C = F^{-1}(S)$ is a [coisotropic submanifold](@entry_id:1122621) of $M$. The [transversality condition](@entry_id:261118) ensures that the [pullback](@entry_id:160816) map $F^*$ establishes an isomorphism between the conormal bundles $\nu_S^*$ and $\nu_C^*$, and this pullback restricts to a morphism of the corresponding Lie algebroids . This confirms that coisotropic [submanifolds](@entry_id:159439) behave naturally under transverse Poisson maps.

### Generalizations and Related Structures

#### Canonical Relations

The notion of a Poisson map, and specifically a symplectomorphism, can be generalized to that of a **canonical relation**. A canonical relation between two symplectic manifolds $(M, \omega_M)$ and $(N, \omega_N)$ is a Lagrangian [submanifold](@entry_id:262388) of the product manifold $M^- \times N$, where $M^-$ denotes the manifold $M$ equipped with the opposite symplectic form $-\omega_M$.

The graph of a map $\Phi: M \to N$ is a canonical relation if and only if $\Phi$ is a symplectomorphism. Canonical relations are more general because a Lagrangian submanifold of a [product space](@entry_id:151533) does not need to be the graph of a map; it can represent a "multi-valued" correspondence. Therefore, the theory of canonical relations provides a framework that generalizes the category of symplectic manifolds with symplectomorphisms as morphisms . It is important to note that the graph of a general Poisson map which is not a [diffeomorphism](@entry_id:147249) is *not* a canonical relation.

#### Local Models: The Minimal Coupling Picture

While reduction theory provides a global quotient, it is often useful to have a local model for the Poisson structure in a neighborhood of the reduced space. Under certain conditions, such as the triviality of the [principal bundle](@entry_id:159429) associated with the reduction, one can construct a Poisson isomorphism between a neighborhood of the reduced [level set](@entry_id:637056) in $M$ and a [product space](@entry_id:151533) $M_{\text{red}} \times \mathfrak{g}^*$.

However, the Poisson structure on this product is not a simple [direct product](@entry_id:143046). It is a **semidirect product** structure, often called a "magnetic" or "twisted" product, that incorporates the curvature of a [connection on a [principal bundl](@entry_id:159386)e](@entry_id:159429). This is known as the [minimal coupling](@entry_id:148226) model. For example, the Poisson bracket on $T^*Q \times \mathfrak{g}^*$ includes a term proportional to the momentum coordinate $\mu \in \mathfrak{g}^*$ and the curvature $F$ of the connection: $\{p_i, p_j\} = \mu F_{ij}(q)$. This structure, which arises directly from the geometry of reduction, provides a concrete example of how non-trivial Poisson structures are constructed and how they deviate from simple products in a way that is linear in the momentum variables . Understanding these local models is a key step towards a deeper analysis of the geometry of Poisson manifolds.