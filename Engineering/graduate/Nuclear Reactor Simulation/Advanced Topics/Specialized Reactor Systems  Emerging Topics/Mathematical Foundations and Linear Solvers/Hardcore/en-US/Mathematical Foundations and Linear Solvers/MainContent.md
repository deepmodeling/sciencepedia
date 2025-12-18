## Introduction
The design and analysis of nuclear reactors rely heavily on high-fidelity numerical simulation, a field where physical principles are translated into predictive computational models. This translation, however, is not a simple [one-to-one mapping](@entry_id:183792); it is a rigorous process built upon a sophisticated mathematical foundation. The journey from the continuous equations of neutron behavior to a computable solution involves complex mathematical transformations that give rise to formidable computational challenges, namely solving vast [systems of linear equations](@entry_id:148943). This article provides a graduate-level exploration of the essential mathematical tools and [numerical algorithms](@entry_id:752770) that make modern reactor simulation possible.

The content is structured to guide you from fundamental theory to practical application. In the first chapter, **Principles and Mechanisms**, we will delve into the mathematical heart of reactor physics, examining the properties of the transport and diffusion operators, establishing their well-posedness using [functional analysis](@entry_id:146220), and exploring how [discretization methods](@entry_id:272547) transform them into large matrix problems. The second chapter, **Applications and Interdisciplinary Connections**, bridges theory and practice by demonstrating how [iterative linear solvers](@entry_id:1126792), such as Krylov subspace methods, and advanced [preconditioning techniques](@entry_id:753685) are applied to solve the core eigenvalue and fixed-source problems in reactor analysis. Finally, the **Hands-On Practices** section offers targeted problems to solidify your understanding of key algorithms like the Conjugate Gradient method and the mechanics of [preconditioning](@entry_id:141204). We begin by examining the foundational principles that govern the mathematical models of reactor physics.

## Principles and Mechanisms

The mathematical simulation of nuclear reactors is built upon a hierarchy of physical models, each with distinct mathematical characteristics that dictate the choice of numerical algorithms and solution strategies. This chapter delves into the fundamental principles governing these models, focusing on the transition from continuous partial differential equations (PDEs) to discrete algebraic systems and the advanced linear solvers required to tackle them. We will explore the [functional analysis](@entry_id:146220) framework that ensures the [well-posedness](@entry_id:148590) of these models, the discretization techniques that render them computable, and the iterative methods designed to efficiently solve the resulting large-scale linear and [eigenvalue problems](@entry_id:142153).

### From Physics to Mathematical Models: Operators in Reactor Physics

At the heart of reactor analysis are mathematical operators that describe the balance of neutrons in phase space (position, energy, and direction). The fidelity of a simulation is largely determined by the choice of operator.

#### The Transport Operator

The most fundamental description at the macroscopic level is given by the linear Boltzmann transport equation. In a simplified, steady-state, monoenergetic form, this equation can be written as:
$$
\mathbf{\Omega}\cdot\nabla \psi(\mathbf{r},\mathbf{\Omega}) + \Sigma_{t}(\mathbf{r})\,\psi(\mathbf{r},\mathbf{\Omega})
= \int_{4\pi} \Sigma_{s}(\mathbf{r}, \mathbf{\Omega}' \to \mathbf{\Omega})\,\psi(\mathbf{r},\mathbf{\Omega}')\,\mathrm{d}\mathbf{\Omega}' + q(\mathbf{r},\mathbf{\Omega})
$$
Here, $\psi(\mathbf{r},\mathbf{\Omega})$ is the [angular neutron flux](@entry_id:1121012) at position $\mathbf{r}$ for neutrons traveling in direction $\mathbf{\Omega}$, $\Sigma_{t}$ is the total interaction cross section, $\Sigma_{s}$ is the [differential scattering cross section](@entry_id:1123684), and $q$ is an external source.

The transport operator, which includes the streaming term $\mathbf{\Omega}\cdot\nabla$, the collision term $\Sigma_t \psi$, and the integral scattering term, is a first-order integro-differential operator. A simplified form, capturing the essential nature of the streaming component, can be represented by an operator $\mathcal{T}\psi = \mathbf{b}(x) \cdot \nabla \psi(x) + \sigma(x) \psi(x)$, where $\mathbf{b}$ represents a streaming direction and $\sigma$ a removal cross section . This operator is of a **first-order hyperbolic** nature. A critical mathematical property of such transport operators, when considered on a Hilbert space like $L^2(\Omega)$ with appropriate inflow boundary conditions, is that they are generally **non-self-adjoint**. This means that the operator is not equal to its adjoint, a fact that can be verified by applying integration by parts and observing that boundary terms do not vanish in a way that preserves symmetry. Consequently, transport operators are also typically **non-normal**, meaning they do not commute with their adjoint ($\mathcal{T}^*\mathcal{T} \neq \mathcal{T}\mathcal{T}^*$). This [non-normality](@entry_id:752585) has profound implications: the spectrum of eigenvalues can be complex, and the choice of iterative solvers must be suited for non-symmetric systems, such as the Generalized Minimal Residual (GMRES) method.

#### The Diffusion Operator

For many reactor applications, particularly in systems where [neutron scattering](@entry_id:142835) is nearly isotropic and the flux is a slowly varying function of angle, the transport equation can be simplified to the [neutron diffusion equation](@entry_id:1128691). In its standard steady-state, one-group form, the equation is:
$$
-\nabla \cdot (D(\mathbf{r}) \nabla \phi(\mathbf{r})) + \Sigma_a(\mathbf{r}) \phi(\mathbf{r}) = S(\mathbf{r})
$$
Here, $\phi(\mathbf{r})$ is the [scalar flux](@entry_id:1131249) (the integral of the angular flux over all directions), $D$ is the diffusion coefficient, $\Sigma_a$ is the absorption cross section, and $S$ is a source term. The operator $\mathcal{L}\phi = -\nabla \cdot (D \nabla \phi) + \Sigma_a \phi$ is a **second-order elliptic** partial differential operator.

In stark contrast to the transport operator, the diffusion operator $\mathcal{L}$ possesses a high degree of symmetry. When defined on an appropriate [function space](@entry_id:136890) with [homogeneous boundary conditions](@entry_id:750371) (e.g., zero flux at the boundary), the operator is **self-adjoint** . This property ensures that its spectrum of eigenvalues is purely real. This fundamental difference in mathematical structure—non-self-adjoint hyperbolic for transport versus self-adjoint elliptic for diffusion—is the primary determinant for the divergent paths of their numerical treatment.

### The Functional Analysis Framework for Diffusion Problems

To rigorously analyze the diffusion equation and construct robust numerical methods like the Finite Element Method (FEM), we must move from the "strong" form of the PDE to its "weak" formulation. This transition requires the tools of [functional analysis](@entry_id:146220).

#### Weak Formulation and Sobolev Spaces

The strong form of the diffusion equation requires the flux $\phi$ to be twice differentiable, a condition that is too restrictive for problems with [material discontinuities](@entry_id:751728) or complex geometries. The [weak formulation](@entry_id:142897) relaxes these requirements. We derive it by multiplying the equation by an arbitrary "[test function](@entry_id:178872)" $v$ and integrating over the reactor domain $\Omega$:
$$
\int_{\Omega} \left( -\nabla \cdot (D \nabla \phi) + \Sigma_a \phi \right) v \, d\mathbf{r} = \int_{\Omega} S v \, d\mathbf{r}
$$
Applying integration by parts (Green's first identity) to the diffusion term yields:
$$
\int_{\Omega} D \nabla \phi \cdot \nabla v \, d\mathbf{r} - \int_{\partial \Omega} v (D \nabla \phi \cdot \mathbf{n}) \, dS + \int_{\Omega} \Sigma_a \phi v \, d\mathbf{r} = \int_{\Omega} S v \, d\mathbf{r}
$$
The [weak form](@entry_id:137295) is designed to handle boundary conditions naturally. For a homogeneous Dirichlet boundary condition ($\phi = 0$ on $\partial\Omega$), we seek a solution $\phi$ and choose test functions $v$ from a space where functions vanish on the boundary. This choice makes the boundary integral $\int_{\partial \Omega} \dots dS$ disappear.

This leads us to the appropriate [function space](@entry_id:136890). The [weak form](@entry_id:137295) involves integrals of first derivatives of $\phi$ and $v$. The natural setting is therefore a space of functions that are themselves square-integrable and whose first derivatives are also square-integrable. This is the **Sobolev space** $H^1(\Omega)$. For problems with homogeneous Dirichlet boundary conditions, we use the subspace $H_0^1(\Omega)$, which contains functions in $H^1(\Omega)$ that are zero on the boundary $\partial\Omega$. Thus, $H_0^1(\Omega)$ is the natural space for both the solution and the test functions .

#### The Bilinear Form: Boundedness and Coercivity

The weak problem can be stated abstractly: find $\phi \in H_0^1(\Omega)$ such that $a(\phi, v) = L(v)$ for all $v \in H_0^1(\Omega)$, where the **[bilinear form](@entry_id:140194)** $a(\cdot, \cdot)$ and [linear functional](@entry_id:144884) $L(\cdot)$ are:
$$
a(u,v) = \int_{\Omega} (D \nabla u \cdot \nabla v + \Sigma_a u v) \, d\mathbf{r}
$$
$$
L(v) = \int_{\Omega} S v \, d\mathbf{r}
$$
The [existence and uniqueness](@entry_id:263101) of a solution to this problem are guaranteed by the **Lax-Milgram theorem**, provided the [bilinear form](@entry_id:140194) $a(u,v)$ is both bounded and **coercive** on the Hilbert space $H_0^1(\Omega)$. Boundedness means $|a(u,v)| \le C \|u\|_{H^1} \|v\|_{H^1}$ for some constant $C$, which holds if $D$ and $\Sigma_a$ are bounded.

Coercivity is a more profound property, acting as a statement of stability. It requires that there exists a constant $\alpha > 0$ such that $a(u,u) \ge \alpha \|u\|_{H^1}^2$ for all $u \in H_0^1(\Omega)$. This property arises directly from the physics. Given that $D(\mathbf{r}) \ge D_{\min} > 0$ and $\Sigma_a(\mathbf{r}) \ge \Sigma_{a,\min} \ge 0$, we have:
$$
a(u,u) = \int_{\Omega} D |\nabla u|^2 \, d\mathbf{r} + \int_{\Omega} \Sigma_a |u|^2 \, d\mathbf{r} \ge D_{\min} \int_{\Omega} |\nabla u|^2 \, d\mathbf{r} + \Sigma_{a,\min} \int_{\Omega} |u|^2 \, d\mathbf{r}
$$
If we define the norm on $H_0^1(\Omega)$ by $\|u\|_{H_0^1}^2 = \int_{\Omega} (|\nabla u|^2 + |u|^2) \, d\mathbf{r}$, it is straightforward to show that $a(u,u) \ge \alpha \|u\|_{H_0^1}^2$ with $\alpha = \min(D_{\min}, \Sigma_{a,\min})$ . This directly connects the [well-posedness](@entry_id:148590) of the mathematical model to the physical constraint that diffusion is present and absorption is non-negative.

A crucial tool in this space is the **Poincaré inequality**, which for a bounded domain states that there is a constant $C_P$ such that $\int_{\Omega} |u|^2 \, d\mathbf{r} \le C_P \int_{\Omega} |\nabla u|^2 \, d\mathbf{r}$ for all $u \in H_0^1(\Omega)$. This implies that the [seminorm](@entry_id:264573) $|\cdot|_{H^1}$ (involving only the gradient) is equivalent to the full $H^1$ norm on $H_0^1(\Omega)$. Therefore, the mapping $(u,v)_{H_0^1} = \int_\Omega \nabla u \cdot \nabla v \, d\mathbf{r}$ defines a valid inner product on $H_0^1(\Omega)$, and the diffusion term alone is coercive on this space .

### The k-Eigenvalue Problem: Spectral Theory

The central problem in reactor physics is determining the criticality of the system, which is formulated as a [generalized eigenvalue problem](@entry_id:151614):
$$
-\nabla \cdot (D \nabla \phi) + \Sigma_a \phi = \frac{1}{k} \nu \Sigma_f \phi
$$
Here, $\nu\Sigma_f$ is the neutron production cross section and $k$ is the effective multiplication factor, or [k-eigenvalue](@entry_id:1126859). The weak form is: find $(\phi, k)$ such that $\phi \in H_0^1(\Omega)$, $\phi \neq 0$, and
$$
a(\phi, v) = \frac{1}{k} b(\phi, v) \quad \text{for all } v \in H_0^1(\Omega),
$$
where $a(\cdot, \cdot)$ is the diffusion/absorption form and $b(u,v) = \int_{\Omega} \nu\Sigma_f u v \, d\mathbf{r}$ is the fission production form.

The spectral properties of this problem can be rigorously established using [operator theory](@entry_id:139990) . We can define an operator $T$ that maps a fission source distribution to the resulting flux distribution. This operator can be shown to be **compact** on the appropriate function space. Compactness is a powerful property, stemming from the fact that the [diffusion operator](@entry_id:136699) "smooths" functions, and it is formally guaranteed by the Rellich-Kondrachov [compact embedding](@entry_id:263276) theorem. Furthermore, because the [bilinear forms](@entry_id:746794) $a(\cdot,\cdot)$ and $b(\cdot,\cdot)$ are symmetric, the operator $T$ can be shown to be **self-adjoint** with respect to the [energy inner product](@entry_id:167297) $a(\cdot,\cdot)$.

The [spectral theorem](@entry_id:136620) for compact, [self-adjoint operators](@entry_id:152188) ensures that the spectrum of eigenvalues $k$ is real and discrete. To prove the existence of a unique, largest positive eigenvalue $k_0$ (the fundamental mode) corresponding to a non-negative flux, one must invoke the **Krein-Rutman theorem**. This theorem, a generalization of the Perron-Frobenius theorem for matrices to [infinite-dimensional spaces](@entry_id:141268), applies to positive operators. Since a positive fission source physically produces a positive neutron flux, the operator $T$ is positive. The Krein-Rutman theorem then guarantees that the spectral radius of $T$ is a simple eigenvalue, $k_0$, with an associated [eigenfunction](@entry_id:149030) $\phi_0$ that can be chosen to be strictly positive inside the domain. This positive [eigenfunction](@entry_id:149030) is the physically meaningful fundamental flux distribution.

### Discretization Methods: From PDEs to Linear Algebra

To solve these equations on a computer, we must discretize them, transforming the infinite-dimensional PDE problem into a finite-dimensional system of algebraic equations.

#### Methods for the Transport Equation

Two primary families of methods are used for the transport equation.

The **Spherical Harmonics ($P_N$) Method** approximates the angular dependence of the flux by expanding it in a truncated series of [spherical harmonics](@entry_id:156424), $Y_{\ell m}(\mathbf{\Omega})$ . Projecting the transport equation onto this basis transforms the single integro-differential equation into a coupled system of first-order PDEs for the expansion coefficients (moments) $\psi_{\ell m}(\mathbf{r})$. A key insight arises from the parity of the spherical harmonics ($Y_{\ell m}(-\mathbf{\Omega}) = (-1)^\ell Y_{\ell m}(\mathbf{\Omega})$). The streaming operator, $\mathbf{\Omega} \cdot \nabla$, is an odd-[parity operator](@entry_id:148434); it couples even-degree moments only with odd-degree moments, and vice versa. This allows the system to be partitioned into two sets of equations: one for even-parity moments and one for odd-parity moments. One set can then be algebraically eliminated to yield a closed, second-order, diffusion-like PDE system for the remaining set. For instance, eliminating the odd moments yields the so-called **even-parity transport equation**, providing a rigorous mathematical bridge between transport and diffusion theories.

The **Discrete Ordinates ($S_N$) Method** takes a different approach . Instead of expanding the angular dependence, it replaces the continuous angular variable $\mathbf{\Omega}$ with a discrete set of quadrature directions $\{\mu_n\}$ and associated weights $\{w_n\}$. The integral in the scattering source term is replaced by a weighted sum over these discrete directions. This results in a large, coupled system of [first-order differential equations](@entry_id:173139), one for each discrete direction $\mu_m$:
$$
\mu_m \frac{d\psi_m(x)}{dx} + \Sigma_t(x) \psi_m(x) = S_s(x, \mu_m) + Q_{ext}(x, \mu_m)
$$
The scattering source $S_s(x, \mu_m)$ for an outgoing direction $\mu_m$ is computed by summing the contributions from fluxes $\psi_n(x)$ in all other incoming directions $\mu_n$. This coupling is expressed through a **[scattering matrix](@entry_id:137017)**, whose entry $(m,n)$ represents the probability of scattering from direction $n$ into direction $m$. If the scattering kernel is expanded in Legendre polynomials, the entry takes the form $C_{mn}(x) = w_{n} \sum_{l=0}^{l_{\max}} \left( \frac{2l+1}{2} \right) \Sigma_{s}^{l}(x) P_{l}(\mu_{m}) P_{l}(\mu_{n})$.

#### Methods for the Diffusion Equation (Finite Element Method)

The Finite Element Method (FEM) is a powerful technique for discretizing the [weak form](@entry_id:137295) of the diffusion equation. The domain $\Omega$ is partitioned into a mesh of simple geometric elements (e.g., triangles or tetrahedra). Within each element, the solution $\phi$ is approximated by a [linear combination](@entry_id:155091) of simple, locally-defined polynomial basis functions (shape functions), $\phi_h(\mathbf{r}) = \sum_j \phi_j N_j(\mathbf{r})$, where $\phi_j$ are the unknown flux values at the element nodes.

Substituting this approximation into the [weak form](@entry_id:137295) and choosing the test functions $v$ to be the basis functions $N_i$ (the Galerkin method) converts the PDE into a matrix system $A\boldsymbol{\phi} = \mathbf{b}$. The matrix $A$ is known as the [global stiffness matrix](@entry_id:138630) and is assembled from element-level contributions. On each element $T_e$, an **[element stiffness matrix](@entry_id:139369)** $K_e$ is computed, with entries $(K_e)_{ij} = a(N_j, N_i)|_{T_e}$. For the diffusion equation, this gives:
$$
(K_e)_{ij} = \int_{T_e} (D \nabla N_j \cdot \nabla N_i + \Sigma_a N_i N_j) \, d\mathbf{r}
$$
As a concrete example, for a 2D triangular element with constant coefficients $D$ and $\Sigma_a$, using linear shape functions, this integral can be evaluated analytically . The resulting element matrix $K_e$ is inherently **symmetric** because the [bilinear form](@entry_id:140194) $a(\cdot,\cdot)$ is symmetric. Furthermore, if $D > 0$ and $\Sigma_a \ge 0$, the matrix $K_e$ can be shown to be **[positive definite](@entry_id:149459)**, a property inherited directly from the coercivity of the continuous [bilinear form](@entry_id:140194). The [global stiffness matrix](@entry_id:138630) $A$, formed by summing these element matrices, will also be symmetric and [positive definite](@entry_id:149459) (SPD).

### Solving the Linear Systems: Iterative Methods

Discretization transforms the PDE into a large, sparse linear system $Ax=b$ or an [eigenvalue problem](@entry_id:143898). Direct solvers like LU factorization become prohibitively expensive for realistic 3D problems, necessitating the use of [iterative methods](@entry_id:139472).

#### Characteristics of the System Matrix

The performance of iterative solvers is critically dependent on the properties of the [system matrix](@entry_id:172230) $A$. A key metric is the **condition number**, $\kappa_2(A) = \|A\|_2 \|A^{-1}\|_2$, which for an SPD matrix is the ratio of its largest to its [smallest eigenvalue](@entry_id:177333), $\lambda_{\max}/\lambda_{\min}$. A large condition number signifies an [ill-conditioned system](@entry_id:142776) that is difficult to solve.

The condition number of the discrete [diffusion operator](@entry_id:136699) is highly sensitive to both physical and numerical parameters .
1.  **Mesh Refinement**: For a pure diffusion problem ($-\nabla^2 \phi = s$), as the mesh spacing $h$ goes to zero, $\lambda_{\max}$ grows like $h^{-2}$ while $\lambda_{\min}$ approaches a constant. Consequently, the condition number deteriorates rapidly, with $\kappa(A) \propto h^{-2}$.
2.  **Coefficient Heterogeneity**: Large spatial variations in the diffusion coefficient $D(\mathbf{r})$, quantified by the ratio $D_{\max}/D_{\min}$, directly increase the condition number. Even localized heterogeneities can significantly degrade solver performance.
3.  **Absorption**: The presence of a sufficiently large absorption term $\Sigma_a$ adds a positive constant to the eigenvalues of the diffusion part. If absorption is strong enough to dominate diffusion (i.e., $\Sigma_{a,\min} \gg D_{\max}h^{-2}$), the eigenvalues of $A$ are clustered around the values of $\Sigma_a$. In this absorption-dominated regime, the condition number becomes largely independent of the mesh size $h$ and is approximated by $\kappa(A) \approx \Sigma_{a,\max}/\Sigma_{a,\min}$.

#### Krylov Subspace Methods

Krylov Subspace Methods (KSMs) are the state-of-the-art for [solving large sparse linear systems](@entry_id:1131946). They operate by generating a sequence of approximate solutions within a growing subspace called the **Krylov subspace**, defined for an initial residual $r_0=b-Ax_0$ as:
$$
\mathcal{K}_m(A,r_0) = \operatorname{span}\{r_0, A r_0, \dots, A^{m-1} r_0\}
$$
KSMs find the "best" approximate solution $x_m$ in the affine space $x_0 + \mathcal{K}_m(A,r_0)$. The definition of "best" distinguishes the main families of KSMs .

**Minimal residual methods**, a prominent family, select the solution $x_m$ that minimizes the Euclidean norm of the corresponding residual, $\|r_m\|_2 = \|b-Ax_m\|_2$. This is geometrically equivalent to enforcing that the new residual $r_m$ is orthogonal to the subspace $A\mathcal{K}_m(A,r_0)$.
*   For general [non-symmetric matrices](@entry_id:153254), such as those from transport discretizations, the **Generalized Minimal Residual (GMRES)** method is used. It employs the Arnoldi process to build an [orthonormal basis](@entry_id:147779) for the Krylov subspace. This process results in a small, upper-Hessenberg [least-squares problem](@entry_id:164198) to be solved at each iteration. A drawback is its "long recurrence" nature, requiring storage of the entire basis, which can become memory-intensive.
*   For [symmetric matrices](@entry_id:156259) (even if indefinite), the **Minimal Residual (MINRES)** method is a more efficient choice. It uses the Lanczos process, a specialization of Arnoldi for [symmetric matrices](@entry_id:156259), which generates the basis with a short-term recurrence. This dramatically reduces memory and computational costs per iteration.

#### Preconditioning

The convergence rate of KSMs depends heavily on the condition number and [eigenvalue distribution](@entry_id:194746) of $A$. **Preconditioning** is a technique to transform the original system $Ax=b$ into an equivalent one that is easier to solve. For example, in **[left preconditioning](@entry_id:165660)**, one solves $M^{-1}Ax = M^{-1}b$, where $M$ is the preconditioner matrix. The goal is to choose $M$ such that it is a good approximation to $A$ (so $M^{-1}A$ is close to the identity matrix and has a small condition number) and such that systems involving $M$ are easy to solve. The KSM is then applied to the preconditioned operator $M^{-1}A$, with the Krylov subspace being built from this new operator and the preconditioned residual $M^{-1}r_0$ .

### Error Control and Quantities of Interest

The ultimate goal of a reactor simulation is not to solve an algebraic system but to compute physical quantities of interest (QoIs), such as the multiplication factor $k_{\text{eff}}$ and the power distribution, to within a specified accuracy. This requires a rigorous framework for error control.

#### Error vs. Residual for Linear Solves

When an iterative solver is used, it is typically stopped when the norm of the residual $r_k = b - Ax_k$ falls below a tolerance. However, a small residual does not always imply a small error $e_k = x - x_k$. The relationship between the two is $r_k = A e_k$. In the standard Euclidean norm, this leads to the bound:
$$
\frac{1}{\kappa_2(A)} \frac{\|r_k\|_2}{\|r_0\|_2} \le \frac{\|e_k\|_2}{\|e_0\|_2} \le \kappa_2(A) \frac{\|r_k\|_2}{\|r_0\|_2}
$$
For [ill-conditioned systems](@entry_id:137611) where $\kappa_2(A) \gg 1$, the [relative error](@entry_id:147538) can be much larger than the relative residual. A more robust approach uses problem-adapted norms . For SPD systems arising from diffusion, the natural norm is the **[energy norm](@entry_id:274966)**, $\|v\|_A = \sqrt{v^\top A v}$. For this norm, there is an exact and computable identity between the error and the residual:
$$
\|e_k\|_A = \|r_k\|_{A^{-1}} = \sqrt{r_k^\top A^{-1} r_k}
$$
This identity means that the [energy norm](@entry_id:274966) of the error is equal to the $A^{-1}$-norm of the residual. Although $\|r_k\|_{A^{-1}}$ is not trivial to compute, it can be tracked within certain KSMs (like the Conjugate Gradient method), providing a much more reliable stopping criterion than one based on the Euclidean norm of the residual.

#### Error Control for the Eigenvalue Problem

Error analysis can be extended to the outer eigenvalue iteration for $k_{\text{eff}}$. For the symmetric [generalized eigenvalue problem](@entry_id:151614) $F\phi = \lambda A\phi$ (with $\lambda=1/k_{\text{eff}}$), the error in an approximate eigenvalue $\lambda$ can be bounded by the norm of the **eigenresidual** $g = F\phi - \lambda A\phi$. A key result, derived from spectral [perturbation theory](@entry_id:138766), is that:
$$
|\lambda - \lambda^\star| \le \|g\|_{A^{-1}}
$$
where $\lambda^\star$ is the exact eigenvalue. This powerful inequality relates the error in the eigenvalue to a computable residual quantity in the $A^{-1}$-norm. Using a first-order Taylor expansion, this translates directly into a bound on the error in the multiplication factor:
$$
|k_{\text{eff}} - k_{\text{eff}}^\star| \approx k_{\text{eff}}^2 |\lambda - \lambda^\star| \le k_{\text{eff}}^2 \|g\|_{A^{-1}}
$$
This provides a rigorous method for choosing the outer iteration tolerance: to achieve a target accuracy on $k_{\text{eff}}$, one must drive the $A^{-1}$-norm of the eigenresidual below the target divided by $k_{\text{eff}}^2$ . This also highlights the importance of adaptive tolerances for the inner linear solves. To prevent the outer iteration from stagnating, the accuracy of the inner solves must be progressively tightened as the outer iteration converges and the eigenresidual decreases.