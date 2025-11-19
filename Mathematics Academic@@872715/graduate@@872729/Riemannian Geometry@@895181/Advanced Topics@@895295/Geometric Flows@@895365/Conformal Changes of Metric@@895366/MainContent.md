## Introduction
Conformal changes of metric, which involve rescaling a Riemannian metric while preserving angles, represent one of the most powerful and versatile tools in modern geometry and theoretical physics. This concept allows us to relate geometrically distinct worlds—such as the flat plane and the curved sphere—within a single, unified framework. The central challenge lies in understanding precisely how the geometric structure of a manifold, from its [connection and curvature](@entry_id:158520) to its global properties, responds to such a transformation. While angles are preserved, almost every other quantity is altered, and quantifying these changes is key to unlocking the full potential of the theory.

This article provides a graduate-level exploration of this topic. The first chapter, "Principles and Mechanisms," will dissect the mathematical machinery governing the transformation of curvature and introduce key invariants like the Weyl tensor. Following this, "Applications and Interdisciplinary Connections" will showcase how these principles are applied to solve problems in [geometric analysis](@entry_id:157700), such as the Yamabe problem, and to formulate fundamental concepts in General Relativity and quantum [field theory](@entry_id:155241). Finally, "Hands-On Practices" will offer concrete exercises to solidify your understanding of these abstract concepts, allowing you to compute and analyze conformal changes in canonical examples.

## Principles and Mechanisms

Having introduced the fundamental concept of a conformal class of metrics, we now delve into the principles and mechanisms governing how geometric quantities transform under conformal changes. This chapter will dissect the mathematical machinery that dictates the interplay between a metric and its conformal cousins, revealing which geometric properties are preserved, which are altered, and which can be controlled. We will begin with the effect on the connection, proceed to the various notions of curvature, and culminate in a discussion of conformally covariant operators, which lie at the heart of modern [geometric analysis](@entry_id:157700).

### The Hierarchy of Geometric Equivalence

A conformal change of a Riemannian metric $g$ on a manifold $M$ is the replacement of $g$ with a new metric $\tilde{g}$ of the form
$$ \tilde{g} = e^{2u} g $$
for some [smooth function](@entry_id:158037) $u: M \to \mathbb{R}$. The function $u$ is often called the **conformal factor**. Two metrics related in this way are said to be **conformally equivalent**, and they belong to the same **conformal class** $[g]$.

The geometric essence of this transformation is that it preserves angles between tangent vectors while rescaling their lengths. If $v, w \in T_pM$ are [tangent vectors](@entry_id:265494) at a point $p$, their lengths and angle $\theta$ under $g$ are $|v|_g$, $|w|_g$, and $\cos\theta = \frac{g(v,w)}{|v|_g |w|_g}$. Under the new metric $\tilde{g}$, their lengths become $|\tilde{v}|_{\tilde{g}} = \sqrt{\tilde{g}(v,v)} = \sqrt{e^{2u(p)}g(v,v)} = e^{u(p)}|v|_g$, but the angle remains unchanged:
$$ \cos\tilde{\theta} = \frac{\tilde{g}(v,w)}{|\tilde{v}|_{\tilde{g}} |\tilde{w}|_{\tilde{g}}} = \frac{e^{2u(p)}g(v,w)}{(e^{u(p)}|v|_g)(e^{u(p)}|w|_g)} = \frac{g(v,w)}{|v|_g |w|_g} = \cos\theta $$
This angle-preserving property is the defining characteristic of [conformal geometry](@entry_id:186351).

Conformal equivalence is the most general of a hierarchy of geometric similarities. It is crucial to distinguish it from its more restrictive relatives [@problem_id:2971834]:

1.  **Isometry**: Two Riemannian manifolds $(M_1, g_1)$ and $(M_2, g_2)$ are isometric if there exists a diffeomorphism $F: M_1 \to M_2$ such that $F^*g_2 = g_1$. This is the strongest form of equivalence, preserving all metric properties, including lengths, angles, and volumes. If we consider the metrics on the same underlying manifold $M$, we say $\tilde{g}$ is isometric to $g$ *via the identity map* if $\tilde{g} = g$. For a conformal change $\tilde{g} = e^{2u}g$, this condition holds if and only if $e^{2u} \equiv 1$, which means $u \equiv 0$.

2.  **Homothety**: A map $F: (M_1, g_1) \to (M_2, g_2)$ is a homothety if $F^*g_2 = c^2 g_1$ for some constant $c > 0$. This is a uniform scaling of the metric. On a single manifold $M$, $\tilde{g} = e^{2u}g$ is homothetic to $g$ *via the identity map* if $e^{2u}$ is a positive constant. This is equivalent to the condition that the function $u$ is a constant.

3.  **Conformal Equivalence**: As defined, this allows the scaling factor $e^{2u}$ to be any smooth positive function on $M$.

A subtle but important point is that a metric that is homothetic to another via the identity map may in fact be isometric to it via a different map. For example, on $M = \mathbb{R}^n$ with the Euclidean metric $g_{\mathbb{E}}$, consider a constant conformal factor $u(x) \equiv u_0$. The new metric is $\tilde{g} = e^{2u_0} g_{\mathbb{E}}$. While $(\mathbb{R}^n, \tilde{g})$ is not isometric to $(\mathbb{R}^n, g_{\mathbb{E}})$ via the identity, it is isometric via the dilation map $D_\lambda(x) = \lambda x$ with $\lambda = e^{-u_0}$. The [pullback](@entry_id:160816) of $\tilde{g}$ by this map is indeed $g_{\mathbb{E}}$, as a direct calculation shows [@problem_id:2971834].

### Transformation of the Connection and Curvature

The fundamental question in [conformal geometry](@entry_id:186351) is how geometric objects, which are defined by the metric, behave under a conformal change. The key to this is understanding the transformation of the Levi-Civita connection.

#### The Levi-Civita Connection

The Levi-Civita connection $\nabla$ is uniquely determined by the metric $g$. A new metric $\tilde{g}$ will have its own unique Levi-Civita connection, $\tilde{\nabla}$. The relationship between them can be derived from the Koszul formula. Let us denote the Christoffel symbols of $g$ and $\tilde{g}$ in a [local coordinate system](@entry_id:751394) by $\Gamma^k_{ij}$ and $\tilde{\Gamma}^k_{ij}$, respectively. A direct computation starting from the Koszul formula for $\tilde{\Gamma}^k_{ij}$ and using $\tilde{g}_{ij} = e^{2u}g_{ij}$ and $\tilde{g}^{ij} = e^{-2u}g^{ij}$ yields the following fundamental relationship [@problem_id:2971824]:
$$ \tilde{\Gamma}^k_{ij} - \Gamma^k_{ij} = \delta^k_i u_j + \delta^k_j u_i - g_{ij} u^k $$
where $u_i = \partial_i u$ are the components of the 1-form $du$, and $u^k = g^{k\ell}u_\ell$ are the components of the [gradient vector](@entry_id:141180) field $\nabla u$.

This formula is of paramount importance. It shows that the difference between two connections, $\tilde{\nabla} - \nabla$, is not itself a connection but a $(1,2)$-tensor field. This tensorial nature of the difference is what allows for a systematic study of how all curvature tensors, which are derivatives of the Christoffel symbols, transform.

#### Curvature Tensors

With the transformation law for the connection in hand, we can derive the corresponding laws for curvature. The results reveal that curvature is highly sensitive to conformal changes.

**Ricci and Scalar Curvature:** The Ricci tensor $\tilde{R}_{ij}$ and scalar curvature $\tilde{R}$ of the metric $\tilde{g} = e^{2u}g$ are related to those of $g$ by the following formulas, which can be derived from the transformation of the Christoffel symbols. For a manifold of dimension $n \ge 3$, the Ricci tensor transforms as [@problem_id:897785]:
$$ \tilde{R}_{ij} = R_{ij} - (n-2)\nabla_i\nabla_j u - g_{ij}\Delta_g u + (n-2)((\nabla_i u)(\nabla_j u) - g_{ij}|\nabla u|^2_g) $$
where $\nabla_i\nabla_j u$ is the Hessian of $u$, $\Delta_g u = g^{ij}\nabla_i\nabla_j u$ is the Laplace-Beltrami operator, and $|\nabla u|^2_g = g^{ij}(\nabla_i u)(\nabla_j u)$.

By taking the trace of this equation with respect to $\tilde{g}^{ij} = e^{-2u}g^{ij}$, we find the transformation law for the scalar curvature:
$$ \tilde{R} = e^{-2u} \left( R - 2(n-1)\Delta_g u - (n-2)(n-1)|\nabla u|^2_g \right) $$
These formulas are the engine of [conformal geometry](@entry_id:186351), but their complexity shows that curvature does not, in general, behave simply under conformal rescaling. A special case arises for $n=2$, where the term $(n-2)$ vanishes, leading to a much simpler structure, as we will see.

**Sectional Curvature:** The [sectional curvature](@entry_id:159738), which captures the notion of curvature of 2-dimensional planes in the tangent space, has an even more intricate transformation law. For a 2-plane $\sigma \subset T_pM$ spanned by a $g$-orthonormal basis $\{X, Y\}$, the sectional curvature $K_{\tilde{g}}(\sigma)$ is given by [@problem_id:2971825]:
$$ K_{\tilde{g}}(\sigma) = e^{-2u} \left( K_g(\sigma) - (\text{Hess}_g u)(X,X) - (\text{Hess}_g u)(Y,Y) - |\nabla^{\sigma^\perp} u|_g^2 \right) $$
where $\text{Hess}_g u$ is the Hessian tensor of $u$ and $\nabla^{\sigma^\perp} u$ is the component of the gradient of $u$ orthogonal to the plane $\sigma$.

This formula immediately dispels several common misconceptions. For instance, the sign of sectional curvature is not a conformal invariant. A dramatic illustration of this is that the flat Euclidean space $(\mathbb{R}^n, g_{\mathbb{E}})$, which has zero sectional curvature everywhere, is conformally equivalent to both the standard $n$-sphere $S^n$ (with [constant positive curvature](@entry_id:268046) $+1$) and [hyperbolic space](@entry_id:268092) $\mathbb{H}^n$ (with constant negative curvature $-1$).

The metric on $\mathbb{R}^n$ corresponding to the sphere is obtained via [stereographic projection](@entry_id:142378). For the unit sphere $S^n$, this metric is $\tilde{g} = \left(\frac{2}{1+|x|^2}\right)^2 g_{\mathbb{E}}$. Here, the original curvature is $K_g=0$, but the new curvature is $K_{\tilde{g}}=+1$ [@problem_id:2971834] [@problem_id:2971802].

Similarly, the Poincaré ball model of hyperbolic space endows the open unit ball $\mathbb{B}^n \subset \mathbb{R}^n$ with the metric $\tilde{g} = \left(\frac{2}{1-|x|^2}\right)^2 g_{\mathbb{E}}$. This metric is manifestly conformal to the flat Euclidean metric, yet a calculation using the transformation law shows it has [constant sectional curvature](@entry_id:272200) $K_{\tilde{g}}=-1$ [@problem_id:2971825]. These canonical examples demonstrate that a [conformally flat manifold](@entry_id:201155) is not necessarily flat, and that both positive and [negative curvature](@entry_id:159335) can arise from a flat background via conformal changes.

### Conformal Flatness and the Weyl Tensor

A Riemannian manifold $(M,g)$ is called **conformally flat** if every point has a neighborhood that is conformally equivalent to an open subset of Euclidean space. The examples of the sphere and [hyperbolic space](@entry_id:268092) show that they are conformally flat. A natural question arises: which manifolds are conformally flat?

In dimension $n=2$, the situation is simple. The transformation law for the Gauss curvature $K$ (which is the sectional curvature in 2D) simplifies to:
$$ \tilde{K} = e^{-2u}(K - \Delta_g u) $$
To make a metric locally flat, we need to find a function $u$ such that $\tilde{K}=0$, which requires solving the equation $\Delta_g u = K_g$. This is a linear, second-order elliptic PDE (the Poisson equation) which is always locally solvable. Thus, *every 2-dimensional Riemannian manifold is locally conformally flat* [@problem_id:2971825]. This is a classical result, equivalent to the existence of local [isothermal coordinates](@entry_id:272481).

In dimensions $n \ge 3$, the situation is far more rigid. Not all manifolds are conformally flat. The obstruction to [conformal flatness](@entry_id:159514) is encoded in a specific part of the Riemann [curvature tensor](@entry_id:181383). The Riemann tensor $R$ can be decomposed into a curvature part determined by the Ricci tensor and a trace-free part known as the **Weyl [conformal tensor](@entry_id:200229)**, $W$. For $n \ge 3$, this decomposition is:
$$ R_{ijkl} = W_{ijkl} + \frac{1}{n-2}(g_{ik}R_{jl} - g_{il}R_{jk} + g_{jl}R_{ik} - g_{jk}R_{il}) - \frac{R}{(n-1)(n-2)}(g_{ik}g_{jl} - g_{il}g_{jk}) $$
The defining property of the Weyl tensor is its behavior under a conformal change $\tilde{g} = e^{2u}g$. Its components transform as:
$$ \tilde{W}_{ijkl} = e^{2u}W_{ijkl} $$
Crucially, this means that the Weyl tensor vanishes for $\tilde{g}$ if and only if it vanishes for $g$. In other words, the condition $W \equiv 0$ is a **conformal invariant**.

A fundamental theorem of Weyl and Schouten states that for $n \ge 4$, a Riemannian manifold is conformally flat if and only if its Weyl tensor is identically zero. (For $n=3$, the Weyl tensor is always zero, and the obstruction is a different tensor called the Cotton tensor).

A concrete example of a manifold that is *not* conformally flat is the product of two 2-spheres, $M^4 = S^2(r_1) \times S^2(r_2)$, for $r_1, r_2 > 0$. A direct calculation of the curvature of this product manifold and its decomposition reveals that its Weyl tensor is non-vanishing, and therefore $S^2 \times S^2$ cannot be conformally flat [@problem_id:2971818].

### Conformally Covariant Operators and the Yamabe Problem

The intricate transformation laws for curvature motivate the search for operators that behave more "naturally" or "covariantly" under conformal changes. Such operators are central to solving geometric problems by recasting them as problems in [partial differential equations](@entry_id:143134).

#### The Conformal Laplacian and the Yamabe Problem

The transformation law for the scalar curvature $\tilde{R}$ is cumbersome. However, by combining it with the Laplacian, one can construct a remarkable operator. For a manifold of dimension $n \ge 3$, the **conformal Laplacian**, or **Yamabe operator**, is defined as:
$$ L_g := -\frac{4(n-1)}{n-2}\Delta_g + R_g $$
The specific constant $\frac{4(n-1)}{n-2}$ is chosen precisely to give this operator a simple and powerful [conformal covariance](@entry_id:189180) property. To reveal this property, it is conventional to parameterize the conformal metric as $\tilde{g} = v^{\frac{4}{n-2}}g$, where $v$ is a smooth positive function. With this normalization, a calculation shows that the scalar curvature $\tilde{R}$ of the new metric is given by the elegant formula [@problem_id:2971811]:
$$ \tilde{R} = v^{-\frac{n+2}{n-2}} L_g(v) $$
This relation is the key to the celebrated **Yamabe problem**. The problem asks: given a compact Riemannian manifold $(M,g)$, can one find a metric $\tilde{g}$ in the same conformal class $[g]$ that has [constant scalar curvature](@entry_id:186408)?
Using the formula above, this geometric problem is transformed into an analytic one. We are seeking a positive function $v$ and a constant $\kappa$ such that $\tilde{R} \equiv \kappa$. This is equivalent to solving the semilinear elliptic PDE:
$$ L_g(v) = \kappa \, v^{\frac{n+2}{n-2}} $$
The study of this equation, known as the Yamabe equation, has been a central theme of [geometric analysis](@entry_id:157700) for decades, with its complete solution by Yamabe, Trudinger, Aubin, and Schoen standing as a landmark achievement.

The Yamabe operator also satisfies a more [general covariance](@entry_id:159290) law. For any [smooth function](@entry_id:158037) $\phi$, it transforms as [@problem_id:2971815]:
$$ L_{\tilde{g}}(\phi) = v^{-\frac{n+2}{n-2}} L_g(v\phi) $$
This property is described by saying $L_g$ is a conformally covariant operator of bidegree $\left(\frac{n-2}{2}, \frac{n+2}{2}\right)$.

### Advanced Topics: The Paneitz Operator and Q-Curvature

The story of conformally covariant operators does not end with the second-order Yamabe operator. In dimension $n=4$, there exists a natural fourth-order analogue. The **Paneitz operator** $P_g$ is defined on a [4-manifold](@entry_id:161847) as [@problem_id:2971823]:
$$ P_g \varphi = \Delta_g^2 \varphi + \nabla^i\left( \left(\frac{2}{3}R_g g_{ij} - 2R_{ij}\right) \nabla^j \varphi \right) $$
The remarkable property of this operator is that under a conformal change $\tilde{g}=e^{2u}g$, it transforms very simply when acting on functions (which are tensors of weight 0):
$$ P_{\tilde{g}}(\varphi) = e^{-4u} P_g(\varphi) $$
This means that, unlike the Yamabe operator, the Paneitz operator is conformally invariant up to a simple scaling factor. This property makes it a powerful tool in 4-dimensional [conformal geometry](@entry_id:186351).

Associated with the Paneitz operator is **Branson's Q-curvature**, a scalar quantity defined in terms of curvature and its derivatives. On a compact [4-manifold](@entry_id:161847), the Q-curvature and Paneitz operator are linked to the conformal change $\hat{g} = e^{2w}g$ by the equation:
$$ P_g w + 2Q_g = 2Q_{\hat{g}} e^{4w} $$
This equation is a fourth-order analogue of the scalar curvature transformation law. A key result is that the total Q-curvature, $\int_M Q_g dV_g$, is a conformal invariant. This immediately implies that one can only hope to find a conformal metric with constant positive Q-curvature if the total Q-curvature is positive to begin with [@problem_id:2971830].

Deeper results, analogous to the solution of the Yamabe problem, connect the existence of metrics with special properties to the analytic properties of the Paneitz operator. For instance, on a compact [4-manifold](@entry_id:161847) with positive Yamabe invariant, a positive total Q-curvature is a sufficient condition to guarantee the existence of a conformal metric with constant positive Q-curvature [@problem_id:2971830]. This is a profound theorem at the intersection of geometry, topology, and nonlinear PDE, showcasing the depth and utility of the principles and mechanisms of [conformal geometry](@entry_id:186351).