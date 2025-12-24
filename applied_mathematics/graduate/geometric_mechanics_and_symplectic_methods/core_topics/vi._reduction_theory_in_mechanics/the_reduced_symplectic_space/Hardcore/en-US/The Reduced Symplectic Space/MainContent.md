## Introduction
In the study of physical systems, symmetries are not merely an aesthetic feature; they are a profound organizing principle that dictates conservation laws and simplifies dynamics. Geometric mechanics provides a powerful language for exploiting these symmetries, and at its heart lies the concept of [symplectic reduction](@entry_id:170200). This procedure offers a systematic method for taming the complexity of a Hamiltonian system by "quotienting out" its continuous symmetries, thereby reducing the number of degrees of freedom and revealing the essential underlying dynamics. The resulting smaller, more manageable phase space is known as the [reduced symplectic space](@entry_id:1130758). This article provides a comprehensive exploration of this fundamental topic, guiding the reader from its mathematical foundations to its diverse applications.

The first chapter, "Principles and Mechanisms," will lay the groundwork by introducing Hamiltonian systems, [momentum maps](@entry_id:178341), and the pivotal Marsden-Weinstein-Meyer theorem. We will then extend this framework to cover the dynamics of reconstruction and the important case of singular reduction. The second chapter, "Applications and Interdisciplinary Connections," will demonstrate the theory's power by applying it to canonical problems in classical mechanics, electromagnetism, and integrable systems, while also forging links to [complex geometry](@entry_id:159080) and quantization. Finally, the "Hands-On Practices" section will provide a set of guided exercises to solidify understanding and build practical skills in applying these concepts. We begin by delving into the core principles that make symplectic reduction possible.

## Principles and Mechanisms

This chapter delves into the core principles of symplectic reduction, a cornerstone of modern [geometric mechanics](@entry_id:169959). We will begin by reviewing the essential geometric structures of Hamiltonian systems and their symmetries. We will then formulate the central theorem of [symplectic reduction](@entry_id:170200), explore its application through a canonical example, and connect it to the theory of constrained systems. Finally, we will venture beyond the standard assumptions to understand the structure of reduced spaces in the singular case.

### Hamiltonian Systems and Symmetries on a Symplectic Manifold

A Hamiltonian system is fundamentally described by a phase space, which is mathematically a **symplectic manifold** $(M, \omega)$. This is a smooth manifold $M$ equipped with a **symplectic form** $\omega$, which is a closed ($d\omega=0$) and non-degenerate $2$-form. The non-degeneracy of $\omega$ is a crucial property with profound consequences. At each point $p \in M$, the [bilinear form](@entry_id:140194) $\omega_p$ on the [tangent space](@entry_id:141028) $T_pM$ is non-degenerate, meaning that if a vector $v \in T_pM$ satisfies $\omega_p(v, w) = 0$ for all $w \in T_pM$, then $v$ must be the [zero vector](@entry_id:156189).

This property establishes a [canonical isomorphism](@entry_id:202335) between the tangent bundle $TM$ and the cotangent bundle $T^*M$. For each [tangent space](@entry_id:141028) $T_pM$, non-degeneracy implies that the linear map from vectors to [covectors](@entry_id:157727), $v \mapsto \omega_p(v, \cdot)$, is injective. Since $T_pM$ and its dual $T_p^*M$ have the same finite dimension, this map is an [isomorphism](@entry_id:137127). Assembling these fiberwise isomorphisms smoothly over the manifold $M$ yields a [vector bundle](@entry_id:157593) [isomorphism](@entry_id:137127), often called the **[musical isomorphism](@entry_id:158753)** associated with $\omega$, which we denote by $\omega^\flat: TM \to T^*M$. This isomorphism is intrinsic to the symplectic structure and does not depend on any additional structure, such as a Riemannian metric. 

The [isomorphism](@entry_id:137127) $\omega^\flat$ provides the link between functions and vector fields that lies at the heart of Hamiltonian dynamics. For any smooth function $f \in C^\infty(M)$, its [exterior derivative](@entry_id:161900) $df$ is a $1$-form, i.e., a section of $T^*M$. Since $\omega^\flat$ is an [isomorphism](@entry_id:137127), there exists a unique vector field, denoted $X_f$, such that $\omega^\flat(X_f) = df$. This vector field $X_f$ is called the **Hamiltonian vector field** of the function (or Hamiltonian) $f$. The defining relation can be written in several equivalent ways:

$$
\omega^\flat(X_f) = df \quad \Leftrightarrow \quad \omega(\cdot, X_f) = df \quad \Leftrightarrow \quad \iota_{X_f}\omega = df
$$

Here, $\iota_{X_f}\omega$ denotes the [interior product](@entry_id:158127) of the vector field $X_f$ with the $2$-form $\omega$. The flow of this vector field, $\dot{x} = X_f(x)$, describes the time evolution of the system. The [existence and uniqueness](@entry_id:263101) of $X_f$ for any [smooth function](@entry_id:158037) $f$ is a direct consequence of the non-degeneracy of $\omega$. 

Symmetries in a Hamiltonian system are represented by a Lie group $G$ acting on the phase space $M$. A symmetry is compatible with the Hamiltonian structure if the group action preserves the symplectic form. Such an action is called a **symplectic action**. This means that for every group element $g \in G$, the corresponding diffeomorphism $\phi_g: M \to M$ is a **[symplectomorphism](@entry_id:1132764)**, satisfying $\phi_g^*\omega = \omega$.

Often, it is more convenient to work with the infinitesimal version of this condition. For each element $\xi$ in the Lie algebra $\mathfrak{g}$ of $G$, we can define an **[infinitesimal generator](@entry_id:270424)**, which is a vector field $\xi_M$ on $M$ given by the derivative of the action at the identity:

$$
\xi_M(x) = \left.\frac{d}{dt}\right|_{t=0} \phi_{\exp(t\xi)}(x)
$$

The action is symplectic if and only if the symplectic form is invariant under the flow of every [infinitesimal generator](@entry_id:270424). This is expressed using the Lie derivative: the action is symplectic if $\mathcal{L}_{\xi_M}\omega = 0$ for all $\xi \in \mathfrak{g}$. For a connected Lie group, this infinitesimal condition is equivalent to the global one. One can show this by considering the family of [pullbacks](@entry_id:160469) $\phi_{\exp(t\xi)}^*\omega$. Its derivative with respect to $t$ is given by $\frac{d}{dt}(\phi_{\exp(t\xi)}^*\omega) = \phi_{\exp(t\xi)}^*(\mathcal{L}_{\xi_M}\omega)$. If $\mathcal{L}_{\xi_M}\omega=0$, then $\phi_{\exp(t\xi)}^*\omega$ is constant in $t$. Since it equals $\omega$ at $t=0$, it must be equal to $\omega$ for all $t$. Because any element in the connected component of the identity of $G$ can be written as a product of exponentials, the invariance extends from [one-parameter subgroups](@entry_id:181957) to the entire component. 

### The Momentum Map: An Encoding of Conservation Laws

For a symplectic action, the condition $\mathcal{L}_{\xi_M}\omega = 0$ has a crucial consequence. Using Cartan's magic formula, $\mathcal{L}_{\xi_M}\omega = d(\iota_{\xi_M}\omega) + \iota_{\xi_M}(d\omega)$, and the fact that $\omega$ is closed ($d\omega=0$), the infinitesimal condition simplifies to $d(\iota_{\xi_M}\omega) = 0$. This means that for every $\xi \in \mathfrak{g}$, the $1$-form $\iota_{\xi_M}\omega$ is closed.

An action is called **Hamiltonian** if it is symplectic and, furthermore, each of these closed $1$-forms is also exact. That is, for each $\xi \in \mathfrak{g}$, there exists a function, which we denote $J^\xi \in C^\infty(M)$, such that:

$$
dJ^\xi = \iota_{\xi_M}\omega
$$

This states that the [infinitesimal generator](@entry_id:270424) $\xi_M$ is the Hamiltonian vector field for the function $J^\xi$. The collection of these functions can be assembled into a single object called the **momentum map** (or moment map), $J: M \to \mathfrak{g}^*$, where $\mathfrak{g}^*$ is the dual of the Lie algebra. The map is defined such that the component function $J^\xi$ is obtained by pairing with $\xi \in \mathfrak{g}$: $J^\xi(x) = \langle J(x), \xi \rangle$.

The existence of a momentum map is not guaranteed for every symplectic action. The obstruction lies in the topology of the manifold $M$. A momentum map exists if and only if the de Rham [cohomology class](@entry_id:263961) $[\iota_{\xi_M}\omega]$ is zero in $H^1(M; \mathbb{R})$ for every $\xi \in \mathfrak{g}$. A simple [sufficient condition](@entry_id:276242) for this is if the first de Rham cohomology group of the manifold is trivial, i.e., $H^1(M; \mathbb{R}) = 0$. In this case, every closed $1$-form is exact, guaranteeing the existence of the functions $J^\xi$. 

A particularly important property a momentum map can have is **equivariance**. The Lie group $G$ acts on its Lie algebra $\mathfrak{g}$ via the [adjoint representation](@entry_id:146773), $\text{Ad}_g(\xi)$, and on the dual $\mathfrak{g}^*$ via the **[coadjoint representation](@entry_id:161716)**, $\text{Ad}^*_g$. A momentum map $J$ is said to be equivariant if it intertwines the action on $M$ with the coadjoint action on $\mathfrak{g}^*$:

$$
J(\phi_g(x)) = \text{Ad}^*_g(J(x)) \quad \text{for all } g \in G, x \in M
$$

For a connected group, this global condition is equivalent to an infinitesimal one involving the Poisson bracket: the map $\xi \mapsto J^\xi$ must be a Lie algebra homomorphism from $(\mathfrak{g}, [\cdot,\cdot])$ to $(C^\infty(M), \{\cdot,\cdot\})$, meaning $\{J^\xi, J^\eta\} = J^{[\xi,\eta]}$ for all $\xi, \eta \in \mathfrak{g}$. Even if a momentum map exists, it may not be equivariant. The failure of [equivariance](@entry_id:636671) is measured by the function $c(\xi, \eta) = \{J^\xi, J^\eta\} - J^{[\xi,\eta]}$, which can be shown to be constant on $M$ if $M$ is connected. This function defines a $2$-[cocycle](@entry_id:200749) on the Lie algebra $\mathfrak{g}$ and thus a class in the Lie algebra cohomology group $H^2(\mathfrak{g}; \mathbb{R})$. If this cohomology group vanishes (as it does for semisimple Lie algebras, by Whitehead's Lemma), any momentum map can be made equivariant by adding a suitable constant element of $\mathfrak{g}^*$. 

The momentum map provides a profound formulation of **Noether's theorem**. If a Hamiltonian $H$ is invariant under the $G$-action, then the momentum map $J$ is a conserved quantity along the trajectories of the system. That is, for any solution curve $x(t)$ of the dynamics $\dot{x}=X_H(x)$, the value $J(x(t))$ is constant in time. This conservation law is the key to simplifying the system.

### The Marsden-Weinstein-Meyer Reduction Theorem

Symplectic reduction is a procedure that uses the conserved quantity provided by the momentum map to construct a new, smaller phase space with a simpler dynamical system. The central result governing this process is the Marsden-Weinstein-Meyer (MWM) theorem.

**Theorem (Marsden-Weinstein-Meyer):** Let $(M, \omega)$ be a symplectic manifold with a proper, Hamiltonian action of a Lie group $G$ and an associated [equivariant momentum map](@entry_id:1124631) $J: M \to \mathfrak{g}^*$. Let $\mu \in \mathfrak{g}^*$ be a **[regular value](@entry_id:188218)** of $J$. Let $G_\mu = \{g \in G \mid \text{Ad}^*_g \mu = \mu\}$ be the stabilizer (or isotropy) subgroup of $\mu$ under the [coadjoint action](@entry_id:170681). If the action of $G_\mu$ on the [level set](@entry_id:637056) $J^{-1}(\mu)$ is **free and proper**, then:

1.  The quotient space $M_\mu := J^{-1}(\mu) / G_\mu$ is a [smooth manifold](@entry_id:156564).
2.  There exists a unique **symplectic form** $\omega_\mu$ on $M_\mu$ such that $\pi_\mu^*\omega_\mu = i_\mu^*\omega$, where $i_\mu: J^{-1}(\mu) \hookrightarrow M$ is the inclusion map and $\pi_\mu: J^{-1}(\mu) \to M_\mu$ is the quotient projection.

The resulting manifold $(M_\mu, \omega_\mu)$ is called the **[reduced symplectic space](@entry_id:1130758)**. Its dimension is $\dim(M) - \dim(G) - \dim(G_\mu)$.

The hypotheses of this theorem are crucial. The condition that $\mu$ is a [regular value](@entry_id:188218) ensures that its [preimage](@entry_id:150899) $J^{-1}(\mu)$ is a smooth submanifold of $M$. The condition that the $G_\mu$ action is free and proper ensures that the [quotient space](@entry_id:148218) is a well-behaved smooth manifold. The theorem's power is that it guarantees the reduced space is not just a [topological space](@entry_id:149165) or a manifold, but a *symplectic* manifold. The reduced form $\omega_\mu$ is, by definition, closed and non-degenerate.  

Because $(M_\mu, \omega_\mu)$ is itself a symplectic manifold, it can serve as a phase space for a new, reduced Hamiltonian system. If the original Hamiltonian $H$ on $M$ is $G$-invariant, it is automatically constant along the orbits of $G_\mu$ within the level set $J^{-1}(\mu)$. Consequently, $H$ descends to a well-defined smooth function $h_\mu$ on the quotient $M_\mu$, called the **reduced Hamiltonian**. The dynamics generated by $H$ on $M$ project to Hamiltonian dynamics on $M_\mu$ generated by $h_\mu$. That is, the projected vector field is precisely the Hamiltonian vector field $X_{h_\mu}$ with respect to the reduced symplectic form $\omega_\mu$. 

### A Canonical Example: Cotangent Bundle Reduction

A quintessential application of symplectic reduction occurs in the context of cotangent bundles, which are the natural phase spaces for many mechanical systems. Let $G$ be a Lie group acting on a configuration manifold $Q$ via $\Phi: G \times Q \to Q$. This action can be "lifted" to an action on [the cotangent bundle](@entry_id:185138) $T^*Q$. This **cotangent lift** is a left action defined as:

$$
g \cdot \alpha_q = (T\Phi_{g^{-1}})^*\alpha_q
$$

Here, $\alpha_q$ is a [covector](@entry_id:150263) at point $q \in Q$, and $(T\Phi_{g^{-1}})^*$ is the pullback map on [covectors](@entry_id:157727) induced by the [tangent map](@entry_id:203492) of the diffeomorphism $\Phi_{g^{-1}}$. The inverse $g^{-1}$ is essential to ensure the composition law for a left action, $(gh)\cdot \alpha_q = g \cdot (h \cdot \alpha_q)$. This map correctly takes a [covector](@entry_id:150263) at base point $q$ to a [covector](@entry_id:150263) at base point $g \cdot q$. 

A remarkable property of the cotangent lift is that it is always Hamiltonian. The cotangent bundle $T^*Q$ carries a canonical $1$-form $\theta_Q$ and a canonical symplectic form $\Omega_Q = -d\theta_Q$. The lifted action preserves $\theta_Q$ and therefore also preserves $\Omega_Q$. Furthermore, it admits a canonical [equivariant momentum map](@entry_id:1124631) given by:

$$
\langle J(\alpha_q), \xi \rangle = \alpha_q(\xi_Q(q))
$$

where $\xi_Q(q)$ is the [infinitesimal generator](@entry_id:270424) of the action on the base manifold $Q$. This provides a rich source of systems to which reduction can be applied. 

The structure of the reduced space depends on the momentum value $\mu$.

*   **Reduction at Zero Momentum ($\mu=0$):** This is a particularly elegant case. If the action of $G$ on $Q$ is free and proper, then the conditions of the MWM theorem are satisfied for $\mu=0$. The reduced space is canonically symplectomorphic to the cotangent bundle of the reduced configuration space:

    $$
    (J^{-1}(0)/G, \omega_0) \cong (T^*(Q/G), \Omega_{Q/G})
    $$
    This result provides a beautiful correspondence between reducing the symmetries at the configuration level (forming $Q/G$) and reducing the full phase space at the zero momentum level. 

*   **Reduction at Non-Zero Momentum ($\mu \neq 0$):** When reducing at a non-zero [regular value](@entry_id:188218) $\mu$, the situation is more intricate. The reduced space $J^{-1}(\mu)/G_\mu$ can still be identified with $T^*(Q/G)$, but the symplectic form is modified. The reduced symplectic form becomes $\Omega_\mu = \Omega_{can} + \pi^*B_\mu$, where $\Omega_{can}$ is the canonical symplectic form on $T^*(Q/G)$, $\pi$ is the bundle projection $T^*(Q/G) \to Q/G$, and $B_\mu$ is a closed $2$-form on $Q/G$ known as a **magnetic term**. This term depends on $\mu$ and the geometry of the [principal bundle](@entry_id:159429) $Q \to Q/G$. The presence of this magnetic term is responsible for phenomena such as the Coriolis effect in mechanics, where dynamics in a rotating frame appear to be influenced by a fictitious magnetic field. 

### Dynamics: Reduction and Reconstruction

The MWM theorem provides a powerful method for simplifying the description of a system's dynamics. Given a $G$-invariant Hamiltonian $H$, instead of solving Hamilton's equations on the large phase space $M$, one can solve the reduced equations on the smaller space $M_\mu$. However, a solution on the reduced space is only part of the story. To understand the full evolution of the original system, we must be able to **reconstruct** the trajectory on $M$ from the trajectory on $M_\mu$.

This reconstruction procedure relies on the geometry of the [quotient map](@entry_id:140877) $\pi_\mu: J^{-1}(\mu) \to M_\mu$. Under the hypotheses of the MWM theorem, this map is a **principal $G_\mu$-bundle**. This structure allows us to decompose the motion into a part "along the base" (the reduced space) and a part "along the fibers" (the group orbits). A **[principal connection](@entry_id:1130166)** $\mathcal{A}$ on this bundle provides the mathematical tool for this decomposition. It is a $\mathfrak{g}_\mu$-valued $1$-form on $J^{-1}(\mu)$ that projects any [tangent vector](@entry_id:264836) to its "vertical" component (tangent to the fiber).

The reconstruction process proceeds as follows:
1.  Solve the reduced Hamilton's equations on $(M_\mu, \omega_\mu)$ for the reduced Hamiltonian $h_\mu$ to find a trajectory $c_\mu(t) \in M_\mu$.
2.  Lift this trajectory to a **horizontal curve** $z_h(t)$ in $J^{-1}(\mu)$. This curve is characterized by $\pi_\mu(z_h(t)) = c_\mu(t)$ and its velocity vectors being horizontal (i.e., $\mathcal{A}(\dot{z}_h(t)) = 0$). The velocity of this [horizontal lift](@entry_id:160651) corresponds to the horizontal part of the full Hamiltonian vector field $X_H$.
3.  The full trajectory $z(t)$ on $M$ must lie in the fiber above $c_\mu(t)$, so it can be written as $z(t) = g(t) \cdot z_h(t)$ for some curve $g(t)$ in the group $G_\mu$.
4.  The group-valued curve $g(t)$ is determined by solving the **reconstruction equation**, which is an ordinary differential equation on $G_\mu$:

    $$
    g(t)^{-1} \dot{g}(t) = \mathcal{A}(X_H(z_h(t)))
    $$

This equation dictates the motion along the symmetry directions, which was factored out during reduction. Together, the [reduced dynamics](@entry_id:166543) and the reconstruction equation provide a complete description of the system's evolution. 

### Connection to Dirac's Theory of Constraints

The language of [symplectic reduction](@entry_id:170200), developed primarily by mathematicians, has a powerful parallel in the language of constrained Hamiltonian systems, developed by physicists following the work of P. A. M. Dirac. The connection between these two viewpoints provides deeper insight into the nature of gauge theories.

In Dirac's formalism, a system is described on a large phase space $M$, but the physical states are restricted to a submanifold $C \subset M$ defined by a set of **constraint functions** $\phi_i=0$. The properties of this constraint [submanifold](@entry_id:262388) are determined by the Poisson brackets of the constraint functions. We define the matrix $C_{ij}(x) = \{\phi_i, \phi_j\}(x)$.

Constraints are classified into two types:
*   **First-Class Constraints:** A set of constraints $\{\phi_i\}$ is first-class if their Poisson brackets vanish on the constraint surface, i.e., $\{\phi_i, \phi_j\} \approx 0$. (The weak equality $\approx$ means equality holds when restricted to $C$.) Geometrically, this condition is equivalent to the constraint submanifold $C$ being **coisotropic**. A submanifold is coisotropic if its symplectic orthogonal space is contained within its tangent space: $(T_x C)^\omega \subset T_x C$. The Hamiltonian vector fields $X_{\phi_i}$ of [first-class constraints](@entry_id:164534) are tangent to $C$ and generate "[gauge transformations](@entry_id:176521)" that move points within $C$ but correspond to the same physical state. The process of identifying these gauge-equivalent points is precisely the quotienting procedure of MWM reduction. The dimension of the physical phase space is $\dim(C) - \dim(\text{gauge orbits}) = (2n-r) - r = 2n-2r$, where $r$ is the number of independent [first-class constraints](@entry_id:164534). 

*   **Second-Class Constraints:** A set of constraints is second-class if the matrix $C_{ij} = \{\phi_i, \phi_j\}$ is invertible on the constraint surface $C$. An invertible skew-symmetric matrix must have even dimension, so the number of [second-class constraints](@entry_id:175584) must be even. Geometrically, this condition is equivalent to the constraint submanifold $C$ being a **symplectic [submanifold](@entry_id:262388)**. The restricted form $\omega|_C$ is non-degenerate. In this case, there are no gauge symmetries to quotient out; the physical phase space is simply the [submanifold](@entry_id:262388) $C$ itself, with its induced symplectic structure. 

Often, physical theories (like electromagnetism or general relativity) are formulated with [first-class constraints](@entry_id:164534). To perform calculations, one must deal with the gauge redundancy. The method of **[gauge fixing](@entry_id:142821)** consists of introducing additional constraints, the gauge-fixing conditions $\chi_a$, which are chosen to intersect each gauge orbit at a single point. The goal is to choose the $\chi_a$ such that the combined set of original constraints $\phi_a$ and gauge-fixing conditions $\chi_a$ becomes second-class. This requires the full matrix of their Poisson brackets to be invertible on the final constraint surface. 

Once one has a set of [second-class constraints](@entry_id:175584) $\Psi_A$, the dynamics can be handled using the **Dirac bracket**. This is a modification of the original Poisson bracket, defined as:

$$
\{F, G\}_D := \{F, G\} - \{F, \Psi_A\} (C^{-1})^{AB} \{\Psi_B, G\}
$$

where $(C^{-1})^{AB}$ is the inverse of the matrix $C_{AB} = \{\Psi_A, \Psi_B\}$. The Dirac bracket has the property that all constraint functions have a vanishing bracket with any other function, i.e., $\{\Psi_A, F\}_D \approx 0$. This allows the constraints to be set strongly to zero within the new bracket structure. The fundamental connection is this: the Dirac bracket evaluated on the gauge-fixed surface is precisely the Poisson bracket of the MWM reduced phase space. This establishes the profound equivalence between the two formalisms for eliminating symmetries. 

### Singular Reduction: When Regularity Fails

The Marsden-Weinstein-Meyer theorem is predicated on strong assumptions, particularly that $\mu$ is a [regular value](@entry_id:188218) of the momentum map. What happens when this condition fails? The values of $\mu$ that are not regular are called **critical values**. These are of great physical and mathematical importance, as they often correspond to configurations with enhanced symmetry or phase transitions.

A value $\mu \in \mathfrak{g}^*$ is a critical value if and only if there exists a point $x \in J^{-1}(\mu)$ that has a non-trivial [isotropy subgroup](@entry_id:200360) $G_x$. In other words, critical values are the images of points that are "more symmetric" than generic points. This has an immediate consequence: if $\mu$ is a critical value, the action of the stabilizer $G_\mu$ on the level set $J^{-1}(\mu)$ cannot be free. This is because for such a point $x$, its [isotropy](@entry_id:159159) algebra $\mathfrak{g}_x$ is a non-trivial subalgebra of $\mathfrak{g}_\mu$, preventing the $G_\mu$ action from being free at $x$. 

When $\mu$ is a critical value, the reduced space $M_\mu = J^{-1}(\mu)/G_\mu$ is generally not a [smooth manifold](@entry_id:156564) but has singularities. The structure of these singular reduced spaces is described by the **Sjamaar-Lerman Theorem**. This theorem reveals that $M_\mu$ is a **stratified symplectic space**. This means that $M_\mu$ can be partitioned into a collection of disjoint, [smooth manifolds](@entry_id:160799) called strata, where each stratum is itself a symplectic manifold.

The stratification arises from the orbit-type decomposition of the original manifold $M$. For each [conjugacy class](@entry_id:138270) $(H)$ of an [isotropy subgroup](@entry_id:200360), the corresponding stratum in the reduced space is $S_{(H)} = (J^{-1}(\mu) \cap M_{(H)})/G_\mu$, where $M_{(H)}$ is the set of all points in $M$ whose [isotropy](@entry_id:159159) group is conjugate to $H$. The Sjamaar-Lerman theorem shows that each such $S_{(H)}$ is a smooth symplectic manifold, with the symplectic form induced from $\omega$ in the usual way. The union of these symplectic strata forms the singular space $M_\mu$, which can be endowed with a compatible **Poisson structure**. The symplectic strata are precisely the symplectic leaves of this Poisson manifold. The proof of this deep result relies on the existence of local [normal form](@entry_id:161181) theorems (the Marle-Guillemin-Sternberg theorem) which provide a standard model for the action near any orbit. 

Crucially, the dynamics of a $G$-invariant Hamiltonian remain well-behaved. The projected flow on the singular space $M_\mu$ exists and, moreover, it respects the stratification. A trajectory that starts in a particular stratum $S_{(H)}$ will remain in that stratum for all time. On each stratum, the reduced flow is Hamiltonian with respect to the stratum's symplectic structure. 

The set of critical values in the image of the momentum map forms a set of "walls". As the momentum value $\mu$ is varied, the topology of the reduced space $M_\mu$ remains constant as long as $\mu$ stays within a connected component of [regular values](@entry_id:161151). However, when $\mu$ crosses a wall, the topology of the reduced space can change dramatically. This **[wall-crossing phenomenon](@entry_id:160224)** is not arbitrary; the change in the manifold structure can be described by a precise [geometric surgery](@entry_id:187761), such as a **symplectic blow-up or blow-down** at a sub-locus corresponding to the critical set. This provides a rich, geometric picture of how phase spaces can transform as symmetry parameters are varied. 