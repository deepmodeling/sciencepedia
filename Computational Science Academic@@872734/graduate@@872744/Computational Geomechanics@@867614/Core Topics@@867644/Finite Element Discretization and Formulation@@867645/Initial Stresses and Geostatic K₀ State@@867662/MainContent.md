## Introduction
The determination of the initial, or *in situ*, stress state within the ground is a cornerstone of [computational geomechanics](@entry_id:747617). This pre-existing stress field, established by geological history long before any engineering activity, dictates how the soil or rock will respond to excavation, loading, and construction. The primary challenge lies in quantifying this state, as the horizontal stresses are statically indeterminate and depend on a complex interplay of material properties and past loading. A failure to accurately define this initial condition can lead to significant errors and numerical instabilities in simulations, rendering predictions unreliable. This article provides a comprehensive exploration of the [geostatic stress](@entry_id:749877) state. We will begin in "Principles and Mechanisms" by dissecting the fundamental concepts, from Terzaghi's [effective stress principle](@entry_id:171867) to the elastic and plastic models that define the at-rest coefficient of earth pressure, $K_0$. Following this, "Applications and Interdisciplinary Connections" will demonstrate the critical role of $K_0$ in practical engineering design, site characterization, and its connections to [hydrogeology](@entry_id:750462) and [thermo-mechanics](@entry_id:172368). Finally, "Hands-On Practices" will offer guided exercises to translate theory into computational application. Let us begin by establishing the principles that govern the [initial stress](@entry_id:750652) field.

## Principles and Mechanisms

The determination of the initial, or *in situ*, stress state within a soil or rock mass is a foundational step in any geomechanical analysis. This initial state, which exists prior to any engineering intervention such as excavation or construction, governs the subsequent mechanical response of the ground. It serves as the reference configuration upon which all changes in stress and strain are superimposed. A precise understanding and correct implementation of the principles governing this initial state are therefore paramount for the accuracy and reliability of computational models. This chapter elucidates the fundamental principles and mechanisms that define the [geostatic stress](@entry_id:749877) state, with a particular focus on the at-rest condition characterized by the coefficient of earth pressure, $K_0$.

### The Foundations of Geostatic Stress

The stress within a soil mass at a given point is a tensor quantity describing the [internal forces](@entry_id:167605) that adjacent particles of the material exert on each other. In geotechnical engineering, a crucial distinction is made between total stress and [effective stress](@entry_id:198048), a concept central to the behavior of [porous media](@entry_id:154591) like soil.

#### The Principle of Effective Stress

Soil is a multiphase material, typically consisting of solid particles, water (or another fluid), and gas. The **total stress**, denoted by the tensor $\boldsymbol{\sigma}$, represents the total force per unit area acting within the soil mass. This stress is supported by both the solid skeleton and the fluid pressure within the pores. In 1936, Karl Terzaghi formulated the revolutionary **[principle of effective stress](@entry_id:197987)**, which states that all measurable effects of a change of stress, such as compression and changes in shearing resistance, are exclusively due to changes in the **effective stress**. The effective stress, $\boldsymbol{\sigma}'$, is defined as the difference between the total stress and the pore [fluid pressure](@entry_id:270067), $u$.

$$ \boldsymbol{\sigma}' = \boldsymbol{\sigma} - u\mathbf{I} $$

Here, $\mathbf{I}$ is the second-order identity tensor. This equation reveals that pore pressure is a scalar quantity that acts equally in all directions, contributing to the normal components of the total stress tensor but not to the shear components [@problem_id:3533893]. The effective stress, by contrast, is the stress that is carried by the solid skeleton of the soil. It is this stress that controls the strength and deformation of the soil.

#### Vertical Equilibrium and Hydrostatic Conditions

In the absence of any tectonic activity, the primary source of stress in a soil deposit is the self-weight of the material. For a laterally extensive, horizontal soil deposit, the state of stress is termed **geostatic**. The fundamental equation governing this state is the condition of [static equilibrium](@entry_id:163498), which ensures that the internal stresses balance the [body forces](@entry_id:174230) (gravity). For a quasi-static system, this is expressed as:

$$ \nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \mathbf{0} $$

where $\nabla \cdot$ is the [divergence operator](@entry_id:265975) and $\mathbf{b}$ is the [body force](@entry_id:184443) vector per unit volume. For a soil with unit weight $\gamma$, the [body force](@entry_id:184443) is $\mathbf{b} = \gamma \mathbf{e}_y$, assuming the $y$-coordinate is directed vertically downward.

For a one-dimensional problem where stress varies only with depth $y$, the [equilibrium equation](@entry_id:749057) simplifies significantly. Adopting the geomechanics sign convention where compressive stresses are positive, the [equilibrium equation](@entry_id:749057) becomes:

$$ \frac{d\sigma_{yy}}{dy} = \gamma $$

Integrating this equation from the ground surface ($y=0$), where the stress is typically zero (in the absence of a surface surcharge), to a depth $y$ gives the vertical total stress, $\sigma_{v}$ (equivalent to $\sigma_{yy}$):

$$ \sigma_v(y) = \int_0^y \gamma(\xi) \,d\xi $$

If the soil is homogeneous with a constant saturated unit weight $\gamma_{\mathrm{sat}}$, this simplifies to $\sigma_v(y) = \gamma_{\mathrm{sat}} y$. [@problem_id:3533879]

In parallel, we must determine the [pore water pressure](@entry_id:753587), $u$. If the [groundwater](@entry_id:201480) is static (i.e., no seepage), the pore [pressure distribution](@entry_id:275409) is **hydrostatic**. With the water table at the ground surface, the [pore pressure](@entry_id:188528) at depth $y$ is given by:

$$ u(y) = \gamma_w y $$

where $\gamma_w$ is the unit weight of water. With both the total stress and pore pressure known, we can find the vertical effective stress, $\sigma'_v$:

$$ \sigma'_v(y) = \sigma_v(y) - u(y) = \gamma_{\mathrm{sat}} y - \gamma_w y = (\gamma_{\mathrm{sat}} - \gamma_w) y = \gamma' y $$

Here, $\gamma' = \gamma_{\mathrm{sat}} - \gamma_w$ is the **buoyant** or **effective unit weight** of the soil. This linear increase of effective stress with depth is a cornerstone of classical [soil mechanics](@entry_id:180264).

#### Calculating Vertical Stresses in Homogeneous and Layered Deposits

The calculation of vertical stress is straightforward for a homogeneous deposit. For example, for a saturated clay layer with $\gamma_{\mathrm{sat}} = 20.5 \, \text{kN/m}^3$ and $\gamma_w = 9.81 \, \text{kN/m}^3$, the total and effective vertical stresses at a depth of $18.2 \, \text{m}$ are calculated as follows [@problem_id:3533879]:

$$ \sigma_v(18.2) = (20.5 \, \text{kN/m}^3)(18.2 \, \text{m}) = 373.1 \, \text{kPa} $$
$$ \sigma'_v(18.2) = (20.5 - 9.81 \, \text{kN/m}^3)(18.2 \, \text{m}) = (10.69 \, \text{kN/m}^3)(18.2 \, \text{m}) = 194.6 \, \text{kPa} $$

For a deposit consisting of multiple layers with different unit weights, the principle remains the same: the total vertical stress at any depth is the cumulative weight of all material above it. The stress profile is piecewise linear, with the slope of the profile changing at each layer interface. The stress itself must be continuous across these interfaces. This can be expressed compactly using the Heaviside step function, $H(\cdot)$. For a multi-layered soil with densities $\rho_1, \rho_2, \dots$ and interface depths $h_1, h_1+h_2, \dots$, the vertical total stress $\sigma_v(y)$ at depth $y$ (measured downwards) under a surface surcharge $q_0$ can be written as [@problem_id:3533949]:

$$ \sigma_v(y) = q_0 + g \left[ \rho_1 y + (\rho_2 - \rho_1)(y - h_1)H(y - h_1) + (\rho_3 - \rho_2)(y - (h_1+h_2))H(y - (h_1+h_2)) + \dots \right] $$

This formulation ensures that the stress derivative correctly reflects the changing unit weight while maintaining stress continuity.

### The At-Rest Condition and Lateral Stress

While vertical stress is determined directly by equilibrium with gravity, horizontal stress is not. It is statically indeterminate and depends on the material's constitutive behavior and its geological history.

#### The Kinematic Constraint of Zero Lateral Strain

For a [geostatic stress](@entry_id:749877) state in a vast, flat-lying deposit, any element of soil is laterally constrained by the surrounding soil. During its geological history of deposition and consolidation, vertical compression due to increasing overburden weight is not accompanied by lateral movement. This imposes a powerful **kinematic constraint**: the horizontal strains are zero, i.e., $\varepsilon_h = 0$. This condition is also known as the **oedometer condition**, named after the laboratory device used to replicate it. It is this constraint that determines the magnitude of the lateral stresses that develop in response to vertical loading [@problem_id:3533937].

#### The Coefficient of Earth Pressure at Rest, $K_0$

The relationship between the horizontal and vertical effective stresses under the condition of zero lateral strain is quantified by the **[coefficient of earth pressure at rest](@entry_id:747449)**, $K_0$:

$$ K_0 = \frac{\sigma'_h}{\sigma'_v} $$

It is fundamentally an effective stress ratio. The horizontal total stress, $\sigma_h$, can be recovered by adding back the [pore pressure](@entry_id:188528): $\sigma_h = \sigma'_h + u = K_0 \sigma'_v + u$. A common misconception is that [pore pressure](@entry_id:188528) acts only vertically; as a scalar pressure, it acts equally in all directions and must be included in all normal components of the total stress tensor [@problem_id:3533893].

The value of $K_0$ is not a universal constant; it is a material property that depends on the soil's composition, density, stress history, and constitutive nature.

#### An Elastic Perspective on $K_0$: Isotropic and Anisotropic Models

The simplest model for soil behavior is linear elasticity. For an isotropic, linear elastic material governed by Hooke's Law, the horizontal strain $\varepsilon_h$ under axisymmetric [geostatic stress](@entry_id:749877) ($\sigma'_h = \sigma'_{h1} = \sigma'_{h2}$) is:

$$ \varepsilon_h = \frac{1}{E'} [ \sigma'_h - \nu' (\sigma'_h + \sigma'_v) ] $$

where $E'$ and $\nu'$ are the effective Young's modulus and Poisson's ratio, respectively. Enforcing the at-rest condition $\varepsilon_h = 0$ yields a direct relationship for $K_0$:

$$ (1-\nu')\sigma'_h = \nu' \sigma'_v \implies K_0 = \frac{\sigma'_h}{\sigma'_v} = \frac{\nu'}{1-\nu'} $$

This equation demonstrates that, from an elastic perspective, $K_0$ is solely a function of Poisson's ratio [@problem_id:3533914, 3533938]. This relationship is only valid as long as the soil's response is purely elastic.

Many natural soils, particularly those formed by [sedimentation](@entry_id:264456), exhibit **anisotropy**—their properties differ with direction. A common idealization is **[transverse isotropy](@entry_id:756140)**, where properties are uniform in the horizontal plane but different in the vertical direction. For such a material, the elastic prediction for $K_0$ involves more parameters. Starting from the constitutive law for a transversely isotropic medium and enforcing $\varepsilon_h = 0$ yields [@problem_id:3533908]:

$$ K_0 = \frac{E_h}{E_v} \frac{\nu_{vh}}{1 - \nu_{hh}} $$

Using the symmetry requirement $\nu_{hv}/E_h = \nu_{vh}/E_v$, this can be simplified to:

$$ K_0 = \frac{\nu_{hv}}{1 - \nu_{hh}} $$

Here, $E_h$ and $E_v$ are the horizontal and vertical moduli, $\nu_{hh}$ is the in-plane horizontal Poisson's ratio, and $\nu_{hv}$ is the ratio describing vertical strain due to horizontal stress. This result shows that stiffness anisotropy, captured by the ratio $E_h/E_v$, directly influences the at-rest stress state, causing divergence from predictions based on isotropic models [@problem_id:3533919].

### Plasticity and the Geostatic State

While elastic models provide a useful starting point, the process of forming a soil deposit through [sedimentation](@entry_id:264456) and consolidation is inherently **plastic** or irreversible. The elastic prediction $K_0 = \nu'/(1-\nu')$ often fails to capture the at-rest state of real soils, particularly those loaded to their maximum-ever stress.

#### Virgin Compression and the Normally Consolidated State

A soil that has never been subjected to an [effective stress](@entry_id:198048) greater than its current one is said to be **normally consolidated (NC)**. The loading path it has followed is called the **virgin compression line**. This process involves irrecoverable particle rearrangement and plastic deformation. The at-rest stress state of an NC soil is therefore not purely an elastic phenomenon but the result of a constrained [plastic flow](@entry_id:201346) process.

#### Jaky's Relation for $K_{0,NC}$: A Plasticity-Based View

Based on considerations of plastic equilibrium in a frictional granular mass, and confirmed by extensive empirical data, Jaky (1944) proposed a simple and widely used formula for $K_0$ in normally consolidated soils:

$$ K_{0,NC} \approx 1 - \sin\phi' $$

where $\phi'$ is the effective friction angle of the soil. This relationship is remarkably effective for a wide range of cohesionless and cohesive NC soils. Its applicability is predicated on several key conditions: the soil must be normally consolidated, in a long-term drained state, with behavior dominated by frictional strength, and without significant structure or cementation that would provide additional [cohesion](@entry_id:188479) [@problem_id:3533919]. Unlike the elastic model, Jaky's relation connects $K_0$ to the soil's plastic strength properties ($\phi'$) rather than its elastic stiffness properties ($\nu'$). The two predictions generally do not coincide, reflecting their different physical origins [@problem_id:3533937].

#### The Influence of Stress History: Overconsolidation and $K_{0,OC}$

Many soil deposits have been subjected to higher effective stresses in the past than they currently experience, for example, due to the erosion of overlying glaciers or soil layers. Such soils are termed **overconsolidated (OC)**. The degree of overconsolidation is quantified by the **Overconsolidation Ratio (OCR)**, defined as the ratio of the maximum past [effective stress](@entry_id:198048) to the current effective stress. In terms of [mean effective stress](@entry_id:751815), this is:

$$ \mathrm{OCR} = \frac{p'_c}{p'} $$

where $p'_c$ is the preconsolidation [mean effective stress](@entry_id:751815) (a measure of the soil's stress memory) and $p'$ is the current [mean effective stress](@entry_id:751815) [@problem_id:3533887].

When a soil is unloaded, it expands elastically. The vertical stress $\sigma'_v$ reduces significantly, but to maintain the zero lateral strain condition, the horizontal stress $\sigma'_h$ reduces by a much smaller amount. This "locks in" a higher horizontal stress relative to the vertical stress. Consequently, $K_0$ increases with the OCR. This relationship is often captured by the empirical formula:

$$ K_{0,OC} = K_{0,NC} \cdot (\mathrm{OCR})^{\alpha} $$

The exponent $\alpha$ is an empirical parameter, but a theoretical basis for it can be found within the framework of Critical State Soil Mechanics (e.g., the Modified Cam-Clay model). In this framework, deformation during virgin compression is partitioned into an elastic (recoverable) component, characterized by the swelling index $\kappa$, and a plastic (irreversible) component. The total compression is governed by the compression index $\lambda$. The fraction of volumetric strain that is plastic during virgin loading is $( \lambda - \kappa ) / \lambda = 1 - \kappa/\lambda$. This ratio represents the degree of plasticity of the soil. It is argued that the evolution of $K_0$ during unloading is governed by this inherent plastic character, leading to the theoretical justification [@problem_id:3533887]:

$$ \alpha \approx 1 - \frac{\kappa}{\lambda} $$

### Integration and Consistency in Computational Practice

In [computational geomechanics](@entry_id:747617), the [initial stress](@entry_id:750652) field is not merely an input value but a complete [boundary value problem](@entry_id:138753) that must be solved or specified in a physically and mathematically consistent manner.

#### The Triad of Admissibility: Equilibrium, Compatibility, and Constitutive Consistency

A valid initial state for a [continuum mechanics](@entry_id:155125) model must simultaneously satisfy three conditions [@problem_id:3533938]:

1.  **Static Admissibility (Equilibrium):** The total stress field $\boldsymbol{\sigma}_0$ must be in equilibrium with the [body forces](@entry_id:174230) $\mathbf{b}$ ($\nabla \cdot \boldsymbol{\sigma}_0 + \mathbf{b} = \mathbf{0}$) and must satisfy any prescribed [traction boundary conditions](@entry_id:167112).
2.  **Kinematic Admissibility (Compatibility):** The strain field must be derivable from a continuous displacement field that honors the [displacement boundary conditions](@entry_id:203261). For the geostatic case, this implies the zero lateral strain constraint.
3.  **Constitutive Consistency:** The [stress and strain](@entry_id:137374) fields must be related by the chosen [constitutive model](@entry_id:747751) of the material. As we saw, for a linear elastic material, this means the prescribed $K_0$ must equal $\nu'/(1-\nu')$.

These three conditions form an inseparable triad. An [initial stress](@entry_id:750652) field that violates any of them is physically unrealizable for the specified model and will lead to erroneous simulation results.

#### Advanced Modeling: Stress-Dependent Elasticity

In more advanced models, elastic parameters like Poisson's ratio may not be constant but may depend on the stress level, e.g., $\nu'_t = \nu'_t(\sigma'_v)$. In this case, the relationship between horizontal and vertical stress becomes a differential one [@problem_id:3533910]:

$$ \frac{d\sigma'_h}{d\sigma'_v} = \frac{\nu_t(\sigma'_v)}{1 - \nu_t(\sigma'_v)} $$

The finite value of $\sigma'_h$ at a certain depth (and thus a certain $\sigma'_v$) is found by integrating this expression from the surface downward:

$$ \sigma'_h(\sigma'_v) = \int_0^{\sigma'_v} \frac{\nu_t(s)}{1 - \nu_t(s)} ds $$

The resulting $K_0(\sigma'_v) = \sigma'_h(\sigma'_v)/\sigma'_v$ is an integrated average over the stress path and is generally not equal to the instantaneous ratio $\nu_t(\sigma'_v) / (1 - \nu_t(\sigma'_v))$ at that depth. This highlights that to achieve a constant $K_0$ with depth in such a model, $\nu_t$ must also be constant.

#### Ensuring a Valid Initial State for Numerical Analysis

When setting up a numerical simulation (e.g., using the Finite Element Method), the [initial stress](@entry_id:750652) field $(\boldsymbol{\sigma}_0, u_0)$ and the initial state of all internal variables of the [constitutive model](@entry_id:747751) (e.g., [preconsolidation pressure](@entry_id:203717) $p_c$ in the Modified Cam-Clay model) must be defined [@problem_id:3533893]. This complete initial state serves as the starting point for all subsequent incremental calculations.

A critical requirement is that the initial [effective stress](@entry_id:198048) state must be **admissible** with respect to the yield surface of the chosen elastoplastic model. The [yield function](@entry_id:167970) $f(\boldsymbol{\sigma}', \mathbf{q})$ defines the boundary of the elastic domain. A physically possible stress state must lie on or inside this surface, i.e., $f(\boldsymbol{\sigma}', \mathbf{q}) \le 0$.

If an analysis is initialized with a stress state $\boldsymbol{\sigma}'_0$ that is outside the [yield surface](@entry_id:175331) ($f(\boldsymbol{\sigma}'_0, \mathbf{q}_0) > 0$), the numerical algorithm will immediately detect an inconsistency. Even with no external load applied, the algorithm will compute a non-zero plastic strain increment to "return" the stress state to the yield surface. This generates spurious plastic deformations and a non-zero residual force in the first step of the analysis, corrupting the entire simulation [@problem_id:3533893]. Therefore, ensuring that the defined [initial stress](@entry_id:750652) state is consistent with the chosen [constitutive model](@entry_id:747751) is not an optional refinement but an absolute prerequisite for a valid analysis. This involves verifying not only equilibrium but also that the [initial stress](@entry_id:750652) point lies within the initial [yield surface](@entry_id:175331), as can be explicitly checked in models like Modified Cam Clay [@problem_id:3533914].