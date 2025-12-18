## Introduction
From the toothpaste we use every morning to the concrete poured at construction sites and the lava flows reshaping landscapes, a unique class of materials known as [yield-stress fluids](@entry_id:196553) plays a crucial role in our world. These materials exhibit a fascinating dual nature: they resist flow like a solid under low stress but behave as a liquid once a critical stress threshold—the [yield stress](@entry_id:274513)—is surpassed. Understanding and predicting this behavior is essential for science and engineering, yet it poses a significant challenge that falls outside the scope of classical Newtonian fluid dynamics. This article provides a comprehensive theoretical and practical guide to the two foundational models used to describe this phenomenon: the Bingham and Herschel-Bulkley models.

Over the next three chapters, we will embark on a structured journey into the world of [viscoplasticity](@entry_id:165397). In the first chapter, **Principles and Mechanisms**, we will dissect the fundamental physics of yielding, explore its microstructural origins, and build the one-dimensional and three-dimensional tensorial forms of the Bingham and Herschel-Bulkley models. We will also confront the unique flow phenomena and computational hurdles these models present. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the remarkable versatility of these concepts, showing how they are applied to solve problems in industrial processing, geophysics, and even [biomedical engineering](@entry_id:268134). Finally, in **Hands-On Practices**, you will have the opportunity to solidify your knowledge by tackling a series of guided problems that bridge theory with practical implementation. We begin by delving into the core principles that define a yield-stress fluid.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanical descriptions of [yield-stress fluids](@entry_id:196553). We will begin by establishing the conceptual foundations of yielding behavior, explore its microstructural origins, and then proceed to construct the canonical mathematical models—Bingham and Herschel-Bulkley—first in one dimension and subsequently in their full tensorial form for general three-dimensional flows. Finally, we will examine the unique flow phenomena and the significant computational challenges that arise from the singular nature of these models.

### The Phenomenon of Yield Stress

A vast array of materials, from commonplace substances like toothpaste and mayonnaise to industrial materials like cement slurries and drilling muds, exhibit a distinct mechanical behavior: they resist flow like a solid when subjected to small stresses but flow like a liquid once a critical stress threshold is exceeded. This threshold is known as the **[yield stress](@entry_id:274513)**, denoted by $\tau_y$, and materials exhibiting this property are termed **[yield-stress fluids](@entry_id:196553)** or viscoplastic materials. Below this critical stress, the material can sustain a load and undergo elastic deformation, but it does not flow irreversibly. Above the [yield stress](@entry_id:274513), the solid-like structure "breaks" or "yields," and the material flows, with its resistance to flow often depending on the rate of deformation.

#### The Ideal Yield-Stress Fluid versus Viscoplastic Reality

In theoretical and [computational mechanics](@entry_id:174464), it is often useful to consider an **ideal yield-stress fluid**. This is a material for which there exists a sharply defined stress threshold, $\tau_y > 0$, below which the rate of deformation is identically zero. This implies that for any applied stress $\tau$ with magnitude $|\tau| < \tau_y$, the material behaves as a rigid solid.

This idealization provides a powerful framework for analysis, but it is important to distinguish it from the behavior of many real materials. Experimentally, some materials that appear to have a [yield stress](@entry_id:274513) may in fact exhibit extremely slow flow, or "creep," even at very low stresses. These materials are better described as highly [shear-thinning](@entry_id:150203) liquids with an extremely high viscosity at low shear rates. A formal distinction can be made by examining the behavior of the **[apparent viscosity](@entry_id:260802)**, defined as $\eta_{app}(\dot{\gamma}) = \tau(\dot{\gamma})/\dot{\gamma}$ for a shear rate $\dot{\gamma} > 0$ .

For an ideal yield-stress fluid, such as one described by the Herschel-Bulkley model, the stress $\tau$ approaches the finite yield stress $\tau_y$ as the shear rate $\dot{\gamma}$ approaches zero. Consequently, the [apparent viscosity](@entry_id:260802) diverges:
$$
\lim_{\dot{\gamma} \to 0^+} \eta_{app}(\dot{\gamma}) = \lim_{\dot{\gamma} \to 0^+} \frac{\tau_y + f(\dot{\gamma})}{\dot{\gamma}} = +\infty
$$
where $f(\dot{\gamma})$ is the viscous contribution to stress that vanishes as $\dot{\gamma} \to 0$. In contrast, for a highly shear-thinning fluid without a true yield stress (e.g., one described by a Carreau model), the stress-strain rate relationship is such that the material possesses a finite, albeit potentially very large, **zero-shear viscosity**, $\eta_0$. For such a fluid, the apparent viscosity approaches this finite limit:
$$
\lim_{\dot{\gamma} \to 0^+} \eta_{app}(\dot{\gamma}) = \eta_0  \infty
$$
The divergence of the apparent viscosity is thus the mathematical signature of an ideal yield-stress fluid. While the debate over whether any real material possesses a "true" [yield stress](@entry_id:274513) in this ideal sense is ongoing, the concept remains indispensable for modeling systems where the timescale of observation is much shorter than the timescale of any potential slow creep.

#### Microstructural Origins of Yielding

The macroscopic phenomenon of yielding is a manifestation of collective behavior at the microstructural level. The specific mechanisms dictate not only the magnitude of the yield stress but also the nature of the post-yield flow. Two primary microscopic origins are commonly considered for athermal suspensions and gels .

1.  **Cohesive Networks:** In many systems, such as colloidal gels or flocculated suspensions, particles are held together by attractive forces (e.g., van der Waals, depletion interactions). At rest, these particles form a space-spanning, percolated network that can resist mechanical stress. Yielding occurs when the applied stress is sufficient to rupture a critical number of these interparticle bonds, causing the network to fail and allowing macroscopic flow. If we consider the number of load-bearing contacts per unit area to be $n_c$ and the characteristic force to break a [single bond](@entry_id:188561) to be $F_b$, the [yield stress](@entry_id:274513) can be estimated through a simple [scaling argument](@entry_id:271998): $\tau_y \sim n_c F_b$. For particles of radius $a$ at a volume fraction $\phi$, geometric considerations suggest $n_c \sim \phi/a^2$, leading to $\tau_y \sim \phi F_b / a^2$. Once flow is initiated, the network is in a continuous state of rupture and reformation. Higher shear rates lead to a more broken-down, weaker structure, resulting in a **shear-thinning** behavior post-yield. This mechanism provides a physical basis for models like the Herschel-Bulkley relation with a flow index $n  1$.

2.  **Frictional Contacts:** In dense, granular systems where interparticle attractions are negligible (e.g., non-colloidal slurries), yielding is governed by [static friction](@entry_id:163518). Particles are jammed into a disordered solid-like state under a confining pressure $p$. For flow to occur, particles must slide past one another, which requires overcoming the [static friction](@entry_id:163518) at their contact points. According to Coulomb's law of friction, the tangential force required to initiate sliding is proportional to the normal force at the contact. Macroscopically, this translates to a [yield stress](@entry_id:274513) that is proportional to the confining pressure: $\tau_y \sim \mu_c p$, where $\mu_c$ is an effective friction coefficient. Post-yield, the resistance to flow arises from a combination of ongoing, rate-independent frictional dissipation and rate-dependent viscous dissipation from the motion of particles through the interstitial fluid. This combination of a constant [yield stress](@entry_id:274513) and a linear viscous contribution provides a microstructural motivation for the Bingham model.

#### Static versus Dynamic Yield Stress

For many complex yield-stress materials, especially those with cohesive networks that can restructure over time (a phenomenon known as **[thixotropy](@entry_id:269726)**), the value of the [yield stress](@entry_id:274513) is history-dependent. A distinction is made between the **static yield stress** ($\tau_{y,s}$) and the **dynamic yield stress** ($\tau_{y,d}$) .

*   The **static [yield stress](@entry_id:274513)**, $\tau_{y,s}$, is the minimum stress required to initiate flow in a material that has been at rest for a significant period. During rest, the microstructure can age and evolve into a more strongly connected or energetically favorable state, increasing its resistance to deformation.
*   The **dynamic [yield stress](@entry_id:274513)**, $\tau_{y,d}$, is the minimum stress required to maintain flow. During steady flow, the microstructure is continuously broken down and does not have time to fully rebuild its at-rest structure.

Because the rested structure provides additional resistance, it is a near-universal observation that the static yield stress is greater than or equal to the dynamic yield stress: $\tau_{y,s} \ge \tau_{y,d}$. The stress overshoot often observed in start-up shear tests is a direct consequence of this difference. Operationally, $\tau_{y,s}$ is best measured by applying a slowly increasing stress ramp or a series of creep tests to a well-rested sample, identifying the minimum stress that produces continuous flow. The dynamic yield stress, $\tau_{y,d}$, is determined by extrapolating the steady-state flow curve (stress vs. shear rate) to zero shear rate, typically measured using a decreasing shear-rate sweep after a strong pre-shear to erase memory of the rest state. The ideal models discussed in this chapter typically use a single yield stress parameter, $\tau_y$, which is most often associated with the dynamic [yield stress](@entry_id:274513).

### One-Dimensional Constitutive Models

To formalize the mechanical behavior of [yield-stress fluids](@entry_id:196553), we begin with idealized models in one dimension, corresponding to a simple shear flow.

#### The Bingham Model

The simplest model that captures the essence of a yield-stress fluid is the **Bingham model**, first proposed by Eugene C. Bingham in 1922. It is constructed from two fundamental postulates: a rigid state below the yield stress and a linear relationship between excess stress and shear rate above it . For a simple shear flow with shear stress $\tau$ and shear rate $\dot{\gamma}$, the model is defined by a piecewise relation:

1.  **Unyielded (Solid) Regime:** If the magnitude of the shear stress is less than or equal to the yield stress, there is no flow.
    $$ \dot{\gamma} = 0 \quad \text{if} \quad |\tau| \le \tau_y $$

2.  **Yielded (Fluid) Regime:** If the magnitude of the shear stress exceeds the yield stress, the material flows. The total stress is the sum of the [yield stress](@entry_id:274513) (which resists flow) and a viscous stress that is linearly proportional to the shear rate.
    $$ |\tau| = \tau_y + \mu_p |\dot{\gamma}| \quad \text{if} \quad |\tau| \gt \tau_y $$

The parameter $\mu_p$ is the **[plastic viscosity](@entry_id:267041)**, representing the material's viscosity in the fully yielded state. It is the slope of the shear stress versus shear rate curve in the flowing regime, $d\tau/d\dot{\gamma} = \mu_p$. Incorporating the sign convention that stress opposes the rate of deformation (i.e., $\operatorname{sgn}(\tau) = \operatorname{sgn}(\dot{\gamma})$), the yielded-state relation can be written more compactly as:
$$
\tau = \tau_y \operatorname{sgn}(\dot{\gamma}) + \mu_p \dot{\gamma}
$$

#### The Herschel-Bulkley Model

While the Bingham model is foundational, many real materials exhibit a non-linear relationship between stress and shear rate in the yielded regime. The **Herschel-Bulkley model** generalizes the Bingham model to account for this [non-linearity](@entry_id:637147), particularly the common phenomenon of shear-thinning . It replaces the linear viscous term with a power-law relationship:

1.  **Unyielded (Solid) Regime:** Identical to the Bingham model.
    $$ \dot{\gamma} = 0 \quad \text{if} \quad |\tau| \le \tau_y $$

2.  **Yielded (Fluid) Regime:** The excess stress above yield follows a power law.
    $$ |\tau| = \tau_y + K |\dot{\gamma}|^n \quad \text{if} \quad |\tau| \gt \tau_y $$

Here, $K$ is the **consistency index** and $n$ is the dimensionless **[flow behavior index](@entry_id:265017)**.
*   For $0 \lt n \lt 1$, the fluid is **shear-thinning**: its [apparent viscosity](@entry_id:260802) decreases with increasing shear rate. This is the most common behavior for [yield-stress fluids](@entry_id:196553).
*   For $n \gt 1$, the fluid is **[shear-thickening](@entry_id:260777)**: its apparent viscosity increases with increasing shear rate.
*   For $n=1$, the Herschel-Bulkley model reduces to the Bingham model, with the consistency $K$ becoming the [plastic viscosity](@entry_id:267041) $\mu_p$.

Furthermore, if the yield stress is set to zero ($\tau_y = 0$), the Herschel-Bulkley model simplifies to the **Ostwald-de Waele [power-law model](@entry_id:272028)**, $|\tau| = K|\dot{\gamma}|^n$, which describes a fluid without a [yield stress](@entry_id:274513) but with non-Newtonian viscosity.

### Generalization to Three-Dimensional Flows

To be useful in analyzing complex, multi-dimensional flows, the scalar models must be generalized to a full tensorial form. This requires careful consideration of the principles of continuum mechanics.

#### The Principle of Objectivity and Invariant-Based Criteria

A fundamental requirement for any [constitutive model](@entry_id:747751) is the **[principle of material frame indifference](@entry_id:194378)** (or objectivity). This principle states that the material's response must be independent of the observer's frame of reference. A change in observer frame corresponds to a [rigid body rotation](@entry_id:167024), represented by an orthogonal tensor $\mathbf{Q}$. A physical quantity like stress transforms as $\boldsymbol{\sigma}' = \mathbf{Q} \boldsymbol{\sigma} \mathbf{Q}^{\top}$. A [constitutive law](@entry_id:167255) must be formulated such that it gives the same prediction of material behavior (e.g., yielding) in any such rotated frame.

For an **isotropic** material, which has no intrinsic preferred direction, this principle implies that any scalar criterion, such as the [yield criterion](@entry_id:193897), must be a function of the **[scalar invariants](@entry_id:193787)** of the stress tensor. A criterion based on a single component of the stress tensor, such as $\sigma_{xy}$, is not objective because that component's value changes under a coordinate system rotation, even when the physical stress state remains the same . For example, a state of pure shear stress can be rotated to a frame where the shear components are zero, which would lead a component-based criterion to falsely predict an unyielded state.

For incompressible or [nearly incompressible materials](@entry_id:752388), yielding is primarily driven by shear and is independent of the [hydrostatic pressure](@entry_id:141627) $p$. Therefore, the [yield criterion](@entry_id:193897) is based on the invariants of the **[deviatoric stress tensor](@entry_id:267642)**, $\boldsymbol{\tau} = \boldsymbol{\sigma} + p\mathbf{I}$. The most common criterion is a function of the second invariant, $J_2(\boldsymbol{\tau}) = \frac{1}{2}\operatorname{tr}(\boldsymbol{\tau}^2) = \frac{1}{2}\boldsymbol{\tau}:\boldsymbol{\tau}$. The magnitude of the [deviatoric stress](@entry_id:163323) is then defined as the **von Mises [equivalent stress](@entry_id:749064)**, $\tau_{eq} = \sqrt{3J_2(\boldsymbol{\tau})}$, or more simply using the Frobenius norm, $\|\boldsymbol{\tau}\| = \sqrt{\boldsymbol{\tau}:\boldsymbol{\tau}} = \sqrt{2J_2(\boldsymbol{\tau})}$.

#### The Tensorial Bingham Model

The generalization of the Bingham model to 3D flows relates the [deviatoric stress tensor](@entry_id:267642) $\boldsymbol{\tau}$ to the [rate-of-deformation tensor](@entry_id:184787) $\mathbf{D} = \frac{1}{2}(\nabla\mathbf{u} + (\nabla\mathbf{u})^{\top})$, where $\mathbf{u}$ is the velocity field . The model is defined by:

1.  **Unyielded (Solid) Regime:** If the magnitude of the [deviatoric stress](@entry_id:163323) is below the [yield stress](@entry_id:274513), the material behaves as a rigid solid, meaning there is no deformation.
    $$ \mathbf{D} = \mathbf{0} \quad \text{if} \quad \|\boldsymbol{\tau}\| \lt \tau_y $$

2.  **Yielded (Fluid) Regime:** When the stress magnitude reaches the yield threshold, the material flows. The total [deviatoric stress](@entry_id:163323) is the sum of a viscous part, proportional to $\mathbf{D}$, and a plastic part of magnitude $\tau_y$ that acts in the direction of deformation.
    $$ \boldsymbol{\tau} = 2\mu_p \mathbf{D} + \tau_y \frac{\mathbf{D}}{\|\mathbf{D}\|} \quad \text{if} \quad \|\boldsymbol{\tau}\| \ge \tau_y $$
Here, the tensor norms are defined using the Frobenius inner product, e.g., $\|\mathbf{D}\| = \sqrt{\mathbf{D}:\mathbf{D}}$. This formulation ensures that $\boldsymbol{\tau}$ and $\mathbf{D}$ are co-axial (have the same [principal directions](@entry_id:276187)) and that the magnitude of the stress satisfies $\|\boldsymbol{\tau}\| = \tau_y + 2\mu_p \|\mathbf{D}\|$, which is the direct tensorial analogue of the scalar model.

#### The Tensorial Herschel-Bulkley Model

Similarly, the Herschel-Bulkley model is generalized by replacing the linear viscous term with a power-law dependence on the magnitude of the rate-of-deformation tensor.

1.  **Unyielded (Solid) Regime:** Identical to the tensorial Bingham model.
    $$ \mathbf{D} = \mathbf{0} \quad \text{if} \quad \|\boldsymbol{\tau}\| \lt \tau_y $$

2.  **Yielded (Fluid) Regime:** The [deviatoric stress](@entry_id:163323) is given by:
    $$ \boldsymbol{\tau} = \left( \frac{\tau_y}{\dot{\gamma}_{eff}} + K \dot{\gamma}_{eff}^{n-1} \right) 2\mathbf{D} $$
    A crucial point in this generalization is the definition of the [scalar shear rate](@entry_id:754538) used in the power-law term. To ensure consistency between the 3D tensorial model and the 1D scalar model derived from [simple shear](@entry_id:180497) experiments, a specific definition of the effective shear rate, $\dot{\gamma}_{eff}$, is required. The standard convention is to define it as $\dot{\gamma}_{eff} = \sqrt{2\mathbf{D}:\mathbf{D}}$ . With this definition, the scalar Herschel-Bulkley relation is recovered exactly for [simple shear](@entry_id:180497).

### Flow Phenomena and Computational Challenges

The unique, non-linear nature of yield-stress models gives rise to distinctive flow phenomena and significant difficulties in computational modeling.

#### Unyielded Plug Regions

A hallmark of yield-stress fluid flows is the formation of **unyielded plug regions** (or "plugs"). These are regions within the flow domain where the local magnitude of the [deviatoric stress](@entry_id:163323) is below the yield stress, $\|\boldsymbol{\tau}\| \lt \tau_y$. By the definition of the constitutive model, the material in these regions does not deform, meaning the rate-of-deformation tensor is zero: $\mathbf{D} = \mathbf{0}$ .

Kinematically, $\mathbf{D} = \mathbf{0}$ implies that the region is undergoing, at most, a [rigid-body motion](@entry_id:265795) (translation and rotation). For example, in [pressure-driven flow](@entry_id:148814) through a pipe or channel, a central plug moves with a uniform axial velocity. It is critical to understand that the stress within the plug is generally **not** zero. The plug acts as a solid object, transmitting stress from one yielded region to another. However, because there is no deformation within the plug, the rate of mechanical [energy dissipation](@entry_id:147406), given by $\Phi = \boldsymbol{\tau}:\mathbf{D}$, is identically zero. Furthermore, the entire plug region can accelerate or decelerate as a single rigid body under the action of net forces, a state where $D\mathbf{u}/Dt \neq \mathbf{0}$ can coexist with $\mathbf{D} = \mathbf{0}$.

#### The Apparent Viscosity Singularity and Regularization

As established earlier, a direct consequence of the ideal yield-stress condition is that the apparent viscosity, $\eta_{app} = \|\boldsymbol{\tau}\|/\|\mathbf{D}\|$, diverges to infinity as the rate of deformation $\|\mathbf{D}\|$ approaches zero . This creates a severe problem for many standard numerical methods for fluid dynamics (e.g., in Computational Fluid Dynamics, CFD), which are often formulated in terms of a [viscosity function](@entry_id:1133844) $\eta(\|\mathbf{D}\|)$. The singularity at $\|\mathbf{D}\| = 0$ makes the governing equations non-differentiable and can lead to numerical instability and non-convergence.

A common practical approach to circumvent this issue is **constitutive regularization**. The idea is to replace the sharp, non-differentiable ideal model with a smooth, single-valued function that approximates it. One of the most widely used is the **Papanastasiou regularization**, which modifies the yield stress term with an exponential factor :
$$
\boldsymbol{\tau} = \left[ \mu_p + \frac{\tau_y \left(1 - \exp(-m \|\mathbf{D}\|)\right)}{\|\mathbf{D}\|} \right] 2\mathbf{D}
$$
Here, $m$ is a large [regularization parameter](@entry_id:162917) with units of time. This model is differentiable at $\|\mathbf{D}\| = 0$ and has a large but finite zero-[shear viscosity](@entry_id:141046) of $\eta_0 = \mu_p + m\tau_y$. As $m \to \infty$, the regularized model pointwise recovers the ideal Bingham model. While effective for obtaining stable numerical solutions, regularization has drawbacks: it introduces a small amount of "artificial creep" in regions that should be unyielded and "smears" the sharp boundary of the [yield surface](@entry_id:175331).

#### Variational Formulations and the Yield Surface as a Free Boundary

From a more fundamental perspective, the location of the boundary between yielded and unyielded regions—the **[yield surface](@entry_id:175331)**—is not known in advance. It is part of the solution to be found, a characteristic of a **[free-boundary problem](@entry_id:636836)**. A powerful mathematical framework that naturally handles this is the theory of **variational inequalities** .

Instead of solving the momentum equation directly, the problem is recast as finding the velocity field $\mathbf{u}$ that minimizes a total energy functional. For a steady, inertialess Bingham flow, this functional includes a smooth term for [viscous dissipation](@entry_id:143708) and a non-smooth, non-differentiable term for [plastic dissipation](@entry_id:201273) due to the yield stress. The minimization problem is equivalent to solving a [variational inequality](@entry_id:172788) of the form:
$$
a(\mathbf{u}, \mathbf{v}-\mathbf{u}) + J(\mathbf{v}) - J(\mathbf{u}) \ge \int_{\Omega} \mathbf{f} \cdot (\mathbf{v}-\mathbf{u}) \, dx
$$
for all admissible velocity fields $\mathbf{v}$. Here, $a(\cdot, \cdot)$ represents the viscous work and $J(\mathbf{v}) = \tau_y \int_{\Omega} \|\nabla^s \mathbf{v}\| \, dx$ is the non-smooth [plastic dissipation](@entry_id:201273) functional.

This formulation avoids the explicit appearance of the singular [apparent viscosity](@entry_id:260802). The yield condition emerges naturally as a constraint, akin to an "obstacle" problem in mechanics. Computationally, this is tackled with advanced algorithms (e.g., augmented Lagrangian or [primal-dual methods](@entry_id:637341)) that treat the [yield criterion](@entry_id:193897) as a constraint on the stress field. These methods directly implement the non-smooth physics and can capture sharp yield surfaces without the artificial smearing introduced by [regularization techniques](@entry_id:261393), providing a more rigorous and accurate approach for computational studies of [yield-stress fluids](@entry_id:196553).