## Introduction
Simulating flows laden with particles, droplets, or bubbles is a fundamental challenge in [computational fluid dynamics](@entry_id:142614) (CFD) with profound implications across science and engineering. From predicting pollutant dispersal in the atmosphere to optimizing industrial combustion and designing next-generation [drug delivery systems](@entry_id:161380), the ability to accurately model these multiphase systems is critical. Discrete Phase Modeling (DPM), a powerful Eulerian-Lagrangian technique, offers a framework for tackling this complexity by tracking the journey of individual particles through a continuous fluid. However, mastering this method requires a deep understanding of the intricate physics governing particle motion and its interaction with the surrounding flow.

This article provides a comprehensive guide to the theory and application of discrete phase modeling and [particle tracking](@entry_id:190741). It aims to bridge the gap between fundamental principles and practical implementation. The reader will embark on a structured journey through the core concepts of DPM. The first chapter, "Principles and Mechanisms," lays the theoretical groundwork, dissecting the particle [equation of motion](@entry_id:264286) and the forces that dictate its trajectory. The second chapter, "Applications and Interdisciplinary Connections," showcases the versatility of DPM by exploring its use in diverse fields, from industrial filtration to astrophysics. Finally, the "Hands-On Practices" section offers concrete problems to solidify understanding and connect theory with computational practice. We begin by exploring the fundamental modeling paradigms and the governing equations that form the bedrock of [particle tracking](@entry_id:190741) simulations.

## Principles and Mechanisms

The motion of a discrete phase, such as solid particles, liquid droplets, or gas bubbles, through a continuous fluid phase is governed by a complex interplay of forces and momentum exchange. In the Eulerian-Lagrangian framework, commonly known as Discrete Phase Modeling (DPM), this dynamic is simulated by tracking the trajectories of individual computational "parcels" representing clusters of real particles, while the carrier fluid is treated as a continuum. This chapter elucidates the fundamental principles and mechanisms that form the basis of this widely used modeling approach.

### Fundamental Modeling Paradigms

The simulation of multiphase flows can be broadly categorized into two main frameworks: the Eulerian-Eulerian approach and the Eulerian-Lagrangian approach. Understanding their core philosophies is essential for selecting the appropriate model for a given physical problem .

The **Eulerian-Eulerian model**, often called the Two-Fluid Model, treats each phase as a fully interpenetrating continuum. For each phase $k$, a set of conservation equations for mass, momentum, and energy is solved on a fixed Eulerian grid. These equations involve field variables such as the volume fraction $\alpha_k(\boldsymbol{x},t)$, velocity $\boldsymbol{u}_k(\boldsymbol{x},t)$, and temperature. The phases are coupled through interphase exchange terms representing forces like drag and lift. This approach is particularly well-suited for dense flows where the [dispersed phase](@entry_id:748551) volume fraction is high and its collective behavior can be described by [continuum mechanics](@entry_id:155125).

In contrast, the **Eulerian-Lagrangian model** or **Discrete Phase Model (DPM)**, adopts a hybrid perspective. The carrier fluid is described in an Eulerian frame by solving the Navier-Stokes equations on a computational grid. The [dispersed phase](@entry_id:748551), however, is treated as a collection of discrete elements (particles, droplets, or bubbles), whose trajectories are tracked individually in a Lagrangian frame. The path of each particle is determined by integrating Newton's second law, accounting for the various forces exerted by the fluid. This approach is most effective for dilute to moderately dense flows where the [dispersed phase](@entry_id:748551) is sufficiently sparse that resolving the details of individual particle-particle interactions and their direct effect on the local flow is computationally feasible or can be modeled statistically.

A cornerstone of the standard DPM approach is the **point-particle assumption**. This assumption simplifies the complex reality of a finite-sized particle by treating it as a point mass concentrated at its center of mass. The forces acting on this [point mass](@entry_id:186768) are calculated based on the properties of the *undisturbed* fluid flow, evaluated at the particle's location. This simplification is computationally efficient as it obviates the need to resolve the flow field around each particle. However, its validity rests on a set of stringent criteria :

1.  The particle diameter, $d_p$, must be much smaller than the characteristic grid spacing of the [fluid simulation](@entry_id:138114), $\Delta$. That is, $d_p \ll \Delta$. This ensures the particle is a sub-grid object, making the concept of an "undisturbed" [fluid velocity](@entry_id:267320) at its location meaningful.

2.  The particle diameter must be much smaller than the smallest scale of fluid motion, the Kolmogorov length scale, $\eta$. That is, $d_p \ll \eta$. This condition ensures that the fluid velocity field is smooth and approximately linear across the particle's volume, justifying the neglect of so-called **Faxén corrections** which account for flow curvature.

3.  The particle Reynolds number, $Re_p$, must be very small, ideally $Re_p \ll 1$. This signifies that the flow around the particle is in the creeping (Stokes) regime, where the disturbance created by the particle is localized and symmetric. At higher $Re_p$, a structured, finite-sized wake forms, which fundamentally violates the "point force" idealization.

While practical models often extend beyond these strict limits using empirical corrections, these conditions define the theoretical foundation upon which the particle equation of motion is built.

### The Particle Equation of Motion

The trajectory of a particle is found by integrating Newton's second law, where the particle's mass times its acceleration is balanced by the sum of forces acting upon it. For a spherical particle of mass $m_p$ and velocity $\boldsymbol{v}_p$, this is written as:

$$m_p \dfrac{d\boldsymbol{v}_p}{dt} = \sum \boldsymbol{F}_i$$

The most comprehensive form of this equation for a small, rigid sphere in a non-uniform, unsteady flow is the **Maxey-Riley-Gatignol equation**. Below, we dissect its primary components, which represent distinct physical mechanisms  .

#### Gravity and Buoyancy

The most straightforward forces are gravity acting on the particle's mass, $m_p \boldsymbol{g}$, and the [buoyancy force](@entry_id:154088), which by Archimedes' principle is equal to the weight of the displaced fluid, $-m_f \boldsymbol{g}$, where $m_f = \rho_f V_p$ is the mass of fluid displaced by the particle of volume $V_p$. These are typically combined into a single net [gravitational force](@entry_id:175476):

$$\boldsymbol{F}_{g/b} = (m_p - m_f)\boldsymbol{g} = (\rho_p - \rho_f)V_p\boldsymbol{g}$$

where $\rho_p$ and $\rho_f$ are the particle and fluid densities, respectively.

#### Drag Force

The drag force is the resistance exerted by the fluid on the particle due to their [relative motion](@entry_id:169798). In the point-particle limit and for low particle Reynolds number ($Re_p \ll 1$), this force is described by **Stokes' law**:

$$\boldsymbol{F}_D = 3\pi\mu d_p (\boldsymbol{u} - \boldsymbol{v}_p)$$

where $\mu$ is the fluid [dynamic viscosity](@entry_id:268228), $d_p$ is the particle diameter, and $(\boldsymbol{u} - \boldsymbol{v}_p)$ is the slip velocity between the undisturbed [fluid velocity](@entry_id:267320) at the particle's location, $\boldsymbol{u}$, and the particle velocity, $\boldsymbol{v}_p$. The drag force always acts to reduce this slip.

#### Pressure-Gradient Force

A particle in an accelerating fluid experiences a force due to the pressure gradient in the surrounding flow field. Even if the particle were held fixed, a pressure gradient $\nabla p$ in the undisturbed flow would exert a [net force](@entry_id:163825) $-V_p \nabla p$ on its volume. For an [incompressible fluid](@entry_id:262924), the momentum equation relates this pressure gradient to fluid acceleration. Neglecting viscous terms (which are part of Faxén corrections), this force on the particle is equal to the mass of the displaced fluid multiplied by the acceleration that a fluid element would have at that location:

$$\boldsymbol{F}_P = m_f \dfrac{D\boldsymbol{u}}{Dt}$$

Here, $\frac{D\boldsymbol{u}}{Dt} = \frac{\partial \boldsymbol{u}}{\partial t} + \boldsymbol{u} \cdot \nabla \boldsymbol{u}$ is the [material derivative](@entry_id:266939) of the fluid, evaluated at the particle's position. This force is particularly important when the fluid itself is undergoing rapid acceleration.

#### Added Mass Force

When a particle accelerates relative to the fluid, it must also accelerate the fluid in its immediate vicinity. By Newton's third law, the fluid exerts a reaction force on the particle. This is the **added mass** or **virtual mass** force. For a rigid sphere, this force is given by:

$$\boldsymbol{F}_{AM} = \dfrac{1}{2} m_f \left( \dfrac{D\boldsymbol{u}}{Dt} - \dfrac{d\boldsymbol{v}_p}{dt} \right)$$

The term is proportional to the relative acceleration between the fluid and the particle. The coefficient $C_{AM}=1/2$ is the inviscid added-mass coefficient for a sphere. This force represents the additional inertia imparted to the system by the co-moving fluid.

#### The Assembled Equation and Effective Inertia

Combining the forces and rearranging the [equation of motion](@entry_id:264286) by gathering all terms involving the particle's acceleration, $\frac{d\boldsymbol{v}_p}{dt}$, on the left-hand side yields a powerful form of the equation :

$$m_p \dfrac{d\boldsymbol{v}_p}{dt} = \boldsymbol{F}_{g/b} + \boldsymbol{F}_D + \boldsymbol{F}_P + \boldsymbol{F}_{AM}$$

Substituting the expressions for the forces gives:

$$m_p \dfrac{d\boldsymbol{v}_p}{dt} = (\rho_p - \rho_f)V_p\boldsymbol{g} + 3\pi\mu d_p (\boldsymbol{u} - \boldsymbol{v}_p) + m_f \dfrac{D\boldsymbol{u}}{Dt} + \dfrac{1}{2} m_f \left( \dfrac{D\boldsymbol{u}}{Dt} - \dfrac{d\boldsymbol{v}_p}{dt} \right)$$

Moving the [particle acceleration](@entry_id:158202) term from the [added mass](@entry_id:267870) force to the left side:

$$\left( m_p + \dfrac{1}{2} m_f \right) \dfrac{d\boldsymbol{v}_p}{dt} = (\rho_p - \rho_f)V_p\boldsymbol{g} + 3\pi\mu d_p (\boldsymbol{u} - \boldsymbol{v}_p) + \dfrac{3}{2} m_f \dfrac{D\boldsymbol{u}}{Dt}$$

This form elegantly reveals that the particle's response to external forces is governed by an **effective inertia** of $(m_p + \frac{1}{2}m_f)$, the sum of its own mass and the [added mass](@entry_id:267870) of the fluid. The right-hand side now contains all external forcing terms. This equation, neglecting the Basset and other higher-order terms, is often referred to as the Maxey-Riley equation.

### Advanced and Unsteady Forces

The equation of motion can include additional terms that are physically important in specific regimes but are often neglected due to their complexity and computational cost.

#### The Basset History Force

The Basset force is a unique and challenging term that accounts for the history of the particle's motion. Its physical origin lies in the slow, [viscous diffusion](@entry_id:187689) of [vorticity](@entry_id:142747) from the particle's surface following a change in its [relative velocity](@entry_id:178060) . This diffusing vorticity continues to influence the stress on the particle at later times, giving rise to a "memory" effect. Mathematically, it is expressed as a convolution integral over the history of the particle's slip acceleration:

$$\boldsymbol{F}_B = 6 \pi a^2 \mu \int_{0}^{t} \dfrac{1}{\sqrt{\pi \nu (t-\tau)}} \dfrac{d}{d \tau} \left( \boldsymbol{u}(\boldsymbol{x}_p(\tau), \tau) - \boldsymbol{v}_p(\tau) \right) d \tau$$

where $a$ is the particle radius and $\nu = \mu/\rho_f$ is the fluid [kinematic viscosity](@entry_id:261275). The kernel $(t-\tau)^{-1/2}$ shows that recent accelerations have a strong influence that slowly decays over time. Because this force is non-local in time, requiring an integral over the entire particle trajectory at each time step, it is computationally very expensive and is often omitted unless the flow is highly unsteady and particles are neutrally buoyant or lighter than the fluid.

#### Lift Forces

In the presence of velocity gradients (shear) or particle rotation, forces can arise that are transverse (perpendicular) to the direction of slip. One of the most important is the **Saffman [lift force](@entry_id:274767)**, which acts on a particle in a [simple shear](@entry_id:180497) flow . It is an inertial effect, arising from the interaction of the [shear flow](@entry_id:266817) with the disturbance created by the particle. For a spherical particle in the limit of small particle Reynolds number ($Re_p$), small shear Reynolds number ($Re_s = d_p^2 |\dot{\gamma}|/\nu \ll 1$), and small slip velocity relative to the shear velocity scale ($|\boldsymbol{u}-\boldsymbol{v}_p| \ll \sqrt{\nu |\dot{\gamma}|}$), the Saffman lift force scales as:

$$F_L \sim \mu d_p^2 |\boldsymbol{u}-\boldsymbol{v}_p| \sqrt{\dfrac{|\dot{\gamma}|}{\nu}}$$

where $\dot{\gamma}$ is the shear rate. This force tends to push particles away from regions of high shear, a phenomenon relevant in many boundary-layer flows.

### Drag Laws Beyond the Stokes Regime

The assumption of Stokes drag is strictly valid only for $Re_p \ll 1$. For most engineering applications, particles experience higher Reynolds numbers, where inertial effects in the flow around the particle become significant, leading to wake formation and increased drag.

The flow regime is characterized by the **particle Reynolds number**, defined as the ratio of inertial to viscous forces in the flow around the particle :

$$Re_p = \dfrac{\rho_f d_p |\boldsymbol{u} - \boldsymbol{v}_p|}{\mu}$$

To account for the deviation from Stokes drag, the drag force is more generally written using a [drag coefficient](@entry_id:276893), $C_D$:

$$\boldsymbol{F}_D = \dfrac{1}{8} \pi d_p^2 \rho_f |\boldsymbol{u} - \boldsymbol{v}_p| (\boldsymbol{u} - \boldsymbol{v}_p) C_D$$

For a sphere, the Stokes law corresponds to $C_D = 24/Re_p$. For higher $Re_p$, $C_D$ must be determined from empirical correlations. A widely used correlation is the **Schiller-Naumann model**, which provides a smooth transition from the Stokes regime to more inertial regimes:

$$C_D = \dfrac{24}{Re_p}(1 + 0.15 Re_p^{0.687})$$

This model is generally applicable for $Re_p$ up to about $1000$. For very high Reynolds numbers ($10^3 \lesssim Re_p \lesssim 2 \times 10^5$), the drag coefficient becomes nearly constant in what is known as the **Newton regime**, with $C_D \approx 0.44$ for a smooth sphere.

### Characterizing Particle-Flow Interaction

The dynamic behavior of particles is not only governed by the forces but also by the timescale of their response relative to the timescale of the fluid flow, and by the collective effect of the particle phase on the fluid.

#### The Stokes Number

A crucial dimensionless parameter for characterizing particle inertia is the **Stokes number ($St$)**. It is defined as the ratio of the particle's characteristic [response time](@entry_id:271485), $\tau_p$, to a characteristic timescale of the flow, $\tau_f$:

$$St = \dfrac{\tau_p}{\tau_f}$$

The **particle [relaxation time](@entry_id:142983), $\tau_p$**, is the time a particle would take to relax to a new fluid velocity under the influence of Stokes drag alone. From the simplified equation of motion, it can be derived as :

$$\tau_p = \dfrac{\rho_p d_p^2}{18\mu}$$

The flow timescale, $\tau_f$, depends on the specific problem; for a [turbulent flow](@entry_id:151300), it might be an eddy turnover time, while for an oscillating flow with frequency $\omega$, it is typically $\tau_f = 1/\omega$.

The Stokes number provides deep physical insight:
-   **$St \ll 1$**: The particle [response time](@entry_id:271485) is much shorter than the flow timescale. The particle has low inertia and acts as a faithful **tracer** of the [fluid motion](@entry_id:182721), following even rapid fluctuations.
-   **$St \gg 1$**: The particle response time is much longer than the flow timescale. The particle has high inertia and its trajectory **decouples** from the fluid fluctuations. It tends to travel in a straight line, cutting through [turbulent eddies](@entry_id:266898).
-   **$St \approx 1$**: The particle responds on a timescale similar to the flow. This can lead to complex behaviors, such as [preferential concentration](@entry_id:199717), where particles are centrifuged out of eddies and accumulate in regions of high strain and low vorticity.

#### Coupling Regimes

The level of interaction between the dispersed and continuous phases determines the complexity of the required model. These "coupling" regimes are classified based on the feedback from the particles to the fluid and on interactions between particles themselves .

-   **One-way coupling**: The fluid affects the motion of the particles, but the particles have a negligible effect on the fluid. This is valid for very dilute flows where the momentum exchanged is insignificant compared to the fluid's momentum. The primary criterion is a low **[mass loading](@entry_id:751706)**, $\Phi_m = (\alpha_p \rho_p) / ((1-\alpha_p)\rho_f)$, with a typical threshold of $\Phi_m \lesssim 0.1$.

-   **Two-way coupling**: The particles affect the fluid in addition to the fluid affecting the particles. This is necessary when the [mass loading](@entry_id:751706) is significant ($\Phi_m \gtrsim 0.1$). The effect of the particles on the fluid is implemented by calculating the momentum, heat, and mass exchanged by all particles in a given fluid [control volume](@entry_id:143882) and adding this as a **source term** to the fluid's governing conservation equations.

-   **Four-way coupling**: In addition to two-way fluid-particle coupling, particle-particle collisions are dynamically significant. This regime is entered when the **collision number**, $N_c$ (the average number of collisions a particle experiences over a flow timescale), is on the order of one or greater ($N_c \gtrsim 1$). This requires an additional computational model, such as a stochastic model or a [discrete element method](@entry_id:748501) (DEM), to handle the momentum and energy exchange during inter-particle collisions.

### Particle Tracking in Turbulent Flows

Applying the DPM in the context of turbulent flow simulations, such as Reynolds-Averaged Navier-Stokes (RANS) or Large-Eddy Simulation (LES), introduces a fundamental [closure problem](@entry_id:160656). The particle [equation of motion](@entry_id:264286) requires the instantaneous [fluid velocity](@entry_id:267320), $\boldsymbol{u}(\boldsymbol{x}_p, t)$, at the particle's location. However, RANS provides only the [mean velocity](@entry_id:150038), and LES provides only the filtered (large-scale) velocity, $\bar{\boldsymbol{u}}$.

#### Stochastic Models for Turbulent Dispersion

To account for the effect of the unresolved turbulent velocity fluctuations on the particle trajectory, **stochastic tracking** or **discrete random walk (DRW)** models are employed. These models add a random velocity component to the mean or resolved velocity to simulate the effect of a turbulent eddy interacting with the particle.

A physically sophisticated approach is based on a **Langevin equation**, which models the evolution of the fluctuating velocity seen by the particle, $u_i'$, as an Ornstein-Uhlenbeck [stochastic process](@entry_id:159502) :

$$du_i' = -\frac{u_i'}{T_L}\,dt + \sqrt{C_0\,\epsilon}\,dW_t$$

This model is constrained by [turbulence theory](@entry_id:264896). The drift term, $-u_i'/T_L$, ensures that the velocity fluctuations decorrelate over the **Lagrangian integral timescale, $T_L$**. The random forcing term, $\sqrt{C_0 \epsilon} dW_t$, represents the random kicks from turbulent eddies, with a magnitude set by the turbulent kinetic energy **dissipation rate, $\epsilon$**, and the universal **Lagrangian structure constant, $C_0$**. The timescale $T_L$ is itself related to the turbulence properties (e.g., $T_L \propto k/\epsilon$). This model provides a way to reconstruct a statistically realistic velocity signal to drive the particle motion.

#### Subgrid-Scale Forces in LES

The need for such stochastic models can be seen most clearly in the context of LES . When the decomposition $\boldsymbol{u} = \bar{\boldsymbol{u}} + \boldsymbol{u}'$ is substituted into the full particle [equation of motion](@entry_id:264286) (e.g., the Maxey-Riley-Gatignol equation), each force term splits into a part dependent on the resolved field $\bar{\boldsymbol{u}}$ and a part dependent on the subgrid-scale (SGS) field $\boldsymbol{u}'$. Summing all the SGS-dependent parts results in a net **unclosed SGS force**, $\boldsymbol{f}_{\mathrm{SGS}}$:

$$\boldsymbol{f}_{\mathrm{SGS}} = \boldsymbol{f}_{\mathrm{SGS}}(\boldsymbol{u}', \nabla\boldsymbol{u}', \frac{D\boldsymbol{u}'}{Dt}, ...)$$

This SGS force represents the real physical effect of the unresolved small-scale eddies on the particle. To solve the particle's motion in an LES, this force must be modeled. The Langevin model described above can be interpreted as a way of modeling the SGS velocity $\boldsymbol{u}'_p$ seen by the particle, which is the primary input needed to estimate the dominant components of $\boldsymbol{f}_{\mathrm{SGS}}$, particularly the SGS drag. This rigorously connects the principles of particle dynamics with the realities of [turbulence modeling](@entry_id:151192) in modern CFD.