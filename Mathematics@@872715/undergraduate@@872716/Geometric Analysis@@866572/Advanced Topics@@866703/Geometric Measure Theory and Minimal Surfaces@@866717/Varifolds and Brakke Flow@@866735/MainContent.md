## Introduction
Classical geometry struggles with surfaces that develop singularities, a common occurrence in [variational problems](@entry_id:756445) and geometric evolution. To analyze these complex shapes, which fall outside the scope of smooth manifold theory, a more robust and general framework is required. This article introduces the powerful tools of [geometric measure theory](@entry_id:187987)—specifically [varifolds](@entry_id:199701) and Brakke flow—to address this gap by representing surfaces as measures. In the following chapters, you will delve into the mathematical foundations of these concepts, explore their practical applications, and engage with hands-on examples. The "Principles and Mechanisms" chapter will construct the theory of [varifolds](@entry_id:199701) from the ground up and define Brakke flow as a [weak solution](@entry_id:146017) to [mean curvature flow](@entry_id:184231). Following this, the "Applications and Interdisciplinary Connections" chapter will demonstrate how these tools are used to solve the Plateau problem, analyze singularities, and connect to fields like materials science. Finally, "Hands-On Practices" will solidify your understanding through concrete problems designed to build intuition.

## Principles and Mechanisms

In this chapter, we transition from the introductory overview of generalized surfaces to the rigorous mathematical framework required for their analysis. We will construct the theory of [varifolds](@entry_id:199701), a cornerstone of [geometric measure theory](@entry_id:187987), which provides a powerful language to describe objects far more general than smooth [submanifolds](@entry_id:159439). Subsequently, we will explore their variational properties, leading to a generalized notion of mean curvature. Finally, we will use this machinery to define Brakke flow, a weak formulation of [mean curvature flow](@entry_id:184231) capable of handling the formation of singularities.

### The Geometric Measure-Theoretic Setting: Varifolds

Classical differential geometry is primarily concerned with smooth [submanifolds](@entry_id:159439). However, many problems in geometry and physics, particularly those arising from [variational principles](@entry_id:198028), naturally lead to objects with singularities or lower regularity. To study such phenomena, we require a framework that can describe "surface-like" objects in a way that is robust under limiting operations. Varifold theory, introduced by Frederick J. Almgren, Jr., provides such a framework by representing generalized surfaces as measures.

#### The Space of Positions and Tangent Planes

A smooth $k$-dimensional [submanifold](@entry_id:262388) of $\mathbb{R}^n$ is characterized at each point not only by its position but also by its [tangent space](@entry_id:141028)—a $k$-dimensional linear subspace of $\mathbb{R}^n$. To generalize this concept, we must consider a space that encodes both position and tangent plane information simultaneously. The positional information resides in the ambient space $\mathbb{R}^n$, while the directional information is captured by the **Grassmannian manifold**.

The **Grassmannian** $G(n,k)$ is the set of all $k$-dimensional linear subspaces (or $k$-planes) of $\mathbb{R}^n$. To use this set in analysis, we must equip it with a topology that makes it a manifold. There are several equivalent ways to do this [@problem_id:3077640].

One approach is to identify each $k$-plane $S \in G(n,k)$ with the unique [orthogonal projection](@entry_id:144168) matrix $P_S: \mathbb{R}^n \to \mathbb{R}^n$ whose image is $S$. This matrix is characterized by being symmetric ($P_S^T = P_S$), idempotent ($P_S^2 = P_S$), and having a trace equal to the dimension of its image, $\mathrm{trace}(P_S) = k$. The set of all such matrices forms a compact, smooth [submanifold](@entry_id:262388) within the vector space of all $n \times n$ matrices. The topology on $G(n,k)$ is the subspace topology induced by this embedding.

An alternative, more abstract construction identifies $G(n,k)$ as a [homogeneous space](@entry_id:159636). The [orthogonal group](@entry_id:152531) $O(n)$ acts transitively on the set of $k$-planes. The stabilizer of a fixed $k$-plane (e.g., $\mathbb{R}^k \times \{0\}^{n-k}$) is the subgroup of orthogonal transformations that preserve this plane, which is isomorphic to $O(k) \times O(n-k)$. Consequently, $G(n,k)$ is homeomorphic to the [quotient space](@entry_id:148218) $O(n)/(O(k) \times O(n-k))$. Endowed with the [quotient topology](@entry_id:150384), $G(n,k)$ becomes a compact, smooth manifold of dimension $k(n-k)$.

The fundamental space for [varifold](@entry_id:194011) theory is the [product space](@entry_id:151533) $\mathbb{R}^n \times G(n,k)$. A point $(x, S)$ in this space represents a $k$-plane $S$ located at the point $x$. We equip this space with the [product topology](@entry_id:154786) and its associated **Borel $\sigma$-algebra**, which is the natural setting for [measure theory](@entry_id:139744).

#### Definition of a General Varifold

With the underlying space established, the definition of a [varifold](@entry_id:194011) is remarkably concise.

A **$k$-dimensional [varifold](@entry_id:194011)** (or $k$-[varifold](@entry_id:194011)) $V$ in an open set $U \subseteq \mathbb{R}^n$ is a **Radon measure** on the product space $U \times G(n,k)$. If $U = \mathbb{R}^n$, we simply call it a $k$-[varifold](@entry_id:194011) in $\mathbb{R}^n$ [@problem_id:3077649].

A Radon measure is a measure on the Borel $\sigma$-algebra of a topological space that is finite on all [compact sets](@entry_id:147575), outer regular on all Borel sets, and inner regular on all open sets. By the Riesz-Markov-Kakutani [representation theorem](@entry_id:275118), such measures correspond to positive linear functionals on the space of [continuous functions with [compact suppor](@entry_id:193381)t](@entry_id:276214), denoted $C_c(U \times G(n,k))$. This means that a [varifold](@entry_id:194011) $V$ is completely determined by the values of the integrals $\int_{U \times G(n,k)} \varphi(x,S) \, dV(x,S)$ for all test functions $\varphi \in C_c(U \times G(n,k))$.

#### The Weight Measure and Mass

A [varifold](@entry_id:194011) $V$ contains information about both position and orientation. Often, we are interested only in the spatial distribution of the generalized surface, ignoring the [tangent plane](@entry_id:136914) information. This is captured by the **weight measure** (or mass measure) of the [varifold](@entry_id:194011), denoted $\|V\|$.

The weight measure $\|V\|$ is a measure on the spatial domain $\mathbb{R}^n$ defined as the **pushforward** of the [varifold](@entry_id:194011) $V$ under the natural projection map $\pi: \mathbb{R}^n \times G(n,k) \to \mathbb{R}^n$, where $\pi(x,S) = x$. By the definition of a [pushforward measure](@entry_id:201640), for any Borel set $A \subseteq \mathbb{R}^n$, the mass of $A$ is given by [@problem_id:3077649] [@problem_id:3077615]:
$$
\|V\|(A) = V(\pi^{-1}(A)) = V(A \times G(n,k))
$$
Since $V$ is a Radon measure and $\pi$ is a continuous map, the weight measure $\|V\|$ is also a Radon measure on $\mathbb{R}^n$.

This distinction gives rise to two different notions of support. The **full support**, $\mathrm{spt}\,V$, is the support of the measure $V$ on the full space $\mathbb{R}^n \times G(n,k)$. The **spatial support**, $\mathrm{spt}\,\|V\|$, is the support of the weight measure $\|V\|$ on the spatial domain $\mathbb{R}^n$. The spatial support is simply the projection of the full support onto $\mathbb{R}^n$ [@problem_id:3077649].

The **mass** of a [varifold](@entry_id:194011) $V$ within an open set $\Omega \subset \mathbb{R}^n$ is defined as $\|V\|(\Omega)$. Since $\|V\|$ is a Radon measure, this mass is guaranteed to be finite if the closure of $\Omega$ is compact [@problem_id:3077615].

#### A Hierarchy of Varifolds: Rectifiable and Integral Varifolds

The definition of a general [varifold](@entry_id:194011) as any Radon measure on $\mathbb{R}^n \times G(n,k)$ is extremely broad. It includes objects that bear little resemblance to surfaces, such as measures that are diffusely spread across the space like dust. To focus on more "surface-like" objects, we introduce important subclasses of [varifolds](@entry_id:199701).

The key concept is **[rectifiability](@entry_id:202091)**. A set $M \subset \mathbb{R}^n$ is called **countably $k$-rectifiable** if, up to a set of $k$-dimensional Hausdorff [measure zero](@entry_id:137864), it can be covered by a countable collection of images of $C^1$ maps from $\mathbb{R}^k$ into $\mathbb{R}^n$. A fundamental theorem of [geometric measure theory](@entry_id:187987) states that for $\mathcal{H}^k$-almost every point $x$ in a $k$-rectifiable set $M$, there exists a unique **approximate [tangent plane](@entry_id:136914)**, denoted $T_x M \in G(n,k)$.

This allows us to define a class of [varifolds](@entry_id:199701) that are explicitly associated with [rectifiable sets](@entry_id:635569). A $k$-[varifold](@entry_id:194011) $V$ is a **rectifiable [varifold](@entry_id:194011)** if there exists a countably $k$-rectifiable set $M \subset \mathbb{R}^n$ and a locally $\mathcal{H}^k$-integrable [multiplicity](@entry_id:136466) function $\theta: M \to [0, \infty)$ such that $V$ can be represented by the pair $(M, \theta)$. This representation, which we may denote as $V = V(M, \theta)$, is given by its action on any [test function](@entry_id:178872) $\varphi \in C_c(\mathbb{R}^n \times G(n,k))$ [@problem_id:3077616] [@problem_id:3077648]:
$$
\int_{\mathbb{R}^n \times G(n,k)} \varphi(x,S) \, dV(x,S) = \int_{M} \varphi(x, T_x M) \, \theta(x) \, d\mathcal{H}^k(x)
$$
Here, $\mathcal{H}^k$ is the $k$-dimensional Hausdorff measure. This formula states that the [varifold](@entry_id:194011) is concentrated on the graph of the approximate [tangent map](@entry_id:203492) over the set $M$, with the measure at each point weighted by the [multiplicity](@entry_id:136466) $\theta(x)$. For such a [varifold](@entry_id:194011), the mass in a set $\Omega$ is simply $\int_{M \cap \Omega} \theta \, d\mathcal{H}^k$ [@problem_id:3077615].

The most important class of [varifolds](@entry_id:199701) for geometric applications are **integral [varifolds](@entry_id:199701)**. An integral [varifold](@entry_id:194011) is a rectifiable [varifold](@entry_id:194011) $V(M,\theta)$ for which the [multiplicity](@entry_id:136466) function $\theta(x)$ takes values in the non-negative integers $\{0, 1, 2, \dots\}$ for $\mathcal{H}^k$-almost every $x \in M$ [@problem_id:3077616] [@problem_id:3077648]. These [varifolds](@entry_id:199701) correspond to our intuition of a geometric object composed of one or more "sheets" of a surface, with the [multiplicity](@entry_id:136466) counting how many sheets overlap at a given point.

### Variational Properties: Mean Curvature

The power of [varifolds](@entry_id:199701) lies not only in their generality but also in their suitability for the [calculus of variations](@entry_id:142234). We can define a notion of [mean curvature](@entry_id:162147) for [varifolds](@entry_id:199701) that generalizes the classical concept from differential geometry.

#### First Variation and Generalized Mean Curvature

The mean curvature of a classical surface is related to how its area changes under small deformations. This principle is generalized to [varifolds](@entry_id:199701) through the **[first variation](@entry_id:174697)**. Given a smooth, compactly supported vector field $X \in C_c^1(\mathbb{R}^n; \mathbb{R}^n)$, we can imagine deforming the ambient space by flowing along $X$ for a short time. The [first variation](@entry_id:174697) of a [varifold](@entry_id:194011) $V$, denoted $\delta V(X)$, is the initial rate of change of the mass of the [varifold](@entry_id:194011) under this deformation. It can be shown to be given by the formula [@problem_id:3077646]:
$$
\delta V(X) := \int_{\mathbb{R}^n \times G(n,k)} \mathrm{div}_S X(x) \, dV(x,S)
$$
where $\mathrm{div}_S X(x)$ is the divergence of the vector field $X$ restricted to the plane $S$. $\delta V$ is a vector-valued distribution, or more precisely, a vector-valued Radon measure.

For a smooth $C^2$ [submanifold](@entry_id:262388) $M$, the divergence theorem on the manifold gives $\int_M \mathrm{div}_M X \, d\mathcal{H}^k = - \int_M X \cdot H_M \, d\mathcal{H}^k$, where $H_M$ is the classical [mean curvature vector](@entry_id:199617). This suggests a way to define [mean curvature](@entry_id:162147) for [varifolds](@entry_id:199701). We say that a [varifold](@entry_id:194011) $V$ has a **[generalized mean curvature](@entry_id:199614) vector** if its [first variation](@entry_id:174697) measure, $\delta V$, can be written as an integral against its weight measure $\|V\|$.

Crucially, this is not always possible. The existence of a [generalized mean curvature](@entry_id:199614) vector $H$ as a function requires that the measure $\delta V$ be **absolutely continuous** with respect to the measure $\|V\|$ (denoted $\delta V \ll \|V\|$). If this condition holds, the Radon-Nikodym theorem guarantees the existence of a unique (up to $\|V\|$-a.e. equality) vector field $H \in L^1_{\mathrm{loc}}(\|V\|; \mathbb{R}^n)$ such that [@problem_id:3077645]:
$$
\delta V(X) = - \int_{\mathbb{R}^n} X(x) \cdot H(x) \, d\|V\|(x) \quad \text{for all } X \in C_c^1(\mathbb{R}^n; \mathbb{R}^n)
$$
The negative sign is a convention to ensure that for a smooth submanifold, this generalized $H$ coincides $\mathcal{H}^k$-[almost everywhere](@entry_id:146631) with the classical [mean curvature vector](@entry_id:199617) [@problem_id:3077645]. If $\delta V$ is not absolutely continuous with respect to $\|V\|$, it has a singular part that cannot be represented by an integral against $d\|V\|$, and a [mean curvature](@entry_id:162147) *function* in this sense does not exist for the entire [first variation](@entry_id:174697) [@problem_id:3077645].

#### Stationary Varifolds

A [varifold](@entry_id:194011) $V$ is called **stationary** if its [first variation](@entry_id:174697) vanishes for all test [vector fields](@entry_id:161384), i.e., $\delta V(X) = 0$ for all $X \in C_c^1(\mathbb{R}^n; \mathbb{R}^n)$ [@problem_id:3077656]. This means the [varifold](@entry_id:194011) is a critical point of the [area functional](@entry_id:635965) with respect to all compactly supported deformations.

If a [stationary varifold](@entry_id:188378) has a [generalized mean curvature](@entry_id:199614) vector $H$ (i.e., if $\delta V \ll \|V\|$), then the condition $\delta V \equiv 0$ is equivalent to the [mean curvature vector](@entry_id:199617) being zero $\|V\|$-almost everywhere. The relation $\int X \cdot H \, d\|V\| = 0$ for all test fields $X$ implies that $H$ must be the [zero vector](@entry_id:156189) almost everywhere. Conversely, if $H=0$ a.e., the integral is trivially zero for all $X$. Stationary integral [varifolds](@entry_id:199701) are the measure-theoretic generalization of classical minimal surfaces [@problem_id:3077656] [@problem_id:3077645].

### Evolution by Mean Curvature: Brakke Flow

Mean curvature flow is the geometric [gradient flow](@entry_id:173722) for the [area functional](@entry_id:635965). A smooth surface evolves in the direction of its [mean curvature vector](@entry_id:199617) to most rapidly decrease its area. This process can lead to the formation of singularities. Brakke flow, developed by Kenneth Brakke, is a weak formulation of [mean curvature flow](@entry_id:184231) within the [varifold](@entry_id:194011) framework that is designed to continue the evolution through and beyond these singular times.

#### From Smooth Flow to a Weak Inequality

Consider a smooth family of [hypersurfaces](@entry_id:159491) $M_t$ evolving by [mean curvature flow](@entry_id:184231). For any time-independent [test function](@entry_id:178872) $\phi \in C_c^1(\mathbb{R}^n)$, the rate of change of the weighted area is given by the identity [@problem_id:3077608]:
$$
\frac{d}{dt} \int_{M_t} \phi \, d\mathcal{H}^{n-1} = \int_{M_t} \left( -\phi |H|^2 + \nabla\phi \cdot H \right) \, d\mathcal{H}^{n-1}
$$
This is an **equality**. The term $-\int \phi |H|^2$ shows that area is dissipated at a rate proportional to the square of the [mean curvature](@entry_id:162147).

When a flow develops a singularity (e.g., a sphere collapsing to a point, or a dumbbell pinching off), the surface ceases to be smooth and may lose a macroscopic amount of area instantaneously. The equality above breaks down. Brakke's insight was to replace this equality with an inequality that allows for this sudden loss of mass but forbids the spontaneous creation of mass.

A family of $k$-[varifolds](@entry_id:199701) $t \mapsto V_t$ with weight measures $\mu_t = \|V_t\|$ and [generalized mean](@entry_id:174166) curvatures $H(\cdot, t)$ is called a **Brakke flow** if for all non-negative [test functions](@entry_id:166589) $\phi \in C_c^1(\mathbb{R}^n \times (0, \infty))$ and for all times $0 \le t_1 \le t_2$, the following inequality holds [@problem_id:3077646]:
$$
\int_{\mathbb{R}^n} \phi(x,t_2)\, d\mu_{t_2}(x) - \int_{\mathbb{R}^n} \phi(x,t_1)\, d\mu_{t_1}(x) \le \int_{t_1}^{t_2} \int_{\mathbb{R}^n} \left( \frac{\partial \phi}{\partial t} + \nabla \phi \cdot H - \phi |H|^2 \right) d\mu_t \, dt
$$
This inequality is the heart of the definition of Brakke flow. It can also be expressed in a time-local form using an upper Dini derivative, stating that for a.e. $t$, $\frac{d}{dt}^+ \int \phi \, d\mu_t \le \int (-\phi |H|^2 + \nabla\phi \cdot H + \partial_t\phi) \, d\mu_t$ [@problem_id:3077645] [@problem_id:3077608].

#### The Essential Role of the Inequality and Non-negative Test Functions

Two features of the Brakke flow definition are paramount: the inequality sign and the restriction to non-negative [test functions](@entry_id:166589). They are deeply intertwined and essential for correctly modeling a dissipative [geometric flow](@entry_id:186019) [@problem_id:3077624].

The use of an inequality ($\le$) instead of an equality is what allows the flow to handle singularities. It states that the change in weighted mass is *at most* what is predicted by the smooth part of the evolution. At a singular time, where mass vanishes abruptly, the left-hand side will be a large negative number, which is permitted by the inequality.

The restriction to **non-negative [test functions](@entry_id:166589)** ($\phi \ge 0$) is crucial for two reasons.

First, from a conceptual standpoint, it enforces the **[irreversibility](@entry_id:140985)** of the flow. The term $-\int \phi |H|^2 d\mu_t$ represents the dissipation of weighted area due to curvature. Since $\phi \ge 0$ and $|H|^2 \ge 0$, this term is always non-positive. This ensures that curvature can only destroy weighted mass, not create it. If $\phi$ were allowed to be negative, this term could become positive, corresponding to an unphysical, anti-dissipative process where curvature spontaneously generates area [@problem_id:3077624].

Second, from a technical perspective, the restriction is necessary for the very derivation of the inequality. Weak solutions like Brakke flows are often constructed as [limits of sequences](@entry_id:159667) of smooth, approximating flows. For the smooth flows, the evolution is governed by an equality. When taking the limit, the linear terms involving $\phi$ and $\nabla\phi$ behave well, but the quadratic term $\int \phi |H_j|^2 d\mu_t^{(j)}$ is problematic. A fundamental result in analysis is that the $L^2$-norm is **weakly lower semicontinuous**. This means that if a [sequence of functions](@entry_id:144875) converges weakly, the norm of the limit is less than or equal to the [limit inferior](@entry_id:145282) of the norms. This property holds for the integral of $|H|^2$ *only when it is weighted by a non-negative function $\phi$*. This [lower semicontinuity](@entry_id:195138) is what transforms the equality for the approximating smooth flows into the one-sided inequality that defines Brakke flow in the limit [@problem_id:3077624]. The non-negativity of $\phi$ is not an arbitrary choice, but a necessary hypothesis to ensure the weak formulation correctly captures the dissipative nature of [mean curvature flow](@entry_id:184231).