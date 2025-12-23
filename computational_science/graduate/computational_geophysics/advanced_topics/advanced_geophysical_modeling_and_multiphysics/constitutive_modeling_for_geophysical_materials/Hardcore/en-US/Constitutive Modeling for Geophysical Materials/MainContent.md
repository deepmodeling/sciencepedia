## Introduction
Constitutive modeling forms the bedrock of modern [computational geophysics](@entry_id:747618), providing the essential mathematical language to describe how Earth's materials—from surface soils to the deep mantle—deform under force. The ability to predict this mechanical response is critical for tackling some of the most pressing challenges in the Earth sciences, including earthquake hazard assessment, resource extraction, and modeling climate-driven changes in glaciers and permafrost. However, the immense diversity of [geophysical materials](@entry_id:749868) and the extreme range of conditions they experience present a significant challenge, necessitating a sophisticated and structured theoretical framework.

This article provides a comprehensive guide to the [constitutive models](@entry_id:174726) that are fundamental to the field. It is designed to build your understanding from the ground up, navigating from foundational concepts to advanced applications. First, in **"Principles and Mechanisms,"** we will dissect the core theories of elasticity, viscosity, plasticity, and [poromechanics](@entry_id:175398), establishing the physical and mathematical basis for each class of model. Next, **"Applications and Interdisciplinary Connections"** will demonstrate how these models are deployed to solve real-world problems in [geomechanics](@entry_id:175967), solid Earth [geophysics](@entry_id:147342), and cryospheric science. Finally, **"Hands-On Practices"** offers the opportunity to translate theory into practice by implementing key algorithms for modeling deformation and failure. We begin by exploring the fundamental principles that govern material response.

## Principles and Mechanisms

The mechanical behavior of [geophysical materials](@entry_id:749868)—from crustal rocks and soils to mantle silicates and polar ice—is extraordinarily diverse. Constitutive models provide the mathematical framework for describing this behavior, linking the forces applied to a material (stress) to the resulting deformation (strain) and its rate of change. This chapter delves into the core principles and mechanisms that underpin the most important classes of [constitutive models](@entry_id:174726) used in [computational geophysics](@entry_id:747618), progressing from simple idealizations to complex, coupled descriptions of material response.

### Elasticity: The Reversible Response

The simplest idealization of a solid is that of an elastic material, where deformation is instantaneous, reversible, and all work done on the material is stored as potential energy. Upon removal of the applied loads, the material returns to its original shape, and the stored energy is fully recovered.

#### Anisotropic Linear Elasticity and Transverse Isotropy

While simple [isotropic elasticity](@entry_id:203237) is a useful starting point, many [geophysical materials](@entry_id:749868) exhibit directional dependence in their stiffness due to their underlying microstructure. Sedimentary rocks like shale, metamorphic rocks with strong [foliation](@entry_id:160209), and even ice single crystals possess inherent anisotropy. A common and important form of [anisotropy in geophysics](@entry_id:746464) is **[transverse isotropy](@entry_id:756140) (TI)**, which describes a material with a single plane of isotropy and an axis of rotational symmetry perpendicular to it. For example, a shale formation often exhibits this property, where the bedding planes form the plane of [isotropy](@entry_id:159159), and the material response is different for loading parallel versus perpendicular to these planes .

For a general linear elastic material, the relationship between the stress tensor $\sigma_{ij}$ and the strain tensor $\varepsilon_{kl}$ is given by the generalized Hooke's Law:
$$
\sigma_{ij} = C_{ijkl} \varepsilon_{kl}
$$
where $C_{ijkl}$ is the fourth-order stiffness tensor, containing up to 21 [independent elastic constants](@entry_id:203649) for the most general anisotropic case. The high number of components makes working with the tensor form cumbersome. For practical applications, we often employ **Voigt notation**, which represents the symmetric second-order stress and strain tensors as six-component vectors and the fourth-order stiffness tensor as a $6 \times 6$ [symmetric matrix](@entry_id:143130), $C_{\alpha\beta}$. The standard mapping is $11 \to 1$, $22 \to 2$, $33 \to 3$, $23 \to 4$, $13 \to 5$, and $12 \to 6$.

For a transversely isotropic material with its symmetry axis aligned with the $x_3$ direction (normal to bedding), the symmetry constraints reduce the number of [independent elastic constants](@entry_id:203649) from 21 to just five. The [stiffness matrix](@entry_id:178659) $C_{\alpha\beta}$ takes the following form :
$$
C_{\text{TI}} = \begin{pmatrix}
C_{11} & C_{12} & C_{13} & 0 & 0 & 0 \\
C_{12} & C_{11} & C_{13} & 0 & 0 & 0 \\
C_{13} & C_{13} & C_{33} & 0 & 0 & 0 \\
0 & 0 & 0 & C_{44} & 0 & 0 \\
0 & 0 & 0 & 0 & C_{44} & 0 \\
0 & 0 & 0 & 0 & 0 & C_{66}
\end{pmatrix}
$$
The five independent constants are typically chosen as ($C_{11}, C_{33}, C_{44}, C_{66}, C_{13}$). Their physical interpretations are crucial for understanding the material's behavior:
*   $C_{11}$: Axial stiffness within the plane of [isotropy](@entry_id:159159) (e.g., stiffness parallel to the shale bedding).
*   $C_{33}$: Axial stiffness along the [axis of symmetry](@entry_id:177299) (e.g., stiffness perpendicular to the shale bedding).
*   $C_{44}$: Shear modulus for planes containing the symmetry axis (e.g., shear on a vertical plane).
*   $C_{66}$: Shear modulus for planes within the plane of isotropy (e.g., shear on the horizontal bedding plane).
*   $C_{13}$: A [coupling coefficient](@entry_id:273384) that relates axial stress in the plane of [isotropy](@entry_id:159159) to [axial strain](@entry_id:160811) along the symmetry axis, and vice versa.

The remaining non-zero components are related to these five through the symmetry conditions: $C_{22}=C_{11}$, $C_{23}=C_{13}$, $C_{55}=C_{44}$, and $C_{12} = C_{11} - 2C_{66}$. This last relation is a direct consequence of the [rotational invariance](@entry_id:137644) in the isotropic plane.

### Viscoelasticity: The Time-Dependent Response

Geophysical materials rarely respond instantaneously. When subjected to a load, they often exhibit a [time-dependent deformation](@entry_id:755974) that combines elastic (spring-like) and viscous (fluid-like) characteristics. This behavior is known as **viscoelasticity**. On geological timescales, rocks in the asthenosphere and mantle flow, but on short timescales (e.g., [seismic waves](@entry_id:164985)), they behave elastically. Viscoelastic models bridge this gap.

A powerful way to conceptualize and model linear viscoelastic behavior is through mechanical analogs composed of springs (representing elastic elements) and dashpots (representing viscous elements). The **Generalized Maxwell Model** provides a versatile framework for capturing a wide spectrum of relaxation behaviors. It consists of a purely elastic spring in parallel with a series of $N$ Maxwell branches. Each Maxwell branch is a spring (modulus $G_i$) and a dashpot (viscosity $\eta_i$) connected in series .

In a shear deformation experiment, the material's response is characterized by the shear [relaxation modulus](@entry_id:189592), $G(t)$, which is the [stress response](@entry_id:168351) to a unit step strain applied at $t=0$. For the Generalized Maxwell model, the total stress is the sum of the stress in the parallel equilibrium spring ($G_\infty$) and the stresses in each of the $N$ Maxwell branches. By solving the differential equation for a single Maxwell branch, one can show that its stress relaxes exponentially over time. The sum of these responses yields the total [relaxation modulus](@entry_id:189592), often expressed as a **Prony series**:
$$
G(t) = G_\infty + \sum_{i=1}^{N} G_i \exp\left(-\frac{t}{\tau_i}\right) \quad \text{for } t \ge 0
$$
Here, $\tau_i = \eta_i / G_i$ is the **relaxation time** of the $i$-th branch, representing the characteristic timescale over which stress in that branch dissipates. The term $G_\infty$ is the equilibrium modulus, representing the solid-like elastic stiffness at infinite time. For the model to be thermodynamically admissible (i.e., for dissipation to always be non-negative), the physical parameters must be non-negative: $G_\infty \ge 0$, $G_i \ge 0$, and $\eta_i > 0$. This ensures that $G(t)$ is a positive, monotonically decreasing function, reflecting that the material cannot spontaneously generate stress.

### Viscosity and Creep: The Irreversible Flow

For processes occurring over very long timescales, such as [mantle convection](@entry_id:203493), glacier flow, or post-seismic relaxation, the elastic component of deformation can be negligible compared to the permanent, irreversible flow. This purely viscous behavior is known as **creep**. Unlike the linear viscosity of simple fluids, the creep of [geophysical materials](@entry_id:749868) is typically highly non-linear.

The relationship between [stress and strain rate](@entry_id:263123) is often expressed using invariants of the [deviatoric stress tensor](@entry_id:267642), $s_{ij}$, and the [strain-rate tensor](@entry_id:266108), $\dot{\epsilon}_{ij}$. The effective stress $\tau_e$ and effective strain rate $\dot{\epsilon}_e$ are defined as:
$$
\tau_e = \left(\frac{1}{2} s_{ij} s_{ij}\right)^{1/2} \quad \text{and} \quad \dot{\epsilon}_e = \left(\frac{1}{2} \dot{\epsilon}_{ij} \dot{\epsilon}_{ij}\right)^{1/2}
$$
A key concept is the **effective viscosity**, $\eta_{\mathrm{eff}}$, defined by the scalar relation $\tau_e = 2 \eta_{\mathrm{eff}} \dot{\epsilon}_e$. For many [geophysical materials](@entry_id:749868), $\eta_{\mathrm{eff}}$ is not constant but depends strongly on stress, temperature, and [microstructure](@entry_id:148601) .

A widely used model for the flow of ice in glaciers and ice sheets is **Glen's flow law**, a [power-law creep](@entry_id:198473) model with an Arrhenius temperature dependence:
$$
\dot{\epsilon}_e = A \tau_e^n \exp\left(-\frac{Q}{RT}\right)
$$
Here, $A$ is a material parameter, $n$ is the [stress exponent](@entry_id:183429) (typically around 3 for ice), $Q$ is the activation energy for creep, $R$ is the [universal gas constant](@entry_id:136843), and $T$ is the [absolute temperature](@entry_id:144687). The corresponding effective viscosity for ice is:
$$
\eta_{\mathrm{eff}}(\tau_e, T) = \frac{\tau_e}{2 \dot{\epsilon}_e} = \frac{1}{2} A^{-1} \tau_e^{1-n} \exp\left(\frac{Q}{RT}\right)
$$
Since $n > 1$, the viscosity is a decreasing function of stress, a behavior known as **shear-thinning**.

For polycrystalline rocks in the lithosphere and mantle, creep often occurs through multiple, competing mechanisms. A common model combines **diffusion creep** (dominant at low stress) and **[dislocation creep](@entry_id:159638)** (dominant at high stress). Since these are parallel mechanisms accommodating the same macroscopic deformation, their strain rates add: $\dot{\epsilon}_e = \dot{\epsilon}_{\text{diff}} + \dot{\epsilon}_{\text{disl}}$.
*   **Diffusion creep** is linear in stress ($n=1$) and sensitive to [grain size](@entry_id:161460) $d$ (typically $\dot{\epsilon}_{\text{diff}} \propto d^{-m}$ with $m>0$).
*   **Dislocation creep** is a power-law in stress with $n > 1$ and is largely independent of [grain size](@entry_id:161460).

The composite [effective viscosity](@entry_id:204056) is then given by :
$$
\eta_{\mathrm{eff}} = \frac{\tau_e}{2(\dot{\epsilon}_{\text{diff}} + \dot{\epsilon}_{\text{disl}})}
$$
In the low-stress, diffusion-dominated regime, this viscosity becomes independent of stress (Newtonian), whereas in the high-stress, dislocation-dominated regime, it becomes shear-thinning, with $\eta_{\mathrm{eff}} \propto \tau_e^{1-n}$.

### Plasticity: Rate-Independent Irreversible Deformation

Plasticity theory describes materials that deform elastically up to a certain stress level, beyond which they undergo permanent, irreversible deformation. Unlike viscosity, classical plasticity is rate-independent, meaning the response does not depend on how quickly the loads are applied. The theory is built on three key components: a **yield criterion** defining the limit of elastic behavior, a **[flow rule](@entry_id:177163)** describing the direction of plastic strain, and a **[hardening law](@entry_id:750150)** describing how the yield criterion evolves with plastic deformation.

#### Frictional Materials: Pressure-Dependent Yielding

For many crustal rocks, soils, and [granular materials](@entry_id:750005), the shear strength is not a fixed value but depends on the confining pressure. The **Mohr-Coulomb criterion** is a classic model that captures this pressure-dependent, frictional behavior. It postulates that failure occurs on a plane within the material when the shear stress $\tau$ on that plane reaches a critical value determined by the normal stress $\sigma_n$ on that same plane, as well as the material's intrinsic **cohesion** $c$ and **internal friction angle** $\phi$:
$$
|\tau| = c + \sigma_n \tan\phi
$$
(Here, compression is taken as positive). Using the Mohr circle construction, this can be expressed in terms of the maximum and minimum principal stresses, $\sigma_1$ and $\sigma_3$. For a material at the point of yielding, the relationship is :
$$
\sigma_1 = \sigma_3 N_\phi + 2c \sqrt{N_\phi} \quad \text{where} \quad N_\phi = \frac{1+\sin\phi}{1-\sin\phi}
$$
For computational modeling, it is often more convenient to express [yield criteria](@entry_id:178101) in terms of [stress invariants](@entry_id:170526). The most common are the mean stress $p$ and the equivalent shear stress (or deviatoric stress invariant) $q$. The Mohr-Coulomb criterion can be mapped into this $(p, q)$ space. For the important case of triaxial compression, this mapping yields a straight line:
$$
q = \left(\frac{6\sin\phi}{3 - \sin\phi}\right)p + \left(\frac{6c\cos\phi}{3 - \sin\phi}\right)
$$
The Mohr-Coulomb [yield surface](@entry_id:175331) in full 3D invariant space is an irregular hexagonal pyramid. This geometric complexity, with its sharp corners, can pose numerical challenges. A common simplification is to use the smooth, conical **Drucker-Prager criterion**, $F = q - \alpha p - k = 0$. The parameters $\alpha$ and $k$ can be calibrated to match the Mohr-Coulomb criterion along a specific stress path, such as triaxial compression, by equating the coefficients of the linear $q-p$ relations .

#### Frictional Sliding: Rate-and-State Friction

On a pre-existing fault surface, friction is not a simple constant but evolves with slip velocity and the history of contact. **Rate-and-state [friction laws](@entry_id:749597)**, developed from laboratory experiments, provide a powerful framework for modeling this evolution and are central to modern [earthquake physics](@entry_id:748780).

The friction coefficient $\mu$ is expressed as a function of the instantaneous slip rate $V$ and one or more [state variables](@entry_id:138790) $\theta$ that represent the evolving properties of the [asperity](@entry_id:197484) contacts on the fault surface . A common form is:
$$
\mu(V, \theta) = \mu_0 + a \ln\left(\frac{V}{V_0}\right) + b \ln\left(\frac{\theta V_0}{D_c}\right)
$$
Here, $\mu_0$ is a reference friction at a reference velocity $V_0$, $a$ and $b$ are dimensionless empirical parameters, and $D_c$ is a characteristic slip distance over which the state evolves. The first logarithmic term is the **direct effect**, causing an instantaneous jump in friction with a change in velocity. The second term is the **evolution effect**.

The state variable $\theta$, which can be interpreted as the average age of the [asperity](@entry_id:197484) contacts, evolves over time. A common evolution law, known as the **aging law** (or Dieterich law), is:
$$
\frac{d\theta}{dt} = 1 - \frac{V\theta}{D_c}
$$
This law implies that contacts strengthen (age) with time when the fault is stationary ($V=0$) and weaken (rejuvenate) with slip.

A critical property of a fault is its steady-state behavior. By setting $\dot{\theta}=0$, we find the steady-state value of the state variable, $\theta_{ss} = D_c/V$. Substituting this into the friction law gives the steady-state friction coefficient $\mu_{ss}(V)$:
$$
\mu_{ss}(V) = \mu_0 + (a-b) \ln\left(\frac{V}{V_0}\right)
$$
The sign of the parameter combination $(a-b)$ determines the stability of sliding. If $(a-b) > 0$, friction increases with slip velocity, leading to stable, [aseismic creep](@entry_id:746526) (**velocity-strengthening**). If $(a-b)  0$, friction decreases with increasing slip velocity, promoting unstable, [stick-slip behavior](@entry_id:755445) and potentially generating earthquakes (**velocity-weakening**) .

### Poromechanics: The Role of Pore Fluids

The presence of fluids within the pore space of rocks and soils profoundly influences their mechanical behavior. Poromechanics is the coupled theory that describes the interaction between the deforming solid skeleton and the pore fluid.

#### The Principle of Effective Stress

The foundational concept of [poromechanics](@entry_id:175398) is the **[principle of effective stress](@entry_id:197987)**. It states that the deformation of the solid skeleton is controlled not by the total stress applied to the material, but by an effective stress, which is the portion of the total stress borne by the solid framework. The simplest form was proposed by Karl Terzaghi for soils, where the [effective stress](@entry_id:198048) tensor $\sigma'$ is related to the total Cauchy stress tensor $\sigma$ and the pore fluid pressure $p$ by $\sigma' = \sigma - pI$, where $I$ is the identity tensor.

This principle was generalized by Maurice Biot for porous rocks where the solid grains themselves are compressible. **Biot's [effective stress principle](@entry_id:171867)** takes the form :
$$
\sigma' = \sigma - \alpha p I
$$
The dimensionless **Biot-Willis coefficient**, $\alpha$, accounts for the [compressibility](@entry_id:144559) of the solid grains relative to the porous skeleton. It is defined as:
$$
\alpha = 1 - \frac{K_d}{K_s}
$$
where $K_d$ is the [bulk modulus](@entry_id:160069) of the drained porous frame and $K_s$ is the intrinsic [bulk modulus](@entry_id:160069) of the solid grains. Since the frame cannot be stiffer than the material it's made from ($K_d \le K_s$), the coefficient $\alpha$ ranges from a value less than 1 (for compressible grains) to 1 (for incompressible grains, $K_s \to \infty$), at which point Biot's law recovers Terzaghi's principle. This coefficient is sometimes also denoted by $b$.

#### Critical State Soil Mechanics

**Critical State Soil Mechanics (CSSM)** provides a comprehensive framework for modeling saturated clays and silts, elegantly unifying their consolidation (compaction) and shear behavior. It combines the [effective stress principle](@entry_id:171867) with concepts of plasticity.

A central tenet is the **critical state concept**: when a soil is sheared continuously, it will eventually evolve towards a "[critical state](@entry_id:160700)" where it deforms at constant volume and constant stress, regardless of its initial density . In the space of effective [stress invariants](@entry_id:170526) ($p', q$), this state corresponds to a line known as the **Critical State Line (CSL)**, defined by $q = M p'$, where $M$ is a material constant.

The **Modified Cam-Clay (MCC) model** is a canonical elastoplastic model built upon this concept. It features a cap-shaped, elliptical yield surface in the $(p', q)$ plane that describes the boundary of the elastic domain. The equation of the [yield surface](@entry_id:175331) is:
$$
f(p', q, p_c') = q^2 + M^2 p'(p' - p_c') = 0
$$
This ellipse passes through the origin, has its apex on the CSL, and intersects the $p'$-axis at the **[preconsolidation pressure](@entry_id:203717)**, $p_c'$. The [preconsolidation pressure](@entry_id:203717) acts as a **hardening parameter**, representing the largest effective mean stress the soil has ever experienced. As the soil undergoes plastic volumetric compaction, $p_c'$ increases, causing the yield surface to expand. This process is known as **hardening**.

The [hardening law](@entry_id:750150) relates the change in $p_c'$ to the increment of plastic volumetric strain, $d\epsilon_v^p$. It is derived from the experimentally observed linear relationship between void ratio and the logarithm of effective pressure during virgin compression and unloading. The resulting law is :
$$
dp_c' = \frac{(1+e) p_c'}{\lambda - \kappa} d\epsilon_v^p
$$
where $\lambda$ is the slope of the virgin compression line and $\kappa$ is the slope of the unloading-reloading (swelling) line in the $e-\ln p'$ plane. In many standard formulations, this is simplified to $\frac{dp_c'}{d\epsilon_v^p} = \frac{p_c'}{\lambda - \kappa}$.

### Advanced Frameworks for Complex Behaviors

To model the full complexity of geophysical processes, which can involve simultaneous elastic deformation, plastic flow, damage, and fluid interaction under large deformations, more general and rigorous theoretical frameworks are required.

#### Thermodynamic Consistency: The Clausius-Duhem Inequality

A fundamental requirement for any physically realistic [constitutive model](@entry_id:747751) is that it must be consistent with the laws of thermodynamics, particularly the second law, which states that entropy (or dissipation) in an isolated system can only increase. For isothermal processes, this is typically enforced through the **Clausius-Duhem inequality**. In a mechanical context, it can be stated as: the [mechanical power](@entry_id:163535) supplied to the material must be greater than or equal to the rate of increase of its stored (free) energy. The difference is the **dissipation**, which must be non-negative.

A powerful method for developing thermodynamically consistent models is to postulate a **Helmholtz free energy** density function, $\psi$, which depends on the observable [state variables](@entry_id:138790) (like [elastic strain](@entry_id:189634) $\boldsymbol{\epsilon}^e$) and a set of internal variables, $\boldsymbol{q}$, that describe the material's [microstructure](@entry_id:148601) (e.g., plastic strain, damage, hardening parameters) . The inequality then takes the form:
$$
\mathcal{D} = \boldsymbol{\sigma} : \dot{\boldsymbol{\epsilon}} - \dot{\psi} \ge 0
$$
For an elasto-plastic-damage porous material, a consistent free energy function can be constructed by additively combining terms representing different storage mechanisms:
$$
\psi(\boldsymbol{\epsilon}^e, d, \kappa, \zeta) = \psi_{el,d}(\boldsymbol{\epsilon}^e, d) + \psi_{hard}(\kappa) + \psi_{poro}(\boldsymbol{\epsilon}^e, \zeta)
$$
A typical form might be :
$$
\psi = \frac{1}{2} (1-d)^2 \boldsymbol{\epsilon}^e : \mathbf{C} : \boldsymbol{\epsilon}^e + h(\kappa) + \frac{1}{2} M \left( \zeta - \alpha \operatorname{tr}\boldsymbol{\epsilon}^e \right)^2
$$
Here, $(1-d)^2$ is a damage degradation function that reduces stiffness, $h(\kappa)$ is a convex hardening function, and the last term captures the Biot-type poromechanical energy storage. This approach automatically provides consistent definitions for stress and other thermodynamic forces, and ensures that the evolution laws for the internal variables lead to positive dissipation.

#### Finite Deformations and Objectivity

Many geophysical processes, such as [mantle convection](@entry_id:203493), folding of rock layers, or flow in a fault gouge, involve deformations that are too large to be described by the small-strain theories discussed so far. Modeling finite deformations requires a more complex kinematic framework.

The deformation is described by the **deformation gradient** tensor, $F = \partial\boldsymbol{x}/\partial\boldsymbol{X}$. A cornerstone of modern [finite-strain plasticity](@entry_id:185352) theory is the **[multiplicative decomposition](@entry_id:199514)** of $F$ into an elastic part, $F_e$, and a plastic part, $F_p$ :
$$
F = F_e F_p
$$
This decomposition is conceptually imagined as a two-step process: first, an irreversible plastic rearrangement of the material into a stress-free intermediate configuration ($F_p$); followed by a reversible elastic deformation from this intermediate configuration to the final, stressed configuration ($F_e$). The Cauchy stress is then determined by the elastic part, $F_e$, via a hyperelastic law. For porous [geomaterials](@entry_id:749838), an important distinction from metals is that plastic deformation can involve volume change due to pore collapse ([compaction](@entry_id:267261)) or opening ([dilatancy](@entry_id:201001)). This means that, unlike in [metal plasticity](@entry_id:176585), the determinant of the [plastic deformation gradient](@entry_id:188153), $J_p = \det(F_p)$, is generally not equal to 1 .

When materials undergo [large rotations](@entry_id:751151) in addition to deformation (e.g., tectonic block rotation), a further challenge arises. A constitutive law must not predict stress changes due to a simple [rigid-body rotation](@entry_id:268623) of the material and the observer. This principle is known as **Material Frame Indifference (MFI)** or objectivity. The standard [material time derivative](@entry_id:190892) of the Cauchy stress, $\dot{\boldsymbol{\sigma}}$, is *not* objective; it changes under a rigid rotation. To formulate a valid hypoelastic law ($\dot{\boldsymbol{\sigma}}$ related to the rate of deformation $D$), one must use an **[objective stress rate](@entry_id:168809)**, which is constructed to be invariant to superposed rotations.

Several such rates have been proposed, including :
*   The **Jaumann rate**, $\overset{\nabla}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma}W - W\boldsymbol{\sigma}$, which uses the [spin tensor](@entry_id:187346) $W = \text{skew}(L)$ to define a [corotational frame](@entry_id:747893).
*   The **Green-Naghdi rate**, $\overset{\circ}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma}\Omega - \Omega\boldsymbol{\sigma}$, which uses the material rotation rate $\Omega = \dot{R}R^T$ from the [polar decomposition](@entry_id:149541) $F=RU$.
*   The **Truesdell rate**, $\stackrel{\triangle}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - L\boldsymbol{\sigma} - \boldsymbol{\sigma}L^T + \text{tr}(D)\boldsymbol{\sigma}$, which is a form of convected derivative.

Each of these rates is objective and ensures that in a [hypoelastic model](@entry_id:750490), a pure [rigid motion](@entry_id:155339) ($D=0$) does not generate spurious stresses. The choice among them can affect the predicted response in simulations involving large shear strains and rotations, and it remains a topic of advanced research in continuum mechanics.