## Introduction
At the core of geometric analysis lies the study of [variational problems](@entry_id:756445), where we seek to optimize geometric quantities such as area and volume. A fundamental question arises: how does the area of a surface change as we deform its shape, and what geometric properties characterize surfaces that are locally area-minimizing? This question necessitates a [differential calculus](@entry_id:175024) for geometric functionals, a role fulfilled by the concept of the [first variation](@entry_id:174697).

This article provides a comprehensive exploration of the [first variation](@entry_id:174697) of the [area functional](@entry_id:635965) and its profound connection to mean curvature. In the first chapter, **Principles and Mechanisms**, we will rigorously derive the [first variation of area](@entry_id:195526) formula, revealing mean curvature as the "gradient" of the [area functional](@entry_id:635965) and establishing the theory of [minimal surfaces](@entry_id:157732). Following this, the chapter on **Applications and Interdisciplinary Connections** will demonstrate the remarkable utility of these ideas, showing how mean curvature governs phenomena from the shape of soap bubbles in physics to the evolution of black holes in general relativity. Finally, **Hands-On Practices** will offer a series of guided problems to reinforce the theoretical concepts through explicit computation. We begin our journey by developing the foundational machinery of the [first variation](@entry_id:174697).

## Principles and Mechanisms

The study of geometric [variational problems](@entry_id:756445), where one seeks to extremize a geometric quantity like area or volume, lies at the heart of [geometric analysis](@entry_id:157700). The foundational tool for this study is the [first variation](@entry_id:174697), which acts as the "derivative" of a geometric functional. In this chapter, we will rigorously develop the [first variation](@entry_id:174697) of the [area functional](@entry_id:635965). This process will naturally lead to the definition and geometric interpretation of [mean curvature](@entry_id:162147), establishing it as the fundamental quantity governing the local geometry of [submanifolds](@entry_id:159439) and their tendency to minimize area.

Throughout this chapter, we will consider a smooth, oriented $n$-dimensional manifold $\Sigma$ smoothly immersed into an $(n+1)$-dimensional Riemannian manifold $(M, g)$ via a map $X: \Sigma \to M$. We denote the [induced metric](@entry_id:160616) on $\Sigma$ by $\gamma = X^*g$, and its associated [volume form](@entry_id:161784) by $d\mu_\gamma$. The area of the [immersed submanifold](@entry_id:264923) is given by the **[area functional](@entry_id:635965)**:
$$
\mathcal{A}(X) = \int_{\Sigma} d\mu_\gamma
$$

### The First Variation of the Area Functional

To understand how the area changes as we deform the immersion, we consider a **smooth one-parameter variation** of $X$. This is a [smooth map](@entry_id:160364) $X: \Sigma \times (-\epsilon, \epsilon) \to M$, where we denote $X_t(\cdot) = X(\cdot, t)$. The initial immersion is $X_0 = X$. The infinitesimal deformation at $t=0$ is captured by the **variation vector field** $V$ along the image of $X$, defined as:
$$
V(p) = \left.\frac{\partial}{\partial t}\right|_{t=0} X_t(p) \quad \text{for } p \in \Sigma
$$
This vector field $V$ can be decomposed at each point into a component tangent to the [submanifold](@entry_id:262388) $X(\Sigma)$ and a component normal to it. For a hypersurface, this decomposition is particularly simple. We choose a smooth unit [normal vector field](@entry_id:268853) $\nu$ along $X(\Sigma)$. Then, the variation vector field can be written as:
$$
V = V^\top + f\nu
$$
where $V^\top$ is the tangential component and $f = g(V, \nu)$ is a [smooth function](@entry_id:158037) on $\Sigma$ representing the magnitude of the normal component [@problem_id:3035271].

The core of the [first variation](@entry_id:174697) calculation is understanding how the induced area element $d\mu_t$ changes with $t$. The derivative of a volume form is related to the trace of the derivative of the metric. A foundational calculation shows that the [first variation](@entry_id:174697) of the area element is given by:
$$
\left.\frac{d}{dt}\right|_{t=0} d\mu_t = \frac{1}{2} \operatorname{tr}_\gamma \left(\left.\frac{d\gamma_t}{dt}\right|_{t=0}\right) d\mu_\gamma
$$
where $\gamma_t = X_t^*g$. The derivative of the metric, $\left.\frac{d\gamma_t}{dt}\right|_{t=0}$, can be shown to depend linearly on the first covariant derivatives of the variation field $V$. This reveals a crucial structural property: because the [area functional](@entry_id:635965)'s integrand depends only on the metric (the [first fundamental form](@entry_id:274022)) and not its derivatives, the [first variation](@entry_id:174697) is a first-order differential operator acting on the variation field $V$ [@problem_id:3035341].

### The Role of Normal and Tangential Variations

The distinct geometric roles of the [normal and tangential components](@entry_id:166204) of the variation field become apparent when we compute their respective contributions to the change in area.

A purely tangential variation, where $V = V^\top$, can be generated by reparametrizing the domain $\Sigma$. Consider a [flow of diffeomorphisms](@entry_id:193938) $\varphi_t: \Sigma \to \Sigma$ generated by a vector field $W$ on $\Sigma$. A variation of the form $X_t = X \circ \varphi_t$ produces a purely tangential variation vector field $V = dX(W)$. By applying the change of variables formula for integration, one can show that the [area functional](@entry_id:635965) is perfectly invariant under such a [reparametrization](@entry_id:176404) [@problem_id:3035227]:
$$
\mathcal{A}(X_t) = \mathcal{A}(X \circ \varphi_t) = \int_{\Sigma} (X \circ \varphi_t)^* d\mu_g = \int_{\Sigma} \varphi_t^*(X^*d\mu_g) = \int_{\Sigma} X^*d\mu_g = \mathcal{A}(X)
$$
This exact invariance for all $t$ means that the [first variation of area](@entry_id:195526) for any purely tangential variation is zero, provided the variation is fixed at the boundary. This is a manifestation of the **[reparametrization invariance](@entry_id:197540)** of the [area functional](@entry_id:635965). Geometrically, simply sliding the domain's parametrization around underneath the immersion does not change the shape or size of the immersed image.

Since tangential variations do not alter the area, the geometrically significant changes must come from the normal component of the variation, $f\nu$. It is these variations that truly deform the shape of the submanifold in the [ambient space](@entry_id:184743).

### Mean Curvature: The Gradient of Area

The previous discussion motivates defining a quantity that captures how the area responds to normal deformations. This quantity is the **[mean curvature](@entry_id:162147)**.

Let us establish a consistent sign convention, which is crucial in this field. We define the **[shape operator](@entry_id:264703)** (or Weingarten map) $S$ with respect to the unit normal $\nu$ as the endomorphism of the tangent space $T_p\Sigma$ given by:
$$
S(U) = -\nabla_U \nu
$$
for any vector field $U$ tangent to $\Sigma$, where $\nabla$ is the Levi-Civita connection of the ambient manifold $(M,g)$. The [shape operator](@entry_id:264703) measures how the [normal vector field](@entry_id:268853) changes as we move along the surface. For a sphere of radius $r$ in Euclidean space with outward normal $\nu$, $S(U) = -(1/r)U$, indicating that the normal vector turns "inward" as we move along any tangent direction.

The **scalar mean curvature** $H$ is defined as the trace of the [shape operator](@entry_id:264703) with respect to the [induced metric](@entry_id:160616) $\gamma$:
$$
H = \operatorname{tr}_\gamma(S) = \gamma^{ij} g(S(\partial_i X), \partial_j X)
$$
With these definitions, a direct calculation of the [first variation of area](@entry_id:195526) for a normal variation $V=f\nu$ yields the fundamental formula:
$$
\left.\frac{d}{dt}\right|_{t=0} \mathcal{A}(X_t) = - \int_{\Sigma} H f \, d\mu_\gamma
$$
This is the **[first variation of area](@entry_id:195526) formula** [@problem_id:3035261]. It reveals that the [mean curvature](@entry_id:162147) $H$ is precisely the function that determines the rate of change of area under a normal deformation. If one thinks of the space of all possible immersions, this formula shows that the "gradient" of the [area functional](@entry_id:635965) is $-H$. This implies that to decrease area most efficiently, one should deform the surface in the direction of $-H\nu$.

An immediate and profound consequence is the Euler-Lagrange equation for the [area functional](@entry_id:635965). A [submanifold](@entry_id:262388) is a **critical point** of the [area functional](@entry_id:635965) (i.e., its area is stationary to first order) if and only if the [first variation](@entry_id:174697) vanishes for all compactly supported variations. Given the formula above, this is equivalent to the condition that its [mean curvature](@entry_id:162147) is identically zero:
$$
H \equiv 0
$$
Such surfaces are called **minimal surfaces**. They are the geometric analogues of geodesics, representing locally area-minimizing configurations.

For a general variation $V = V^\top + f\nu$, where $V^\top$ is induced by a vector field $W$ on $\Sigma$, the full [first variation](@entry_id:174697) formula combines the tangential and normal contributions [@problem_id:3035271]:
$$
\left.\frac{d}{dt}\right|_{t=0} \mathcal{A}(X_t) = \int_{\Sigma} (\operatorname{div}_\gamma W - fH) \, d\mu_\gamma = \int_{\partial\Sigma} g(W, \eta) \, d\sigma - \int_{\Sigma} fH \, d\mu_\gamma
$$
where $\eta$ is the outward conormal to the boundary $\partial\Sigma$. This general form confirms that the interior geometry is governed by $H$, while the tangential variation only contributes a boundary term.

### Geometric Interpretations of Mean Curvature

While the variational definition of mean curvature is powerful, its geometric meaning can be understood through several equivalent characterizations.

#### Curvature Tensors and the Mean Curvature Vector

The shape operator $S$ is intimately related to the **[second fundamental form](@entry_id:161454)**, a [symmetric bilinear form](@entry_id:148281) $A$ defined as:
$$
A(U, W) = g(S(U), W) = -g(\nabla_U \nu, W)
$$
The scalar mean curvature is simply the trace of this form: $H = \operatorname{tr}_\gamma(A)$ [@problem_id:3035278].

The scalar mean curvature $H$ depends on the choice of unit normal $\nu$. If we reverse the orientation by choosing $-\nu$, the [shape operator](@entry_id:264703) flips its sign, $S \to -S$, and so does the scalar mean curvature, $H \to -H$. The geometrically invariant object is the **[mean curvature vector](@entry_id:199617)**, defined as:
$$
\mathbf{H} = H\nu
$$
Under the change $\nu \to -\nu$, the product remains invariant: $(-H)(-\nu) = H\nu = \mathbf{H}$. Thus, the [mean curvature vector](@entry_id:199617) is an intrinsic geometric property of the unoriented hypersurface [@problem_id:3035330]. Its magnitude $|g(\mathbf{H}, \mathbf{H})|^{1/2} = |H|$ represents the "intensity" of the [mean curvature](@entry_id:162147), and its direction indicates the preferred direction of area reduction. In higher codimension, where there is a space of normal vectors, the [mean curvature vector](@entry_id:199617) is the more natural object, defined as the trace of the vector-valued [second fundamental form](@entry_id:161454).

#### Mean Curvature and the Laplacian

Mean curvature can also be expressed in terms of differential operators on the [submanifold](@entry_id:262388), providing a crucial link to analysis and [partial differential equations](@entry_id:143134). For a submanifold $\Sigma \subset \mathbb{R}^{n+1}$, its [mean curvature vector](@entry_id:199617) is given by the Laplace-Beltrami operator acting on the immersion map $X$ itself [@problem_id:3035311]:
$$
\mathbf{H} = \Delta_\Sigma X
$$
where $\Delta_\Sigma = \operatorname{div}_\Sigma \nabla_\Sigma$ is the intrinsic Laplacian of $\Sigma$. This remarkable formula identifies the [mean curvature vector](@entry_id:199617) as a measure of how the immersion map deviates from being a [harmonic function](@entry_id:143397). The condition for a [minimal surface](@entry_id:267317), $H=0$, becomes the system of elliptic PDEs $\Delta_\Sigma X = 0$.

#### Mean Curvature as Averaged Normal Curvature

The scalar [mean curvature](@entry_id:162147) also possesses a clear intuitive meaning. At a point $p \in \Sigma$, the **[normal curvature](@entry_id:270966)** in a tangent direction $U$ (with $\|U\|=1$) is $k_n(U) = A(U,U) = g(S(U),U)$. This measures the curvature of the curve formed by intersecting $\Sigma$ with the 2-plane spanned by $U$ and $\nu$. The scalar mean curvature $H$ is the sum of the [principal curvatures](@entry_id:270598) (the eigenvalues of $S$), so $H/n$ is their arithmetic mean. More generally, it can be shown that $H/n$ is the average of the normal curvatures over all tangent directions [@problem_id:3035311]:
$$
\frac{H}{n} = \frac{1}{\text{vol}(S^{n-1})} \int_{U \in T_p\Sigma, \|U\|=1} k_n(U) \, d\sigma(U)
$$
This gives $H$ the geometric interpretation of an averaged "bending" of the surface at a point.

### Stationarity, Stability, and Generalizations

The [first variation](@entry_id:174697) allows us to identify critical points of the [area functional](@entry_id:635965), but it does not tell us whether these points are local minima, maxima, or saddle points. This is the question of **stability**.

A minimal surface ($H=0$) is **stable** if the [second variation of area](@entry_id:187529) is non-negative for all compactly supported normal variations. The [second variation formula](@entry_id:180586) for a [minimal surface](@entry_id:267317) under a variation $f\nu$ is [@problem_id:3035335]:
$$
\left.\frac{d^2}{dt^2}\right|_{t=0} \mathcal{A}(X_t) = \int_{\Sigma} \left( |\nabla_\gamma f|^2 - |A|^2 f^2 \right) \, d\mu_\gamma
$$
where $|A|^2 = \operatorname{tr}(S^2)$ is the squared norm of the [second fundamental form](@entry_id:161454) (the [sum of squares](@entry_id:161049) of [principal curvatures](@entry_id:270598)).
Stability requires the term $|\nabla_\gamma f|^2$ (which is always non-negative) to dominate the term $-|A|^2f^2$.
- For a flat plane in $\mathbb{R}^3$, the [second fundamental form](@entry_id:161454) is zero, so $|A|^2=0$. The second variation is $\int |\nabla f|^2 d\mu \geq 0$, so the plane is a [stable minimal surface](@entry_id:636062).
- However, there exist minimal surfaces for which $|A|^2$ is large enough that the second variation can become negative for certain choices of $f$. A classic example is the [catenoid](@entry_id:271627) in $\mathbb{R}^3$. This demonstrates that [stationarity](@entry_id:143776) ($H=0$) does not imply stability [@problem_id:3035335].

Finally, the concepts developed for smooth immersions can be extended to much rougher geometric objects. This requires a more robust definition of regularity and curvature.
- **Regularity**: To define a classical, pointwise [second fundamental form](@entry_id:161454) and mean curvature, the immersion $X$ must be at least of class $C^2$. If $X$ is only $C^1$, the second derivatives required to define curvature do not exist in a classical sense, and one must resort to a weak or distributional notion of curvature [@problem_id:3035254].
- **Varifolds**: Geometric Measure Theory provides a powerful framework for studying non-smooth surfaces using **[varifolds](@entry_id:199701)**. A [varifold](@entry_id:194011) is essentially a measure on the space of tangent planes. For this very general class of objects, a [first variation of area](@entry_id:195526) and a corresponding **[generalized mean curvature](@entry_id:199614)** can be defined. If the [first variation](@entry_id:174697) measure is absolutely continuous with respect to the [varifold](@entry_id:194011)'s area measure, the [generalized mean curvature](@entry_id:199614) exists as an $L^p$ vector field. This framework successfully extends the theory of minimal surfaces to objects with singularities and is a cornerstone of modern geometric analysis [@problem_id:3035245].

In summary, the [first variation of area](@entry_id:195526) provides not only the definition of [mean curvature](@entry_id:162147) but also a deep insight into its role as the driving force behind area minimization. This variational perspective is the gateway to the rich theories of minimal surfaces, [constant mean curvature](@entry_id:194008) surfaces, and [geometric flows](@entry_id:198994) like the [mean curvature flow](@entry_id:184231).