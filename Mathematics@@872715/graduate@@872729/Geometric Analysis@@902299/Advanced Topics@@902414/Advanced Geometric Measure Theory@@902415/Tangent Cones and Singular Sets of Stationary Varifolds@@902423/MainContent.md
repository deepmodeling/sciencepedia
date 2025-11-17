## Introduction
In the pursuit of understanding generalized minimal surfaces, [geometric measure theory](@entry_id:187987) provides a powerful framework that extends classical [differential geometry](@entry_id:145818) to accommodate objects with singularities. At the heart of this framework lie **[stationary varifolds](@entry_id:183360)**, which are measure-theoretic objects that serve as the weak formulation of [minimal surfaces](@entry_id:157732). While these generalized surfaces enjoy strong compactness properties, they can exhibit complex singular sets where the structure deviates from that of a [smooth manifold](@entry_id:156564). The central challenge, and the focus of this article, is to characterize these singularities and understand their geometric structure. How can we probe the infinitesimal behavior of a [varifold](@entry_id:194011) at a [singular point](@entry_id:171198), and what can this tell us about the size and nature of the overall [singular set](@entry_id:187696)?

This article addresses this fundamental problem by exploring the theory of [tangent cones](@entry_id:191609) and the structure of singular sets for [stationary varifolds](@entry_id:183360). Across three chapters, you will gain a comprehensive understanding of the core concepts and their applications.
*   The first chapter, **"Principles and Mechanisms,"** establishes the foundational theory. We will introduce [stationary varifolds](@entry_id:183360), derive the crucial [monotonicity formula](@entry_id:203421), and explain how the blow-up method leads to the concept of [tangent cones](@entry_id:191609). We will then use these tools to develop the [regularity theory](@entry_id:194071), including Allard's theorem, and analyze the dimensional bounds and stratification of the [singular set](@entry_id:187696).
*   Next, **"Applications and Interdisciplinary Connections"** will demonstrate the far-reaching impact of this theory. We will see how the abstract analysis of singularities provides concrete insights into physical phenomena like soap films, defects in materials, the celebrated Bernstein problem in PDEs, and the proof of the Positive Mass Theorem in general relativity.
*   Finally, **"Hands-On Practices"** will provide opportunities to apply these concepts to concrete problems, reinforcing the theoretical principles through guided calculations and analysis of key examples.

We begin our exploration by delving into the principles and mechanisms that govern the local structure of [stationary varifolds](@entry_id:183360), starting with their definition and the pivotal notion of [stationarity](@entry_id:143776).

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms that govern the structure of [stationary varifolds](@entry_id:183360), with a particular focus on the analysis of their singular sets. We will explore how the concept of stationarity leads to a powerful [monotonicity formula](@entry_id:203421), which in turn enables the use of [blow-up analysis](@entry_id:187686) to probe the infinitesimal structure of these generalized surfaces. This process yields [tangent cones](@entry_id:191609), whose geometric properties provide a deep and nuanced understanding of the dichotomy between regular and singular points, ultimately leading to a classification and dimensional bounding of the [singular set](@entry_id:187696) itself.

### The Nature of Stationary Varifolds

To analyze the singularities of generalized minimal surfaces, we must first establish a rigorous definition of these objects and the notion of minimality in a weak, measure-theoretic sense.

#### Definition of Varifolds

In classical [differential geometry](@entry_id:145818), a surface is a smooth manifold. However, to accommodate singularities and to work within a framework with strong compactness properties, [geometric measure theory](@entry_id:187987) employs a more general notion: the **[varifold](@entry_id:194011)**. A [varifold](@entry_id:194011) does not just represent a set of points in space; it also encodes the distribution of tangent planes at each point.

Formally, a **$k$-dimensional [varifold](@entry_id:194011)** $V$ in an open set $U \subseteq \mathbb{R}^n$ is a Radon measure on the product space $U \times G(n,k)$, where $G(n,k)$ is the **Grassmannian** of unoriented $k$-dimensional linear subspaces of $\mathbb{R}^n$. A point in this product space is a pair $(x, S)$, representing a location $x \in U$ and a potential tangent $k$-plane $S \in G(n,k)$. The [varifold](@entry_id:194011) $V$ assigns a "weight" to regions in this combined space of positions and planes.

From the [varifold](@entry_id:194011) $V$, we can recover the total "mass" or generalized area by integrating out the directional information. This is accomplished via the **weight measure** (or mass measure) of $V$, denoted $\|V\|$, which is a Radon measure on $U$. It is defined as the [pushforward](@entry_id:158718) of $V$ under the natural projection map $\pi: U \times G(n,k) \to U$ given by $\pi(x,S) = x$. Consequently, for any Borel set $A \subset U$, the mass of $V$ in $A$ is given by $\|V\|(A) = V(A \times G(n,k))$ [@problem_id:3033944]. This framework is powerful because it allows for objects with non-unique or rapidly oscillating tangent planes, which are represented by a non-trivial distribution of the measure $V$ over the $G(n,k)$ fiber for a fixed $x$.

An important subclass of [varifolds](@entry_id:199701) are **integral [varifolds](@entry_id:199701)**. For an integral [varifold](@entry_id:194011), the weight measure $\|V\|$ takes the form $\theta \mathcal{H}^k \llcorner M$, where $M$ is a countably $k$-rectifiable set, $\mathcal{H}^k$ is the $k$-dimensional Hausdorff measure, and $\theta: M \to \mathbb{N}$ is a locally $\mathcal{H}^k$-integrable positive integer-valued function called the **multiplicity**. The [varifold](@entry_id:194011) measure $V$ itself is then concentrated on pairs $(x, T_xM)$, where $T_xM$ is the unique approximate tangent plane to $M$ that exists for $\mathcal{H}^k$-almost every $x \in M$.

#### Stationarity and Generalized Mean Curvature

The concept of a minimal surface, one that locally minimizes area, is generalized to [varifolds](@entry_id:199701) through the notion of [stationarity](@entry_id:143776). A smooth $k$-dimensional [submanifold](@entry_id:262388) is minimal if its [mean curvature vector](@entry_id:199617) is zero everywhere. For a [varifold](@entry_id:194011), this condition is expressed in a weak form using the **[first variation of area](@entry_id:195526)**. The [first variation](@entry_id:174697) of a [varifold](@entry_id:194011) $V$, denoted $\delta V$, is a distribution that measures how the mass $\|V\|$ changes under infinitesimal deformations of the [ambient space](@entry_id:184743). Specifically, for any compactly supported smooth vector field $X$ on $U$, the [first variation](@entry_id:174697) is defined as
$$
\delta V(X) = \int_{U \times G(n,k)} \mathrm{div}_S X(x) \, dV(x,S),
$$
where $\mathrm{div}_S X(x)$ is the trace of the gradient of $X$ restricted to the plane $S$.

A [varifold](@entry_id:194011) $V$ is said to be **stationary** if its [first variation](@entry_id:174697) is identically zero, i.e., $\delta V(X) = 0$ for all such test vector fields $X$. This condition is the weak or distributional formulation of having zero mean curvature. When the [first variation](@entry_id:174697) $\delta V$ can be represented by integration against a vector-valued function $H_V \in L^1_{\mathrm{loc}}(\|V\|; \mathbb{R}^n)$, this function is called the **[generalized mean curvature](@entry_id:199614)** vector of $V$. The relationship is typically expressed as $\delta V(X) = -\int_U \langle H_V(x), X(x) \rangle \, d\|V\|(x)$. From this representation, it is clear that a [varifold](@entry_id:194011) $V$ for which $H_V$ exists is stationary if and only if its [generalized mean curvature](@entry_id:199614) vanishes [almost everywhere](@entry_id:146631) with respect to its own weight measure, i.e., $H_V = 0$ $\|V\|$-a.e. [@problem_id:3033942]. Stationary [varifolds](@entry_id:199701) are thus the natural generalization of classical [minimal submanifolds](@entry_id:204492) to a setting that allows for singularities.

#### The Hierarchy of Minimal Surfaces: Stationarity, Stability, and Area-Minimization

Stationarity is the most general notion of minimality. There exist more restrictive, and thus more regular, classes of "minimal" objects. Understanding this hierarchy is crucial for appreciating the specific challenges and results associated with [stationary varifolds](@entry_id:183360).

1.  **Stationary Varifolds**: As defined, these are [critical points](@entry_id:144653) of the [area functional](@entry_id:635965) ($\delta V = 0$). This is a [first-order condition](@entry_id:140702). A simple example that is stationary but not a smooth manifold is the union of three half-planes in $\mathbb{R}^3$ meeting at $120^\circ$ angles along a common line.

2.  **Stable Minimal Hypersurfaces**: For a [stationary varifold](@entry_id:188378), one can consider the [second variation of area](@entry_id:187529). A [stationary varifold](@entry_id:188378) is **stable** if its [second variation of area](@entry_id:187529) is non-negative for all compactly supported deformations. This is a second-order condition, implying that the [varifold](@entry_id:194011) is a [local minimum](@entry_id:143537) of area with respect to small perturbations.

3.  **Area-Minimizing Currents**: The strongest condition is that of being **area-minimizing**. This typically applies to a more structured object, an **integral current** $T$ (an oriented analogue of an integral [varifold](@entry_id:194011)). A current $T$ is area-minimizing if its mass is less than or equal to the mass of any other current $T'$ with the same boundary, i.e., $\partial T' = \partial T$.

These classes are strictly nested:
$$
\text{Area-Minimizing} \implies \text{Stable} \implies \text{Stationary}
$$
The reverse implications do not hold. For example, a catenoid is a classical minimal surface (stationary and stable) but is not area-minimizing on a global scale. As we will see, the regularity properties of these objects become progressively stronger as we move up this hierarchy. Much of the theory of [stationary varifolds](@entry_id:183360) is dedicated to understanding what can be said with only the weakest of these assumptions. [@problem_id:3033956]

### The Blow-Up Method: Uncovering Local Structure

The central strategy for analyzing the behavior of a [stationary varifold](@entry_id:188378) $V$ near a point $x_0$ is the **blow-up method**. This technique is analogous to zooming in with a microscope of infinite power. By examining the structure that emerges in the limit, we can classify the point $x_0$ as regular or singular and characterize the nature of the singularity.

#### The Monotonicity Formula and Density

The engine that drives the blow-up method is the **[monotonicity formula](@entry_id:203421)**, a fundamental consequence of [stationarity](@entry_id:143776). For a stationary $k$-[varifold](@entry_id:194011) $V$ in $\mathbb{R}^n$, we define the **scale-dependent density function** at a point $x \in \mathbb{R}^n$ and radius $r>0$ as the ratio of the [varifold](@entry_id:194011)'s mass in the ball $B_r(x)$ to the volume of a standard $k$-dimensional ball of the same radius:
$$
\Theta^k(\|V\|, x, r) = \frac{\|V\|(B_r(x))}{\omega_k r^k},
$$
where $\omega_k$ is the volume of the unit ball in $\mathbb{R}^k$.

The [monotonicity formula](@entry_id:203421) states that for any [stationary varifold](@entry_id:188378) $V$, the function $r \mapsto \Theta^k(\|V\|, x, r)$ is **non-decreasing** for $r > 0$. More precisely, for any $0  \sigma  \rho$, we have:
$$
\frac{\|V\|(B_\rho(x))}{\omega_k \rho^k} - \frac{\|V\|(B_\sigma(x))}{\omega_k \sigma^k} = \frac{1}{\omega_k} \int_{B_\rho(x) \setminus B_\sigma(x)} \frac{|(y-x)^\perp|^2}{|y-x|^{k+2}} \, d\|V\|(y)
$$
where $(y-x)^\perp$ is the component of the vector $y-x$ that is orthogonal to the approximate [tangent space](@entry_id:141028) of $V$ at $y$ [@problem_id:3033945]. Since the integrand on the right-hand side is non-negative, the formula immediately implies that the density function is non-decreasing.

A crucial consequence of this monotonicity is that the limit as $r \to 0$ must exist. This limit is called the **density** of $V$ at $x$:
$$
\Theta^k(\|V\|, x) = \lim_{r \to 0^+} \Theta^k(\|V\|, x, r).
$$
This density is a fundamental invariant of the [varifold](@entry_id:194011) at the point $x$. For example, if $V$ corresponds to a smooth $k$-dimensional [minimal submanifold](@entry_id:200568) with multiplicity $\theta$, its density at any point on the [submanifold](@entry_id:262388) is exactly $\theta$. At a [singular point](@entry_id:171198), the density can be non-integer and reflects the geometric complexity of the singularity.

#### Existence of Tangent Cones: Compactness and Blow-Ups

The blow-up procedure is formalized by considering a sequence of rescaled [varifolds](@entry_id:199701). For a point $x_0$ and a sequence of radii $r_i \to 0$, we define the **blow-up sequence** of [varifolds](@entry_id:199701) $(V_i)$ by pushing forward $V$ under the dilation maps $\eta_{x_0, r_i}(y) = (y - x_0)/r_i$. The resulting [varifold](@entry_id:194011) is $V_i = (\eta_{x_0, r_i})_\# V$.

The [monotonicity formula](@entry_id:203421) is precisely what guarantees that this sequence has a well-behaved limit. The formula implies that the density $\Theta^k(\|V\|, x_0, r)$ is bounded for $r$ in any compact interval of $(0, \infty)$. This provides a uniform local mass bound on the rescaled [varifolds](@entry_id:199701) $V_i$. This mass bound is the key hypothesis for **Allard's Compactness Theorem**, which states that a sequence of $m$-[varifolds](@entry_id:199701) $(V_i)$ in an open set $U$, satisfying uniform bounds on their local mass ($\sup_i \|V_i\|(K)  \infty$) and on their [first variation](@entry_id:174697) ($\sup_i |\delta V_i|(K)  \infty$) for all compact $K \subset U$, has a subsequence that converges to a limit [varifold](@entry_id:194011) $V$.

For a [stationary varifold](@entry_id:188378), the [first variation](@entry_id:174697) is zero, so the second condition is trivially satisfied. The [monotonicity formula](@entry_id:203421) provides the first condition. Therefore, for any sequence of radii $r_i \to 0$, the blow-up sequence $(V_i)$ has at least one convergent subsequence. Any such limit is called a **[tangent cone](@entry_id:159686)** to $V$ at $x_0$ [@problem_id:3033950]. The set of all possible [tangent cones](@entry_id:191609) at $x_0$ is denoted $\mathrm{Tan}(V, x_0)$.

#### Fundamental Properties of Tangent Cones

Tangent cones inherit fundamental properties from the original [stationary varifold](@entry_id:188378).
1.  **Stationarity**: The property of being stationary is preserved under the blow-up limit. Thus, every tangent cone is itself a [stationary varifold](@entry_id:188378) [@problem_id:3033942].
2.  **Conical Structure**: A [tangent cone](@entry_id:159686) is always a **cone**. This means it is invariant under dilations from the origin; if $C$ is a [tangent cone](@entry_id:159686), then for any $\lambda > 0$, the rescaled [varifold](@entry_id:194011) $(\eta_{0,\lambda})_\# C$ is equal to $C$. Its support is a geometric cone with its vertex at the origin. This property arises because the blow-up process "forgets" the original scale [@problem_id:3033932].

The weight measure of a tangent [varifold](@entry_id:194011), $\|C\|$, is a **tangent measure** to the original weight measure $\|V\|$ at $x_0$. This means $\|C\|$ is a weak limit of rescaled measures $c_j (\eta_{x_0, r_j})_\# \|V\|$ for suitable normalization constants $c_j$. The existence of a finite, positive density $\Theta^k(\|V\|, x_0)$ ensures that we can choose $c_j = (\omega_k r_j^k)^{-1}$ to obtain a non-zero limit measure [@problem_id:3033932]. In summary, blowing up a [stationary varifold](@entry_id:188378) at a point yields a stationary cone, which represents the infinitesimal structure of the [varifold](@entry_id:194011) at that point.

### The Regularity Theory

With the tool of [tangent cones](@entry_id:191609), we can now precisely define and analyze the regular and singular parts of a [stationary varifold](@entry_id:188378).

#### The Regular and Singular Sets

The support of a [stationary varifold](@entry_id:188378) can be partitioned into two sets: the regular set and the [singular set](@entry_id:187696).
-   The **regular set**, denoted $\operatorname{Reg}(V)$, consists of all points $x_0 \in \mathrm{spt}\|V\|$ where the [varifold](@entry_id:194011) is locally a smooth [minimal surface](@entry_id:267317). More precisely, $x_0 \in \operatorname{Reg}(V)$ if there exists a radius $r>0$ such that $\mathrm{spt}\|V\| \cap B_r(x_0)$ is a smooth, $m$-dimensional $C^{1,\alpha}$ [embedded submanifold](@entry_id:273162), and the [varifold](@entry_id:194011) measure restricted to this ball is simply this submanifold counted with a constant integer [multiplicity](@entry_id:136466) [@problem_id:3033940]. At such a point, the tangent cone is unique and is the $m$-dimensional [tangent plane](@entry_id:136914) to the manifold, counted with the same multiplicity.
-   The **[singular set](@entry_id:187696)**, $\operatorname{Sing}(V)$, is simply the complement of the regular set within the support: $\operatorname{Sing}(V) = \mathrm{spt}\|V\| \setminus \operatorname{Reg}(V)$. These are the points where the [varifold](@entry_id:194011) fails to be a smooth manifold locally.

#### Allard's Regularity Theorem: The Mechanism of Smoothness

The primary tool for proving a point is regular is **Allard's Regularity Theorem**. This is a quantitative result that provides an explicit criterion for smoothness. It states that if an integral [varifold](@entry_id:194011) $V$ is "almost flat" in a ball, then it must be a smooth graph. "Almost flat" means three conditions are met for a small constant $\varepsilon > 0$:
1.  **Mass-flatness**: The mass is close to that of a single disk, e.g., $\|V\|(B_r(x_0)) \le (1+\varepsilon)\omega_m r^m$.
2.  **Tilt-flatness**: The [varifold](@entry_id:194011) is geometrically close to a reference plane $P$, as measured by a small **[tilt-excess](@entry_id:194845)**.
3.  **Mean Curvature-flatness**: The [generalized mean curvature](@entry_id:199614) $H_V$ is small in a [scale-invariant](@entry_id:178566) $L^p$ norm (for $p > m$).

If these conditions hold, Allard's theorem guarantees that in a smaller, concentric ball, the support of $V$ is the graph of a $C^{1,\alpha}$ function over the reference plane $P$, where the exponent $\alpha = 1-m/p$. The theorem even provides a quantitative estimate for the $C^{1,\alpha}$ norm of this function in terms of the excess and [mean curvature](@entry_id:162147) norms [@problem_id:3033962]. For a [stationary varifold](@entry_id:188378), the [mean curvature](@entry_id:162147) term is zero, simplifying the hypotheses. This theorem is the engine of regularity: it translates geometric proximity to a plane into analytic smoothness.

#### Almost-Everywhere Regularity and Higher Codimension Branching

A direct consequence of Allard's regularity theorem and the [monotonicity formula](@entry_id:203421) is **Allard's almost-everywhere regularity theorem**. It states that for any stationary integral $m$-[varifold](@entry_id:194011) $V$, the [singular set](@entry_id:187696) has zero measure with respect to the [varifold](@entry_id:194011)'s own weight measure: $\|V\|(\operatorname{Sing}(V)) = 0$ [@problem_id:3033940]. This is a profound result: while singularities can exist, they are "small" in a measure-theoretic sense. The [varifold](@entry_id:194011) is regular "[almost everywhere](@entry_id:146631)".

However, the picture is more subtle than a simple dichotomy between smooth points and transverse intersections. Especially in [codimension](@entry_id:273141) greater than one (when $n-k \ge 2$), [stationary varifolds](@entry_id:183360) can exhibit **branching**. A branch point is a singularity where the [tangent cone](@entry_id:159686) is a single plane, but with an integer multiplicity $q \ge 2$. While the infinitesimal structure is a plane, the local structure is not a single smooth sheet but rather $q$ sheets that come together.

A classic example is the surface in $\mathbb{R}^4 \cong \mathbb{C}^2$ given by the [holomorphic map](@entry_id:264170) $F: \mathbb{C} \to \mathbb{C}^2$, $F(z) = (z^2, z^3)$. Since holomorphic maps produce minimal surfaces, the associated [varifold](@entry_id:194011) is stationary. At the origin $z=0$, the derivative vanishes, indicating a [branch point](@entry_id:169747). The [tangent cone](@entry_id:159686) at the origin can be shown to be the complex line $\{(w,0) \mid w \in \mathbb{C}\}$ counted with multiplicity 2. Near the origin, the surface is not a single $C^1$ graph, demonstrating that the regularity conclusion of Allard's theorem (in its single-sheeted graphical form) fails despite the [tangent cone](@entry_id:159686) being a plane [@problem_id:3033939]. This shows that even if the tangent cone is a plane, its multiplicity matters greatly.

### The Structure of the Singular Set

Given that singularities can and do exist, the final frontier is to understand their structure. This involves asking about the uniqueness of [tangent cones](@entry_id:191609) and the size (e.g., Hausdorff dimension) of the [singular set](@entry_id:187696).

#### Uniqueness of Tangent Cones

While the [compactness theorem](@entry_id:148512) guarantees the *existence* of [tangent cones](@entry_id:191609) along subsequences of radii, it does not guarantee that the limit is independent of the chosen subsequence. At a "well-behaved" point, we expect a unique [tangent cone](@entry_id:159686). At more complex singularities, the [varifold](@entry_id:194011) might oscillate between different conical structures at different scales, leading to multiple possible [tangent cones](@entry_id:191609).

Uniqueness can be guaranteed by imposing stronger conditions on how the [varifold](@entry_id:194011) approaches its infinitesimal limit. Two celebrated criteria for uniqueness are:
1.  **Hölder Decay of Tilt-Excess**: If the [tilt-excess](@entry_id:194845) $E(r)$ (a measure of how far the [varifold](@entry_id:194011) deviates from the best-fitting plane at scale $r$) decays at a Hölder rate, i.e., $E(r) \le C r^{2\alpha}$ for some $\alpha > 0$, then the tangent cone is unique and must be a plane. The proof relies on showing that the sequence of best-fitting planes at dyadically shrinking scales forms a Cauchy sequence in the Grassmannian, forcing convergence to a unique limiting plane [@problem_id:3033946].
2.  **Dini Convergence of Frequency**: In settings where an Almgren-Weiss frequency function $N(r)$ can be defined, this function is monotonic. The limit $\lambda = \lim_{r \to 0} N(r)$ gives the degree of homogeneity of any [tangent cone](@entry_id:159686). If the convergence is fast enough to satisfy a Dini condition, $\int_0^{r_0} \frac{N(r)-\lambda}{r} \, dr  \infty$, then the family of rescaled [varifolds](@entry_id:199701) is a Cauchy family, which again implies the existence of a unique [tangent cone](@entry_id:159686) [@problem_id:3033946].

#### Stratification by Symmetry: The $\mathcal{S}^j$ Strata

A powerful method for organizing the [singular set](@entry_id:187696) is to stratify it based on the symmetries of the [tangent cones](@entry_id:191609). A key measure of a cone's symmetry is the dimension of its **lineality space** (or **spine**), which is the maximal linear subspace $L$ such that the cone can be written as a product $C = L \times C'$, where $C'$ is a cone in the orthogonal complement $L^\perp$. The dimension of $L$ is the number of directions in which the cone is translationally invariant. For a $k$-plane, the lineality space is the plane itself, so its dimension is $k$. For a "truly conical" cone with a unique vertex, the dimension is 0.

The **$j$-th stratum of the [singular set](@entry_id:187696)**, $\mathcal{S}^j(V)$, is defined as the set of points $x \in \mathrm{spt}\|V\|$ such that *every* tangent cone at $x$ has a lineality space of dimension at most $j$:
$$
\mathcal{S}^j(V) = \{ x \in \mathrm{spt}\|V\| \mid \forall C \in \mathrm{Tan}(V,x), \, \dim L(C) \le j \}.
$$
By this definition, if a point $x$ belongs to $\mathcal{S}^j(V)$, its [tangent cones](@entry_id:191609) cannot have more than $j$ flat directions. This immediately implies a nested inclusion of closed sets:
$$
\mathcal{S}^0(V) \subset \mathcal{S}^1(V) \subset \dots \subset \mathcal{S}^{k-1}(V).
$$
This holds simply because the condition $\dim L(C) \le j$ implies $\dim L(C) \le j+1$ [@problem_id:3033936]. The set $\mathcal{S}^{k-1}(V)$ contains the entire [singular set](@entry_id:187696), because a regular point has a tangent $k$-plane as its unique tangent cone, for which $\dim L(C) = k$, thus violating the condition for being in $\mathcal{S}^{k-1}(V)$.

#### Dimensional Bounds on the Singular Set

The stratification of the [singular set](@entry_id:187696) is not merely a notational exercise; it leads to concrete geometric information. The seminal result in this direction is **Federer's Dimension Reduction Principle**, which provides an upper bound on the Hausdorff dimension of each stratum:
$$
\dim_{\mathcal{H}} \mathcal{S}^j(V) \le j.
$$
This remarkable inductive result asserts that the set of points whose [tangent cones](@entry_id:191609) have at most $j$ directions of symmetry can itself have a Hausdorff dimension of at most $j$ [@problem_id:3033933]. A direct consequence is that for a stationary integral $k$-[varifold](@entry_id:194011) in $\mathbb{R}^{k+1}$ (the hypersurface case), the entire [singular set](@entry_id:187696) has dimension at most $k-1$, since $\operatorname{Sing}(V) \subset \mathcal{S}^{k-1}(V)$.

For the more restrictive classes of area-minimizing or stable [minimal hypersurfaces](@entry_id:188002) in $\mathbb{R}^{k+1}$, the [regularity theory](@entry_id:194071) is dramatically stronger. A landmark result states that for such [hypersurfaces](@entry_id:159491), the [singular set](@entry_id:187696) is much smaller:
$$
\dim_{\mathcal{H}} \operatorname{Sing}(V) \le k-7.
$$
This deep theorem implies complete regularity for low dimensions:
-   If $k \le 6$, an area-minimizing hypersurface in $\mathbb{R}^{k+1}$ must be entirely smooth ($\operatorname{Sing}(V) = \emptyset$).
-   If $k=7$, singularities can exist, but they must be isolated points (a set of Hausdorff dimension 0). The first example of such a singularity is provided by the celebrated Simons cone in $\mathbb{R}^8$ [@problem_id:3033933].

This sharp dimensional bound highlights the profound impact that stronger variational assumptions (stability and area-minimization) have on taming the possible singularities of generalized [minimal surfaces](@entry_id:157732).