## Introduction
Understanding how local soil deposits modify [earthquake ground motion](@entry_id:748778) is a central task in [geotechnical earthquake engineering](@entry_id:749881). This phenomenon, known as site response, can dramatically amplify shaking and is a critical factor in [seismic hazard](@entry_id:754639) assessment. While simpler frequency-domain methods provide useful estimates, they cannot fully capture the complex, nonlinear, and [history-dependent behavior](@entry_id:750346) of soil under strong shaking. To overcome this limitation, engineers and researchers turn to the more rigorous and physically faithful approach of [site response analysis](@entry_id:754930) in the time domain.

This article provides a graduate-level exploration of this powerful computational method. It addresses the knowledge gap between simplified analyses and the sophisticated simulations required to predict phenomena like [liquefaction](@entry_id:184829) and [soil-structure interaction](@entry_id:755022). By progressing through three comprehensive chapters, the reader will gain a deep understanding of the entire analysis workflow.

First, **Principles and Mechanisms** will establish the theoretical foundation, deriving the governing [equations of motion](@entry_id:170720) and explaining the physics of [wave propagation](@entry_id:144063). This chapter will delve into the critical role of [constitutive modeling](@entry_id:183370), from [linear viscoelasticity](@entry_id:181219) to advanced nonlinear and [effective stress](@entry_id:198048) models that capture [hysteretic damping](@entry_id:750492) and pore pressure generation. Next, **Applications and Interdisciplinary Connections** will demonstrate the method's practical utility, showcasing its use in [model verification](@entry_id:634241), [soil-structure interaction](@entry_id:755022) analysis, [probabilistic risk assessment](@entry_id:194916), and its links to fields like signal processing. Finally, a series of **Hands-On Practices** will provide opportunities to engage directly with core challenges, such as filtering input motions and implementing a stable numerical solver. We begin by dissecting the fundamental principles that form the bedrock of this analysis technique.

## Principles and Mechanisms

The analysis of site response in the time domain represents a direct simulation of the physical process of [seismic wave propagation](@entry_id:165726) through a soil column. Unlike frequency-domain methods that rely on the [principle of superposition](@entry_id:148082) and are thus restricted to linear or equivalent-linear systems, time-domain analysis permits the direct integration of the equations of motion with fully nonlinear, history-dependent [constitutive models](@entry_id:174726). This chapter elucidates the fundamental principles and mechanisms underpinning this powerful computational approach, from the governing differential equations to the intricacies of [constitutive modeling](@entry_id:183370) and the physically consistent application of seismic input.

### The Semi-Discrete Equation of Motion

The foundation of a time-domain [site response analysis](@entry_id:754930) is the [balance of linear momentum](@entry_id:193575). For a soil continuum of domain $\Omega$ with mass density $\rho$, the governing [partial differential equation](@entry_id:141332) is:

$ \rho \ddot{\mathbf{u}} = \nabla \cdot \boldsymbol{\sigma} + \mathbf{b} $

where $\mathbf{u}$ is the displacement vector, $\boldsymbol{\sigma}$ is the Cauchy stress tensor, $\mathbf{b}$ is the [body force](@entry_id:184443) vector (e.g., gravity), and double dots denote the [second partial derivative](@entry_id:172039) with respect to time (acceleration). In typical one-dimensional (1D) [site response analysis](@entry_id:754930) considering vertically propagating horizontal shear waves, [body forces](@entry_id:174230) are often neglected, and the equation simplifies considerably.

To solve this equation numerically, the continuous soil domain is discretized, most commonly using the **Finite Element (FE) method**. This procedure transforms the partial differential equation into a system of second-order ordinary differential equations in time. Through a standard Galerkin [weak form](@entry_id:137295) procedure, where the governing equation is multiplied by a set of weighting functions (chosen to be the [shape functions](@entry_id:141015) $\mathbf{N}$) and integrated over the domain, one arrives at the semi-discrete [equation of motion](@entry_id:264286):

$ \mathbf{M}\ddot{\mathbf{U}}(t) + \mathbf{C}\dot{\mathbf{U}}(t) + \mathbf{K}\mathbf{U}(t) = \mathbf{F}(t) $

Here, $\mathbf{U}(t)$ is the global vector of nodal displacements as a function of time. The matrices $\mathbf{M}$, $\mathbf{C}$, and $\mathbf{K}$ are the global mass, damping, and stiffness matrices, respectively, assembled from element-level contributions. The vector $\mathbf{F}(t)$ represents the nodal forces arising from external sources, such as boundary tractions or [body forces](@entry_id:174230). The formulation and interpretation of these matrices and vectors, particularly the damping matrix $\mathbf{C}$ and the force vector $\mathbf{F}(t)$, are central to the entire analysis and will be the focus of subsequent sections [@problem_id:3559369].

### Fundamentals of Wave Propagation in Layered Media

Before examining the complexities of [nonlinear material models](@entry_id:193383) and boundary conditions, it is instructive to review the behavior of [elastic waves](@entry_id:196203) in layered media from first principles. The amplification or de-amplification of [seismic waves](@entry_id:164985) is a direct consequence of wave reflections and transmissions at interfaces between layers with different properties.

The key property governing these interactions is the **shear impedance**, $Z$, defined as the product of mass density $\rho$ and shear-wave velocity $c_s$:

$ Z = \rho c_s $

Consider a simple scenario of an upgoing shear wave in a bedrock layer (Layer 2) impinging upon an overlying soil layer (Layer 1). At the interface, a portion of the wave's energy is transmitted into Layer 1, and a portion is reflected back into Layer 2. The amplitudes of the transmitted and reflected waves are governed by the impedance contrast between the two layers. By enforcing continuity of displacement and traction at the interface, one can derive the [reflection and transmission coefficients](@entry_id:149385).

For instance, at a traction-free surface, the boundary condition of zero shear stress requires that an upgoing wave reflects entirely as a downgoing wave of the same amplitude and polarity (for particle velocity). This leads to a doubling of particle velocity and motion at the free surface. At the base of the soil layer, a downgoing wave will reflect upwards. The amplitude and polarity of this reflection depend on the impedance contrast with the underlying bedrock. For a soil layer with impedance $Z_1$ over a stiffer bedrock with impedance $Z_2 > Z_1$, the velocity reflection coefficient for a downgoing wave at the base is given by $R_{v,base} = (Z_1 - Z_2) / (Z_1 + Z_2)$. Since $Z_1  Z_2$, this coefficient is negative, meaning the particle velocity pulse will invert its polarity upon reflection from the base.

This process of reverberation within the soil layer—waves traveling up, reflecting off the free surface, traveling down, and reflecting off the base—forms the physical basis for site-specific frequency-dependent amplification. A short input pulse at the base generates a train of pulses at the surface, separated by the round-trip travel time in the layer ($2h/c_{s1}$), with amplitudes that decay and alternate in polarity due to the reflections at the base. This idealized behavior provides essential intuition for interpreting the results of more complex numerical simulations [@problem_id:3559366].

### Constitutive Modeling of Dynamic Soil Behavior

The accuracy of a time-domain [site response analysis](@entry_id:754930) depends critically on the [constitutive model](@entry_id:747751) used to relate [stress and strain](@entry_id:137374), which determines the stiffness matrix $\mathbf{K}$ and damping matrix $\mathbf{C}$. Soils exhibit complex behavior that is both highly nonlinear and dissipative.

#### Linear Viscoelasticity: The Basis for Damping

To understand material damping, we begin with the theory of **[linear viscoelasticity](@entry_id:181219)**, which combines the elastic response of a solid (spring) and the viscous response of a fluid (dashpot). The two simplest models are the **Kelvin-Voigt model** (spring and dashpot in parallel) and the **Maxwell model** (spring and dashpot in series).

-   The **Kelvin-Voigt model** results in the stress-strain relation $\tau = G\gamma + \eta\dot{\gamma}$, where $G$ is the [shear modulus](@entry_id:167228) and $\eta$ is viscosity. This model represents a solid with delayed elasticity; under a constant stress, it exhibits **creep** (time-dependent strain) that asymptotically approaches a finite value. Its energy dissipation, represented by the loss angle, increases with loading frequency.

-   The **Maxwell model** has the differential form $\dot{\tau} + (\eta/G)^{-1}\tau = \eta\dot{\gamma}$. It represents a fluid with elastic properties. Under a constant strain, it exhibits **stress relaxation**, where the stress decays exponentially over a characteristic [relaxation time](@entry_id:142983) $\tau_r = \eta/G$. Under constant stress, it creeps indefinitely.

These models, while simplistic, introduce the fundamental concepts of time-dependent material response that are essential for modeling [energy dissipation](@entry_id:147406) (damping) in the time domain [@problem_id:3559392].

For a physically admissible model, the [constitutive law](@entry_id:167255) must adhere to fundamental physical principles. The principle of **causality** requires that the current stress can only depend on the past and present strain history, not future strains. For a linear viscoelastic material described by a Boltzmann superposition integral with a [relaxation modulus](@entry_id:189592) $G(t)$, this implies that the [relaxation modulus](@entry_id:189592) must be zero for negative time, $G(t)=0$ for $t0$. A second principle, **passivity**, derived from the second law of thermodynamics, requires that the material cannot generate energy. For any admissible strain history, the [net work](@entry_id:195817) done on the material must be non-negative. This imposes strong constraints on the mathematical form of $G(t)$. It can be shown that passivity requires $G(t)$ to be a **completely monotone** function for $t>0$, meaning it is positive, decreasing, convex, and its derivatives alternate in sign indefinitely. This ensures non-negative energy dissipation for any possible loading path [@problem_id:3559386].

#### Nonlinearity and Hysteresis in Soils

While [linear viscoelasticity](@entry_id:181219) provides a framework for damping, the actual dynamic behavior of soil is fundamentally nonlinear. When subjected to [cyclic loading](@entry_id:181502), soils exhibit stress-strain paths that form **[hysteresis](@entry_id:268538) loops**. The area enclosed by a loop, $\Delta W = \oint \tau d\gamma$, represents the energy dissipated per unit volume of material during that cycle. This hysteretic energy dissipation is the primary source of material damping in soils at moderate to large shear strains.

To quantify this damping in a way that is compatible with simpler models, the concept of **equivalent [viscous damping](@entry_id:168972) ratio**, $\xi_{eq}$, is introduced. It is defined as the ratio of the hysteretic energy dissipated in one cycle, $\Delta W$, to the maximum [elastic strain energy](@entry_id:202243) stored during that cycle, $W_{max}$, scaled by a factor of $4\pi$:

$ \xi_{eq} = \frac{\Delta W}{4 \pi W_{max}} $

The maximum stored energy, $W_{max}$, is typically taken as the area of the triangle under the line from the origin to the peak of the stress-strain loop, $W_{max} = \frac{1}{2}\tau_{max}\gamma_{max}$. The [shear modulus](@entry_id:167228) corresponding to this line is the **secant [shear modulus](@entry_id:167228)**, $G_{sec} = \tau_{max}/\gamma_{max}$. Both $G_{sec}$ and $\xi_{eq}$ are not material constants; they are strongly dependent on the cyclic [shear strain](@entry_id:175241) amplitude, $\gamma_{max}$. As strain amplitude increases, $G_{sec}$ typically decreases (modulus reduction), and $\xi_{eq}$ typically increases as the hysteresis loops become wider [@problem_id:3559345].

#### Computational Frameworks: Equivalent-Linear vs. Nonlinear Analysis

Two primary computational frameworks exist to account for this strain-dependent behavior:

1.  **The Equivalent-Linear (EQL) Method:** This is an iterative, approximate method typically performed in the frequency domain. It treats the soil as a linear viscoelastic material, but with properties chosen to be "compatible" with the level of strain induced by the earthquake. The analysis involves an iterative loop: (a) assume initial values for $G$ and $\xi$ for each layer; (b) compute the seismic response for the entire time history; (c) calculate an "effective strain" (often taken as 65% of the peak strain) for each layer; (d) update the values of $G$ and $\xi$ for each layer based on the effective strain using standard modulus reduction and damping curves; (e) repeat until the properties used in the analysis are consistent with those derived from the computed strains. The EQL method's primary limitation is that it uses a single value of modulus and damping for the entire duration of the earthquake, thereby failing to capture the true instantaneous nonlinear response, such as [stiffness degradation](@entry_id:202277) within a single cycle or progressive softening under irregular loading [@problem_id:3559401].

2.  **Nonlinear Time-Domain Analysis:** This is a more rigorous approach that directly integrates the equation of motion step-by-step in the time domain. It employs a nonlinear [constitutive model](@entry_id:747751) that defines the stress-strain relationship at each point in time based on the current state of strain and its history. Instead of using a constant [secant modulus](@entry_id:199454), the model updates the **instantaneous tangent modulus**, $G_t = \partial\tau/\partial\gamma$, at each integration point and time step. Energy dissipation is an intrinsic outcome of the hysteretic stress-strain loops prescribed by the model's loading, unloading, and reloading rules (e.g., Masing-type rules). This method naturally captures the evolution of stiffness and damping throughout the shaking and is considered a more physically faithful representation of soil behavior [@problem_id:3559401].

#### Advanced Topic: Effective Stress Coupling and Pore Pressure Generation

For saturated granular soils like sands and silts, a total [stress analysis](@entry_id:168804) can be insufficient, especially under strong shaking where the generation of excess [pore water pressure](@entry_id:753587) can lead to significant stiffness and strength loss, a phenomenon known as **[soil liquefaction](@entry_id:755029)**. A more advanced **effective stress analysis** is required, which couples the mechanical deformation of the soil skeleton with the flow of pore fluid.

This is typically achieved by solving a coupled system of equations for the solid skeleton displacement $u(z,t)$ and the excess pore pressure $p(z,t)$. The system consists of two primary governing equations [@problem_id:3559347]:

1.  **Momentum Balance for the Mixture:** The equation for the solid skeleton's motion remains similar to the total stress case, but the shear stress is now an effective shear stress, determined by an [effective stress](@entry_id:198048) [constitutive model](@entry_id:747751).
    $ \rho\ddot{u} = \frac{\partial \tau_{xz}}{\partial z} $

2.  **Fluid Mass Conservation:** This equation, derived from [poromechanics](@entry_id:175398) theory, governs the generation and dissipation (diffusion) of [pore pressure](@entry_id:188528).
    $ n\beta_f \dot{p} + \alpha\dot{\varepsilon}_v - \frac{\partial}{\partial z}\left(\frac{k}{\mu}\frac{\partial p}{\partial z}\right) = 0 $

The key to this coupled problem lies in the [feedback mechanisms](@entry_id:269921). Shearing of the soil skeleton causes a tendency for volume change (contractancy or dilatancy), represented by the [volumetric strain rate](@entry_id:272471) term $\dot{\varepsilon}_v$. In contractive soils, this term acts as a source, generating excess pore pressure $p$. According to Terzaghi's **[effective stress principle](@entry_id:171867)**, the effective confining stress on the soil skeleton is reduced as [pore pressure](@entry_id:188528) builds up ($\sigma'_m = \sigma_m - p$). Since the [shear modulus](@entry_id:167228) $G'$ of granular soils is highly dependent on this effective confining stress, an increase in pore pressure leads to a reduction in stiffness ($G' \downarrow$ as $p \uparrow$). This [stiffness degradation](@entry_id:202277), in turn, affects the dynamic response of the soil column, completing the feedback loop. This formulation allows for the explicit simulation of [liquefaction](@entry_id:184829) and its effects on ground motion.

### Boundary Conditions and Seismic Input

The forcing function $\mathbf{F}(t)$ in the [equation of motion](@entry_id:264286) arises from the seismic input applied at the base of the numerical model. The correct definition and application of this input are critical for a physically meaningful analysis.

#### Defining the Input Motion: "Outcrop" versus "Within" Records

Seismic input is typically specified as an acceleration, velocity, or displacement time history. These records can represent two different physical scenarios [@problem_id:3559348]:

-   An **outcrop motion** is the motion that would be recorded at a free surface of the bedrock if the soil column were not present. Due to the free-surface reflection, this motion is approximately twice the amplitude of the underlying incident wave arriving from depth ($v_{out} \approx 2v_{in}$).
-   A **within motion** (or incident motion) represents the upward-propagating wave itself, before it is affected by any free-surface reflections ($v_{within} = v_{in}$). This is a theoretical motion that cannot be directly measured.

The choice of which motion to use, and how to use it, depends on the type of base boundary condition employed in the model.

#### Modeling the Soil-Bedrock Interface

There are two primary methods for applying the seismic input at the base of the discretized soil column, corresponding to different physical idealizations of the underlying half-space [@problem_id:3559369].

1.  **Kinematic Input (Prescribed Motion):** In this approach, the displacement (or velocity/acceleration) of the base nodes is prescribed as a known function of time, $\mathbf{U}_p(t)$. The [equation of motion](@entry_id:264286) is partitioned to solve for the free degrees of freedom $\mathbf{U}_r$ subject to the prescribed base motion. The resulting equation takes the form:
    $ \mathbf{M}_{rr}\ddot{\mathbf{U}}_r + \mathbf{C}_{rr}\dot{\mathbf{U}}_r + \mathbf{K}_{rr}\mathbf{U}_r = \mathbf{F}_r(t) - \mathbf{M}_{rp}\ddot{\mathbf{U}}_p(t) - \mathbf{C}_{rp}\dot{\mathbf{U}}_p(t) - \mathbf{K}_{rp}\mathbf{U}_p(t) $
    The main drawback of this method is that a prescribed motion boundary is **perfectly reflecting**. It does not allow energy from downgoing waves within the soil column to radiate back into the underlying bedrock, which is physically unrealistic. This can trap wave energy in the model and lead to spurious resonances. Furthermore, using an outcrop motion directly as the prescribed input is inconsistent, as it imposes free-surface motion at a non-free interface [@problem_id:3559348].

2.  **Traction Input (Viscous/Absorbing Boundary):** A more physically robust approach is to model the underlying [elastic half-space](@entry_id:194631) as a **viscous nonreflecting boundary**. This boundary applies a traction (force) to the base of the soil column that accounts for both the incident seismic wave and the radiation of energy away from the soil. The traction $\bar{t}(t)$ exerted by the half-space on the soil base is given by:
    $ \bar{t}(t) = -Z_b v_b(t) + 2Z_b v_{in}(t) $
    where $Z_b$ is the impedance of the bedrock, $v_b(t)$ is the velocity at the base of the soil column, and $v_{in}(t)$ is the incident wave velocity. The term $-Z_b v_b(t)$ acts as a dashpot that absorbs energy radiating downward from the soil, preventing spurious reflections. The term $2Z_b v_{in}(t)$ is the driving force from the incident wave. This traction is converted to a nodal force vector $\mathbf{F}(t)$ and applied to the full equation of motion. This boundary condition correctly handles both outcrop motions (by setting $v_{in} = \frac{1}{2}v_{out}$) and within motions (by setting $v_{in} = v_{within}$) [@problem_id:3559348] [@problem_id:3559369].

#### Practical Considerations: Baseline Correction of Input Records

Recorded ground motion accelerograms are not perfect. They often contain low-frequency noise or small offsets that, when integrated, can lead to non-physical, drifting velocity and displacement time histories. A ground motion from a tectonic event should, in the absence of permanent tectonic fling, result in zero final velocity and zero final displacement after the shaking has ceased.

To ensure this physical consistency, a **baseline correction** procedure is a mandatory pre-processing step for any input acceleration record $a_{in}(t)$ used in a time-domain analysis. This procedure modifies the record to enforce two conditions over its duration $T$ [@problem_id:3559370]:

1.  **Zero Final Velocity:** The final velocity $v_{in}(T)$ must be zero. Since $v_{in}(T) = \int_0^T a_{in}(t)dt$ (for zero [initial velocity](@entry_id:171759)), this requires that the integral of the acceleration record is zero.
    $ \int_0^T a_{in}(t) dt \approx 0 $

2.  **Zero Final Displacement:** The final displacement $u_{in}(T)$ must be zero. Since $u_{in}(T) = \int_0^T v_{in}(t)dt$, this requires that the integral of the velocity history (itself obtained by integrating the acceleration) is also zero.
    $ \int_0^T v_{in}(t) dt \approx 0 $

Failure to enforce these conditions will introduce spurious permanent drift into the computed response of the soil column, corrupting the simulation results. Various filtering and [polynomial fitting](@entry_id:178856) techniques are used in practice to perform this essential correction.