## Introduction
While many fluid dynamics problems can be adequately described by assuming a simple, [linear relationship](@entry_id:267880) between [stress and strain rate](@entry_id:263123), a vast number of fluids encountered in nature and industry defy this Newtonian ideal. Materials such as polymer melts, paints, biological fluids, and geophysical flows exhibit complex rheological behaviors that fundamentally alter their dynamics. The field of non-Newtonian computational fluid dynamics (CFD) addresses the crucial challenge of predicting the behavior of these materials, where viscosity can change with shear rate, and fluids can exhibit both liquid-like and solid-like (viscoelastic) properties. A mastery of this topic is essential for engineers and scientists seeking to design processes, develop new materials, and understand the natural world.

This article provides a comprehensive journey into the principles, applications, and practice of non-Newtonian rheology in CFD. It bridges the gap between fundamental theory and practical implementation, equipping you with the knowledge to tackle complex fluid flow problems. We will begin in the first chapter, **Principles and Mechanisms**, by systematically building the theoretical framework, from Generalized Newtonian models for shear-thinning and [yield-stress fluids](@entry_id:196553) to foundational [viscoelastic models](@entry_id:192483) like the Oldroyd-B, exploring their microstructural origins and the unique phenomena they predict. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate how these models are leveraged to solve real-world problems in diverse fields such as [chemical engineering](@entry_id:143883), polymer processing, and [bioengineering](@entry_id:271079). Finally, the **Hands-On Practices** chapter offers a series of guided problems to solidify your understanding of key concepts, from deriving viscometric functions to implementing numerical regularizations.

## Principles and Mechanisms

This chapter delineates the fundamental principles and constitutive mechanisms that govern the behavior of non-Newtonian fluids within the context of [computational fluid dynamics](@entry_id:142614). We will systematically build from the simplest [rheological models](@entry_id:193749) to more complex descriptions that capture the hallmark phenomena of viscoelasticity, connecting macroscopic behavior to microscopic origins and addressing key computational challenges.

### Generalized Newtonian Fluid Models

The most direct extension of the Newtonian fluid model is the **Generalized Newtonian Fluid (GNF)**. In this framework, the fluid remains purely viscous, meaning the stress responds instantaneously to the [rate of strain](@entry_id:267998). However, unlike a Newtonian fluid where viscosity is a constant material property, the viscosity of a GNF is a function of the deformation rate. The constitutive relationship for the deviatoric (or extra) stress tensor, $\boldsymbol{\tau}$, is given by:

$$
\boldsymbol{\tau} = 2 \eta(\dot{\gamma}) \mathbf{D}
$$

Here, $\mathbf{D} = \frac{1}{2}(\nabla\mathbf{u} + (\nabla\mathbf{u})^\top)$ is the symmetric [rate-of-deformation tensor](@entry_id:184787), and $\eta(\dot{\gamma})$ is the **[apparent viscosity](@entry_id:260802)**. The [apparent viscosity](@entry_id:260802) depends on the magnitude of the deformation, which is quantified by the **effective shear rate**, $\dot{\gamma}$. This [scalar invariant](@entry_id:159606) is defined from the second invariant of the [rate-of-deformation tensor](@entry_id:184787): $\dot{\gamma} = \sqrt{2 \mathbf{D}:\mathbf{D}}$.

#### Shear-Rate Dependent Viscosity: The Power-Law Model

A ubiquitous and empirically useful GNF is the **[power-law model](@entry_id:272028)**, also known as the Ostwald-de Waele model. It describes the [apparent viscosity](@entry_id:260802) as:

$$
\eta(\dot{\gamma}) = K \dot{\gamma}^{n-1}
$$

In this expression, $K$ is the **consistency index** (with units of $\text{Pa}\cdot\text{s}^n$), and $n$ is the dimensionless **[flow behavior index](@entry_id:265017)**. The nature of the fluid's response is determined by the value of $n$ . We can classify the behavior by examining how the viscosity changes with the shear rate, which is determined by the sign of the derivative $\frac{\partial\eta}{\partial\dot{\gamma}}$:

$$
\frac{\partial\eta}{\partial\dot{\gamma}} = \frac{\partial}{\partial\dot{\gamma}}(K \dot{\gamma}^{n-1}) = K(n-1)\dot{\gamma}^{n-2}
$$

Since $K>0$ and $\dot{\gamma}>0$, the term $\dot{\gamma}^{n-2}$ is always positive. Therefore, the sign of the derivative is dictated solely by the factor $(n-1)$. This leads to three distinct behaviors:

1.  **Shear-thinning (Pseudoplastic)**: For $n  1$, we have $(n-1)  0$, which makes $\frac{\partial\eta}{\partial\dot{\gamma}}  0$. The [apparent viscosity](@entry_id:260802) decreases as the fluid is sheared more rapidly. This is the most common non-Newtonian behavior, observed in materials like paints, ketchup, and many [polymer solutions](@entry_id:145399). For instance, paint flows easily when brushed (high shear rate) but is thick enough not to drip off the brush (low shear rate).

2.  **Newtonian**: For $n = 1$, we have $(n-1) = 0$, making $\frac{\partial\eta}{\partial\dot{\gamma}} = 0$. The viscosity $\eta = K$ is constant, and we recover the Newtonian fluid model.

3.  **Shear-thickening (Dilatant)**: For $n > 1$, we have $(n-1) > 0$, which makes $\frac{\partial\eta}{\partial\dot{\gamma}} > 0$. The [apparent viscosity](@entry_id:260802) increases with the shear rate. This behavior is seen in concentrated suspensions, such as a mixture of cornstarch and water, which can feel fluid when stirred slowly but becomes almost solid when struck suddenly. A specific case is when $n=2$, where the viscosity increases linearly with the shear rate, and $\frac{\partial\eta}{\partial\dot{\gamma}} = K$ becomes a positive constant .

While simple, the [power-law model](@entry_id:272028) has unphysical limits, predicting infinite viscosity as $\dot{\gamma} \to 0$ for [shear-thinning fluids](@entry_id:265951) and zero viscosity for [shear-thickening fluids](@entry_id:262963). More complex models like the Carreau-Yasuda model address this by introducing plateaus for viscosity at very low and very high shear rates.

#### Yield Stress Fluids

A distinct class of materials, known as **[viscoplastic fluids](@entry_id:271743)**, behave like a rigid solid below a certain stress threshold and flow like a liquid above it. This threshold is called the **[yield stress](@entry_id:274513)**, denoted $\tau_y$. In regions where the magnitude of the stress is below the [yield stress](@entry_id:274513), the material does not deform. This condition defines **[plug flow](@entry_id:263994)** regions in a flow field :

$$
\|\boldsymbol{\tau}\| \le \tau_y \implies \mathbf{D} = \mathbf{0}
$$

where $\|\boldsymbol{\tau}\| = \sqrt{\frac{1}{2}\boldsymbol{\tau}:\boldsymbol{\tau}}$ is the von Mises stress invariant. When the stress exceeds $\tau_y$, the material "yields" and begins to flow. Two common models describe this yielded behavior:

-   The **Bingham model** is the simplest viscoplastic model, describing the yielded state with a [linear relationship](@entry_id:267880) between [stress and strain rate](@entry_id:263123):
    $$
    \|\boldsymbol{\tau}\| = \tau_y + \mu_p \dot{\gamma}, \quad \text{for } \|\boldsymbol{\tau}\|  \tau_y
    $$
    Here, $\mu_p$ is the **[plastic viscosity](@entry_id:267041)**, which governs the fluid's resistance to flow once yielded. The corresponding tensor form that ensures coaxiality between [stress and strain rate](@entry_id:263123) is $\boldsymbol{\tau} = \left(\mu_p + \frac{\tau_y}{\dot{\gamma}}\right) 2\mathbf{D}$.

-   The **Herschel-Bulkley model** generalizes the Bingham model by combining [yield stress](@entry_id:274513) with power-law behavior in the yielded state:
    $$
    \|\boldsymbol{\tau}\| = \tau_y + K \dot{\gamma}^n, \quad \text{for } \|\boldsymbol{\tau}\|  \tau_y
    $$
    This model can describe materials that are both viscoplastic and [shear-thinning](@entry_id:150203) ($n1$) or [shear-thickening](@entry_id:260777) ($n1$). Toothpaste and grease are common examples of [yield-stress fluids](@entry_id:196553).

### Introduction to Viscoelasticity

While GNFs capture shear-rate dependency, they lack what is arguably the most fascinating aspect of [complex fluids](@entry_id:198415): memory. **Viscoelastic fluids** exhibit both viscous (liquid-like) and elastic (solid-like) characteristics. Their current state of stress depends not only on the instantaneous rate of deformation but also on the history of deformation. This memory effect is the origin of many counter-intuitive phenomena.

#### Linear Viscoelasticity: The Building Blocks

To understand the concept of memory, it is instructive to start with **[linear viscoelasticity](@entry_id:181219) (LVE)**, which describes the response to infinitesimally small deformations. The behavior of LVE materials can be idealized using mechanical analogues of springs (which store energy, representing elasticity) and dashpots (which dissipate energy, representing viscosity) .

-   The **Maxwell model** consists of a spring and a dashpot in series. It is the simplest model to capture **[stress relaxation](@entry_id:159905)**. If a constant strain is applied, the [initial stress](@entry_id:750652) relaxes exponentially over time with a characteristic **relaxation time**, $\lambda = \eta/G$, where $\eta$ is the dashpot viscosity and $G$ is the spring modulus. Its differential form is $\sigma + \lambda \dot{\sigma} = \eta \dot{\varepsilon}$.

-   The **Kelvin-Voigt model** consists of a spring and a dashpot in parallel. It is a simple model for **creep**. When a constant stress is applied, the strain approaches its final value gradually.

These simple LVE models introduce the crucial concept of a [relaxation time](@entry_id:142983), $\lambda$, which quantifies the material's memory. While LVE is limited to small deformations, it provides the conceptual basis for the more complex nonlinear models required for general CFD simulations.

#### Nonlinear Viscoelasticity: The Oldroyd-B Model

For finite deformations typical in CFD, we require nonlinear [viscoelastic models](@entry_id:192483). The **Oldroyd-B model** is a [canonical model](@entry_id:148621) for dilute [polymer solutions](@entry_id:145399) and serves as a cornerstone of [computational rheology](@entry_id:747633) . It models the fluid as a two-component mixture: a Newtonian solvent with viscosity $\eta_s$, and dissolved polymer chains that contribute an elastic component to the stress.

The total extra stress tensor $\boldsymbol{\tau}$ is decomposed as:
$$
\boldsymbol{\tau} = \boldsymbol{\tau}_s + \boldsymbol{\tau}_p = 2\eta_s\mathbf{D} + \boldsymbol{\tau}_p
$$
where $\boldsymbol{\tau}_s$ is the solvent stress and $\boldsymbol{\tau}_p$ is the polymer stress.

The key challenge in formulating an evolution equation for $\boldsymbol{\tau}_p$ is ensuring that the model is independent of the observer's reference frame, a principle known as **[material frame indifference](@entry_id:166014)**. A simple time derivative $\frac{\partial\boldsymbol{\tau}_p}{\partial t}$ is not objective. An objective time derivative must be used. For models derived from the [kinetic theory](@entry_id:136901) of polymers, the appropriate derivative is the **[upper-convected derivative](@entry_id:756365)**, defined for a tensor $\mathbf{A}$ as:
$$
\overset{\nabla}{\mathbf{A}} \equiv \frac{D\mathbf{A}}{Dt} - (\nabla\mathbf{u})\cdot\mathbf{A} - \mathbf{A}\cdot(\nabla\mathbf{u})^\top
$$
where $\frac{D}{Dt}$ is the [material derivative](@entry_id:266939). The [upper-convected derivative](@entry_id:756365) correctly accounts for the rotation and stretching of the tensor with the flow.

The evolution of the polymer stress in the Oldroyd-B model is given by an upper-convected Maxwell equation:
$$
\boldsymbol{\tau}_p + \lambda \overset{\nabla}{\boldsymbol{\tau}_p} = 2\eta_p\mathbf{D}
$$
Here, $\lambda$ is the polymer relaxation time and $\eta_p$ is the polymer contribution to the viscosity. The total zero-[shear viscosity](@entry_id:141046) of the fluid is $\eta_0 = \eta_s + \eta_p$.

### Microstructural Foundations: The Conformation Tensor

The Oldroyd-B model, while macroscopic, has a firm grounding in the microscopic physics of polymer chains. A simple yet powerful microscopic model is the **Hookean dumbbell**, which represents a polymer chain as two beads connected by a linear spring . The state of the polymer solution can be described by the statistical distribution of the dumbbell end-to-end vectors, $\mathbf{q}$.

Rather than tracking the full [distribution function](@entry_id:145626), we can work with its second moment, the **conformation tensor** $\mathbf{A}$:
$$
\mathbf{A}(\mathbf{x}, t) = \langle \mathbf{q}\mathbf{q} \rangle
$$
The conformation tensor is a [symmetric positive-definite](@entry_id:145886) tensor that describes the average stretch and orientation of the polymer chains. An isotropic state corresponds to $\mathbf{A} \propto \mathbf{I}$, whereas anisotropic stretch is captured by the off-diagonal components and differing diagonal components.

The kinetic theory of Hookean dumbbells leads to a closed evolution equation for the conformation tensor:
$$
\mathbf{A} + \lambda \overset{\nabla}{\mathbf{A}} = \frac{k_B T}{H}\mathbf{I}
$$
where $k_B$ is the Boltzmann constant, $T$ is temperature, and $H$ is the [spring constant](@entry_id:167197) of the dumbbell. This equation reveals that in a flow, the conformation tensor evolves towards a state determined by a balance between advective stretching (the $\overset{\nabla}{\mathbf{A}}$ term) and relaxation towards the isotropic equilibrium state $(k_B T / H)\mathbf{I}$.

The macroscopic polymer stress $\boldsymbol{\tau}_p$ is directly related to the microscopic conformation via the **Kramers expression**:
$$
\boldsymbol{\tau}_p = n_p H \langle \mathbf{q}\mathbf{q} \rangle - n_p k_B T \mathbf{I} = n_p H \mathbf{A} - n_p k_B T \mathbf{I}
$$
where $n_p$ is the number density of dumbbells. Using the relations for the polymer modulus $G = n_p k_B T$ and viscosity $\eta_p = G\lambda$, this can be written as:
$$
\boldsymbol{\tau}_p = G(\mathbf{A} - \mathbf{I}) = \frac{\eta_p}{\lambda}(\mathbf{A} - \mathbf{I})
$$
(assuming a normalization where $\mathbf{A}_{eq}=\mathbf{I}$). This formulation in terms of the conformation tensor is often preferred in CFD as it guarantees the physical [realizability](@entry_id:193701) of the stress tensor. For instance, in a steady simple shear flow $\mathbf{u} = (\dot{\gamma}y, 0, 0)$, this model predicts a constant shear stress $\tau_{p,xy} = \eta_p \dot{\gamma}$ .

### Characteristic Phenomena of Viscoelastic Flows

Differential [constitutive models](@entry_id:174726) like Oldroyd-B predict a host of phenomena not seen in Newtonian or Generalized Newtonian fluids.

#### Normal Stress Differences and the Weissenberg Effect

In a simple shear flow, a Newtonian fluid only generates a shear stress. A viscoelastic fluid, however, also develops **[normal stress differences](@entry_id:191914)**. These are defined as:

-   First Normal Stress Difference: $N_1 = \sigma_{xx} - \sigma_{yy} = \tau_{xx} - \tau_{yy}$
-   Second Normal Stress Difference: $N_2 = \sigma_{yy} - \sigma_{zz} = \tau_{yy} - \tau_{zz}$

For the Oldroyd-B model in steady simple shear, one can solve the [constitutive equation](@entry_id:267976) to find :
$$
N_1 = 2 \eta_p \lambda \dot{\gamma}^2  0
$$
$$
N_2 = 0
$$
The positive first [normal stress difference](@entry_id:199507) $N_1$ signifies a tension along the direction of the [streamlines](@entry_id:266815). This "[hoop stress](@entry_id:190931)" is responsible for the famous **Weissenberg effect**, or rod-climbing phenomenon. When a rod is rotated in a bath of viscoelastic fluid, this tension along the circular streamlines pulls the fluid inwards and forces it to climb the rod, in stark contrast to a Newtonian fluid where centrifugal forces would create a dip at the surface . The height of the climb, $h$, can be estimated by balancing the normal stress with the [hydrostatic pressure](@entry_id:141627): $\rho g h \sim N_1$.

#### Extensional Viscosity and Trouton Ratio

Viscoelastic fluids often behave dramatically differently in extensional (stretching) flows compared to shear flows. We can define an **extensional viscosity** as the ratio of the principal tensile stress difference to the extension rate $\dot{\varepsilon}$. For a steady uniaxial extension, the **uniaxial extensional viscosity** is $\eta_{E,u} = (\sigma_{zz} - \sigma_{xx})/\dot{\varepsilon}$. For planar extension, it is $\eta_{E,p} = (\sigma_{xx} - \sigma_{yy})/\dot{\varepsilon}$.

The **Trouton ratio**, $Tr$, is the ratio of the extensional viscosity to the shear viscosity, $\eta$. For a Newtonian fluid, this ratio is a constant: $Tr_u = 3$ for uniaxial extension and $Tr_p = 4$ for planar extension . For [viscoelastic fluids](@entry_id:198948), however, the Trouton ratio can be a strong function of the extension rate. In the limit of very slow flows, the viscoelastic fluid behaves like a Newtonian fluid with viscosity $\eta_0$, so the Trouton ratios approach their Newtonian values. However, as $\dot{\varepsilon}$ increases, polymer stretching can cause a dramatic rise in extensional viscosity, a phenomenon known as **[strain hardening](@entry_id:160233)**, leading to Trouton ratios that are orders of magnitude larger than 3 or 4. This high resistance to stretching is critical in processes like [fiber spinning](@entry_id:159058) and [film blowing](@entry_id:195775).

#### Dimensionless Groups in Viscoelastic Flow

The interplay between inertia, viscosity, and elasticity is governed by a set of [dimensionless numbers](@entry_id:136814), which can be derived by non-dimensionalizing the governing equations .

-   **Reynolds Number ($Re = \rho UL/\eta_0$)**: The familiar ratio of [inertial forces](@entry_id:169104) to viscous forces.
-   **Weissenberg Number ($Wi = \lambda U/L$)**: The ratio of the fluid's relaxation time $\lambda$ to a [characteristic time scale](@entry_id:274321) of the flow, $L/U$. It quantifies the importance of elasticity. For $Wi \ll 1$, the fluid has time to relax and behaves like a GNF. For $Wi \gg 1$, elastic effects dominate.
-   **Deborah Number ($De = \lambda/T$)**: Similar to $Wi$, but it compares the relaxation time to a [characteristic time scale](@entry_id:274321) of the *observation*, $T$, which may be different from the flow time scale (e.g., the period of an oscillation).
-   **Viscosity Ratio ($\beta = \eta_s / \eta_0$)**: In two-fluid models like Oldroyd-B, this ratio specifies the solvent's contribution to the total viscosity.

### Advanced Models and Computational Considerations

The Oldroyd-B model, while foundational, has limitations: it predicts a constant [shear viscosity](@entry_id:141046) and zero second [normal stress difference](@entry_id:199507), which is contrary to experimental observations for many [polymer solutions](@entry_id:145399). More advanced models have been developed to capture this richer physics.

#### The Giesekus Model

The **Giesekus model** extends the Oldroyd-B model by introducing a nonlinear term that accounts for **anisotropic hydrodynamic drag** on the polymer molecules . Its equation for the polymer stress is:
$$
\boldsymbol{\tau}_p + \lambda \overset{\nabla}{\boldsymbol{\tau}_p} + \frac{\alpha \lambda}{\eta_p}(\boldsymbol{\tau}_p \cdot \boldsymbol{\tau}_p) = 2\eta_p\mathbf{D}
$$
The new quadratic term is governed by the **mobility factor** $\alpha \in [0, 1/2]$. When $\alpha = 0$, the model reduces to the UCM/Oldroyd-B model. When $\alpha  0$, this term has profound effects:
-   It produces **shear-thinning** [apparent viscosity](@entry_id:260802).
-   It predicts a **non-zero, negative second [normal stress difference](@entry_id:199507)** ($N_2  0$), which is in qualitative agreement with experiments for many [polymer solutions](@entry_id:145399).

The Giesekus model provides a more realistic description while retaining the structure of a differential [constitutive model](@entry_id:747751).

#### The High-Weissenberg Number Problem (HWNP)

A major challenge in the [numerical simulation](@entry_id:137087) of [viscoelastic flows](@entry_id:276797) is the **High-Weissenberg Number Problem (HWNP)** . This is a numerical instability that occurs in simulations at high $Wi$, where standard [numerical schemes](@entry_id:752822) fail. The root cause is the failure of the [discretization](@entry_id:145012) to preserve the [symmetric positive-definite](@entry_id:145886) (SPD) property of the conformation tensor $\mathbf{A}$.

The continuous evolution equation for $\mathbf{A}$ mathematically guarantees that if $\mathbf{A}$ is initially SPD, it remains so for all time. However, standard [numerical schemes](@entry_id:752822) for the [transport equation](@entry_id:174281) involve linear updates in matrix space. The strong advective and source terms at high $Wi$ can cause the numerical solution $\mathbf{A}^{n+1}$ to "step over" the boundary of the SPD cone, resulting in a tensor with negative eigenvalues. This is unphysical and leads to a catastrophic blow-up of the simulation.

A powerful and widely used solution to the HWNP is the **log-conformation transformation**. This technique, pioneered by Fattal and Kupferman, involves a change of variables to the [matrix logarithm](@entry_id:169041) of the conformation tensor, $\boldsymbol{\Psi} = \log\mathbf{A}$. The key advantages are:
1.  **Guaranteed Positive-Definiteness**: The evolution equation is solved for the [symmetric tensor](@entry_id:144567) $\boldsymbol{\Psi}$. The conformation tensor is then recovered at each step by taking the [matrix exponential](@entry_id:139347), $\mathbf{A} = \exp(\boldsymbol{\Psi})$. Since the exponential of any real [symmetric matrix](@entry_id:143130) is always SPD, this procedure inherently enforces the physical constraint on $\mathbf{A}$.
2.  **Improved Stability**: The transformation results in a more stable evolution equation for $\boldsymbol{\Psi}$, where the terms that cause exponential growth in the original formulation are tamed. This allows for stable computations at much higher Weissenberg numbers, enabling the exploration of highly elastic [flow regimes](@entry_id:152820).

By understanding these principles, models, and computational strategies, researchers and engineers can effectively simulate and analyze the complex and fascinating behavior of non-Newtonian fluids.