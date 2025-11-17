## Introduction
The Reilly formula stands as a cornerstone of modern geometric analysis, providing a profound and quantitative link between the analytic properties of functions on a manifold and the geometry of the manifold itself, including its boundary. Its significance lies in its ability to translate local information, captured by [partial differential equations](@entry_id:143134), into global geometric and topological consequences. The formula addresses the fundamental problem of relating the "bulk" or interior of a domain to its boundary, a theme that runs deep through mathematics. This article offers a graduate-level exploration of this powerful identity, guiding the reader from its foundational principles to its most impactful applications.

Across three chapters, this article will build a complete understanding of the Reilly formula. The first chapter, **Principles and Mechanisms**, meticulously lays the groundwork, establishing the necessary differential-geometric operators, deriving the formula from the Bochner identity, and examining the regularity conditions for its validity. The second chapter, **Applications and Interdisciplinary Connections**, showcases the formula's utility as a versatile tool, demonstrating how it yields sharp eigenvalue estimates in [spectral geometry](@entry_id:186460), proves seminal [geometric inequalities](@entry_id:197381) and [rigidity theorems](@entry_id:198222), and underpins the modern theory of [geometric stability](@entry_id:193596). Finally, the **Hands-On Practices** chapter provides a set of targeted problems designed to solidify comprehension by applying the concepts to concrete examples in Euclidean space and on the sphere.

## Principles and Mechanisms

This chapter elucidates the fundamental principles underpinning the Reilly formula. We begin by establishing the necessary differential-geometric toolkit, including a careful treatment of sign conventions for key operators. We then explore the [intrinsic and extrinsic geometry](@entry_id:161677) of a manifold's boundary, which provides the essential language for formulating [boundary value problems](@entry_id:137204). With these preliminaries, we derive the Reilly formula from the Bochner-Weitzenböck identity and the [divergence theorem](@entry_id:145271). Finally, we discuss the regularity conditions required for the formula's validity and explore its generalizations to weighted measures and quasilinear operators, illustrating the breadth and power of this integral identity in modern geometric analysis.

### Foundational Operators and Green's Identity

The study of partial differential equations on a Riemannian manifold $(M^n, g)$ relies on a standard set of [differential operators](@entry_id:275037). For a [smooth function](@entry_id:158037) $f \in C^\infty(M)$, its **gradient**, denoted $\nabla f$ (or $\mathrm{grad} f$), is the vector field metrically dual to its differential $df$, defined by the relation $g(\nabla f, X) = df(X)$ for any vector field $X$. The **divergence** of a vector field $X$, denoted $\mathrm{div}(X)$, is the metric trace of its covariant derivative, $\mathrm{div}(X) = \mathrm{tr}_g(\nabla X)$.

The **Laplace-Beltrami operator**, or Laplacian, $\Delta$, is a second-order differential operator that generalizes the familiar Laplacian from Euclidean space. A point of frequent confusion in the literature is its sign convention. In [geometric analysis](@entry_id:157700), the Laplacian is typically defined as a "positive" operator, in the sense that its [principal symbol](@entry_id:190703) is positive definite. This convention defines the Laplacian as the [divergence of the gradient](@entry_id:270716):
$$ \Delta f = \mathrm{div}(\nabla f) $$
In contrast, much of the PDE literature prefers a convention where the Laplacian is a negative operator, $\tilde{\Delta} f = -\mathrm{div}(\nabla f)$, such that in Euclidean coordinates, $\tilde{\Delta} f = -\sum_i \partial_{ii} f$. It is crucial to be aware of these differing conventions when consulting various sources. Throughout this text, we shall adopt the [geometric analysis](@entry_id:157700) convention, $\Delta = \mathrm{div}(\nabla)$. [@problem_id:3036528] [@problem_id:3036533]

The fundamental link between bulk integrals and boundary integrals on a compact manifold $M$ with a smooth boundary $\partial M$ is provided by the **[divergence theorem](@entry_id:145271)**, a generalization of Stokes' theorem. For any smooth vector field $X$ on $M$, it states:
$$ \int_M \mathrm{div}(X) \, dV_g = \int_{\partial M} g(X, \nu) \, dA_g $$
where $dV_g$ is the Riemannian volume measure on $M$, $dA_g$ is the induced hypersurface measure on $\partial M$, and $\nu$ is the outward-pointing unit [normal vector field](@entry_id:268853) along $\partial M$.

A direct and indispensable consequence of the [divergence theorem](@entry_id:145271) is **Green's first identity**. We derive it by applying the divergence theorem to the vector field $X = v \nabla u$ for two [smooth functions](@entry_id:138942) $u, v \in C^\infty(M)$. Using the product rule for the divergence, $\mathrm{div}(v \nabla u) = g(\nabla v, \nabla u) + v \, \mathrm{div}(\nabla u)$, and our definition of the Laplacian, we have:
$$ \mathrm{div}(v \nabla u) = g(\nabla u, \nabla v) + v \Delta u $$
Integrating this identity over $M$ and applying the divergence theorem to the left-hand side yields:
$$ \int_{\partial M} g(v \nabla u, \nu) \, dA_g = \int_M g(\nabla u, \nabla v) \, dV_g + \int_M v \Delta u \, dV_g $$
Recognizing that $g(\nabla u, \nu) = \partial_\nu u$ is the **[normal derivative](@entry_id:169511)** of $u$, we arrive at Green's first identity:
$$ \int_M g(\nabla u, \nabla v) \, dV_g = -\int_M v \Delta u \, dV_g + \int_{\partial M} v \, \partial_\nu u \, dA_g $$
This identity is the cornerstone of [integration by parts](@entry_id:136350) on manifolds and is the primary analytic tool used in the derivation of the Reilly formula. Note that if one were to use the PDE convention $\tilde{\Delta} = -\Delta$, the sign on the bulk term $\int_M v \tilde{\Delta} u \, dV_g$ would become positive. Furthermore, since the choice of $u$ and $v$ is arbitrary, an equivalent form is obtained by swapping their roles. [@problem_id:3036528]

### The Geometry of the Boundary

The Reilly formula relates interior properties of a function to its behavior on the boundary, mediated by the boundary's geometry. To express this relationship, we must introduce the key tensors that describe the extrinsic curvature of $\partial M$ as a [submanifold](@entry_id:262388) of $M$.

Let $\nabla^{\partial M}$ be the Levi-Civita connection on $(\partial M, g|_{\partial M})$. The connection $\nabla$ on $M$ and $\nabla^{\partial M}$ are related by the **Gauss formula**. For [vector fields](@entry_id:161384) $X, Y$ tangent to $\partial M$, the vector $\nabla_X Y$ can be decomposed into its tangential and normal parts:
$$ \nabla_X Y = \nabla^{\partial M}_X Y + II(X, Y)\nu $$
The [symmetric tensor](@entry_id:144567) $II$ is the **[second fundamental form](@entry_id:161454)** of $\partial M$. It measures the extent to which $\partial M$ is curved within the ambient manifold $M$. Its sign depends on the choice of normal vector. A common convention, which we adopt, defines the [second fundamental form](@entry_id:161454) via the **shape operator** (or Weingarten map) $S$. For a vector $X \in T_p \partial M$, the [shape operator](@entry_id:264703) is defined as $S(X) = \nabla_X \nu$. Crucially, for any $X$ tangent to the boundary, the vector $\nabla_X \nu$ is also tangent to the boundary. This can be seen by differentiating the identity $g(\nu, \nu) = 1$ along $X$, which yields $2g(\nabla_X \nu, \nu) = 0$. The shape operator is a self-adjoint endomorphism of the [tangent space](@entry_id:141028) of the boundary. [@problem_id:3036530]

The [second fundamental form](@entry_id:161454) is then defined as $II(X, Y) = g(S(X), Y) = g(\nabla_X \nu, Y)$. The trace of the [second fundamental form](@entry_id:161454) (or equivalently, of the shape operator) is the **mean curvature** $H = \mathrm{tr}_{\partial M}(II) = \mathrm{tr}(S)$. This scalar function measures the average [extrinsic curvature](@entry_id:160405) of the boundary at each point. For a sphere of radius $R$ in Euclidean space, with the outward normal, our convention gives $H = (n-1)/R > 0$. [@problem_id:3036530]

With these geometric tools, we can relate differential operators on the ambient manifold $M$ to their counterparts on the boundary $\partial M$. The gradient $\nabla f$ of a function $f$ on $M$ can be decomposed at any point on $\partial M$ into its tangential and normal components:
$$ \nabla f = \nabla_T f + (\partial_\nu f)\nu $$
Here, $\nabla_T f$ is the **tangential gradient**, which is simply the gradient of the restriction of $f$ to $\partial M$, computed with the [induced metric](@entry_id:160616). [@problem_id:3036518]

More subtle is the relationship between the Hessians. The **ambient Hessian** is the tensor $\nabla^2 f(X, Y) = g(\nabla_X \nabla f, Y)$. The **boundary Hessian** is $\nabla^2_T f(X, Y) = g(\nabla^{\partial M}_X \nabla_T f, Y)$. A careful calculation using the Gauss formula reveals their relationship for [tangent vectors](@entry_id:265494) $X, Y$:
$$ \nabla^2 f(X, Y) = \nabla^2_T f(X, Y) + II(X, Y) \partial_\nu f $$
Taking the trace of this identity over an orthonormal basis of $T_p \partial M$ leads to a fundamental relationship between the ambient Laplacian $\Delta f$, the **tangential Laplacian** $\Delta_T f = \mathrm{tr}_{\partial M}(\nabla^2_T f)$, and the mean curvature $H$:
$$ \Delta_T f = \Delta f - \nabla^2 f(\nu, \nu) - H \partial_\nu f $$
This formula shows that the tangential Laplacian is not simply the restriction of the ambient Laplacian to the boundary. The difference involves the second normal derivative of $f$ and a term coupling the mean curvature to the first [normal derivative](@entry_id:169511). These identities are the algebraic key to transforming the boundary terms in the Reilly formula into their [canonical form](@entry_id:140237). [@problem_id:3036518]

### The Reilly Formula: Derivation and Statement

The Reilly formula is an integral identity that arises from the pointwise **Bochner-Weitzenböck identity**. For any [smooth function](@entry_id:158037) $f$ on a Riemannian manifold, this identity reads:
$$ \frac{1}{2}\Delta(|\nabla f|^2) = |\nabla^2 f|^2 + \mathrm{Ric}(\nabla f, \nabla f) + g(\nabla (\Delta f), \nabla f) $$
Here, $|\nabla^2 f|^2$ is the squared Hilbert-Schmidt norm of the Hessian tensor, and $\mathrm{Ric}(\nabla f, \nabla f)$ is the Ricci curvature tensor evaluated in the direction of the gradient. This identity is a cornerstone of [geometric analysis](@entry_id:157700), relating the Laplacian of the gradient's energy to the function's second derivatives and the manifold's curvature.

To derive the Reilly formula, we first rearrange the Bochner identity and combine it with the divergence of the vector field $(\Delta f)\nabla f$:
$$ \mathrm{div}((\Delta f)\nabla f) = g(\nabla(\Delta f), \nabla f) + (\Delta f)^2 $$
Combining these two pointwise identities allows us to express the integrand of the Reilly formula as a sum of divergences:
$$ (\Delta f)^2 - |\nabla^2 f|^2 - \mathrm{Ric}(\nabla f, \nabla f) = \mathrm{div}((\Delta f)\nabla f) - \frac{1}{2}\Delta(|\nabla f|^2) $$
Integrating this equation over the manifold $M$ and applying the [divergence theorem](@entry_id:145271) to each term on the right-hand side yields:
$$ \int_M \left( (\Delta f)^2 - |\nabla^2 f|^2 - \mathrm{Ric}(\nabla f, \nabla f) \right) dV_g = \int_{\partial M} \left( (\Delta f)\partial_\nu f - \frac{1}{2}\partial_\nu(|\nabla f|^2) \right) dA_g $$
The final step is to substitute the decomposition formulas for the boundary operators from the previous section into the boundary integrand. After significant algebraic manipulation, this yields the **Reilly formula**:
$$ \int_M \left( (\Delta f)^2 - |\nabla^2 f|^2 - \mathrm{Ric}(\nabla f, \nabla f) \right) dV_g = \int_{\partial M} \left( H(\partial_\nu f)^2 + II(\nabla_T f, \nabla_T f) + 2\partial_\nu f \Delta_T f - 2g(\nabla_T(\partial_\nu f), \nabla_T f) \right) dA_g $$
This powerful formula connects a bulk integral, involving the Hessian and Ricci curvature, to a boundary integral, involving the [extrinsic curvature](@entry_id:160405) ([mean curvature](@entry_id:162147) and second fundamental form) and the boundary data of the function. [@problem_id:3036519]

### Special Cases and Interpretations

The power of the Reilly formula is best appreciated by considering key special cases.

#### Closed Manifolds and the Integral Bochner Identity
If the manifold $M$ is closed, meaning its boundary $\partial M$ is empty, then all boundary integrals vanish. In this scenario, the Reilly formula simplifies to:
$$ \int_M \left( (\Delta f)^2 - |\nabla^2 f|^2 - \mathrm{Ric}(\nabla f, \nabla f) \right) dV_g = 0 $$
This is known as the **integral Bochner identity**. It is a fundamental result in its own right, providing a global constraint on the second derivatives of any smooth function on a closed manifold. For example, on a manifold with non-negative Ricci curvature ($\mathrm{Ric}(X, X) \ge 0$), it implies the inequality $\int_M (\Delta f)^2 dV_g \ge \int_M |\nabla^2 f|^2 dV_g$. This inequality has profound consequences for the analysis of harmonic functions and the [topology of manifolds](@entry_id:267834) with positive curvature. [@problem_id:3036529]

### Rigor and Regularity Conditions

The derivation presented above assumed that the manifold, its boundary, and the function $f$ are all smooth ($C^\infty$). This classical setting ensures all terms are well-defined pointwise and the divergence theorem applies without issue. However, in [modern analysis](@entry_id:146248), it is crucial to understand the minimal regularity required for such an identity to hold. [@problem_id:3036526]

The Reilly formula can be extended to functions in the Sobolev space $f \in H^2(M)$. In this weak setting, the derivatives $\nabla f$, $\nabla^2 f$, and $\Delta f$ are only guaranteed to be in $L^2(M)$. Consequently, the bulk integrand terms like $(\Delta f)^2$ and $|\nabla^2 f|^2$ are in $L^1(M)$, ensuring the bulk integral is well-defined.

The boundary terms require more care. For the theory to work, the manifold and its boundary must possess sufficient regularity. A standard set of assumptions is that the metric $g$ is of class $C^{1,1}$ (its components have Lipschitz first derivatives) and the boundary $\partial M$ is a $C^2$ (or at least $C^{1,1}$) hypersurface. Under these conditions:
- The geometric quantities, mean curvature $H$ and second fundamental form $II$, are well-defined and belong to $L^\infty(\partial M)$.
- The Sobolev [trace theorems](@entry_id:203967) apply. For $f \in H^2(M)$, the trace of its gradient, $\nabla f|_{\partial M}$, is in $H^{1/2}(\partial M)$, and the trace of the function itself, $f|_{\partial M}$, is in $H^{3/2}(\partial M)$.
- Consequently, the [normal derivative](@entry_id:169511) $\partial_\nu f$ and the tangential gradient $\nabla_T f$ are in $H^{1/2}(\partial M)$, which embeds into $L^2(\partial M)$. Terms like $H(\partial_\nu f)^2$ are therefore integrable on the boundary.
- The most subtle term involves the tangential Laplacian. Since $f|_{\partial M} \in H^{3/2}(\partial M)$, its tangential Laplacian $\Delta_T f$ is only a distribution in the dual space $H^{-1/2}(\partial M)$. The corresponding boundary term, such as $\int_{\partial M} (\partial_\nu f)(\Delta_T f) dA_g$, must be interpreted not as a classical integral but as a duality pairing $\langle \Delta_T f, \partial_\nu f \rangle_{H^{-1/2} \times H^{1/2}}$, which is well-defined.

The proof in this weak setting proceeds by an approximation argument: one takes a sequence of smooth functions $f_k \to f$ in $H^2(M)$, applies the classical Reilly formula to each $f_k$, and passes to the limit using the continuity of the trace operators and the stability of the duality pairings. If the boundary is only Lipschitz, the very definition of curvature becomes problematic, and the Reilly formula in this form no longer holds without reinterpreting the geometric terms in a weak (e.g., distributional) sense. [@problem_id:3036526] [@problem_id:3036527]

### Generalizations and Advanced Perspectives

The principles underlying the Reilly formula are remarkably robust and can be extended to more general contexts, providing powerful tools for studying weighted measures and nonlinear equations.

#### Weighted Reilly Formula and Bakry-Émery Theory
A significant generalization arises in the context of manifolds with a weighted measure, $d\mu = e^{-V} dV_g$, for some smooth potential function $V$. This setting is central to Bakry-Émery theory. The natural Laplacian in this context is the **drift Laplacian** (or Witten Laplacian), $\Delta_V f = \Delta f - g(\nabla V, \nabla f)$, which is self-adjoint with respect to the weighted measure $d\mu$.

The entire Bochner-Reilly machinery can be adapted to this operator. The role of the Ricci tensor is replaced by the **Bakry-Émery Ricci tensor**, $\mathrm{Ric}_V = \mathrm{Ric} + \nabla^2 V$. The derivation proceeds in parallel with the classical case, but uses the weighted divergence theorem. The final result is a **weighted Reilly formula** of the form:
$$ \int_\Omega \left( (\Delta_V f)^2 - |\nabla^2 f|^2 - \mathrm{Ric}_V(\nabla f, \nabla f) \right) d\mu = \int_{\partial \Omega} \mathcal{B}_V(f) e^{-V} dA_g $$
The boundary integrand $\mathcal{B}_V(f)$ has a structure that mirrors the classical case but incorporates the potential $V$. For instance, the [mean curvature](@entry_id:162147) term becomes $H_V (\partial_\nu f)^2$, where $H_V = H - \partial_\nu V$ is the **weighted mean curvature**. This framework is instrumental in proving sharp [geometric inequalities](@entry_id:197381) and has deep connections to [optimal transport](@entry_id:196008) and statistical mechanics. [@problem_id:3036539]

#### Quasilinear Extensions and the p-Laplacian
Extending these ideas to nonlinear operators, such as the **p-Laplacian** $\Delta_p u = \mathrm{div}(|\nabla u|^{p-2}\nabla u)$, presents significant challenges. The operator is quasilinear, meaning its linearization depends on the solution $u$ itself. This leads to two main difficulties: **anisotropy** (the operator's behavior depends on the direction of $\nabla u$) and **degeneracy** (the operator degenerates where $\nabla u = 0$).

A rigorous framework for a "$p$-Reilly formula" must address both issues. The key steps involve:
1.  **Linearization:** Analyze the linearized operator, which reveals an [anisotropic diffusion](@entry_id:151085) tensor $A_u = |\nabla u|^{p-2}(I + (p-2)\frac{\nabla u \otimes \nabla u}{|\nabla u|^2})$. This tensor captures the directional dependence.
2.  **Regularization:** Handle the degeneracy at the critical set $\{\nabla u = 0\}$ by introducing a [regularization parameter](@entry_id:162917) $\varepsilon > 0$, for instance, by replacing $|\nabla u|^2$ with $|\nabla u|^2+\varepsilon$.
3.  **Anisotropic Boundary Geometry:** Derive an identity for the regularized, anisotropic [linear operator](@entry_id:136520). The resulting boundary terms must be defined with respect to the anisotropic structure. This involves defining an **anisotropic [mean curvature](@entry_id:162147)** as a weighted trace of the shape operator, where the weighting is done by the [anisotropy tensor](@entry_id:746467) $A_u$.
4.  **Limiting Argument:** Pass to the limit as $\varepsilon \to 0$ to recover an identity for the original $p$-Laplacian.

This sophisticated program demonstrates that while the core principles of the Reilly formula are adaptable, their application to nonlinear settings requires a substantial increase in technical and conceptual machinery, pushing into the frontiers of modern geometric PDE theory. [@problem_id:3036540]