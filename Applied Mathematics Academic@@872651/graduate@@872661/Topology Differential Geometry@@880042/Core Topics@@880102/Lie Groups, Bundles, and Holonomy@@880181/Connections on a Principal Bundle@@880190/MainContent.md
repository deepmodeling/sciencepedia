## Introduction
The theory of [principal bundles](@entry_id:160029) provides a powerful geometric framework for understanding [symmetries in physics](@entry_id:173615) and mathematics, yet a bundle itself is a static structure. To describe dynamics, field interactions, or the comparison of geometric data across different points on a manifold, we require a concept of differentiation and transport. This knowledge gap is bridged by the mathematical construct of a **connection**. A connection enriches a [principal bundle](@entry_id:159429) with a rule for "connecting" nearby fibers, giving rise to a rich geometric structure with profound physical and topological implications.

This article offers a comprehensive exploration of connections on [principal bundles](@entry_id:160029). In the first chapter, **Principles and Mechanisms**, we will establish the rigorous mathematical foundation, defining the [connection one-form](@entry_id:275839), its associated [horizontal distribution](@entry_id:196663), and deriving the fundamental concepts of [parallel transport](@entry_id:160671), [holonomy](@entry_id:137051), and curvature. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the power of this formalism by showing how it provides the natural language for modern gauge theories in physics—from electromagnetism to Yang-Mills theory—and a tool for uncovering deep topological invariants in geometry. Finally, the **Hands-On Practices** chapter will provide a series of guided problems to solidify these concepts, allowing you to apply the theory to concrete calculations of horizontal lifts, curvature, and [gauge transformations](@entry_id:176521). By progressing through these sections, you will gain a robust understanding of how connections serve as a unifying principle across geometry and physics.

## Principles and Mechanisms

In the preceding chapter, the concept of a [principal bundle](@entry_id:159429) was introduced as the natural geometric arena for gauge theories. It provides a framework that elegantly separates the geometry of the base manifold (spacetime) from the [internal symmetries](@entry_id:199344) of the theory, encoded in the structure group. However, a bundle by itself is a static object. To describe dynamics, such as the interaction of particles or the evolution of fields, we need a notion of differentiation and transport. This is the role of a **connection**. A connection provides a rule for comparing fiber elements at infinitesimally separated points on the base manifold, effectively "connecting" them. This chapter introduces the mathematical formalism of a connection and explores its fundamental properties and consequences, namely parallel transport, holonomy, and curvature.

### The Connection One-Form and the Horizontal Distribution

The tangent space $T_p P$ at any point $p$ in the total space $P$ of a [principal bundle](@entry_id:159429) $\pi: P \to M$ contains a special subspace: the **vertical subspace** $V_p P$. This subspace consists of all vectors tangent to the fiber passing through $p$. Formally, the vertical subspace is the kernel of the differential of the projection map, $V_p P = \ker(d\pi)_p$. The vertical subspace at $p$ is isomorphic to the Lie algebra $\mathfrak{g}$ of the structure group $G$, with the [isomorphism](@entry_id:137127) given by mapping $\xi \in \mathfrak{g}$ to the fundamental vector field $\xi_P$ evaluated at $p$.

A **connection** on the [principal bundle](@entry_id:159429) $P$ is a specification of a complementary subspace at every point, called the **horizontal subspace** $H_p P$, such that $T_p P = H_p P \oplus V_p P$. This choice must be made smoothly across all points and must be compatible with the [group action](@entry_id:143336) on the bundle.

The most powerful and elegant way to define this [horizontal distribution](@entry_id:196663) is through a differential form. A **[connection one-form](@entry_id:275839)** is a $\mathfrak{g}$-valued [one-form](@entry_id:276716) $\omega \in \Omega^1(P, \mathfrak{g})$ that satisfies two defining axioms [@problem_id:2970934] [@problem_id:3031875]:

1.  **Reproduction of Fundamental Vector Fields**: The form $\omega$ maps any fundamental vector field back to the corresponding Lie algebra element. For every $\xi \in \mathfrak{g}$,
    $$
    \omega(\xi_P) = \xi
    $$
    where $\xi_P(p) = \frac{d}{dt}\big|_{t=0} (p \cdot \exp(t\xi))$ is the fundamental vector field associated with $\xi$. This axiom essentially calibrates the one-form on the vertical directions. It ensures that $\omega$ provides an [isomorphism](@entry_id:137127) from the vertical space $V_p P$ to $\mathfrak{g}$.

2.  **Ad-Equivariance**: The form $\omega$ transforms in a specific way under the right action of the group $G$. For any $g \in G$, let $R_g: P \to P$ be the right action map $p \mapsto p \cdot g$. The axiom requires that the pullback of $\omega$ by this map is related to the adjoint representation of $G$ on $\mathfrak{g}$:
    $$
    R_g^* \omega = \operatorname{Ad}_{g^{-1}} \omega
    $$
    where $\operatorname{Ad}_{g^{-1}}(X) = g^{-1}Xg$ for $X \in \mathfrak{g}$ (if $G$ is a [matrix group](@entry_id:156202)). This axiom ensures that the choice of horizontal subspaces is consistent with the symmetry of the bundle.

With the [connection form](@entry_id:160771) $\omega$ in hand, the horizontal subspace at $p$ is defined as its kernel:
$$
H_p P = \ker(\omega_p) = \{ X \in T_p P \mid \omega_p(X) = 0 \}
$$
The first axiom ensures that the only vertical vector in $\ker(\omega_p)$ is the [zero vector](@entry_id:156189), so $H_p P \cap V_p P = \{0\}$. Since the dimension of $V_p P$ is $\dim(\mathfrak{g})$, the dimension of $H_p P$ is $\dim(T_p P) - \dim(\mathfrak{g}) = (\dim(M) + \dim(G)) - \dim(G) = \dim(M)$. This matches the dimension of the tangent space $T_{\pi(p)}M$ of the base manifold.

Furthermore, these definitions guarantee that the [horizontal distribution](@entry_id:196663) $H = \bigcup_{p \in P} H_p P$ is a smooth, $G$-[invariant distribution](@entry_id:750794), and that the differential map $(d\pi)_p$ provides an [isomorphism](@entry_id:137127) from the horizontal subspace $H_p P$ to the tangent space $T_{\pi(p)} M$ of the base manifold [@problem_id:3031875]. The [horizontal distribution](@entry_id:196663) thus provides a way to "lift" [tangent vectors](@entry_id:265494) from the base manifold $M$ to the total space $P$.

Let's make this concrete with an example. Consider the trivial [principal bundle](@entry_id:159429) $P = \mathbb{R}^2 \times U(1)$ over the base $M = \mathbb{R}^2$. A point in $P$ is $(x, y, \theta)$, where $(x,y) \in \mathbb{R}^2$ and $\theta$ is the angle for $U(1)$. The Lie algebra $\mathfrak{u}(1)$ is identified with $\mathbb{R}$. Let's examine the [connection one-form](@entry_id:275839) $\omega = -y dx + x dy + d\theta$ [@problem_id:1530240]. A [tangent vector](@entry_id:264836) $X_p \in T_p P$ at a point $p=(x,y,\theta)$ can be written as $X_p = a (\frac{\partial}{\partial x})_p + b (\frac{\partial}{\partial y})_p + c (\frac{\partial}{\partial \theta})_p$. The vertical subspace is spanned by $(\frac{\partial}{\partial \theta})_p$.

Applying the [connection form](@entry_id:160771) to $X_p$:
$$
\omega_p(X_p) = (-y dx + x dy + d\theta) \left( a \frac{\partial}{\partial x} + b \frac{\partial}{\partial y} + c \frac{\partial}{\partial \theta} \right) = -ya + xb + c
$$
A vector is horizontal if $\omega_p(X_p) = 0$, which means $c = ya - xb$. Any vector $X_p$ can be decomposed into a horizontal part $X_p^H$ and a vertical part $X_p^V$. The vertical part must be a multiple of the basis for the vertical space, so $X_p^V = k (\frac{\partial}{\partial \theta})_p$ for some constant $k$. We can find $k$ by recalling that $\omega$ must annihilate the horizontal component, but not the vertical one. In fact, from the first axiom, we can see that the vertical part of any vector $X_p$ is given by $\omega_p(X_p)$ times the generator of the vertical direction. Let's find the decomposition for the vector $X_p = 2 (\frac{\partial}{\partial x})_p + (\frac{\partial}{\partial y})_p + 4 (\frac{\partial}{\partial \theta})_p$ at the point $p = (3, 4, \pi/6)$.

First, we evaluate $\omega_p(X_p)$:
$$
\omega_p(X_p) = -(4)(2) + (3)(1) + 4 = -8 + 3 + 4 = -1
$$
The fundamental vector field corresponding to the basis element $1 \in \mathbb{R} \cong \mathfrak{u}(1)$ is simply $\frac{\partial}{\partial \theta}$. Since $\omega(\frac{\partial}{\partial \theta}) = d\theta(\frac{\partial}{\partial \theta}) = 1$, the vertical component of $X_p$ is given by $X_p^V = \omega_p(X_p) \cdot (\frac{\partial}{\partial \theta})_p = -1 \cdot (\frac{\partial}{\partial \theta})_p$.

The horizontal component is then $X_p^H = X_p - X_p^V$:
$$
X_p^H = \left( 2 \frac{\partial}{\partial x} + 1 \frac{\partial}{\partial y} + 4 \frac{\partial}{\partial \theta} \right)_p - \left( -1 \frac{\partial}{\partial \theta} \right)_p = 2 \left(\frac{\partial}{\partial x}\right)_p + 1 \left(\frac{\partial}{\partial y}\right)_p + 5 \left(\frac{\partial}{\partial \theta}\right)_p
$$
As a check, applying $\omega_p$ to $X_p^H$ gives $-(4)(2) + (3)(1) + 5 = -8 + 3 + 5 = 0$, confirming that $X_p^H$ is indeed horizontal [@problem_id:1530240]. This decomposition is a central mechanism provided by any connection. A more involved example for a non-abelian $SU(2)$ connection can be found in [@problem_id:933812].

### Parallel Transport and Holonomy

The [horizontal distribution](@entry_id:196663) allows us to define the concept of **parallel transport**. Given a smooth path $\gamma: [0,1] \to M$ on the base manifold, a **[horizontal lift](@entry_id:160651)** of $\gamma$ is a path $\tilde{\gamma}: [0,1] \to P$ in the total space such that it projects down to $\gamma$ (i.e., $\pi(\tilde{\gamma}(t)) = \gamma(t)$) and its tangent vector is always horizontal (i.e., $\tilde{\gamma}'(t) \in H_{\tilde{\gamma}(t)} P$ for all $t$).

For any starting point $p_0$ in the fiber over $\gamma(0)$, there exists a unique [horizontal lift](@entry_id:160651) $\tilde{\gamma}$ starting at $p_0$. The endpoint of this lift, $p_1 = \tilde{\gamma}(1)$, lies in the fiber over $\gamma(1)$. The process of moving from $p_0$ to $p_1$ by following the unique [horizontal lift](@entry_id:160651) of $\gamma$ is called parallel transport. This defines a map from the fiber over $\gamma(0)$ to the fiber over $\gamma(1)$. Since the fibers are principal [homogeneous spaces](@entry_id:271488) for $G$, this map can be identified with an element of $G$.

If the path $\gamma$ is a closed loop, starting and ending at $x_0 = \gamma(0) = \gamma(1)$, parallel transport defines a map from the fiber $\pi^{-1}(x_0)$ to itself. This map is given by right multiplication by a specific group element $g_\gamma \in G$. This element is called the **holonomy** of the connection along the loop $\gamma$. The set of all such elements for all loops based at $x_0$ forms a subgroup of $G$, called the **[holonomy group](@entry_id:160097)**.

In practice, for a local section, parallel transport is calculated by solving a differential equation. For a path $\gamma(t)$, the parallel transport of a state $\Psi$ (which can be thought of as a section of an associated [vector bundle](@entry_id:157593)) is governed by the equation
$$
\frac{d\Psi}{dt} + A_{\mu}(\gamma(t))\frac{d\gamma^\mu}{dt}\Psi(t) = 0
$$
where $A$ is the local [connection form](@entry_id:160771). The solution gives the final state as $\Psi(t_f) = U_\gamma \Psi(t_i)$, where $U_\gamma$ is the [parallel transport](@entry_id:160671) operator, also known as a **Wilson line**. It is given by the path-ordered exponential:
$$
U_{\gamma} = \mathcal{P} \exp\left(-\int_{\gamma} A\right)
$$
As an illustration, consider an $SU(2)$ connection on $\mathbb{R}^2$ given by $A = i(\alpha y \sigma_1 dx + \beta x \sigma_2 dy)$ and a straight-line path from $(0,0)$ to $(L, \eta L)$ [@problem_id:933814]. Parametrizing the path as $\gamma(t) = (Lt, \eta L t)$ for $t \in [0,1]$, we evaluate the integral of the connection pullback along the path:
$$
\int_\gamma A = \int_0^1 A_\mu(\gamma(t)) \frac{d\gamma^\mu}{dt} dt = \int_0^1 \left( i\alpha(\eta Lt)\sigma_1 \cdot L + i\beta(Lt)\sigma_2 \cdot (\eta L) \right) dt
$$
$$
= i\eta L^2 (\alpha\sigma_1 + \beta\sigma_2) \int_0^1 t \,dt = \frac{i\eta L^2}{2}(\alpha\sigma_1 + \beta\sigma_2)
$$
Since the matrix being integrated is proportional to a constant matrix $N = \alpha\sigma_1 + \beta\sigma_2$, the path-ordering $\mathcal{P}$ is trivial, and the parallel transport operator is a standard matrix exponential:
$$
U_\gamma = \exp\left( - \frac{i\eta L^2}{2}(\alpha\sigma_1 + \beta\sigma_2) \right)
$$
This can be evaluated using properties of Pauli matrices to find an explicit matrix, demonstrating how the abstract concept of parallel transport leads to concrete physical predictions.

### Local Forms and Gauge Transformations

While the [connection one-form](@entry_id:275839) $\omega$ on $P$ is the geometrically fundamental object, it is often more practical to work with a related form on the base manifold $M$. This is achieved by choosing a **local section**, which is a map $s: U \to P$ from an open set $U \subset M$ into the total space such that $\pi(s(x)) = x$ for all $x \in U$. A section is essentially a choice of a point in the fiber above each point in $U$.

Given a section $s$, we can pull back the [connection form](@entry_id:160771) $\omega$ to obtain a $\mathfrak{g}$-valued one-form on $U$:
$$
A = s^*\omega \in \Omega^1(U, \mathfrak{g})
$$
This form $A$ is known as the **local [connection form](@entry_id:160771)** or, in physics, the **[gauge potential](@entry_id:188985)**.

The choice of section is not unique. If we choose a different section $s'$, it will be related to $s$ by a function $u: U \to G$ such that $s'(x) = s(x) \cdot u(x)$. This change of local section is called a **gauge transformation**. The local [connection form](@entry_id:160771) $A'$ corresponding to the section $s'$ is related to $A$ by the **gauge transformation law**. A careful derivation using the axioms of $\omega$ shows:
$$
A' = \operatorname{Ad}_{u^{-1}} A + u^{-1} du
$$
where $u^{-1}du$ is the Maurer-Cartan form on $G$ pulled back to $U$. This equation is fundamental to all gauge theories. For a [matrix group](@entry_id:156202), it reads $A' = u^{-1}Au + u^{-1}du$. It is crucial to note that different conventions exist; for example, a transformation of the form $uAu^{-1} + du u^{-1}$ would correspond to a different convention for the bundle action [@problem_id:3031875].

To see this transformation in action, consider an $SU(2)$ [gauge potential](@entry_id:188985) on $\mathbb{R}^3$ with components $A_y = \alpha z T_1$ and $A_z = \beta y T_2$ (with $A_x = 0$), where $T_a$ are the generators of $\mathfrak{su}(2)$ [@problem_id:933695]. Let's apply a [gauge transformation](@entry_id:141321) $g(x,y,z) = \exp(\gamma y T_3)$. The $y$-component of the transformed potential $A'_y$ is given by:
$$
A'_y = g^{-1} A_y g + g^{-1} \partial_y g
$$
The first term is the [adjoint action](@entry_id:141823): $g^{-1}A_y g = g^{-1}(\alpha z T_1)g = \alpha z (g^{-1} T_1 g)$. The action of $g = \exp(\gamma y T_3)$ is a rotation around the third axis in the Lie algebra. Specifically, $g^{-1}T_1 g = \cos(\gamma y)T_1 - \sin(\gamma y)T_2$.
The second term is $g^{-1}\partial_y g = g^{-1} (\gamma T_3 g) = \gamma T_3$.
Combining these gives:
$$
A'_y = \alpha z (\cos(\gamma y)T_1 - \sin(\gamma y)T_2) + \gamma T_3
$$
From this expression, we can read off the component of $A'_y$ along the generator $T_2$, which is $-\alpha z \sin(\gamma y)$. This demonstrates how the components of the [gauge potential](@entry_id:188985) mix and change under a [gauge transformation](@entry_id:141321).

### Curvature: The Measure of Non-Integrability

What happens if we [parallel transport](@entry_id:160671) a vector around an infinitesimal closed loop? If the connection is "flat", we should return to where we started. If not, the [holonomy](@entry_id:137051) will be a non-identity group element. The **curvature** of a connection is the quantity that measures this failure. Geometrically, it measures the "twisting" of the horizontal subspaces, or more formally, the failure of the [horizontal distribution](@entry_id:196663) to be integrable.

The holonomy around an infinitesimal rectangular loop in the $x$-$y$ plane is, to leading order, given by $Hol(\gamma, A) \approx \mathbf{1} + F_{xy} \,dx \wedge dy$, where $F_{xy}$ is the component of the curvature 2-form [@problem_id:933822]. This provides a deep [geometric interpretation of curvature](@entry_id:637485) as infinitesimal holonomy.

Formally, the **[curvature two-form](@entry_id:187677)** $\Omega$ is a $\mathfrak{g}$-valued two-form on the total space $P$, defined by the **Cartan structure equation**:
$$
\Omega = d\omega + \frac{1}{2}[\omega, \omega]
$$
Here, the bracket $[\alpha, \beta]$ of two $\mathfrak{g}$-valued forms is defined by combining the [wedge product](@entry_id:147029) of forms with the Lie bracket in $\mathfrak{g}$: for a $p$-form $\alpha$ and a $q$-form $\beta$, $[\alpha, \beta](X_1, \dots) = \frac{1}{p!q!} \sum_{\sigma} \operatorname{sgn}(\sigma) [\alpha(X_{\sigma(1)}, \dots), \beta(X_{\sigma(p+1)}, \dots)]$.

The [curvature form](@entry_id:158424) $\Omega$ has two fundamental properties that follow directly from this definition and the axioms of $\omega$ [@problem_id:3031875]:
1.  **Horizontality**: $\Omega$ vanishes if any of its arguments is a vertical vector. That is, $\iota_{\xi_P} \Omega = 0$ for any fundamental vector field $\xi_P$.
2.  **Ad-Equivariance**: $\Omega$ transforms under the [group action](@entry_id:143336) just like $\omega$ does: $R_g^* \Omega = \operatorname{Ad}_{g^{-1}}\Omega$. This property can be verified through a direct, albeit lengthy, calculation [@problem_id:933679].

Because of these properties, $\Omega$ is a basic form, meaning it is determined by its values on horizontal vectors and is projectable to the base manifold. Pulling back $\Omega$ by a local section $s$ gives the **local [curvature form](@entry_id:158424)** or **field strength** $F$ on $U \subset M$:
$$
F = s^*\Omega = s^*(d\omega + \frac{1}{2}[\omega,\omega]) = d(s^*\omega) + \frac{1}{2}[s^*\omega, s^*\omega]
$$
This gives the local form of the Cartan structure equation in terms of the [gauge potential](@entry_id:188985) $A$:
$$
F = dA + \frac{1}{2}[A, A]
$$
This is one of the most important equations in modern physics, relating the field strength (the physically observable field) to the [gauge potential](@entry_id:188985).

Let's compute the curvature for a given connection. Consider the $\mathfrak{su}(3)$-valued connection on $\mathbb{R}^3$ given by $A = g y L_1 dx + g x L_2 dy$, where $L_1, L_2$ are constant matrices [@problem_id:1530284]. We want to find the component $F_{xy}$ of the curvature $F = F_{xy} dx \wedge dy + \dots$. The formula for the components is $F_{\mu\nu} = \partial_\mu A_\nu - \partial_\nu A_\mu + [A_\mu, A_\nu]$.
Here, $A_x = g y L_1$ and $A_y = g x L_2$.
$$
F_{xy} = \partial_x(g x L_2) - \partial_y(g y L_1) + [g y L_1, g x L_2]
$$
$$
F_{xy} = g L_2 - g L_1 + g^2 xy [L_1, L_2]
$$
This calculation shows how both the non-constancy of the potential (the derivative terms) and the non-abelian nature of the group (the commutator term) contribute to the curvature.

### The Bianchi Identity and Flat Connections

The [curvature form](@entry_id:158424) is not arbitrary; it must satisfy a differential constraint known as the **Bianchi identity**. Taking the exterior derivative of the Cartan structure equation for $\Omega$ and using the properties of the [exterior derivative](@entry_id:161900) and the Lie bracket leads to the remarkably simple result:
$$
d\Omega + [\omega, \Omega] = 0
$$
This expression is often denoted by $D\Omega = 0$, where $D$ is the [covariant exterior derivative](@entry_id:197546). This identity is a direct consequence of the definitions and holds for any connection [@problem_id:3031875] [@problem_id:1530271]. When pulled back to the base manifold, it gives the local form of the Bianchi identity: $dF + [A, F] = 0$, often written as $D_A F = 0$.

A connection is called **flat** if its curvature is zero, i.e., $\Omega = 0$. Locally, this means $F = dA + \frac{1}{2}[A, A] = 0$. Flat connections are geometrically special. The vanishing of curvature means that the [horizontal distribution](@entry_id:196663) is integrable in the sense of Frobenius; the horizontal subspaces piece together to form a family of submanifolds. This implies that the holonomy of the connection around a contractible loop is trivial.

On a [simply connected manifold](@entry_id:184703) (or an open, simply connected subset $U \subset M$), a flat connection is always "pure gauge." This means that if $F=0$ on $U$, there exists a gauge transformation $u: U \to G$ that makes the connection trivial, i.e., the transformed [gauge potential](@entry_id:188985) $A'$ is zero. The gauge transformation $u$ is found by solving the system of differential equations $du = -Au$ [@problem_id:3031875]. The condition $F=0$ is precisely the [integrability condition](@entry_id:160334) for this system of equations. One can solve for $u(x)$ by path-integrating $A$ from a base point, and on a simply-[connected domain](@entry_id:169490), the result is independent of the path [@problem_id:933693].

It is critical to distinguish this local result from the global situation. A flat connection on a non-[simply connected manifold](@entry_id:184703) $M$ does *not* imply that the [principal bundle](@entry_id:159429) is trivial. The holonomy around non-contractible loops can be non-trivial, which can act as an obstruction to finding a global flat section, meaning the bundle itself can be topologically non-trivial [@problem_id:3031875].

### Connection to Riemannian Geometry

The abstract language of [principal bundles](@entry_id:160029) and connections unifies many concepts in geometry. A prime example is the Levi-Civita connection from Riemannian geometry [@problem_id:2972191]. The [tangent bundle](@entry_id:161294) $TM$ of a manifold can be viewed as a [vector bundle](@entry_id:157593) associated with the **principal [frame bundle](@entry_id:187852)** $\mathrm{Fr}(M)$. A point in $\mathrm{Fr}(M)$ over $x \in M$ is an ordered basis (a "frame") of the tangent space $T_x M$. The structure group is $G = \mathrm{GL}(n, \mathbb{R})$.

A connection on $TM$, such as the Levi-Civita connection, can be seen as a connection induced by a principal connection on $\mathrm{Fr}(M)$. In a local coordinate system $\{x^i\}$, the coordinate vectors $\{\partial_i\}$ form a local frame (a local section of $\mathrm{Fr}(M)$). The local [connection form](@entry_id:160771) $A = s^*\omega$ is a $\mathfrak{gl}(n, \mathbb{R})$-valued one-form, which is simply a matrix of real-valued [one-forms](@entry_id:270392), $A = (\omega^i{}_j)$.

These connection [one-forms](@entry_id:270392) are directly related to the Christoffel symbols $\Gamma^i{}_{jk}$ of the connection, which are defined by $\nabla_{\partial_k} \partial_j = \Gamma^i{}_{jk} \partial_i$. The relationship is:
$$
\omega^i{}_j = \Gamma^i{}_{jk} dx^k
$$
Thus, the Christoffel symbols are nothing more than the components of the local connection [one-forms](@entry_id:270392) in a [coordinate basis](@entry_id:270149).

The defining properties of the Levi-Civita connection can also be phrased in this language:
-   **Torsion-free**: The condition $T(X,Y) = \nabla_X Y - \nabla_Y X - [X,Y] = 0$ is equivalent, in a coordinate frame, to the symmetry of the lower indices of the Christoffel symbols: $\Gamma^i{}_{jk} = \Gamma^i{}_{kj}$.
-   **Metric-compatibility**: The condition $\nabla g = 0$ implies that in an [orthonormal frame](@entry_id:189702) (not necessarily a coordinate frame), the matrix of [connection forms](@entry_id:263247) $(\omega^i{}_j)$ is skew-symmetric. This property does not translate to a simple symmetry for the Christoffel symbols, which are defined in a coordinate frame.

Finally, the powerful geometric idea of "locally [inertial frames](@entry_id:200622)" in general relativity has a beautiful counterpart here. At any point $p \in M$, one can choose Riemannian [normal coordinates](@entry_id:143194) such that all Christoffel symbols vanish at that point: $\Gamma^i{}_{jk}(p) = 0$. From the relation above, this is equivalent to the local [connection form](@entry_id:160771) vanishing at that point, $A_p = 0$. In the language of gauge theory, this corresponds to choosing a gauge where the [gauge potential](@entry_id:188985) is zero at a point.