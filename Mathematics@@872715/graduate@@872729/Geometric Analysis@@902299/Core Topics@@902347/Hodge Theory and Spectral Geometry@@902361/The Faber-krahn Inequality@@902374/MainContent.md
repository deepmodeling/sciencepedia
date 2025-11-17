## Introduction
The Faber-Krahn inequality is a landmark theorem in [spectral geometry](@entry_id:186460) that provides a definitive answer to a profound question: which shape, for a given volume, has the lowest [fundamental frequency](@entry_id:268182) of vibration? This principle establishes a deep connection between the geometry of a domain and the spectral properties of the Laplace operator. It addresses the fundamental problem of optimizing an eigenvalue under a geometric constraint, revealing that the most symmetric shape—the ball—is the unique optimizer. This article offers a comprehensive exploration of this pivotal inequality.

The following chapters will guide you through the theory and its far-reaching consequences. In "Principles and Mechanisms," we will rigorously define the first Dirichlet eigenvalue using [variational methods](@entry_id:163656) and detail the elegant proof mechanism of spherical symmetrization. Following that, "Applications and Interdisciplinary Connections" will explore the inequality's impact on physics, from the pitch of a drum to the ground state energy of a quantum particle, and situate it within the broader context of spectral theory and geometry. Finally, "Hands-On Practices" will provide concrete problems to solidify your understanding of the inequality's theoretical and computational aspects.

## Principles and Mechanisms

The Faber-Krahn inequality stands as a landmark result in [spectral geometry](@entry_id:186460), providing a definitive answer to the question of which shape, among all domains of a fixed volume, possesses the lowest fundamental frequency of vibration. This chapter delves into the principles and mechanisms that underpin this celebrated inequality. We will begin by rigorously defining the [fundamental frequency](@entry_id:268182), known as the first Dirichlet eigenvalue, and exploring its essential properties. We will then introduce the powerful technique of spherical symmetrization and demonstrate how it serves as the engine for the proof, translating a classical geometric principle into a profound statement about partial differential operators.

### The First Dirichlet Eigenvalue: A Variational Perspective

The physical context for our discussion is the vibration of a membrane fixed at its boundary. The modes of vibration correspond to solutions of the Helmholtz equation, which emerges from the wave equation after [separation of variables](@entry_id:148716). For a domain $\Omega \subset \mathbb{R}^n$ with boundary $\partial\Omega$, this is the [eigenvalue problem](@entry_id:143898) for the Laplace operator $-\Delta$:
$$
\begin{cases}
-\Delta u = \lambda u  \text{in } \Omega \\
u = 0  \text{on } \partial\Omega
\end{cases}
$$
Here, $u$ represents the amplitude of the vibration, and the eigenvalues $\lambda$ are proportional to the squares of the possible frequencies. The lowest possible frequency corresponds to the smallest positive eigenvalue, $\lambda_1(\Omega)$, often called the **principal eigenvalue** or **fundamental frequency**.

While this classical formulation is intuitive, [modern analysis](@entry_id:146248) demands a more robust framework that can accommodate domains with non-smooth boundaries. This is achieved through a weak formulation grounded in the theory of Sobolev spaces. The appropriate space for functions satisfying the zero boundary condition is the Sobolev space $H_0^1(\Omega)$. This space is formally defined as the completion of the space of infinitely differentiable functions with [compact support](@entry_id:276214) in $\Omega$, denoted $C_c^\infty(\Omega)$, with respect to the $H^1$ norm, $\|u\|_{H^1} = (\int_\Omega (|u|^2 + |\nabla u|^2) dx)^{1/2}$. The condition $u=0$ on $\partial\Omega$ is thus built into the structure of the space, a concept far more versatile than pointwise evaluation, especially for domains with complex boundaries [@problem_id:3035144] [@problem_id:3035163].

To obtain the [weak formulation](@entry_id:142897), we multiply the PDE by a [test function](@entry_id:178872) $v \in H_0^1(\Omega)$ and integrate over $\Omega$. Applying Green's first identity (integration by parts), we find that a nonzero function $u \in H_0^1(\Omega)$ is a weak solution if it satisfies:
$$
\int_{\Omega} \nabla u \cdot \nabla v \, dx = \lambda \int_{\Omega} u v \, dx \quad \text{for all } v \in H_0^1(\Omega).
$$
Setting the [test function](@entry_id:178872) $v=u$, we obtain a crucial identity for any [eigenfunction](@entry_id:149030) $u$:
$$
\int_{\Omega} |\nabla u|^2 \, dx = \lambda \int_{\Omega} |u|^2 \, dx.
$$
This motivates the definition of the **Rayleigh quotient**, $R(u)$:
$$
R(u) = \frac{\int_{\Omega} |\nabla u|^2 \, dx}{\int_{\Omega} |u|^2 \, dx}.
$$
The first Dirichlet eigenvalue, $\lambda_1(\Omega)$, is then characterized variationally as the minimum possible value of this quotient over all admissible functions. This is the celebrated **Rayleigh-Ritz principle** [@problem_id:3035176].

**Definition 2.1 (First Dirichlet Eigenvalue):** For a bounded open set $\Omega \subset \mathbb{R}^n$, the first Dirichlet eigenvalue of the Laplacian is defined as
$$
\lambda_1(\Omega) = \inf_{u \in H_0^1(\Omega) \setminus \{0\}} \frac{\int_{\Omega} |\nabla u|^2 \, dx}{\int_{\Omega} |u|^2 \, dx}.
$$
This variational characterization is profoundly important. It guarantees that $\lambda_1(\Omega)$ is the smallest eigenvalue of the Dirichlet Laplacian [@problem_id:3035144]. The existence of a non-trivial function $u_1 \in H_0^1(\Omega)$, the first [eigenfunction](@entry_id:149030), that actually attains this [infimum](@entry_id:140118) is a non-trivial result. It follows from the direct method of the calculus of variations, which relies on the **Rellich-Kondrachov theorem**. This theorem states that for a bounded domain $\Omega$, the embedding of $H_0^1(\Omega)$ into $L^2(\Omega)$ is compact. This compactness is the key ingredient that allows one to extract a strongly convergent subsequence in $L^2$ from a weakly convergent minimizing sequence in $H_0^1$, ensuring that a minimizer exists [@problem_id:3035144].

Furthermore, for any bounded domain $\Omega$, the **Poincaré inequality** guarantees the existence of a constant $C_\Omega$ such that $\|u\|_{L^2(\Omega)} \le C_\Omega \|\nabla u\|_{L^2(\Omega)}$ for all $u \in H_0^1(\Omega)$. From the Rayleigh quotient, it is immediately clear that $\lambda_1(\Omega) \ge C_\Omega^{-2} > 0$. Therefore, the first Dirichlet eigenvalue is strictly positive for any bounded domain. In fact, $\lambda_1(\Omega)$ is precisely the reciprocal of the square of the optimal (smallest) Poincaré constant, $\lambda_1(\Omega) = C_\Omega^{-2}$ [@problem_id:3035144]. This positivity distinguishes the Dirichlet problem from the Neumann problem (where the boundary condition is on the [normal derivative](@entry_id:169511)), for which the first eigenvalue is always zero, corresponding to a constant [eigenfunction](@entry_id:149030). For the Dirichlet problem, a non-zero [constant function](@entry_id:152060) can never belong to $H_0^1(\Omega)$, so zero is never an eigenvalue.

### Scaling Properties and Dimensional Consistency

Before tackling the Faber-Krahn inequality, it is instructive to understand how the first eigenvalue behaves under a change of scale. Consider a domain $\Omega$ and its dilation by a factor $t>0$, denoted $t\Omega = \{tx : x \in \Omega\}$. How does $\lambda_1(t\Omega)$ relate to $\lambda_1(\Omega)$?

We can answer this directly from the Rayleigh-Ritz principle. Let $v$ be a [test function](@entry_id:178872) on $t\Omega$. We can relate it to a [test function](@entry_id:178872) $u$ on $\Omega$ by setting $u(x) = v(tx)$. A [change of variables](@entry_id:141386) in the Rayleigh quotient for $v$ on $t\Omega$ reveals the scaling behavior. The $L^2$-norm term (denominator) transforms as:
$$
\int_{t\Omega} |v(y)|^2 \, dy = \int_{\Omega} |u(x)|^2 (t^n \, dx) = t^n \int_{\Omega} |u(x)|^2 \, dx.
$$
The Dirichlet energy (numerator) requires the [chain rule](@entry_id:147422) for the gradient, $\nabla_y v(y) = t^{-1} \nabla_x u(x)$. Its transformation is:
$$
\int_{t\Omega} |\nabla_y v(y)|^2 \, dy = \int_{\Omega} |t^{-1} \nabla_x u(x)|^2 (t^n \, dx) = t^{n-2} \int_{\Omega} |\nabla_x u(x)|^2 \, dx.
$$
The Rayleigh quotient for $v$ on $t\Omega$ is therefore related to that of $u$ on $\Omega$ by a simple factor:
$$
\frac{\int_{t\Omega} |\nabla v|^2 \, dy}{\int_{t\Omega} |v|^2 \, dy} = \frac{t^{n-2} \int_{\Omega} |\nabla u|^2 \, dx}{t^n \int_{\Omega} |u|^2 \, dx} = t^{-2} \frac{\int_{\Omega} |\nabla u|^2 \, dx}{\int_{\Omega} |u|^2 \, dx}.
$$
Since this holds for any test function and the mapping between function spaces is a [bijection](@entry_id:138092), the infima are also related by this factor. This yields the fundamental scaling law [@problem_id:3035124]:
$$
\lambda_1(t\Omega) = \frac{1}{t^2} \lambda_1(\Omega).
$$
This law states that if you expand a domain, its [fundamental frequency](@entry_id:268182) decreases, and vice-versa.

This scaling behavior has a crucial consequence for any [isoperimetric inequality](@entry_id:196977) involving $\lambda_1$. The volume of the domain scales as $|t\Omega| = t^n |\Omega|$. An inequality comparing $\lambda_1$ for domains of a fixed volume must be independent of the absolute size of that volume, depending only on shape. We can construct a scale-invariant quantity by finding the power $\alpha$ such that $\lambda_1(\Omega) |\Omega|^\alpha$ is constant under dilation.
$$
\lambda_1(t\Omega) |t\Omega|^\alpha = (t^{-2} \lambda_1(\Omega)) (t^n |\Omega|)^\alpha = t^{n\alpha - 2} \lambda_1(\Omega)|\Omega|^\alpha.
$$
For this quantity to be invariant, the exponent of $t$ must be zero, which implies $n\alpha - 2 = 0$, or $\alpha = 2/n$. This shows that the quantity $\lambda_1(\Omega) |\Omega|^{2/n}$ is invariant under scaling [@problem_id:3035157]. Consequently, any inequality comparing $\lambda_1(\Omega)$ across domains must do so by bounding this [scale-invariant](@entry_id:178566) quantity. This naturally leads to the form of the Faber-Krahn inequality.

### The Faber-Krahn Inequality and the Mechanism of Symmetrization

We are now ready to state the central theorem.

**Theorem 2.2 (Faber-Krahn Inequality):** Let $\Omega \subset \mathbb{R}^n$ be a bounded open set. Let $B$ be a ball with the same Lebesgue measure as $\Omega$, i.e., $|B| = |\Omega|$. Then
$$
\lambda_1(\Omega) \ge \lambda_1(B).
$$
Equality holds if and only if $\Omega$ is a ball (up to a set of measure zero).

This theorem asserts that among all shapes with a given volume, the ball is the unique minimizer of the first Dirichlet eigenvalue [@problem_id:3035176]. The proof is a masterpiece of analysis, relying on a technique that transforms an arbitrary function into a radially symmetric one while controlling its key properties. This technique is known as **spherical decreasing rearrangement**.

Given a non-negative function $u \in H_0^1(\Omega)$, its spherical decreasing rearrangement, denoted $u^*$, is a function defined on the ball $B$ of equal measure, $|B| = |\Omega|$. It is constructed to be spherically symmetric about the origin and non-increasing in the radial direction. The defining characteristic of $u^*$ is that it is **equimeasurable** with $u$. This means that for any height $t > 0$, the volume of the region where $u$ exceeds $t$ is the same as the volume of the region where $u^*$ exceeds $t$ [@problem_id:3035175]:
$$
|\{x \in \Omega : u(x) > t\}| = |\{x \in B : u^*(x) > t\}| \quad \text{for all } t > 0.
$$
One can visualize this process as slicing the graph of $u$ into infinitesimally thin horizontal layers, turning each layer into a circular disk of the same area, and then stacking these disks in decreasing order of size to form the graph of $u^*$ [@problem_id:3035160].

This construction has two magical properties that are the pillars of the Faber-Krahn proof:

1.  **Preservation of $L^p$ norms:** A direct consequence of equimeasurability and the layer-cake representation of integrals is that the $L^p$ norm of the function is preserved under rearrangement. For any $p \in [1, \infty]$, we have $\|u\|_{L^p(\Omega)} = \|u^*\|_{L^p(B)}$. For our purposes, the case $p=2$ is essential:
    $$
    \int_{\Omega} |u|^2 \, dx = \int_{B} |u^*|^2 \, dx.
    $$
    This means the denominator of the Rayleigh quotient remains unchanged after rearrangement [@problem_id:3035175] [@problem_id:3035160].

2.  **The Pólya-Szegő Inequality:** While the $L^2$ norm is preserved, the Dirichlet energy (the integral of the squared gradient) systematically *decreases* or stays the same. This is the celebrated Pólya-Szegő inequality:
    $$
    \int_{\Omega} |\nabla u|^2 \, dx \ge \int_{B} |\nabla u^*|^2 \, dx.
    $$
    This inequality is the functional counterpart of the geometric [isoperimetric inequality](@entry_id:196977), a connection we will explore shortly.

With these two properties, the proof of the Faber-Krahn inequality becomes remarkably elegant. Let $u_1$ be a first [eigenfunction](@entry_id:149030) for $\Omega$, which we can assume is non-negative. Its Rayleigh quotient is exactly $\lambda_1(\Omega)$. Now, consider its rearrangement $u_1^*$ on the ball $B$. We must first verify that $u_1^*$ is an admissible [test function](@entry_id:178872) for $\lambda_1(B)$, i.e., that $u_1^* \in H_0^1(B)$. This technical point is crucial; it follows by approximating $u_1 \in H_0^1(\Omega)$ with a sequence of [smooth functions](@entry_id:138942) with [compact support](@entry_id:276214) in $\Omega$, whose rearrangements are compactly supported strictly inside $B$. By continuity arguments involving the Pólya-Szegő inequality and the [trace operator](@entry_id:183665), one shows that the [limit function](@entry_id:157601) $u_1^*$ also has zero trace on $\partial B$ [@problem_id:3035148].

Since $u_1^*$ is a valid [test function](@entry_id:178872) for $\lambda_1(B)$, its Rayleigh quotient must be greater than or equal to the infimum, $\lambda_1(B)$. We can now assemble the final chain of inequalities [@problem_id:3035175]:
$$
\lambda_1(\Omega) = \frac{\int_{\Omega} |\nabla u_1|^2 \, dx}{\int_{\Omega} |u_1|^2 \, dx} \ge \frac{\int_{B} |\nabla u_1^*|^2 \, dx}{\int_{\Omega} |u_1|^2 \, dx} = \frac{\int_{B} |\nabla u_1^*|^2 \, dx}{\int_{B} |u_1^*|^2 \, dx} \ge \lambda_1(B).
$$
The first inequality is due to Pólya-Szegő, the equality is from $L^2$ norm preservation, and the final inequality is from the Rayleigh-Ritz principle applied to the ball $B$. This completes the proof. The framework is valid under very general conditions on the domain $\Omega$: it need only be an open set of finite Lebesgue measure. No assumptions of [connectedness](@entry_id:142066) or boundary regularity are required [@problem_id:3035163].

### The Isoperimetric Principle at the Core

The proof's linchpin is the Pólya-Szegő inequality. What is its origin? It is a direct functional consequence of the classical **[isoperimetric inequality](@entry_id:196977)**, which states that among all sets of a given volume in $\mathbb{R}^n$, the ball has the minimum surface area (perimeter).

The connection is forged by the **[coarea formula](@entry_id:162087)**, which allows us to express the Dirichlet energy as an integral over the [level sets](@entry_id:151155) of the function. For a function $u$, the [coarea formula](@entry_id:162087) combined with the Cauchy-Schwarz inequality leads to a lower bound on its Dirichlet energy involving the perimeters, $P(\{u>t\})$, of its superlevel sets. The [isoperimetric inequality](@entry_id:196977) states that $P(\{u>t\}) \ge P(B_t)$, where $B_t$ is a ball with the same volume as $\{u>t\}$.

When we integrate this "pointwise" [geometric inequality](@entry_id:749850) over all [level sets](@entry_id:151155) $t$, we obtain a "global" functional inequality for the entire function's energy. The rearranged function $u^*$ is constructed so that its level sets *are* the balls $B_t$, for which the [isoperimetric inequality](@entry_id:196977) is an equality. Thus, the Dirichlet energy of $u^*$ achieves the lower bound derived for the energy of $u$. This shows that the [isoperimetric inequality](@entry_id:196977) for sets implies the Pólya-Szegő inequality for functions. In a deep sense, they are equivalent principles [@problem_id:3035125]. The process of rearrangement translates the perimeter-minimizing property of the ball from the level of sets to the energy-minimizing property at the level of functions.

### The Rigidity of the Minimizer: Why the Ball is Unique

The Faber-Krahn theorem includes a rigidity statement: equality holds only if $\Omega$ is a ball. Proving this requires showing that any non-spherical deviation incurs a strict penalty in the eigenvalue. An essential first step is to establish that any minimizing domain must be **connected**.

We can prove this by contradiction. Assume a minimizer for $\lambda_1$ at a fixed volume $V$ is a [disconnected set](@entry_id:158535) $\Omega_* = \Omega_1 \cup \Omega_2$, where $\Omega_1$ and $\Omega_2$ are disjoint, non-empty open sets. The space $H_0^1(\Omega_*)$ splits into functions supported on $\Omega_1$ and $\Omega_2$, and the first eigenvalue is simply the minimum of the eigenvalues of the components: $\lambda_1(\Omega_*) = \min\{\lambda_1(\Omega_1), \lambda_1(\Omega_2)\}$. Let's say $\lambda_1(\Omega_1)$ is the minimum.

A first [eigenfunction](@entry_id:149030) $u_*$ for $\Omega_*$ must then be supported entirely on $\Omega_1$ and be identically zero on $\Omega_2$. This means $\lambda_1(\Omega_*) = \lambda_1(\Omega_1)$. But the volume of $\Omega_1$ is strictly less than $V$. We now have a domain $\Omega_1$ with volume $|\Omega_1|  V$ that achieves the minimal eigenvalue $\lambda_1(\Omega_*)$. We can now take this "active" component $\Omega_1$ and attach an open set of volume $V - |\Omega_1|$ to form a new [connected domain](@entry_id:169490) $\widetilde{\Omega}$ with total volume $V$. Because $\Omega_1$ is strictly contained in $\widetilde{\Omega}$, a strong version of domain [monotonicity](@entry_id:143760) for the eigenvalue applies: $\lambda_1(\widetilde{\Omega})  \lambda_1(\Omega_1)$.

We have thus constructed a domain $\widetilde{\Omega}$ of volume $V$ such that $\lambda_1(\widetilde{\Omega})  \lambda_1(\Omega_1) = \lambda_1(\Omega_*)$, contradicting the assumption that $\Omega_*$ was a minimizer. Therefore, any domain that minimizes the first Dirichlet eigenvalue must be connected [@problem_id:3035166]. This result, combined with a careful analysis of the equality conditions in the Pólya-Szegő and isoperimetric inequalities, leads to the full rigidity conclusion: the only minimizer is the ball.