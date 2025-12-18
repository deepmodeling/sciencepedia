## Introduction
In computational electromagnetics, the direct [finite element discretization](@entry_id:193156) of the vector wave equation is a path fraught with numerical peril. While mathematically straightforward, standard approaches often produce solutions contaminated by spurious, non-physical modes, compromising the accuracy of simulations for critical applications like cavity resonance and [wave propagation](@entry_id:144063). This knowledge gap—the discrepancy between the continuous physics and its discrete approximation—necessitates a more robust and principled approach. The [mixed finite element method](@entry_id:166313) emerges as a powerful solution, recasting the problem to explicitly enforce the physical constraints that standard methods fail to capture.

This article provides a comprehensive exploration of mixed finite element formulations, designed to equip you with a deep understanding of this essential numerical technique. You will learn not only how it works but why it is so effective. The journey is structured into three main parts. In "Principles and Mechanisms," we will delve into the mathematical foundations, uncovering how Lagrange multipliers, specialized function spaces, and the elegant structure of the de Rham complex combine to guarantee stable and accurate solutions. Next, "Applications and Interdisciplinary Connections" will showcase the method's versatility, from advanced [multiphysics modeling](@entry_id:752308) in electromagnetics to its profound analogies in fluid and [solid mechanics](@entry_id:164042). Finally, "Hands-On Practices" will bridge theory and application, guiding you through exercises that illuminate the core concepts and their practical implications.

## Principles and Mechanisms

In the numerical analysis of electromagnetic phenomena, the direct [discretization](@entry_id:145012) of second-order vector wave equations often encounters significant challenges. While mathematically elegant, standard formulations can lead to numerical solutions contaminated by non-physical artifacts. The development of mixed finite element formulations provides a robust and principled framework to overcome these difficulties by recasting the problem to explicitly enforce physical constraints that are only implicitly satisfied in the original equations. This chapter elucidates the fundamental principles behind [mixed formulations](@entry_id:167436), the mechanisms by which they operate, and the mathematical structures that guarantee their stability and accuracy.

### The Challenge of Spurious Modes in Standard Formulations

Let us begin with the time-harmonic Maxwell's equations in a source-free, bounded domain $\Omega \subset \mathbb{R}^3$, filled with a material of permittivity $\varepsilon$ and permeability $\mu$. By eliminating the magnetic field $\boldsymbol{H}$, we arrive at the familiar vector wave equation for the electric field $\boldsymbol{E}$:
$$
\nabla \times (\mu^{-1} \nabla \times \boldsymbol{E}) - \omega^2 \varepsilon \boldsymbol{E} = \boldsymbol{0}
$$
This equation is typically complemented by boundary conditions, such as the [perfect electric conductor](@entry_id:753331) (PEC) condition $\boldsymbol{n} \times \boldsymbol{E} = \boldsymbol{0}$ on the boundary $\partial\Omega$. A standard [weak formulation](@entry_id:142897) involves seeking a solution $\boldsymbol{E}$ in a suitable [function space](@entry_id:136890) such that for all test functions $\boldsymbol{F}$ in that same space:
$$
(\mu^{-1} \nabla \times \boldsymbol{E}, \nabla \times \boldsymbol{F}) - \omega^2 (\varepsilon \boldsymbol{E}, \boldsymbol{F}) = 0
$$
where $(\cdot, \cdot)$ denotes the $L^2(\Omega)$ inner product.

While this formulation appears straightforward, its discretization using standard [finite element methods](@entry_id:749389) can be perilous, particularly for eigenvalue problems such as finding the [resonant modes](@entry_id:266261) of a cavity . The numerical spectrum often becomes polluted with **[spurious modes](@entry_id:163321)**—eigenpairs $(\omega_h^2, \boldsymbol{E}_h)$ that are purely artifacts of the [discretization](@entry_id:145012) and do not correspond to any physical resonance.

The root of this problem lies in the structure of the curl-[curl operator](@entry_id:184984), $\nabla \times \mu^{-1} \nabla \times$. A fundamental identity of vector calculus is that the curl of any [gradient field](@entry_id:275893) is zero: $\nabla \times (\nabla p) = \boldsymbol{0}$. Consequently, the kernel (or null space) of the continuous curl-[curl operator](@entry_id:184984) is vast, containing the [infinite-dimensional space](@entry_id:138791) of all [gradient fields](@entry_id:264143). In the full system of Maxwell's equations, this ambiguity is resolved by an additional physical law: Gauss's law for electricity, which in a source-free region dictates that the electric field must be solenoidal, $\nabla \cdot (\varepsilon \boldsymbol{E}) = 0$. A field that is both a gradient, $\boldsymbol{E} = \nabla p$, and solenoidal, $\nabla \cdot (\varepsilon \nabla p) = 0$, must satisfy a Laplace-type equation. With appropriate boundary conditions (e.g., PEC), this implies that such a field must be zero for non-static cases. Thus, the [divergence-free constraint](@entry_id:748603) implicitly filters the unphysical [gradient fields](@entry_id:264143) from the [solution space](@entry_id:200470).

The issue arises when this structure is not perfectly replicated at the discrete level. A finite element space $V_h$ used to approximate $\boldsymbol{E}$ has a discrete curl operator $\nabla_h \times$ and a [discrete gradient](@entry_id:171970) operator $\nabla_h$. It is not guaranteed that the kernel of the discrete curl-[curl operator](@entry_id:184984), when restricted to be discretely [divergence-free](@entry_id:190991), will be trivial. If the discrete divergence constraint is not properly enforced, the discrete problem may admit non-trivial solutions that are essentially [discrete gradient](@entry_id:171970) fields, which have near-zero curl. These appear as spurious solutions, often with near-zero eigenvalues, corrupting the physically meaningful part of the spectrum .

### The Mixed Formulation: Enforcing Constraints with Lagrange Multipliers

The central idea of the [mixed finite element method](@entry_id:166313) is to address this deficiency directly by introducing an auxiliary variable, a **Lagrange multiplier**, to explicitly enforce the divergence constraint. Instead of solving a single equation for $\boldsymbol{E}$, we solve a coupled system for the pair $(\boldsymbol{E}, p)$, where $p$ is the Lagrange multiplier associated with the constraint $\nabla \cdot (\varepsilon \boldsymbol{E}) = 0$.

Let us construct such a formulation . The goal is to find $(\boldsymbol{E}, p)$ that satisfies the vector wave equation and the divergence constraint simultaneously. The resulting [saddle-point problem](@entry_id:178398), in its weak form, seeks a pair $(\boldsymbol{E}, p)$ in a [product space](@entry_id:151533) $V \times Q$ such that for all [test functions](@entry_id:166589) $(\boldsymbol{F}, q) \in V \times Q$:
$$
(\mu^{-1} \nabla \times \boldsymbol{E}, \nabla \times \boldsymbol{F}) - \omega^2 (\varepsilon \boldsymbol{E}, \boldsymbol{F}) + b(\boldsymbol{F}, p) = (\boldsymbol{f}, \boldsymbol{F})
$$
$$
b(\boldsymbol{E}, q) = (g, q)
$$
Here, $\boldsymbol{f}$ and $g$ represent source terms (which are zero for the cavity eigenvalue problem), and $b(\cdot, \cdot)$ is a [bilinear form](@entry_id:140194) that couples the field $\boldsymbol{E}$ and the multiplier $p$. This coupling form is precisely the weak representation of the divergence constraint.

The specific form of $b(\cdot, \cdot)$ depends on the choice of the function space $Q$ for the multiplier. Two common choices arise:

1.  **Multiplier in $H^1(\Omega)$**: If we choose the multiplier space to be $Q = H^1(\Omega)$, the space of scalar functions with square-integrable gradients, we can use [integration by parts](@entry_id:136350) on the constraint equation $\int_\Omega q (\nabla \cdot (\varepsilon \boldsymbol{E})) \, dV = 0$. This yields $-\int_\Omega \nabla q \cdot (\varepsilon \boldsymbol{E}) \, dV$ plus a boundary term. If we choose a multiplier space where functions vanish on the boundary, $Q=H_0^1(\Omega)$, the boundary term disappears. The coupling form becomes $b(\boldsymbol{E}, q) = -(\varepsilon \boldsymbol{E}, \nabla q)$. The resulting [mixed formulation](@entry_id:171379) is: find $(\boldsymbol{E}, p) \in V \times H_0^1(\Omega)$ such that for all $(\boldsymbol{F}, q) \in V \times H_0^1(\Omega)$:
    $$
    (\mu^{-1} \nabla \times \boldsymbol{E}, \nabla \times \boldsymbol{F}) - \omega^2 (\varepsilon \boldsymbol{E}, \boldsymbol{F}) - (\varepsilon \boldsymbol{F}, \nabla p) = (\boldsymbol{f}, \boldsymbol{F})
    $$
    $$
    -(\varepsilon \boldsymbol{E}, \nabla q) = (g, q)
    $$
    This formulation correctly enforces the constraint and eliminates spurious gradient modes .

2.  **Multiplier in $L^2(\Omega)$**: An alternative is to choose the multiplier space to be $Q = L^2(\Omega)$, the space of square-integrable scalar functions. In this case, no [integration by parts](@entry_id:136350) is performed on the constraint term, and the coupling is $b(\boldsymbol{E}, q) = (\nabla \cdot (\varepsilon \boldsymbol{E}), q)$. This requires the field space $V$ to have sufficient regularity for the divergence of its elements to be well-defined in $L^2(\Omega)$.

### The Mathematical Foundation: Vector Sobolev Spaces and Weak Derivatives

A rigorous treatment of [mixed formulations](@entry_id:167436) demands a precise understanding of the underlying [function spaces](@entry_id:143478). The natural settings for [electromagnetic fields](@entry_id:272866) are the **vector Sobolev spaces**.

The space **$H(\mathrm{curl}; \Omega)$** is the space of square-integrable [vector fields](@entry_id:161384) whose curl is also square-integrable:
$$
H(\mathrm{curl}; \Omega) = \{ \boldsymbol{v} \in (L^2(\Omega))^3 : \nabla \times \boldsymbol{v} \in (L^2(\Omega))^3 \}
$$
This is the natural energy space for fields governed by curl-based laws, such as the electric field $\boldsymbol{E}$ and magnetic field $\boldsymbol{H}$. A crucial feature of this space is that its members possess a well-defined **tangential trace** on the boundary $\partial\Omega$. The [trace operator](@entry_id:183665) $\gamma_t: \boldsymbol{v} \mapsto \boldsymbol{n} \times \boldsymbol{v}|_{\partial\Omega}$ maps continuously from $H(\mathrm{curl}; \Omega)$ to a fractional Sobolev space on the boundary, $H^{-1/2}(\mathrm{div}_{\Gamma}; \partial\Omega)$. This allows for the strong imposition of [essential boundary conditions](@entry_id:173524) like the PEC condition, by seeking solutions in the subspace $H_0(\mathrm{curl}; \Omega) = \{ \boldsymbol{v} \in H(\mathrm{curl}; \Omega) : \boldsymbol{n} \times \boldsymbol{v}|_{\partial\Omega} = \boldsymbol{0} \}$ .

The space **$H(\mathrm{div}; \Omega)$** is the space of square-integrable [vector fields](@entry_id:161384) whose divergence is also square-integrable:
$$
H(\mathrm{div}; \Omega) = \{ \boldsymbol{v} \in (L^2(\Omega))^3 : \nabla \cdot \boldsymbol{v} \in L^2(\Omega) \}
$$
This is the natural space for flux densities like $\boldsymbol{D} = \varepsilon\boldsymbol{E}$ and $\boldsymbol{B} = \mu\boldsymbol{H}$. Fields in $H(\mathrm{div}; \Omega)$ have a well-defined **normal trace**. The operator $\gamma_n: \boldsymbol{v} \mapsto \boldsymbol{v} \cdot \boldsymbol{n}|_{\partial\Omega}$ maps continuously from $H(\mathrm{div}; \Omega)$ to the space $H^{-1/2}(\partial\Omega)$. This is essential for handling boundary conditions on normal field components, such as $\boldsymbol{n} \cdot \boldsymbol{B} = 0$ for a PEC boundary or $\boldsymbol{n} \cdot \boldsymbol{D} = 0$ for a PMC boundary .

With this machinery, we can be more precise about the weak divergence. For a field like the [electric flux](@entry_id:266049) density $\boldsymbol{D} = \varepsilon\boldsymbol{E}$ that may only be in $(L^2(\Omega))^3$, its divergence is not an $L^2$ function but a distribution. We define the **weak divergence** $\mathrm{div}_w(\boldsymbol{D})$ as an element of the dual space $H^{-1}(\Omega)$ by its action on test functions $p \in H_0^1(\Omega)$:
$$
\langle \mathrm{div}_w(\boldsymbol{D}), p \rangle := - \int_{\Omega} \boldsymbol{D} \cdot \nabla p \, dx
$$
This definition is a direct consequence of the [divergence theorem](@entry_id:145271), where the choice of test functions from $H_0^1(\Omega)$ (which vanish on the boundary) elegantly circumvents the need for the boundary term involving the normal trace of $\boldsymbol{D}$, a term which is not well-defined for a general $L^2$ vector field . This formal duality pairing underpins the coupling terms in [mixed formulations](@entry_id:167436).

### Stability and the de Rham Complex

The solvability and stability of the discrete saddle-point system are not automatic. They depend critically on a [compatibility condition](@entry_id:171102) between the finite element spaces for the field and the multiplier, known as the **Ladyzhenskaya–Babuška–Brezzi (LBB) condition**, or [inf-sup condition](@entry_id:174538). For the coupling bilinear form $b(\cdot, \cdot)$, the LBB condition states that there must exist a constant $\beta > 0$, independent of the mesh size, such that:
$$
\inf_{q_h \in Q_h} \sup_{\boldsymbol{v}_h \in V_h} \frac{b(\boldsymbol{v}_h, q_h)}{\|\boldsymbol{v}_h\|_{V} \|q_h\|_{Q}} \ge \beta
$$
For the Maxwell problem where we enforce $\nabla \cdot (\varepsilon \boldsymbol{E}) = 0$ with a multiplier $p \in L^2_0(\Omega)$, the condition becomes:
$$
\inf_{q \in L_0^2(\Omega)} \sup_{\boldsymbol{v} \in H_0(\mathrm{curl},\Omega)} \frac{\int_\Omega (\nabla \cdot (\varepsilon \boldsymbol{v})) q \, d\boldsymbol{x}}{\|\boldsymbol{v}\|_{H(\mathrm{curl},\Omega)} \|q\|_{L^2(\Omega)}} \ge \beta
$$
Intuitively, this condition ensures that for any potential instability in the multiplier space (any function $q$), there exists a field $\boldsymbol{v}$ in the primary space that can "see" and control it through a non-zero coupling. A pair of finite element spaces satisfying this condition guarantees a stable and convergent numerical method .

How do we construct finite element spaces that satisfy this crucial condition? The answer lies in a deep mathematical structure known as the **de Rham complex**. This complex is a sequence of spaces and [differential operators](@entry_id:275037) that encodes the fundamental structure of [vector calculus](@entry_id:146888):
$$
H^1(\Omega) \xrightarrow{\nabla} H(\mathrm{curl}; \Omega) \xrightarrow{\nabla \times} H(\mathrm{div}; \Omega) \xrightarrow{\nabla \cdot} L^2(\Omega) \rightarrow 0
$$
The property that the composition of any two successive operators is zero (e.g., $\nabla \times (\nabla p) = \boldsymbol{0}$) is built in. On a [simply connected domain](@entry_id:197423), this sequence is **exact**, which means the image of each operator is precisely the kernel of the next one . For example, any curl-free field in $H(\mathrm{curl}; \Omega)$ is the gradient of some potential in $H^1(\Omega)$.

The key to stable [mixed finite element methods](@entry_id:165231) is to use families of elements that create a discrete version of this [exact sequence](@entry_id:149883). This approach is known as **Finite Element Exterior Calculus (FEEC)**. The canonical element families that achieve this are:
*   **Lagrange elements** (nodal-based) for approximating functions in $H^1(\Omega)$.
*   **Nédélec elements** (edge-based) for approximating fields in $H(\mathrm{curl}; \Omega)$. The lowest-order Nédélec space on a tetrahedron consists of vector fields of the form $\boldsymbol{v}(\boldsymbol{x}) = \boldsymbol{a} + \boldsymbol{b} \times \boldsymbol{x}$, with degrees of freedom defined as the [line integral](@entry_id:138107) of the field's tangential component along each of the 6 edges, $\int_{e_\ell} \boldsymbol{v} \cdot \boldsymbol{t}_\ell \, ds$. This construction naturally ensures the continuity of the tangential component across element faces, which is the conformity requirement for $H(\mathrm{curl}; \Omega)$ .
*   **Raviart-Thomas elements** (face-based) for approximating fields in $H(\mathrm{div}; \Omega)$. The lowest-order Raviart-Thomas space on a tetrahedron consists of [vector fields](@entry_id:161384) of the form $\boldsymbol{v}(\boldsymbol{x}) = \boldsymbol{a} + b \boldsymbol{x}$, with degrees of freedom defined as the flux of the field's normal component across each of the 4 faces, $\int_{f_k} \boldsymbol{v} \cdot \boldsymbol{n}_k \, dS$. This ensures normal component continuity, the conformity requirement for $H(\mathrm{div}; \Omega)$ .
*   **Discontinuous [piecewise polynomials](@entry_id:634113)** for approximating functions in $L^2(\Omega)$.

When these "compatible" element families are used together, they form a discrete de Rham complex that satisfies a discrete LBB condition. This structure-preserving property is the ultimate reason for their success in eliminating spurious modes .

### The Algebraic Viewpoint and Convergence

The mixed [weak formulation](@entry_id:142897) leads to a linear system with a characteristic block-operator structure. For a cavity problem, this takes the form :
$$
\begin{pmatrix} A  B^T \\ B  0 \end{pmatrix} \begin{pmatrix} \boldsymbol{E} \\ p \end{pmatrix} = \begin{pmatrix} \boldsymbol{0} \\ 0 \end{pmatrix}
$$
Here, $A$ represents the [discretization](@entry_id:145012) of the $(\nabla \times, \nabla \times) - \omega^2(\cdot, \cdot)$ operator, and $B$ represents the discrete [divergence operator](@entry_id:265975) coupling the two fields. If the operator $A$ is invertible, one can formally eliminate the field $\boldsymbol{E} = -A^{-1}B^T p$, and substitute it into the second equation to get an equation purely for the multiplier $p$: $(-B A^{-1} B^T) p = 0$. The operator $S = -B A^{-1} B^T$ is known as the **Schur complement**. This shows how the introduction of the constraint effectively modifies the original problem operator.

Finally, for the challenging case of eigenvalue problems, the use of compatible elements provides a rigorous guarantee of convergence. The theoretical underpinning is the **discrete compactness property**. This property asserts that a sequence of discrete fields, chosen from the discretely divergence-free subspace and having uniformly bounded curl-norm, possesses a subsequence that converges strongly in $L^2(\Omega)$. This discrete property mirrors a continuous compactness result for Maxwell's equations (Weck's selection theorem). It is a direct consequence of the FEEC framework, specifically the existence of uniformly bounded, commuting interpolation operators. The discrete compactness property is the final, crucial ingredient that, when combined with abstract spectral [approximation theory](@entry_id:138536), proves that the eigenvalues computed with a compatible [mixed finite element method](@entry_id:166313) will converge to the true physical eigenvalues, free from spurious mode pollution  .