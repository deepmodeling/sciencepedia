## Introduction
Variational principles represent a cornerstone of modern physics and engineering, offering a profoundly elegant and powerful alternative to the traditional, force-balance-based formulation of continuum mechanics. Instead of focusing on local differential equations, this framework posits that the behavior of a physical system is governed by a [global optimization](@entry_id:634460) principle, such as minimizing total energy or making an [action functional](@entry_id:169216) stationary. This perspective not only provides deeper physical insight but also serves as the indispensable foundation for many advanced computational methods used in [geophysics](@entry_id:147342). This article bridges the gap between abstract theory and practical application, demonstrating how these principles are leveraged to model complex geophysical phenomena.

The article is structured to guide the reader from foundational theory to state-of-the-art applications. In the first chapter, **Principles and Mechanisms**, we will establish the mathematical language of [continuum mechanics](@entry_id:155125), including [kinematics](@entry_id:173318), [stress measures](@entry_id:198799), and the formulation of core [variational principles](@entry_id:198028) like Hamilton's principle and the [principle of minimum potential energy](@entry_id:173340). The second chapter, **Applications and Interdisciplinary Connections**, will showcase the versatility of this framework by exploring its use in geodynamics, [seismology](@entry_id:203510), and [multiphysics coupling](@entry_id:171389), culminating in its role in solving [large-scale inverse problems](@entry_id:751147) via the [adjoint-state method](@entry_id:633964). Finally, the **Hands-On Practices** chapter provides concrete exercises to solidify the understanding of these concepts, translating theoretical knowledge into practical problem-solving skills.

## Principles and Mechanisms

Variational principles provide a powerful and elegant framework for formulating the laws of [continuum mechanics](@entry_id:155125). Instead of starting with local force balances, these principles posit that the physical behavior of a system is governed by the stationarity of a global scalar quantity, typically an action or [energy functional](@entry_id:170311). This perspective not only offers deeper physical insight but also serves as the natural foundation for modern computational methods, such as the [finite element method](@entry_id:136884). This chapter elucidates the core principles and mechanisms, beginning with the fundamental description of deformation and stress, proceeding to the central [variational principles](@entry_id:198028), and culminating in advanced applications for handling constraints, dissipation, and inverse problems.

### Kinematics of Deformation: The Lagrangian Perspective

To describe the motion of a deformable body, we must first establish a coordinate system. In the **Lagrangian**, or **material description**, we track the motion of individual material particles. We define a fixed, undeformed **reference configuration**, denoted $\mathcal{B}_0$, in which each particle is identified by a position vector $X$. As the body deforms, it occupies a time-dependent **current configuration**, $\mathcal{B}_t$, where the same particle is now at position $x$. The motion is thus completely described by the **deformation map** $\varphi$, which gives the current position of a particle as a function of its original position and time: $x = \varphi(X, t)$.

The **displacement field**, $u(X, t)$, is the vector connecting a particle's initial position to its final position:
$$
u(X, t) = \varphi(X, t) - X
$$
To quantify local deformation, we examine how an infinitesimal material vector $dX$ in the reference configuration is transformed into a vector $dx$ in the current configuration. By the [chain rule](@entry_id:147422), $dx = \frac{\partial \varphi}{\partial X} dX$. The second-order tensor that performs this mapping is the **[deformation gradient](@entry_id:163749)**, denoted by $F$:
$$
F = \nabla_X \varphi(X, t) = \frac{\partial \varphi}{\partial X}
$$
where $\nabla_X$ is the gradient with respect to the material coordinates $X$. The [deformation gradient](@entry_id:163749) is a fundamental measure of local deformation, encompassing local stretching, shearing, and rotation. It can also be expressed in terms of the [displacement field](@entry_id:141476):
$$
F = \nabla_X (X + u) = \nabla_X X + \nabla_X u = I + \nabla_X u
$$
where $I$ is the second-order identity tensor.

A pure measure of strain should be independent of rigid body rotations. The deformation gradient itself does not satisfy this, as a pure rotation results in an orthogonal $F$ ($F^T F = I$) that is not the identity tensor. To construct a proper strain measure, we compare the squared length of a material element before and after deformation. The initial squared length is $ds_0^2 = dX \cdot dX = dX^T I dX$. The squared length after deformation is $ds^2 = dx \cdot dx$. Expressing $dx$ in terms of $dX$ using the deformation gradient, we get:
$$
ds^2 = (F dX)^T (F dX) = dX^T F^T F dX
$$
The tensor $C = F^T F$ is called the **Right Cauchy-Green deformation tensor**. It characterizes the local change in metric properties, "pulled back" to the reference configuration. The change in squared length is then $ds^2 - ds_0^2 = dX^T (C - I) dX$. From this, we define the **Green-Lagrange strain tensor** $E$ as the symmetric tensor that provides half of this change:
$$
E = \frac{1}{2} (C - I) = \frac{1}{2} (F^T F - I)
$$
By substituting $F = I + \nabla_X u$, we can express the Green-Lagrange strain in terms of the [displacement gradient](@entry_id:165352):
$$
E = \frac{1}{2} \left( (I + (\nabla_X u)^T)(I + \nabla_X u) - I \right) = \frac{1}{2} \left( \nabla_X u + (\nabla_X u)^T + (\nabla_X u)^T (\nabla_X u) \right)
$$
The tensor $E$ is a true measure of strain: it is zero if and only if the deformation is a [rigid body motion](@entry_id:144691). As it is defined entirely in the reference configuration, it is an objective, material measure suitable for formulating constitutive laws in finite-strain elasticity . For infinitesimal deformations where the quadratic term $(\nabla_X u)^T (\nabla_X u)$ is negligible, $E$ reduces to the familiar linearized strain tensor $\epsilon = \frac{1}{2}(\nabla_X u + (\nabla_X u)^T)$.

### Stress Tensors and Work Conjugacy

Stress is the measure of internal forces acting within a deformable body. As with kinematic quantities, different stress tensors can be defined depending on the configuration in which forces and areas are measured. The relationships between these tensors are not arbitrary but are dictated by the principle of **[work conjugacy](@entry_id:194957)**, which arises from the invariance of virtual power.

The most intuitive stress measure is the **Cauchy stress tensor**, $\sigma$. It is defined in the current configuration $\Omega_t$ and relates the traction vector (force per unit area) $t$ acting on a surface with unit normal $n$ to that normal: $t = \sigma n$. For a classical (non-polar) continuum, the [balance of angular momentum](@entry_id:181848) requires $\sigma$ to be symmetric. The rate of work done by internal stresses per unit current volume, or power density, is given by the contraction of the stress with the [rate-of-deformation tensor](@entry_id:184787) $d = \frac{1}{2}(\nabla_x v + (\nabla_x v)^T)$, where $v$ is the spatial [velocity field](@entry_id:271461). The total internal virtual power is thus:
$$
\delta W_{\text{int}} = \int_{\Omega_t} \sigma : \nabla_x^s w \, dv
$$
where $w$ is a virtual [velocity field](@entry_id:271461) and $\nabla_x^s w$ is its symmetric part. This establishes that $(\sigma, d)$ is a work-conjugate pair.

For many problems, especially in [solid mechanics](@entry_id:164042), it is more convenient to perform all calculations in the fixed reference configuration $\Omega_0$. To do this, we must define stress tensors that are work-conjugate to our material [strain measures](@entry_id:755495). By requiring that the internal power remains invariant under a [change of coordinates](@entry_id:273139) from $\Omega_t$ to $\Omega_0$, we can derive these material stress tensors. The transformation involves the [volume element](@entry_id:267802) change $dv = J dV$, where $J = \det F$, and the [velocity gradient](@entry_id:261686) transformation $\nabla_x w = (\nabla_X w) F^{-1}$. Substituting these into the power integral yields:
$$
\delta W_{\text{int}} = \int_{\Omega_0} \left( \sigma : ((\nabla_X w) F^{-1}) \right) J \, dV = \int_{\Omega_0} (J \sigma F^{-T}) : \nabla_X w \, dV
$$
This leads to the definition of the **first Piola-Kirchhoff (PK1) stress tensor**, $P$:
$$
P = J \sigma F^{-T}
$$
The PK1 stress is work-conjugate to the material [velocity gradient](@entry_id:261686) $\nabla_X w$, which corresponds to the rate of change of the [deformation gradient](@entry_id:163749), $\dot{F}$. Unlike $\sigma$, $P$ is generally not symmetric. It is a "two-point" tensor, relating forces in the current configuration to areas in the reference configuration.

To obtain a fully material stress measure that is also symmetric, we introduce the **second Piola-Kirchhoff (PK2) stress tensor**, $S$. It is defined by the transformation $P = FS$, or equivalently, $S = F^{-1} P$. Substituting the expression for $P$ gives:
$$
S = F^{-1}(J \sigma F^{-T}) = J F^{-1} \sigma F^{-T}
$$
The symmetry of $\sigma$ ensures that $S$ is also symmetric. To find its work-conjugate pair, we re-examine the [power density](@entry_id:194407), $P:\nabla_X w$. Substituting $P=FS$ and noting that $\nabla_X w$ can be identified as the variation of the deformation gradient, $\delta F$:
$$
P : \delta F = (FS) : \delta F = S : (F^T \delta F)
$$
Crucially, because $S$ is symmetric, it can be shown that $S : (F^T \delta F) = S : \delta E$, where $\delta E = \frac{1}{2}(\delta F^T F + F^T \delta F)$ is the variation of the Green-Lagrange [strain tensor](@entry_id:193332). The internal virtual power can therefore be expressed as:
$$
\delta W_{\text{int}} = \int_{\Omega_0} S : \delta E \, dV
$$
This establishes that the symmetric second Piola-Kirchhoff stress tensor $S$ is work-conjugate to the Green-Lagrange strain tensor $E$. These distinct but related [stress measures](@entry_id:198799) and their work-conjugate kinematic pairs form the cornerstone of formulating [variational principles](@entry_id:198028) in different mechanical frames .

### The Principle of Stationary Action in Elastodynamics

The most general variational principle in classical mechanics is **Hamilton's Principle**, or the [principle of stationary action](@entry_id:151723). It states that the true trajectory of a dynamic system between two points in time, $t_0$ and $t_1$, is one that renders the **[action functional](@entry_id:169216)** $S$ stationary. The action is defined as the time integral of the Lagrangian, $L = T - V$, where $T$ is the total kinetic energy and $V$ is the [total potential energy](@entry_id:185512) of the system.

For a continuous elastic body, these energies are integrals over the material domain $\Omega_0$. In a Lagrangian description, the kinetic energy is:
$$
T = \int_{\Omega_0} \frac{1}{2} \rho_0 |\dot{u}|^2 \, dV
$$
where $\rho_0(X)$ is the mass density in the reference configuration and $\dot{u}(X,t)$ is the [material time derivative](@entry_id:190892) of the displacement. For a **hyperelastic** material, the potential energy is the total stored [strain energy](@entry_id:162699), which is the integral of a **stored energy density function**, $W(F)$, that depends on the [deformation gradient](@entry_id:163749):
$$
V = \int_{\Omega_0} W(F(X,t)) \, dV
$$
The [action functional](@entry_id:169216) for a hyperelastic solid in the absence of external forces is therefore :
$$
S[u] = \int_{t_0}^{t_1} L \, dt = \int_{t_0}^{t_1} \int_{\Omega_0} \left( \frac{1}{2} \rho_0 |\dot{u}|^2 - W(F) \right) \, dV dt
$$
Hamilton's principle requires that the [first variation](@entry_id:174697) of the action, $\delta S$, vanishes for all admissible variations $\delta u$ that are zero at the time endpoints ($t_0, t_1$) and on any part of the boundary with prescribed displacements. Computing this variation:
$$
\delta S = \int_{t_0}^{t_1} \int_{\Omega_0} \left( \rho_0 \dot{u} \cdot \delta \dot{u} - \frac{\partial W}{\partial F} : \delta F \right) \, dV dt = 0
$$
Recognizing that $\frac{\partial W}{\partial F}$ is, by definition, the first Piola-Kirchhoff stress $P$, and that $\delta F = \nabla_X(\delta u)$, we can integrate by parts in time and space. This process transfers derivatives from the variation $\delta u$ to the fields $u$ and $P$. The requirement that the resulting expression be zero for arbitrary $\delta u$ yields the strong form of the equations of motion in the material frame, $\rho_0 \ddot{u} - \text{Div}_X P = 0$, and the associated [natural boundary conditions](@entry_id:175664) (e.g., zero traction on a free surface). This illustrates a profound aspect of variational principles: the local differential equations governing the physics are derived as the Euler-Lagrange equations of a global functional.

### Quasistatics and the Principle of Minimum Potential Energy

In many geophysical applications, deformations occur slowly, so inertial effects are negligible ($\ddot{u} \approx 0$). In this quasi-[static limit](@entry_id:262480), the kinetic energy term in the action vanishes. The governing principle simplifies to the **[principle of minimum potential energy](@entry_id:173340)**, which states that an elastic body is in [stable equilibrium](@entry_id:269479) if its total potential energy $\Pi[u]$ is at a minimum. The functional $\Pi[u]$ includes the stored [strain energy](@entry_id:162699) $V$ and the potential energy of external loads $W_{\text{ext}}$:
$$
\Pi[u] = \int_{\Omega} W(\epsilon(u)) \, d\Omega - \int_{\Omega} b \cdot u \, d\Omega - \int_{\Gamma_N} \bar{t} \cdot u \, d\Gamma
$$
Here, for simplicity, we consider the small-strain case where the energy density $W$ is a function of the linearized strain $\epsilon(u)$. The terms $b$ and $\bar{t}$ represent body forces (like gravity) and prescribed tractions on the Neumann boundary $\Gamma_N$, respectively.

The equilibrium state is found by seeking the [displacement field](@entry_id:141476) $u$ that makes the functional stationary, i.e., $\delta \Pi = 0$. The variation of $\Pi$ is:
$$
\delta \Pi = \int_{\Omega} \frac{\partial W}{\partial \epsilon} : \delta \epsilon \, d\Omega - \int_{\Omega} b \cdot \delta u \, d\Omega - \int_{\Gamma_N} \bar{t} \cdot \delta u \, d\Gamma = 0
$$
Recognizing $\sigma = \frac{\partial W}{\partial \epsilon}$, this gives the weak form of equilibrium, also known as the [principle of virtual work](@entry_id:138749): find $u$ such that for all admissible virtual displacements $\delta u$:
$$
\int_{\Omega} \sigma(u) : \epsilon(\delta u) \, d\Omega = \int_{\Omega} b \cdot \delta u \, d\Omega + \int_{\Gamma_N} \bar{t} \cdot \delta u \, d\Gamma
$$

This variational framework provides a crucial distinction between two types of boundary conditions .
-   **Essential boundary conditions** (e.g., prescribed displacement $u = \bar{u}$ on a boundary portion $\Gamma_D$) are constraints on the [solution space](@entry_id:200470) itself. They are enforced *a priori* by requiring that both the trial solution $u$ and the [test functions](@entry_id:166589) (virtual displacements) $\delta u$ belong to specific [function spaces](@entry_id:143478). For instance, the solution $u$ must be in a space of functions that take the value $\bar{u}$ on $\Gamma_D$, while the [virtual displacement](@entry_id:168781) $\delta u$ must vanish on $\Gamma_D$.

-   **Natural boundary conditions** (e.g., prescribed traction $\sigma n = \bar{t}$ on $\Gamma_N$) are not imposed on the [function space](@entry_id:136890). Instead, they emerge *as a consequence* of the variational principle. If we integrate the internal work term by parts, a boundary integral $\int_{\Gamma_N} (\sigma n) \cdot \delta u \, d\Gamma$ appears. Since the variation $\delta u$ is arbitrary on $\Gamma_N$, this term must cancel with the external work term $\int_{\Gamma_N} \bar{t} \cdot \delta u \, d\Gamma$, which naturally enforces the condition $\sigma n = \bar{t}$. The inclusion of the traction term in the potential energy functional ensures that the correct physical boundary condition is satisfied by the solution.

### Material Constitution in Variational Formulations

The specific mechanical behavior of a material is encoded in its [stored energy function](@entry_id:166355) $W$. For the common case of [linear elasticity](@entry_id:166983), $W$ is a quadratic function of the strain tensor $\mathbf{E}$:
$$
\Psi(\mathbf{E}) = \frac{1}{2} E_{ij} C_{ijkl} E_{kl}
$$
The material properties are entirely contained within the fourth-order **[stiffness tensor](@entry_id:176588)** $C_{ijkl}$. For an [isotropic material](@entry_id:204616), $C_{ijkl}$ depends on only two independent constants (e.g., Lamé parameters $\lambda$ and $\mu$). For an **anisotropic** material, such as layered sedimentary rock or minerals with a preferred crystal orientation, $C_{ijkl}$ has a more complex structure with up to 21 independent components.

For the variational problem to be physically meaningful and mathematically **well-posed** (i.e., have a unique, stable solution), the [stiffness tensor](@entry_id:176588) $C_{ijkl}$ must satisfy certain conditions :
1.  **Symmetry**: The tensor must possess minor symmetries ($C_{ijkl} = C_{jikl} = C_{ijlk}$) arising from the symmetry of the [stress and strain](@entry_id:137374) tensors, and a [major symmetry](@entry_id:198487) ($C_{ijkl} = C_{klij}$) which is a necessary condition for the material to be hyperelastic (i.e., for the existence of the potential $\Psi$).

2.  **Positive-Definiteness**: The strain energy stored must be positive for any non-zero strain. This is mathematically expressed as a condition of uniform [positive-definiteness](@entry_id:149643) (or [ellipticity](@entry_id:199972)): there must exist a constant $\alpha > 0$ such that for any non-zero symmetric [strain tensor](@entry_id:193332) $\mathbf{E}$,
    $$
    E_{ij} C_{ijkl} E_{kl} \ge \alpha E_{mn} E_{mn}
    $$
    This condition ensures that the [energy functional](@entry_id:170311) is strictly convex and coercive. Coercivity, combined with **Korn's inequality** (a fundamental result in elasticity that bounds the displacement norm by the strain norm for problems with sufficient displacement constraints), guarantees the [existence and uniqueness](@entry_id:263101) of a solution to the boundary-value problem via the Lax-Milgram theorem. This [positive-definiteness](@entry_id:149643) also implies the weaker **Legendre-Hadamard condition**, which is necessary for [material stability](@entry_id:183933) and real wave speeds, but is not by itself sufficient for the uniqueness of static solutions.

### Variational Methods for Kinematic Constraints

A significant advantage of variational principles is their flexibility in handling kinematic constraints, such as the [incompressibility](@entry_id:274914) of a material. In [geophysics](@entry_id:147342), materials like mantle rock or water-saturated sediments are often modeled as nearly or perfectly incompressible.

#### Mixed Formulations via Lagrange Multipliers

To enforce a hard constraint, such as incompressibility ($J = \det F = 1$), one can introduce a **Lagrange multiplier** field. This gives rise to a **mixed variational principle**. Instead of minimizing the [energy functional](@entry_id:170311) $\Pi[u]$, we seek a stationary point of an **augmented Lagrangian** functional that depends on both the displacement $u$ and the multiplier field $p$, which physically represents pressure :
$$
\mathcal{L}(u, p) = \int_{\Omega_0} \left[ W(F) - p(J-1) \right] dV - W_{\text{ext}}(u)
$$
Stationarity of $\mathcal{L}$ with respect to the two independent fields $(u, p)$ yields two sets of Euler-Lagrange equations.
-   Variation with respect to the multiplier, $\delta_p \mathcal{L} = 0$, yields the weak form of the constraint itself: $\int_{\Omega_0} \delta p (J-1) dV = 0$, which implies $J=1$.
-   Variation with respect to the displacement, $\delta_u \mathcal{L} = 0$, yields the weak form of the momentum balance, but now the stress tensor includes a term from the constraint. The resulting first Piola-Kirchhoff stress is $P = \frac{\partial W}{\partial F} - p J F^{-T}$. The pressure $p$ is no longer determined by the deformation itself but is an independent unknown that adjusts to enforce the constraint.

#### Penalty Formulations

An alternative to the exact enforcement of a constraint is the **[penalty method](@entry_id:143559)**, which approximates the constraint by adding a high-energy penalty for its violation to the potential energy functional. For [incompressibility](@entry_id:274914), the modified energy density becomes:
$$
\Psi_{\kappa}(F) = \Psi(F) + \frac{\kappa}{2} (J-1)^2
$$
where $\kappa$ is a large, positive penalty parameter (e.g., a bulk modulus). This leads to a standard displacement-based variational problem, but with a modified stress tensor. Comparing the resulting stress to the one from the [mixed formulation](@entry_id:171379) reveals that the Lagrange multiplier $p$ is implicitly approximated by $p_{\kappa} = -\kappa(J-1)$ . As $\kappa \to \infty$, the solution of the penalty problem converges to the solution of the constrained problem.

#### Application to Volumetric Locking

The distinction between these methods is of paramount importance in computational mechanics. Standard finite element discretizations of the displacement-only formulation for [nearly incompressible materials](@entry_id:752388) (large $\kappa$) suffer from **volumetric locking**. The [discrete space](@entry_id:155685) of kinematically admissible deformations becomes overly constrained, leading to artificially stiff behavior and meaningless results.

Mixed formulations, born from the Lagrange multiplier approach, circumvent this issue. By treating pressure as an independent field, the [incompressibility constraint](@entry_id:750592) $\text{div } u = 0$ (in the small-strain limit) is enforced weakly, not pointwise, which provides the necessary flexibility for the discrete solution space. This leads to a **saddle-point** [system of linear equations](@entry_id:140416) of the form :
$$
\begin{pmatrix} \boldsymbol{K}  \boldsymbol{G}^{\top} \\ \boldsymbol{G}  -\frac{1}{\kappa}\boldsymbol{M} \end{pmatrix} \begin{pmatrix} \boldsymbol{U} \\ \boldsymbol{P} \end{pmatrix} = \begin{pmatrix} \boldsymbol{F} \\ \boldsymbol{0} \end{pmatrix}
$$
Here, $\boldsymbol{K}$ is the [stiffness matrix](@entry_id:178659), $\boldsymbol{G}$ is a [discrete gradient](@entry_id:171970) operator, and $\boldsymbol{M}$ is a pressure [mass matrix](@entry_id:177093). For this system to be stable, the discrete spaces for displacement and pressure must satisfy the celebrated **Ladyzhenskaya-Babuška-Brezzi (LBB)** or [inf-sup condition](@entry_id:174538). While the penalty method avoids the LBB condition, it suffers from severe ill-conditioning of the [stiffness matrix](@entry_id:178659) as $\kappa$ grows large, which is another manifestation of locking .

### Advanced Applications and Extensions

The power of [variational principles](@entry_id:198028) extends beyond conservative, static elasticity.

#### Dissipative Systems

Many [geophysical materials](@entry_id:749868) exhibit viscoelastic behavior, where energy is dissipated during deformation. While a potential [energy functional](@entry_id:170311) does not exist for the full system, [variational principles](@entry_id:198028) can be extended to handle dissipation. The [principle of virtual work](@entry_id:138749) remains valid, but the stress is now additively decomposed into a conservative part from a free energy potential $W(\varepsilon)$ and a dissipative part from a **dissipation potential** $\mathcal{D}(\dot{\varepsilon})$:
$$
\sigma(\varepsilon, \dot{\varepsilon}) = \frac{\partial W(\varepsilon)}{\partial \varepsilon} + \frac{\partial \mathcal{D}(\dot{\varepsilon})}{\partial \dot{\varepsilon}}
$$
This framework is not only useful for deriving the governing equations but also for constructing numerical time-integration schemes ([variational integrators](@entry_id:174311)) that correctly respect the energy-dissipation balance of the system, ensuring long-term numerical stability and physical fidelity .

#### Adjoint Methods in Inverse Problems

Perhaps one of the most impactful applications of [variational principles](@entry_id:198028) in modern [computational geophysics](@entry_id:747618) is in solving inverse problems, such as **Full Waveform Inversion (FWI)**. The goal of FWI is to find the Earth's material parameters (e.g., seismic velocity) that best explain observed seismic data. This is framed as a PDE-[constrained optimization](@entry_id:145264) problem: minimize a [misfit functional](@entry_id:752011) $J(p)$ that measures the difference between simulated and observed data, subject to the wave equation governing the pressure field $p$.

The gradient of the [misfit functional](@entry_id:752011) with respect to the material parameters is needed for efficient optimization. This gradient can be computed efficiently using the **adjoint method**, which is derived from a variational principle. We construct a Lagrangian by augmenting the [misfit functional](@entry_id:752011) with the wave equation, using the **adjoint field** $\lambda$ as the Lagrange multiplier :
$$
\mathcal{L}(p, \lambda, m) = J(p) + \int_0^T \int_{\Omega} \lambda \left( \mathcal{A}(m)p - s \right) \, dx dt
$$
where $\mathcal{A}(m)p = s$ represents the wave equation with model parameters $m$. By demanding that the variation of $\mathcal{L}$ with respect to the state variable $p$ be zero, we derive the **[adjoint equation](@entry_id:746294)**. This is a wave equation for the adjoint field $\lambda$ that propagates backwards in time, driven by sources determined by the data residual (the misfit). For example, if the misfit is based on [surface pressure](@entry_id:152856) measurements, the adjoint source becomes a boundary condition on $\lambda$; if the misfit is based on interior measurements, the adjoint source is a volumetric term. Once the forward and adjoint fields are computed, the desired gradient of the misfit with respect to the model parameters $m$ can be calculated with one additional integral, making the process computationally feasible for large-scale problems. This elegant and powerful technique is a direct application of the [calculus of variations](@entry_id:142234) to complex, real-world scientific challenges.