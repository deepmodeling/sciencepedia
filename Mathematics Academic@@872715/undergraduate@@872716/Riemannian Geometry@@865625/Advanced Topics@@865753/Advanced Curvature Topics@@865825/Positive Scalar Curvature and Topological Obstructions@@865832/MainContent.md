## Introduction
In the field of Riemannian geometry, [scalar curvature](@entry_id:157547) stands as a fundamental, albeit coarse, measure of a manifold's intrinsic geometry. The seemingly simple question—which manifolds can be endowed with a metric of positive scalar curvature (PSC)?—unveils a remarkably deep and intricate relationship between the local geometry of a space and its global topology. This question has driven decades of research, revealing that while some manifolds readily admit such metrics, others are fundamentally obstructed by their topological structure. This article addresses this central problem by systematically exploring both the obstructions to and constructions of PSC metrics.

Across the following chapters, you will gain a comprehensive understanding of this fascinating subject. The journey begins in **"Principles and Mechanisms"**, where we will define [scalar curvature](@entry_id:157547) within the hierarchy of curvature concepts and explore the two most profound [topological obstructions](@entry_id:634492): one arising from the study of [minimal hypersurfaces](@entry_id:188002), pioneered by Schoen and Yau, and the other from the [index theory](@entry_id:270237) of the Dirac operator on [spin manifolds](@entry_id:200931). Next, **"Applications and Interdisciplinary Connections"** will showcase the power of these ideas, demonstrating how constructive methods like surgery create vast families of PSC manifolds and how the PSC condition forges deep links with [geometric analysis](@entry_id:157700), [low-dimensional topology](@entry_id:145498), and [noncommutative geometry](@entry_id:158436). Finally, **"Hands-On Practices"** will provide concrete exercises to calculate curvature on fundamental examples like spheres and tori, solidifying the theoretical concepts discussed.

## Principles and Mechanisms

This chapter delves into the fundamental principles governing scalar curvature and the mechanisms through which it interacts with the underlying topology of a manifold. We will begin by situating [scalar curvature](@entry_id:157547) within the hierarchy of Riemannian curvature concepts, proceed to explore its surprisingly flexible nature, and then dedicate the majority of our analysis to the profound [topological obstructions](@entry_id:634492) that limit its sign. Finally, we will examine powerful constructive methods that affirm the prevalence of positive scalar curvature in the absence of such obstructions.

### The Hierarchy of Curvature

In Riemannian geometry, curvature is a multi-layered concept. The most detailed information is contained in the Riemann [curvature tensor](@entry_id:181383), which captures the [non-commutativity](@entry_id:153545) of covariant derivatives. From this tensor, we derive progressively coarser, yet often more globally significant, [geometric invariants](@entry_id:178611).

The **sectional curvature**, $K(\sigma)$, is a function on the set of all $2$-dimensional planes $\sigma$ in each [tangent space](@entry_id:141028) $T_pM$. It describes the curvature of the manifold restricted to that specific plane and is the geometric notion closest to the classical Gaussian curvature of surfaces.

By averaging sectional curvatures at a point, we arrive at **Ricci curvature**. For a given [unit vector](@entry_id:150575) $v \in T_pM$, the Ricci curvature $\operatorname{Ric}(v,v)$ is the sum of the sectional curvatures of all planes containing $v$. More formally, if $\{e_1, \dots, e_{n-1}, v\}$ is an orthonormal basis for $T_pM$, then
$$
\operatorname{Ric}(v,v) = \sum_{i=1}^{n-1} K(\mathrm{span}\{v, e_i\})
$$
The Ricci tensor, $\operatorname{Ric}$, is a [symmetric bilinear form](@entry_id:148281) that captures this averaged curvature information for every direction. [@problem_id:3062031]

The final step in this averaging process yields the **scalar curvature**, $R$. At each point $p \in M$, the scalar curvature $R(p)$ is a single real number obtained by taking the trace of the Ricci tensor with respect to the metric $g$. For any orthonormal basis $\{e_j\}_{j=1}^n$ of $T_pM$, the scalar curvature is given by:
$$
R(p) = \sum_{j=1}^n \operatorname{Ric}(e_j, e_j) = \operatorname{tr}_g(\operatorname{Ric}_p)
$$
This represents a total average of the curvature at the point $p$. Combining the definitions, we see that [scalar curvature](@entry_id:157547) is the sum of the sectional curvatures of planes spanned by all distinct pairs of vectors in an [orthonormal basis](@entry_id:147779):
$$
R(p) = \sum_{i \neq j} K(\mathrm{span}\{e_i, e_j\}) = 2\sum_{1 \le i  j \le n} K(\mathrm{span}\{e_i,e_j\})
$$
This final expression makes the averaging nature of [scalar curvature](@entry_id:157547) explicit. [@problem_id:3062049]

This hierarchy leads to a natural set of implications for positivity. If a manifold has strictly [positive sectional curvature](@entry_id:193532), $K0$, then every term in the sum for $\operatorname{Ric}(v,v)$ is positive, implying positive Ricci curvature, $\operatorname{Ric}0$. Similarly, if $\operatorname{Ric}0$, it is a positive-definite bilinear form, and its trace, the scalar curvature $R$, must be positive. Thus, for any dimension $n \ge 2$, we have the strict implications:
$$
K  0 \implies \operatorname{Ric}  0 \implies R  0
$$
It is a crucial fact of Riemannian geometry that, for dimensions $n \ge 3$, none of these implications can be reversed. [@problem_id:3062033]

For instance, the product manifold $S^2 \times S^2$ endowed with the product of standard round metrics has $\operatorname{Ric}0$. However, any $2$-plane spanned by a vector tangent to the first $S^2$ and a vector tangent to the second $S^2$ has zero sectional curvature. Therefore, it does not have $K0$. [@problem_id:3062033]

More subtly, [positive scalar curvature](@entry_id:203664) does not imply positive Ricci curvature. The [scalar curvature](@entry_id:157547) being positive only means the trace of the Ricci tensor is positive; this does not preclude the tensor from having negative eigenvalues. A powerful illustration is the product manifold $M = S^2 \times H^2$, where $S^2$ is the sphere and $H^2$ is the hyperbolic plane. Let's equip $S^2$ with a metric of constant Gaussian curvature $+C_1$ and $H^2$ with a metric of constant Gaussian curvature $-C_2$, where $C_1, C_2  0$. The [scalar curvature](@entry_id:157547) of the product is the sum of the scalar curvatures of the factors, $R_M = R_{S^2} + R_{H^2} = 2C_1 - 2C_2$. By choosing $C_1  C_2$ (e.g., $C_1=2, C_2=1$), we can ensure $R_M  0$ everywhere. However, planes tangent to the $H^2$ factor have negative sectional curvature, and directions tangent to $H^2$ will have negative Ricci curvature contributions. This explicitly demonstrates a manifold with $R0$ that possesses directions of negative Ricci and sectional curvature. [@problem_id:3062049]

### The Malleability of Scalar Curvature

Before investigating obstructions, it is essential to understand that the sign of [scalar curvature](@entry_id:157547) is not a topological invariant. The existence of a metric with [positive scalar curvature](@entry_id:203664) (PSC) is a property of the [smooth structure](@entry_id:159394) of a manifold, but a single manifold can often admit metrics with vastly different scalar curvature signatures.

A fundamental tool for understanding this is the behavior of curvature under a constant conformal scaling of the metric. Let $(M,g)$ be a Riemannian manifold, and consider a new metric $g' = c^2 g$ for some constant $c0$. A direct calculation shows that the Christoffel symbols, and consequently the type $(1,3)$ Riemann and Ricci tensors, are invariant under this scaling: $\Gamma' = \Gamma$, $R'^{\ell}{}_{ijk} = R^{\ell}{}_{ijk}$, and $\mathrm{Ric}'_{ij} = \mathrm{Ric}_{ij}$. However, the scalar curvature is computed by tracing with the *inverse* metric, which scales as $g'^{ij} = c^{-2}g^{ij}$. This leads to the transformation law:
$$
R' = g'^{ij}\mathrm{Ric}'_{ij} = (c^{-2}g^{ij})(\mathrm{Ric}_{ij}) = c^{-2} R_g
$$
Thus, constant scaling preserves the sign of the scalar curvature. This simple fact implies that any [topological obstruction](@entry_id:201389) to PSC cannot be circumvented by merely scaling the metric. [@problem_id:3062010]

A more dramatic demonstration of malleability involves non-constant scaling or the use of [product manifolds](@entry_id:270208). Consider the manifold $M = S^2 \times \Sigma_g$, where $\Sigma_g$ is a closed [orientable surface](@entry_id:274245) of genus $g \ge 2$. Let $g_{S^2}$ be the standard round metric on $S^2$ (with [scalar curvature](@entry_id:157547) $R_{S^2}=2$) and $h_{\Sigma}$ be a hyperbolic metric on $\Sigma_g$ (with $R_{h_{\Sigma}}=-2$). We can construct a family of [product metrics](@entry_id:160866) $\hat{g}_t = g_{S^2} \oplus t h_{\Sigma}$ for $t0$. The [scalar curvature](@entry_id:157547) of the rescaled factor $(\Sigma_g, t h_{\Sigma})$ is $R_{t h_{\Sigma}} = t^{-1} R_{h_{\Sigma}} = -2/t$. The scalar curvature of the product manifold is the sum:
$$
R_{\hat{g}_t} = R_{g_{S^2}} + R_{t h_{\Sigma}} = 2 - \frac{2}{t}
$$
By varying the parameter $t$, we can control the sign of the scalar curvature on the *same underlying manifold* $M$:
- If $t1$, then $R_{\hat{g}_t}  0$.
- If $t1$, then $R_{\hat{g}_t}  0$.
- If $t=1$, then $R_{\hat{g}_t} = 0$.

This explicitly shows that the existence of a PSC metric is a subtle global property, as the same manifold $S^2 \times \Sigma_g$ admits metrics of positive, negative, and zero [scalar curvature](@entry_id:157547). [@problem_id:3062022] This motivates the central question: what topological features can *obstruct* the existence of a PSC metric, no matter how one tries to construct it?

### The Gauss-Bonnet Obstruction in Dimension Two

The simplest and most complete story of scalar curvature obstruction occurs on two-dimensional surfaces. For a surface $(M^2, g)$, the scalar curvature $R$ is simply twice the Gaussian curvature $K$, i.e., $R=2K$. Thus, the condition $R0$ is equivalent to $K0$. [@problem_id:3062033]

The celebrated **Gauss-Bonnet Theorem** for a closed, oriented surface states that the total curvature is a [topological invariant](@entry_id:142028):
$$
\int_{M^2} K \, dA = 2\pi \chi(M^2)
$$
where $\chi(M^2)$ is the Euler characteristic of the surface. If a surface admits a metric with $K0$ everywhere, then the integral on the left must be strictly positive. This immediately implies that $\chi(M^2)  0$. According to the classification of closed, [orientable surfaces](@entry_id:271413), the only such surface is the 2-sphere $S^2$ (with $\chi(S^2)=2$).

This provides a complete classification: the only closed, [orientable surface](@entry_id:274245) admitting a metric of [positive scalar curvature](@entry_id:203664) is the sphere. For the torus $T^2$, $\chi(T^2)=0$, so any metric on it must have its [total curvature](@entry_id:157605) integrate to zero, forbidding $K0$ (or $K0$) everywhere. For surfaces of [genus](@entry_id:267185) $g \ge 2$, $\chi(\Sigma_g) = 2-2g  0$, which also forbids a PSC metric. [@problem_id:3062049] [@problem_id:3062031]

It is natural to ask if this principle generalizes. Does $R0$ on a higher-dimensional manifold $M^n$ imply that its Euler characteristic $\chi(M^n)$ is positive? The answer is no. The higher-dimensional Chern-Gauss-Bonnet theorem expresses $\chi(M^n)$ as an integral of a complex polynomial in the curvature tensor, which is not, in general, proportional to the scalar curvature. For instance, the manifold $S^1 \times S^3$ has $\chi(S^1 \times S^3) = \chi(S^1)\chi(S^3) = 0 \times 0 = 0$, yet it admits a [product metric](@entry_id:637352) with [scalar curvature](@entry_id:157547) $R=60$. Even more strikingly, the manifold $\Sigma_g \times S^2$ (for $g \ge 2$) has $\chi(\Sigma_g \times S^2) = \chi(\Sigma_g)\chi(S^2) = (2-2g)(2)  0$, but it can be given a [product metric](@entry_id:637352) with [positive scalar curvature](@entry_id:203664). Clearly, different and deeper mechanisms are required to understand obstructions in dimensions $n \ge 3$. [@problem_id:3062071]

### Obstruction via Minimal Hypersurfaces

One of the most powerful techniques for obstructing PSC in higher dimensions, pioneered by Richard Schoen and Shing-Tung Yau, involves [minimal hypersurfaces](@entry_id:188002). The core idea is that [positive scalar curvature](@entry_id:203664) in an ambient manifold exerts a destabilizing influence on [minimal hypersurfaces](@entry_id:188002) within it.

Consider a closed, embedded, [minimal hypersurface](@entry_id:196896) $\Sigma^{n-1} \subset M^n$. Minimal means its [mean curvature](@entry_id:162147) is zero. The stability of $\Sigma$ is determined by the second variation of its area. For a normal variation of $\Sigma$ with speed function $\phi \in C^\infty(\Sigma)$, the second variation is given by the integral of the Jacobi operator:
$$
\delta^{2}\operatorname{Area}(\phi) = \int_{\Sigma} \left( |\nabla_{\Sigma}\phi|^2 - (\lvert A \rvert^{2} + \operatorname{Ric}_{M}(\nu,\nu)) \phi^{2} \right) d\mu_{\Sigma}
$$
where $A$ is the second fundamental form of $\Sigma$ and $\nu$ is its unit normal. A [minimal hypersurface](@entry_id:196896) is **stable** if $\delta^{2}\operatorname{Area}(\phi) \ge 0$ for all functions $\phi$. This inequality is opposed by the "potential" term $(\lvert A \rvert^{2} + \operatorname{Ric}_{M}(\nu,\nu))$.

The crucial link to ambient scalar curvature comes from the **Gauss equation**, which relates the curvatures of $M$ and $\Sigma$. For a [minimal hypersurface](@entry_id:196896) ($H=0$), it gives:
$$
\operatorname{Ric}_{M}(\nu,\nu) = \frac{1}{2} (\mathrm{Scal}_{M} - \mathrm{Scal}_{\Sigma} + \lvert A \rvert^{2})
$$
Substituting this into the potential term reveals the direct influence of the ambient scalar curvature $\mathrm{Scal}_{M}$. The [stability inequality](@entry_id:186352) depends on an integral involving $-\mathrm{Scal}_{M} \phi^2 / 2$. This means a positive $\mathrm{Scal}_{M}$ makes the potential larger, which in turn makes the integrand more negative and stability harder to achieve. [@problem_id:3062018]

This leads to a profound obstruction mechanism:
1.  Suppose a manifold $M^n$ for topological reasons must contain a stable [minimal hypersurface](@entry_id:196896) (e.g., any incompressible hypersurface).
2.  If the assumption that $\mathrm{Scal}_M  0$ can be shown to contradict the stability of this hypersurface, then $M$ cannot admit a PSC metric.

This is precisely the argument used to prove that the $n$-torus $T^n$ for $n \ge 3$ does not admit a metric of [positive scalar curvature](@entry_id:203664). Topologically, $T^n$ contains an incompressible torus $T^{n-1}$. Schoen and Yau proved that in a manifold with $\operatorname{Ric}0$, any such hypersurface must be stable. They then refined the argument to show that if $\mathrm{Scal}_M  0$, the existence of such a stable [minimal hypersurface](@entry_id:196896) leads to a contradiction. [@problem_id:3062033]

### Obstruction via Index Theory

A second, completely different mechanism for obstructing PSC comes from the analysis of the Dirac operator on [spin manifolds](@entry_id:200931). This approach, initiated by André Lichnerowicz and fully realized through the Atiyah-Singer index theorem, links [scalar curvature](@entry_id:157547) to a deep topological invariant called the $\hat{A}$-[genus](@entry_id:267185).

An oriented Riemannian manifold $(M^n, g)$ is **spin** if its second Stiefel-Whitney class $w_2(M) \in H^2(M; \mathbb{Z}_2)$ vanishes. This topological condition allows for the construction of a [spinor bundle](@entry_id:635590) $S \to M$. On sections of this bundle (spinors), one can define a canonical first-order differential operator called the **Dirac operator**, $D$. Locally, for an [orthonormal frame](@entry_id:189702) $\{e_i\}$, it is given by $D\psi = \sum_i e_i \cdot \nabla^S_{e_i} \psi$, where $\cdot$ denotes Clifford multiplication and $\nabla^S$ is the covariant derivative induced by the Levi-Civita connection. [@problem_id:3062052]

The key to the obstruction is the **Weitzenböck-Lichnerowicz formula**, which relates the square of the Dirac operator to the connection Laplacian $\nabla^{S*}\nabla^S$ and the scalar curvature $R$:
$$
D^2 = \nabla^{S*}\nabla^S + \frac{1}{4}R
$$
Now, suppose $M$ is a closed [spin manifold](@entry_id:159034) with a PSC metric, so $R  0$ everywhere. Let $\psi$ be a **harmonic [spinor](@entry_id:154461)**, meaning $D\psi=0$. This implies $D^2\psi=0$. Taking the $L^2$ inner product with $\psi$ and integrating over $M$ gives:
$$
0 = \int_M \langle D^2\psi, \psi \rangle \, dV = \int_M \left( |\nabla^S\psi|^2 + \frac{1}{4}R|\psi|^2 \right) dV
$$
Since $R  0$, both terms in the integrand are non-negative. For their sum to be zero, both must vanish everywhere. The term $\frac{1}{4}R|\psi|^2 = 0$ implies $|\psi|^2=0$, so $\psi=0$. This is a powerful "[vanishing theorem](@entry_id:636963)": a closed [spin manifold](@entry_id:159034) with a metric of [positive scalar curvature](@entry_id:203664) has no non-zero harmonic [spinors](@entry_id:158054). Its kernel, $\ker D$, is trivial. [@problem_id:3062024]

The final step is to invoke the **Atiyah-Singer Index Theorem**. For a closed, even-dimensional [spin manifold](@entry_id:159034), the theorem equates the analytical index of the Dirac operator to the topological $\hat{A}$-[genus](@entry_id:267185): $\mathrm{index}(D^+) = \hat{A}(M)$. Since a PSC metric implies $\ker D = \{0\}$, it follows that $\mathrm{index}(D^+) = 0$. This yields the celebrated obstruction:
*If a closed, even-dimensional [spin manifold](@entry_id:159034) $M$ admits a metric of [positive scalar curvature](@entry_id:203664), its $\hat{A}$-genus must be zero.*

Therefore, if a [spin manifold](@entry_id:159034) has $\hat{A}(M) \neq 0$, it is topologically obstructed from admitting any PSC metric. The spin condition is essential here. The manifold $\mathbb{C}P^2$, for example, is not spin ($w_2(\mathbb{C}P^2) \neq 0$) and its topologically computed $\hat{A}$-genus is $-\frac{1}{8}$. However, this non-vanishing does not form an obstruction, because the Dirac operator is not defined and the [index theory](@entry_id:270237) argument does not apply. Indeed, $\mathbb{C}P^2$ is known to admit a PSC metric (the Fubini-Study metric). [@problem_id:3062050]

### Construction via Surgery

The study of [positive scalar curvature](@entry_id:203664) is not solely a story of obstructions. There are also powerful constructive methods that show PSC is, in a sense, a common property for manifolds that are not topologically obstructed. The most important of these is the surgery theorem of Mikhail Gromov and H. Blaine Lawson.

**Surgery** is a fundamental operation in topology for constructing new manifolds from old ones. To perform surgery on a manifold $M^n$ along an embedded $k$-sphere $S^k$, one removes a tubular neighborhood of the sphere (diffeomorphic to $S^k \times D^{n-k}$) and glues in a different piece ($D^{k+1} \times S^{n-k-1}$) along their common boundary.

The Gromov-Lawson surgery theorem states that this process is compatible with positive scalar curvature, provided the surgery is performed in high enough codimension.
*If $M^n$ ($n \ge 3$) is a closed manifold admitting a metric of [positive scalar curvature](@entry_id:203664), and if $M'$ is obtained from $M$ by a surgery along an embedded sphere $S^k$ of [codimension](@entry_id:273141) $n-k \ge 3$, then $M'$ also admits a metric of [positive scalar curvature](@entry_id:203664).* [@problem_id:3062043]

This theorem is immensely powerful. It allows one to start with simple manifolds known to have PSC (like the sphere $S^n$) and perform a sequence of surgeries to generate vast classes of topologically [complex manifolds](@entry_id:159076) that also must admit PSC. This shifts the perspective on the problem: rather than asking which manifolds have PSC, we are led to ask what are the fundamental obstructions that prevent a manifold from being constructed in this way. This theorem, together with the obstructions from [minimal surfaces](@entry_id:157732) and [index theory](@entry_id:270237), forms the backbone of our modern understanding of the relationship between [curvature and topology](@entry_id:264903).