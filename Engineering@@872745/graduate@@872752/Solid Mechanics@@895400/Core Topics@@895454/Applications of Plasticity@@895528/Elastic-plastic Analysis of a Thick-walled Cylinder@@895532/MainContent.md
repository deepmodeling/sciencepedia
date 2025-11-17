## Introduction
The [elastic-plastic analysis](@entry_id:181788) of a [thick-walled cylinder](@entry_id:189222) is a classic yet critical topic in [solid mechanics](@entry_id:164042), forming the bedrock for the design of high-performance pressure vessels, pipelines, and mechanical components. While purely elastic design is often the goal, understanding how a structure behaves after localized yielding has begun is essential for ensuring safety, predicting failure, and optimizing material use. This article addresses the knowledge gap between purely elastic theory and fully [plastic collapse](@entry_id:191981) by providing a complete framework for analyzing a cylinder as it transitions from the elastic to the plastic state.

Across the following chapters, you will gain a deep understanding of this fundamental problem. The journey begins in **Principles and Mechanisms**, where we will derive the governing [equations of equilibrium](@entry_id:193797) and [kinematics](@entry_id:173318) and introduce the core concepts of plasticity, including [yield criteria](@entry_id:178101) and flow rules. Next, **Applications and Interdisciplinary Connections** will showcase how these principles are applied in real-world engineering, from selecting appropriate boundary conditions and [yield criteria](@entry_id:178101) to leveraging the autofrettage process for enhanced performance, with extensions into materials science and [geomechanics](@entry_id:175967). Finally, **Hands-On Practices** will provide you with the opportunity to solve practical problems, solidifying your grasp of the stress and strain fields in an elastic-plastic cylinder.

## Principles and Mechanisms

The analysis of an elastic-plastic [thick-walled cylinder](@entry_id:189222) is a canonical problem in [solid mechanics](@entry_id:164042), integrating fundamental principles of equilibrium, [kinematics](@entry_id:173318), and material constitutive behavior. It provides a clear illustration of how stress concentrations lead to localized yielding and the subsequent spread of a [plastic zone](@entry_id:191354) within an otherwise elastic body. This chapter systematically develops the theoretical framework required for this analysis, beginning with the universal equations of mechanics and progressing through elastic response, yield inception, and post-yield [plastic flow](@entry_id:201346).

### Governing Equations for an Axisymmetric Cylinder

Regardless of the material's constitutive response (elastic or plastic), the stress and strain fields within the cylinder must satisfy the fundamental principles of [mechanical equilibrium](@entry_id:148830) and kinematic compatibility. For a long, [thick-walled cylinder](@entry_id:189222) subjected to axisymmetric loading (i.e., loading that is independent of the angular coordinate $\theta$), the problem simplifies considerably. We adopt a [cylindrical coordinate system](@entry_id:266798) $(r, \theta, z)$ with the $z$-axis coinciding with the cylinder's axis.

#### Equilibrium

The state of stress at any point is described by the Cauchy stress tensor $\boldsymbol{\sigma}$. For an axisymmetric problem, the principal stress directions align with the coordinate axes, and all shear stress components are zero: $\tau_{r\theta} = \tau_{rz} = \tau_{\theta z} = 0$. The normal stress components, [radial stress](@entry_id:197086) $\sigma_r$, hoop (or circumferential) stress $\sigma_\theta$, and axial stress $\sigma_z$, are functions of the [radial coordinate](@entry_id:165186) $r$ only.

In the absence of body forces, the static equilibrium condition, expressed as the divergence of the stress tensor being zero ($\nabla \cdot \boldsymbol{\sigma} = \mathbf{0}$), reduces to a single, non-trivial [ordinary differential equation](@entry_id:168621). By considering the balance of forces on an infinitesimal cylindrical element, we arrive at the **radial [equilibrium equation](@entry_id:749057)** [@problem_id:2633851]:

$$
\frac{d\sigma_r}{dr} + \frac{\sigma_r - \sigma_\theta}{r} = 0
$$

This equation provides a fundamental relationship between the rate of change of [radial stress](@entry_id:197086) and the difference between the radial and hoop stresses at any point within the cylinder wall.

#### Kinematics and Plane Strain

The deformation of the cylinder under axisymmetric loading is characterized by a [displacement field](@entry_id:141476) where points move only in the radial direction. Thus, the [displacement vector](@entry_id:262782) $\mathbf{u}$ has components $u_r = u(r)$, $u_\theta = 0$, and $u_z$ is independent of $r$ and $\theta$.

The relationship between this displacement field and the resulting strains is described by the **[kinematic equations](@entry_id:173032)**. For small strains, the [normal strain](@entry_id:204633) components in the [cylindrical coordinate system](@entry_id:266798) are derived from the symmetric gradient of the displacement field [@problem_id:2633890]:

- **Radial Strain:** $\varepsilon_r = \frac{\partial u_r}{\partial r} = \frac{du}{dr}$
- **Hoop Strain:** $\varepsilon_\theta = \frac{u_r}{r} = \frac{u}{r}$
- **Axial Strain:** $\varepsilon_z = \frac{\partial u_z}{\partial z}$

For a cylinder that is very long relative to its diameter, it is common to analyze its behavior away from the ends. If the ends are constrained from expanding or contracting, the [axial strain](@entry_id:160811) can be assumed to be zero throughout the cylinder. This condition, $\varepsilon_z = 0$, is known as **plane strain**. Under this assumption, the [kinematic equations](@entry_id:173032) are fully defined by the radial displacement $u(r)$, and we have the compatibility equation $\frac{d}{dr}(r\varepsilon_\theta) = \varepsilon_r$. The [plane strain](@entry_id:167046) condition is a powerful simplification that is highly relevant for many engineering applications, such as long pipelines and gun barrels.

### Elastic Behavior and the Onset of Yielding

As long as the stresses within the cylinder are sufficiently low, the material behaves elastically. For most metals, this behavior is well-described by the theory of linear [isotropic elasticity](@entry_id:203237).

#### Elastic Constitutive Relations

The [constitutive law](@entry_id:167255), or **Hooke's Law**, connects the stress tensor to the [strain tensor](@entry_id:193332). For a linear, isotropic, elastic material, this relationship is given by:

$$
\sigma_{ij} = \lambda \, \mathrm{tr}(\boldsymbol{\varepsilon}) \, \delta_{ij} + 2G \, \varepsilon_{ij}
$$

where $\boldsymbol{\varepsilon}$ is the [small-strain tensor](@entry_id:754968), $\mathrm{tr}(\boldsymbol{\varepsilon}) = \varepsilon_{kk}$ is the trace of the strain tensor (representing volumetric strain), $\delta_{ij}$ is the Kronecker delta, and $\lambda$ and $G$ are the **Lamé parameters**. These are related to the more familiar Young's modulus $E$ and Poisson's ratio $\nu$ by $G = \frac{E}{2(1+\nu)}$ (the shear modulus) and $\lambda = \frac{E\nu}{(1+\nu)(1-2\nu)}$.

For the axisymmetric cylinder problem with [principal strains](@entry_id:197797) $\varepsilon_r$, $\varepsilon_\theta$, and $\varepsilon_z$, the component-wise stress-strain relations are [@problem_id:2633847]:
$$
\sigma_r = \lambda(\varepsilon_r+\varepsilon_\theta+\varepsilon_z) + 2G\varepsilon_r
$$
$$
\sigma_\theta = \lambda(\varepsilon_r+\varepsilon_\theta+\varepsilon_z) + 2G\varepsilon_\theta
$$
$$
\sigma_z = \lambda(\varepsilon_r+\varepsilon_\theta+\varepsilon_z) + 2G\varepsilon_z
$$

Under the **[plane strain](@entry_id:167046)** condition ($\varepsilon_z=0$), these relations simplify. Notably, the axial stress $\sigma_z$ is generally not zero; it is the stress required to enforce the zero [axial strain](@entry_id:160811) constraint:
$$
\sigma_z = \lambda(\varepsilon_r + \varepsilon_\theta) = \nu(\sigma_r + \sigma_\theta)
$$

Combining the [equilibrium equation](@entry_id:749057), kinematic relations, and these elastic [constitutive laws](@entry_id:178936) yields a system of equations that can be solved for the stress distribution in a purely elastic cylinder. The resulting expressions for $\sigma_r(r)$ and $\sigma_\theta(r)$ are known as the **Lamé equations**. For a cylinder with inner radius $a$ and outer radius $b$, subjected to internal pressure $p_i$ and zero external pressure, the elastic stresses are:
$$
\sigma_r(r) = \frac{p_i a^2}{b^2 - a^2} \left( 1 - \frac{b^2}{r^2} \right)
$$
$$
\sigma_\theta(r) = \frac{p_i a^2}{b^2 - a^2} \left( 1 + \frac{b^2}{r^2} \right)
$$

#### Yield Criteria

The elastic regime is limited. When the stress state reaches a critical level, the material begins to deform permanently, or **yield**. For ductile metals, experimental evidence shows that yielding is largely caused by stress components that produce shape change (distortion), while being nearly independent of stress components that cause uniform volume change (hydrostatic pressure).

This observation motivates the decomposition of any stress tensor $\boldsymbol{\sigma}$ into a **hydrostatic** part and a **deviatoric** part:
$$
\boldsymbol{\sigma} = \sigma_m \mathbf{I} + \mathbf{s}
$$
where $\sigma_m = \frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma}) = \frac{1}{3}(\sigma_r + \sigma_\theta + \sigma_z)$ is the [mean stress](@entry_id:751819), $\mathbf{I}$ is the identity tensor, and $\mathbf{s}$ is the **stress deviator tensor**. The hydrostatic part causes only volume change in an isotropic elastic material, while the deviatoric part causes distortion.

Yield criteria are mathematical functions, defined in [stress space](@entry_id:199156), that predict the onset of plastic deformation. Since yielding is independent of hydrostatic pressure, these criteria are functions only of the [deviatoric stress tensor](@entry_id:267642) $\mathbf{s}$ [@problem_id:2633872].

- **Tresca (Maximum Shear Stress) Criterion:** This criterion posits that yielding occurs when the maximum shear stress in the material reaches a critical value, $k$. This value is calibrated from a simple test, typically a [uniaxial tension test](@entry_id:195375) where the yield stress is $\sigma_Y$. In [uniaxial tension](@entry_id:188287), the maximum shear stress is $\sigma_Y/2$, so the criterion is $\tau_{max} = k = \sigma_Y/2$ [@problem_id:2633821].

- **von Mises (Distortion Energy) Criterion:** This criterion, which generally provides a better fit for most metals, posits that yielding occurs when the [elastic strain energy](@entry_id:202243) of distortion per unit volume reaches a critical value. This is equivalent to the second invariant of the [deviatoric stress tensor](@entry_id:267642), $J_2 = \frac{1}{2}\mathbf{s}:\mathbf{s}$, reaching a critical value. This is operationalized through the **von Mises [equivalent stress](@entry_id:749064)**, $\sigma_{eq}$:
$$
\sigma_{eq} = \sqrt{3J_2} = \sqrt{\frac{1}{2} \left[ (\sigma_r - \sigma_\theta)^2 + (\sigma_\theta - \sigma_z)^2 + (\sigma_z - \sigma_r)^2 \right]}
$$
Yielding occurs when $\sigma_{eq} = \sigma_Y$. This criterion is intrinsically pressure-insensitive because $\sigma_{eq}$ depends only on stress differences, which are unaffected by adding a hydrostatic component to the stress state [@problem_id:2633872]. In a state of pure shear, yielding occurs at a stress $\tau = k$. The von Mises criterion predicts a relationship $k = \sigma_Y / \sqrt{3}$ [@problem_id:2633821]. For a [plane stress](@entry_id:172193) state (where $\sigma_z=0$), a common simplification for open-ended cylinders, the [equivalent stress](@entry_id:749064) reduces to $\sigma_{eq} = \sqrt{\sigma_r^2 - \sigma_r \sigma_\theta + \sigma_\theta^2}$ [@problem_id:2633877].

#### Predicting First Yield

By substituting the Lamé equations for the elastic stress field into the von Mises yield criterion, we can determine the [internal pressure](@entry_id:153696) $p_i$ that will cause the cylinder to first yield. The [equivalent stress](@entry_id:749064) $\sigma_{eq}$ is found to be maximum at the inner radius $r=a$, where the [stress concentration](@entry_id:160987) is highest. Therefore, yielding always begins at the inner surface. By setting $\sigma_{eq}(a) = \sigma_Y$, we can solve for the specific pressure, $p_{yield}$, at which [plastic deformation](@entry_id:139726) initiates [@problem_id:2633855].

### Post-Yield Behavior and Plastic Flow

Once the [yield stress](@entry_id:274513) is exceeded, the material enters the plastic regime. The analysis requires a more sophisticated constitutive theory that can account for irreversible deformation.

#### Fundamental Postulates of Plasticity

Rate-independent [metal plasticity](@entry_id:176585) is built upon a set of core principles that describe the material's behavior during [plastic loading](@entry_id:753518) [@problem_id:2633841]:

1.  **Additive Strain Decomposition:** The total [strain rate tensor](@entry_id:198281) $\dot{\boldsymbol{\varepsilon}}$ is assumed to be the sum of an [elastic strain](@entry_id:189634) rate $\dot{\boldsymbol{\varepsilon}}^e$ and a plastic [strain rate](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}^p$:
    $$
    \dot{\boldsymbol{\varepsilon}} = \dot{\boldsymbol{\varepsilon}}^e + \dot{\boldsymbol{\varepsilon}}^p
    $$
    The [elastic strain](@entry_id:189634) rate remains governed by the time derivative of Hooke's Law, $\dot{\boldsymbol{\sigma}} = \mathbb{C}_e : \dot{\boldsymbol{\varepsilon}}^e$.

2.  **Yield Function:** A [yield function](@entry_id:167970) $f(\boldsymbol{\sigma}, \kappa) \le 0$ defines the boundary of the elastic domain in stress space. Here, $\kappa$ represents one or more [internal state variables](@entry_id:750754) that describe the history of plastic deformation (e.g., hardening). For materials without hardening (**[perfect plasticity](@entry_id:753335)**), the yield function is $f(\boldsymbol{\sigma}) = \sigma_{eq} - \sigma_Y = 0$, where $\sigma_Y$ is a constant.

3.  **Flow Rule:** This rule specifies the direction of the plastic [strain rate](@entry_id:154778) vector. The **[associated flow rule](@entry_id:201731)** is a widely adopted postulate stating that the plastic strain rate is normal to the [yield surface](@entry_id:175331) in [stress space](@entry_id:199156):
    $$
    \dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}}
    $$
    where $\dot{\lambda} \ge 0$ is the [plastic multiplier](@entry_id:753519), a scalar that is non-zero only during active [plastic loading](@entry_id:753518). For the von Mises criterion, the gradient $\frac{\partial f}{\partial \boldsymbol{\sigma}}$ is proportional to the [deviatoric stress tensor](@entry_id:267642) $\mathbf{s}$. Specifically, $\frac{\partial f}{\partial \boldsymbol{\sigma}} = \frac{3}{2}\frac{\mathbf{s}}{\sigma_{eq}}$ [@problem_id:2633904].

4.  **Plastic Incompressibility:** A direct and crucial consequence of using a pressure-independent [yield criterion](@entry_id:193897) (like von Mises) with an [associated flow rule](@entry_id:201731) is that the resulting plastic flow is **isochoric**, or volume-preserving. This is because the plastic [strain rate tensor](@entry_id:198281) is proportional to the [deviatoric stress tensor](@entry_id:267642), which is traceless. Therefore, the plastic [volumetric strain rate](@entry_id:272471) is zero [@problem_id:2633833] [@problem_id:2633904]:
    $$
    \mathrm{tr}(\dot{\boldsymbol{\varepsilon}}^p) = \dot{\varepsilon}^p_{rr} + \dot{\varepsilon}^p_{\theta\theta} + \dot{\varepsilon}^p_{zz} = 0
    $$
    This implies that all volume change in the material remains purely elastic, while plastic flow only contributes to the deviatoric (shape-changing) part of the deformation.

5.  **Hardening and Consistency:** During [plastic flow](@entry_id:201346), the stress state must remain on the yield surface. This is enforced by the **consistency condition**, $\dot{f}=0$. If the material exhibits **[strain hardening](@entry_id:160233)**, the [yield surface](@entry_id:175331) expands as plastic deformation accumulates. This is modeled by allowing the yield stress $\sigma_Y$ to be a function of an equivalent plastic strain, $\varepsilon_p^{eq}$. Common **[isotropic hardening](@entry_id:164486) laws** include linear hardening, $\sigma_Y = \sigma_{Y0} + H\varepsilon_p^{eq}$, and power-law hardening, $\sigma_Y = K(\varepsilon_p^{eq})^n$ [@problem_id:2633869]. The rate of change of yield stress with plastic strain, $H' = d\sigma_Y/d\varepsilon_p^{eq}$, is known as the plastic modulus. The combination of the elastic law and the plastic consistency condition gives rise to an **[elastoplastic tangent modulus](@entry_id:189492)** that governs the overall stress-strain response during [plastic loading](@entry_id:753518). For [perfect plasticity](@entry_id:753335) ($H'=0$), the material can sustain no further increase in [equivalent stress](@entry_id:749064).

### The Complete Elastic-Plastic Boundary Value Problem

As the [internal pressure](@entry_id:153696) $p_i$ is increased beyond the initial yield pressure $p_{yield}$, a [plastic zone](@entry_id:191354) develops from the inner radius $r=a$ and expands outward to a radius $r=r_p$. The cylinder is now composed of an inner plastic [annulus](@entry_id:163678) ($a \le r \le r_p$) and an outer elastic shell ($r_p \le r \le b$). To solve for the stress and displacement fields in this state, we must formulate a complete [boundary value problem](@entry_id:138753) that respects the governing equations in each region and ensures a smooth transition between them [@problem_id:2633841].

The formulation consists of the following components:

- **Universal Equations (valid for $a \le r \le b$):**
    - Equilibrium: $\frac{d\sigma_r}{dr} + \frac{\sigma_r - \sigma_\theta}{r} = 0$
    - Kinematics: $\varepsilon_r = \frac{du}{dr}$, $\varepsilon_\theta = \frac{u}{r}$, with the plane strain constraint $\varepsilon_z = 0$.

- **Constitutive Law in the Elastic Region ($r_p \le r \le b$):**
    - The full set of 3D isotropic Hooke's laws, specialized for plane strain, relates stresses to strains.

- **Constitutive Law in the Plastic Region ($a \le r \le r_p$):**
    - The stress state must satisfy the yield condition at all times: $\sigma_{eq}(\sigma_r, \sigma_\theta, \sigma_z) = \sigma_Y$.
    - The deformation is governed by the elastoplastic flow theory, incorporating the additive decomposition of strain and the [associated flow rule](@entry_id:201731).

- **Boundary Conditions:**
    - At the inner surface, $r=a$: $\sigma_r(a) = -p_i$.
    - At the outer surface, $r=b$: $\sigma_r(b) = 0$.

- **Interface Conditions (at $r=r_p$):**
    - The transition from the elastic to the plastic region must be seamless. This requires:
        1.  **Continuity of Traction:** The [radial stress](@entry_id:197086) $\sigma_r$ must be continuous.
        2.  **Continuity of Displacement:** The radial displacement $u$ must be continuous.
        3.  **Inception of Yield:** The stress state at the interface, as determined from the elastic solution, must lie exactly on the yield surface: $\sigma_{eq}(\boldsymbol{\sigma}(r_p)) = \sigma_Y$.

Solving this coupled system of differential and algebraic equations allows one to determine the stress and displacement fields throughout the cylinder, as well as the extent of the plastic zone $r_p$, for any given [internal pressure](@entry_id:153696) $p_i$ greater than the initial yield pressure.