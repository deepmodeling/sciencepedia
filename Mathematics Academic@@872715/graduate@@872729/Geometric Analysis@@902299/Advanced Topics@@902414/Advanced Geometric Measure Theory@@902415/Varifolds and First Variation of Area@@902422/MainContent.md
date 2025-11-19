## Introduction
In the quest to find and understand surfaces that minimize area, a central problem in geometric analysis, classical [differential geometry](@entry_id:145818) often falls short. The smooth manifolds it describes cannot account for the singularities that naturally arise when taking limits of area-minimizing sequences, such as the junctions in a soap film network. To bridge this gap, the theory of [varifolds](@entry_id:199701) provides a powerful and comprehensive framework for studying generalized surfaces, complete with their potential irregularities. This article serves as an introduction to this essential tool of modern [geometric measure theory](@entry_id:187987).

This article is structured to build your understanding from the ground up. In the "Principles and Mechanisms" chapter, we will rigorously define [varifolds](@entry_id:199701), explore the [first variation of area](@entry_id:195526), and introduce the fundamental theorems of compactness and regularity that give the theory its analytical power. Following this, the "Applications and Interdisciplinary Connections" chapter will demonstrate how these abstract principles are applied to solve concrete problems, from analyzing the structure of [minimal surfaces](@entry_id:157732) and their singularities to modeling physical phenomena and [geometric flows](@entry_id:198994). Finally, the "Hands-On Practices" section provides targeted exercises to solidify your grasp of the core computational and conceptual mechanics. By the end, you will have a solid foundation in the theory of [varifolds](@entry_id:199701) and its role in solving [variational problems](@entry_id:756445) in geometry and beyond.

## Principles and Mechanisms

In this chapter, we delve into the formal principles and mechanisms that govern the theory of [varifolds](@entry_id:199701). We begin by constructing the definition of a [varifold](@entry_id:194011) from first principles, emphasizing its role as a generalization of the concept of a surface. We then explore the central analytical tool of the theory: the [first variation of area](@entry_id:195526). This leads to the notion of [stationary varifolds](@entry_id:183360), which are [weak solutions](@entry_id:161732) to the area minimization problem. Finally, we will introduce the foundational theorems of compactness, [rectifiability](@entry_id:202091), and regularity, which constitute the core power of this framework for solving problems in [geometric analysis](@entry_id:157700).

### The Varifold as a Generalized Surface

The classical theory of submanifolds provides a robust framework for studying smooth surfaces. However, when dealing with [variational problems](@entry_id:756445), such as finding surfaces that minimize area, one often encounters sequences of smooth surfaces that converge to an object with singularities. The theory of [varifolds](@entry_id:199701), developed by Frederick J. Almgren Jr., provides a powerful extension of the concept of a surface that is perfectly suited to handle such limits and singularities.

#### The Unoriented Nature of Area

The foundational insight motivating the structure of [varifolds](@entry_id:199701) is that the area of a surface is an inherently unoriented quantity. The area of a parametrized $k$-dimensional surface in $\mathbb{R}^n$ depends on the magnitude of the Jacobian, typically through an integral involving a term like $\sqrt{\det(Df^T Df)}$, which is invariant under changes of orientation. This is in stark contrast to objects like **[integral currents](@entry_id:201630)**, which are designed to generalize oriented [submanifolds](@entry_id:159439) and preserve a version of Stokes's theorem. An integral current changes sign if its orientation is reversed. Consequently, the sum of two currents with opposite orientations can result in cancellation, leading to a zero current even if the underlying surfaces do not disappear [@problem_id:3036972].

Varifolds, by design, do not encode orientation. The "superposition" of a [varifold](@entry_id:194011) with itself results in a new [varifold](@entry_id:194011) with double the mass (or multiplicity), reflecting the geometric reality of two surfaces lying on top of one another. This non-cancellation property is crucial for the existence theory of area-minimizing surfaces [@problem_id:3036972].

To formalize this unoriented nature, we must describe the [tangent space](@entry_id:141028) at each point as an unoriented object. This is accomplished using the **Grassmannian manifold**, denoted $G(n,k)$, which is the space of all $k$-dimensional linear subspaces of $\mathbb{R}^n$. Each point in $G(n,k)$ represents a $k$-plane passing through the origin, without a specified orientation. This is the correct space for [varifold](@entry_id:194011) theory because, as we will see, the [first variation of area](@entry_id:195526) also depends only on the unoriented [tangent plane](@entry_id:136914), not on a choice of orientation. In contrast, theories of oriented surfaces and currents utilize the oriented Grassmannian $\widetilde{G}(n,k)$, which is the two-sheeted [covering space](@entry_id:139261) of $G(n,k)$ [@problem_id:3037023].

#### The Formal Definition of a Varifold

With this background, we can state the formal definition. A **$k$-[varifold](@entry_id:194011)** $V$ in $\mathbb{R}^n$ is a Radon measure on the [product space](@entry_id:151533) $\mathbb{R}^n \times G(n,k)$.

Intuitively, a [varifold](@entry_id:194011) $V$ describes a generalized $k$-dimensional surface by specifying, at each point $x \in \mathbb{R}^n$, a distribution of tangent $k$-planes and an associated mass for each. The total space $\mathbb{R}^n \times G(n,k)$ provides the necessary structure to locate a piece of surface in space (the $\mathbb{R}^n$ factor) and describe its orientation-free tangent plane (the $G(n,k)$ factor).

Associated with any [varifold](@entry_id:194011) $V$ is its **weight measure** (or mass measure), denoted $\mu_V$, which is a Radon measure on $\mathbb{R}^n$. It is defined as the [pushforward](@entry_id:158718) of the measure $V$ under the projection map $\pi: \mathbb{R}^n \times G(n,k) \to \mathbb{R}^n$ where $\pi(x,S) = x$. For any Borel set $A \subset \mathbb{R}^n$, its weight is given by:
$$
\mu_V(A) = V(A \times G(n,k))
$$
Since $V$ is a Radon measure and the projection $\pi$ is continuous, $\mu_V$ is also a Radon measure on $\mathbb{R}^n$. The change of variables formula for this [pushforward measure](@entry_id:201640) is fundamental: for any bounded Borel function $f: \mathbb{R}^n \to \mathbb{R}$, we have
$$
\int_{\mathbb{R}^n} f(x) \, d\mu_V(x) = \int_{\mathbb{R}^n \times G(n,k)} f(\pi(x,S)) \, dV(x,S) = \int_{\mathbb{R}^n \times G(n,k)} f(x) \, dV(x,S)
$$
This relationship allows us to move between integrals over the base space $\mathbb{R}^n$ and integrals over the full [varifold](@entry_id:194011) space $\mathbb{R}^n \times G(n,k)$ [@problem_id:3037016].

### Rectifiable and Integral Varifolds

The definition of a [varifold](@entry_id:194011) as a Radon measure is very general. A crucial subclass consists of [varifolds](@entry_id:199701) that correspond to our geometric intuition of surfaces, which may have singularities but are fundamentally $k$-dimensional.

A set $S \subset \mathbb{R}^n$ is **countably $k$-rectifiable** if it can be covered, up to a set of $k$-dimensional Hausdorff [measure zero](@entry_id:137864), by the images of countably many Lipschitz (or $C^1$) maps from $\mathbb{R}^k$ to $\mathbb{R}^n$. Such sets possess an **approximate [tangent plane](@entry_id:136914)** $T_x S \in G(n,k)$ for $\mathcal{H}^k$-almost every point $x \in S$, where $\mathcal{H}^k$ is the $k$-dimensional Hausdorff measure.

A $k$-[varifold](@entry_id:194011) $V$ is said to be **rectifiable** if it can be represented by a pair $(S, \theta)$, where $S$ is a countably $k$-rectifiable set and $\theta: S \to [0, \infty)$ is a [locally integrable function](@entry_id:175678) called the **multiplicity function**. The correspondence is given by the formula:
$$
\int_{\mathbb{R}^n \times G(n,k)} \varphi(x,P) \, dV(x,P) = \int_S \varphi(x, T_x S) \, \theta(x) \, d\mathcal{H}^k(x)
$$
for every continuous function $\varphi$ with [compact support](@entry_id:276214) on $\mathbb{R}^n \times G(n,k)$ [@problem_id:3036991]. This means that a rectifiable [varifold](@entry_id:194011) is entirely determined by a geometric set $S$, a density $\theta$ on that set, and the geometrically defined tangent planes of $S$. Its weight measure is simply $\mu_V = \theta \mathcal{H}^k \llcorner S$, the Hausdorff measure on $S$ weighted by the [multiplicity](@entry_id:136466) function. It is important to note that the converse is not true; a [varifold](@entry_id:194011) whose weight measure has this form is not necessarily rectifiable, as the measure on $G(n,k)$ might not be concentrated on the approximate tangent planes [@problem_id:3036991].

An **integral [varifold](@entry_id:194011)** is a rectifiable [varifold](@entry_id:194011) whose [multiplicity](@entry_id:136466) function $\theta(x)$ takes values in the positive integers $\mathbb{N} = \{1, 2, 3, \dots\}$ for $\mathcal{H}^k$-almost every $x \in S$ [@problem_id:3036991]. These are the [varifolds](@entry_id:199701) that arise as limits of sums of classical submanifolds.

### The First Variation of Area and Stationarity

The central analytical tool in [varifold](@entry_id:194011) theory is the [first variation of area](@entry_id:195526), which generalizes the notion of the gradient of the [area functional](@entry_id:635965). It measures how the total mass of a [varifold](@entry_id:194011) changes under an infinitesimal deformation of the [ambient space](@entry_id:184743).

#### The First Variation Formula

Let $X \in C_c^1(\mathbb{R}^n; \mathbb{R}^n)$ be a smooth vector field with [compact support](@entry_id:276214). This vector field generates a flow $\Phi_t: \mathbb{R}^n \to \mathbb{R}^n$. The [first variation](@entry_id:174697) of a [varifold](@entry_id:194011) $V$ with respect to $X$, denoted $\delta V(X)$, is the rate of change of the mass of the deformed [varifold](@entry_id:194011) at time $t=0$. A fundamental calculation shows that this can be expressed as an integral over the [varifold](@entry_id:194011) itself:
$$
\delta V(X) = \int_{\mathbb{R}^n \times G(n,k)} \operatorname{div}_S X(x) \, dV(x,S)
$$
Here, $\operatorname{div}_S X(x)$ is the **tangential divergence** of the vector field $X$ along the $k$-plane $S$ at the point $x$. If $\{e_1, \dots, e_k\}$ is an [orthonormal basis](@entry_id:147779) for the plane $S$, the tangential divergence is given by the trace of the tangential part of the derivative of $X$:
$$
\operatorname{div}_S X(x) = \sum_{i=1}^k \langle D_xX(e_i), e_i \rangle
$$
It is crucial to distinguish this from the ambient divergence $\operatorname{div} X(x) = \sum_{j=1}^n \langle D_xX(f_j), f_j \rangle$ (for an orthonormal basis $\{f_j\}$ of $\mathbb{R}^n$), which involves derivatives in all directions. The [first variation](@entry_id:174697) formula exclusively uses the tangential divergence, reinforcing the principle that variations of area depend only on the tangential components of the deformation [@problem_id:3037016] [@problem_id:3036976].

For a rectifiable [varifold](@entry_id:194011) $V = v(S, \theta)$, this definition simplifies to a more concrete integral over the rectifiable set $S$:
$$
\delta V(X) = \int_S \operatorname{div}_{T_x S} X(x) \, \theta(x) \, d\mathcal{H}^k(x)
$$
where $T_x S$ is the approximate [tangent plane](@entry_id:136914) to $S$ at $x$ [@problem_id:3036991].

#### Generalized Mean Curvature

The [first variation](@entry_id:174697) formula can be transformed using [integration by parts](@entry_id:136350), which reveals its connection to [mean curvature](@entry_id:162147). For a smooth, weighted $m$-dimensional manifold $M$ with boundary $\partial M$ and weight function $w$, the [first variation](@entry_id:174697) of the associated [varifold](@entry_id:194011) $V_w$ is [@problem_id:3037021]:
$$
\delta V_w(X) = \int_M w \, \mathrm{div}_M X \, d\mathcal{H}^m = - \int_M \langle X, w H + \nabla^M w \rangle \, d\mathcal{H}^m + \int_{\partial M} \langle X, w \nu \rangle \, d\mathcal{H}^{m-1}
$$
where $H$ is the [mean curvature vector](@entry_id:199617) of $M$, $\nabla^M w$ is the tangential gradient of the weight function, and $\nu$ is the outward-pointing unit co-[normal vector field](@entry_id:268853) along the boundary $\partial M$. This formula shows that the [first variation](@entry_id:174697) is determined by an interior term involving mean curvature and a boundary term.

This motivates the definition of [mean curvature](@entry_id:162147) for general [varifolds](@entry_id:199701). A [varifold](@entry_id:194011) $V$ has **locally bounded [first variation](@entry_id:174697)** if the distribution $\delta V$ can be represented by a vector-valued Radon measure on $\mathbb{R}^n$. If this measure $\delta V$ is also absolutely continuous with respect to the weight measure $\mu_V$ (denoted $\delta V \ll \mu_V$), the Radon-Nikodym theorem guarantees the existence of a $\mu_V$-locally integrable vector field $H_V: \mathbb{R}^n \to \mathbb{R}^n$ such that:
$$
\delta V(X) = - \int_{\mathbb{R}^n} \langle X(x), H_V(x) \rangle \, d\mu_V(x)
$$
The vector field $H_V$ is called the **[generalized mean curvature](@entry_id:199614) vector** of the [varifold](@entry_id:194011) $V$. It is defined $\mu_V$-almost everywhere and is unique up to modification on sets of $\mu_V$-measure zero. The negative sign is a convention that makes $H_V$ coincide with the classical [mean curvature vector](@entry_id:199617) for smooth [hypersurfaces](@entry_id:159491) [@problem_id:3037015] [@problem_id:3036976].

#### Stationary Varifolds and Minimal Surfaces

A [varifold](@entry_id:194011) $V$ is called **stationary** if its [first variation](@entry_id:174697) is zero for all compactly supported [vector fields](@entry_id:161384) $X$, i.e., $\delta V(X) = 0$. This condition signifies that the [varifold](@entry_id:194011) is a critical point of the [area functional](@entry_id:635965).

From the definition of the [generalized mean curvature](@entry_id:199614) vector, it is clear that if a [varifold](@entry_id:194011) has a [mean curvature vector](@entry_id:199617) $H_V$, it is stationary if and only if $H_V = 0$ for $\mu_V$-almost every point [@problem_id:3036976]. Stationary [varifolds](@entry_id:199701) are thus the natural weak formulation of **[minimal surfaces](@entry_id:157732)** (surfaces with zero mean curvature).

This connection is particularly clear and important for graphical surfaces. Let $\Omega \subset \mathbb{R}^n$ be an open domain and consider the [graph of a function](@entry_id:159270) $u: \Omega \to \mathbb{R}$. The [varifold](@entry_id:194011) $V$ associated with this graph is stationary if and only if $u$ is a [weak solution](@entry_id:146017) to the **[minimal surface equation](@entry_id:187309)**:
$$
\operatorname{div}\left(\frac{Du}{\sqrt{1+|Du|^{2}}}\right) = 0
$$
For a function of low regularity, e.g., $u \in W^{1,1}_{\text{loc}}(\Omega)$, this is understood in the weak sense, meaning that for all [test functions](@entry_id:166589) $\varphi \in C_c^1(\Omega)$:
$$
\int_{\Omega} \frac{\langle Du(x), D\varphi(x) \rangle}{\sqrt{1+|Du(x)|^2}} \, dx = 0
$$
The theory of [stationary varifolds](@entry_id:183360) provides the ideal framework for studying [existence and regularity](@entry_id:635920) of solutions to this highly non-linear [partial differential equation](@entry_id:141332) [@problem_id:3036976].

### Fundamental Theorems

The utility of [varifold](@entry_id:194011) theory stems from a collection of powerful theorems concerning the convergence, structure, and regularity of [varifolds](@entry_id:199701). These results, primarily due to Almgren and William K. Allard, allow one to deduce strong geometric properties from relatively weak analytic assumptions.

#### Convergence and Compactness

A sequence of [varifolds](@entry_id:199701) $\{V_i\}$ **converges weakly** to a [varifold](@entry_id:194011) $V$, written $V_i \rightharpoonup V$, if they converge as Radon measures on $\mathbb{R}^n \times G(n,k)$. That is, for every $\varphi \in C_c^0(\mathbb{R}^n \times G(n,k))$, we have $\int \varphi \, dV_i \to \int \varphi \, dV$ [@problem_id:3037022].

This mode of convergence has several important properties:
1.  **Continuity of First Variation**: If $V_i \rightharpoonup V$, then $\delta V_i(X) \to \delta V(X)$ for every [test vector](@entry_id:172985) field $X$. This follows because the function $(x,S) \mapsto \operatorname{div}_S X(x)$ is continuous with [compact support](@entry_id:276214) [@problem_id:3037022].
2.  **Lower Semicontinuity of First Variation Mass**: If $V_i \rightharpoonup V$ and the total mass of the first variations is uniformly bounded, i.e., $\sup_i \|\delta V_i\|(\mathbb{R}^n)  \infty$, then the limit [varifold](@entry_id:194011) $V$ also has bounded [first variation](@entry_id:174697), and its mass is bounded by the [limit inferior](@entry_id:145282) of the sequence: $\|\delta V\|(\mathbb{R}^n) \le \liminf_{i\to\infty} \|\delta V_i\|(\mathbb{R}^n)$ [@problem_id:3037022].

These properties are essential ingredients in **Allard's Compactness Theorem**, which states that any sequence of $k$-[rectifiable varifolds](@entry_id:634475) in $\mathbb{R}^n$ with uniformly bounded mass and uniformly bounded [first variation](@entry_id:174697) mass has a subsequence that converges weakly to a $k$-rectifiable [varifold](@entry_id:194011). This theorem guarantees the existence of solutions to [variational problems](@entry_id:756445) by allowing one to take limits of minimizing sequences.

#### Allard's Rectifiability Theorem

While [varifolds](@entry_id:199701) can be very general, many interesting [varifolds](@entry_id:199701) that arise in applications are, in fact, rectifiable. Allard's [rectifiability](@entry_id:202091) theorem gives a powerful criterion for when this is true. It states:

**Theorem (Allard's Rectifiability Theorem):** Let $V$ be a $k$-[varifold](@entry_id:194011) in $\mathbb{R}^n$. If $V$ has locally bounded [first variation](@entry_id:174697) and its weight measure $\mu_V$ has positive and finite $k$-dimensional density $\Theta^k(\mu_V, x)$ for $\mu_V$-almost every $x$, then $V$ is a $k$-rectifiable [varifold](@entry_id:194011).

Here, the density is defined as $\Theta^k(\mu,x) = \lim_{r \to 0} \frac{\mu(B_r(x))}{\omega_k r^k}$, where $\omega_k$ is the volume of the unit $k$-ball. The theorem's intuition is profound: if a generalized surface has a well-defined $k$-dimensional mass distribution at almost every point (the density condition) and is not infinitely "crinkled" (the bounded [first variation](@entry_id:174697) condition), then it must be composed of differentiable $k$-dimensional pieces [@problem_id:3036992].

#### Allard's Regularity Theorem

For a [varifold](@entry_id:194011) known to be rectifiable, one can ask a deeper question: is its support actually a [smooth manifold](@entry_id:156564)? Allard's regularity theorem provides a condition for this, establishing a bridge from the weak setting of [varifolds](@entry_id:199701) to the classical world of differential geometry. This is an $\varepsilon$-regularity result.

**Theorem (Allard's Regularity Theorem):** Let $V$ be an $m$-rectifiable [varifold](@entry_id:194011) in $B_\rho(x_0) \subset \mathbb{R}^n$. Assume its [generalized mean curvature](@entry_id:199614) $H_V$ belongs to $L^p(\mu_V)$ for some $p>m$. There exist constants $\varepsilon_0 > 0$ and $C  \infty$ depending only on $m, n, p$ such that if $V$ is sufficiently close to a flat plane $P$ in $B_\rho(x_0)$ in the sense that its [mass ratio](@entry_id:167674) is close to 1, its **[tilt-excess](@entry_id:194845)** is small, and its scale-invariant $L^p$ norm of $H_V$ is small, then the support of $V$ in a smaller ball $B_{\gamma \rho}(x_0)$ is the graph of a $C^{1,\alpha}$ function $u: P \to P^\perp$ with Hölder exponent $\alpha = 1-m/p$.

The **[tilt-excess](@entry_id:194845)** measures the average squared deviation of the [varifold](@entry_id:194011)'s tangent planes from the fixed plane $P$. The theorem essentially states that if a rectifiable [varifold](@entry_id:194011) with sufficiently integrable mean curvature is "almost flat" and "almost minimal" at a certain scale, then it is not just rectifiable but actually smooth ($C^{1,\alpha}$) in a slightly smaller region. This theorem is a cornerstone of the [regularity theory for minimal surfaces](@entry_id:183566) and other [variational problems](@entry_id:756445), as it provides a mechanism to prove that solutions are smooth away from a small [singular set](@entry_id:187696) [@problem_id:3037003].