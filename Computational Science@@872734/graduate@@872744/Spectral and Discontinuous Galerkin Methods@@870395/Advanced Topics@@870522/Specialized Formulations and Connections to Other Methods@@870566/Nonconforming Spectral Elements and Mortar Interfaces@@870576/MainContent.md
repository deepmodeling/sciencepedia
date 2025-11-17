## Introduction
High-order [spectral element methods](@entry_id:755171) (SEM) offer exceptional accuracy for [solving partial differential equations](@entry_id:136409), but their traditional reliance on conforming meshes—where elements must align perfectly—imposes significant constraints on geometric complexity and algorithmic flexibility. In many advanced applications, from [adaptive mesh refinement](@entry_id:143852) to [multiphysics](@entry_id:164478) simulations, the need to couple grids of different resolutions or polynomial orders is not an exception but the rule. This necessity creates a fundamental challenge: how to rigorously and stably connect discrete [function spaces](@entry_id:143478) that do not match at their shared boundaries.

This article addresses this challenge by providing a comprehensive exploration of **[nonconforming spectral elements](@entry_id:752622) and the mortar interface method**. The [mortar method](@entry_id:167336) serves as a powerful and mathematically sound framework for abandoning strict [pointwise continuity](@entry_id:143284) in favor of a weaker, integral-based coupling. This shift unlocks immense flexibility, enabling robust simulations on complex, nonconforming grids.

Over the next three chapters, you will gain a deep, practical understanding of this essential technique.
*   **Principles and Mechanisms** will lay the theoretical groundwork, introducing weak continuity, the Lagrange multiplier formulation, and the critical Babuška-Brezzi stability condition.
*   **Applications and Interdisciplinary Connections** will showcase the method's power in real-world scenarios, including [high-performance computing](@entry_id:169980), computational fluid dynamics, and fluid-structure interaction, while comparing it to related techniques like Discontinuous Galerkin methods.
*   **Hands-On Practices** will guide you through implementing and analyzing key components of the [mortar method](@entry_id:167336), bridging the gap between theory and code.

## Principles and Mechanisms

In the preceding chapter, we explored the foundations of [spectral element methods](@entry_id:755171) on conforming meshes, where adjacent elements align perfectly, sharing nodes and edges in a way that allows for the straightforward construction of globally continuous function spaces. While elegant, the constraint of mesh conformity can be overly restrictive in many practical applications, such as [adaptive mesh refinement](@entry_id:143852), multi-physics coupling, and large-scale parallel computing. This chapter delves into the principles and mechanisms of **nonconforming [spectral element methods](@entry_id:755171)**, which relax this constraint, offering substantially greater flexibility. At the heart of these methods lies the **mortar interface**, a powerful mathematical and computational tool for rigorously coupling discretizations that do not match at their boundaries.

### The Challenge of Nonconforming Meshes

A conforming spectral element discretization constructs a global approximation space $V_h$ that is a true subspace of the underlying continuous [solution space](@entry_id:200470), typically a Sobolev space such as $H^1(\Omega)$. A key property of functions in $H^1(\Omega)$ is that they are continuous across any internal boundary within the domain. For a [piecewise polynomial approximation](@entry_id:178462), this implies that for any two adjacent elements $K^+$ and $K^-$, the traces of a function $v_h \in V_h$ must match perfectly along their common interface $\Gamma$:
$$
\gamma_{\Gamma} v_h|_{K^+} = \gamma_{\Gamma} v_h|_{K^-} \quad \text{almost everywhere on } \Gamma.
$$
This is known as **strong continuity** or **$C^0$-continuity**. In nodal [spectral element methods](@entry_id:755171), this is achieved by ensuring that adjacent elements share the same set of nodes on their common interface and by identifying the corresponding degrees of freedom.

A [discretization](@entry_id:145012) is deemed **nonconforming** when the assembled global space $V_h$ is not a subspace of $H^1(\Omega)$ because the strong continuity constraint is violated at one or more interfaces. Such a mismatch, or **nonconformity**, can arise from several sources common in advanced scientific computing [@problem_id:3403313]:

1.  **$p$-nonconformity**: Adjacent elements may employ different polynomial degrees, a strategy known as **$p$-refinement**. If element $K^+$ uses a [polynomial approximation](@entry_id:137391) of degree $p^+$ and its neighbor $K^-$ uses degree $p^- \neq p^+$, their [trace spaces](@entry_id:756085) on the interface $\Gamma$ will be different [polynomial spaces](@entry_id:753582). A trace function from the higher-degree element generally cannot be represented in the trace space of the lower-degree element, making pointwise equality impossible to enforce for all functions in the space.

2.  **$h$-nonconformity**: Local [mesh refinement](@entry_id:168565), or **$h$-refinement**, can lead to situations where a single large element abuts several smaller elements. The nodes on the edge of the large element will not all have corresponding nodes on the edges of the smaller elements. A node on a refined edge that does not coincide with a node on the coarse edge is known as a **[hanging node](@entry_id:750144)**. The presence of [hanging nodes](@entry_id:750145) inherently breaks the one-to-one nodal correspondence required for strong continuity [@problem_id:3403318].

3.  **Nodal nonconformity**: Even if polynomial degrees and [mesh topology](@entry_id:167986) match, nonconformity can arise if the underlying nodal distributions are different. For instance, if one element's trace is defined by nodes at Gauss-Lobatto-Legendre (GLL) points and the adjacent element's trace uses Gauss points, the nodal sets will not coincide, again precluding a simple identification of degrees of freedom [@problem_id:3403313].

The critical distinction between one-dimensional and higher-dimensional problems is the measure of the interface. In a 1D problem, the interface between two elements is a single point. If both elements use a nodal basis that includes the endpoints (like the GLL basis), this single interface point is a shared node. Continuity can be enforced by equating the single degree of freedom at this point, even if the polynomial degrees differ ($p_1 \neq p_2$). For example, on the domain $\Omega = [-1,1]$ partitioned into $\Omega_1 = [-1,0]$ and $\Omega_2=[0,1]$ with polynomial degrees $p_1=4$ and $p_2=2$, the total number of degrees of freedom is $(p_1+1) + (p_2+1) - 1 = (5+3)-1 = 7$, where one degree of freedom is removed by enforcing continuity at the single interface point $x=0$ [@problem_id:3403332].

In two or three dimensions, however, the interface is a line segment or a surface patch with positive measure. The non-aligning interior nodes along this interface prevent a simple conforming assembly. Naive pointwise matching is ill-defined, necessitating a more sophisticated approach to couple the disparate discretizations.

### The Mortar Method: A Framework for Weak Continuity

The [mortar method](@entry_id:167336) provides a mathematically rigorous and computationally flexible framework for coupling nonconforming discretizations. The central idea is to abandon the goal of strong (pointwise) continuity and instead enforce a **weak continuity** constraint in an integral sense.

Let us consider the Poisson problem on a domain $\Omega$ partitioned into two non-conforming subdomains, $\Omega^+$ and $\Omega^-$, sharing an interface $\Gamma$. The standard [weak formulation](@entry_id:142897) seeks a solution $u \in H^1_0(\Omega)$ by testing against all functions $v \in H^1_0(\Omega)$. In our nonconforming setting, we work with a "broken" function space where solutions are sought in $H^1(\Omega^+)$ and $H^1(\Omega^-)$ but are not necessarily continuous across $\Gamma$. To couple the two subdomains, we introduce a new [function space](@entry_id:136890) on the interface, the **mortar space**, denoted $\Lambda_h(\Gamma)$. The strong continuity condition $u^+ - u^- = 0$ on $\Gamma$ is replaced by the weak constraint:
$$
\int_{\Gamma} \mu_h (u^+ - u^-) \, \mathrm{d}s = 0, \quad \forall \mu_h \in \Lambda_h.
$$
This condition forces the jump in the solution, $[u] \equiv u^+ - u^-$, to be $L^2$-orthogonal to the mortar space $\Lambda_h$. This does not guarantee that the jump is zero at every point, but it ensures that the jump is zero "on average" when weighted by any function from the mortar space.

To incorporate this constraint into the variational problem, we introduce a **Lagrange multiplier**, $\lambda_h \in \Lambda_h$, which is an independent field defined only on the interface. The Lagrange multiplier physically represents the normal flux across the interface, $-\nabla u \cdot \mathbf{n}$. The resulting system is a [saddle-point problem](@entry_id:178398) for the pair $(u_h, \lambda_h)$ [@problem_id:3403320].

### Variational Formulation and the Stability Condition

Let's formalize the saddle-point system for the Poisson problem $-\Delta u = f$. We seek a solution pair $(u_h, \lambda_h)$ in the broken [discrete space](@entry_id:155685) $V_h \times \Lambda_h$ such that:
$$
\begin{align}
\sum_{k \in \{+,-\}} \int_{\Omega^k} \nabla u_h \cdot \nabla v_h \, \mathrm{d}x - \int_{\Gamma} \lambda_h [v_h] \, \mathrm{d}s = \int_{\Omega} f v_h \, \mathrm{d}x, \quad \forall v_h \in V_h \\
\int_{\Gamma} \mu_h [u_h] \, \mathrm{d}s = 0, \quad \forall \mu_h \in \Lambda_h
\end{align}
$$
Here, we have used the convention that $[v_h] = v_h^+ - v_h^-$ and the integral involving $\lambda_h$ arises naturally from [integration by parts](@entry_id:136350) over the subdomains. The first equation represents the weak form of the PDE on the subdomains coupled by the flux term, while the second equation enforces the [weak continuity constraint](@entry_id:756660).

The [well-posedness](@entry_id:148590) of this saddle-point system is not automatic. It requires a delicate balance between the trace space of $V_h$ on the interface, let's call it $W_h(\Gamma)$, and the mortar space $\Lambda_h$. This balance is formalized by the celebrated **Babuška-Brezzi (or inf-sup) condition**, which states that there must exist a constant $\beta > 0$, independent of the [discretization](@entry_id:145012), such that:
$$
\inf_{\lambda_h \in \Lambda_h \setminus \{0\}} \sup_{w_h \in W_h(\Gamma) \setminus \{0\}} \frac{\int_{\Gamma} w_h \lambda_h \, \mathrm{d}s}{\|w_h\|_{W} \|\lambda_h\|_{\Lambda}} \ge \beta.
$$
where $\| \cdot \|_W$ and $\| \cdot \|_{\Lambda}$ are appropriate norms on the trace and multiplier spaces (typically $H^{1/2}(\Gamma)$ and $H^{-1/2}(\Gamma)$ related norms). Intuitively, this condition ensures that for every possible Lagrange multiplier function $\lambda_h \in \Lambda_h$, there is a trace function $w_h \in W_h(\Gamma)$ that it is not orthogonal to.

Failure to satisfy the [inf-sup condition](@entry_id:174538) leads to a loss of stability. This typically occurs when the mortar space $\Lambda_h$ is "too large" or "too rich" compared to the trace space $W_h(\Gamma)$. In such cases, there may exist a non-zero **spurious mode** $\lambda_{\text{spur}} \in \Lambda_h$ that is orthogonal to the *entire* trace space $W_h(\Gamma)$. This spurious mode becomes part of the [nullspace](@entry_id:171336) of the discrete operator, polluting the solution with non-physical oscillations.

As a concrete example, consider an interface where the trace space is the space of linear polynomials, $W_h(\Gamma) = \mathbb{P}_1([-1,1])$, and we improperly choose the mortar space to be quadratic polynomials, $\Lambda_h = \mathbb{P}_2([-1,1])$. We seek a non-zero $\lambda_{\text{spur}}(s) = a_0 + a_1 s + a_2 s^2$ that is orthogonal to every function in $\mathbb{P}_1$. It suffices to test orthogonality against the basis $\{1, s\}$. The conditions $\int_{-1}^1 \lambda_{\text{spur}}(s) \cdot 1 \, \mathrm{d}s = 0$ and $\int_{-1}^1 \lambda_{\text{spur}}(s) \cdot s \, \mathrm{d}s = 0$ lead to the constraints $a_1=0$ and $a_0 = -a_2/3$. This defines a family of [spurious modes](@entry_id:163321) proportional to $s^2 - 1/3$. The specific mode with unit $L^2$-norm is $\lambda_{\text{spur}}(s) = \frac{3\sqrt{10}}{4}(s^2 - 1/3)$, which is a scaled version of the second Legendre polynomial $P_2(s)$ [@problem_id:3403330]. A stable choice of mortar space, for instance, would be $\mathbb{P}_{p-2}$ for a trace space of degree $p$, or other specific choices that are proven to satisfy the inf-sup condition.

### Algebraic Realization: The $L^2$ Projection

From a computational perspective, the [weak continuity constraint](@entry_id:756660) is realized through an **$L^2$ projection**. Let's designate one side of the interface as the "master" (or non-mortar) side and the other as the "slave" (or mortar) side. The [weak continuity constraint](@entry_id:756660) enforces that the $L^2$ projection of the master trace onto the slave trace space must equal the slave trace. More generally, both traces are projected onto the common mortar space.

Consider an interface $\Gamma$ with a "fine" side (e.g., higher polynomial degree or finer mesh) and a "coarse" side. Let their [trace spaces](@entry_id:756085) be $V_h^{\text{fine}}|_{\Gamma}$ and $V_h^{\text{coarse}}|_{\Gamma}$. A common and stable mortar coupling involves projecting the fine trace onto the [coarse space](@entry_id:168883). We seek a projection $u_c \in V_h^{\text{coarse}}|_{\Gamma}$ of a given fine trace $u_f \in V_h^{\text{fine}}|_{\Gamma}$ such that the error is orthogonal to the [coarse space](@entry_id:168883):
$$
\int_{\Gamma} (u_c - u_f) v_c \, \mathrm{d}\Gamma = 0, \quad \forall v_c \in V_h^{\text{coarse}}|_{\Gamma}.
$$
To translate this into an algebraic system, we introduce bases for the [trace spaces](@entry_id:756085). Let $u_f$ and $u_c$ be represented by coefficient vectors $\mathbf{u}_f$ and $\mathbf{u}_c$. The [orthogonality condition](@entry_id:168905) becomes a linear system:
$$
\mathbf{M}_c \mathbf{u}_c = \mathbf{B} \mathbf{u}_f.
$$
Here, $\mathbf{M}_c$ is the **mass matrix** on the coarse side, with entries $(\mathbf{M}_c)_{ij} = \int_{\Gamma} \phi_i^c \phi_j^c \, \mathrm{d}\Gamma$, and $\mathbf{B}$ is the **coupling [mass matrix](@entry_id:177093)** (or [projection matrix](@entry_id:154479)), with entries $\mathbf{B}_{ij} = \int_{\Gamma} \phi_i^c \phi_j^f \, \mathrm{d}\Gamma$.

The coefficient vector of the projection is then found by solving this system: $\mathbf{u}_c = \mathbf{M}_c^{-1} \mathbf{B} \mathbf{u}_f$. The algebraic operator for the projection is thus $\mathbf{P} = \mathbf{M}_c^{-1} \mathbf{B}$ [@problem_id:3403347]. This operator acts as a transfer function, mapping degrees of freedom on the fine side to their corresponding projected values on the coarse side.

### Basis Selection for the Mortar Space

The structure and conditioning of the [mass matrix](@entry_id:177093) $\mathbf{M}_c$, and thus the efficiency of computing the projection, depend critically on the choice of basis for the mortar space [@problem_id:3403364]. Two common choices for a mortar space of polynomials of degree $p_M$ on a reference interval $[-1,1]$ are:

1.  **Modal Basis (Legendre Polynomials):** Using the Legendre polynomials $\{P_k\}_{k=0}^{p_M}$ as the basis is highly advantageous for affine (straight) interfaces. Due to the [orthogonality property](@entry_id:268007) $\int_{-1}^1 P_i(s) P_j(s) \, \mathrm{d}s = \frac{2}{2i+1}\delta_{ij}$, the mass matrix $\mathbf{M}$ becomes diagonal [@problem_id:3403320]. Inverting a diagonal matrix is trivial. The condition number of this matrix scales as $\mathcal{O}(p_M)$, which is excellent.

2.  **Nodal Basis (Gauss-Lobatto-Legendre Lagrange Polynomials):** Using the Lagrange polynomials $\{\ell_i\}_{i=0}^{p_M}$ associated with the GLL nodes is another option. With exact integration, this basis yields a dense, non-orthogonal mass matrix. Its condition number grows as $\mathcal{O}(p_M^2)$, which is significantly worse than the [modal basis](@entry_id:752055) for high polynomial degrees. However, a common practice is to compute the matrix entries using GLL quadrature with the same nodes as the basis. This technique, known as **[mass lumping](@entry_id:175432)**, results in a [diagonal mass matrix](@entry_id:173002), but the underlying quadrature rule is not exact for the integrand, meaning the resulting projection is no longer the exact $L^2$ projection.

The choice between these bases involves a trade-off. The modal Legendre basis provides a well-conditioned, exact projection on affine interfaces but is less local. The nodal GLL basis is naturally local but leads to an [ill-conditioned system](@entry_id:142776) unless [mass lumping](@entry_id:175432) is employed, which sacrifices the exactness of the projection.

### Advanced Considerations: Curved Geometries and Related Methods

The principles of mortar coupling extend to more complex scenarios.

**Curved Geometries:** When elements are curved, the interface $\Gamma$ is also curved. Integrals on $\Gamma$ are computed by pulling them back to a reference segment $\hat{\Gamma} = [-1,1]$. If the physical interface is parameterized by a mapping $x_f: \hat{\Gamma} \to \Gamma$, the [change of variables](@entry_id:141386) for a line integral introduces a Jacobian factor equal to the length of the tangent vector:
$$
\int_{\Gamma} u v \, \mathrm{d}s = \int_{-1}^{1} (u \circ x_f)(\eta) (v \circ x_f)(\eta) \, \|\mathbf{x}_f'(\eta)\| \, \mathrm{d}\eta.
$$
For [high-order methods](@entry_id:165413), the geometry itself is often represented using the same high-order polynomial basis as the solution, a technique called **[isoparametric mapping](@entry_id:173239)** [@problem_id:3403359]. A key consequence of curved geometries is that the Jacobian $\|\mathbf{x}_f'(\eta)\|$ is generally not constant. This means that even with a modal Legendre basis, the mortar [mass matrix](@entry_id:177093) $\mathbf{M}_{ij} = \int_{-1}^1 P_i(\eta) P_j(\eta) \|\mathbf{x}_f'(\eta)\| \, \mathrm{d}\eta$ is no longer diagonal, presenting additional computational challenges [@problem_id:3403364].

**Primal and Dual Formulations:** The saddle-point formulation is often called the **primal mortar formulation**. An alternative, the **dual mortar formulation**, is designed for computational efficiency. It involves constructing a special biorthogonal basis for the mortar space, which allows the Lagrange multipliers to be eliminated locally at the element level via **[static condensation](@entry_id:176722)**. This results in a smaller global system that is symmetric and positive-definite, but with a more complex sparsity pattern [@problem_id:3403365].

**Connection to Discontinuous Galerkin (DG) Methods:** Mortar methods are closely related to Discontinuous Galerkin (DG) methods. Both frameworks handle discontinuities at element interfaces by enforcing [weak coupling](@entry_id:140994) conditions. A stabilized primal mortar formulation, which adds a penalty term proportional to the projected jump $\tau \int_{\Gamma} \Pi([u]) \Pi([v]) \, ds$, closely resembles the interface terms in a [symmetric interior penalty](@entry_id:755719) DG (SIPG) method. The DG formulation typically includes flux averaging terms and a penalty on the full jump, $\sigma \int_{\Gamma} [u][v] \, ds$. The two interface operators become identical under specific conditions: the mortar space must contain the DG trace space (so that the projection $\Pi$ becomes the [identity operator](@entry_id:204623) on the space of jumps), and the penalty parameters must be equal ($\tau = \sigma$) [@problem_id:3403372]. This connection highlights a deep unity among modern numerical methods for handling nonconformity and discontinuities.