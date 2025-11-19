## Introduction
The study of [differential forms](@entry_id:146747) on [smooth manifolds](@entry_id:160799) provides a powerful framework for understanding intrinsic [topological properties](@entry_id:154666), elegantly captured by de Rham cohomology. However, this topological structure exists independently of any geometric measure. A fundamental question arises: how does introducing a metric—a way to measure lengths and angles—interact with and enrich this topological picture? The answer lies at the heart of Hodge theory, which introduces a canonical differential operator, the Hodge Laplacian, that masterfully bridges the analytical, geometric, and topological worlds.

This article addresses the construction and profound implications of this operator. It moves beyond the purely topological aspects of the exterior derivative to explore the rich structure that emerges when combined with a Riemannian metric.

The reader will embark on a comprehensive exploration of this subject. The first chapter, **Principles and Mechanisms**, will deconstruct the Hodge Laplacian into its fundamental components—the [exterior derivative](@entry_id:161900), the Hodge star, and the [codifferential](@entry_id:197182)—and establish its core properties, culminating in the celebrated Hodge Decomposition Theorem. The second chapter, **Applications and Interdisciplinary Connections**, will showcase the operator's immense utility, demonstrating how it reveals the topology of canonical spaces, proves powerful [vanishing theorems](@entry_id:193143), and provides the analytical backbone for theories in modern physics and Kähler geometry. Finally, **Hands-On Practices** will offer a set of guided problems to solidify these theoretical concepts through concrete computation and application.

## Principles and Mechanisms

In this chapter, we transition from the introductory concepts of [differential forms](@entry_id:146747) to the core machinery of Hodge theory. Our objective is to construct and analyze a canonical second-order differential operator, the **Hodge Laplacian**, which acts on the space of [differential forms](@entry_id:146747). This operator, arising from the interplay between the topological structure of the [exterior derivative](@entry_id:161900) and the geometric structure of a Riemannian metric, provides a profound link between the analysis, geometry, and topology of a manifold. We will dissect its constituent parts, establish its fundamental properties, and explore the mechanisms through which it reveals deep structural information about the underlying space.

### The Operators of Hodge Theory

The Hodge Laplacian is built from three fundamental operators: the exterior derivative $d$, the Hodge star operator $\star$, and the [codifferential](@entry_id:197182) $\delta$. Understanding each is a prerequisite for understanding their synthesis.

#### The Exterior Derivative $d$

As established previously, the **[exterior derivative](@entry_id:161900)** $d$ is a sequence of maps $d_k: \Omega^k(M) \to \Omega^{k+1}(M)$ that generalizes the gradient, curl, and divergence operations of vector calculus. Its definition and properties are intrinsic to the smooth structure of the manifold, independent of any metric. Two of its most crucial properties are its [nilpotency](@entry_id:147926) and its behavior with respect to the wedge product.

First, the property that applying the [exterior derivative](@entry_id:161900) twice yields zero, expressed as $d \circ d = 0$ or simply **$d^2 = 0$**, is fundamental. This captures, in an abstract setting, the familiar [vector calculus identities](@entry_id:161863) $\text{curl}(\text{grad} f) = \mathbf{0}$ and $\text{div}(\text{curl} \mathbf{F}) = 0$. This [nilpotency](@entry_id:147926) is the cornerstone of de Rham cohomology, allowing us to define closed forms (those in $\ker d$) and [exact forms](@entry_id:269145) (those in $\mathrm{im}\ d$), where every exact form is necessarily closed.

Second, the [exterior derivative](@entry_id:161900) acts as a graded derivation of degree $+1$ on the algebra of [differential forms](@entry_id:146747). This is codified in the **graded Leibniz rule**: for any $\alpha \in \Omega^k(M)$ and $\beta \in \Omega^\ell(M)$, the following holds:
$$
d(\alpha \wedge \beta) = (d\alpha) \wedge \beta + (-1)^k \alpha \wedge (d\beta)
$$
These two properties completely characterize the exterior derivative and are essential for all subsequent constructions [@problem_id:2998558].

#### The Hodge Star Operator $\star$ and the Inner Product

While the exterior derivative is a topological tool, the introduction of a Riemannian metric $g$ endows the manifold with a rich geometric structure. The metric defines, at each point $p \in M$, an inner product on the tangent space $T_pM$. This inner product extends naturally to an inner product, which we also denote by $\langle \cdot, \cdot \rangle_g$, on the space of $k$-covectors $\Lambda^k T_p^*M$.

The **Hodge star operator**, denoted $\star$, is the crucial link between this pointwise inner product and the [exterior algebra](@entry_id:201164) of forms. For an $n$-dimensional oriented Riemannian manifold $(M, g)$, the Hodge star is a [linear isomorphism](@entry_id:270529) $\star: \Omega^k(M) \to \Omega^{n-k}(M)$ defined pointwise by the relation:
$$
\alpha \wedge (\star\beta) = \langle \alpha, \beta \rangle_g \, d\mathrm{vol}_g
$$
for all $\alpha, \beta \in \Omega^k(M)$, where $d\mathrm{vol}_g$ is the Riemannian volume form associated with the metric $g$ and the orientation. Applying the operator twice results in a simple scaling: on a $k$-form $\omega$, it can be shown that $\star\star\omega = (-1)^{k(n-k)}\omega$.

This pointwise inner product can be integrated over the manifold to define a global **$L^2$ inner product** on the space of $k$-forms:
$$
\langle \alpha, \beta \rangle_{L^2} = \int_M \langle \alpha, \beta \rangle_g \, d\mathrm{vol}_g = \int_M \alpha \wedge (\star\beta)
$$
This inner product turns the space of square-integrable $k$-forms into a Hilbert space, providing the analytic framework for Hodge theory.

#### The Codifferential $\delta$

With the $L^2$ inner product established, we can now introduce the **[codifferential](@entry_id:197182)**, or Hodge-de Rham operator, $\delta: \Omega^k(M) \to \Omega^{k-1}(M)$. It is defined as the formal adjoint of the [exterior derivative](@entry_id:161900) $d$ with respect to the $L^2$ inner product. This means that for any forms $\alpha \in \Omega^{k-1}(M)$ and $\beta \in \Omega^k(M)$ (where at least one has [compact support](@entry_id:276214), or if $M$ is a closed manifold), the following holds:
$$
\langle d\alpha, \beta \rangle_{L^2} = \langle \alpha, \delta\beta \rangle_{L^2}
$$
This definition elegantly mirrors the concept of an [adjoint operator](@entry_id:147736) in linear algebra. Using this adjoint property and Stokes' theorem, one can derive an explicit formula for the [codifferential](@entry_id:197182) in terms of the Hodge star and the [exterior derivative](@entry_id:161900) [@problem_id:2998573]:
$$
\delta = (-1)^{n(k+1)+1} \star d \star
$$
This formula makes it clear that, unlike the exterior derivative $d$, the [codifferential](@entry_id:197182) $\delta$ is fundamentally dependent on the metric $g$ through the presence of the Hodge star operator. Consequently, $\delta$ does not, in general, commute with [pullbacks](@entry_id:160469) under arbitrary [smooth maps](@entry_id:203730) [@problem_id:2998558].

Just as $d^2=0$, the [codifferential](@entry_id:197182) is also nilpotent: **$\delta^2 = 0$**. This can be proven elegantly from its definition as the adjoint of $d$. For appropriate forms $\alpha$ and $\beta$, we have $\langle \delta^2 \alpha, \beta \rangle = \langle \delta\alpha, d\beta \rangle = \langle \alpha, d^2\beta \rangle = \langle \alpha, 0 \rangle = 0$. Since this holds for all $\beta$, we must have $\delta^2\alpha = 0$ [@problem_id:2998558] [@problem_id:2998573]. Forms in the kernel of $\delta$ are called **co-closed**, while forms in the image of $\delta$ are called **co-exact**.

#### Concrete Examples and Interpretations

To build intuition, it is invaluable to connect these abstract definitions to more familiar concepts from vector calculus on a Riemannian manifold $(M,g)$ [@problem_id:3035715].

For a $0$-form, i.e., a smooth function $f \in \Omega^0(M)$, the [codifferential](@entry_id:197182) $\delta$ maps to the space of $(-1)$-forms, which is trivial. Thus, we always have:
$$
\delta f = 0
$$

For a $1$-form $\alpha \in \Omega^1(M)$, the situation is more interesting. Associated with $\alpha$ is its dual vector field $\alpha^\sharp$, defined by $g(\alpha^\sharp, Y) = \alpha(Y)$ for any vector field $Y$. A local coordinate calculation reveals a beautiful identity:
$$
\delta\alpha = -\text{div}(\alpha^\sharp)
$$
where $\text{div}(V) = \frac{1}{\sqrt{\det(g_{ij})}} \sum_j \frac{\partial}{\partial x^j}(\sqrt{\det(g_{ij})} V^j)$ is the standard expression for the [divergence of a vector field](@entry_id:136342) $V$ in Riemannian geometry. In this sense, the [codifferential](@entry_id:197182) acting on $1$-forms is a direct generalization of the negative divergence. For example, on $\mathbb{R}^2$ with a conformal metric $g = e^{2xy}(dx^2+dy^2)$, for the $1$-form $\alpha = (x^2y+\sin(x))dx + (\exp(xy)+y)dy$, one finds that $\delta\alpha = -e^{-2xy}(\frac{\partial \alpha_1}{\partial x} + \frac{\partial \alpha_2}{\partial y}) = -e^{-2xy}(2xy + \cos(x) + xe^{xy} + 1)$ [@problem_id:3035715].

### The Hodge Laplacian $\Delta$

Having defined the operators $d$ and $\delta$, we are now positioned to introduce the central object of our study.

#### Definition and Basic Properties

The **Hodge Laplacian** (or Laplace-de Rham operator) is the second-order differential operator $\Delta: \Omega^k(M) \to \Omega^k(M)$ defined as:
$$
\Delta = d\delta + \delta d
$$
This operator should be thought of as a natural generalization of the classical Laplacian on functions. For a function $f \in \Omega^0(M)$, we have $\delta f = 0$, so $\Delta f = d\delta f + \delta d f = \delta(df)$. Using the interpretation $\delta\alpha = -\text{div}(\alpha^\sharp)$, we find $\Delta f = -\text{div}((\text{grad} f)^\sharp)$, which is the standard definition of the Laplace-Beltrami operator on functions.

The Hodge Laplacian can also be seen as the square of the **de Rham operator** $D = d + \delta$. This operator maps the space of all forms $\Omega^\bullet(M)$ to itself. Its square is $D^2 = (d+\delta)(d+\delta) = d^2 + d\delta + \delta d + \delta^2$. Since $d^2=0$ and $\delta^2=0$, this simplifies to $\Delta = D^2$ [@problem_id:2998573].

A key algebraic property is that the Laplacian commutes with both the exterior derivative and the [codifferential](@entry_id:197182). The proof is a straightforward consequence of [nilpotency](@entry_id:147926):
$$
d\Delta = d(d\delta + \delta d) = d^2\delta + d\delta d = d\delta d
$$
$$
\Delta d = (d\delta + \delta d)d = d\delta d + \delta d^2 = d\delta d
$$
Thus, $d\Delta = \Delta d$. A similar calculation shows $\delta\Delta = \Delta\delta$ [@problem_id:2998558]. This means that if $\alpha$ is an eigenform of the Laplacian, then so are $d\alpha$ and $\delta\alpha$.

It is important to distinguish the Laplacian, which is the sum $d\delta + \delta d$ (sometimes called the [anti-commutator](@entry_id:139754)), from the graded commutator $[d,\delta] = d\delta - (-1)^{(1)(-1)}\delta d = d\delta+\delta d$. In this case, the Hodge Laplacian *is* the graded commutator of $d$ and $\delta$ [@problem_id:2998573].

#### Self-Adjointness and Positivity

Two analytic properties of the Hodge Laplacian are paramount, especially on closed (compact and without boundary) Riemannian manifolds. The operator $\Delta$ is **formally self-adjoint** with respect to the $L^2$ inner product, meaning $\langle \Delta\alpha, \beta \rangle_{L^2} = \langle \alpha, \Delta\beta \rangle_{L^2}$. This follows directly from the fact that $d$ and $\delta$ are adjoints of each other:
$$
\langle \Delta\alpha, \beta \rangle = \langle d\delta\alpha, \beta \rangle + \langle \delta d\alpha, \beta \rangle = \langle \delta\alpha, \delta\beta \rangle + \langle d\alpha, d\beta \rangle
$$
The final expression is symmetric in $\alpha$ and $\beta$, proving self-adjointness [@problem_id:2998573].

Moreover, this calculation immediately reveals that $\Delta$ is a **non-negative operator**. By setting $\beta = \alpha$ in the identity above, we obtain a fundamental formula often called the Hodge-de Rham identity:
$$
\langle \Delta\alpha, \alpha \rangle_{L^2} = \langle \delta\alpha, \delta\alpha \rangle_{L^2} + \langle d\alpha, d\alpha \rangle_{L^2} = \| \delta\alpha \|_{L^2}^2 + \| d\alpha \|_{L^2}^2 \ge 0
$$
This identity is the analytic heart of Hodge theory. It shows that the "energy" of a form under the Laplacian, $\langle \Delta\alpha, \alpha \rangle$, is the sum of the squared lengths of its derivative and its coderivative [@problem_id:2998558] [@problem_id:2998573].

#### The Laplacian as an Elliptic Operator

The Hodge Laplacian is a prime example of an **[elliptic operator](@entry_id:191407)**. In the theory of partial differential equations, [ellipticity](@entry_id:199972) is a condition on the highest-order terms of an operator that guarantees strong regularity properties for its solutions. This condition is formulated in terms of the operator's **[principal symbol](@entry_id:190703)**.

For a second-order operator like $\Delta$, the [principal symbol](@entry_id:190703) $\sigma_2(\Delta)$ at a point $(x, \xi)$ in [the cotangent bundle](@entry_id:185138) is an endomorphism of the fibre $\Lambda^k T_x^*M$. A detailed calculation shows that the [principal symbol](@entry_id:190703) of the Hodge Laplacian is remarkably simple:
$$
\sigma_2(\Delta)(x, \xi) = |\xi|_g^2 \, \mathrm{Id}
$$
where $|\xi|_g$ is the norm of the [covector](@entry_id:150263) $\xi$ and $\mathrm{Id}$ is the identity map on $\Lambda^k T_x^*M$. An operator is called **strongly elliptic** if its [principal symbol](@entry_id:190703) is positive definite in a specific sense. For the Hodge Laplacian, we check the condition by taking the inner product: for any non-zero form $\eta$ in the fibre,
$$
\langle \sigma_2(\Delta)(x,\xi)\eta, \eta \rangle = \langle (|\xi|_g^2 \, \mathrm{Id}) \eta, \eta \rangle = |\xi|_g^2 \langle \eta, \eta \rangle = |\xi|_g^2 |\eta|^2
$$
This satisfies the [strong ellipticity](@entry_id:755529) condition $\langle \sigma_2(\Delta)(x,\xi)\eta, \eta \rangle \ge c |\xi|_g^2 |\eta|^2$ with the optimal constant $c=1$ [@problem_id:3035682].

The consequence of ellipticity is profound. One key result is **[elliptic regularity](@entry_id:177548)**: if $\Delta\alpha = \beta$ and the form $\beta$ is smooth, then the form $\alpha$ must also be smooth. In particular, any distributional solution to $\Delta\alpha=0$ is automatically a smooth form. Another consequence, crucial for Hodge theory on compact manifolds, is that the kernel of an [elliptic operator](@entry_id:191407) is finite-dimensional.

### The Bridge to Geometry and Topology

We now arrive at the central purpose of the Hodge Laplacian: to serve as a bridge connecting the analytic properties of [differential forms](@entry_id:146747) to the geometric and [topological properties](@entry_id:154666) of the manifold.

#### Harmonic Forms

A [differential form](@entry_id:174025) $\alpha$ is defined to be **harmonic** if it is in the kernel of the Hodge Laplacian, i.e., $\Delta\alpha = 0$. On a closed manifold, the non-negativity of $\Delta$ provides a powerful characterization of [harmonic forms](@entry_id:193378). From the identity $\langle \Delta\alpha, \alpha \rangle_{L^2} = \|d\alpha\|_{L^2}^2 + \|\delta\alpha\|_{L^2}^2$, we see that $\Delta\alpha = 0$ if and only if $\langle \Delta\alpha, \alpha \rangle = 0$. This, in turn, is true if and only if both terms on the right-hand side are zero. Therefore:

A $k$-form $\alpha$ on a closed Riemannian manifold is harmonic if and only if it is both closed ($d\alpha=0$) and co-closed ($\delta\alpha=0$). [@problem_id:2998558] [@problem_id:3035686]

This is a pivotal result. It transforms the problem of solving a second-order partial differential equation ($\Delta\alpha = 0$) into the equivalent problem of solving a pair of first-order equations ($d\alpha=0$ and $\delta\alpha=0$).

#### The Hodge Decomposition Theorem

The existence of harmonic forms, guaranteed by the theory of [elliptic operators](@entry_id:181616) on compact manifolds, leads to the celebrated **Hodge decomposition theorem**. This theorem states that on a compact, oriented Riemannian manifold, the space of smooth $k$-forms $\Omega^k(M)$ admits a unique [orthogonal decomposition](@entry_id:148020):
$$
\Omega^k(M) = \mathcal{H}^k(M) \oplus \mathrm{im}(d_{k-1}) \oplus \mathrm{im}(\delta_{k+1})
$$
where $\mathcal{H}^k(M)$ is the finite-dimensional space of harmonic $k$-forms, $\mathrm{im}(d)$ is the space of [exact forms](@entry_id:269145), and $\mathrm{im}(\delta)$ is the space of co-[exact forms](@entry_id:269145).

This decomposition has a monumental consequence for topology. The de Rham cohomology group $H^k_{dR}(M)$ is defined as the [quotient space](@entry_id:148218) $\ker(d_k) / \mathrm{im}(d_{k-1})$. The Hodge theorem establishes a [canonical isomorphism](@entry_id:202335) between this purely topological object and the analytically defined space of harmonic forms:
$$
H^k_{dR}(M) \cong \mathcal{H}^k(M)
$$
This isomorphism implies that every de Rham cohomology class contains exactly one harmonic representative. Furthermore, this harmonic representative is the unique element in its [cohomology class](@entry_id:263961) that has the minimum $L^2$ norm. This is because any other form $\omega$ in the same class can be written as $\omega = \alpha + d\eta$, where $\alpha$ is harmonic. The orthogonality of the Hodge decomposition implies $\|\omega\|^2 = \|\alpha\|^2 + \|d\eta\|^2 \ge \|\alpha\|^2$ [@problem_id:3035686].

#### The Weitzenböck Formula: Curvature Meets Analysis

The metric dependence of the Laplacian hints at a deep connection to curvature. This connection is made explicit by the **Weitzenböck formulas**. For a $1$-form $\alpha$, the most fundamental of these identities reads:
$$
(\Delta \alpha)_i = -\sum_{j,k} g^{jk}(\nabla_j \nabla_k \alpha_i) + \sum_j \mathrm{Ric}_{ij} \alpha^j
$$
In this formula, $\nabla$ is the Levi-Civita connection and $\mathrm{Ric}$ is the Ricci curvature tensor. The term $-\nabla^*\nabla \alpha = -\sum g^{jk}\nabla_j\nabla_k\alpha_i$ is known as the **connection Laplacian** or Bochner Laplacian. The formula states that the Hodge Laplacian differs from the connection Laplacian by a zero-order term determined entirely by the manifold's curvature.

This formula can be derived by expanding the definition $\Delta=d\delta+\delta d$ in local [normal coordinates](@entry_id:143194) at a point $p$. The calculation involves commuting covariant derivatives, which is precisely where the Riemann [curvature tensor](@entry_id:181383) appears via the Ricci identity, eventually simplifying to the Ricci tensor term [@problem_id:2998568]. The Weitzenböck formula is a powerful tool. For example, if a manifold has positive Ricci curvature ($\mathrm{Ric}(\alpha^\sharp, \alpha^\sharp) > 0$), then for any harmonic $1$-form $\alpha$, we can integrate the formula to find $0 = \int_M \langle \Delta\alpha, \alpha \rangle = \int_M (|\nabla\alpha|^2 + \mathrm{Ric}(\alpha^\sharp, \alpha^\sharp)) d\mathrm{vol}_g$. Since both terms in the integrand are non-negative, they must both be zero. $\mathrm{Ric}(\alpha^\sharp, \alpha^\sharp)=0$ implies $\alpha=0$. Thus, a [compact manifold](@entry_id:158804) with positive Ricci curvature has no non-trivial harmonic $1$-forms, which implies its first Betti number $b_1(M)$ is zero. This is a classic example of how geometric conditions constrain topology via the Hodge Laplacian.

#### The Metric Dependence of $\Delta$

It is crucial to remember that while cohomology is a topological invariant, the Hodge Laplacian and its [harmonic forms](@entry_id:193378) are not. They depend fundamentally on the choice of Riemannian metric. Consider a [conformal change of metric](@entry_id:195227) $\tilde{g} = e^{2f}g$ for some [smooth function](@entry_id:158037) $f$. One can explicitly calculate the transformation laws for the operators involved [@problem_id:3035694]:
- The Hodge star transforms as: $\tilde{\star}\omega = e^{(n-2k)f} \star\omega$ for a $k$-form $\omega$.
- The [codifferential](@entry_id:197182) transforms in a more complex way involving derivatives of $f$: $\tilde{\delta}\beta = e^{-2f}\delta\beta - (n-2k-2) e^{-2f} i_{\text{grad }f} \beta$ for a $(k+1)$-form $\beta$.
- Consequently, the Hodge Laplacian $\tilde{\Delta}$ does not simply scale with $\Delta$, but acquires additional lower-order terms involving derivatives of $f$.

This illustrates that changing the metric changes the notion of what it means to be harmonic. However, the dimension of the space of harmonic forms, being equal to the Betti number, remains invariant.

### Extensions of the Theory

The classical Hodge theory on compact, closed manifolds can be extended to more general settings, which requires careful handling of the analytic foundations.

#### Manifolds with Boundary

If a [compact manifold](@entry_id:158804) $M$ has a smooth boundary $\partial M$, the Hodge Laplacian $\Delta$ is no longer automatically self-adjoint on the space of all smooth forms. To obtain a self-adjoint operator, one must restrict its domain by imposing boundary conditions. The requirement for self-adjointness, derived from Green's identity, leads to two canonical choices of boundary conditions [@problem_id:2998566]:

1.  **Absolute Boundary Conditions:** These conditions require the "normal parts" of the form and its [exterior derivative](@entry_id:161900) to vanish at the boundary. For a form $\omega \in \Omega^k(M)$, let $n(\omega) = i^*(\iota_\nu \omega)$ be its normal component, where $\iota_\nu$ is interior multiplication by the outward normal vector $\nu$. The conditions are:
    $$
    n(\omega) = 0 \quad \text{and} \quad n(d\omega) = 0 \quad \text{on } \partial M
    $$

2.  **Relative Boundary Conditions:** These conditions require the "tangential parts" of the form and its [codifferential](@entry_id:197182) to vanish at the boundary. For a form $\omega$, let $t(\omega) = i^*\omega$ be its tangential component. The conditions are:
    $$
    t(\omega) = 0 \quad \text{and} \quad t(\delta\omega) = 0 \quad \text{on } \partial M
    $$

Each of these choices defines a distinct [self-adjoint extension](@entry_id:151493) of the Laplacian, leading to different spaces of [harmonic forms](@entry_id:193378) and corresponding absolute and [relative cohomology](@entry_id:272456) groups.

#### Non-Compact Manifolds and $L^2$ Cohomology

On [non-compact manifolds](@entry_id:262738), the theory becomes even more subtle. One works with the Hilbert space of square-integrable forms, $L^2\Omega^k(M)$. A key technical point is the self-adjointness of the operators. While $\Delta$ on compactly supported smooth forms is symmetric, it is not guaranteed to have a unique [self-adjoint extension](@entry_id:151493).

A fundamental result states that if the manifold $(M,g)$ is **complete**, then the Hodge Laplacian is **essentially self-adjoint**. This means it has a unique [self-adjoint extension](@entry_id:151493), making the space of $L^2$ harmonic forms, $\mathcal{H}^k_{(2)}(M) = \ker \Delta$, unambiguously defined [@problem_id:2998570]. On a complete manifold, the space of $L^2$ [harmonic forms](@entry_id:193378) can again be characterized as the intersection of the kernels of the (appropriately defined) $L^2$ operators $d$ and $\delta$. Furthermore, [elliptic regularity](@entry_id:177548) still holds: any $L^2$ form $\omega$ satisfying $\Delta\omega = 0$ in a distributional sense is in fact a smooth form satisfying the equation classically [@problem_id:2998570].

The Hodge decomposition theorem also has an analogue in this setting. For a complete manifold, one has an [orthogonal decomposition](@entry_id:148020) of the Hilbert space:
$$
L^2\Omega^k(M) = \mathcal{H}^k_{(2)}(M) \oplus \overline{\mathrm{im}(d)} \oplus \overline{\mathrm{im}(\delta)}
$$
where the bar denotes the closure in the $L^2$ norm. This decomposition establishes an isomorphism between the space of $L^2$ harmonic forms and the **reduced $L^2$ cohomology group** $H^k_{(2),\text{red}}(M) = \ker d / \overline{\mathrm{im} d}$ [@problem_id:3035687]. If the range of $d$ is also a [closed subspace](@entry_id:267213), then the reduced and unreduced cohomology groups coincide, and the classical-style Hodge decomposition holds without [closures](@entry_id:747387). However, unlike the compact case, the space of $L^2$ [harmonic forms](@entry_id:193378) $\mathcal{H}^k_{(2)}(M)$ can be infinite-dimensional, even for manifolds with [bounded geometry](@entry_id:189959) such as hyperbolic space [@problem_id:3035687].