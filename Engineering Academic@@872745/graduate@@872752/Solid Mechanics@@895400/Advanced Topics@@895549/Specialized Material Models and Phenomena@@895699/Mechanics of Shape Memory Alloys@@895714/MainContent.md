## Introduction
Shape Memory Alloys (SMAs) are a class of advanced materials renowned for their remarkable properties, including the [shape memory effect](@entry_id:160076) and [superelasticity](@entry_id:159356). These behaviors, which allow SMAs to recover seemingly permanent deformations, have opened doors to innovations in fields from medicine to aerospace. However, harnessing their full potential requires a deep understanding of the complex thermomechanical phenomena that govern their response. This article addresses the need for a rigorous mechanics-based framework to describe, model, and predict the behavior of SMAs under various loading and thermal conditions.

This article is structured to provide a comprehensive graduate-level understanding of SMA mechanics. The journey begins in the "Principles and Mechanisms" chapter, where we will delve into the thermodynamic and crystallographic foundations of the martensitic phase transformation and develop the continuum mechanics framework for [constitutive modeling](@entry_id:183370). Next, the "Applications and Interdisciplinary Connections" chapter will showcase how these fundamental principles are translated into real-world technologies, exploring their use in biomedical devices, robotic actuators, and damping systems. Finally, the "Hands-On Practices" section will offer a series of problems designed to solidify your grasp of key theoretical concepts and their practical application. Through this structured approach, you will gain the knowledge to analyze and engineer systems utilizing these extraordinary smart materials.

## Principles and Mechanisms

The remarkable behaviors of Shape Memory Alloys (SMAs), including the [shape memory effect](@entry_id:160076) and [superelasticity](@entry_id:159356), are rooted in a diffusionless, solid-solid [phase transformation](@entry_id:146960) between a high-symmetry parent phase, **[austenite](@entry_id:161328)**, and a low-symmetry product phase, **martensite**. This chapter elucidates the fundamental principles governing this transformation, from its thermodynamic and crystallographic origins to the [continuum mechanics](@entry_id:155125) frameworks used to model its macroscopic consequences.

### Thermodynamic and Crystallographic Foundations

At its core, the behavior of an SMA is governed by the competition between its [austenite](@entry_id:161328) and [martensite](@entry_id:162117) phases. Understanding this competition requires a synthesis of thermodynamics, which dictates [phase stability](@entry_id:172436), and crystallography, which describes the [kinematics](@entry_id:173318) of the transformation.

#### Phase Stability and Transformation Temperatures

The [austenite](@entry_id:161328) phase, typically possessing a cubic crystal structure (e.g., B2 in NiTi), is thermodynamically stable at high temperatures and low stresses. In contrast, the martensite phase, which has a lower [crystal symmetry](@entry_id:138731) (e.g., monoclinic B19' in NiTi), is stable at low temperatures. The [relative stability](@entry_id:262615) of the phases at a given temperature $T$ and Cauchy stress $\boldsymbol{\sigma}$ is determined by the specific Gibbs free energy, $g(T, \boldsymbol{\sigma})$. The phase with the lower Gibbs energy is the stable one.

The transition between these phases is a **thermoelastic [martensitic transformation](@entry_id:158998)**. In the absence of stress, this transformation is driven by temperature changes. Upon cooling, the high-temperature [austenite](@entry_id:161328) phase does not transform into martensite immediately upon reaching the equilibrium temperature where their free energies are equal. Instead, transformation begins at a lower temperature known as the **[martensite start temperature](@entry_id:194618)**, $M_s$. The transformation progresses as the material is cooled further, completing at the **martensite finish temperature**, $M_f$. Upon subsequent heating from the fully martensitic state, the reverse transformation to [austenite](@entry_id:161328) does not begin until the **austenite start temperature**, $A_s$, is reached, and it completes at the **[austenite](@entry_id:161328) finish temperature**, $A_f$.

This phenomenon, where the transformation on cooling and heating occurs at different temperatures, is known as **[thermal hysteresis](@entry_id:154614)**. The characteristic temperatures typically follow the order $M_f  M_s$ and $A_s  A_f$. Furthermore, due to dissipative effects inherent to the transformation, a hysteresis loop is formed such that $A_s > M_f$ and often $A_f > M_s$. The specific ordering can vary, but a common sequence for SMAs with small [hysteresis](@entry_id:268538) is $M_f  A_s  M_s  A_f$ [@problem_id:2661289].

#### The Clausius-Clapeyron Relation and Latent Heat

The [martensitic transformation](@entry_id:158998) is a **[first-order phase transition](@entry_id:144521)**. This has a crucial thermodynamic consequence: it is accompanied by a discontinuity in first-order derivatives of the free energy, such as entropy and strain. The change in specific entropy, $\Delta s = s_M - s_A$, between the martensite ($s_M$) and austenite ($s_A$) phases is non-zero. This gives rise to a **latent heat** of transformation, $L = T \Delta s$, which is the heat exchanged with the surroundings during the phase change. Since [austenite](@entry_id:161328) is the high-entropy phase ($s_A > s_M$), the forward transformation ($A \to M$) upon cooling is **exothermic** ($\Delta s  0$), releasing heat. Conversely, the reverse transformation ($M \to A$) upon heating is **endothermic** ($-\Delta s > 0$), absorbing heat from the surroundings [@problem_id:2661289].

The interplay between stress, temperature, and [phase stability](@entry_id:172436) is quantitatively described by the **Clausius-Clapeyron relation**. For a uniaxial stress state $\sigma$ coexisting with a transformation strain $\epsilon_L$, the equilibrium condition $g_A(\sigma, T) = g_M(\sigma, T)$ must hold along the transformation line. This implies that any change in Gibbs energy must be equal for both phases, $dg_A = dg_M$. Starting from the differential form $dg = -s dT - \epsilon d\sigma$, we arrive at:
$$
\frac{d\sigma}{dT} = \frac{s_A - s_M}{\epsilon_M - \epsilon_A} = \frac{-\Delta s_{\mathrm{vol}}}{\epsilon_L}
$$
where $\Delta s_{\mathrm{vol}} = s_M - s_A$ is the change in entropy per unit volume, and $\epsilon_L$ is the transformation strain. Since the forward transformation is exothermic ($\Delta s_{\mathrm{vol}}  0$) and produces a positive strain under tension ($\epsilon_L > 0$), the slope $d\sigma/dT$ is positive. This means that a higher stress is required to induce the transformation at a higher temperature.

This relation provides a powerful link between macroscopic mechanical measurements and fundamental thermodynamic properties. For instance, by measuring the slope of the transformation plateau stress with temperature, $d\sigma/dT$, and the transformation strain, $\epsilon_L$, one can estimate the entropy of transformation [@problem_id:2661291].

**Example:** Consider a NiTi alloy with a measured transformation stress sensitivity of $d\sigma/dT = 6\,\mathrm{MPa/K}$ and a recoverable transformation strain of $\epsilon_L = 0.06$. The material density is $\rho = 6450\,\mathrm{kg/m^3}$. The mass-specific entropy change, $\Delta s_{\mathrm{mech}}$, can be estimated from the Clausius-Clapeyron relation, $\Delta s_{\mathrm{mech}} = - \Delta s_{\mathrm{vol}} / \rho = (\epsilon_L / \rho) (d\sigma/dT)$:
$$
\Delta s_{\mathrm{mech}} = \frac{0.06}{6450\,\mathrm{kg/m^3}} \times (6 \times 10^6\,\mathrm{Pa/K}) \approx 55.8\,\mathrm{J/(kg \cdot K)}
$$
This value, derived from [mechanical testing](@entry_id:203797), can be compared to the [entropy change](@entry_id:138294) measured directly via calorimetry, for example, from a measured [latent heat](@entry_id:146032) $\Delta h_{\mathrm{cal}} = 20\,\mathrm{kJ/kg}$ at $T_0 = 330\,\mathrm{K}$, which gives $\Delta s_{\mathrm{cal}} = \Delta h_{\mathrm{cal}}/T_0 \approx 60.6\,\mathrm{J/(kg \cdot K)}$. The close agreement between these values validates the underlying thermodynamic theory [@problem_id:2661291].

#### Crystallographic Kinematics

The [martensitic transformation](@entry_id:158998) is diffusionless and displacive, meaning it occurs through a coordinated shear-like displacement of atoms rather than by atomic migration. The crystallographic relationship between the parent austenite lattice and a single variant of the [martensite](@entry_id:162117) lattice is described by a **lattice correspondence**, which can be represented by a [linear map](@entry_id:201112) or [deformation gradient](@entry_id:163749), $C$. The pure deformation part of this map is given by the [right stretch tensor](@entry_id:193756) $U$ from the polar decomposition $C=RU$, where $R$ is a rotation. This tensor $U$ is known as the **Bain stretch**, and it quantifies the straining of the crystal lattice [@problem_id:2661335].

In general, the Bain stretch $U$ alone cannot transform the [austenite](@entry_id:161328) lattice into the [martensite](@entry_id:162117) lattice while maintaining a coherent, undistorted interface. To achieve this, an additional deformation, known as a **lattice-invariant shear**, is required. In thermoelastic martensites, this shear is typically accomplished by fine-scale **twinning** within the martensite. This twinning process is crucial because it is crystallographically reversible. Under an applied stress or upon heating, the [twin boundaries](@entry_id:160148) can move easily, allowing the deformation to be recovered with minimal energy loss. This reversibility is the microstructural origin of the [shape memory effect](@entry_id:160076) and [superelasticity](@entry_id:159356) [@problem_id:2661289]. The combination of the Bain stretch and the lattice-invariant shear results in a total shape deformation that can leave a specific plane, the **habit plane**, un-distorted and un-rotated on average. The existence of such a plane is a condition for kinematic compatibility at the austenite-martensite interface and is mathematically expressed by the fundamental equation of the crystallographic theory of martensite (developed by Wechsler, Lieberman, and Read, and later by Ball and James):
$$
RU - I = \boldsymbol{a} \otimes \boldsymbol{n}
$$
Here, $I$ is the identity tensor, $R$ is a rotation, $\boldsymbol{a}$ is the shape-change vector, and $\boldsymbol{n}$ is the unit normal to the habit plane. The existence of a solution $(\boldsymbol{a}, \boldsymbol{n}, R)$ for a given Bain stretch $U$ is the condition for a habit plane to form [@problem_id:2661335].

### Continuum Thermodynamics and Constitutive Modeling Framework

To build predictive models of SMA behavior, these physical mechanisms must be translated into the mathematical language of [continuum mechanics](@entry_id:155125). The standard approach utilizes an internal variable framework grounded in thermodynamics.

#### Internal Variables and Kinematics

In a small-strain setting, the state of the material is described not only by the observable strain and temperature but also by a set of **internal variables** that represent the evolution of the [microstructure](@entry_id:148601). For SMAs, the most important internal variables are:
-   The **[martensite](@entry_id:162117) [volume fraction](@entry_id:756566)**, $\xi$, a scalar variable ranging from $\xi=0$ (pure [austenite](@entry_id:161328)) to $\xi=1$ (pure martensite).
-   The **transformation [strain tensor](@entry_id:193332)**, $\boldsymbol{\epsilon}^{tr}$, a symmetric second-order tensor that captures the inelastic strain resulting from the [phase transformation](@entry_id:146960) and the orientation of martensite variants.

The total [infinitesimal strain tensor](@entry_id:167211), $\boldsymbol{\epsilon}$, is assumed to be additively decomposed into an elastic part, $\boldsymbol{\epsilon}^{e}$, and the transformation strain:
$$
\boldsymbol{\epsilon} = \boldsymbol{\epsilon}^{e} + \boldsymbol{\epsilon}^{tr}
$$
If temperature changes are significant, a [thermal strain](@entry_id:187744) term, $\boldsymbol{\epsilon}^{th}$, may also be included. The Cauchy stress, $\boldsymbol{\sigma}$, is then related to the elastic strain through a hyperelastic law, typically a linear Hooke's law: $\boldsymbol{\sigma} = \mathbb{C}:\boldsymbol{\epsilon}^{e} = \mathbb{C}:(\boldsymbol{\epsilon} - \boldsymbol{\epsilon}^{tr})$, where $\mathbb{C}$ is the [fourth-order elasticity tensor](@entry_id:188318) [@problem_id:2661326].

#### The Dissipation Inequality and Thermodynamic Forces

The evolution of the internal variables is not arbitrary; it must obey the [second law of thermodynamics](@entry_id:142732). For an [isothermal process](@entry_id:143096), this is enforced through the **Clausius-Duhem inequality**, which states that the rate of [mechanical dissipation](@entry_id:169843) must be non-negative. This inequality is derived by combining the first and second laws of thermodynamics. Starting from the local [energy balance](@entry_id:150831) and introducing the Helmholtz free energy per unit mass, $\psi = e - Ts$, the reduced [dissipation inequality](@entry_id:188634) (neglecting thermal dissipation) for a continuum with mass density $\rho$ is:
$$
\mathcal{D}_{\text{mech}} = \boldsymbol{\sigma} : \dot{\boldsymbol{\epsilon}} - \rho(\dot{\psi} + s\dot{T}) \ge 0
$$
To make this inequality useful, we express the rate of free energy, $\dot{\psi}$, in terms of the rates of the state variables. Assuming the free energy depends on the [elastic strain](@entry_id:189634) and the internal variables, $\psi(\boldsymbol{\epsilon}^e, \xi, \boldsymbol{\epsilon}^{tr}, T)$, and applying the [chain rule](@entry_id:147422) and the Coleman-Noll procedure, we can identify the non-dissipative [constitutive relations](@entry_id:186508) and a residual inequality for the dissipative processes. The standard procedure yields the elastic law $\boldsymbol{\sigma} = \rho \frac{\partial \psi}{\partial \boldsymbol{\epsilon}^e}$ and reduces the [dissipation inequality](@entry_id:188634) to a [sum of products](@entry_id:165203) of thermodynamic forces and their conjugate rates (fluxes) [@problem_id:2661336].

For a free energy with an additive structure $\psi = \psi_e(\boldsymbol{\epsilon}^e) + \psi_{int}(\xi, \boldsymbol{\epsilon}^{tr})$, the [dissipation inequality](@entry_id:188634) becomes:
$$
\left( \boldsymbol{\sigma} - \rho \frac{\partial \psi_{int}}{\partial \boldsymbol{\epsilon}^{tr}} \right) : \dot{\boldsymbol{\epsilon}}^{tr} + \left( - \rho \frac{\partial \psi_{int}}{\partial \xi} \right) \dot{\xi} \ge 0
$$
This powerful result reveals the **[thermodynamic forces](@entry_id:161907)** that drive the evolution of the internal variables. The force conjugate to the transformation [strain rate](@entry_id:154778) $\dot{\boldsymbol{\epsilon}}^{tr}$ is $X_{tr} = \boldsymbol{\sigma} - \rho \frac{\partial \psi_{int}}{\partial \boldsymbol{\epsilon}^{tr}}$, and the force conjugate to the rate of [martensite](@entry_id:162117) fraction $\dot{\xi}$ is $Y_{\xi} = - \rho \frac{\partial \psi_{int}}{\partial \xi}$. Constitutive models must then specify evolution laws for $\dot{\boldsymbol{\epsilon}}^{tr}$ and $\dot{\xi}$ as functions of these forces, ensuring that their product is always non-negative [@problem_id:2661336].

### Phenomenological Mechanisms and their Mathematical Representation

The abstract thermodynamic framework provides the "grammar" for constructing models, but the specific "vocabulary"—the material's constitutive response—is encoded in the Helmholtz free energy function and the kinetic laws governing the internal variables.

#### The Role of the Free Energy Landscape

The Helmholtz free energy density, $\psi$, can be thought of as an energy landscape over the space of state variables. Its shape dictates the material's [equilibrium states](@entry_id:168134) and the driving forces for transformation. A common and effective approach is to decompose $\psi$ additively into distinct physical contributions [@problem_id:2661292]:
$$
\psi(\boldsymbol{\epsilon}^e, \xi, \boldsymbol{\epsilon}^{tr}, T) = \psi^{e}(\boldsymbol{\epsilon}^e, T) + \psi^{ch}(\xi, T) + \psi^{hd}(\boldsymbol{\epsilon}^{tr}, \xi)
$$
-   **Elastic Energy $\psi^e$**: This term stores the recoverable energy from elastic deformation. It is typically a quadratic function of the [elastic strain](@entry_id:189634), $\psi^e = \frac{1}{2}\boldsymbol{\epsilon}^e : \mathbb{C} : \boldsymbol{\epsilon}^e$. It may also include terms that define the material's [specific heat](@entry_id:136923).
-   **Chemical Energy $\psi^{ch}$**: This part captures the intrinsic free energy difference between the [austenite](@entry_id:161328) and [martensite](@entry_id:162117) phases. It is often modeled as a function that is linear in temperature, such as $\psi^{ch} \propto (T - T_0)\xi$, reflecting the latent heat of transformation.
-   **Hardening Energy $\psi^{hd}$**: This term represents the energy stored in the microstructure due to the transformation itself, such as elastic energy from incompatibilities between variants or energy stored at interfaces. It can also model effects like hardening, where the resistance to further transformation increases as $\xi$ evolves.

For a model to be thermodynamically and mechanically stable, the free energy function must satisfy certain **convexity/concavity conditions**. Mechanical stability requires that $\psi$ be a convex function of its mechanical state variables (e.g., $\boldsymbol{\epsilon}^e$, $\boldsymbol{\epsilon}^{tr}$, $\xi$) at a fixed temperature. This ensures that an [equilibrium state](@entry_id:270364) corresponds to a unique minimum energy state. Thermal stability requires that $\psi$ be a [concave function](@entry_id:144403) of temperature, which is equivalent to having a non-negative specific heat. These conditions place mathematical constraints on the functional forms and parameters used in the model. For instance, in $\psi^e$, the [elasticity tensor](@entry_id:170728) $\mathbb{C}$ must be [positive definite](@entry_id:149459). If the hardening energy includes a coupling between $\boldsymbol{\epsilon}^{tr}$ and $\xi$, such as $\psi^{hd} = \frac{1}{2}H_{tr}(\boldsymbol{\epsilon}^{tr}:\boldsymbol{\epsilon}^{tr}) + \frac{1}{2}h\xi^2 - b\xi(\mathbf{E}_0:\boldsymbol{\epsilon}^{tr})$, joint [convexity](@entry_id:138568) requires not only $H_{tr}0$ and $h \ge 0$, but also a condition on the coupling term, $b^2 \le H_{tr}h$, which can be derived from the Schur complement of the Hessian matrix [@problem_id:2661292].

#### Origin of the Superelastic Stress Plateau

One of the most defining features of [superelasticity](@entry_id:159356) is the long, flat stress plateau observed during loading and unloading. This behavior can be elegantly explained as a direct consequence of a **nonconvex energy landscape**. If we consider a simplified energy density $\psi(\epsilon)$ as a function of total strain, it can be visualized as a "two-well" potential: one well corresponding to the austenite phase and a second, lower-energy well (at high strain) corresponding to the martensite phase. A material body under a prescribed average strain $\bar{\epsilon}$ will arrange its internal state to minimize its total free energy.

Instead of adopting a uniform strain $\bar{\epsilon}$ that falls in the high-energy "hump" between the two wells, the material can achieve a much lower energy state by forming a fine mixture of the two phases. One part of the material remains [austenite](@entry_id:161328) at a lower strain $\epsilon_A$, while the other part transforms to [martensite](@entry_id:162117) at a higher strain $\epsilon_M$. These two strains correspond to the points of tangency of a line that is tangent to both energy wells. This construction is known as the **[common tangent construction](@entry_id:138004)**, and it defines the convex envelope of the nonconvex energy function.

The slope of this common tangent is the equilibrium stress, $\sigma_p$, at which the two phases coexist. As the macroscopic strain $\bar{\epsilon}$ is increased, the volume fraction of the [martensite](@entry_id:162117) phase simply increases according to a lever rule, while the stress remains constant at the plateau value $\sigma_p$. For a simple model with two quadratic energy wells of equal stiffness $E$, $\psi_A = \frac{1}{2}E\epsilon^2$ and $\psi_M = \frac{1}{2}E(\epsilon - \epsilon_L)^2 + \Delta g$, the equilibrium plateau stress is found to be [@problem_id:2661309]:
$$
\sigma_p = \frac{\Delta g}{\epsilon_L}
$$
This shows that the plateau stress is directly proportional to the chemical energy barrier $\Delta g$ and inversely proportional to the transformation strain $\epsilon_L$.

#### Transformation Kinetics and Hysteresis

The stress plateau described by the [common tangent construction](@entry_id:138004) represents a perfectly reversible process without [hysteresis](@entry_id:268538). Real SMAs, however, exhibit significant hysteresis. This dissipative behavior is captured through kinetic laws that govern the evolution of the internal variables.

A **transformation surface** is defined in stress-temperature space as a function $f(\boldsymbol{\sigma}, T, \dots) = 0$ that signals the onset of transformation. The simplest criterion is based on a **Schmid-type driving force**, which assumes transformation is driven by the work of the stress projected onto the transformation strain direction, $Y = \boldsymbol{\sigma}:\Delta\boldsymbol{\epsilon}^{tr}$. However, experiments show that many SMAs exhibit **[tension-compression asymmetry](@entry_id:201728)**, where the stress required for transformation in tension is different from that in compression. This is a non-Schmid effect, often attributed to the influence of hydrostatic stress or other stress components. To model this, the transformation surface can be modified with terms that are [odd functions](@entry_id:173259) of the stress. A common approach is to add a pressure-dependent term [@problem_id:2661274]:
$$
f(\boldsymbol{\sigma}, T) = |\boldsymbol{\sigma}:\Delta\boldsymbol{\epsilon}^{tr}| + \beta \, \text{tr}(\boldsymbol{\sigma}) - Y_c(T) = 0
$$
where $\beta$ is a material parameter capturing the pressure sensitivity and $Y_c(T)$ is the critical driving force.

The hysteresis loop itself arises from energy dissipation during the transformation. This dissipation is fundamentally **rate-independent**, meaning the area of the quasi-static stress-strain loop does not vanish as the loading rate approaches zero. This distinguishes it starkly from viscoelastic hysteresis, which is rate-dependent. This rate-independent dissipation can be modeled by postulating a **dissipation potential**, $\Phi(\dot{\xi})$, which is a convex, non-[smooth function](@entry_id:158037) of the rate of the internal variable. This leads to a threshold-based evolution law, often expressed via Kuhn-Tucker conditions, where transformation only occurs when the driving force reaches a critical dissipative threshold. This mechanism naturally introduces [path dependence](@entry_id:138606) (different behavior for loading vs. unloading) and a persistent [hysteresis loop](@entry_id:160173) [@problem_id:2661342]. Additional contributions to hysteresis come from energetic barriers, such as the energy required to create and move interfaces, which can be modeled by including gradients of the internal variables (e.g., $\nabla\xi$) in the free energy [@problem_id:2661342].

### From Single Crystal to Polycrystal: Homogenization

The [constitutive models](@entry_id:174726) described above are often formulated for a single crystal. However, engineering components are typically **polycrystalline**, consisting of a vast number of randomly oriented grains. Predicting the aggregate response requires a **[homogenization](@entry_id:153176)** scheme to average the behavior of the constituent grains.

The simplest homogenization models are the **Voigt** and **Reuss** estimates. The Voigt model assumes a uniform strain field throughout the polycrystal (iso-strain), leading to an effective modulus that is the volume-weighted arithmetic mean of the phase moduli:
$$
E_{\mathrm{V}} = (1-\xi)E_{\mathrm{A}} + \xi E_{\mathrm{M}}
$$
The Reuss model assumes a uniform stress field (iso-stress), leading to an effective compliance that is the [arithmetic mean](@entry_id:165355) of the phase compliances, or an effective modulus that is the harmonic mean:
$$
E_{\mathrm{R}} = \left( \frac{1-\xi}{E_{\mathrm{A}}} + \frac{\xi}{E_{\mathrm{M}}} \right)^{-1}
$$
For a fixed [microstructure](@entry_id:148601) (i.e., constant $\xi$), the Voigt and Reuss estimates provide rigorous [upper and lower bounds](@entry_id:273322), respectively, for the effective *elastic* modulus of the composite. More sophisticated methods, like the **self-consistent scheme**, treat each grain as an inclusion in an effective medium and typically yield estimates that lie between the Voigt and Reuss bounds [@problem_id:2661325].

It is crucial to distinguish between the **[effective elastic modulus](@entry_id:181086)** and the **[algorithmic tangent modulus](@entry_id:199979)**. The former describes the purely elastic response of the aggregate at a fixed phase fraction $\xi$. The latter describes the overall slope of the macroscopic stress-strain curve, which includes the effects of ongoing phase transformation ($\dot{\xi} \neq 0$). During the superelastic plateau, the [algorithmic tangent](@entry_id:165770) can be very small (close to zero), and is generally much lower than the elastic Reuss bound, reflecting the profound softening effect of the transformation [@problem_id:2661325]. Therefore, while [homogenization](@entry_id:153176) schemes are essential for estimating the elastic properties of the mixed-phase material, they must be embedded within a larger constitutive framework that correctly captures the dissipative evolution of the phase fraction to predict the full thermomechanical response.