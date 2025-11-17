## Introduction
Manifolds with [positive scalar curvature](@entry_id:203664) (PSC) are a central object of study in modern [differential geometry](@entry_id:145818), representing a broad and geometrically rich class of spaces that sit at the intersection of analysis, topology, and even mathematical physics. A fundamental question driving the field is to determine precisely which manifolds admit a metric of positive scalar curvature. This inquiry naturally splits into two complementary pursuits: developing methods to construct such metrics on diverse topological spaces, and discovering profound [topological obstructions](@entry_id:634492) that prevent their existence. This article provides a comprehensive overview of this deep and active area of research.

This exploration will begin by establishing the foundational **Principles and Mechanisms** that govern PSC geometry. We will move from the basic definitions of curvature and their hierarchy to the sophisticated tools of [conformal geometry](@entry_id:186351), including the celebrated Yamabe problem. We will then examine the powerful constructive surgery techniques pioneered by Gromov and Lawson, and contrast them with the deep obstructions to PSC that arise from the [index theory](@entry_id:270237) of the Dirac operator and the analysis of [minimal surfaces](@entry_id:157732). Following this, the chapter on **Applications and Interdisciplinary Connections** will showcase how these principles are applied to achieve major classification theorems for manifolds, revealing surprising connections to general relativity, operator algebras, and the study of [exotic smooth structures](@entry_id:160763). Finally, a series of **Hands-On Practices** will provide an opportunity to engage directly with the core computational and theoretical techniques, reinforcing the concepts discussed and bridging the gap between theory and application.

## Principles and Mechanisms

This chapter delves into the core principles and mechanisms that govern the study of manifolds with positive scalar curvature (PSC). We transition from the foundational definitions of curvature to the sophisticated analytical and topological tools used to construct PSC metrics and to identify obstructions to their existence. The narrative will weave through three central themes: the [conformal geometry](@entry_id:186351) of the Yamabe problem, the geometric engineering of PSC metrics via surgery, and the profound obstructions arising from [index theory](@entry_id:270237) and minimal surfaces.

### From Sectional to Scalar Curvature: A Hierarchy of Positivity

The notion of curvature on a Riemannian manifold $(M^n, g)$ is fundamentally local, captured by the Riemann [curvature tensor](@entry_id:181383) $R$. While this tensor contains complete information about the second-order geometry of the metric, its complexity makes it difficult to work with directly. Geometric analysis often relies on more tractable, averaged quantities derived from it.

The most intuitive of these is the **sectional curvature**, $K_g(\sigma)$, which describes the curvature of the manifold restricted to a two-dimensional plane $\sigma$ in the tangent space $T_pM$. For an orthonormal basis $\{X, Y\}$ of $\sigma$, it is given by $K_g(\sigma) = \langle R(X,Y)Y, X \rangle_g$. A manifold with [positive sectional curvature](@entry_id:193532) is, in a very strong sense, positively curved at every point and in every direction.

Averaging the sectional curvatures at a point yields the **Ricci curvature tensor**, $\mathrm{Ric}_g$. For a [unit tangent vector](@entry_id:262985) $v \in T_pM$, the Ricci curvature $\mathrm{Ric}_g(v,v)$ is the sum of the sectional curvatures of all planes containing $v$. Specifically, if $\{e_1, \dots, e_n\}$ is an orthonormal basis of $T_pM$ with $e_1 = v$, then:
$$
\mathrm{Ric}_g(v,v) = \sum_{j=2}^n K_g(\operatorname{span}\{e_1, e_j\})
$$
From this expression, it is immediately clear that if a manifold has strictly [positive sectional curvature](@entry_id:193532), its Ricci curvature must also be strictly positive definite.

Finally, the most coarse measure of curvature at a point is the **scalar curvature**, $R_g$, obtained by taking the trace of the Ricci tensor with respect to the metric. In any [orthonormal basis](@entry_id:147779) $\{e_i\}$ of $T_pM$, the [scalar curvature](@entry_id:157547) is the sum of the diagonal components of the Ricci tensor:
$$
R_g(p) = \mathrm{tr}_g(\mathrm{Ric}_g) = \sum_{i=1}^n \mathrm{Ric}_g(e_i, e_i)
$$
Substituting the expression for Ricci curvature in terms of sectional curvatures, we find a direct relationship between scalar and sectional curvatures [@problem_id:3032082]:
$$
R_g(p) = \sum_{i=1}^n \sum_{j \neq i} K_g(\operatorname{span}\{e_i, e_j\}) = 2 \sum_{1 \le i  j \le n} K_g(\operatorname{span}\{e_i, e_j\})
$$
This formula reveals that the scalar curvature is, up to a factor of 2, the sum of all sectional curvatures of planes spanned by pairs of basis vectors in an [orthonormal frame](@entry_id:189702). It immediately follows that if all sectional curvatures are positive, the [scalar curvature](@entry_id:157547) must also be positive.

We thus have a clear hierarchy of curvature conditions:
$$
\text{Positive Sectional Curvature} \implies \text{Positive Ricci Curvature} \implies \text{Positive Scalar Curvature}
$$
However, the reverse implications are false. Scalar curvature is a significantly weaker condition than Ricci or sectional curvature. A classic and illustrative [counterexample](@entry_id:148660) is the product manifold $M = S^2 \times S^2$ equipped with the product of the standard round metrics of [constant sectional curvature](@entry_id:272200) $1$. The scalar curvature of a product manifold is the sum of the scalar curvatures of its factors. Since the [scalar curvature](@entry_id:157547) of the standard $S^2$ is $2$, the scalar curvature of $S^2 \times S^2$ is constant and equal to $2+2=4$, which is strictly positive. However, consider a [tangent plane](@entry_id:136914) $\sigma \subset T_{(x,y)}(S^2 \times S^2)$ spanned by a "mixed" pair of vectors—one tangent to the first $S^2$ factor and one tangent to the second. The sectional curvature of such a plane is zero. Therefore, $(S^2 \times S^2, g_{\text{product}})$ is a manifold with positive scalar curvature but does not have [positive sectional curvature](@entry_id:193532) everywhere [@problem_id:3032082]. This example underscores that the study of [positive scalar curvature](@entry_id:203664) is distinct from, and more general than, the study of manifolds with stronger [curvature bounds](@entry_id:200421).

### The Conformal Viewpoint and the Yamabe Problem

A powerful perspective in the study of scalar curvature arises from considering how it behaves under **conformal changes** of the metric. Two metrics $g_1$ and $g_2$ are conformally related if $g_2 = f \cdot g_1$ for some smooth positive function $f$ on $M$. This defines an equivalence relation, and the set of all metrics conformal to a given metric $g$ is called its **conformal class**, denoted $[g]$.

For dimensions $n \ge 3$, it is conventional to parameterize the conformal factor as $f = u^{\frac{4}{n-2}}$ for a smooth positive function $u$. Under this change, $g_u = u^{\frac{4}{n-2}}g$, the [scalar curvature](@entry_id:157547) $R_{g_u}$ of the new metric is related to the original scalar curvature $R_g$ by a remarkable transformation law [@problem_id:3032060]:
$$
R_{g_u} = u^{-\frac{n+2}{n-2}} \left( R_g u - \frac{4(n-1)}{n-2} \Delta_g u \right)
$$
where $\Delta_g = \operatorname{div}_g(\nabla_g)$ is the Laplace-Beltrami operator. The specific structure of the term in parentheses motivates the definition of a special second-order differential operator, known as the **conformal Laplacian** or the **Yamabe operator**:
$$
L_g := -\frac{4(n-1)}{n-2}\Delta_g + R_g
$$
With this operator, the transformation law takes the elegant form $R_{g_u} = u^{-\frac{n+2}{n-2}} (L_g u)$. The importance of this particular combination of the Laplacian and the scalar curvature is revealed by its own transformation property. For any [smooth function](@entry_id:158037) $\varphi$, the operator exhibits a simple covariance law under conformal change [@problem_id:3032086]:
$$
L_{g_u}(\varphi) = u^{-\frac{n+2}{n-2}} L_g(u\varphi)
$$
This property is central to the entire conformal theory of [scalar curvature](@entry_id:157547).

This framework leads directly to one of the most celebrated problems in [geometric analysis](@entry_id:157700): the **Yamabe problem**. It asks: given a closed Riemannian manifold $(M^n, g)$, does its conformal class $[g]$ contain a metric with [constant scalar curvature](@entry_id:186408)? Using the transformation law, this is equivalent to finding a smooth positive function $u$ that solves the nonlinear PDE:
$$
L_g u = k \cdot u^{\frac{n+2}{n-2}}
$$
where $k$ is the desired [constant scalar curvature](@entry_id:186408) and the exponent $\frac{n+2}{n-2}$ is the critical Sobolev exponent. This equation is the Euler-Lagrange equation for the volume-normalized total [scalar curvature](@entry_id:157547) functional, known as the **Yamabe quotient**:
$$
Q_g(\phi) = \frac{\int_M (a_n |\nabla \phi|_g^2 + R_g \phi^2) \, d\mu_g}{(\int_M |\phi|^{\frac{2n}{n-2}} \, d\mu_g)^{\frac{n-2}{n}}}
$$
where $a_n = \frac{4(n-1)}{n-2}$. The [infimum](@entry_id:140118) of this quotient over all non-zero [smooth functions](@entry_id:138942) is a conformal invariant called the **Yamabe constant** of the class $[g]$, denoted $Y(M, [g])$. The supremum of these constants over all conformal classes on $M$ is a [topological invariant](@entry_id:142028) of the manifold, the **Yamabe invariant** $\sigma(M)$ [@problem_id:3032105].

The complete resolution of the Yamabe problem (by Yamabe, Trudinger, Aubin, and Schoen) shows that this infimum is always achieved, thus guaranteeing the existence of a [constant scalar curvature](@entry_id:186408) metric in any conformal class. Of particular interest to us is the sign of this constant. There is a direct and fundamental connection between the sign of the Yamabe constant and the existence of PSC metrics: a conformal class $[g]$ contains a metric of positive scalar curvature if and only if its Yamabe constant $Y(M, [g])$ is positive.

The reasoning is as follows [@problem_id:3032105]. If there exists a metric $\tilde{g} \in [g]$ with $R_{\tilde{g}} > 0$ everywhere, then the associated Yamabe operator $L_{\tilde{g}} = -a_n \Delta_{\tilde{g}} + R_{\tilde{g}}$ is a coercive (positive-definite) operator. By the Sobolev inequality on a compact manifold, the numerator of the Yamabe quotient (computed with $\tilde{g}$) controls the denominator, ensuring that the quotient is bounded below by a positive constant. Thus, its infimum $Y(M,[g])$ must be positive. Conversely, if $Y(M,[g]) > 0$, the solution to the Yamabe problem provides a minimizing function $u$ that yields a metric $\hat{g} = u^{\frac{4}{n-2}}g$ with [constant scalar curvature](@entry_id:186408) equal to $Y(M,[g])$, which is by assumption positive.

### Constructions of Positive Scalar Curvature Metrics

While the Yamabe problem addresses the existence of PSC metrics within a single conformal class, a distinct and equally important question is how to construct new manifolds that admit PSC metrics from existing ones. The pioneering work of Gromov and Lawson provided powerful surgical techniques for this purpose.

A cornerstone result is the **[connected sum](@entry_id:263574) theorem**, which states that if two closed manifolds $M_1^n$ and $M_2^n$ (of dimension $n \ge 3$) admit metrics of [positive scalar curvature](@entry_id:203664), then their [connected sum](@entry_id:263574) $M_1 \# M_2$ also admits a PSC metric. The proof is an explicit metric construction. The procedure involves removing small [geodesic balls](@entry_id:201133) from each manifold and gluing the resulting spherical boundaries together via a "neck" or "bridge." The main challenge is to construct a metric on this neck that has [positive scalar curvature](@entry_id:203664) and smoothly matches the metrics on either side.

A standard approach models the neck as a cylinder $S^{n-1} \times [-L, L]$ endowed with a [warped product metric](@entry_id:633914) of the form $g_{\text{neck}} = dt^2 + f(t)^2 g_{S^{n-1}}$, where $g_{S^{n-1}}$ is the standard round metric on the sphere. The "profile function" $f(t)$ must interpolate between the radii of the two spheres being glued. The [scalar curvature](@entry_id:157547) of this neck metric depends on $f$, $f'$, and $f''$. The key insight of the **Gromov-Lawson construction** is that by making the neck sufficiently long (large $L$), the derivative terms $f'$ and $f''$ can be made arbitrarily small. The [scalar curvature](@entry_id:157547) then becomes dominated by the [intrinsic curvature](@entry_id:161701) of the spherical fibers, which is positive for $n-1 \ge 2$ (i.e., $n \ge 3$). This allows for the construction of a PSC metric on the neck that can be smoothly attached to the remaining parts of the manifolds [@problem_id:3032059].

This idea was generalized to a comprehensive **surgery theorem**. An elementary surgery of [codimension](@entry_id:273141) $q=n-k$ on a manifold $M$ consists of removing a tubular neighborhood of an embedded sphere $S^k$ (diffeomorphic to $S^k \times D^{n-k}$) and gluing in a handle $D^{k+1} \times S^{n-k-1}$. The Gromov-Lawson surgery theorem states that if a closed manifold $(M^n,g)$ has a PSC metric, and $M'$ is obtained from $M$ by a surgery of [codimension](@entry_id:273141) $q \ge 3$, then $M'$ also admits a PSC metric.

The proof is again a direct construction, but it requires a more sophisticated building block than the simple warped cylinder. The crucial ingredient is the **torpedo metric**. This is a specially designed PSC metric on the $q$-dimensional disk $D^q$. It is rotationally symmetric, of the form $dr^2 + \phi(r)^2 g_{S^{q-1}}$, and is constructed such that its scalar curvature is strictly positive everywhere, yet it becomes a perfect [product metric](@entry_id:637352) (a cylinder) near its boundary. The existence of such a metric is guaranteed precisely by the condition that the dimension of the disk is $q \ge 3$. This torpedo metric is used as a model for the metric on the disk fibers of the handle being glued in, ensuring the entire new piece has positive scalar curvature and can be smoothly attached [@problem_id:3032113].

A fascinating aspect of this method is its limitation. The direct metric construction fails for surgeries of [codimension](@entry_id:273141) $q=2$. An analysis of the [scalar curvature](@entry_id:157547) formula for a doubly [warped product metric](@entry_id:633914) on the surgery neck, $g = ds^2 + a(s)^2 g_{S^p} + b(s)^2 g_{S^{q-1}}$, reveals the problem. The positive contribution to the [scalar curvature](@entry_id:157547) comes from the intrinsic curvature of the spherical fibers. When $q=2$, the fiber is the circle $S^1$, which is flat—its [scalar curvature](@entry_id:157547) is zero. The term in the scalar curvature formula that scales like $(q-1)(q-2)/b(s)^2$, which is the main source of controllable positive curvature in the $q \ge 3$ case, vanishes identically. Without this term, there is no longer a mechanism to ensure the scalar curvature remains positive while satisfying the geometric boundary conditions for the surgery [@problem_id:3032117]. Although Schoen and Yau later proved the [codimension](@entry_id:273141)-2 surgery theorem using entirely different and more difficult [minimal surface](@entry_id:267317) techniques, the failure of the direct construction highlights the subtle dependence of these geometric engineering methods on dimension.

### Obstructions to Positive Scalar Curvature

The flip side of constructing PSC metrics is proving that certain manifolds cannot admit them at all. Such results are known as obstruction theorems, and they arise from deep connections between geometry, analysis, and topology.

#### Index-Theoretic Obstructions

The most famous obstruction to positive scalar curvature comes from the [index theory](@entry_id:270237) of the Dirac operator. This line of reasoning requires the manifold to possess additional topological structure. A Riemannian manifold $(M^n, g)$ is said to be a **[spin manifold](@entry_id:159034)** if it admits a **spin structure**. This is a topological condition, equivalent (for oriented manifolds) to the vanishing of the second Stiefel-Whitney class, $w_2(M)=0$.

On a [spin manifold](@entry_id:159034), one can construct a special [vector bundle](@entry_id:157593) called the **[spinor bundle](@entry_id:635590)**, $\mathbb{S}$. Its sections are known as spinor fields or [spinors](@entry_id:158054). Associated with this bundle is a canonical first-order [differential operator](@entry_id:202628) called the **Dirac operator**, $D$, which is defined in a local [orthonormal frame](@entry_id:189702) $\{e_i\}$ by $D = \sum_{i=1}^n c(e_i)\nabla_{e_i}$, where $\nabla$ is the covariant derivative on the [spinor bundle](@entry_id:635590) (induced by the Levi-Civita connection) and $c(e_i)$ denotes Clifford multiplication by the vector $e_i$ [@problem_id:3032109].

The critical link between the Dirac operator and the geometry of the manifold is provided by the celebrated **Lichnerowicz formula** (or Lichnerowicz-Weitzenböck formula):
$$
D^2 = \nabla^*\nabla + \frac{1}{4} R_g
$$
Here, $\nabla^*\nabla$ is the connection Laplacian on the [spinor bundle](@entry_id:635590), a non-negative operator, and $R_g$ is the scalar curvature acting as a multiplication operator [@problem_id:3032109].

This formula leads to a powerful [vanishing theorem](@entry_id:636963). Suppose a closed [spin manifold](@entry_id:159034) $M$ admits a metric with strictly [positive scalar curvature](@entry_id:203664), $R_g  0$. Let $\psi$ be a harmonic spinor, meaning $D\psi = 0$. This implies $D^2\psi = 0$. Taking the $L^2$ inner product of the Lichnerowicz formula with $\psi$ and integrating over $M$ gives:
$$
\int_M \langle (\nabla^*\nabla + \frac{1}{4} R_g) \psi, \psi \rangle \, d\mu_g = \int_M |\nabla \psi|^2 \, d\mu_g + \frac{1}{4} \int_M R_g |\psi|^2 \, d\mu_g = 0
$$
Since $R_g > 0$, both terms in the sum are non-negative. Their sum can only be zero if both are zero. The second term being zero implies that $\psi$ must be identically zero. Therefore, a closed [spin manifold](@entry_id:159034) with a [positive scalar curvature](@entry_id:203664) metric has no non-zero harmonic [spinors](@entry_id:158054); its Dirac operator has a trivial kernel, $\ker(D) = \{0\}$.

The final step is to connect this analytical fact to the topology of the manifold using the **Atiyah-Singer Index Theorem**. For the Dirac operator on a [spin manifold](@entry_id:159034) of dimension $n=4k$, the theorem states that its analytical index is equal to a topological invariant of the manifold called the **$\hat{A}$-[genus](@entry_id:267185)**, $\hat{A}(M)$:
$$
\text{index}(D) = \dim(\ker D^+) - \dim(\ker D^-) = \hat{A}(M)
$$
Since $\ker(D) = \ker(D^+) \oplus \ker(D^-)$, the vanishing of $\ker(D)$ implies that both $\ker(D^+)$ and $\ker(D^-)$ are trivial. Consequently, $\text{index}(D) = 0$. This forces the [topological invariant](@entry_id:142028) $\hat{A}(M)$ to be zero. The contrapositive of this statement is the famed Lichnerowicz obstruction: if a closed [spin manifold](@entry_id:159034) $M$ (of dimension $4k$) has a non-zero $\hat{A}$-[genus](@entry_id:267185), it cannot admit any Riemannian metric of positive scalar curvature [@problem_id:3032069].

The spin assumption is absolutely essential for this argument. Without a spin structure, the [spinor bundle](@entry_id:635590) and the Dirac operator are not defined, the Lichnerowicz formula is meaningless, and the entire chain of reasoning collapses. Indeed, there exist non-[spin manifolds](@entry_id:200931) that admit PSC metrics. For example, the product manifold $M = \mathbb{R}\mathbb{P}^2 \times S^2$ is non-orientable and therefore non-spin. However, as a product of two manifolds that admit PSC metrics, it also admits a PSC metric. For this manifold, the Lichnerowicz obstruction is not applicable, and the $\hat{A}$-genus is not even defined as a characteristic number [@problem_id:3032098].

#### Minimal Hypersurface Obstructions

A second, fundamentally different class of obstructions was discovered by Schoen and Yau, using methods from [geometric measure theory](@entry_id:187987) and the analysis of [minimal surfaces](@entry_id:157732). This method relies on an inductive argument on the dimension of the manifold. The two main pillars of their approach are:

1.  **Existence and Regularity of Minimal Hypersurfaces:** For any non-trivial $(n-1)$-homology class in a closed manifold $M^n$ of dimension $n \le 7$, there exists an area-minimizing representative which is a smooth, embedded, two-sided, and stable [minimal hypersurface](@entry_id:196896).
2.  **PSC Propagation to Hypersurfaces:** A closed, two-sided, stable [minimal hypersurface](@entry_id:196896) $\Sigma^{n-1}$ embedded in a manifold $(M^n, g)$ with [positive scalar curvature](@entry_id:203664) itself admits a metric of [positive scalar curvature](@entry_id:203664).

This pair of results allows one to deduce the existence of a PSC metric on a lower-dimensional [submanifold](@entry_id:262388) if the ambient manifold has one. This can be iterated to produce a powerful obstruction, particularly for **aspherical manifolds**—those for which the [higher homotopy groups](@entry_id:159688) $\pi_k(M)$ are trivial for all $k \ge 2$.

The argument proceeds by contradiction [@problem_id:3032068]. Assume an aspherical manifold $M^n$ (with $n \le 7$) admits a PSC metric. If one can find a suitable sequence of non-[trivial homology](@entry_id:265875) classes, one can iteratively apply the Schoen-Yau results to construct a sequence of [submanifolds](@entry_id:159439) $\Sigma^{n-1}, \Sigma^{n-2}, \dots, S^2$, each admitting a PSC metric. The final object is a 2-dimensional surface $S$ which, by the Gauss-Bonnet theorem, must be a sphere since it has a PSC metric ($\chi(S)>0$). By its construction as an iterated intersection of Poincaré duals to cohomology classes, this sphere $S$ must represent a non-[trivial homology](@entry_id:265875) class in $H_2(M)$. However, since $M$ is aspherical, the Hurewicz theorem implies that any map from $S^2$ into $M$ is [null-homotopic](@entry_id:153762) and thus induces the zero map on homology. The inclusion of our constructed sphere $S$ into $M$ must therefore represent the zero homology class. This contradiction—that $[S]$ is simultaneously trivial and non-trivial—proves that the initial assumption must be false. The manifold $M$ cannot admit a metric of [positive scalar curvature](@entry_id:203664). This method, which links [scalar curvature](@entry_id:157547) to the fundamental group and topology via minimal surfaces, provides a beautiful and powerful alternative to the index-theoretic approach.