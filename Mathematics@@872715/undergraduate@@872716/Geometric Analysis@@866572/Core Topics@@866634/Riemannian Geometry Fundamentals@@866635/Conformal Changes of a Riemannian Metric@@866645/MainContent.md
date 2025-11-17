## Introduction
In the field of [differential geometry](@entry_id:145818), a conformal change of a Riemannian metric is a fundamental transformation that locally rescales notions of distance while leaving angles intact. This angle-preserving property makes [conformal geometry](@entry_id:186351) a powerful bridge between the rigidity of isometric geometry and the flexibility of topology. However, understanding the precise impact of these transformations on the geometric landscape—particularly on curvature—presents a significant challenge. This article addresses this by systematically exploring how geometric quantities respond to conformal scaling.

Across three chapters, you will gain a comprehensive understanding of this vital topic. The first chapter, "Principles and Mechanisms," establishes the foundational definitions and derives the transformation laws for essential geometric objects like volume, the Laplacian, and curvature. The second chapter, "Applications and Interdisciplinary Connections," showcases how these principles are applied to solve landmark problems such as the Uniformization Theorem and the Yamabe problem, and reveals deep connections to complex analysis, [geometric flows](@entry_id:198994), and theoretical physics. Finally, "Hands-On Practices" provides an opportunity to solidify your understanding by working through concrete calculations and conceptual problems central to the theory.

## Principles and Mechanisms

A conformal change of a Riemannian metric is one of the most fundamental transformations in [differential geometry](@entry_id:145818). It represents a rescaling of the metric at each point by a positive scalar function. While this transformation changes notions of distance, length, and volume, it preserves angles. This angle-preserving property is the hallmark of [conformal geometry](@entry_id:186351) and gives it a distinct character, bridging the gap between rigid Riemannian geometry and more flexible topological structures. This chapter explores the principles of [conformal transformations](@entry_id:159863) and the mechanisms by which they alter the geometric landscape of a manifold.

### Definition and Fundamental Properties

Let $(M, g)$ be a smooth $n$-dimensional Riemannian manifold. A new metric $\tilde{g}$ on $M$ is said to be **conformally related** to $g$ if there exists a smooth, positive function $\Omega$ on $M$ such that $\tilde{g} = \Omega^2 g$. It is common and convenient to express the conformal factor as the square of a function to simplify expressions involving lengths, or as an exponential, $\tilde{g} = e^{2u} g$, for a smooth function $u \in C^\infty(M)$. In this chapter, we will primarily use the exponential form. At each point $p \in M$, and for any pair of tangent vectors $v, w \in T_pM$, the relationship is given by:

$$
\tilde{g}_p(v, w) = e^{2u(p)} g_p(v, w)
$$

The most crucial consequence of this definition is the preservation of angles. The angle $\theta$ between two non-zero [tangent vectors](@entry_id:265494) $v$ and $w$ at a point $p$ is determined by the metric via the familiar formula from linear algebra:

$$
\cos \theta_g(v, w) = \frac{g_p(v, w)}{\|v\|_g \|w\|_g}
$$

where $\|v\|_g = \sqrt{g_p(v,v)}$ is the norm induced by the metric $g$. Under the conformal change to $\tilde{g}$, the inner product in the numerator is scaled by $e^{2u(p)}$. The new [norm of a vector](@entry_id:154882) $v$ is $\|\cdot\|_{\tilde{g}}$:

$$
\|v\|_{\tilde{g}} = \sqrt{\tilde{g}_p(v,v)} = \sqrt{e^{2u(p)} g_p(v,v)} = e^{u(p)} \sqrt{g_p(v,v)} = e^{u(p)} \|v\|_g
$$

The norm of each vector is thus scaled by $e^{u(p)}$. When we compute the cosine of the angle with respect to the new metric $\tilde{g}$, the scaling factors cancel out perfectly [@problem_id:3043434]:

$$
\cos \theta_{\tilde{g}}(v, w) = \frac{\tilde{g}_p(v, w)}{\|v\|_{\tilde{g}} \|w\|_{\tilde{g}}} = \frac{e^{2u(p)} g_p(v, w)}{(e^{u(p)} \|v\|_g)(e^{u(p)} \|w\|_g)} = \frac{e^{2u(p)} g_p(v, w)}{e^{2u(p)} \|v\|_g \|w\|_g} = \frac{g_p(v, w)}{\|v\|_g \|w\|_g} = \cos \theta_g(v, w)
$$

Since the cosine of the angle is unchanged, the angle itself is preserved. This property distinguishes [conformal maps](@entry_id:271672) from general diffeomorphisms and isometries.

The set of all metrics on $M$ that can be obtained by conformally scaling a given metric $g$ is called the **conformal class** of $g$, denoted by $[g]$.
$$
[g] = \{ e^{2u} g \mid u \in C^\infty(M) \}
$$
It is important to distinguish between conformal equivalence and isometry. An isometry is a [diffeomorphism](@entry_id:147249) $\phi: (M, g_1) \to (M, g_2)$ such that $\phi^* g_2 = g_1$. Isometries preserve all metric properties, including distances and volumes. Conformal equivalence is a much weaker condition. For example, consider the standard round metric $g_{\mathrm{rd}}$ on the unit sphere $\mathbb{S}^n$. The metric $\tilde{g} = c^2 g_{\mathrm{rd}}$ for a constant $c > 0$ with $c \ne 1$ is clearly in the conformal class of $g_{\mathrm{rd}}$. However, $(S^n, \tilde{g})$ is not isometric to $(S^n, g_{\mathrm{rd}})$. An easy way to see this is to compare their total volumes. The volume element scales by $c^n$, so $\mathrm{Vol}(S^n, \tilde{g}) = c^n \mathrm{Vol}(S^n, g_{\mathrm{rd}})$. Since the total volume is an isometric invariant, the two manifolds cannot be isometric [@problem_id:3043437].

### Transformation of Geometric Quantities

While angles are invariant, most other geometric quantities are transformed in a systematic way that depends on the conformal factor $e^{2u}$ and its derivatives.

#### Lengths, Volumes, and Differential Operators

The transformation rules for elementary quantities follow directly from the definition.
- **Length of vectors**: $\|v\|_{\tilde{g}} = e^{u} \|v\|_g$.
- **Volume element**: In [local coordinates](@entry_id:181200), the volume element is $d\mathrm{vol}_g = \sqrt{\det(g_{ij})} dx^1 \wedge \dots \wedge dx^n$. Since $\tilde{g}_{ij} = e^{2u} g_{ij}$, the determinant of the metric tensor transforms as $\det(\tilde{g}_{ij}) = \det(e^{2u} g_{ij}) = (e^{2u})^n \det(g_{ij}) = e^{2nu} \det(g_{ij})$. Therefore, the [volume element](@entry_id:267802) scales as:
  $$
  d\mathrm{vol}_{\tilde{g}} = e^{nu} d\mathrm{vol}_g
  $$
- **Inverse Metric and Gradient**: The [inverse metric](@entry_id:273874) transforms by the reciprocal factor, $\tilde{g}^{ij} = e^{-2u} g^{ij}$. The squared norm of the gradient of a function $f$, given by $|\nabla f|_g^2 = g^{ij} (\partial_i f)(\partial_j f)$, transforms accordingly:
  $$
  |\nabla f|_{\tilde{g}}^2 = \tilde{g}^{ij} (\partial_i f)(\partial_j f) = e^{-2u} g^{ij} (\partial_i f)(\partial_j f) = e^{-2u} |\nabla f|_g^2
  $$

#### The Special Nature of Two Dimensions: Invariant Energies and Operators

The interplay between the scaling of the gradient norm and the [volume element](@entry_id:267802) reveals a remarkable property of two-dimensional geometry. Consider the **Dirichlet energy** of a function $f$:
$$
E_g(f) = \frac{1}{2} \int_M |\nabla f|_g^2 d\mathrm{vol}_g
$$
Under the conformal change $\tilde{g} = e^{2u}g$, the integrand transforms as:
$$
|\nabla f|_{\tilde{g}}^2 d\mathrm{vol}_{\tilde{g}} = (e^{-2u} |\nabla f|_g^2) (e^{nu} d\mathrm{vol}_g) = e^{(n-2)u} |\nabla f|_g^2 d\mathrm{vol}_g
$$
In general, for $n \ge 3$, the Dirichlet energy is not conformally invariant. However, in dimension $n=2$, the exponent becomes $n-2=0$, and the conformal factors cancel precisely. For a 2-dimensional surface, the [volume element](@entry_id:267802) is the area element $d\mu_g$, and we find:
$$
|\nabla f|_{\tilde{g}}^2 d\mu_{\tilde{g}} = e^{(2-2)u} |\nabla f|_g^2 d\mu_g = |\nabla f|_g^2 d\mu_g
$$
Integrating over the manifold, we see that the Dirichlet energy is conformally invariant in dimension 2 [@problem_id:3043418]:
$$
E_{\tilde{g}}(f) = E_g(f) \quad (\text{for } n=2)
$$

This invariance extends to the **Laplace-Beltrami operator**, $\Delta_g f = \mathrm{div}_g(\nabla f)$. The general transformation law is:
$$
\Delta_{\tilde{g}} f = e^{-2u} (\Delta_g f + (n-2) \langle \nabla u, \nabla f \rangle_g)
$$
where $\langle \cdot, \cdot \rangle_g$ is the inner product on [covectors](@entry_id:157727) induced by $g$. Again, for $n=2$, the formula simplifies dramatically:
$$
\Delta_{\tilde{g}} f = e^{-2u} \Delta_g f \quad (\text{for } n=2)
$$
This simple relationship has profound consequences. A function $f$ is called **harmonic** if $\Delta_g f = 0$. From the transformation law, it is clear that if $f$ is harmonic with respect to $g$, then $\Delta_{\tilde{g}} f = e^{-2u} \cdot 0 = 0$, so $f$ is also harmonic with respect to $\tilde{g}$. The converse is also true, as $e^{-2u}$ is always positive. Thus, the property of being a [harmonic function](@entry_id:143397) is a conformal invariant in two dimensions [@problem_id:3043445]. This is a cornerstone of complex analysis, where [harmonic functions](@entry_id:139660) are intimately tied to [holomorphic functions](@entry_id:158563), which represent [conformal maps](@entry_id:271672).

### Transformation of Curvature

Curvature, which measures the failure of a manifold to be locally Euclidean, transforms in a more complex manner.

#### Scalar Curvature
The most important curvature transformation law for many applications in geometric analysis governs the **[scalar curvature](@entry_id:157547)**. If $\tilde{g} = e^{2u} g$ on an $n$-dimensional manifold ($n \ge 3$), the scalar curvature $\tilde{R}$ of $\tilde{g}$ is related to the [scalar curvature](@entry_id:157547) $R$ of $g$ by:
$$
\tilde{R} = e^{-2u} \left( R - 2(n-1)\Delta_g u - (n-2)(n-1)|\nabla u|_g^2 \right)
$$
This formula is a non-linear second-order elliptic partial differential equation for the conformal factor $u$. It allows us to prescribe the scalar curvature of a metric within a given conformal class. For example, if we start with a metric $g$ and wish to find a conformally related metric $\tilde{g}$ with a desired scalar curvature $\tilde{R}_{target}$, we must solve the above equation for $u$. This is the central idea behind the celebrated **Yamabe problem**, which asks whether every compact Riemannian manifold without boundary is conformally equivalent to one with [constant scalar curvature](@entry_id:186408).

#### Conformally Flat Manifolds and the Weyl Tensor

A particularly important class of manifolds are those that are **conformally flat**. A manifold $(M,g)$ is conformally flat if every point has a neighborhood that is conformally equivalent to an open subset of Euclidean space $(\mathbb{R}^n, \delta)$. In other words, locally, one can always find a conformal factor $u$ such that $g = e^{2u} \delta$.

Since curvature is not a conformal invariant, how can we detect if a manifold is conformally flat? The answer lies in decomposing the Riemann curvature tensor. For dimensions $n \ge 3$, there is a part of the Riemann tensor, the **Weyl curvature tensor** $W$, whose vanishing is conformally invariant. Its formula is:
$$
W_{ijkl} = R_{ijkl} - \frac{1}{n-2}(\mathrm{Ric}_{ik}g_{jl} - \mathrm{Ric}_{il}g_{jk} + \mathrm{Ric}_{jl}g_{ik} - \mathrm{Ric}_{jk}g_{il}) + \frac{R}{(n-1)(n-2)}(g_{ik}g_{jl} - g_{il}g_{jk})
$$
The crucial property of the Weyl tensor is that the condition $W=0$ is preserved under conformal changes. A fundamental theorem states that for $n \ge 3$, a Riemannian manifold is conformally flat if and only if its Weyl tensor is identically zero.

A classic example is the standard unit sphere $(\mathbb{S}^n, g_{\mathrm{rd}})$ for $n \ge 3$. The sphere is known to be a space of [constant sectional curvature](@entry_id:272200) $K=1$. Its curvature tensors are given by:
- Riemann tensor: $R_{ijkl} = 1 \cdot (g_{ik}g_{jl} - g_{il}g_{jk})$
- Ricci tensor: $\mathrm{Ric}_{ij} = (n-1)g_{ij}$
- Scalar curvature: $R = n(n-1)$

Substituting these into the formula for the Weyl tensor, a direct calculation shows that the terms exactly cancel, yielding $W_{ijkl} = 0$ [@problem_id:3043422]. This confirms that the sphere is conformally flat.

The explicit conformal map is given by **[stereographic projection](@entry_id:142378)**, $\sigma: \mathbb{S}^n \setminus \{N\} \to \mathbb{R}^n$, from the north pole $N$ to the equatorial [hyperplane](@entry_id:636937). The inverse map $\iota: \mathbb{R}^n \to \mathbb{S}^n \setminus \{N\}$ is given by:
$$
\iota(x) = \left( \frac{2x}{1+|x|^2}, \frac{|x|^2-1}{1+|x|^2} \right)
$$
A direct computation of the [pullback metric](@entry_id:161465) $g_{\mathrm{st}} = \iota^* g_{\mathrm{rd}}$ shows that it is conformally related to the Euclidean metric $\delta$ [@problem_id:3043447]:
$$
g_{\mathrm{st}} = \left( \frac{2}{1+|x|^2} \right)^2 \delta
$$
This explicitly demonstrates the [conformal flatness](@entry_id:159514) of the sphere. Note that the resulting metric $g_{\mathrm{st}}$ on $\mathbb{R}^n$ is conformally flat (as it is conformal to the flat metric $\delta$), but it is not itself flat. We can verify this by calculating its [scalar curvature](@entry_id:157547). Using the transformation formula with $g = \delta$ (so $R=0$) and $e^{2u} = (2/(1+|x|^2))^2$, we find that the [scalar curvature](@entry_id:157547) of $g_{\mathrm{st}}$ is $R_{g_{\mathrm{st}}} = n(n-1)$, a non-zero constant [@problem_id:3043428].

This provides a general strategy to construct metrics that are conformally flat but not flat. Any metric of the form $g = e^{2u} \delta$ on $\mathbb{R}^n$ has a vanishing Weyl tensor and is thus conformally flat. However, if the function $u$ is chosen appropriately, the scalar curvature will be non-zero, proving the metric is not flat [@problem_id:3043427]. For instance, the metric $g_a = \exp(2a|x|^2) \delta$ on $\mathbb{R}^n$ ($n \ge 3$) has scalar curvature $R_{g_a}(0) = -4an(n-1)$ at the origin. For any $a \ne 0$, this curvature is non-zero, so the space is not flat, despite being conformally flat.

Conversely, a conformal change can be used to generate curvature. The famous **Poincaré disk model** of hyperbolic geometry equips the [unit disk](@entry_id:172324) $\mathbb{D} = \{z \in \mathbb{C} : |z|  1\}$ with the metric
$$
g_P = \frac{4}{(1-|z|^2)^2} \delta
$$
where $\delta$ is the flat Euclidean metric. This is a [conformal transformation](@entry_id:193282) of a flat domain. A calculation starting from the metric components yields Christoffel symbols, the Riemann tensor, and finally the Gaussian curvature. The result is that the Gaussian curvature of this metric is constant and equal to $-1$ everywhere on the disk [@problem_id:3043443]. This demonstrates how a simple conformal scaling can transform a [flat space](@entry_id:204618) into a space of constant negative curvature.

### Applications in Geometric Analysis

The systematic way in which geometric quantities scale under conformal changes has deep implications in the field of [geometric analysis](@entry_id:157700), where techniques from partial differential equations are used to study geometric problems.

#### Critical Sobolev Exponents

Many geometric problems involve inequalities relating the size of a function to the size of its derivative, such as the Sobolev inequality: $\|u\|_{L^p} \le C \|\nabla u\|_{L^2}$. A natural question is which of these analytic inequalities are compatible with the underlying geometry of the manifold. One way to enforce compatibility is to demand that the inequality be invariant under a constant conformal rescaling of the metric, $\tilde{g} = \lambda^2 g$ for a constant $\lambda  0$.

Let's analyze how the two sides of the inequality transform for $n \ge 3$.
- The right-hand side involves the $L^2$ norm of the gradient, which is the square root of the Dirichlet energy. We saw that $E_{\tilde{g}}(u) = \lambda^{n-2} E_g(u)$. Thus, $\|\nabla u\|_{L^2(\tilde{g})} = \lambda^{(n-2)/2} \|\nabla u\|_{L^2(g)}$.
- The left-hand side is the $L^p$ norm of the function. It transforms as $\|u\|_{L^p(\tilde{g})} = (\int |u|^p d\mathrm{vol}_{\tilde{g}})^{1/p} = (\int |u|^p \lambda^n d\mathrm{vol}_g)^{1/p} = \lambda^{n/p} \|u\|_{L^p(g)}$.

For the Sobolev inequality to be conformally consistent, the scaling factors must match:
$$
\frac{n}{p} = \frac{n-2}{2} \implies p(n-2) = 2n \implies p = \frac{2n}{n-2}
$$
This exponent, $p^* = \frac{2n}{n-2}$, is known as the **critical Sobolev exponent**. Its "[criticality](@entry_id:160645)" arises precisely from its special relationship with the conformal structure of the manifold. This exponent plays a crucial role in the resolution of the Yamabe problem and in the study of non-linear PDEs on manifolds [@problem_id:3043423].

#### Completeness

Conformal changes can also have a dramatic effect on the global properties of a manifold, such as [metric completeness](@entry_id:186235). A Riemannian manifold is complete if every Cauchy sequence of points converges to a point within the manifold. Incomplete spaces have "holes" or "edges" at a finite distance.

Consider the Euclidean space $\mathbb{R}^n$ with a radial conformal change $\tilde{g} = e^{2u(|x|)}\delta$. The Euclidean space $(\mathbb{R}^n, \delta)$ is complete. However, $(\mathbb{R}^n, \tilde{g})$ may not be. The completeness can be tested by measuring the length of a path that goes to infinity, for instance, a radial ray from the origin. The length of such a ray is:
$$
L = \int_0^\infty e^{u(r)} dr
$$
The manifold is complete if and only if this integral diverges for all paths escaping to infinity, which, by [radial symmetry](@entry_id:141658), reduces to checking this integral. If $L$ is finite, one can traverse from the origin to "infinity" in a finite distance, proving the space is incomplete.

This leads to a fascinating analysis of how the [asymptotic behavior](@entry_id:160836) of the conformal factor determines completeness. For example, if $u(r)$ behaves like $-\alpha \ln r$ for large $r$, then $e^{u(r)}$ behaves like $r^{-\alpha}$. The integral $\int^\infty r^{-\alpha} dr$ converges if $\alpha  1$ and diverges if $\alpha \le 1$. Therefore, the value $\alpha_* = 1$ is a critical threshold: for decay rates faster than $-\ln r$, the space becomes incomplete [@problem_id:3043431]. A simple case is the metric on $\mathbb{R}^n$ with $u(r) = -\ln(1+r^2)$, corresponding to $\alpha=2$. The distance from the origin to infinity is $\int_0^\infty \frac{dr}{1+r^2} = \frac{\pi}{2}$, a finite number, rendering the space incomplete.

In summary, conformal changes of a Riemannian metric provide a rich framework for generating new geometries from old ones. By understanding the precise mechanisms by which lengths, curvatures, and operators transform, we gain powerful tools to construct exotic geometric spaces, probe the relationship between analysis and geometry, and solve deep problems in both fields.