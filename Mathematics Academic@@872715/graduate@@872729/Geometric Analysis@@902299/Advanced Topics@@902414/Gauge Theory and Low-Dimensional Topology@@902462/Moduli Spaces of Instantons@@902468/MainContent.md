## Introduction
The [moduli spaces](@entry_id:159780) of instantons represent a cornerstone of modern [geometric analysis](@entry_id:157700), providing a profound link between the [differential geometry](@entry_id:145818) of connections and the topology of the underlying manifolds. Arising as special solutions to the Yang-Mills equations in four dimensions, [instantons](@entry_id:153491) are not merely mathematical constructs but have deep roots in quantum [field theory](@entry_id:155241). The central challenge this article addresses is how to rigorously define, analyze, and ultimately utilize the space of all such solutions—the moduli space—to extract meaningful geometric and topological information.

This article provides a graduate-level introduction to this rich subject. We will begin our journey in the **Principles and Mechanisms** chapter by establishing the variational definition of instantons and exploring the topological framework that classifies them. We will then develop the essential analytical tools, from the Atiyah-Hitchin-Singer deformation complex to the Kuranishi model and Uhlenbeck [compactification](@entry_id:150518), which are necessary to understand the intricate local and global structure of these spaces. Following this, the **Applications and Interdisciplinary Connections** chapter will demonstrate the power of this framework, showcasing how instanton [moduli spaces](@entry_id:159780) are used to construct the celebrated Donaldson invariants in four-[manifold topology](@entry_id:270831) and how they connect to algebraic geometry and modern theoretical physics. Finally, the **Hands-On Practices** chapter offers a series of guided problems, allowing readers to engage directly with key computations, such as proving the [conformal invariance](@entry_id:191867) of the anti-[self-duality](@entry_id:140268) condition and calculating the dimension of the moduli space.

## Principles and Mechanisms

This chapter delves into the foundational principles and analytic mechanisms that govern the structure and properties of instanton [moduli spaces](@entry_id:159780). We begin with the variational definition of instantons as absolute minimizers of the Yang-Mills energy, explore the topological framework that classifies the underlying bundles, and then develop the local and global analytic tools necessary to understand the geometry of their [moduli spaces](@entry_id:159780).

### The Variational Principle: Instantons as Minimizers

The starting point for the study of instantons is the **Yang-Mills functional**. Let $P \to X$ be a principal $G$-bundle over a closed, oriented Riemannian $4$-manifold $(X, g)$, where $G$ is a compact, semisimple Lie group. The Lie algebra $\mathfrak{g}$ is equipped with an $\mathrm{Ad}$-invariant inner product $\langle \cdot, \cdot \rangle$. For any connection $A$ on $P$, its curvature $F_A$ is a $\mathfrak{g}$-valued $2$-form on $X$. The Yang-Mills functional measures the total strength of the curvature field:

$$
YM(A) := \int_X |F_A|^2 \, d\mathrm{vol}_g
$$

where the norm $|F_A|^2$ is computed using the metric $g$ on $X$ and the inner product on $\mathfrak{g}$. A central question in [gauge theory](@entry_id:142992) is to find the connections that are [critical points](@entry_id:144653) of this functional. These are called **Yang-Mills connections**. A more restrictive and geometrically profound condition is to find the absolute minima of $YM(A)$ within a fixed topological class of the bundle $P$.

The key to finding these minima in four dimensions lies in the special structure of the space of $2$-forms. The Hodge star operator $*: \Omega^2(X) \to \Omega^2(X)$ is an involution ($*^2 = 1$) on an oriented $4$-manifold, allowing for a decomposition of the space of $2$-forms into the $(\pm 1)$-eigenspaces of self-dual and anti-[self-dual forms](@entry_id:272716): $\Omega^2(X, \mathfrak{g}_P) = \Omega^{2,+}(X, \mathfrak{g}_P) \oplus \Omega^{2,-}(X, \mathfrak{g}_P)$. We can accordingly decompose the curvature into its self-dual and anti-self-dual parts:

$$
F_A = F_A^+ + F_A^-, \quad \text{where} \quad F_A^\pm = \frac{1}{2}(F_A \pm *F_A)
$$

This decomposition is orthogonal with respect to the $L^2$ inner product on forms. Consequently, the Yang-Mills functional splits into two non-negative terms:

$$
YM(A) = \int_X |F_A^+ + F_A^-|^2 \, d\mathrm{vol}_g = \int_X (|F_A^+|^2 + |F_A^-|^2) \, d\mathrm{vol}_g = \|F_A^+\|_{L^2}^2 + \|F_A^-\|_{L^2}^2
$$

This expression is purely geometric. Remarkably, it can be related to a purely topological quantity. Chern-Weil theory provides a topological invariant, the second Chern number (for $G=\mathrm{SU}(n)$) or a related Pontryagin number, which can be computed by integrating a [characteristic polynomial](@entry_id:150909) of the curvature. For a standard choice of normalization, this [topological charge](@entry_id:142322) $k$ is given by:

$$
k = -\frac{1}{8\pi^2} \int_X \langle F_A \wedge F_A \rangle
$$

This value $k$ depends only on the [isomorphism](@entry_id:137127) class of the bundle $P$, not on the choice of connection $A$. Using the self-dual and anti-self-[dual decomposition](@entry_id:169794), the integrand can be rewritten to reveal a deep connection to the $L^2$-norms of $F_A^+$ and $F_A^-$:

$$
\int_X \langle F_A \wedge F_A \rangle = \int_X \langle F_A^+ + F_A^-, *(F_A^+ - F_A^-) \rangle \, d\mathrm{vol}_g = \|F_A^+\|_{L^2}^2 - \|F_A^-\|_{L^2}^2
$$

Combining these two fundamental identities gives the celebrated **Bogomolny-Prasad-Sommerfield (BPS) bound** [@problem_id:3032233]. We have:
1. $YM(A) = \|F_A^+\|_{L^2}^2 + \|F_A^-\|_{L^2}^2$
2. $-8\pi^2 k = \|F_A^+\|_{L^2}^2 - \|F_A^-\|_{L^2}^2$

Adding these equations yields $YM(A) - 8\pi^2 k = 2\|F_A^+\|_{L^2}^2$, while subtracting them gives $YM(A) + 8\pi^2 k = 2\|F_A^-\|_{L^2}^2$. Since the squared norms are non-negative, we obtain the inequality:

$$
YM(A) \ge 8\pi^2 |k|
$$

This provides a universal lower bound on the Yang-Mills energy for any connection in a topological class with charge $k$. The bound is topological, depending only on $k$. Equality is achieved if and only if one of the terms, $\|F_A^+\|_{L^2}^2$ or $\|F_A^-\|_{L^2}^2$, vanishes.
- If $k > 0$, the minimum energy $8\pi^2 k$ is attained precisely when $\|F_A^+\|_{L^2}^2 = 0$, which means $F_A^+ = 0$.
- If $k  0$, the minimum energy $8\pi^2 |k|$ is attained precisely when $\|F_A^-\|_{L^2}^2 = 0$, which means $F_A^- = 0$ (or $*F_A = F_A$).

A connection satisfying the equation $F_A^+ = 0$ is called an **anti-self-dual (ASD) connection**, or an **instanton**. A connection satisfying $F_A^- = 0$ is a **self-dual (SD) connection**. By convention, particularly in the study of $4$-manifold invariants initiated by Donaldson, one focuses on ASD connections. Thus, [instantons](@entry_id:153491) are not merely critical points of the Yang-Mills functional; they are the absolute minimizers of energy in a given topological sector (assuming $k>0$). This variational property is the source of their [geometric rigidity](@entry_id:189736) and analytical importance.

### The Topological Setting: Bundles and Charges

The BPS bound reveals that the existence of [instantons](@entry_id:153491) is tied to the topological charge $k$. This charge, in turn, is determined by the isomorphism class of the [principal bundle](@entry_id:159429). The classification of bundles depends on the structure group $G$ and the topology of the base manifold $X$. For the groups most relevant to Donaldson theory, $\mathrm{SU}(2)$ and $\mathrm{SO}(3)$, the classification schemes present important differences [@problem_id:3032227].

For a principal $\mathrm{SU}(2)$-bundle over a $4$-manifold $X$, the classification is remarkably simple. Isomorphism classes of $\mathrm{SU}(2)$-bundles are in [one-to-one correspondence](@entry_id:143935) with the fourth cohomology group $H^4(X; \mathbb{Z})$. The classifying invariant is the **second Chern class** $c_2(P) \in H^4(X; \mathbb{Z})$. The [instanton](@entry_id:137722) number is its evaluation on the [fundamental class](@entry_id:158335) of $X$: $k = c_2(P)[X]$. Since $c_2(P)$ is an integral class, the charge $k$ is always an integer.

The situation for principal $\mathrm{SO}(3)$-bundles is more subtle. The classification is governed by two characteristic classes:
1. The **second Stiefel-Whitney class** $w_2(P) \in H^2(X; \mathbb{Z}/2)$, which is the obstruction to lifting the $\mathrm{SO}(3)$-bundle to an $\mathrm{SU}(2)$-bundle via the [double cover](@entry_id:183816) $\mathrm{SU}(2) \to \mathrm{SO}(3)$.
2. The **first Pontryagin class** $p_1(P) \in H^4(X; \mathbb{Z})$.

These two classes are not independent. They must satisfy a [congruence relation](@entry_id:272002) involving the Pontryagin square operation $\mathcal{P}: H^2(X; \mathbb{Z}/2) \to H^4(X; \mathbb{Z}/4)$, namely $p_1(P) \pmod{4} \equiv \mathcal{P}(w_2(P))$. For an $\mathrm{SO}(3)$-bundle, the [instanton](@entry_id:137722) charge is defined as $k = -\frac{1}{4}p_1(P)[X]$. The [congruence relation](@entry_id:272002) implies that $k$ is not necessarily an integer. Specifically, $k \pmod{1} \equiv -\frac{1}{4} \mathcal{P}(w_2(P))[X]$. If $w_2(P) \neq 0$, the instanton charge can be a strict fraction, such as an integer plus $\frac{1}{4}$ or $\frac{1}{2}$.

If an $\mathrm{SO}(3)$-bundle $P_{\mathrm{SO}(3)}$ is obtained from an $\mathrm{SU}(2)$-bundle $P_{\mathrm{SU}(2)}$ via the [adjoint representation](@entry_id:146773) (i.e., $P_{\mathrm{SO}(3)} = \mathrm{ad}(P_{\mathrm{SU}(2)})$), then its structure group lifts to $\mathrm{SU}(2)$ by construction. This immediately implies that $w_2(P_{\mathrm{SO}(3)}) = 0$. In this case, the Pontryagin class is related to the second Chern class by the fundamental formula $p_1(P_{\mathrm{SO}(3)}) = -4c_2(P_{\mathrm{SU}(2)})$. The instanton charge for the $\mathrm{SO}(3)$-bundle becomes $k_{\mathrm{SO}(3)} = -\frac{1}{4}(-4c_2(P_{\mathrm{SU}(2)}))[X] = c_2(P_{\mathrm{SU}(2)})[X] = k_{\mathrm{SU}(2)}$, which is an integer. This demonstrates the consistency of the definitions and highlights that fractional charges are a unique feature of $\mathrm{SO}(3)$-bundles that do not admit an $\mathrm{SU}(2)$-structure.

### The Local Structure: Deformation Theory

The space of all gauge-[equivalence classes](@entry_id:156032) of ASD connections on a fixed bundle $P$ is the **[moduli space of instantons](@entry_id:187011)**, denoted $\mathcal{M}$. To understand its geometry, we first study its local structure by linearizing the ASD equation $F_A^+ = 0$ around a known solution. This infinitesimal analysis is captured by the **deformation complex**.

Let $A$ be an ASD connection. A small deformation of $A$ can be written as $A+a$, where $a$ is a $\mathfrak{g}$-valued $1$-form. The curvature of the deformed connection is $F_{A+a} = F_A + d_A a + \frac{1}{2}[a,a]$. The ASD equation becomes $(F_A + d_A a + \frac{1}{2}[a,a])^+ = 0$. Since $F_A^+ = 0$, the linearized equation for an infinitesimal deformation $a$ is $(d_A a)^+ = 0$.

Deformations of the form $a = d_A u$ for some $\mathfrak{g}$-valued function $u \in \Omega^0(X, \mathfrak{g}_P)$ correspond to infinitesimal [gauge transformations](@entry_id:176521). These are considered trivial deformations as they do not change the point in the moduli space. The [tangent space](@entry_id:141028) to the moduli space should therefore be the space of linearized solutions modulo trivial deformations.

This structure is elegantly summarized by the **Atiyah-Hitchin-Singer deformation complex** [@problem_id:3032258]:
$$
0 \to \Omega^0(X, \mathfrak{g}_P) \xrightarrow{d_A} \Omega^1(X, \mathfrak{g}_P) \xrightarrow{d_A^+} \Omega^{2,+}(X, \mathfrak{g}_P) \to 0
$$
where $d_A^+ = \pi_+ \circ d_A$ is the composition of the covariant derivative with the projection onto self-dual $2$-forms. The fact that this is a cochain complex (i.e., $d_A^+ \circ d_A = 0$) is a crucial consequence of the ASD condition itself. The composition is $\pi_+(d_A(d_A u)) = \pi_+([F_A, u])$. Since $A$ is ASD, $F_A$ is anti-self-dual. The Lie bracket $[F_A, u]$ is therefore also an anti-self-dual $2$-form, so its projection to the self-dual part, $\pi_+([F_A, u])$, is zero.

The cohomology groups of this elliptic complex provide the infinitesimal picture of the moduli space at $[A]$:
- $H_A^0 = \ker(d_A)$: The Lie algebra of the stabilizer group of the connection $A$.
- $H_A^1 = \ker(d_A^+) / \mathrm{im}(d_A)$: The formal tangent space to the [moduli space](@entry_id:161715) $\mathcal{M}$ at $[A]$. Its dimension is the "expected dimension" of the [moduli space](@entry_id:161715).
- $H_A^2 = \mathrm{coker}(d_A^+) = \Omega^{2,+}/\mathrm{im}(d_A^+)$: The obstruction space. If $H_A^2 \neq 0$, the moduli space may not be a [smooth manifold](@entry_id:156564) at $[A]$.

A connection $A$ is called **irreducible** if its stabilizer is just the center of the group $G$. Otherwise, it is **reducible**. For $G=\mathrm{SU}(2)$, the center is $\{\pm I\}$, while for $G=\mathrm{SO}(3)$, it is trivial. Reducibility corresponds to $H_A^0$ being non-zero. The [moduli space](@entry_id:161715) $\mathcal{M}$ naturally stratifies according to the stabilizer type [@problem_id:3032260]. The set of irreducible connections forms an open, dense stratum. The loci of reducible connections form lower-dimensional subvarieties where the [moduli space](@entry_id:161715) is typically singular.
- At a regular, irreducible point (where $H_A^2 = 0$ and $H_A^0=0$), the moduli space is locally a [smooth manifold](@entry_id:156564) of dimension $\dim H_A^1$.
- At a reducible point, the non-trivial stabilizer group acts on the [tangent space](@entry_id:141028). For a generic reducible connection on an $\mathrm{SU}(2)$ or $\mathrm{SO}(3)$ bundle, the stabilizer is isomorphic to $\mathrm{U}(1)$ or $\mathrm{SO}(2) \cong S^1$. The local model of the [moduli space](@entry_id:161715) is a quotient of a vector space by this group action, which typically results in an **[orbifold](@entry_id:159587) singularity**.

### The Analytical Framework: The Kuranishi Model

The deformation complex provides a formal, [linear approximation](@entry_id:146101). To construct a rigorous local model of the moduli space, especially near [singular points](@entry_id:266699), a more powerful [nonlinear analysis](@entry_id:168236) is required. This is achieved through the **Kuranishi method**, which provides a finite-[dimensional reduction](@entry_id:197644) of the infinite-dimensional problem [@problem_id:3032254].

The strategy involves two main steps. First, we must handle the infinite-dimensional redundancy due to the gauge group. This is done by imposing a gauge-fixing condition to select a unique representative in each gauge orbit near our solution $A$. A standard choice is the **Coulomb gauge**, $d_A^*a = 0$, where $d_A^*$ is the formal adjoint of $d_A$. This condition defines a slice in the space of connections that is transverse to the gauge orbits.

The ASD equation for a nearby connection $A+a$ in the Coulomb slice is the coupled system:
$$
\begin{cases}
d_A^+ a + (a \wedge a)^+ = 0 \\
d_A^* a = 0
\end{cases}
$$
The linearization of this system is governed by the [elliptic operator](@entry_id:191407) $D = d_A^* \oplus d_A^+$. Elliptic theory on a compact manifold guarantees that $D$ is a Fredholm operator, meaning its kernel and cokernel are finite-dimensional. These are precisely related to the cohomology of the deformation complex: $\ker D \cong H_A^1$ and $\mathrm{coker} D \cong H_A^0 \oplus H_A^2$.

The Kuranishi method employs a form of Lyapunov-Schmidt reduction. The space of $1$-forms $a$ is split into $\ker D$ and its [orthogonal complement](@entry_id:151540). The nonlinear equation is likewise projected onto the image of $D$ and its cokernel.
1. The projection onto the infinite-dimensional space $\mathrm{im} D$ is an equation of the form $D w = N(v, w)$, where $v \in \ker D$, $w$ is in the complement, and $N$ is the nonlinear term. Since $D$ is invertible on $\mathrm{im} D$, one can solve for $w$ as a function of $v$, $w = \Gamma(v)$, using the Implicit Function Theorem for Banach spaces. This effectively parameterizes all nearby solutions in the slice by the finite-dimensional space $\ker D \cong H_A^1$.
2. Substituting this solution $a(v) = v + \Gamma(v)$ back into the equation, we are left with the projection onto the finite-dimensional cokernel, which must also be zero. This yields the **Kuranishi map**:
$$
\kappa: U \subset H_A^1 \to H_A^2, \quad \kappa(v) = \Pi_{H_A^2} \left( (a(v) \wedge a(v))^+ \right)
$$
The local structure of the [moduli space](@entry_id:161715) (in the chosen slice) is precisely the zero set of this smooth, finite-dimensional map, $\kappa^{-1}(0)$. If the connection is regular ($H_A^2=0$), the map is trivial and the moduli space is locally a manifold modeled on $H_A^1$. If obstructions exist ($H_A^2 \neq 0$), the local structure is a potentially singular variety cut out by the Kuranishi map.

### Global Structure I: Compactness and Bubbling

While the Kuranishi model describes the local geometry of the [moduli space](@entry_id:161715), defining global invariants requires understanding its global structure. A primary question is whether the [moduli space](@entry_id:161715) $\mathcal{M}_k$ is compact. In general, it is not.

A sequence of ASD connections $\{A_i\}$ can fail to have a convergent subsequence if their curvature becomes concentrated in smaller and smaller regions. This phenomenon is known as **bubbling**. The fundamental theorem of Uhlenbeck on the compactness of Yang-Mills fields provides a precise description of this process.

The key insight comes from a rescaling argument [@problem_id:3032237]. Suppose the curvature measures $|F_{A_i}|^2 \, d\mathrm{vol}_g$ converge weakly to a measure that includes a Dirac delta mass at a point $x_0 \in X$. This signifies energy concentration. If one "zooms in" on the point $x_0$ by rescaling the metric and pulling back the connections $A_i$, the sequence of rescaled connections, after suitable [gauge fixing](@entry_id:142821), converges to a non-trivial ASD connection on the [tangent space](@entry_id:141028) $T_{x_0}X \cong \mathbb{R}^4$. This limiting connection on $\mathbb{R}^4$ is the "bubble". The [conformal invariance](@entry_id:191867) of the Yang-Mills energy and the ASD equation in four dimensions is essential for this argument. A finite-energy ASD connection on $\mathbb{R}^4$ can be conformally mapped to a smooth ASD connection on the sphere $S^4$, which must have an integer [instanton](@entry_id:137722) number. This proves that the energy (and [topological charge](@entry_id:142322)) lost in a bubble is quantized in integer multiples of the basic [instanton](@entry_id:137722) energy $8\pi^2$.

To handle the non-compactness of $\mathcal{M}_k$, one defines the **Uhlenbeck compactification** $\overline{\mathcal{M}}_k$ by formally adding these [limit points](@entry_id:140908) or "ideal instantons" [@problem_id:3032245]. An element of $\overline{\mathcal{M}}_k$ consists of a pair:
1. A (possibly trivial) ASD connection $[A_\infty]$ of charge $k-\ell$ on $X$.
2. A finite multiset of points in $X$, $\{x_1^{m_1}, \dots, x_r^{m_r}\}$, representing the locations and integer charges of the bubbles, such that the total charge is conserved: $\sum m_j = \ell$.

As a set, the Uhlenbeck compactification has a stratified structure:
$$
\overline{\mathcal{M}}_k = \bigsqcup_{\ell=0}^{k} \mathcal{M}_{k-\ell} \times \mathrm{Sym}^{\ell}(X)
$$
where $\mathrm{Sym}^{\ell}(X)$ denotes the space of unordered multisets of $\ell$ points in $X$. The top stratum ($\ell=0$) is the original [moduli space](@entry_id:161715) $\mathcal{M}_k$. The lower strata correspond to [instantons](@entry_id:153491) that have split into a lower-charge instanton on $X$ and one or more bubbles. It is crucial to recognize that $\overline{\mathcal{M}}_k$ is a compact stratified space, not typically a [manifold with boundary](@entry_id:160030). The codimension of the first bubbling stratum ($\ell=1$) is $4$, which has profound consequences for the definition of invariants.

### Global Structure II: Transversality and Invariants

The second obstacle to using the [moduli space](@entry_id:161715) to define invariants is the presence of singularities, which can occur even on the top stratum $\mathcal{M}_k$. For the [moduli space](@entry_id:161715) to be a [smooth manifold](@entry_id:156564) (or at least a well-behaved [orbifold](@entry_id:159587)), a condition known as **[transversality](@entry_id:158669)** must hold. This means that the nonlinear ASD operator must cut out its zero set transversely.

This condition can fail. Reducible connections are a notorious source of [transversality](@entry_id:158669) failure that is stable under [metric perturbations](@entry_id:160321) [@problem_id:3032256]. A powerful technique to enforce [transversality](@entry_id:158669) is to perturb the underlying geometric problem [@problem_id:3032232]. One can either:
1. Perturb the Riemannian metric $g$ on $X$.
2. Perturb the ASD equation itself, for instance by considering $F_A^+ = \nu$, where $\nu$ is a small, generic, gauge-equivariant self-dual $2$-form.

The Sard-Smale theorem guarantees that for a generic choice of such a perturbation, the resulting perturbed moduli space of irreducible connections, $\mathcal{M}_k^\nu$, is a smooth, [orientable manifold](@entry_id:276936) of the expected dimension. This solves the singularity problem on the irreducible locus.

We are now faced with defining invariants on a space $\mathcal{M}_k^\nu$ that is smooth but non-compact. The Donaldson invariants are obtained by integrating cohomology classes over this space. The non-compactness is handled by using the Uhlenbeck compactification. Because the first bubbling stratum has [codimension](@entry_id:273141) $4$, any cohomology class on $\mathcal{M}_k^\nu$ of degree less than $4$ can be represented by a [differential form](@entry_id:174025) with [compact support](@entry_id:276214). The integral of such a form is well-defined and finite. An analysis of cobordisms between [moduli spaces](@entry_id:159780) for different generic perturbations shows that the resulting integral is independent of the perturbation, thus yielding a topological invariant of $X$.

The final ingredient is the source of these cohomology classes. They are constructed via the **Donaldson $\mu$-map**. This map associates cohomology classes on the moduli space $\mathcal{M}$ to homology classes on the base manifold $X$. The construction requires a **universal bundle** $\mathbb{P} \to \mathcal{M} \times X$ [@problem_id:3032236]. While constructing this bundle rigorously involves technicalities (often using a based gauge group), the result is a characteristic class, such as the universal Pontryagin class $p_1(\mathrm{ad}\,\mathbb{P}) \in H^4(\mathcal{M} \times X; \mathbb{Z})$. The $\mu$-map is then defined using the slant product:
$$
\mu: H_i(X; \mathbb{Z}) \to H^{4-i}(\mathcal{M}; \mathbb{Q})
$$
$$
\mu(\alpha) := -\frac{1}{4} \left( p_1(\mathrm{ad}\,\mathbb{P}) / \alpha \right)
$$
where $\alpha \in H_i(X; \mathbb{Z})$ and $/$ denotes the slant product. The [cup product](@entry_id:159554) of several such $\mu$-classes can be paired with the [fundamental class](@entry_id:158335) of the (perturbed) [moduli space](@entry_id:161715) to define the Donaldson polynomial invariants.

A practical strategy to simplify the entire picture is to work in a setting where reducible solutions do not exist. As noted earlier, reducible $\mathrm{SO}(3)$-connections require the structure group to reduce to a subgroup like $\mathrm{SO}(2)$. This reduction is only possible if $w_2(P)=0$. Therefore, by choosing to study instantons on an $\mathrm{SO}(3)$-bundle with $w_2(P) \neq 0$, one can exclude the possibility of reducible connections from the outset, significantly simplifying the analysis of singularities and [transversality](@entry_id:158669) [@problem_id:3032256].