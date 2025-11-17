## Introduction
In [computational geomechanics](@entry_id:747617), accurately simulating phenomena like landslides, [soil liquefaction](@entry_id:755029), and significant [foundation settlement](@entry_id:749535) involves large deformations where linearized small-strain theories fail. This necessitates the use of geometrically nonlinear formulations, and a fundamental choice arises: in which reference frame should we formulate and solve the governing equations? The two dominant frameworks for addressing this challenge are the **Total Lagrangian (TL)** and **Updated Lagrangian (UL)** formulations. This article provides a comprehensive exploration of these two powerful approaches, demystifying their theoretical underpinnings and practical implications to guide engineers and researchers in selecting and applying the appropriate method for their specific problems.

We will begin in the first chapter, "Principles and Mechanisms," by building the essential kinematic and kinetic language of [finite strain theory](@entry_id:176941), from deformation gradients to [work-conjugate stress](@entry_id:182069) and strain pairs, culminating in the formal derivation of both the TL and UL weak forms. The second chapter, "Applications and Interdisciplinary Connections," will demonstrate how these formulations are applied to real-world geotechnical challenges, including advanced [constitutive modeling](@entry_id:183370), stability analysis, and [multiphysics coupling](@entry_id:171389). Finally, the "Hands-On Practices" section will solidify these concepts through guided problems, reinforcing the theoretical knowledge with practical computation.

## Principles and Mechanisms

In the analysis of geomechanical systems undergoing [large deformations](@entry_id:167243), a critical choice must be made regarding the frame of reference in which the governing equations of motion and equilibrium are expressed. This choice fundamentally dictates the mathematical form of the kinematic quantities, the [stress measures](@entry_id:198799) employed, and the computational procedure for solving the resulting nonlinear equations. This chapter delves into the principles and mechanisms underpinning the two most prevalent frameworks in [computational solid mechanics](@entry_id:169583): the **Total Lagrangian (TL)** and **Updated Lagrangian (UL)** formulations. We will begin by establishing the fundamental kinematic language used to describe [finite deformation](@entry_id:172086), then explore the rigorous definitions of stress and strain required for this regime, and finally construct the TL and UL formulations from these foundational concepts, highlighting their practical implications for numerical implementation.

### Kinematics of Deformation: Describing Motion

The motion of a continuum body is described by a mapping $\boldsymbol{\varphi}$ that tracks the position of each material point over time. A point identified by its position vector $\mathbf{X}$ in the initial, undeformed **reference configuration** ($B_0$) moves to a new position $\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X},t)$ in the **current configuration** ($B_t$). The local properties of this mapping are entirely captured by the **[deformation gradient](@entry_id:163749)** tensor, $\mathbf{F}$, defined as the gradient of the motion with respect to the reference coordinates:

$$ \mathbf{F} = \frac{\partial \mathbf{x}}{\partial \mathbf{X}} = \nabla_X \boldsymbol{\varphi} $$

The deformation gradient is the cornerstone of [finite deformation theory](@entry_id:202998). It acts as a linear operator that maps a differential material [line element](@entry_id:196833) $d\mathbf{X}$ in the reference configuration to its corresponding element $d\mathbf{x}$ in the current configuration [@problem_id:3568051]. This relationship is expressed as:

$$ d\mathbf{x} = \mathbf{F} d\mathbf{X} $$

This mapping extends to surface and volume elements as well. A differential [volume element](@entry_id:267802) $dV$ in the reference configuration transforms to $dv$ in the current configuration according to the rule $dv = J dV$, where $J = \det(\mathbf{F})$ is the **Jacobian** of the deformation. The Jacobian represents the local change in volume; for any physically admissible motion that prevents matter from interpenetrating or inverting, we must have $J > 0$. The mapping of an oriented surface element, described by its normal vector and area ($\mathbf{N} dA$ in $B_0$ and $\mathbf{n} da$ in $B_t$), is given by the celebrated **Nanson's formula**:

$$ \mathbf{n} da = J \mathbf{F}^{-T} \mathbf{N} dA $$

where $\mathbf{F}^{-T}$ denotes the inverse transpose of $\mathbf{F}$ [@problem_id:3568051]. This relation is crucial for transforming forces and fluxes between the two configurations.

While $\mathbf{F}$ completely describes the local deformation, it does not distinguish between pure stretch and pure [rigid body rotation](@entry_id:167024). The **[polar decomposition theorem](@entry_id:753554)** provides this crucial physical insight by uniquely decomposing $\mathbf{F}$ into the product of a proper orthogonal tensor $\mathbf{R}$ (representing rotation) and a symmetric, [positive-definite tensor](@entry_id:204409) $\mathbf{U}$ (representing stretch) [@problem_id:3568009]:

$$ \mathbf{F} = \mathbf{R} \mathbf{U} $$

The tensor $\mathbf{U}$ is known as the **[right stretch tensor](@entry_id:193756)** and acts in the reference configuration. This decomposition is fundamental to constructing [strain measures](@entry_id:755495) that are independent of rigid body rotations, a property known as **objectivity**.

### Measuring Strain: The Challenge of Objectivity

For large deformations, the [infinitesimal strain tensor](@entry_id:167211) is inadequate because it is not objective. A valid [finite strain](@entry_id:749398) measure must quantify pure deformation, remaining unaffected by any superposed [rigid body motion](@entry_id:144691). The [polar decomposition](@entry_id:149541) provides a clear path to achieving this.

Consider the change in the squared length of the material fiber $d\mathbf{X}$. Its initial squared length is $|d\mathbf{X}|^2 = d\mathbf{X} \cdot d\mathbf{X}$. Its final squared length is $|d\mathbf{x}|^2 = d\mathbf{x} \cdot d\mathbf{x} = (\mathbf{F}d\mathbf{X}) \cdot (\mathbf{F}d\mathbf{X}) = d\mathbf{X} \cdot (\mathbf{F}^T \mathbf{F}) d\mathbf{X}$. The change in squared length is thus governed by the tensor $\mathbf{F}^T\mathbf{F}$. This tensor is known as the **right Cauchy-Green deformation tensor**, denoted by $\mathbf{C}$:

$$ \mathbf{C} = \mathbf{F}^T \mathbf{F} $$

Using the polar decomposition, we see that $\mathbf{C} = (\mathbf{R}\mathbf{U})^T(\mathbf{R}\mathbf{U}) = \mathbf{U}^T\mathbf{R}^T\mathbf{R}\mathbf{U} = \mathbf{U}^2$. This reveals that $\mathbf{C}$ depends only on the [stretch tensor](@entry_id:193200) $\mathbf{U}$ and is completely independent of the rotation $\mathbf{R}$. It is therefore an objective measure of deformation.

From $\mathbf{C}$, we define the **Green-Lagrange [strain tensor](@entry_id:193332)** $\mathbf{E}$ as:

$$ \mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I}) = \frac{1}{2}(\mathbf{F}^T\mathbf{F} - \mathbf{I}) $$

The tensor $\mathbf{E}$ is the natural strain measure for descriptions referred to the initial configuration, as it is a [material tensor](@entry_id:196294) field defined on $B_0$. Its objectivity is guaranteed because it depends only on $\mathbf{U}$ [@problem_id:3568032] [@problem_id:3568009].

For descriptions referred to the current configuration, a parallel set of measures can be defined. The **left Cauchy-Green (or Finger) tensor** is $\mathbf{B} = \mathbf{F}\mathbf{F}^T$, and the corresponding **Euler-Almansi [strain tensor](@entry_id:193332)** is defined as:

$$ \mathbf{e} = \frac{1}{2}(\mathbf{I} - \mathbf{B}^{-1}) $$

The tensor $\mathbf{e}$ is a [spatial tensor](@entry_id:185799) field, defined on $B_t$, and it quantifies strain relative to the geometry of the current configuration [@problem_id:3568001]. The Green-Lagrange and Euler-Almansi strain tensors are related through the deformation mapping by the push-forward operation $\mathbf{e} = \mathbf{F}^{-T}\mathbf{E}\mathbf{F}^{-1}$ [@problem_id:3568001].

### Measuring Stress: A Framework of Energetic Conjugacy

Just as there are multiple ways to measure strain, there are several distinct but related tensors used to measure stress. The choice of stress measure is not arbitrary; it is rigidly dictated by the choice of strain measure through the principle of **[work conjugacy](@entry_id:194957)**. This principle stems from the requirement that the [mechanical power](@entry_id:163535) density (the rate of work per unit volume) must be invariant regardless of the descriptive framework. This concept of power invariance is the essential link between all stress and strain measures [@problem_id:3568021].

The most physically intuitive stress measure is the **Cauchy stress tensor** $\mathbf{\sigma}$, also known as the [true stress](@entry_id:190985). It is a [spatial tensor](@entry_id:185799) defined in the current configuration $B_t$. Its fundamental property, established by Cauchy's stress theorem, is that it linearly relates the outward unit normal $\mathbf{n}$ of any surface in $B_t$ to the **[traction vector](@entry_id:189429)** $\mathbf{t}$ (force per unit current area) acting on that surface [@problem_id:3568013]:

$$ \mathbf{t} = \mathbf{\sigma} \mathbf{n} $$

The [power density](@entry_id:194407) per unit current volume is given by the contraction of the Cauchy stress with the **[rate-of-deformation tensor](@entry_id:184787)** $\mathbf{d}$, which is the symmetric part of the [spatial velocity gradient](@entry_id:187198) $\mathbf{l} = \dot{\mathbf{F}}\mathbf{F}^{-1}$.

To relate this to Lagrangian measures, we consider the power density per unit reference volume, $p_V$, which must equal the [power density](@entry_id:194407) per unit current volume multiplied by the volume ratio $J$.

$$ p_V = J (\mathbf{\sigma} : \mathbf{d}) $$

From this single starting point, we can derive all other [stress measures](@entry_id:198799) by ensuring the power density remains the same when expressed in terms of different strain rates.

1.  **Kirchhoff Stress ($\tau$)**: This spatial stress measure is defined to absorb the Jacobian factor, simplifying the power expression.
    -   Definition: $\mathbf{\tau} = J\mathbf{\sigma}$
    -   Work-conjugate [strain rate](@entry_id:154778): $\mathbf{d}$
    -   Power density: $p_V = \mathbf{\tau}:\mathbf{d}$

2.  **First Piola-Kirchhoff Stress ($\mathbf{P}$)**: This is a material, or Lagrangian, stress measure. It is derived by transforming the power expression to be conjugate to the rate of the deformation gradient, $\dot{\mathbf{F}}$.
    -   Derivation: $p_V = \mathbf{\tau}:\mathbf{d} = (J\mathbf{\sigma}):(\dot{\mathbf{F}}\mathbf{F}^{-1}) = (J\mathbf{\sigma}\mathbf{F}^{-T}):\dot{\mathbf{F}}$. This identifies $\mathbf{P}$ as the term conjugate to $\dot{\mathbf{F}}$.
    -   Definition: $\mathbf{P} = J\mathbf{\sigma}\mathbf{F}^{-T}$
    -   Work-conjugate strain rate: $\dot{\mathbf{F}}$
    -   Power density: $p_V = \mathbf{P}:\dot{\mathbf{F}}$
    The PK1 stress is also known as the **[nominal stress](@entry_id:201335)**. It has the physical meaning of relating the reference normal $\mathbf{N}$ to the force vector acting on the current surface, expressed per unit reference area [@problem_id:3568050]. It is a "two-point" tensor as it maps a vector in $B_0$ to a vector in $B_t$, and it is generally not symmetric.

3.  **Second Piola-Kirchhoff Stress ($\mathbf{S}$)**: This is another fundamental material stress measure, specifically designed to be work-conjugate to the rate of the Green-Lagrange strain, $\dot{\mathbf{E}}$.
    -   Derivation: Starting from $p_V = \mathbf{P}:\dot{\mathbf{F}}$ and using the relation $\mathbf{P} = \mathbf{F}\mathbf{S}$, it can be shown that this is equivalent to $p_V = \mathbf{S}:\dot{\mathbf{E}}$.
    -   Definition: $\mathbf{S}$ is related to $\mathbf{P}$ by $\mathbf{P}=\mathbf{F}\mathbf{S}$, which implies $\mathbf{S} = \mathbf{F}^{-1}\mathbf{P}$. Substituting the definition of $\mathbf{P}$ gives the direct relation to Cauchy stress: $\mathbf{S} = J \mathbf{F}^{-1}\mathbf{\sigma}\mathbf{F}^{-T}$.
    -   Work-conjugate strain/[strain rate](@entry_id:154778): $\mathbf{E}$ / $\dot{\mathbf{E}}$
    -   Power density: $p_V = \mathbf{S}:\dot{\mathbf{E}}$
    The PK2 stress is a fully material quantity. If $\mathbf{\sigma}$ is symmetric (as it is, by [balance of angular momentum](@entry_id:181848)), then $\mathbf{S}$ is also symmetric. Its key property is that it forms an objective, work-conjugate pair $(\mathbf{S}, \mathbf{E})$ within the reference configuration [@problem_id:3568050].

### The Total and Updated Lagrangian Formulations

With the necessary kinematic and kinetic quantities established, we can now formally define the two primary large-deformation formulations. Both are derived from the **[principle of virtual work](@entry_id:138749)**, which states that for a body in equilibrium, the [internal virtual work](@entry_id:172278) equals the external virtual work for any admissible [virtual displacement](@entry_id:168781).

#### The Total Lagrangian (TL) Formulation

The Total Lagrangian formulation is characterized by the consistent use of the initial, undeformed configuration $B_0$ as the single, fixed reference for all calculations throughout the entire analysis [@problem_id:3567995].

The [weak form](@entry_id:137295) of the [equilibrium equations](@entry_id:172166) is expressed as an integral over the reference volume $B_0$:
$$ \int_{B_0} \mathbf{S} : \delta\mathbf{E} \, dV_0 = \text{Virtual work of external forces} $$
The [internal virtual work](@entry_id:172278) is expressed using the work-conjugate pair $(\mathbf{S}, \mathbf{E})$. This approach has a significant computational advantage: the domain of integration $B_0$ is constant, so [element shape functions](@entry_id:198891) and their gradients with respect to material coordinates need to be computed only once.

However, the formulation is inherently nonlinear. This **[geometric nonlinearity](@entry_id:169896)** arises because the Green-Lagrange strain $\mathbf{E}$ is a quadratic function of the displacement gradients, i.e., $\mathbf{E} = \frac{1}{2}(\nabla_X\mathbf{u} + (\nabla_X\mathbf{u})^T + (\nabla_X\mathbf{u})^T\nabla_X\mathbf{u})$. Consequently, even for a linear elastic material (where $\mathbf{S}$ is linearly related to $\mathbf{E}$), the internal force vector becomes a nonlinear function of the nodal displacements. A numerical solution, typically using the Newton-Raphson method, requires the repeated calculation of the residual vector and [tangent stiffness matrix](@entry_id:170852) based on the current estimate of the displacement field [@problem_id:3568010].

#### The Updated Lagrangian (UL) Formulation

The Updated Lagrangian formulation takes a different approach. Instead of a fixed reference frame, it uses the most recently computed configuration as the reference for the next incremental step [@problem_id:3568000]. For an increment from time $t$ to $t+\Delta t$, the configuration $B_t$ serves as the reference frame.

The [weak form](@entry_id:137295) of equilibrium is expressed as an integral over the current configuration $B_t$:
$$ \int_{B_t} \mathbf{\sigma} : \delta\mathbf{d} \, dV_t = \text{Virtual work of external forces} $$
Here, the [internal virtual work](@entry_id:172278) uses the Cauchy stress $\mathbf{\sigma}$ and the virtual rate of deformation $\mathbf{d}$ (or an incremental spatial strain measure).

The primary computational consequence of the UL formulation is that the domain of integration changes at every step. This means that for each load increment (and each iteration within it), all geometry-dependent quantities must be re-evaluated based on the updated nodal coordinates. This includes:
-   The element Jacobian matrices, which map from the parent element to the [current element](@entry_id:188466).
-   The spatial gradients of the shape functions (the $\mathbf{B}$-matrix), which depend on the element Jacobian.
-   The outward unit normals on boundaries where tractions or contact conditions are applied.

Furthermore, the [consistent tangent stiffness matrix](@entry_id:747734) in the UL formulation contains two components: a **[material stiffness](@entry_id:158390)** part arising from the constitutive response, and a **geometric stiffness** (or [initial stress](@entry_id:750652)) part that depends directly on the current level of Cauchy stress $\mathbf{\sigma}$. Both must be re-evaluated in the current configuration [@problem_id:3568012].

### Comparison of Formulations

The choice between the TL and UL formulations involves a trade-off between the complexity of the kinematic and kinetic measures versus the complexity of the computational procedure [@problem_id:3568004].

-   **Total Lagrangian (TL):**
    -   **Reference:** Fixed initial configuration $B_0$.
    -   **Measures:** Uses complex material stress and strain measures ($\mathbf{S}, \mathbf{E}$).
    -   **Integration:** Performed over a constant domain, simplifying some aspects of the FE implementation (e.g., shape function gradients are constant).
    -   **Nonlinearity:** Stems primarily from the nonlinear strain-displacement relation.

-   **Updated Lagrangian (UL):**
    -   **Reference:** The configuration is updated at each step.
    -   **Measures:** Uses more intuitive spatial measures ($\mathbf{\sigma}, \mathbf{d}$).
    -   **Integration:** Performed over a continuously changing domain, requiring re-computation of all geometric quantities at each step.
    -   **Nonlinearity:** Stems from both material response and the changing geometry, with the latter explicitly appearing in the [geometric stiffness](@entry_id:172820) term.

In modern [computational geomechanics](@entry_id:747617), both formulations are used extensively. While they are theoretically equivalent and will produce the same results for a given problem, their implementation details and [computational efficiency](@entry_id:270255) can differ depending on the specific class of problem being solved, particularly the nature of the material's [constitutive law](@entry_id:167255).