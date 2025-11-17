## Introduction
In Riemannian geometry, the holonomy group serves as a powerful invariant, capturing the global effects of curvature by measuring how vectors twist when parallel transported along closed loops. For a generic manifold, this group is the largest possible, the [special orthogonal group](@entry_id:146418) $\mathrm{SO}(n)$. A central question in modern geometry is: what special geometric structures arise when the [holonomy group](@entry_id:160097) is a [proper subgroup](@entry_id:141915) of $\mathrm{SO}(n)$? This leads to the theory of [special holonomy](@entry_id:158889) manifolds—spaces of exceptional beauty and rigidity whose existence has profound implications across mathematics and physics. This article addresses this question, providing a comprehensive overview of the principles, applications, and practices related to these remarkable geometric objects.

This article is structured into three chapters to guide you from foundational theory to practical application. The first chapter, **Principles and Mechanisms**, introduces the holonomy group, explains the principle of [holonomy](@entry_id:137051) reduction through parallel tensors, and presents Berger's celebrated classification of possible [holonomy groups](@entry_id:191471). It culminates with an introduction to [calibrated geometry](@entry_id:182222), showing how the parallel forms defining [special holonomy](@entry_id:158889) can be used to identify volume-minimizing [submanifolds](@entry_id:159439). The second chapter, **Applications and Interdisciplinary Connections**, explores concrete constructions of [special holonomy](@entry_id:158889) manifolds, their topological constraints, and their crucial role in geometric analysis and theoretical physics, including the study of minimal surfaces and the SYZ conjecture in [mirror symmetry](@entry_id:158730). Finally, the **Hands-On Practices** chapter provides a set of targeted problems to solidify your understanding of these abstract concepts through direct computation and conceptual reasoning.

## Principles and Mechanisms

The geometric character of a Riemannian manifold is encoded in its curvature, which measures the infinitesimal deviation of the geometry from that of flat Euclidean space. The concept of [holonomy](@entry_id:137051) provides a powerful global manifestation of this curvature. It captures the cumulative effect of curvature as one traverses finite paths, providing a bridge between the local, differential properties of the manifold and its global, algebraic and topological structure. In this chapter, we explore the fundamental principles of holonomy, the mechanism of holonomy reduction, and the profound geometric consequences that arise when the holonomy group is "special", leading to the theory of calibrated geometries.

### The Holonomy Group and Curvature

The holonomy group is fundamentally a concept associated with a [connection on a principal bundle](@entry_id:159386). For a Riemannian manifold $(M,g)$, the relevant bundle is the bundle of orthonormal frames, and the connection is the Levi-Civita connection $\nabla$.

#### The Definition of Holonomy

Consider a connected $n$-dimensional Riemannian manifold $(M,g)$. At each point $p \in M$, the [tangent space](@entry_id:141028) $T_pM$ is an $n$-dimensional [inner product space](@entry_id:138414). Given a piecewise smooth path $\gamma: [0,1] \to M$, the Levi-Civita connection $\nabla$ provides a canonical way to "parallel transport" [tangent vectors](@entry_id:265494) along $\gamma$. This defines a linear [isometry](@entry_id:150881) $P_\gamma: T_{\gamma(0)}M \to T_{\gamma(1)}M$.

If we consider a loop $\gamma$ based at a point $p$ (i.e., $\gamma(0)=\gamma(1)=p$), the [parallel transport](@entry_id:160671) map $P_\gamma$ becomes a linear isometry of the tangent space at $p$ onto itself, $P_\gamma: T_pM \to T_pM$. The set of all such transformations, obtained by considering all possible piecewise smooth loops based at $p$, forms a group under composition. This is the **[holonomy group](@entry_id:160097)** of the connection at $p$, denoted $\mathrm{Hol}_p(g)$. By choosing an [orthonormal basis](@entry_id:147779) for $T_pM$, we can identify $\mathrm{Hol}_p(g)$ with a subgroup of the [orthogonal group](@entry_id:152531) $\mathrm{O}(n)$. If $M$ is oriented, the holonomy group is a subgroup of the [special orthogonal group](@entry_id:146418), $\mathrm{Hol}_p(g) \subseteq \mathrm{SO}(n)$. Since different base points in a connected manifold can be joined by a path, their [holonomy groups](@entry_id:191471) are conjugate, and we often speak of "the" [holonomy group](@entry_id:160097) $\mathrm{Hol}(g)$.

The holonomy group measures the failure of a global system of parallel vector fields to exist. If the holonomy group is trivial, meaning $P_\gamma = \mathrm{id}$ for all loops $\gamma$, then the manifold is locally flat (i.e., has zero curvature).

#### Restricted Holonomy and Global Topology

The [holonomy group](@entry_id:160097) $\mathrm{Hol}_p$ is a Lie group, but it is not always connected. Its identity component, denoted $\mathrm{Hol}_p^0$, is called the **restricted holonomy group**. A fundamental theorem states that $\mathrm{Hol}_p^0$ is precisely the subgroup generated by parallel transports along all [null-homotopic](@entry_id:153762) loops based at $p$—that is, loops that can be continuously shrunk to the point $p$ [@problem_id:3033755].

The difference between the full and restricted [holonomy groups](@entry_id:191471) is purely topological. The collection of connected components of $\mathrm{Hol}_p$ forms a discrete group, the [quotient group](@entry_id:142790) $\mathrm{Hol}_p/\mathrm{Hol}_p^0$. This group is determined by the manifold's fundamental group, $\pi_1(M,p)$, which classifies loops up to homotopy. There is a natural surjective [group homomorphism](@entry_id:140603)
$$
\Phi: \pi_1(M,p) \to \mathrm{Hol}_p/\mathrm{Hol}_p^0
$$
defined by sending the homotopy class of a loop $[\gamma]$ to the coset containing its parallel transport operator, $\Phi([\gamma]) = P_\gamma \mathrm{Hol}_p^0$. This map essentially captures the "holonomy of non-contractible loops."

A direct consequence is that if the manifold $M$ is **simply connected** (i.e., $\pi_1(M,p)$ is the [trivial group](@entry_id:151996)), then every loop is [null-homotopic](@entry_id:153762). In this case, the generators for $\mathrm{Hol}_p$ and $\mathrm{Hol}_p^0$ coincide, and thus $\mathrm{Hol}_p = \mathrm{Hol}_p^0$. The [holonomy group](@entry_id:160097) is necessarily connected [@problem_id:3033755]. This simplification is why many foundational results about holonomy, including Berger's classification, are stated for simply connected manifolds.

#### The Ambrose-Singer Theorem: Curvature as Infinitesimal Holonomy

While the restricted [holonomy group](@entry_id:160097) $\mathrm{Hol}_p^0$ is generated by transport around [null-homotopic](@entry_id:153762) loops, its structure is ultimately determined by purely local data: the [curvature tensor](@entry_id:181383) $R$. The curvature tensor $R(X,Y)Z$ can be interpreted as the infinitesimal change in a vector $Z$ when it is parallel transported around a small parallelogram-shaped loop defined by vectors $X$ and $Y$.

The precise relationship is given by the **Ambrose-Singer Holonomy Theorem**. It states that the Lie algebra of the [holonomy group](@entry_id:160097), $\mathfrak{hol}_p$, is the smallest Lie subalgebra of $\mathfrak{so}(T_pM)$ that contains all curvature endomorphisms transported back to $p$. More formally, $\mathfrak{hol}_p$ is generated by all endomorphisms of $T_pM$ of the form
$$
(P_{\gamma_t})^{-1} \circ R_{\gamma(t)}(X,Y) \circ P_{\gamma_t}
$$
where $\gamma$ is any path starting at $p$, $t$ is a parameter along the path, and $X,Y$ are tangent vectors at the point $\gamma(t)$ [@problem_id:3031942]. In essence, the Lie algebra of holonomy is spanned by the values of the [curvature tensor](@entry_id:181383) at every point on the manifold, identified as endomorphisms of a single tangent space via [parallel transport](@entry_id:160671). This powerful theorem establishes that the structure of the connected [holonomy group](@entry_id:160097) $\mathrm{Hol}_p^0$ is entirely determined by the algebraic properties of the [curvature tensor](@entry_id:181383) across the manifold [@problem_id:3033755].

#### Example: Manifolds of Constant Curvature

To see the Ambrose-Singer theorem in action, consider a connected, simply connected $n$-dimensional Riemannian manifold $(M,g)$ with [constant sectional curvature](@entry_id:272200) $K \neq 0$. The [curvature tensor](@entry_id:181383) of such a space has a very specific algebraic form:
$$
R_q(X,Y)Z = K \left( g(Y,Z)X - g(X,Z)Y \right)
$$
for any tangent vectors $X, Y, Z$ at a point $q \in M$.

Let's find the generators of the holonomy algebra $\mathfrak{hol}_p$. A generator is of the form $A_{u,v} = (P_{\gamma_t})^{-1} \circ R_{\gamma(t)}(P_{\gamma_t}u, P_{\gamma_t}v) \circ P_{\gamma_t}$ for $u, v \in T_pM$. Since parallel transport $P_{\gamma_t}$ is an isometry, we find that the action of this generator on a vector $w \in T_pM$ is
$$
A_{u,v}(w) = K \left( g_p(v,w)u - g_p(u,w)v \right)
$$
Remarkably, this expression is independent of the path $\gamma$ and the point $\gamma(t)$. This means the holonomy algebra is generated by the set of endomorphisms $\{ A_{u,v} \mid u,v \in T_pM \}$. If we choose an [orthonormal basis](@entry_id:147779) $\{e_i\}$ for $T_pM$, these generators are spanned by the endomorphisms $A_{e_i, e_j} = K(e_j \otimes e_i^\flat - e_i \otimes e_j^\flat)$. This is precisely the set of all skew-symmetric endomorphisms on $T_pM$. Thus, the holonomy algebra is the full special orthogonal Lie algebra, $\mathfrak{hol}_p = \mathfrak{so}(n)$. Since $M$ is simply connected, the [holonomy group](@entry_id:160097) is the corresponding connected Lie group, $\mathrm{Hol}(g) = \mathrm{SO}(n)$.

This calculation [@problem_id:3033721] shows that for a generic manifold (like one with constant non-zero curvature), the holonomy group is as large as possible: $\mathrm{SO}(n)$. This motivates the central question of the theory: under what conditions is the [holonomy group](@entry_id:160097) a *proper* subgroup of $\mathrm{SO}(n)$? Such manifolds are said to have **[special holonomy](@entry_id:158889)**.

### The Principle of Holonomy Reduction and Berger's Classification

Special [holonomy](@entry_id:137051) arises when the [curvature tensor](@entry_id:181383) possesses specific algebraic symmetries. These symmetries restrict the Lie algebra it can generate, leading to a smaller holonomy group. This reduction has profound geometric implications.

#### Parallel Tensors and Holonomy Reduction

The **principle of [holonomy](@entry_id:137051) reduction** states that the [holonomy group](@entry_id:160097) $\mathrm{Hol}_p(g)$ is a subgroup of $\mathrm{SO}(n)$ if and only if there exists some [tensor field](@entry_id:266532) $T$ on $M$ that is parallel with respect to the Levi-Civita connection, i.e., $\nabla T = 0$. A tensor $T$ is parallel if and only if it is invariant under [parallel transport](@entry_id:160671) along any loop. This means that for any $p \in M$, the tensor $T_p$ at that point must be fixed by every element of the [holonomy group](@entry_id:160097) $\mathrm{Hol}_p(g)$. Consequently, $\mathrm{Hol}_p(g)$ must be a subgroup of the stabilizer of the tensor $T_p$:
$$
\mathrm{Hol}_p(g) \subseteq \mathrm{Stab}_{\mathrm{SO}(n)}(T_p)
$$
The existence of a parallel [tensor field](@entry_id:266532) is therefore equivalent to a reduction of the structure group of the tangent bundle. For example, a manifold admitting a parallel non-degenerate 2-form is a [symplectic manifold](@entry_id:637770); if this form is also compatible with the metric, the manifold is Kähler and its [holonomy](@entry_id:137051) is reduced to the [unitary group](@entry_id:138602) $\mathrm{U}(m)$.

This principle connects holonomy to [representation theory](@entry_id:137998). Given a [holonomy group](@entry_id:160097) $G \subset \mathrm{SO}(n)$, the space of parallel tensors of a certain type on the manifold corresponds to the subspace of tensors fixed by the action of $G$. For instance, on a 6-manifold with [holonomy group](@entry_id:160097) $\mathrm{SU}(3)$, the tangent space at a point $p$ can be identified with $\mathbb{C}^3$. The space of real 3-forms, $\Lambda^3(T_p^*M)$, is a 20-dimensional representation of $\mathrm{SU}(3)$. By decomposing this representation into [irreducible components](@entry_id:153033), one finds that the subspace of invariant vectors is 2-dimensional. This implies the existence of a 2-dimensional space of parallel 3-forms on the manifold [@problem_id:3033740]. These are spanned by the real and imaginary parts of the parallel complex [volume form](@entry_id:161784), which defines the manifold as a Calabi-Yau 3-fold.

#### Reducible versus Irreducible Holonomy

The representation of the holonomy group $\mathrm{Hol}_p$ on the tangent space $T_pM$ may be reducible or irreducible. If the representation is **reducible**, it means there exists a proper, non-trivial subspace $V \subset T_pM$ that is invariant under the action of $\mathrm{Hol}_p$. By the de Rham decomposition theorem, this occurs if and only if the manifold $(M,g)$ is locally a Riemannian product, $(M_1 \times M_2, g_1+g_2)$. In this case, the [holonomy group](@entry_id:160097) of the product is the product of the [holonomy groups](@entry_id:191471) of the factors, $\mathrm{Hol}(g) = \mathrm{Hol}(g_1) \times \mathrm{Hol}(g_2)$.

A concrete example is a [4-manifold](@entry_id:161847) with a [product metric](@entry_id:637352) of the form $g = f(u,v)(du^2+dv^2) + h(x,y)(dx^2+dy^2)$. If the functions $f$ and $h$ are non-constant, the holonomy group of each 2D factor is $\mathrm{SO}(2)$. The [holonomy](@entry_id:137051) of the [4-manifold](@entry_id:161847) is then the reducible group $\mathrm{SO}(2) \times \mathrm{SO}(2) \subset \mathrm{SO}(4)$ [@problem_id:3033726].

If the [holonomy](@entry_id:137051) representation is **irreducible**, the tangent space cannot be split into [invariant subspaces](@entry_id:152829). This means the manifold is not a local product and is, in a sense, "geometrically indecomposable".

#### Berger's Classification Theorem

The central result in the theory is **Berger's classification theorem**, which provides a complete list of possible [holonomy groups](@entry_id:191471) for simply connected, irreducible, non-symmetric Riemannian manifolds. (Symmetric spaces form a separate class and their [holonomy](@entry_id:137051) is fully understood). The astonishing result is that the list is very short.

**Berger's List:** Let $(M^n,g)$ be a simply connected, irreducible, non-symmetric Riemannian manifold. Then its [holonomy group](@entry_id:160097) $\mathrm{Hol}(g)$ must be one of the following:

- **The generic case:**
    - $\mathrm{SO}(n)$ for $n \ge 2$: The manifold has no special parallel tensors besides the metric itself.

- **The special cases:**
    - $\mathrm{U}(m)$ for $n=2m, m \ge 2$: **Kähler manifolds**. These admit a parallel complex structure $J$ and a parallel Kähler 2-form $\omega$.
    - $\mathrm{SU}(m)$ for $n=2m, m \ge 2$: **Calabi-Yau manifolds**. These are Ricci-flat Kähler manifolds, admitting a parallel complex [volume form](@entry_id:161784) $\Omega$.
    - $\mathrm{Sp}(m)$ for $n=4m, m \ge 1$: **Hyperkähler manifolds**. These admit a triplet $(I,J,K)$ of parallel complex structures satisfying the quaternion relations.
    - $\mathrm{Sp}(m)\cdot \mathrm{Sp}(1)$ for $n=4m, m \ge 1$: **Quaternionic-Kähler manifolds**. These admit a parallel rank-3 bundle of almost complex structures.
    - $\mathrm{G}_2$ for $n=7$: **$\mathrm{G}_2$ manifolds**. An exceptional case defined by a parallel 3-form.
    - $\mathrm{Spin}(7)$ for $n=8$: **$\mathrm{Spin}(7)$ manifolds**. An exceptional case defined by a parallel 4-form.

This classification [@problem_id:3033748] is the bedrock of [special geometry](@entry_id:194564). Each entry on this list corresponds to a rich geometric theory defined by the existence of parallel tensors that reduce the [holonomy](@entry_id:137051).

### Mechanisms of Exceptional Holonomy

The appearance of the exceptional Lie groups $\mathrm{G}_2$ and $\mathrm{Spin}(7)$ on Berger's list is particularly fascinating. They are not arbitrary additions but arise naturally from the algebraic geometry of forms and spinors in low dimensions.

#### Stabilizers of Forms and Spinors

The key idea is that these exceptional groups are precisely the stabilizer subgroups of certain "generic" or canonical algebraic objects in their defining representations.

**The $\mathrm{G}_2$ Holonomy:** The group $\mathrm{G}_2$ appears as a holonomy group in dimension 7 through two related mechanisms:
1.  **Stabilizer of a 3-form:** The space of 3-forms on $\mathbb{R}^7$, $\Lambda^3(\mathbb{R}^7)^*$, is 35-dimensional. The [general linear group](@entry_id:141275) $\mathrm{GL}(7, \mathbb{R})$ acts on this space. There is a special [open orbit](@entry_id:198493) of so-called **stable 3-forms**. The stabilizer of any form $\varphi$ in this orbit is precisely the exceptional group $\mathrm{G}_2$. A dimension count confirms this: $\dim \mathrm{GL}(7, \mathbb{R}) - \dim \mathrm{G}_2 = 49 - 14 = 35 = \dim \Lambda^3(\mathbb{R}^7)^*$. Thus, a manifold with a parallel stable 3-form will have its holonomy reduced to $\mathrm{G}_2$ [@problem_id:2968905].
2.  **Stabilizer of a [spinor](@entry_id:154461):** The [spin group](@entry_id:189920) $\mathrm{Spin}(7)$ has an 8-dimensional irreducible [real representation](@entry_id:186010), the spin representation $\Delta_7$. The group $\mathrm{Spin}(7)$ acts transitively on the unit sphere $S^7 \subset \Delta_7$. The stabilizer of any single nonzero spinor $\psi \in \Delta_7$ is a subgroup of $\mathrm{Spin}(7)$ isomorphic to $\mathrm{G}_2$. Again, a dimension count verifies this: $\dim \mathrm{Spin}(7) - \dim \mathrm{G}_2 = 21 - 14 = 7 = \dim S^7$. Therefore, a 7-manifold that is also a [spin manifold](@entry_id:159034) and admits a parallel nonzero [spinor](@entry_id:154461) must have its holonomy contained in $\mathrm{G}_2$ [@problem_id:2968905].

**The $\mathrm{Spin}(7)$ Holonomy:** In dimension 8, the group $\mathrm{Spin}(8)$ has two 8-dimensional real irreducible representations, the half-spin representations $S^+$ and $S^-$. The group $\mathrm{Spin}(8)$ acts transitively on the unit sphere $S^7 \subset S^+$. The stabilizer of a single nonzero chiral [spinor](@entry_id:154461) $\psi \in S^+$ is a subgroup isomorphic to $\mathrm{Spin}(7)$. The dimension count works out: $\dim \mathrm{Spin}(8) - \dim \mathrm{Spin}(7) = 28 - 21 = 7 = \dim S^7$. Consequently, an 8-dimensional [spin manifold](@entry_id:159034) admitting a parallel nonzero chiral [spinor](@entry_id:154461) has its [holonomy](@entry_id:137051) reduced to $\mathrm{Spin}(7)$ [@problem_id:2968905]. The existence of this [parallel spinor](@entry_id:194081) is equivalent to the existence of a parallel 4-form, the Cayley form.

#### The Algebra of a $\mathrm{G}_2$-Structure

The existence of a parallel tensor endows the manifold with a rich algebraic structure at every point. A $\mathrm{G}_2$-structure, for instance, is defined by a stable 3-form $\varphi$. This single object determines the entire Riemannian geometry.
- **The Metric:** The metric $g_\varphi$ can be recovered from $\varphi$ via the identity:
$$
g_{\varphi}(u,v)\,\mathrm{vol}_{\varphi} = \frac{1}{6} (i_{u}\varphi) \wedge (i_{v}\varphi) \wedge \varphi
$$
where $u,v$ are vector fields, $i_u$ is [interior product](@entry_id:158127), and $\mathrm{vol}_\varphi$ is the induced [volume form](@entry_id:161784).
- **The Cross Product:** The 3-form $\varphi$ defines a [vector cross product](@entry_id:156484) $\times_\varphi: TM \times TM \to TM$ via the relation
$$
g_\varphi(u \times_\varphi v, w) = \varphi(u,v,w)
$$
for all vectors $u,v,w$. This is equivalent to defining the [1-form](@entry_id:275851) dual to the cross product as $(u \times_\varphi v)^\flat = i_v i_u \varphi$.
- **The Hodge Dual:** The Hodge dual of $\varphi$ with respect to the [induced metric](@entry_id:160616) $g_\varphi$ is a 4-form $\psi = *_{g_\varphi} \varphi$, known as the associative 4-form. The norm of the 3-form is constant everywhere: $\varphi \wedge *_{g_\varphi}\varphi = |\varphi|^2 \mathrm{vol}_\varphi = 7 \mathrm{vol}_\varphi$ [@problem_id:3033737].

If the holonomy is exactly $\mathrm{G}_2$, the form $\varphi$ is parallel ($\nabla\varphi=0$). This implies $\nabla\psi=0$ as well. These parallel forms have profound consequences for the geometry of submanifolds, which we now explore.

### Calibrated Geometries

The parallel forms that define [special holonomy](@entry_id:158889) manifolds are often examples of a more general structure known as a calibration. The theory of calibrated geometries, developed by Reese Harvey and H. Blaine Lawson, provides a powerful method for identifying volume-minimizing [submanifolds](@entry_id:159439).

#### Calibrations and Volume Minimization

Let $(M^n, g)$ be a Riemannian manifold.

A **calibration** is a closed $k$-form $\alpha$ (i.e., $d\alpha=0$) whose **comass** is everywhere less than or equal to one. The comass at a point $p$ is the maximum value the form can attain on any oriented $k$-dimensional plane in $T_pM$:
$$
\|\alpha\|_{\infty, p} = \sup \left\{ \alpha_p(\xi) \mid \xi \text{ is a unit simple } k\text{-vector in } \Lambda^k T_p M \right\} \le 1
$$
An oriented $k$-dimensional submanifold $N \subset M$ is said to be **calibrated** by $\alpha$ if the form achieves its maximum possible value on every tangent space of $N$. That is, the restriction of $\alpha$ to $N$ is equal to the volume form of $N$:
$$
\alpha|_{T_p N} = \mathrm{vol}_{N,p} \quad \text{for all } p \in N.
$$
[@problem_id:3033712]

#### The Harvey-Lawson Theorem

The importance of these definitions lies in the following fundamental theorem.

**Harvey-Lawson Minimality Theorem:** Let $\alpha$ be a calibration on $(M,g)$. Any compact, oriented submanifold $N$ calibrated by $\alpha$ is **volume-minimizing in its real homology class**. This means that for any other compact, oriented submanifold $N'$ homologous to $N$ (i.e., $[N']=[N] \in H_k(M,\mathbb{R})$), we have
$$
\mathrm{Vol}(N) \le \mathrm{Vol}(N').
$$
The proof is a remarkably elegant application of Stokes' Theorem. Because $N$ is calibrated, its volume is $\mathrm{Vol}(N) = \int_N \mathrm{vol}_N = \int_N \alpha$. Since $N$ and $N'$ are homologous, there is a $(k+1)$-chain $C$ such that $\partial C = N - N'$. As $\alpha$ is closed ($d\alpha=0$), Stokes' theorem gives $\int_N \alpha - \int_{N'} \alpha = \int_{\partial C} \alpha = \int_C d\alpha = 0$. Thus, $\mathrm{Vol}(N) = \int_{N'} \alpha$. Finally, the comass condition implies that on $N'$, the form $\alpha$ is everywhere less than or equal to the volume form, $\alpha|_{N'} \le \mathrm{vol}_{N'}$. Integrating this inequality gives $\int_{N'} \alpha \le \int_{N'} \mathrm{vol}_{N'} = \mathrm{Vol}(N')$. Chaining these together, we get $\mathrm{Vol}(N) \le \mathrm{Vol}(N')$. [@problem_id:3033712]

#### Calibration, Minimality, and Stability

The property of being calibrated is extremely strong.
- A calibrated submanifold is automatically a **[minimal submanifold](@entry_id:200568)**, meaning its [mean curvature](@entry_id:162147) is zero. This is because being a global volume minimizer in its homology class implies it must be a critical point for the volume functional, and the [critical points](@entry_id:144653) are precisely the [minimal submanifolds](@entry_id:204492).
- Furthermore, a calibrated [submanifold](@entry_id:262388) is **stable**. Stability means that the second variation of volume is non-negative for all compactly supported variations. Since a calibrated submanifold is an absolute minimizer (not just a local one), its second variation must be non-negative [@problem_id:3033385].

It is crucial to note that the converse is not true. A minimal and stable submanifold is not necessarily calibrated. Calibration is a sufficient, but not necessary, condition for stability.

#### Calibrations from Special Holonomy

The theory of [special holonomy](@entry_id:158889) provides the most important and fertile source of calibrations. The parallel forms that characterize manifolds with [special holonomy](@entry_id:158889) are automatically closed ($\nabla\alpha=0$ implies $d\alpha=0$) and can be normalized to have comass one. These forms then calibrate special families of submanifolds whose geometry is intimately tied to the holonomy group.

The primary examples are [@problem_id:3033748]:
- **Kähler manifolds** ($\mathrm{Hol}=\mathrm{U}(m)$): The Kähler form $\omega$ is parallel. The powers of the Kähler form, $\alpha_k = \frac{1}{k!}\omega^k$, are calibrations. For $k=1, \dots, m$, the form $\alpha_k$ calibrates **complex [submanifolds](@entry_id:159439)** of complex dimension $k$.
- **Calabi-Yau manifolds** ($\mathrm{Hol}=\mathrm{SU}(m)$): In addition to the Kähler calibrations, the real part of the parallel complex [volume form](@entry_id:161784), $\mathrm{Re}(\Omega)$, is a calibration. It calibrates a class of [minimal submanifolds](@entry_id:204492) of real dimension $m$ known as **special Lagrangian submanifolds**.
- **$\mathrm{G}_2$ manifolds** ($\mathrm{Hol}=\mathrm{G}_2$): The parallel 3-form $\varphi$ calibrates 3-dimensional **associative submanifolds**. Its Hodge dual, the parallel 4-form $\psi=*\varphi$, calibrates 4-dimensional **coassociative [submanifolds](@entry_id:159439)**.
- **$\mathrm{Spin}(7)$ manifolds** ($\mathrm{Hol}=\mathrm{Spin}(7)$): The parallel 4-form $\Phi$, known as the Cayley form, calibrates 4-dimensional **Cayley submanifolds**.

In this way, the abstract algebraic condition of [special holonomy](@entry_id:158889) provides a powerful machine for producing concrete examples of volume-minimizing [submanifolds](@entry_id:159439), weaving together algebraic geometry, representation theory, and geometric analysis.