## Introduction
The mechanical behavior of [crystalline materials](@entry_id:157810), such as metals and alloys, is fundamentally dictated by their underlying atomic lattice structure. Predicting their response to deformation—from elastic distortion to permanent [plastic flow](@entry_id:201346) and eventual failure—is a central challenge in materials science and engineering. While simpler [continuum models](@entry_id:190374) often treat materials as isotropic, this assumption breaks down at the grain scale, where anisotropy, [crystallographic texture](@entry_id:186522), and heterogeneous deformation dominate. The Crystal Plasticity Finite Element Method (CPFEM) emerges as a powerful [multiscale modeling framework](@entry_id:1128335) designed to bridge this gap, explicitly linking the physics of microscopic [crystallographic slip](@entry_id:196486) to the macroscopic mechanical response. By embedding detailed constitutive laws for single crystals within the robust structure of continuum mechanics and the [finite element method](@entry_id:136884), CPFEM provides unparalleled insight into how material structure governs properties.

This article provides a comprehensive guide to the theory and application of CPFEM. We will begin in **Principles and Mechanisms** by dissecting the core of the method, from the [finite deformation kinematics](@entry_id:195826) that separate elastic and plastic response to the constitutive laws that govern slip and hardening. Next, in **Applications and Interdisciplinary Connections**, we will explore how CPFEM functions as a virtual laboratory to predict [texture evolution](@entry_id:194385), analyze polycrystalline behavior, and connect simulation with experiment in the broader context of Integrated Computational Materials Engineering (ICME). Finally, the **Hands-On Practices** section offers guided exercises to solidify understanding by implementing key components of a CPFEM code. Through this journey, you will gain the knowledge to leverage CPFEM for advanced material analysis and design.

## Principles and Mechanisms

The behavior of [crystalline materials](@entry_id:157810) under load is governed by a complex interplay of elastic [lattice distortion](@entry_id:1127106) and irreversible plastic flow. The Crystal Plasticity Finite Element Method (CPFEM) provides a powerful framework for modeling these phenomena by embedding the physics of [crystallographic slip](@entry_id:196486) within the robust mathematical structure of continuum mechanics and the [finite element method](@entry_id:136884). This section elucidates the core principles and mechanisms that constitute the CPFEM, from the fundamental [kinematics of finite deformation](@entry_id:1126915) to the detailed constitutive laws and the numerical algorithms that bring them to life.

### Finite Deformation Kinematics

At the heart of modern CPFEM lies a kinematic framework capable of handling the [large deformations](@entry_id:167243) and rotations characteristic of [metal forming](@entry_id:188560) and failure processes.

#### The Multiplicative Decomposition of the Deformation Gradient

The total deformation of a material body is described by the **deformation gradient** tensor, $\mathbf{F}$, which maps line elements from a reference configuration to the current, deformed configuration. To properly separate the recoverable elastic deformation from the permanent plastic deformation, CPFEM employs a **multiplicative decomposition** of $\mathbf{F}$, a concept rigorously formulated by Lee. This decomposition postulates the existence of a conceptual, stress-free **intermediate configuration**.

The total deformation is viewed as a sequence of two mappings :
1.  A plastic mapping, $\mathbf{F}^p$, from the reference configuration to the intermediate configuration. This represents the cumulative effect of permanent, shape-altering plastic flow, which in crystals is primarily due to the motion of dislocations ([crystallographic slip](@entry_id:196486)). Crucially, this process is considered **lattice-invariant**; the orientation of the crystal lattice in the intermediate configuration is identical to that in the reference configuration.
2.  An elastic mapping, $\mathbf{F}^e$, from the intermediate configuration to the final, current configuration. This encompasses both the recoverable elastic stretching and distortion of the crystal lattice, which gives rise to stress and stored elastic energy, and the [rigid-body rotation](@entry_id:268623) of the lattice, which describes the evolution of [crystallographic texture](@entry_id:186522).

This sequence is mathematically expressed as:
$$
\mathbf{F} = \mathbf{F}^e \mathbf{F}^p
$$

A fundamental physical principle of plastic flow by dislocation motion in metals is that it conserves volume. This is enforced by the constraint of **[plastic incompressibility](@entry_id:183440)** on the [plastic deformation gradient](@entry_id:188153):
$$
\det(\mathbf{F}^p) = 1
$$
From the multiplicative property of the determinant, the total volume change, $J = \det(\mathbf{F})$, is therefore given by $J = \det(\mathbf{F}^e \mathbf{F}^p) = \det(\mathbf{F}^e) \det(\mathbf{F}^p) = \det(\mathbf{F}^e)$. This elegantly demonstrates that all volumetric deformation is accommodated by the elastic response of the lattice, driven by the hydrostatic component of stress .

The choice of a multiplicative decomposition over a simpler additive split of strain, e.g., $\mathbf{E} = \mathbf{E}^e + \mathbf{E}^p$ for a [strain tensor](@entry_id:193332) $\mathbf{E}$, is not arbitrary. An additive split is only valid for infinitesimally small strains and rotations. When rotations are large, an [additive decomposition](@entry_id:1120795) of a symmetric strain measure fails to be objective (i.e., invariant under superposed rigid-body motions) and cannot correctly represent the underlying nonlinear kinematics where deformation and rotation do not commute. The multiplicative framework, by contrast, naturally separates the plastic shear from the subsequent elastic distortion and lattice rotation, providing a kinematically consistent method for updating the orientation of [crystallographic slip](@entry_id:196486) systems as the material deforms .

#### Rate Formulation and the Evolution of Crystal Orientation

The evolution of the system is described by the rates of deformation. The **[spatial velocity gradient](@entry_id:187198)**, $\mathbf{l}$, is defined in the current configuration as $\mathbf{l} = \dot{\mathbf{F}}\mathbf{F}^{-1}$. Taking the time derivative of the multiplicative decomposition yields an [additive decomposition](@entry_id:1120795) of the [spatial velocity gradient](@entry_id:187198):
$$
\mathbf{l} = \dot{\mathbf{F}}^e (\mathbf{F}^e)^{-1} + \mathbf{F}^e \left( \dot{\mathbf{F}}^p (\mathbf{F}^p)^{-1} \right) (\mathbf{F}^e)^{-1}
$$
This is commonly written as $\mathbf{l} = \mathbf{l}^e + \mathbf{l}^p$, where $\mathbf{l}^e = \dot{\mathbf{F}}^e (\mathbf{F}^e)^{-1}$ is the elastic velocity gradient and $\mathbf{l}^p = \mathbf{F}^e \mathbf{L}^p (\mathbf{F}^e)^{-1}$ is the spatial plastic [velocity gradient](@entry_id:261686). The tensor $\mathbf{L}^p = \dot{\mathbf{F}}^p (\mathbf{F}^p)^{-1}$ is the **plastic velocity gradient** defined in the intermediate configuration, and the operation $\mathbf{F}^e (\cdot) (\mathbf{F}^e)^{-1}$ is a **push-forward** that maps tensors from the intermediate to the current configuration  .

The total spin of the material, $\mathbf{W} = \text{skew}(\mathbf{l})$, can be decomposed into contributions from the elastic and plastic parts. The **[lattice spin](@entry_id:198780)**, which describes the rate of rotation of the crystal lattice itself, is a key component of the elastic spin, $\mathbf{W}^e = \text{skew}(\mathbf{l}^e)$. The evolution of the lattice orientation, often represented by an orthogonal tensor $\mathbf{R}^e$ from the [polar decomposition](@entry_id:149541) $\mathbf{F}^e = \mathbf{R}^e \mathbf{U}^e$, is governed by the [lattice spin](@entry_id:198780). A standard postulate in CPFEM is that the rate of change of the lattice orientation is given by the elastic spin, $\dot{\mathbf{R}}^e (\mathbf{R}^e)^T = \mathbf{W}^e$. The [total spin](@entry_id:153335) is the sum of this elastic spin and a [plastic spin](@entry_id:188692) arising from the plastic [velocity gradient](@entry_id:261686): $\mathbf{W} = \mathbf{W}^e + \text{skew}(\mathbf{l}^p)$. This partitioning is crucial for correctly predicting the evolution of [crystallographic texture](@entry_id:186522) during [plastic deformation](@entry_id:139726) .

### Constitutive Laws for Single Crystals

The kinematic framework must be complemented by [constitutive laws](@entry_id:178936) that define the material's specific response to loading. These laws describe the elastic behavior, the mechanism of plastic flow, and the evolution of the material's internal state.

#### Elastic Response: Anisotropic Hyperelasticity

The elastic behavior of a crystal is inherently anisotropic, reflecting the underlying symmetry of its atomic lattice. In the [finite deformation](@entry_id:172086) framework, this is described by a **hyperelastic** model, where the stress is derived from a stored elastic energy density function, $\psi$. This energy is a function of the [elastic deformation](@entry_id:161971), typically expressed in terms of the elastic right Cauchy-Green tensor, $\mathbf{C}^e = (\mathbf{F}^e)^T \mathbf{F}^e$.

For the common case where elastic strains are small, the hyperelastic law can be approximated by a linear relationship between a stress measure and an [elastic strain](@entry_id:189634) measure. For instance, the Cauchy stress $\boldsymbol{\sigma}$ in the spatial frame can be related to a small elastic strain tensor $\boldsymbol{\varepsilon}^e$ via a fourth-order [stiffness tensor](@entry_id:176588) $\mathbf{C}$:
$$
\sigma_{ij} = C_{ijkl} \varepsilon^e_{kl}
$$
The [stiffness tensor](@entry_id:176588) $\mathbf{C}$ in the spatial frame is not constant; it changes as the crystal lattice rotates. It is obtained by transforming the constant crystal [stiffness tensor](@entry_id:176588), $\mathbf{C}^c$ (defined in the crystal's reference frame), using the lattice [rotation tensor](@entry_id:191990) $\mathbf{R}$ that maps the crystal axes to the spatial axes . The transformation rule for the components is:
$$
C_{ijkl} = R_{ip} R_{jq} R_{kr} R_{ls} C^c_{pqrs}
$$
This transformation correctly preserves all the necessary properties of the [stiffness tensor](@entry_id:176588), including its minor and major symmetries and its [positive definiteness](@entry_id:178536), ensuring that the elastic response is both physically realistic and thermodynamically consistent.

#### Plastic Response: Crystallographic Slip

Plastic deformation in [crystalline materials](@entry_id:157810) is accommodated by the shearing of atomic planes along specific [crystallographic directions](@entry_id:137393).

**Geometry of Slip**
A **[slip system](@entry_id:155264)**, indexed by $\alpha$, is defined by a pair of [unit vectors](@entry_id:165907): the **slip direction** $\mathbf{s}^\alpha$ and the **slip plane normal** $\mathbf{m}^\alpha$. These vectors are defined with respect to the crystal lattice and are therefore fixed in the reference and intermediate configurations. Their [crystallographic indices](@entry_id:202168), such as the Miller indices $(hkl)$ for the plane and direction indices $[uvw]$ for the direction, can be converted into Cartesian vector components. For example, in a Face-Centered Cubic (FCC) crystal with its axes aligned with a Cartesian basis, the primary [slip system](@entry_id:155264) $(111)[1\bar{1}0]$ corresponds to a unit [slip plane](@entry_id:275308) normal $\mathbf{m}^\alpha = \frac{1}{\sqrt{3}}(1, 1, 1)$ and a unit slip direction $\mathbf{s}^\alpha = \frac{1}{\sqrt{2}}(1, -1, 0)$ . These vectors are orthogonal, $\mathbf{s}^\alpha \cdot \mathbf{m}^\alpha = 0$, reflecting that the slip direction lies within the slip plane.

**The Plastic Velocity Gradient**
The cornerstone of the crystal plasticity constitutive model is the expression for the plastic [velocity gradient](@entry_id:261686), $\mathbf{L}^p$, in the intermediate configuration. It is formulated as the sum of the [simple shear](@entry_id:180497) contributions from all active slip systems :
$$
\mathbf{L}^p = \sum_{\alpha} \dot{\gamma}^\alpha \mathbf{s}^\alpha \otimes \mathbf{m}^\alpha
$$
Here, $\dot{\gamma}^\alpha$ is the scalar **shear rate** on slip system $\alpha$. This equation provides the direct link between the microscopic slip rates and the macroscopic rate of [plastic deformation](@entry_id:139726).

**Driving Force for Slip: Resolved Shear Stress**
For slip to occur on a given system, a sufficient driving force must be present. This driving force is the **resolved shear stress**, $\tau^\alpha$, which is the component of the macroscopic stress tensor that acts in the slip direction on the slip plane. This concept is encapsulated in **Schmid's Law**.

In the [finite strain](@entry_id:749398) context, the Cauchy stress $\boldsymbol{\sigma}$ exists in the current (spatial) configuration, while the [slip system](@entry_id:155264) vectors $\mathbf{s}^\alpha$ and $\mathbf{m}^\alpha$ are defined in the intermediate configuration. To compute the [resolved shear stress](@entry_id:201022), the slip system must be mapped to the current configuration. A [line element](@entry_id:196833) in the slip direction, $\mathbf{s}^\alpha$, is pushed forward to $\mathbf{F}^e \mathbf{s}^\alpha$. The slip plane normal, $\mathbf{m}^\alpha$, transforms according to Nanson's formula, which leads to the transformation $(\mathbf{F}^e)^{-T} \mathbf{m}^\alpha$. The resolved shear stress is then the projection of the Cauchy stress onto the properly transformed and normalized [slip system](@entry_id:155264) vectors :
$$
\tau^{\alpha} = \boldsymbol{\sigma} : \left( \frac{\mathbf{F}^{e} \mathbf{s}^{\alpha}}{\|\mathbf{F}^{e} \mathbf{s}^{\alpha}\|} \otimes \frac{(\mathbf{F}^{e})^{-T} \mathbf{m}^{\alpha}}{\|(\mathbf{F}^{e})^{-T} \mathbf{m}^{\alpha}\|} \right)
$$
This thermodynamically consistent definition ensures that the [plastic dissipation](@entry_id:201273) rate, $\boldsymbol{\sigma} : \mathbf{d}^p$ (where $\mathbf{d}^p = \text{sym}(\mathbf{l}^p)$), is equal to the sum of the power dissipated on each [slip system](@entry_id:155264), $\sum_\alpha \tau^\alpha \dot{\gamma}^\alpha$ .

**Beyond Schmid's Law: Non-Schmid Effects**
While Schmid's Law provides an excellent first approximation, experiments have shown that for some materials, particularly Body-Centered Cubic (BCC) metals, the resistance to slip depends not only on the resolved shear stress but also on other components of the stress tensor. These are known as **non-Schmid effects**. Their physical origin lies in the complex, non-planar core structure of [screw dislocations](@entry_id:182908) in BCC crystals.

To capture these effects, the effective driving stress in the constitutive model is augmented with non-Schmid projections, such as the stress normal to the [slip plane](@entry_id:275308). A key feature of these models is that the non-Schmid contribution is often coupled to the sign of the Schmid stress, $\text{sign}(\tau^\alpha)$. This [non-linear dependence](@entry_id:265776) on stress components breaks the symmetry of the material response under a reversal of the applied stress (e.g., tension versus compression), allowing the model to capture the experimentally observed **[tension-compression asymmetry](@entry_id:201728)** that is a hallmark of many BCC alloys .

#### Evolution Laws for Internal Variables

The state of the material is not fully described by [stress and strain](@entry_id:137374) alone. Internal [state variables](@entry_id:138790), which capture the history of deformation, are required to model phenomena like work hardening. The constitutive model must specify evolution laws for these variables.

**The Flow Rule**
The **[flow rule](@entry_id:177163)** is a [constitutive equation](@entry_id:267976) that relates the slip rate $\dot{\gamma}^\alpha$ to the driving force $\tau^\alpha$ and the current resistance to slip. A widely used form is the rate-dependent, viscoplastic [power-law model](@entry_id:272028) :
$$
\dot{\gamma}^\alpha = \dot{\gamma}_0 \left| \frac{\tau^\alpha}{g^\alpha} \right|^n \text{sign}(\tau^\alpha)
$$
In this equation:
-   $g^\alpha$ is the current **slip resistance** or [critical resolved shear stress](@entry_id:159240) (CRSS) of system $\alpha$, an internal variable that represents the material's strength.
-   $\dot{\gamma}_0$ is a reference shear rate, setting the timescale of the process.
-   $n$ is the **rate-sensitivity exponent**. A larger value of $n$ corresponds to weaker rate sensitivity, and in the limit $n \to \infty$, the model approaches [rate-independent plasticity](@entry_id:754082) where slip occurs only when $|\tau^\alpha| = g^\alpha$.

**Hardening Laws**
The slip resistance $g^\alpha$ is not constant but evolves as plastic deformation proceeds, a phenomenon known as **work hardening**. This is due to the accumulation and interaction of dislocations.

A common model for the evolution of $g^\alpha$ is the **Voce-type [isotropic hardening](@entry_id:164486) law**, which describes how the resistance of a system increases due to slip on that same system (self-hardening) :
$$
g^\alpha(\Gamma^\alpha) = \tau_0^\alpha + (\tau_s^\alpha - \tau_0^\alpha) \left(1 - \exp(-\theta^\alpha \Gamma^\alpha) \right)
$$
Here, $\Gamma^\alpha = \int_0^t |\dot{\gamma}^\alpha| d\tilde{t}$ is the total accumulated slip on the system. The parameters have clear physical meaning: $\tau_0^\alpha$ is the initial CRSS, $\tau_s^\alpha$ is the saturation CRSS at [large deformations](@entry_id:167243), and $\theta^\alpha$ controls the rate of hardening.

A more sophisticated model incorporates **latent hardening**, which accounts for the fact that slip on one system ($\beta$) hardens other systems ($\alpha$). This is captured by a hardening matrix $h_{\alpha\beta}$ in a rate-form law :
$$
\dot{g}^\alpha = \sum_{\beta} h_{\alpha\beta} |\dot{\gamma}^\beta|
$$
The diagonal terms ($h_{\alpha\alpha}$) represent self-hardening, while the off-diagonal terms ($h_{\alpha\beta}, \alpha \neq \beta$) represent latent hardening. These parameters, which are crucial for predicting realistic macroscopic [work hardening](@entry_id:142475) and [texture evolution](@entry_id:194385), can be calibrated through specialized single-crystal experiments. It is important to note that this form of hardening is isotropic, meaning it increases the size of the [yield surface](@entry_id:175331) but does not shift its center. To model [kinematic hardening](@entry_id:172077) effects like the Bauschinger effect, additional [backstress](@entry_id:198105) internal variables are required.

### The Finite Element Method for Crystal Plasticity

The principles outlined above describe the behavior at a single material point. The "FE" in CPFEM refers to the use of the Finite Element Method to solve the continuum boundary value problem for a body composed of such material points.

#### Governing Equations and the Two-Level Solution Strategy

The governing equation for a quasi-static problem is the [balance of linear momentum](@entry_id:193575), $\nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \mathbf{0}$, where $\mathbf{b}$ is the body force. In FEM, this is solved in its integral or **[weak form](@entry_id:137295)**, derived from the [principle of virtual work](@entry_id:138749) :
$$
\int_{\Omega} \boldsymbol{\sigma} : \nabla \delta \mathbf{u} \, d\Omega = \int_{\Omega} \mathbf{b} \cdot \delta \mathbf{u} \, d\Omega + \int_{\partial \Omega_t} \mathbf{t} \cdot \delta \mathbf{u} \, dS
$$
Here, $\delta\mathbf{u}$ is a virtual displacement field, and the equation must hold for all such admissible fields. This equation can be formulated in the current configuration (an Updated Lagrangian approach) or, by transforming all quantities back to the reference configuration, in a Total Lagrangian framework .

Since the stress $\boldsymbol{\sigma}$ is a highly nonlinear function of the deformation history, this [weak form](@entry_id:137295) represents a system of nonlinear algebraic equations for the nodal displacements. CPFEM employs a **two-level solution strategy** to solve this system :
1.  **Global Level**: A global [iterative solver](@entry_id:140727), typically the Newton-Raphson method, is used to find the nodal displacements that satisfy the [weak form](@entry_id:137295) ([global equilibrium](@entry_id:148976)).
2.  **Local Level**: At each integration point (Gauss point) within each element, a local constitutive update is performed to calculate the stress corresponding to the current estimate of deformation from the global solver.

#### The Gauss Point Constitutive Update

The heart of the "M" in CPFEM is the local constitutive update algorithm. For a given total deformation gradient $F^{n+1}$ at the end of a time step, the algorithm must determine the updated internal variables (e.g., $F_p^{n+1}, g^{\alpha, n+1}$) and the corresponding stress $\boldsymbol{\sigma}^{n+1}$. A standard, robust procedure is the **elastic predictor, plastic corrector** scheme :

1.  **Elastic Predictor**: Assume the entire deformation increment is elastic. A trial elastic state is computed using the plastic state from the previous step: $F_e^{\text{tr}} = F^{n+1} (F_p^n)^{-1}$.
2.  **Plastic Corrector**: The trial state is checked against the [flow rule](@entry_id:177163). If [plastic flow](@entry_id:201346) is indicated, a system of nonlinear equations based on an **[implicit integration](@entry_id:1126415)** scheme (e.g., backward-Euler) for the flow and [hardening laws](@entry_id:183802) must be solved to find the correct plastic slip increments $\Delta\gamma^\alpha$.
3.  **Update State**: During the corrector iterations, the [plastic deformation gradient](@entry_id:188153) is updated. To ensure frame-invariance and preserve plastic volume, this is typically done using the **[exponential map](@entry_id:137184)**: $F_p^{n+1} = \exp(\sum_\alpha \Delta\gamma^\alpha \mathbf{s}^\alpha \otimes \mathbf{m}^\alpha) F_p^n$.
4.  **Final Stress**: Once the slip increments have converged, the final state variables and the final stress $\boldsymbol{\sigma}^{n+1}$ are computed.

#### The Algorithmic Tangent and Global Convergence

The Newton-Raphson method used at the global level requires the [tangent stiffness matrix](@entry_id:170852), which is the linearization of the [weak form](@entry_id:137295) with respect to the nodal displacements. The material contribution to this stiffness matrix, for a Total Lagrangian formulation using the Second Piola-Kirchhoff stress $\mathbf{S}$ and Green-Lagrange strain $\mathbf{E}$, is :
$$
\mathbf{K}_{\text{mat}} = \int_{\Omega_0} \mathbf{B}_0^T \mathbb{C}^{\text{alg}} \mathbf{B}_0 \, d\Omega_0
$$
where $\mathbf{B}_0$ is the [strain-displacement matrix](@entry_id:163451). The fourth-order tensor $\mathbb{C}^{\text{alg}}$ is the **[consistent algorithmic tangent](@entry_id:166068)**, defined as the exact linearization of the numerical constitutive update algorithm, $\mathbb{C}^{\text{alg}} = \partial \mathbf{S} / \partial \mathbf{E}$.

Using the purely elastic tangent or any other approximation instead of the [consistent algorithmic tangent](@entry_id:166068) results in an inexact Jacobian for the global Newton solve. This destroys the method's characteristic **[quadratic convergence](@entry_id:142552)**, typically reducing it to a much slower linear rate, or even preventing convergence altogether. The rigorous derivation and implementation of the [algorithmic tangent](@entry_id:165770), which must account for the sensitivity of the converged slip increments to changes in total strain, is therefore essential for the efficiency and robustness of any CPFEM code   .

### Advanced Topics: Strain Localization and Regularization

A critical aspect of plasticity modeling is the prediction of [strain localization](@entry_id:176973), such as the formation of shear bands. In standard, local, [rate-independent plasticity](@entry_id:754082) models, the onset of localization is associated with the loss of [ellipticity](@entry_id:199972) of the governing partial differential equations, which occurs when the material exhibits softening behavior. This mathematical [ill-posedness](@entry_id:635673) manifests in FEM simulations as a pathological **[mesh dependence](@entry_id:174253)**: the width of the computed shear band shrinks as the mesh is refined, and the predicted failure load depends on the element size .

To remedy this, the constitutive model must be regularized by introducing an intrinsic length or time scale. CPFEM offers two primary pathways for regularization:
-   **Rate-Dependent Viscoplasticity**: As described by the power-law [flow rule](@entry_id:177163), rate dependence introduces a natural time scale. The governing equations become parabolic in nature, which prevents the instantaneous formation of infinitely sharp bands. The resulting shear band has a finite, mesh-objective width that is controlled by material parameters like the rate sensitivity $n$ and the loading rate.
-   **Strain-Gradient Plasticity**: This approach augments the material's free energy with terms that depend on the gradients of plastic strain (e.g., $|\nabla \gamma^\alpha|^2$). This introduces an [intrinsic material length scale](@entry_id:197348), $l$, into the constitutive theory. The governing equations become higher-order, and the predicted shear band width is finite and scales with $l$, leading to mesh-objective solutions.

Both approaches restore the [well-posedness](@entry_id:148590) of the boundary value problem and allow for the predictive simulation of failure modes involving intense [strain localization](@entry_id:176973).