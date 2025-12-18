## Introduction
Noether's theorem stands as a cornerstone of theoretical physics, establishing a profound and beautiful connection between the symmetries of a physical system and its conserved quantities. While often first encountered in a coordinate-based context, its true elegance and power are revealed through the modern language of geometric mechanics. This article aims to bridge the gap between introductory derivations and the advanced, intrinsic formulation used in contemporary research. It moves beyond local coordinates to explore the deep geometric structures that underlie physical laws, providing a unified framework for a vast array of dynamical systems.

By navigating through this material, you will gain a comprehensive understanding of Noether's theorem in its geometric setting. The "Principles and Mechanisms" chapter will lay the theoretical groundwork, reformulating Lagrangian and Hamiltonian mechanics on [smooth manifolds](@entry_id:160799) and introducing the crucial concepts of Lie [group actions](@entry_id:268812) and [momentum maps](@entry_id:178341). Subsequently, "Applications and Interdisciplinary Connections" will demonstrate the theorem's unifying power by applying these principles to diverse areas, from celestial mechanics and [rigid body dynamics](@entry_id:142040) to [field theory](@entry_id:155241) and [nonholonomic systems](@entry_id:173158). Finally, the "Hands-On Practices" section will provide an opportunity to solidify this knowledge by solving concrete problems in this advanced context.

We begin our journey by establishing the fundamental principles, translating the familiar [variational principle](@entry_id:145218) of classical mechanics into the rigorous and elegant language of [differential geometry](@entry_id:145818).

## Principles and Mechanisms

This chapter delves into the core principles and mechanisms of Noether's theorem within the modern framework of geometric mechanics. We move beyond the coordinate-based derivations of introductory physics to a more powerful and elegant formulation on [smooth manifolds](@entry_id:160799). This geometric perspective not only provides deeper insight into the structure of physical laws but also equips us with tools applicable to a vast range of systems, from celestial mechanics to fluid dynamics and [field theory](@entry_id:155241).

### The Variational Principle on Manifolds

The foundation of Lagrangian mechanics is the **[principle of stationary action](@entry_id:151723)**. In the geometric setting, we begin with a smooth, finite-dimensional manifold $Q$, the **configuration space** of the system. The state of the system at any instant includes not only its configuration but also its velocity. The space encompassing all possible configurations and their corresponding velocities is the **tangent bundle**, denoted $TQ$. A point in $TQ$ is a pair $(q, v)$, where $q \in Q$ and $v \in T_qQ$, the [tangent space](@entry_id:141028) to $Q$ at $q$.

The dynamics are encoded in a single scalar function, the **Lagrangian**, $L: TQ \times \mathbb{R} \to \mathbb{R}$, which may depend on position, velocity, and time. A path or trajectory of the system is a curve in the configuration space, $\gamma: [t_0, t_1] \to Q$. To formulate a well-defined variational problem, the path must be sufficiently smooth for its velocity vector, $\dot{\gamma}(t) \in T_{\gamma(t)}Q$, to be a continuous function of time. This requires the path $\gamma$ to be of at least class $C^1$.

The **[action functional](@entry_id:169216)**, $S$, assigns a real number to each such path by integrating the Lagrangian along it:
$$
S[\gamma] = \int_{t_0}^{t_1} L(\gamma(t), \dot{\gamma}(t), t) \, dt
$$
Hamilton's principle asserts that the physical trajectory of the system between two fixed configurations, $\gamma(t_0) = q_0$ and $\gamma(t_1) = q_1$, is one that renders the [action functional](@entry_id:169216) stationary. This means that for any smooth one-parameter family of paths $\gamma_\epsilon(t)$ that start and end at the same points (i.e., $\gamma_0 = \gamma$ and $\gamma_\epsilon(t_0) = q_0$, $\gamma_\epsilon(t_1) = q_1$), the [first variation](@entry_id:174697) of the action must vanish:
$$
\delta S = \left. \frac{d}{d\epsilon} \right|_{\epsilon=0} S[\gamma_\epsilon] = 0
$$
To carry out this differentiation and arrive at the celebrated Euler-Lagrange equations, certain regularity conditions must be met. The calculation involves an [integration by parts](@entry_id:136350), which requires moving a time derivative off the variation of the velocity, $\delta\dot{\gamma}$, and onto the partial derivative of the Lagrangian with respect to velocity, $\partial L / \partial v$. For all the necessary derivatives to be well-defined and continuous, the standard [sufficient condition](@entry_id:276242) is that the Lagrangian $L$ must be of class $C^2$ with respect to its arguments on $TQ \times \mathbb{R}$ . Under these conditions, the stationarity of the action implies that the physical path $\gamma(t)$ must satisfy the **Euler-Lagrange equations**:
$$
\frac{d}{dt} \left( \frac{\partial L}{\partial v^i} \right) - \frac{\partial L}{\partial q^i} = 0
$$
where $(q^i, v^i)$ are local coordinates on $TQ$.

### Symmetries as Lie Group Actions

In the geometric framework, a symmetry of a physical system is formalized as a **Lie group action** that leaves the dynamics invariant. Let $G$ be a Lie group. A smooth **left action** of $G$ on the configuration manifold $Q$ is a [smooth map](@entry_id:160364) $\Phi: G \times Q \to Q$ satisfying two properties:
1.  **Identity:** $\Phi(e, q) = q$ for all $q \in Q$, where $e$ is the [identity element](@entry_id:139321) of $G$.
2.  **Compatibility:** $\Phi(g_1, \Phi(g_2, q)) = \Phi(g_1 g_2, q)$ for all $g_1, g_2 \in G$ and $q \in Q$.

For each group element $g \in G$, the map $\Phi_g(q) := \Phi(g, q)$ is a [diffeomorphism](@entry_id:147249) of $Q$ onto itself. This transformation of the configuration space naturally induces a transformation on the tangent bundle $TQ$, known as the **tangent lift**. The lifted action of $g$ on a state $(q, v_q) \in TQ$ is given by the [tangent map](@entry_id:203492) of $\Phi_g$:
$$
\mathrm{T}\Phi_g : TQ \to TQ, \quad \mathrm{T}\Phi_g(v_q) = (\mathrm{T}_q\Phi_g)(v_q)
$$
where $\mathrm{T}_q\Phi_g: T_qQ \to T_{\Phi_g(q)}Q$ is the derivative (or Jacobian) of the map $\Phi_g$ at the point $q$. The lifted state is $(\Phi_g(q), (\mathrm{T}_q\Phi_g)(v_q))$.

A Lagrangian $L: TQ \to \mathbb{R}$ (assumed to be time-independent for simplicity) is said to possess the symmetry $G$, or to be **$G$-invariant**, if its value is unchanged by the lifted action of any element of the group. That is, for all $g \in G$ and for all $(q, v_q) \in TQ$:
$$
L(\mathrm{T}\Phi_g(v_q)) = L(v_q), \quad \text{or equivalently,} \quad L \circ \mathrm{T}\Phi_g = L
$$
This is the precise geometric statement that the "laws of physics" described by $L$ are the same at all configurations related by the [symmetry group](@entry_id:138562) $G$ .

### Noether's Theorem: The Lagrangian Perspective

Noether's theorem reveals a profound connection: every [continuous symmetry](@entry_id:137257) of the Lagrangian corresponds to a conserved quantity. To see this in the geometric setting, we shift our focus from the [finite group](@entry_id:151756) transformations $\Phi_g$ to their infinitesimal counterparts.

An element $\xi$ of the Lie algebra $\mathfrak{g} = T_eG$ of the group $G$ generates a [one-parameter subgroup](@entry_id:142545) $\exp(s\xi) \in G$. The action of this subgroup on a point $q \in Q$ creates a curve through $q$. The velocity vector of this curve at $s=0$ defines a vector field on $Q$, called the **[infinitesimal generator](@entry_id:270424)** of the action corresponding to $\xi$:
$$
\xi_Q(q) = \left. \frac{d}{ds} \right|_{s=0} \Phi(\exp(s\xi), q)
$$
This vector field $\xi_Q$ encapsulates the "direction" of the symmetry transformation on the configuration manifold. This [infinitesimal generator](@entry_id:270424) on $Q$ can itself be lifted to a vector field $\xi_{TQ}$ on the tangent bundle $TQ$, which generates the lifted flow.

The invariance condition $L \circ \mathrm{T}\Phi_{\exp(s\xi)} = L$ can be differentiated with respect to $s$ at $s=0$. This yields the infinitesimal condition for invariance: the Lie derivative of the Lagrangian with respect to the lifted vector field $\xi_{TQ}$ must be zero:
$$
\mathcal{L}_{\xi_{TQ}} L = 0
$$
Noether's theorem, in this language, states that if the Lagrangian is invariant under the action of $G$, then for each $\xi \in \mathfrak{g}$, the quantity
$$
J_\xi(q,v) = \left\langle \frac{\partial L}{\partial v}, \xi_Q(q) \right\rangle
$$
is conserved along any trajectory satisfying the Euler-Lagrange equations. Here, $\frac{\partial L}{\partial v}$ is the **fiber derivative** of $L$, which gives the [canonical momentum](@entry_id:155151) covector, and $\langle \cdot, \cdot \rangle$ denotes the natural pairing between a [covector](@entry_id:150263) and a vector. The quantity $J_\xi$ is the **Noether current** or conserved momentum associated with the symmetry generator $\xi$. For a Lagrangian of mechanical type, $L(q, \dot{q}) = \frac{1}{2} g_{ij}(q) \dot{q}^i \dot{q}^j - V(q)$, the fiber derivative is $\frac{\partial L}{\partial \dot{q}^i} = g_{ij}(q) \dot{q}^j$. The conserved quantity is then explicitly $J_\xi(q, \dot{q}) = g_{ij}(q) \xi^i(q) \dot{q}^j$, which is the projection of the covariant momentum onto the symmetry direction .

#### Example: Rotational Invariance and Angular Momentum

Let us illustrate this with a classic example. Consider a particle of mass $m$ moving in the plane $Q = \mathbb{R}^2$ under a potential $V$ that depends only on the distance from the origin, $V = V(|q|)$. The Lagrangian is $L(q,v) = \frac{m}{2}|v|^2 - V(|q|)$. This system is symmetric under rotations, which form the Lie group $G = \mathrm{SO}(2)$. The action is $\Phi(R, q) = Rq$, where $R$ is a rotation matrix.

The Lie algebra $\mathfrak{so}(2)$ is one-dimensional and can be generated by the skew-symmetric matrix $\Xi = \begin{pmatrix} 0 & -1 \\ 1 & 0 \end{pmatrix}$. For the generator $\xi=1$, the [one-parameter subgroup](@entry_id:142545) is the family of rotation matrices $R(s) = \exp(s\Xi)$. The [infinitesimal generator](@entry_id:270424) vector field on $Q$ is:
$$
\xi_Q(q) = \left. \frac{d}{ds} \right|_{s=0} (R(s)q) = \Xi q = \begin{pmatrix} -q_2 \\ q_1 \end{pmatrix}
$$
The Lagrangian is invariant because rotations preserve the norms $|q|$ and $|v|$. According to Noether's theorem, the conserved quantity is $J_\xi = \langle \frac{\partial L}{\partial v}, \xi_Q \rangle$. The momentum is $\frac{\partial L}{\partial v} = mv = (mv_1, mv_2)$. The conserved Noether current is thus the inner product:
$$
J(q,v) = (mv_1)(-q_2) + (mv_2)(q_1) = m(q_1 v_2 - q_2 v_1)
$$
This is precisely the familiar expression for the angular momentum about the origin, which we now understand as the conserved quantity associated with [rotational symmetry](@entry_id:137077) .

### The Intrinsic Geometry of Lagrangian Systems

The Euler-Lagrange equations provide a coordinate-dependent description of motion. To achieve a fully geometric and intrinsic picture, we introduce canonical structures on the [tangent bundle](@entry_id:161294) $TQ$. The key objects are the **Poincaré-Cartan 1-form** $\theta_L$ and the **presymplectic 2-form** $\omega_L$.

The form $\theta_L$ can be defined intrinsically as the pullback of the [1-form](@entry_id:275851) $dL$ by the vertical endomorphism $S: TTQ \to TTQ$, which projects [tangent vectors](@entry_id:265494) to $TQ$ onto their vertical components. An equivalent and perhaps more intuitive definition is via the **fiber derivative** (or **Legendre transform**) $F_L: TQ \to T^*Q$, which maps a state $(q,v)$ to the [canonical momentum](@entry_id:155151) $(q, p)$, where $p = \frac{\partial L}{\partial v}$. The cotangent bundle $T^*Q$ carries a canonical 1-form $\theta_{\text{can}}$, and $\theta_L$ is its [pullback](@entry_id:160816): $\theta_L = (F_L)^* \theta_{\text{can}}$. In local coordinates $(q^i, v^i)$ on $TQ$, this gives the simple expression:
$$
\theta_L = \frac{\partial L}{\partial v^i} dq^i
$$
The [exterior derivative](@entry_id:161900) of this 1-form (with a conventional minus sign) defines the presymplectic 2-form:
$$
\omega_L = -d\theta_L
$$
This 2-form $\omega_L$ is **symplectic** (i.e., closed and non-degenerate) if the Lagrangian is **regular**, meaning the fiber Hessian matrix $\frac{\partial^2 L}{\partial v^i \partial v^j}$ is invertible. If the Lagrangian is **singular**, then $\omega_L$ is degenerate (has a non-trivial kernel) and is called **presymplectic**.

The dynamics can be elegantly expressed using these forms. The **Lagrangian energy** function is defined as $E_L = \Delta(L) - L$, where $\Delta$ is the Liouville vector field generating dilations along the fibers of $TQ$. In coordinates, $E_L = v^i \frac{\partial L}{\partial v^i} - L$. The Euler-Lagrange equations are then completely equivalent to the single, intrinsic equation:
$$
i_{X_L} \omega_L = dE_L
$$
where $X_L$ is the vector field on $TQ$ whose [integral curves](@entry_id:161858) are the system's trajectories, and $i_X \omega$ denotes the [interior product](@entry_id:158127). This equation determines the dynamical flow $X_L$. If $L$ is regular, $\omega_L$ is invertible and $X_L$ is uniquely determined. If $L$ is singular, this presymplectic equation only has solutions under certain [consistency conditions](@entry_id:637057) on a constraint [submanifold](@entry_id:262388), a situation that forms the basis for the theory of [constrained systems](@entry_id:164587) .

### The Hamiltonian Perspective: Momentum Maps

While the Lagrangian formalism lives on the tangent bundle $TQ$, the Hamiltonian formalism is naturally situated on the **[cotangent bundle](@entry_id:161289)** $T^*Q$, the space of positions and momenta. This space is the canonical **phase space** of the system, and it comes equipped with a canonical symplectic structure. The canonical [1-form](@entry_id:275851) $\theta_{\text{can}}$ (in [local coordinates](@entry_id:181200) $(q^i, p_i)$, $\theta_{\text{can}} = p_i dq^i$) gives rise to the **canonical symplectic 2-form** $\omega = -d\theta_{\text{can}} = dq^i \wedge dp_i$. A manifold equipped with a closed, non-degenerate 2-form like $(T^*Q, \omega)$ is called a **symplectic manifold**.

When a Lie group $G$ acts on the configuration space $Q$, this action can be "lifted" to an action on the phase space $T^*Q$, called the **cotangent lift**. A symmetry action on a symplectic manifold $(M, \omega)$ is called **Hamiltonian** if it not only preserves the symplectic form (i.e., is an action by symplectomorphisms) but also admits a **momentum map**.

A **momentum map** is a function $J: M \to \mathfrak{g}^*$ from the phase space to the dual of the Lie algebra of the [symmetry group](@entry_id:138562), which serves as the space of conserved quantities. It is defined by the fundamental relation that for every element $\xi \in \mathfrak{g}$, the Hamiltonian vector field generated by the function $J^\xi(m) := \langle J(m), \xi \rangle$ is precisely the [infinitesimal generator](@entry_id:270424) of the action $\xi_M$:
$$
i_{\xi_M} \omega = d J^\xi
$$
Noether's theorem in the Hamiltonian setting is particularly elegant: if a Hamiltonian function $H: M \to \mathbb{R}$ is invariant under the $G$-action, then the momentum map $J$ is conserved along the Hamiltonian flow of $H$. That is, for any trajectory $m(t)$, the value $J(m(t))$ is constant.

#### Example: Symmetries of Euclidean Space

Consider the phase space $T^*\mathbb{R}^2$ with coordinates $(x_1, x_2, p_1, p_2)$ and symplectic form $\omega = dx_1 \wedge dp_1 + dx_2 \wedge dp_2$. Let the group of [rigid motions](@entry_id:170523) in the plane, $G = \mathrm{SE}(2)$, act on the system. An element of $\mathrm{SE}(2)$ is a pair $(R, a)$ of a rotation $R \in \mathrm{SO}(2)$ and a translation $a \in \mathbb{R}^2$. The cotangent lift of this action is $(x,p) \mapsto (Rx+a, Rp)$.

The Lie algebra $\mathfrak{se}(2)$ has generators for translations in the $x_1$ and $x_2$ directions, and for rotations. By applying the defining relation of the momentum map for each generator, we can compute the components of $J: T^*\mathbb{R}^2 \to \mathfrak{se}(2)^*$.
- For translation in $x_1$, $\xi_M = \partial/\partial x_1$, and $dJ^{\text{trans}_1} = i_{\partial/\partial x_1} \omega = dp_1$. Thus, $J^{\text{trans}_1} = p_1$.
- For translation in $x_2$, $\xi_M = \partial/\partial x_2$, and $dJ^{\text{trans}_2} = i_{\partial/\partial x_2} \omega = dp_2$. Thus, $J^{\text{trans}_2} = p_2$.
- For rotation, $\xi_M = -x_2 \partial/\partial x_1 + x_1 \partial/\partial x_2 - p_2 \partial/\partial p_1 + p_1 \partial/\partial p_2$, and $dJ^{\text{rot}} = i_{\xi_M}\omega = d(x_1p_2 - x_2p_1)$. Thus, $J^{\text{rot}} = x_1p_2 - x_2p_1$.

The full momentum map combines these components. In a basis dual to the generators, $J(x,p) = (p_1, p_2, x_1p_2 - x_2p_1)$. These are the conserved linear and angular momenta, which we now understand as components of a single geometric object, the momentum map .

### The Structure of Conserved Quantities: Equivariance and Coadjoint Orbits

The momentum map is more than just a collection of conserved quantities; it possesses a rich geometric structure. A crucial property is **$\mathrm{Ad}^*$-[equivariance](@entry_id:636671)**. A momentum map $J: M \to \mathfrak{g}^*$ is equivariant if it intertwines the [group action](@entry_id:143336) on $M$ with the **coadjoint action** $\mathrm{Ad}^*$ of $G$ on $\mathfrak{g}^*$:
$$
J(g \cdot m) = \mathrm{Ad}^*_g(J(m)) \quad \text{for all } g \in G, m \in M
$$
This property is not guaranteed for all Hamiltonian actions but holds for a large and important class. Its significance is profound: it implies that $J$ is a **Poisson map**. This means it preserves the algebraic bracket structure, mapping the Poisson bracket on the phase space $(M, \omega)$ to the natural **Lie-Poisson bracket** on the dual of the Lie algebra, $(\mathfrak{g}^*, \{\cdot, \cdot\}_{\mathrm{LP}})$.

This has remarkable consequences for a class of systems called **collective systems**, whose Hamiltonians are of the form $H = h \circ J$ for some function $h: \mathfrak{g}^* \to \mathbb{R}$. For such a system, the trajectory of the conserved quantity itself, $\mu(t) = J(m(t))$, is not static but evolves according to the Lie-Poisson equations on $\mathfrak{g}^*$:
$$
\frac{d\mu}{dt} = X_h^{\mathrm{LP}}(\mu)
$$
where $X_h^{\mathrm{LP}}$ is the Hamiltonian vector field for $h$ with respect to the Lie-Poisson bracket. The phase space of these dynamics on $\mathfrak{g}^*$ is foliated by **[symplectic leaves](@entry_id:158259)**, which are precisely the orbits of the coadjoint action, known as **coadjoint orbits**. Since the Lie-Poisson flow is always tangent to these leaves, the trajectory $\mu(t)$ is forever confined to the single coadjoint orbit containing its initial value $\mu(0)$ . This principle, known as the Lie-Poisson reduction theorem, is fundamental to the study of complex systems like the dynamics of a rigid body or an [ideal fluid](@entry_id:272764).

### Extensions of the Noether Formalism

The core theorem can be extended and generalized in several important directions, revealing its true robustness and breadth.

#### Quasi-Invariance and Gauge Symmetries

A Lagrangian need not be strictly invariant for a conservation law to exist. It is sufficient for it to be **quasi-invariant**, meaning that under a symmetry transformation, it changes by a [total time derivative](@entry_id:172646) of a function on the configuration space:
$$
L \circ \mathrm{T}\Phi_g = L + \frac{dF_g}{dt}
$$
This situation is common in electromagnetic theory. The presence of the term $F_g$ modifies the conservation law. The conserved quantity is no longer just the standard Noether current, but is corrected by a term derived from $F_g$. For an infinitesimal symmetry generated by $\xi$, the modified conserved quantity is:
$$
I_\xi = \left\langle \frac{\partial L}{\partial v}, \xi_Q(q) \right\rangle - C(q; \xi)
$$
where the correction term $C(q; \xi)$, known as an **affine [cocycle](@entry_id:200749)**, is given by $C(q; \xi) = \left.\frac{d}{ds}\right|_{s=0} F_{\exp(s\xi)}(q)$.

A paradigmatic example is a particle with charge $q_{el}$ in a constant magnetic field $B$. The Lagrangian $L = \frac{m}{2}|\dot{q}|^2 + \frac{q_{el}B}{2c}(-y\dot{x} + x\dot{y})$ is not invariant under translations, say by a vector $(a,b)$. Instead, it changes by a [total time derivative](@entry_id:172646). The corresponding function $F_{(a,b)}(x,y)$ can be found, and its infinitesimal version gives the [cocycle](@entry_id:200749) correction $C(x,y; (a,b)) = \frac{q_{el}B}{2c}(ay-bx)$ . The resulting conserved quantity is a "magnetic momentum," which differs from the [canonical momentum](@entry_id:155151).

#### The Poisson Setting

The [symplectic framework](@entry_id:1132750) is itself a special case of a more general structure. A **Poisson manifold** $(M, \{\cdot,\cdot\})$ is a manifold where the algebra of [smooth functions](@entry_id:138942) $C^\infty(M)$ is equipped with a **Poisson bracket**—a bilinear operation that is antisymmetric, satisfies the Jacobi identity, and acts as a derivation (the Leibniz rule). Every symplectic manifold is a Poisson manifold, but the converse is not true; Poisson manifolds can have degenerate brackets.

A [group action](@entry_id:143336) on a Poisson manifold is **Hamiltonian** if it preserves the bracket and admits a momentum map $J: M \to \mathfrak{g}^*$ satisfying the condition that the fundamental vector field $X_\xi$ is the Hamiltonian vector field for the function $J^\xi = \langle J, \xi \rangle$. Noether's theorem holds in this general setting: for any $G$-invariant Hamiltonian $H$, the components of the momentum map are conserved. The proof follows directly from the properties of the Poisson bracket:
$$
\frac{d}{dt} J^\xi = \{J^\xi, H\} = X_{J^\xi}(H) = X_\xi(H)
$$
Since $H$ is $G$-invariant, its derivative along any symmetry generator is zero, $X_\xi(H) = 0$, proving the conservation of $J^\xi$ . This formulation is essential for systems that are not naturally symplectic, such as the Lie-Poisson dynamics on $\mathfrak{g}^*$ mentioned previously.

#### Nonholonomic Systems

A final important extension concerns systems with **nonholonomic constraints**—constraints on velocities that are not integrable to constraints on positions (e.g., a rolling ball that cannot slip). The dynamics of such systems are governed by the Lagrange-d'Alembert principle, which restricts virtual displacements to those consistent with the constraints. This introduces non-potential constraint forces into the equations of motion.

The presence of these constraint forces generally breaks the conservation of momentum predicted by Noether's theorem. Even if the Lagrangian and the constraint distribution are invariant under a symmetry group $G$, the [time evolution](@entry_id:153943) of the [canonical momentum](@entry_id:155151) $J_\xi$ is given by:
$$
\frac{d}{dt} J_\xi = \langle \Lambda, \xi_Q \rangle
$$
where $\Lambda$ is the constraint force [covector](@entry_id:150263). The standard conservation law fails because the [constraint forces](@entry_id:170257) can do "work" along the symmetry direction. Consequently, the dynamics are no longer Hamiltonian in the standard sense, and the flow is not symplectic.

However, a conservation law can be recovered under a special condition: if the symmetry itself respects the constraints. If the [infinitesimal generator](@entry_id:270424) of a symmetry, $\xi_Q$, is a vector field that is everywhere tangent to the constraint distribution $D$ (a so-called "horizontal" symmetry), then the constraint force $\Lambda$ (which is in the [annihilator](@entry_id:155446) of $D$) cannot do work along it. In this case, $\langle \Lambda, \xi_Q \rangle = 0$, and the corresponding **nonholonomic momentum** $J_\xi$ is conserved . This highlights that in the world of [nonholonomic mechanics](@entry_id:1128848), not all symmetries are created equal; only those compatible with the constraints lead to conservation laws.