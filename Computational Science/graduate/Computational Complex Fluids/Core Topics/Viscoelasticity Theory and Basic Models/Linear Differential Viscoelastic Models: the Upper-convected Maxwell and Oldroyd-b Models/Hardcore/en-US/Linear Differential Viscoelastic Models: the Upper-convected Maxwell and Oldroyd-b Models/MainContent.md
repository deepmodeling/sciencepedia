## Introduction
Many common materials, from [polymer solutions](@entry_id:145399) and molten plastics to biological fluids, exhibit complex flow behaviors that defy simple classification as either a solid or a liquid. These "viscoelastic" fluids possess both the energy-dissipating properties of a viscous liquid and the energy-storing properties of an elastic solid, endowing them with a "memory" of their past deformation. Capturing this behavior mathematically is a central challenge in rheology and fluid mechanics. While simple one-dimensional models can introduce the concept of [viscoelasticity](@entry_id:148045), extending them to three-dimensional flows requires a rigorous framework to ensure physical predictions are independent of the observer's frame of reference, addressing a key knowledge gap left by naive generalizations.

This article provides a comprehensive exploration of two foundational differential [viscoelastic models](@entry_id:192483): the Upper-Convected Maxwell (UCM) and Oldroyd-B models. It serves as a guide for graduate students and researchers in [computational complex fluids](@entry_id:1122778), bridging the gap between abstract theory and practical application. The journey begins in **Principles and Mechanisms**, where we will construct these models from the ground up, explore their microstructural origins in polymer kinetic theory, and analyze their predictive power—and critical failures—in canonical flow fields. Next, **Applications and Interdisciplinary Connections** will showcase the models' utility in explaining macroscopic phenomena like the rod-climbing effect, connecting to experimental [rheometry](@entry_id:184183), and framing advanced challenges in computational science and [soft matter physics](@entry_id:145473). Finally, **Hands-On Practices** offers a set of curated problems designed to reinforce these concepts and develop a working command of the models.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanics of elementary differential [viscoelastic models](@entry_id:192483), focusing on the Upper-Convected Maxwell (UCM) and Oldroyd-B models. We will construct these models from first principles, explore their microstructural underpinnings, analyze their predictions in canonical flow fields, and critically evaluate their limitations.

### From One-Dimensional Models to Frame-Invariant Tensors

The concept of [viscoelasticity](@entry_id:148045) can be introduced using a simple one-dimensional mechanical analogue: the **Maxwell element**. This element consists of a linear elastic spring and a linear viscous dashpot connected in series. The spring represents the solid-like elastic energy storage, where stress ($\sigma$) is proportional to strain ($\gamma_s$): $\sigma = G \gamma_s$, with $G$ being the elastic modulus. The dashpot represents the liquid-like viscous [energy dissipation](@entry_id:147406), where stress is proportional to the strain rate ($\dot{\gamma}_d$): $\sigma = \eta_p \dot{\gamma}_d$, with $\eta_p$ being the polymer viscosity.

In a series arrangement, the stress $\sigma$ is uniform across both elements, and the total strain rate $\dot{\gamma}$ is the sum of the individual rates, $\dot{\gamma} = \dot{\gamma}_s + \dot{\gamma}_d$. By differentiating the spring law with respect to time, we find $\dot{\gamma}_s = (1/G)\dot{\sigma}$. Combining these relations yields:
$$ \dot{\gamma} = \frac{1}{G}\dot{\sigma} + \frac{1}{\eta_p}\sigma $$
Rearranging this equation to express the evolution of stress gives the celebrated **scalar Maxwell model**:
$$ \sigma + \lambda \dot{\sigma} = \eta_p \dot{\gamma} $$
Here, we have introduced the **relaxation time**, $\lambda = \eta_p / G$, a [characteristic timescale](@entry_id:276738) representing the time required for the stress in the material to relax after a deformation is ceased. This simple equation captures the essence of viscoelastic memory: the current stress depends not only on the current [rate of strain](@entry_id:267998) but also on its history, encapsulated by the time-derivative term .

To be useful in fluid dynamics, this scalar model must be generalized to a three-dimensional, tensorial framework. A naive extension might replace the scalar stress $\sigma$ with the polymeric extra stress tensor $\boldsymbol{\tau}$, the scalar strain rate $\dot{\gamma}$ with the [rate-of-deformation tensor](@entry_id:184787) $2\boldsymbol{D}$, and the time derivative $\dot{(\cdot)}$ with the material derivative $D(\cdot)/Dt$. However, such a "naïve extension" is physically invalid because it is not **objective**, or **frame-indifferent**. An objective [constitutive equation](@entry_id:267976) must yield the same physical predictions regardless of the observer's [rigid-body motion](@entry_id:265795) (e.g., translation or rotation). The [material derivative](@entry_id:266939) of a tensor is not objective; it produces spurious stresses in a fluid undergoing simple rigid-body rotation .

### Kinematic Decomposition and Objective Derivatives

To construct a valid tensorial model, we must first understand the kinematics of fluid motion. The velocity gradient tensor, $\mathbf{L} = \nabla \boldsymbol{v}$, can be uniquely decomposed into a symmetric part and an antisymmetric part:
$$ \mathbf{L} = \mathbf{D} + \mathbf{W} $$
where
$$ \boldsymbol{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^{\top}) \quad \text{and} \quad \boldsymbol{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^{\top}) $$
The [symmetric tensor](@entry_id:144567) $\boldsymbol{D}$ is the **[rate-of-deformation tensor](@entry_id:184787)** (or [rate-of-strain tensor](@entry_id:260652)), which describes how material elements are stretched and distorted. The [antisymmetric tensor](@entry_id:191090) $\boldsymbol{W}$ is the **[vorticity tensor](@entry_id:189621)** (or [spin tensor](@entry_id:187346)), which describes the rate of rigid-body rotation of material elements.

Crucially, it is the deformation, encoded by $\boldsymbol{D}$, that generates stress in a material. Pure rigid-body rotation, described by $\boldsymbol{W}$ (where $\boldsymbol{D}=\boldsymbol{0}$), should not generate any elastic stress. Therefore, in a valid constitutive model, the "source" term that creates stress must be exclusively a function of $\boldsymbol{D}$. The [vorticity tensor](@entry_id:189621) $\boldsymbol{W}$, along with $\boldsymbol{D}$, will appear in the time derivative to ensure it correctly accounts for the rotation and advection of the stress tensor, satisfying the [principle of objectivity](@entry_id:185412) .

This leads to the concept of **[objective time derivatives](@entry_id:189677)**. These are special derivative operators that are invariant under changes of observer frame. For a second-order tensor $\boldsymbol{\tau}$, several such derivatives exist, including:
- The **[upper-convected derivative](@entry_id:756365)**: $\overset{\triangledown}{\boldsymbol{\tau}} = \frac{D\boldsymbol{\tau}}{Dt} - \mathbf{L}\boldsymbol{\tau} - \boldsymbol{\tau}\mathbf{L}^{\top}$
- The **[lower-convected derivative](@entry_id:1127499)**: $\underset{\triangledown}{\boldsymbol{\tau}} = \frac{D\boldsymbol{\tau}}{Dt} + \mathbf{L}^{\top}\boldsymbol{\tau} + \boldsymbol{\tau}\mathbf{L}$
- The **co-rotational (or Jaumann) derivative**: $\overset{\circ}{\boldsymbol{\tau}} = \frac{D\boldsymbol{\tau}}{Dt} + \boldsymbol{\tau}\boldsymbol{W} - \boldsymbol{W}\boldsymbol{\tau}$

The choice between these derivatives is not arbitrary but is informed by the underlying microstructure of the fluid. For many [polymer solutions](@entry_id:145399), the stress arises from the deformation of molecular structures that are stretched and transported by the flow. If these structures are assumed to deform **affinely** (i.e., their constituent points move with the macroscopic fluid velocity), the resulting stress tensor behaves mathematically as a **contravariant** second-order tensor. The transport rule consistent with a contravariant tensor is the upper-convected derivative. This provides a strong physical justification for its use in [polymer rheology](@entry_id:144905) .

### The Upper-Convected Maxwell and Oldroyd-B Models

Using the upper-convected derivative, we can now formulate a frame-invariant generalization of the Maxwell model. This is the **Upper-Convected Maxwell (UCM) model**:
$$ \boldsymbol{\tau} + \lambda \overset{\triangledown}{\boldsymbol{\tau}} = 2 \eta_p \boldsymbol{D} $$
This model describes a purely viscoelastic fluid with relaxation time $\lambda$ and viscosity $\eta_p$.

Many real [polymer solutions](@entry_id:145399), however, consist of polymer molecules dissolved in a simple viscous liquid, such as water or oil. The **Oldroyd-B model** captures this by describing the fluid as a parallel combination of two components: a polymeric contribution that behaves as a UCM fluid, and a purely viscous Newtonian solvent. The total extra stress tensor $\boldsymbol{T}$ is the sum of the polymeric stress $\boldsymbol{\tau}_p$ and the solvent stress $\boldsymbol{\tau}_s$:
$$ \boldsymbol{T} = \boldsymbol{\tau}_p + \boldsymbol{\tau}_s $$
where the solvent stress is given by the standard Newtonian law, $\boldsymbol{\tau}_s = 2\eta_s\boldsymbol{D}$ (with $\eta_s$ being the solvent viscosity), and the polymeric stress follows the UCM evolution:
$$ \boldsymbol{\tau}_p + \lambda \overset{\triangledown}{\boldsymbol{\tau}}_p = 2 \eta_p \boldsymbol{D} $$
The total stress in the fluid is then given by the Cauchy stress tensor $\boldsymbol{\sigma} = -p\mathbf{I} + \boldsymbol{T}$, where $p$ is the isotropic pressure and $\mathbf{I}$ is the identity tensor . This two-component formulation provides a simple yet powerful framework for describing dilute [polymer solutions](@entry_id:145399).

### Microstructural Origins: The Hookean Dumbbell Model

The macroscopic UCM and Oldroyd-B models can be rigorously derived from a microscopic model of polymer chains in solution. The simplest such model is the **Hookean dumbbell model**, which represents a polymer chain as two "beads" connected by a frictionless linear (Hookean) spring . The beads experience hydrodynamic drag from the solvent and random thermal kicks (Brownian motion), while the spring exerts an entropic restoring force.

From the force balance on the beads, one can derive an evolution equation for the probability distribution of the dumbbell's end-to-end vector, $\mathbf{q}$. From this, an evolution equation for the second moment of this vector, $\langle \mathbf{q}\mathbf{q} \rangle$, can be obtained. This second-moment tensor is known as the **conformation tensor**, often denoted $\boldsymbol{A}$, and it describes the average shape and orientation of the polymer chains. For a Hookean dumbbell model, the evolution of a suitably non-dimensionalized [conformation tensor](@entry_id:1122882) $\boldsymbol{A}$ is found to be :
$$ \overset{\triangledown}{\boldsymbol{A}} = -\frac{1}{\lambda}(\boldsymbol{A} - \boldsymbol{I}) $$
At equilibrium (no flow), the polymer coils are, on average, isotropic, so $\boldsymbol{A}_{eq} = \boldsymbol{I}$. Under flow, $\boldsymbol{A}$ deviates from the identity, representing the stretching and alignment of the polymer chains.

The macroscopic polymeric stress $\boldsymbol{\tau}_p$ is directly related to the average conformation of the polymer chains. Using the Kramers expression from kinetic theory, the stress is found to be proportional to the deviation of the conformation tensor from its equilibrium state:
$$ \boldsymbol{\tau}_p = G (\boldsymbol{A} - \boldsymbol{I}) $$
Here, $G$ is the **[elastic modulus](@entry_id:198862)** of the polymer solution. Combining this stress-conformation relation with the evolution equation for $\boldsymbol{A}$ precisely recovers the UCM [constitutive equation](@entry_id:267976). This microstructural view provides concrete expressions for the macroscopic parameters. The [elastic modulus](@entry_id:198862) is given by $G = n k_B T$, where $n$ is the [number density](@entry_id:268986) of polymers, $k_B$ is the Boltzmann constant, and $T$ is the absolute temperature. The relaxation time $\lambda$ is related to the bead drag coefficient $\zeta$ and the spring constant $H$. Furthermore, the polymer viscosity and relaxation time are related to the modulus via $\eta_p = G\lambda$. This yields two equivalent and powerful expressions for the modulus  :
$$ G = n k_B T = \frac{\eta_p}{\lambda} $$
This connection between the macroscopic rheological parameters and the underlying microscopic physics is a cornerstone of modern polymer science.

### Flow Regimes and Characteristic Dimensionless Numbers

To analyze [viscoelastic flows](@entry_id:276797), it is essential to define dimensionless numbers that characterize the relative importance of different physical effects. For [viscoelasticity](@entry_id:148045), the two most important are the **Weissenberg number ($Wi$)** and the **Deborah number ($De$)**.

- The **Weissenberg number**, $Wi = \lambda \dot{\gamma}_c$, compares the material's relaxation time $\lambda$ to the [characteristic timescale](@entry_id:276738) of the deformation, $1/\dot{\gamma}_c$, where $\dot{\gamma}_c$ is a characteristic magnitude of the [rate-of-deformation tensor](@entry_id:184787) (e.g., $U/L$ for a flow with characteristic velocity $U$ and length scale $L$). $Wi$ quantifies the importance of nonlinear elastic effects. When $Wi \ll 1$, the fluid has ample time to relax, and its response is nearly Newtonian. When $Wi \gtrsim 1$, elastic effects become significant.

- The **Deborah number**, $De = \lambda / T_{proc}$, compares the relaxation time $\lambda$ to a [characteristic timescale](@entry_id:276738) of the flow process, $T_{proc}$. This timescale could be related to the period of an oscillation, the residence time in a device, or the timescale over which boundary conditions change. $De$ quantifies the importance of unsteadiness and memory effects.

In steady flows, the only process timescale is the deformation timescale, so $T_{proc} \sim 1/\dot{\gamma}_c$, and thus $De = Wi$. However, in unsteady flows, they can be distinct and govern different aspects of the response. For example, in small-amplitude oscillatory shear (SAOS) with frequency $\omega$ and strain amplitude $\gamma_0$, the process time is $T_{proc} \sim 1/\omega$ and the characteristic strain rate is $\dot{\gamma}_c \sim \gamma_0 \omega$. This leads to $De = \lambda \omega$ and $Wi = \lambda \gamma_0 \omega$. Here, $De$ governs the linear viscoelastic response (the phase lag between [stress and strain](@entry_id:137374)), while $Wi$ controls the magnitude of nonlinear effects like normal stresses. The [linear viscoelastic regime](@entry_id:193354) is defined by $Wi \ll 1$, which can be satisfied even for large $De$ if the strain amplitude $\gamma_0$ is sufficiently small .

### Predictions in Canonical Flows

Analyzing a model's predictions in simple, well-defined flows is a crucial step in understanding its behavior.

#### Steady Simple Shear Flow

In a steady [simple shear flow](@entry_id:1131665), $\boldsymbol{v} = (\dot{\gamma}y, 0, 0)$, the Oldroyd-B model makes several key predictions. By solving the [constitutive equations](@entry_id:138559), we find the viscometric functions :
- **Shear Viscosity:** $\eta(\dot{\gamma}) = \frac{\sigma_{xy}}{\dot{\gamma}} = \eta_s + \eta_p$. The model predicts a constant shear viscosity, independent of the shear rate.
- **First Normal Stress Difference:** $N_1 = \sigma_{xx} - \sigma_{yy} = 2\eta_p\lambda\dot{\gamma}^2$. The model predicts a positive $N_1$ that grows quadratically with the shear rate. This represents a tension along the streamlines, the cause of phenomena like the Weissenberg (rod-climbing) effect.
- **Second Normal Stress Difference:** $N_2 = \sigma_{yy} - \sigma_{zz} = 0$. The model predicts a zero second normal stress difference.

#### Small-Amplitude Oscillatory Shear (SAOS)

SAOS is a standard rheological experiment used to probe the linear viscoelastic properties of materials. For an applied oscillatory strain, the Oldroyd-B model predicts the [complex viscosity](@entry_id:192623) $\eta^*(\omega) = \eta' - i\eta''$, from which the storage and loss moduli, $G'(\omega)$ and $G''(\omega)$, are derived :
$$ \eta^*(\omega) = \eta_s + \frac{\eta_p}{1 + i\omega\lambda} $$
$$ G'(\omega) = \omega\eta''(\omega) = \frac{\eta_p\lambda\omega^2}{1 + \lambda^2\omega^2} $$
$$ G''(\omega) = \omega\eta'(\omega) = \omega\eta_s + \frac{\eta_p\omega}{1 + \omega^2\lambda^2} $$
The **[storage modulus](@entry_id:201147)** $G'$ represents the elastic (solid-like) character, or energy stored per cycle, while the **[loss modulus](@entry_id:180221)** $G''$ represents the viscous (liquid-like) character, or energy dissipated as heat. At low frequencies ($De = \lambda\omega \ll 1$), $G'' > G'$, indicating predominantly liquid-like behavior. At high frequencies ($De \gg 1$), $G' > G''$, indicating predominantly solid-like (elastic) behavior.

#### Steady Extensional Flow

Extensional flows, where fluid elements are stretched, are particularly revealing for viscoelastic fluids. In a steady uniaxial extensional flow with strain rate $\dot{\varepsilon}$, the Oldroyd-B model predicts that the polymer chains stretch along the principal extension axis. The degree of stretch, captured by the conformation tensor component $A_{xx}$, is given by :
$$ A_{xx} = \frac{1}{1 - 2\lambda\dot{\varepsilon}} = \frac{1}{1 - 2Wi} $$
This expression reveals a critical singularity: as the Weissenberg number $Wi = \lambda\dot{\varepsilon}$ approaches a value of $1/2$, the predicted polymer stretch $A_{xx}$ diverges to infinity. This is known as the **[coil-stretch transition](@entry_id:184176)**.

This microscopic divergence has a dramatic macroscopic consequence. The **extensional viscosity**, $\eta_E$, which is a measure of a fluid's resistance to stretching, also diverges at this critical strain rate. For the Oldroyd-B model, it is given by:
$$ \eta_E = 3\eta_s + \frac{3\eta_p}{(1 - 2\lambda\dot{\varepsilon})(1 + \lambda\dot{\varepsilon})} $$
The divergence as $\dot{\varepsilon} \to (2\lambda)^{-1}$ is a hallmark prediction of the model, signifying an immense resistance to strong extensional flows .

### Model Limitations and the High Weissenberg Number Problem

While the Oldroyd-B model is a foundational tool, its simplifying assumptions lead to several significant predictive failures when compared to experiments on real [polymer solutions](@entry_id:145399) :

1.  **Constant Shear Viscosity:** The model predicts a constant shear viscosity, whereas most polymer solutions exhibit **[shear thinning](@entry_id:274107)**—their viscosity decreases at higher shear rates. This is because [real polymer chains](@entry_id:1130709) align with the flow, reducing their resistance. The Hookean dumbbell model does not capture this alignment mechanism accurately.
2.  **Zero Second Normal Stress Difference:** The model predicts $N_2=0$. Experiments, however, typically measure a small, non-zero (and often negative) $N_2$. This discrepancy arises from the oversimplified isotropic drag and affine deformation assumptions in the dumbbell model.
3.  **Unbounded Extensional Viscosity:** The divergence of the extensional viscosity is a direct result of the Hookean spring, which can be stretched infinitely. Real polymer chains have a finite contour length, a property known as **[finite extensibility](@entry_id:1124989)**. This physical constraint means that real extensional viscosities, while very large, are bounded. The model's prediction of a singularity is therefore unphysical.

This last failure, the extensional singularity, is the root cause of the notorious **High Weissenberg Number Problem (HWNP)** in numerical simulations of [viscoelastic flows](@entry_id:276797). Complex flows, such as [flow past a cylinder](@entry_id:202297) or through a contraction, contain [stagnation points](@entry_id:276398) where the flow is locally extensional. In simulations using the Oldroyd-B model, as the Weissenberg number approaches the critical value, the unphysical [stress singularity](@entry_id:166362) leads to the formation of extremely sharp stress boundary layers that are impossible to resolve with a finite computational mesh, causing the simulation to break down .

Addressing the HWNP requires both numerical and physical improvements. Numerically, techniques like the **log-conformation representation** have been developed to guarantee that the [conformation tensor](@entry_id:1122882) remains positive-definite, a condition often violated by standard schemes in the presence of steep gradients, thereby enhancing stability . Physically, the model itself must be improved. By replacing the Hookean spring with a [non-linear spring](@entry_id:171332) that accounts for [finite extensibility](@entry_id:1124989) (as in the FENE-P model), the extensional singularity is removed. This "regularizes" the model, leading to bounded stresses and alleviating the source of the [numerical instability](@entry_id:137058), allowing for more robust simulations at high Weissenberg numbers.

In summary, the UCM and Oldroyd-B models provide invaluable insight into the fundamental physics of viscoelasticity, including relaxation, normal stresses, and elastic response. However, their limitations highlight the need for more sophisticated models to capture the rich and complex [rheology](@entry_id:138671) of real polymeric materials.