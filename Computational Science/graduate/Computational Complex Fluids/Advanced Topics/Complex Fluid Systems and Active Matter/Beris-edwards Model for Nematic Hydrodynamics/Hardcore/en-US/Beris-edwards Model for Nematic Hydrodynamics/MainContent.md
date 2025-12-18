## Introduction
The Beris-Edwards model stands as a cornerstone of modern [soft matter physics](@entry_id:145473), offering a powerful and thermodynamically consistent framework for describing the complex [hydrodynamics](@entry_id:158871) of [nematic liquid crystals](@entry_id:136355). Its significance lies in its ability to capture the intricate, two-way coupling between macroscopic fluid flow and the microscopic [orientational order](@entry_id:753002) of the constituent molecules. This unified approach resolves challenges that simpler theories cannot address, such as the structure of defect cores and the transition between different flow behaviors. This article provides a graduate-level exploration of this essential model, systematically building the theory from its foundational principles to its most advanced applications.

The reader will embark on a structured journey through the Beris-Edwards framework. The first chapter, **"Principles and Mechanisms,"** meticulously derives the governing equations. It begins by defining the [order parameter tensor](@entry_id:193031) and then constructs the Landau-de Gennes free energy, ultimately coupling the dynamics of order and flow through the principles of non-equilibrium thermodynamics. Following this theoretical foundation, the **"Applications and Interdisciplinary Connections"** chapter demonstrates the model's remarkable predictive power across diverse fields, analyzing static structures in [liquid crystal](@entry_id:202281) displays, the complex rheology of nematic fluids, and the emergent dynamics of active matter. Finally, **"Hands-On Practices"** presents a series of computational problems designed to solidify understanding by applying the model to practical scenarios, such as calculating dimensionless numbers and identifying [topological defects](@entry_id:138787).

## Principles and Mechanisms

The Beris-Edwards model provides a comprehensive continuum framework for describing the [hydrodynamics](@entry_id:158871) of [nematic liquid crystals](@entry_id:136355). It captures the intricate interplay between the macroscopic fluid flow and the microscopic [orientational order](@entry_id:753002) of the constituent molecules. This chapter elucidates the fundamental principles and mechanisms that underpin the model, systematically constructing its governing equations from concepts of statistical mechanics, continuum mechanics, and non-equilibrium thermodynamics.

### The Order Parameter Tensor

The central variable in the Beris-Edwards model is the **[order parameter tensor](@entry_id:193031)**, denoted by $Q(\boldsymbol{x}, t)$. This quantity provides a continuous field description of the local orientational order of the anisotropic molecules that constitute the [liquid crystal](@entry_id:202281).

#### Definition and Fundamental Properties

Microscopically, the orientation of a single elongated molecule can be described by a unit vector $\boldsymbol{u}$ aligned with its long axis. In a [nematic phase](@entry_id:140504), these molecules exhibit long-range orientational order, tending to align along a common direction. The $Q$-tensor is defined as the ensemble average of the second moment of the molecular [orientation distribution function](@entry_id:191240), made traceless. Specifically, it is the deviatoric part of the second moment tensor $\langle \boldsymbol{u} \boldsymbol{u} \rangle$:

$Q = \langle \boldsymbol{u} \boldsymbol{u} - \frac{1}{3} I \rangle$

where $I$ is the $3 \times 3$ identity tensor and $\langle \cdot \rangle$ denotes an average over the local distribution of molecular orientations. This definition immediately imparts two crucial properties to the $Q$-tensor .

First, $Q$ is **symmetric**. The [dyadic product](@entry_id:748716) $\boldsymbol{u} \boldsymbol{u}$ is a [symmetric tensor](@entry_id:144567) since its components are $(u_i u_j) = (u_j u_i)$. As the ensemble average is a linear operation that preserves symmetry, and the identity tensor $I$ is symmetric, $Q$ must be symmetric at all points in space and time.

Second, $Q$ is **traceless**. The trace of $Q$ is given by $\operatorname{tr}(Q) = \langle \operatorname{tr}(\boldsymbol{u} \boldsymbol{u}) - \operatorname{tr}(\frac{1}{3} I) \rangle$. The trace of the [dyadic product](@entry_id:748716) is $\operatorname{tr}(\boldsymbol{u} \boldsymbol{u}) = \boldsymbol{u} \cdot \boldsymbol{u} = |\boldsymbol{u}|^2 = 1$, since $\boldsymbol{u}$ is a unit vector. The trace of the identity tensor in three dimensions is 3, so $\operatorname{tr}(\frac{1}{3} I) = 1$. Therefore, $\operatorname{tr}(Q) = \langle 1 - 1 \rangle = 0$. These two properties, symmetry and tracelessness, reduce the number of independent components of the $Q$-tensor from nine to five.

#### Classification of Nematic States: Uniaxiality and Biaxiality

The local state of [nematic order](@entry_id:187456) is fully characterized by the [eigenvalues and eigenvectors](@entry_id:138808) of the [symmetric tensor](@entry_id:144567) $Q$. As a real symmetric $3 \times 3$ tensor, $Q$ has three real eigenvalues, which we denote by $\lambda_1, \lambda_2, \lambda_3$. The tracelessness condition implies that $\lambda_1 + \lambda_2 + \lambda_3 = 0$. The nature of the [nematic order](@entry_id:187456) is classified by the degeneracy of these eigenvalues :

-   **Isotropic State**: This state corresponds to a complete lack of orientational order, where molecular orientations are random. In this case, all eigenvalues are equal. The tracelessness condition forces them all to be zero: $\lambda_1 = \lambda_2 = \lambda_3 = 0$. This implies that the [order parameter tensor](@entry_id:193031) itself is the zero tensor, $Q = 0$.

-   **Uniaxial State**: This is the most common nematic state, characterized by a single preferred axis of alignment. In this case, there is one distinct eigenvalue and two [degenerate eigenvalues](@entry_id:187316). The eigenvalues take the form $(\lambda_a, \lambda_b, \lambda_b)$. The tracelessness condition requires $\lambda_a + 2\lambda_b = 0$, or $\lambda_a = -2\lambda_b$. The eigenvector corresponding to the distinct eigenvalue $\lambda_a$ is called the **director**, denoted by the [unit vector](@entry_id:150575) $\boldsymbol{n}$. The physical interpretation is that molecules preferentially align along the axis $\boldsymbol{n}$. In this state, the $Q$-tensor can be written in the form:
    $Q = S \left( \boldsymbol{n} \boldsymbol{n} - \frac{1}{3} I \right)$
    where $S$ is the **[scalar order parameter](@entry_id:197670)**, which quantifies the degree of alignment along the director. A positive $S$ corresponds to a prolate (rod-like) nematic, while a negative $S$ would describe an oblate (disc-like) nematic. By diagonalizing this tensor, one can relate the eigenvalues to $S$: the eigenvalues are $\{\frac{2S}{3}, -\frac{S}{3}, -\frac{S}{3}\}$ .

-   **Biaxial State**: This is a more complex state of order where there are three distinct, mutually orthogonal principal axes of alignment. This corresponds to the case where all three eigenvalues of $Q$ are distinct: $\lambda_1 \neq \lambda_2 \neq \lambda_3 \neq \lambda_1$. A simple example of a biaxial state is one with eigenvalues $\{\lambda, -\lambda, 0\}$ for some non-zero $\lambda$ .

The distinction between these states can also be made using [scalar invariants](@entry_id:193787) of the $Q$-tensor, which are independent of the coordinate system. The lowest-order non-trivial invariants are $I_2 = \operatorname{tr}(Q^2)$ and $I_3 = \operatorname{tr}(Q^3)$. The [characteristic polynomial](@entry_id:150909) of a traceless $3 \times 3$ tensor is given by $\lambda^3 - \frac{1}{2}I_2 \lambda - \frac{1}{3}I_3 = 0$. A state is uniaxial if and only if this polynomial has a repeated root, which occurs when its discriminant is zero. This condition leads to the elegant criterion that a state is uniaxial (or isotropic) if and only if its invariants satisfy the relation:
$(\operatorname{tr}(Q^3))^2 = \frac{1}{6} (\operatorname{tr}(Q^2))^3$
If this equality does not hold and $\operatorname{tr}(Q^2) > 0$, the state is biaxial . This provides a powerful, coordinate-free method for identifying the local symmetry of the [nematic order](@entry_id:187456).

### The Thermodynamics of Orientational Order

The dynamics of the [order parameter tensor](@entry_id:193031) are governed by the tendency of the system to minimize its total free energy. The Beris-Edwards model employs a **Landau-de Gennes [free energy functional](@entry_id:184428)**, which expresses the energy of a given configuration $Q(\boldsymbol{x})$ as an integral over the system volume. This functional is composed of a bulk part, which depends only on the local value of $Q$, and an elastic part, which penalizes spatial variations in $Q$.

#### The Bulk Free Energy and the Isotropic-Nematic Transition

The bulk free energy density, $f_b$, is constructed as a polynomial expansion in [scalar invariants](@entry_id:193787) of $Q$. To respect the [fundamental symmetries](@entry_id:161256) of the [nematic phase](@entry_id:140504) (in particular, the head-tail symmetry, which means that $\boldsymbol{n}$ and $-\boldsymbol{n}$ describe the same physical state), the expansion must be in terms of rotationally invariant combinations of $Q$. Since the tensor $Q$ itself is invariant under the transformation $\boldsymbol{n} \to -\boldsymbol{n}$, all its invariants, including both even and odd powers like $\operatorname{tr}(Q^2)$ and $\operatorname{tr}(Q^3)$, automatically respect this symmetry.

The minimal expansion up to quartic order in $Q$ that is sufficient to describe the isotropic-[nematic phase](@entry_id:140504) transition is given by:
$f_b(Q) = \frac{A}{2}\operatorname{tr}(Q^2) - \frac{B}{3}\operatorname{tr}(Q^3) + \frac{C}{4}\left(\operatorname{tr}(Q^2)\right)^2$
The coefficients in this expansion have distinct physical meanings :

-   The coefficient $A$ is temperature-dependent, typically assumed to have a [linear form](@entry_id:751308) $A = A_0(T - T^*)$, where $A_0 > 0$ and $T^*$ is the isotropic phase supercooling limit. This term governs the stability of the isotropic phase ($Q=0$). For high temperatures ($T > T^*$), $A > 0$, and the free energy has a single minimum at $Q=0$, corresponding to a stable isotropic phase.

-   The coefficient $B$ is a positive constant for conventional rod-like [liquid crystals](@entry_id:147648). The cubic term, $-\frac{B}{3}\operatorname{tr}(Q^3)$, breaks the symmetry between states with positive and negative order (i.e., between prolate and oblate nematic states) and, crucially, makes the isotropic-nematic transition **first-order**. A [first-order transition](@entry_id:155013) is characterized by a discontinuous jump in the order parameter and [phase coexistence](@entry_id:147284).

-   The coefficient $C$ must be positive to ensure [thermodynamic stability](@entry_id:142877). The quartic term, $\frac{C}{4}(\operatorname{tr}(Q^2))^2$, ensures that the free energy is bounded from below for large values of the order parameter.

The interplay of these terms results in a rich free energy landscape. As the temperature is lowered, a second minimum corresponding to a [nematic phase](@entry_id:140504) appears. The [first-order transition](@entry_id:155013) occurs at a temperature $T_{NI} > T^*$ where the free energy of the nematic minimum equals that of the isotropic minimum ($f_b(Q_{nematic}) = f_b(0) = 0$). In the uniaxial approximation, this coexistence is found to occur when the coefficient $A$ reaches the value $A = B^2 / (27C)$ .

#### The Elastic Free Energy and Frank Elasticity

When the order parameter varies in space, there is an associated energetic cost known as **elastic energy**. This energy penalizes deformations such as splay, twist, and bend. In the Landau-de Gennes framework, this is described by terms involving gradients of the $Q$-tensor. The most general expression quadratic in gradients contains several independent invariants. A common and useful simplification is the **one-constant approximation**, where the elastic free energy density is written as:

$f_{el} = \frac{L}{2} (\partial_k Q_{ij}) (\partial_k Q_{ij})$

Here, $L$ is a single elastic constant, and summation over repeated indices is implied. This term elegantly encodes the energy of all fundamental director deformations. To see this, we can analyze the uniaxial case with a constant [scalar order parameter](@entry_id:197670) $S$ and a spatially varying director $\boldsymbol{n}(\boldsymbol{x})$ . Substituting $Q_{ij} = S(n_i n_j - \delta_{ij}/3)$ into the expression for $f_{el}$ and performing the contraction yields:

$(\partial_k Q_{ij}) (\partial_k Q_{ij}) = 2S^2 (\partial_k n_i) (\partial_k n_i)$

A fundamental identity in [vector calculus](@entry_id:146888) relates the sum of squared director gradients to the classical Frank-Oseen deformation modes (neglecting surface terms): $(\partial_k n_i) (\partial_k n_i) = (\nabla \cdot \boldsymbol{n})^2 + (\boldsymbol{n} \cdot (\nabla \times \boldsymbol{n}))^2 + |\boldsymbol{n} \times (\nabla \times \boldsymbol{n})|^2$. These three terms correspond to the squared magnitudes of **splay**, **twist**, and **bend**, respectively.

Thus, the one-constant Landau-de Gennes elastic energy maps directly to the one-constant Frank-Oseen energy, $f_{Frank} = \frac{K}{2}[(\nabla \cdot \boldsymbol{n})^2 + (\nabla \times \boldsymbol{n})^2]$. By comparing the expressions, we find a direct relationship between the LdG elastic constant $L$ and the Frank elastic constant $K$: $K = 2LS^2$ . This mapping provides a crucial link between the more general tensor theory and the simpler, but highly intuitive, director-based theory.

A more general LdG elastic energy includes multiple [elastic constants](@entry_id:146207) ($L_1, L_2, \dots$), which can be mapped to the distinct Frank constants for splay ($K_1$), twist ($K_2$), and bend ($K_3$) in the limit of small director gradients, providing a more detailed description of the material's anisotropic elastic response .

### The Coupled Equations of Motion

The Beris-Edwards model describes the complete hydrodynamic behavior by coupling the evolution of the order parameter $Q$ to the evolution of the fluid velocity $\boldsymbol{u}$, described by a modified Navier-Stokes equation.

#### Flow Kinematics and the Principle of Objectivity

The motion of the fluid is locally characterized by the **[velocity gradient tensor](@entry_id:270928)**, $W_{\alpha \beta} = \partial_\beta u_\alpha$. This tensor can be uniquely decomposed into its symmetric and antisymmetric parts :

-   The **[rate-of-strain tensor](@entry_id:260652)**, $D = \frac{1}{2}(W + W^T)$, which describes the deformation (stretching and shearing) of a fluid element.
-   The **[vorticity tensor](@entry_id:189621)**, $\Omega = \frac{1}{2}(W - W^T)$, which describes the local [rigid-body rotation](@entry_id:268623) rate of a fluid element.

A fundamental requirement for any valid [constitutive equation](@entry_id:267976) in continuum mechanics is the principle of **[material frame indifference](@entry_id:166014)**, or **objectivity**. This principle states that the physical laws must be independent of the observer's motion, particularly a superposed [rigid-body rotation](@entry_id:268623). A quantity is objective if its governing equation transforms covariantly under such a change of frame.

The standard time derivative following a fluid element, the **material derivative** $DQ/Dt = (\partial_t + \boldsymbol{u} \cdot \nabla)Q$, is *not* objective. Under a change of frame corresponding to a rotation with angular velocity tensor $\Omega_{rot}$, the [material derivative](@entry_id:266939) transforms as $(DQ/Dt)^* = R (DQ/Dt) R^T + [\Omega_{rot}, Q^*]$, where $[\cdot, \cdot]$ is the commutator. The presence of the commutator term means the material derivative fails to transform as a proper tensor.

To construct an objective evolution equation, this non-objective behavior must be precisely canceled. This is achieved by defining an **[objective time derivative](@entry_id:1129024)**, often called a **co-rotational derivative**. The Beris-Edwards equation accomplishes this by subtracting a specific flow-coupling term from the material derivative .

#### The Evolution of the Order Parameter

The evolution equation for the $Q$-tensor balances the advection and rotation by the flow against the thermodynamic relaxation towards the free energy minimum. Its general form is:
$(\partial_t + \boldsymbol{u} \cdot \nabla)Q - S(W, Q) = \Gamma H$

The left side represents an [objective time derivative](@entry_id:1129024), while the right side is the dissipative relaxation term. Let's examine each component.

-   **The Molecular Field $H$**: This is the [thermodynamic force](@entry_id:755913) conjugate to the order parameter $Q$. It drives the system towards a local minimum of the free energy functional $F[Q] = \int f(Q, \nabla Q) dV$. It is defined via the variational derivative of the free energy, projected to ensure it remains symmetric and traceless:
    $H = -\left(\frac{\delta F}{\delta Q}\right)_{ST} = -\frac{\delta F}{\delta Q} + \frac{I}{3} \operatorname{tr}\left(\frac{\delta F}{\delta Q}\right)$
    For the standard Landau-de Gennes free energy, this calculation yields an explicit expression for $H$ in terms of $Q$ and its spatial derivatives .

-   **The Rotational Diffusivity $\Gamma$**: This is a positive transport coefficient that represents the mobility of the orientational degrees of freedom, acting as an inverse [rotational viscosity](@entry_id:200002).

-   **The Co-rotational Term $S(W, Q)$**: This crucial term describes the reversible coupling between the fluid flow and the orientational order. It must be constructed to satisfy several physical principles: it must be objective, it must preserve the symmetry and tracelessness of $Q$, and it must correctly describe the kinematics of a second-moment tensor. The form that satisfies these requirements is a generalized Jaumann derivative  :
    $S(W, Q) = (\xi D + \Omega)(Q + \frac{I}{3}) + (Q + \frac{I}{3})(\xi D - \Omega) - 2\xi(Q + \frac{I}{3})\operatorname{tr}(QD)$
    This expression contains the [vorticity tensor](@entry_id:189621) $\Omega$ and the rate-of-strain tensor $D$. The term involving $\Omega$ ensures that the orientational structure co-rotates with the local fluid vorticity, canceling the non-objective part of the [material derivative](@entry_id:266939). The terms involving $D$ describe how the fluid strain stretches and aligns the nematic texture. The coupling is mediated by the **[flow-alignment parameter](@entry_id:1125094)** $\xi$, which is a material property that determines whether the nematic is flow-aligning or tumbling in simple shear flow .

The combined term $(\partial_t + \boldsymbol{u} \cdot \nabla)Q - S(W, Q)$ constitutes an [objective time derivative](@entry_id:1129024) of the order parameter, ensuring that the full evolution equation is frame-indifferent.

#### The Momentum Balance Equation

The evolution of the fluid velocity $\boldsymbol{u}$ is governed by a modified Navier-Stokes equation that accounts for the back-reaction of the [nematic order](@entry_id:187456) on the flow. The [momentum balance](@entry_id:1128118) for an incompressible fluid of density $\rho$ is:
$\rho(\partial_t \boldsymbol{u} + \boldsymbol{u} \cdot \nabla \boldsymbol{u}) = -\nabla p + \nabla \cdot \sigma_{viscous} + \nabla \cdot \sigma^Q$

Here, $p$ is the pressure that enforces the incompressibility constraint $\nabla \cdot \boldsymbol{u} = 0$, and $\sigma_{viscous} = 2\eta D$ is the standard viscous stress for a Newtonian fluid with viscosity $\eta$. The new element is the **liquid crystal stress tensor**, $\sigma^Q$, which represents the additional stresses arising from the orientational degrees of freedom. This stress tensor has two main contributions: a reversible "elastic" stress from spatial distortions of the [director field](@entry_id:195269) (Ericksen stress) and a stress arising from the flow-alignment coupling . The full expression for the symmetric part of this stress tensor in the Beris-Edwards model is derived from [thermodynamic consistency](@entry_id:138886) principles, as discussed next.

### Thermodynamic Consistency and Onsager Reciprocity

The specific mathematical forms of the co-rotational term $S(W,Q)$ and the liquid crystal stress $\sigma^Q$ are not arbitrary. They are deeply connected through the [second law of thermodynamics](@entry_id:142732), which requires that the total rate of entropy production in the system must be non-negative. This principle is often expressed through Onsager's [reciprocal relations](@entry_id:146283) for systems near equilibrium.

#### The Energy Balance and Entropy Production

For an isothermal, incompressible system, the rate of change of the total energy (kinetic plus free energy) is equal to the negative of the total power dissipated. By calculating the time derivative of the total energy, one can identify the rate of [energy dissipation](@entry_id:147406) per unit volume, which must be non-negative . This rate is found to be:
$\mathcal{T}\dot{s} = 2\eta D:D + \Gamma H:H + \sigma^Q : W + H:S(W,Q) \ge 0$

where $\mathcal{T}$ is the temperature and $\dot{s}$ is the [entropy production](@entry_id:141771) rate. The first two terms, $2\eta D:D$ (viscous heating) and $\Gamma H:H$ (orientational relaxation), are guaranteed to be non-negative since $\eta > 0$ and $\Gamma > 0$. These represent the purely dissipative processes in the system.

#### The Reciprocal Relationship between Stress and Alignment

For the [second law of thermodynamics](@entry_id:142732) to hold under all possible flow conditions, the remaining terms, which represent the reversible power exchange between the flow and the nematic orientation, must sum to zero:
$\sigma^Q : W + H:S(W,Q) = 0$

This crucial power balance equation establishes a reciprocal relationship between the [constitutive relations](@entry_id:186508) for stress and alignment. It acts as a constraint that links the form of $\sigma^Q$ to the form of $S(W,Q)$. The term $H:S(W,Q)$ represents the rate of free energy change due to flow-induced advection and alignment, while $\sigma^Q:W$ represents the power supplied to the fluid by the liquid crystal stresses. This condition ensures that any energy put into orientational modes by the flow is exactly balanced by the work done by the resulting elastic stresses on the fluid in any reversible process.

This reciprocity is manifested in the final expressions for the stress tensor and the flow-coupling term. The parameters that appear in the expression for $S(W,Q)$, such as the [flow-alignment parameter](@entry_id:1125094) $\xi$, must also appear in the expression for $\sigma^Q$. The thermodynamically consistent form for the symmetric part of the liquid crystal stress is :
$\sigma^Q = -L (\nabla Q) (\nabla Q)^T - \xi \left[ H(Q+\frac{I}{3}) + (Q+\frac{I}{3})H - 2(Q+\frac{I}{3})\operatorname{tr}(QH) \right]$
(shown here in a simplified one-elastic-constant form).

This profound connection, rooted in Onsager-Casimir reciprocity, ensures that the Beris-Edwards model is not merely a phenomenological construction but a thermodynamically consistent theory of [nematic hydrodynamics](@entry_id:180688), guaranteeing that its predictions will respect the fundamental laws of physics .