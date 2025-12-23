## Introduction
The dynamic interplay between flowing blood and the compliant walls of blood vessels is a cornerstone of cardiovascular function. This complex [fluid-structure interaction](@entry_id:171183) (FSI) governs everything from the propagation of the pulse wave to the regulation of local blood flow. However, disruptions in these mechanics are also central to the development and progression of devastating cardiovascular diseases, including aneurysms, [atherosclerosis](@entry_id:154257), and hypertension. Understanding, predicting, and ultimately intervening in these conditions requires a rigorous framework that can bridge the gap between fluid dynamics and solid mechanics.

This article provides a comprehensive exploration of FSI in the vasculature, designed to equip you with the fundamental knowledge to model and analyze these intricate systems. We will delve into the core principles, mathematical formalisms, and physical phenomena that define [vascular mechanics](@entry_id:1133731). You will learn how disparate mathematical descriptions for fluids and solids are coupled to create a unified model, how the unique material properties of blood and arterial tissue are represented, and how these models are applied to pressing clinical and biological questions.

Across the following chapters, we will first establish the theoretical foundation in "Principles and Mechanisms," covering the governing equations and constitutive laws. We will then explore "Applications and Interdisciplinary Connections," demonstrating how FSI modeling is used to create patient-specific diagnostic tools, understand disease, and link mechanics to cell biology. Finally, "Hands-On Practices" will provide opportunities to apply these concepts to practical problems in vascular biomechanics.

## Principles and Mechanisms

The interaction between flowing blood and the deformable vascular wall is a complex, multiphysics phenomenon central to cardiovascular health and disease. Understanding this fluid-structure interaction (FSI) requires a rigorous application of continuum mechanics principles to both the fluid and solid domains, coupled with a precise mathematical description of the conditions at their interface. This chapter elucidates these core principles and the fundamental mechanisms that govern vascular FSI, from the governing equations and material laws to the key physical phenomena and numerical strategies employed in their simulation.

### Mathematical Description of the Coupled System

A robust FSI model begins with a consistent mathematical framework for describing the motion and deformation of the blood and the vessel wall. Because fluids and solids behave so differently, distinct kinematic descriptions are typically adopted for each, creating a coupled system that presents unique theoretical and computational challenges.

#### Kinematic Frameworks: Lagrangian and Eulerian Descriptions

In continuum mechanics, the motion of a body is described by mapping points from a fixed **reference configuration** to a time-varying **current configuration**. The choice of coordinate system for this description is a foundational modeling decision.

The **Lagrangian description**, also known as the material description, tracks individual material points of a body as they move through space. A physical quantity is expressed as a function of a particle's initial position, $\mathbf{X}$ (the material coordinate), and time $t$. The position of that particle at any time is given by the deformation map, $\mathbf{x} = \boldsymbol{\chi}(\mathbf{X}, t)$. Local deformation is quantified by the **[deformation gradient](@entry_id:163749)**, $\mathbf{F} = \nabla_{\!X}\boldsymbol{\chi}$, which describes the stretching and rotation of the material. This framework is exceptionally well-suited for modeling solids, such as the arterial wall. Its primary advantages are that material points retain their identity, which is essential for history-dependent constitutive laws (e.g., viscoelasticity), and that a computational mesh defined on the reference configuration does not become distorted, regardless of how large the deformation becomes.

In contrast, the **Eulerian description**, or spatial description, focuses on fixed points in space, $\mathbf{x}$, and describes the physical properties of the material that passes through those points at time $t$. This approach is standard for fluid dynamics. Blood, as a fluid, undergoes continuous and [large deformations](@entry_id:167243), advection, and mixing. Attempting to track individual fluid parcels with a Lagrangian framework would lead to extreme computational mesh distortion, rendering simulations intractable. The Eulerian framework naturally avoids this issue by observing the flow within a domain whose geometry may evolve but whose coordinate system is not tied to material particles.

The standard approach in vascular FSI is therefore to model the solid arterial wall in a Lagrangian frame and the fluid blood in an Eulerian frame. The central challenge then becomes coupling these disparate descriptions at their moving boundary.

#### Governing Equations of the Continuum

With the kinematic frameworks established, we can state the fundamental laws of motion for each domain.

##### The Solid Domain: Lagrangian Formulation

The motion of the arterial wall is governed by the [balance of linear momentum](@entry_id:193575). In the Lagrangian frame, this is most conveniently expressed in the reference configuration. This avoids the complexity of integrating over a moving domain. The resulting [equation of motion](@entry_id:264286) for the solid is:

$$
\rho_0 \ddot{\mathbf{u}} = \nabla_{\!X} \cdot \mathbf{P} + \rho_0 \mathbf{b}
$$

Here, $\rho_0$ is the material density in the reference configuration, $\mathbf{u}(\mathbf{X}, t) = \boldsymbol{\chi}(\mathbf{X}, t) - \mathbf{X}$ is the displacement of a material point, and $\ddot{\mathbf{u}}$ is its acceleration (the [material time derivative](@entry_id:190892)). The vector $\mathbf{b}$ represents [body forces](@entry_id:174230) per unit mass (e.g., gravity), which are typically negligible in [arterial mechanics](@entry_id:1121120). The crucial term is $\nabla_{\!X} \cdot \mathbf{P}$, the divergence of the **first Piola-Kirchhoff stress tensor** $\mathbf{P}$. This tensor represents forces in the current configuration acting on areas in the reference configuration. It is an unsymmetric tensor related to the true, symmetric **Cauchy stress** $\boldsymbol{\sigma}$ (force per current area) via the deformation gradient $\mathbf{F}$ and its determinant $J = \det(\mathbf{F})$:

$$
\mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-T}
$$

This formulation elegantly contains all information about the [structural dynamics](@entry_id:172684) within the fixed reference domain, making it the standard for solid mechanics computations.

##### The Fluid Domain: Eulerian and ALE Formulations

For the blood, the governing equations are the incompressible Navier-Stokes equations, which represent conservation of mass and momentum. In the standard Eulerian frame, they are:

$$
\nabla \cdot \mathbf{u}_f = 0
$$

$$
\rho_f \left( \frac{\partial \mathbf{u}_f}{\partial t} + (\mathbf{u}_f \cdot \nabla) \mathbf{u}_f \right) = \nabla \cdot \boldsymbol{\sigma}_f + \rho_f \mathbf{b}
$$

where $\rho_f$ is the fluid density, $\mathbf{u}_f$ is the fluid velocity field, and $\boldsymbol{\sigma}_f$ is the fluid Cauchy stress tensor. The term $\frac{\partial \mathbf{u}_f}{\partial t} + (\mathbf{u}_f \cdot \nabla) \mathbf{u}_f$ is the [material acceleration](@entry_id:270992) of a fluid particle. The primary difficulty is that the fluid domain, $\Omega_f(t)$, is not fixed; its boundary moves with the deforming arterial wall. Solving the equations on a fixed Eulerian grid is therefore problematic.

To address this, the **Arbitrary Lagrangian-Eulerian (ALE)** formulation is widely used. The ALE approach introduces a computational mesh that can move independently of both the fluid particles and the fixed spatial frame. The velocity of this mesh is denoted by $\mathbf{w}(\mathbf{x}, t)$. The [material time derivative](@entry_id:190892) of any quantity is then re-expressed in terms of the time derivative on the moving mesh (the ALE derivative) and a convective term relative to the [mesh motion](@entry_id:163293). For the fluid velocity $\mathbf{u}_f$, the [material acceleration](@entry_id:270992) becomes:

$$
\frac{D\mathbf{u}_f}{Dt} = \frac{\partial \mathbf{u}_f}{\partial t}\bigg|_{\boldsymbol{\chi}} + ((\mathbf{u}_f - \mathbf{w}) \cdot \nabla) \mathbf{u}_f
$$

The first term is the ALE time derivative, taken at a constant mesh coordinate $\boldsymbol{\chi}$. The second term is the [convective derivative](@entry_id:262900), where $(\mathbf{u}_f - \mathbf{w})$ is the [relative velocity](@entry_id:178060) of the fluid with respect to the [moving mesh](@entry_id:752196). Substituting this into the momentum equation gives the ALE form of the Navier-Stokes equations:

$$
\rho_f \left( \frac{\partial \mathbf{u}_f}{\partial t}\bigg|_{\boldsymbol{\chi}} + ((\mathbf{u}_f - \mathbf{w}) \cdot \nabla) \mathbf{u}_f \right) = \nabla \cdot \boldsymbol{\sigma}_f + \rho_f \mathbf{b}
$$

In this formulation, the ALE time derivative and the convective term explicitly depend on the arbitrary mesh velocity $\mathbf{w}$, making them frame-dependent terms. The ALE method provides a versatile bridge between the pure Lagrangian and Eulerian viewpoints, allowing the computational fluid domain to deform and track the moving solid boundary.

### The Fluid-Structure Interface: Coupling Conditions

Having defined the governing equations within each domain, the system is closed by specifying the conditions that couple them at the shared, moving interface $\Gamma_{\text{fsi}}(t)$. These conditions enforce the fundamental physical principles of contact: kinematic compatibility and dynamic equilibrium.

#### Kinematic Condition: No-Slip and No-Penetration

The kinematic condition dictates that the fluid at the interface must move with the solid boundary. For a viscous fluid like blood, this encompasses both the **no-penetration** condition (the normal component of the fluid velocity must match the normal velocity of the wall) and the **no-slip** condition (the tangential components must also match). This is expressed as a single vector equality: the fluid velocity at the interface must equal the wall velocity.

This statement requires careful formulation due to the different kinematic frameworks. The fluid velocity $\mathbf{u}_f$ is an Eulerian field, dependent on spatial position $\mathbf{x}$. The wall velocity is the [material time derivative](@entry_id:190892) of the wall's [displacement field](@entry_id:141476) $\mathbf{d}$, which is a Lagrangian quantity dependent on the reference position $\mathbf{X}_w$. To equate them, the fluid velocity must be evaluated at the current spatial location of the wall particle. This leads to the precise statement of the kinematic coupling condition:

$$
\mathbf{u}_f(\boldsymbol{\chi}_w(\mathbf{X}_w, t), t) = \dot{\mathbf{d}}(\mathbf{X}_w, t) \quad \text{for all } \mathbf{X}_w \text{ on the reference interface}
$$

Here, $\mathbf{u}_f(\cdot, t)$ is the Eulerian fluid velocity field, $\boldsymbol{\chi}_w(\mathbf{X}_w, t)$ is the deformation map giving the current position of a wall particle, and $\dot{\mathbf{d}}(\mathbf{X}_w, t) = \partial \mathbf{d}(\mathbf{X}_w, t) / \partial t$ is the velocity of that wall particle. This equation ensures that fluid particles on the boundary adhere to and move with the material of the arterial wall.

#### Dynamic Condition: Traction Continuity

The dynamic condition is a statement of Newton's third law: the force per unit area (traction) exerted by the fluid on the wall must be equal and opposite to the traction exerted by the wall on the fluid. If we define $\mathbf{n}$ as the unit normal on the interface pointing outward from the fluid domain, this condition is expressed as:

$$
\boldsymbol{\sigma}_f \mathbf{n} = \boldsymbol{\sigma}_s \mathbf{n}
$$

This ensures that forces are balanced at the interface, preventing any unphysical net force that would cause infinite acceleration of a massless surface.

The essence of this dynamic coupling can be illustrated with a simplified model. Consider a static, pressurized, thin-walled cylindrical artery of radius $r_i$ and thickness $h$. The internal [fluid pressure](@entry_id:270067) $p$ exerts a force that tends to split the cylinder apart. This force is balanced by the internal circumferential stress, or **hoop stress** $\sigma_{\theta}$, within the wall material. By considering a [force balance](@entry_id:267186) on a half-cylinder, the fluid pressure integrated over the projected area ($p \cdot 2r_i L$) must equal the [hoop stress](@entry_id:190931) integrated over the cut wall area ($\sigma_{\theta} \cdot 2hL$). This equilibrium reduces to the well-known Law of Laplace for a thin-walled cylinder:

$$
\sigma_{\theta} = \frac{p r_i}{h}
$$

This simple relation is a direct consequence of [traction continuity](@entry_id:756091), where the fluid's normal traction (pressure) is balanced by the solid's internal stress. For instance, a typical blood pressure of $p = 13.2 \, \mathrm{kPa}$ in an artery with $r_i = 1.8 \, \mathrm{mm}$ and $h = 0.42 \, \mathrm{mm}$ would generate a wall [hoop stress](@entry_id:190931) of approximately $\sigma_{\theta} = 56.6 \, \mathrm{kPa}$. In a full dynamic FSI simulation, this balance of traction must be satisfied continuously in time and space at the moving interface.

### Constitutive Modeling: Defining Material Behavior

The governing equations are general to any continuum. To model a specific system like an artery, they must be supplemented with **constitutive laws** that describe the material behavior—how stress relates to deformation.

#### Blood Rheology: From Newtonian to Non-Newtonian Models

For an incompressible generalized Newtonian fluid, the deviatoric part of the Cauchy stress, $\boldsymbol{\tau}_f$, is related to the [rate-of-deformation tensor](@entry_id:184787), $\mathbf{D} = \frac{1}{2}(\nabla \mathbf{u}_f + (\nabla \mathbf{u}_f)^T)$, by:

$$
\boldsymbol{\tau}_f = 2 \mu(\dot{\gamma}) \mathbf{D}
$$

where $\dot{\gamma} = \sqrt{2\mathbf{D}:\mathbf{D}}$ is the [scalar shear rate](@entry_id:754538). The function $\mu(\dot{\gamma})$ is the [apparent viscosity](@entry_id:260802), and different choices for this function define different [rheological models](@entry_id:193749).

*   **Newtonian Model**: For flow in large arteries where shear rates are high, it is often sufficient to assume blood behaves as a **Newtonian fluid** with a constant [dynamic viscosity](@entry_id:268228), $\mu \approx 3.5 \times 10^{-3} \, \mathrm{Pa \cdot s}$.

*   **Shear-Thinning Models**: Blood is a suspension of cells, and at lower shear rates, [red blood cells](@entry_id:138212) tend to aggregate into stacks called "rouleaux". These aggregates increase the fluid's resistance to flow. As shear rate increases, the rouleaux break up, and the apparent viscosity decreases. This **[shear-thinning](@entry_id:150203)** behavior is significant in smaller vessels or regions of flow stagnation. The **Carreau-Yasuda model** is a sophisticated [empirical model](@entry_id:1124412) that captures this behavior:
    $$
    \mu(\dot{\gamma}) = \mu_{\infty} + (\mu_{0} - \mu_{\infty}) \left[ 1 + (\lambda \dot{\gamma})^{a} \right]^{\frac{n - 1}{a}}
    $$
    Here, $\mu_0$ and $\mu_\infty$ are the viscosities at zero and infinite shear rates, respectively; $\lambda$ is a time constant; and $a$ and $n$ ($n \lt 1$ for [shear-thinning](@entry_id:150203)) are dimensionless parameters that shape the transition.

*   **Yield-Stress Models**: At very low shear rates, the rouleaux network can form a structure that resists flow entirely until a certain **[yield stress](@entry_id:274513)**, $\tau_y$, is exceeded. The **Casson model** is often used to describe this behavior in blood, relating shear stress $\tau$ to shear rate $\dot{\gamma}$ in [simple shear](@entry_id:180497) as:
    $$
    \sqrt{\tau} = \sqrt{\tau_{y}} + \sqrt{\eta_{C}} \sqrt{\dot{\gamma}} \quad (\text{for } \tau \ge \tau_y)
    $$
    where $\eta_C$ is a consistency parameter. Below the yield stress ($\tau \lt \tau_y$), there is no flow ($\dot{\gamma}=0$).

#### Arterial Wall Mechanics: Hyperelastic and Anisotropic Models

The arterial wall is a complex composite material exhibiting nonlinear, anisotropic, and nearly incompressible behavior. This is captured using **hyperelastic** models, where the stress is derived from a **[strain-energy density function](@entry_id:755490)**, $W$, which represents the elastic energy stored per unit reference volume.

*   **Linear Elasticity**: For very small deformations, a simple linear elastic model can be used as a first approximation. The [strain energy](@entry_id:162699) is a quadratic function of the Green-Lagrange strain tensor $\mathbf{E} = \frac{1}{2}(\mathbf{F}^T\mathbf{F} - \mathbf{I})$:
    $$
    W_{\mathrm{lin}}(\mathbf{E}) = \tfrac{1}{2}\lambda (\mathrm{tr}\,\mathbf{E})^{2} + \mu\,\mathrm{tr}(\mathbf{E}^{2})
    $$
    where $\lambda$ and $\mu$ are the Lamé parameters.

*   **Fung-type Exponential Models**: Arterial tissue exhibits significant stiffening at higher strains. To capture this, Fung proposed phenomenological exponential models. A common form for orthotropic tissue (with different properties in axial and circumferential directions) is:
    $$
    W_{\mathrm{Fung}}(\mathbf{E}) = \tfrac{c}{2}\left(\exp\left[Q(\mathbf{E})\right] - 1\right)
    $$
    where $c$ is a stress-like parameter and $Q(\mathbf{E})$ is a quadratic form of the strain components (e.g., $Q = b_{11} E_{\theta\theta}^{2} + b_{22} E_{zz}^{2} + 2 b_{12} E_{\theta\theta}E_{zz} + \dots$).

*   **Anisotropic Fiber-Reinforced Models**: The mechanical properties of the arterial wall are dominated by its micro-constituents: a soft, isotropic ground matrix (elastin) reinforced by much stiffer collagen fibers, typically arranged in helical families. The **Holzapfel-Gasser-Ogden (HGO) model** is a widely used micromechanically-motivated model that explicitly accounts for this structure. The [strain energy](@entry_id:162699) is additively decomposed into an isotropic part for the matrix and anisotropic parts for the fiber families:
    $$
    W_{\mathrm{HGO}}(\mathbf{C}) = W_{\text{iso}}(I_1) + W_{\text{aniso}}
    $$
    The isotropic part is often a Neo-Hookean term, $W_{\text{iso}} = \frac{\mu}{2}(I_1-3)$, where $I_1 = \mathrm{tr}(\mathbf{C})$ is the first invariant of the right Cauchy-Green tensor $\mathbf{C} = \mathbf{F}^T\mathbf{F}$. The anisotropic part models the contribution of two symmetrically oriented fiber families. A common form is:
    $$
    W_{\text{aniso}} = \sum_{i=1}^{2}\tfrac{k_{1}}{2 k_{2}}\left(\exp\left[k_{2}\langle E_i \rangle^2\right] - 1\right)
    $$
    where $I_{4i} = \mathbf{N}_i \cdot \mathbf{C} \mathbf{N}_i$ measures the squared stretch in the fiber directions $\mathbf{N}_i$, and $E_i = \kappa(I_1-3) + (1-3\kappa)(I_{4i}-1)$ is an effective fiber strain that includes a dispersion parameter $\kappa \in [0, 1/3]$ to account for the [angular distribution](@entry_id:193827) of fibers. The parameters $k_1$ (stress-like) and $k_2$ (dimensionless) control the fiber stiffness and [non-linearity](@entry_id:637147), and the Macauley brackets $\langle \cdot \rangle$ ensure that fibers only bear load when in tension ($E_i \gt 0$).

### Key Physical Mechanisms and Phenomena

The interplay of fluid inertia, viscosity, and structural elasticity gives rise to several characteristic phenomena that can be understood through [dimensional analysis](@entry_id:140259) and simplified models.

#### Dimensionless Parameters in Vascular FSI

Dimensionless numbers provide a powerful way to characterize the dominant physical forces in a flow. In vascular [hemodynamics](@entry_id:149983), several are critical:

*   **Reynolds Number ($\mathrm{Re} = \rho_f U D / \mu$)**: The ratio of inertial to viscous forces. In the human aorta ($D \approx 2.5 \, \mathrm{cm}, U \approx 0.4 \, \mathrm{m/s}$), $\mathrm{Re}$ can reach $2000-4000$, indicating that inertial forces are dominant and flow can be transitional or mildly turbulent. In small arteries ($D \approx 2 \, \mathrm{mm}, U \approx 0.1 \, \mathrm{m/s}$), $\mathrm{Re}$ is much lower, around $30-100$, and viscous forces are more significant.

*   **Womersley Number ($\alpha = \frac{D}{2}\sqrt{\omega/\nu}$)**: The ratio of transient [inertial forces](@entry_id:169104) to [viscous forces](@entry_id:263294), where $\omega$ is the angular frequency of the [cardiac cycle](@entry_id:147448) and $\nu$ is the kinematic viscosity. It governs the shape of the velocity profile in pulsatile flow. For $\alpha \gg 1$ (e.g., $\alpha \sim 17$ in the aorta), inertial effects dominate, leading to flat, "plug-like" velocity profiles. For $\alpha \sim 1$ (e.g., $\alpha \sim 1.4$ in small arteries), viscous effects have time to diffuse across the vessel, resulting in more parabolic profiles.

*   **Strouhal Number ($\mathrm{St} = \omega D / U$)**: The ratio of local (unsteady) acceleration to convective acceleration. It characterizes the importance of flow unsteadiness relative to the mean flow.

*   **Dean Number ($\mathrm{De} = \mathrm{Re}\sqrt{D/(2R_c)}$)**: Characterizes the strength of secondary, swirling flows in curved vessels (with [radius of curvature](@entry_id:274690) $R_c$). In the curved aortic arch, $\mathrm{De}$ can be on the order of $10^3$, leading to strong [secondary flows](@entry_id:754609) that significantly influence wall shear stress patterns.

#### The Added-Mass Effect

When a structure is immersed in a fluid, the accelerating fluid exerts an [inertial force](@entry_id:167885) on the structure. This is known as the **[added-mass effect](@entry_id:746267)**. From the structure's perspective, it behaves as if its own mass has been increased. This mechanism is a crucial component of the dynamic FSI coupling.

The impact of [added mass](@entry_id:267870) can be clearly illustrated by a simplified model of a radially vibrating artery. The natural frequency of the arterial wall vibrating in a vacuum (the "dry" frequency, $f_d$) is determined by its stiffness $K$ and mass $M_s$, with $\omega_d^2 = K/M_s$. When filled with fluid, the total effective mass of the system becomes the wall mass plus the added mass of the fluid, $M_a$. The "wet" natural frequency, $f_w$, is then given by $\omega_w^2 = K/(M_s + M_a)$. This immediately leads to the relationship:

$$
f_w = \frac{f_d}{\sqrt{1 + M_a/M_s}}
$$

The fluid's presence always lowers the natural frequency of the structure. The magnitude of this frequency shift is governed by the non-dimensional mass ratio $M_a/M_s$. In arteries, where the density of the wall ($\rho_s \approx 1200 \, \mathrm{kg/m^3}$) is close to that of blood ($\rho_f \approx 1060 \, \mathrm{kg/m^3}$), the [added mass](@entry_id:267870) is significant and can substantially alter the dynamic response of the vessel.

#### Wall Shear Stress and its Biological Significance

One of the most important outputs of vascular FSI analysis is the **wall shear stress (WSS)**, $\boldsymbol{\tau}_w$. This is the tangential component of the [traction vector](@entry_id:189429) exerted by the flowing blood on the luminal surface of the artery. Endothelial cells lining the artery wall are highly sensitive [mechanoreceptors](@entry_id:164130) that sense WSS and transduce this mechanical signal into biochemical responses, a process known as [mechanotransduction](@entry_id:146690). WSS is therefore a critical regulator of vascular health and remodeling.

While the instantaneous WSS vector is complex, several time-averaged metrics are commonly used to correlate hemodynamic environments with biological outcomes. These are typically defined at each point $\mathbf{x}$ on the wall:

*   **Time-Averaged Wall Shear Stress (TAWSS)**: The magnitude of the WSS vector averaged over a cardiac cycle of period $T$. Arterial regions are typically exposed to a TAWSS of $1-7 \, \mathrm{Pa}$. Regions of chronically low TAWSS are prone to atherosclerosis.
    $$
    \mathrm{TAWSS}(\mathbf{x}) = \frac{1}{T} \int_{0}^{T} \| \boldsymbol{\tau}_w(\mathbf{x}, t) \| dt
    $$

*   **Oscillatory Shear Index (OSI)**: A dimensionless metric that quantifies the unidirectionality of the WSS vector over the [cardiac cycle](@entry_id:147448). It ranges from $0$ (for unidirectional shear) to $0.5$ (for purely oscillatory shear with zero mean). High OSI indicates disturbed flow with significant flow reversal, which is also strongly pro-atherogenic.
    $$
    \mathrm{OSI}(\mathbf{x}) = \frac{1}{2} \left( 1 - \frac{\left\| \int_{0}^{T} \boldsymbol{\tau}_w(\mathbf{x}, t) dt \right\|}{\int_{0}^{T} \| \boldsymbol{\tau}_w(\mathbf{x}, t) \| dt} \right)
    $$

*   **Relative Residence Time (RRT)**: A metric that combines TAWSS and OSI to estimate the residence time of atherogenic particles near the wall. It is inversely proportional to the magnitude of the mean WSS vector. High RRT is correlated with sites of lesion development.
    $$
    \mathrm{RRT}(\mathbf{x}) = \frac{1}{(1 - 2\,\mathrm{OSI}(\mathbf{x}))\,\mathrm{TAWSS}(\mathbf{x})}
    $$

### Numerical Mechanisms for Unfitted FSI

Solving the fully coupled FSI problem is computationally demanding. While [body-fitted mesh](@entry_id:746897) methods (where the fluid mesh conforms to the moving boundary) are common, they can be challenging for the [large deformations](@entry_id:167243) and complex geometries found in patient-specific vascular models. An alternative class of methods are **[unfitted methods](@entry_id:173094)**, where the fluid is solved on a fixed or non-conforming background grid, and the solid is "immersed" within it. These methods differ primarily in the numerical mechanism used to enforce the [interface coupling](@entry_id:750728) conditions.

*   **Immersed Boundary (IB) and Immersed Finite Element (IFEM) Methods**: These methods represent the structure as a set of Lagrangian points embedded in the Eulerian fluid grid. The dynamic coupling is achieved by calculating elastic forces on the Lagrangian points and spreading them to the surrounding fluid grid as a [body force](@entry_id:184443), typically using a regularized Dirac [delta function](@entry_id:273429). The kinematic coupling is enforced by interpolating the fluid velocity from the Eulerian grid to the Lagrangian points and using that to advect the structure. This creates a weak, penalty-like enforcement of the [interface conditions](@entry_id:750725).

*   **Fictitious Domain Methods**: In this approach, the fluid equations are solved over a larger, simple-shaped domain that contains both the fluid and solid. The kinematic constraint ($\mathbf{u}_f = \dot{\mathbf{d}}$) is then enforced strictly on the interface (or throughout the solid domain) using a field of **Lagrange multipliers**. This leads to a saddle-point system that must be solved for the fluid velocity, pressure, and the multipliers, which physically represent the [constraint forces](@entry_id:170257).

*   **Nitsche-based Methods**: This family of methods enforces [interface conditions](@entry_id:750725) weakly within the [variational formulation](@entry_id:166033) of the problem, but without introducing Lagrange multipliers. This is achieved by adding carefully designed terms to the [weak form](@entry_id:137295), including a symmetric term for consistency, a skew-symmetric term for stability, and a mesh-dependent penalty term to enforce the kinematic constraint. These methods often require additional stabilization techniques for the "cut cells" of the background grid that are intersected by the immersed boundary.

Each of these numerical mechanisms provides a different trade-off between implementation complexity, computational cost, and the mathematical rigor with which the fundamental [interface conditions](@entry_id:750725) are satisfied.