## Introduction
Granular materials, from sand dunes and soil to powders in pharmaceutical manufacturing, are ubiquitous in nature and industry. Despite their simple constituents, their collective behavior is remarkably complex, exhibiting properties of solids, liquids, and gases. Understanding and predicting this behavior is a central challenge in fields ranging from geomechanics to process engineering. The Discrete Element Method (DEM) has emerged as a preeminent computational tool to address this challenge, offering a direct route to connect the microscopic interactions between individual particles to the macroscopic, bulk phenomena we observe.

The primary knowledge gap that DEM addresses is the lack of continuum models that can universally capture the rich physics of granular systems, such as [force chains](@entry_id:199587), [dilatancy](@entry_id:201001), and segregation. By simulating the system from the bottom up, particle by particle, DEM provides a virtual laboratory to uncover the fundamental principles governing these behaviors.

This article provides a graduate-level exploration of the DEM framework. In **Principles and Mechanisms**, we will dissect the algorithmic core of the method, from [contact detection](@entry_id:1122952) to force calculation and time integration. We will then explore its vast utility in **Applications and Interdisciplinary Connections**, showcasing how DEM is used to solve real-world problems in geophysics, materials science, and biomechanics. Finally, the **Hands-On Practices** section will offer practical exercises to solidify your understanding of key computational concepts, empowering you to apply these powerful techniques in your own research and practice.

## Principles and Mechanisms

The Discrete Element Method (DEM) is a powerful computational framework for simulating the motion and interaction of a large number of discrete particles. While the introductory chapter has outlined the broad context and applications of DEM, this chapter delves into the fundamental principles and mechanisms that constitute the method's theoretical and algorithmic core. We will systematically dissect the computational cycle, explore the physical models that govern particle interactions, and discuss how the microscopic rules of DEM give rise to macroscopic, observable phenomena.

### The Algorithmic Core of DEM

At its heart, DEM simulates the collective behavior of a granular system by tracking the motion of each individual particle. This motion is governed by Newton's laws, where forces and torques arise from inter-particle contacts, external fields such as gravity, and interactions with boundaries. There are two canonical paradigms for implementing this principle, distinguished by how they handle particle contacts: the soft-sphere, time-driven method and the hard-sphere, event-driven method.

The **hard-sphere event-driven** approach treats particles as perfectly [rigid bodies](@entry_id:1131033) that cannot overlap. Their motion consists of periods of free flight, interrupted by instantaneous, binary collisions. The simulation proceeds by calculating the exact time of the next collision event in the entire system, advancing the simulation clock to that moment, resolving the collision by applying conservation laws (momentum and energy, the latter modified by a [coefficient of restitution](@entry_id:170710)), and then determining the next collision. This method is highly efficient for **dilute systems**, such as granular gases, where the [mean free time](@entry_id:194961) between collisions, $t_{\mathrm{mf}}$, is much larger than the physical duration of a contact, $t_c$. In this regime, the assumption of instantaneous, well-separated binary collisions ($t_c \ll t_{\mathrm{mf}}$) is a valid and computationally advantageous approximation. However, as the particle density or [packing fraction](@entry_id:156220), $\phi$, increases, the frequency of collisions rises dramatically, and the likelihood of nearly simultaneous, multi-particle interactions grows. This breaks the fundamental assumption of binary collisions, leading to both theoretical difficulties (e.g., inelastic collapse) and a catastrophic loss of computational efficiency, making the event-driven approach unsuitable for dense granular matter.

In contrast, the **soft-sphere time-driven** approach allows for a small, physically meaningful overlap between particles. This overlap, $\delta$, is not a numerical artifact but a representation of local [surface deformation](@entry_id:1132671). The [contact force](@entry_id:165079) is modeled as a continuous function of this overlap and the relative velocity of the contacting surfaces. The simulation progresses by integrating Newton's equations of motion for every particle forward in discrete time steps, $\Delta t$. At each step, contact forces are calculated for all overlapping particles, and these forces are used to update particle velocities and positions. This method inherently accommodates multiple, simultaneous, and enduring contacts, which are the defining features of **dense systems** ($\phi$ near [random close packing](@entry_id:143300)). In such systems, particles form persistent, force-transmitting networks, often called **[force chains](@entry_id:199587)**, and the concept of a "collision" is replaced by that of a finite-duration contact. The time-driven method is therefore the standard for simulating dense granular flows, static packings, and powders, where the contact duration $t_c$ is a significant physical timescale, often comparable to particle rearrangement times . The remainder of this chapter will focus on the principles and mechanisms of this widely used time-driven approach.

### The Time-Driven (Soft-Sphere) Method in Detail

The soft-sphere DEM operates on a computational cycle that is repeated for thousands or millions of time steps. This loop consists of three main stages: (1) detecting which particles are in contact, (2) calculating the forces and torques resulting from these contacts, and (3) integrating the equations of motion to update the state of each particle.

#### Contact Detection

A brute-force approach to [contact detection](@entry_id:1122952) would involve checking every particle against every other particle, a process with a computational complexity of $O(N^2)$, where $N$ is the number of particles. For simulations with many particles, this quadratic scaling is prohibitively expensive. To overcome this, a two-stage strategy is employed, dividing the task into a broad phase and a narrow phase.

The goal of the **broad-phase** is to quickly cull the vast majority of particle pairs that are too far apart to possibly be in contact. This is achieved using computationally cheap, approximate geometric tests. A common and effective broad-phase method is **spatial partitioning**, where the simulation domain is divided into a grid of cells. Each particle is mapped to the cell containing its center. To find potential contacts for a given particle, one only needs to check against other particles in its own cell and in the immediately adjacent cells. For a cubic grid, this constitutes a search over a $3 \times 3 \times 3$ block of 27 cells. For this method to be guaranteed to find all contacts between spherical particles, the cell side length, $s$, must be greater than or equal to the diameter of the largest particle, $2r_{\max}$. This ensures that the centers of any two contacting spheres must lie in cells that are, at most, immediate neighbors. Under the assumption of a homogeneous particle distribution at a fixed [volume fraction](@entry_id:756566), the number of particles to check against for any given particle becomes a constant independent of the total number of particles $N$. This reduces the [average-case complexity](@entry_id:266082) of the broad-phase to $O(N)$.

Once the broad-phase has generated a much smaller list of candidate pairs, the **narrow-phase** performs a precise geometric test on each pair to determine if they are actually in contact. For the candidate pairs that are in contact, the narrow-phase algorithm computes the exact geometric quantities required for force calculation, such as the overlap distance and the contact normal vector .

#### Force Calculation

After a contact between two particles has been identified, the interaction force and torque must be computed. This requires a precise description of the [contact kinematics](@entry_id:165205) and a constitutive model for the contact forces.

##### Kinematics of Contact

Consider two spherical particles, $i$ and $j$, with radii $R_i$ and $R_j$, positions $\mathbf{x}_i$ and $\mathbf{x}_j$, translational velocities $\mathbf{v}_i$ and $\mathbf{v}_j$, and angular velocities $\boldsymbol{\omega}_i$ and $\boldsymbol{\omega}_j$. The fundamental kinematic quantities describing their contact are:

1.  **The center-to-center vector** $\mathbf{d}_{ij} = \mathbf{x}_j - \mathbf{x}_i$, and the corresponding distance $d = \|\mathbf{d}_{ij}\|$.
2.  **The contact [unit normal vector](@entry_id:178851)**, which by convention points from particle $i$ to particle $j$: $\mathbf{n} = \frac{\mathbf{x}_j - \mathbf{x}_i}{\|\mathbf{x}_j - \mathbf{x}_i\|}$.
3.  **The normal overlap**, $\delta$, which is the amount of interpenetration. It is defined as a non-negative quantity:
    $$
    \delta = \max(0, R_i + R_j - d)
    $$
    A non-zero $\delta$ signifies a contact.

4.  **The [relative velocity](@entry_id:178060) at the contact point**, $\mathbf{v}_c$. This is not simply the difference in the particles' center-of-mass velocities, as it must account for the surface velocity due to rotation. The velocity of the contact point on particle $i$ is $\mathbf{v}_i^c = \mathbf{v}_i + \boldsymbol{\omega}_i \times (R_i \mathbf{n})$, and on particle $j$ is $\mathbf{v}_j^c = \mathbf{v}_j + \boldsymbol{\omega}_j \times (-R_j \mathbf{n})$. The relative velocity of particle $j$'s surface with respect to particle $i$'s surface at the contact point is therefore:
    $$
    \mathbf{v}_c = \mathbf{v}_j^c - \mathbf{v}_i^c = (\mathbf{v}_j - \mathbf{v}_i) - (R_i \boldsymbol{\omega}_i + R_j \boldsymbol{\omega}_j) \times \mathbf{n}
    $$
    This [relative velocity](@entry_id:178060) vector is then decomposed into a normal component, $\mathbf{v}_n = (\mathbf{v}_c \cdot \mathbf{n})\mathbf{n}$, and a tangential component, $\mathbf{v}_t = \mathbf{v}_c - \mathbf{v}_n$. These quantities, $\delta$, $\mathbf{v}_n$, and $\mathbf{v}_t$, serve as the inputs to the force models .

##### Normal Force Models

The [normal force](@entry_id:174233), $\mathbf{F}_n$, acts along the line of centers to resist compression and dissipate energy. Its magnitude $F_n$ is a function of the normal overlap $\delta$ and the normal [relative velocity](@entry_id:178060) $v_n = \mathbf{v}_c \cdot \mathbf{n}$.

A widely used and computationally simple model is the **linear spring-dashpot model**:
$$
F_n = k_n \delta + \gamma_n v_n
$$
Here, $k_n$ is a normal stiffness coefficient (the "spring") that generates a repulsive force proportional to overlap, and $\gamma_n$ is a [damping coefficient](@entry_id:163719) (the "dashpot") that generates a dissipative force proportional to the relative normal velocity. While computationally efficient, this model is an approximation. The stiffness of a real contact is not constant.

For more physically realistic simulations of elastic particles, the **Hertz model** is employed. Derived from [contact mechanics](@entry_id:177379), this model assumes frictionless, non-adhesive, [elastic contact](@entry_id:201366) between smooth spheres at small strains. It predicts a non-linear relationship between force and overlap:
$$
F_n = \frac{4}{3} E^* \sqrt{R^*} \delta^{3/2}
$$
The parameters $E^*$ and $R^*$ are the effective Young's modulus and effective radius of the contacting pair, defined as:
$$
\frac{1}{E^*} = \frac{1 - \nu_1^2}{E_1} + \frac{1 - \nu_2^2}{E_2} \quad \text{and} \quad \frac{1}{R^*} = \frac{1}{R_1} + \frac{1}{R_2}
$$
where $E_{1,2}$ and $\nu_{1,2}$ are the Young's moduli and Poisson's ratios of the two particles. For two [identical particles](@entry_id:153194), these reduce to $E^* = E / [2(1-\nu^2)]$ and $R^* = R/2$. The Hertz model correctly captures the stiffening of the contact as overlap increases, a result of the growing contact area. It is, however, purely elastic, meaning it conserves energy and corresponds to a [coefficient of restitution](@entry_id:170710) of 1. To model [inelastic collisions](@entry_id:137360), the Hertz model must be augmented with a dissipative (damping) term .

For cohesive materials where attractive surface forces are significant, the contact model must be further extended. Two classic models for adhesive contact are the **Johnson-Kendall-Roberts (JKR)** model and the **Derjaguin-Muller-Toporov (DMT)** model. The choice between them depends on the balance between [elastic deformation](@entry_id:161971) and [surface adhesion](@entry_id:201783), quantified by the dimensionless **Tabor parameter**, $\mu$:
$$
\mu = \left( \frac{R (\Delta\gamma)^2}{(E^*)^2 z_0^3} \right)^{1/3}
$$
where $\Delta\gamma$ is the [work of adhesion](@entry_id:181907) and $z_0$ is the characteristic range of [surface forces](@entry_id:188034).

*   The **JKR model** is applicable for large, compliant, "sticky" particles, where $\mu$ is large (e.g., $\mu \gtrsim 5$). In this limit, elastic deformation is significant, and adhesion is modeled as cohesive stresses acting *within* an enlarged contact area.
*   The **DMT model** is applicable for small, stiff particles with weaker adhesion, where $\mu$ is small (e.g., $\mu \lesssim 0.1$). Here, elastic deformation is minimal, and adhesion is modeled as a long-range attractive force acting *outside* the unmodified Hertzian contact area.
*   For intermediate values of $\mu$, the system is in a transition regime requiring more complex models .

##### Tangential Force Models

The tangential force, $\mathbf{F}_t$, which arises from the tangential component of the [relative velocity](@entry_id:178060), $\mathbf{v}_t$, is responsible for friction. It is typically modeled using a tangential spring to represent elastic [shear deformation](@entry_id:170920), combined with a slider element. The tangential force builds up elastically until it reaches a limit defined by a friction law, most commonly the Coulomb friction law, $| \mathbf{F}_t | \le \mu_f F_n$, where $\mu_f$ is the [coefficient of static friction](@entry_id:163255). Once this limit is reached, the surfaces begin to slide. This tangential force, acting at a distance from the particle's center, also produces a torque that induces rotation.

#### Integration of Motion

With all forces and torques computed, the final step in the computational cycle is to integrate the equations of motion forward in time.

##### Equations of Motion and Orientation

For each particle $i$, the translational and rotational dynamics are governed by the Newton-Euler equations:
$$
m_i \frac{d\mathbf{v}_i}{dt} = \sum_j \mathbf{F}_{ij}^{\text{contact}} + \mathbf{F}_i^{\text{body}}
$$
$$
\mathbf{I}_i \frac{d\boldsymbol{\omega}_i}{dt} + \boldsymbol{\omega}_i \times (\mathbf{I}_i \boldsymbol{\omega}_i) = \sum_j \mathbf{T}_{ij}^{\text{contact}}
$$
where $\mathbf{I}_i$ is the [moment of inertia tensor](@entry_id:148659), and the sums are over all contacts and body forces (like gravity).

While integrating position and velocity is straightforward, integrating orientation presents a challenge. A common three-parameter representation, **Euler angles**, suffers from a problem known as **gimbal lock**. At certain orientations (e.g., a pitch angle of $\pm 90^\circ$), two of the three rotational axes align, leading to a loss of a degree of freedom and numerical singularities.

To avoid this, modern DEM codes almost universally use **[unit quaternions](@entry_id:204470)**. A unit quaternion $\mathbf{q} = (q_0, q_1, q_2, q_3)$ is a 4-component vector with $\|\mathbf{q}\|=1$ that provides a global, singularity-free representation of orientation. The orientation is updated by integrating the kinematic equation relating the time derivative of the [quaternion](@entry_id:1130460) to the body's angular velocity $\boldsymbol{\omega}$ (expressed in the body frame):
$$
\dot{\mathbf{q}} = \frac{1}{2} \mathbf{q} \otimes \boldsymbol{\omega}^{\text{quat}}
$$
where $\boldsymbol{\omega}^{\text{quat}} = (0, \omega_x, \omega_y, \omega_z)$ and $\otimes$ denotes [quaternion multiplication](@entry_id:154753). While the exact continuous-time dynamics preserve the unit norm of $\mathbf{q}$, [numerical integration](@entry_id:142553) schemes (like Euler or Runge-Kutta) introduce [discretization errors](@entry_id:748522) that cause the norm to drift. Therefore, it is essential in practice to periodically re-normalize the [quaternion](@entry_id:1130460) ($\mathbf{q} \leftarrow \mathbf{q}/\|\mathbf{q}\|$) to prevent the accumulation of error. A key advantage of this approach is that a normalized quaternion can be used to reconstruct a perfectly orthonormal rotation matrix at each step, preventing spurious deformations that can arise from numerical error when updating a rotation matrix directly .

##### Time Integration and Stability

The soft-sphere DEM typically employs an **[explicit time integration](@entry_id:165797) scheme**, such as the velocity Verlet or [central difference method](@entry_id:163679). These schemes are computationally efficient as they do not require solving a large system of equations at each time step. However, their numerical stability is conditional. The time step, $\Delta t$, must be small enough to resolve the fastest dynamics in the system.

The fastest dynamics correspond to the oscillation of the stiffest contact between the lightest particles. A contact can be approximated as a linear spring-mass-damper system. The stability analysis of the [central difference scheme](@entry_id:747203) for an undamped oscillator with stiffness $k$ and effective mass $m_{\text{eff}}$ reveals that the numerical solution will become unstable if the time step is too large. The stability limit defines a **[critical time step](@entry_id:178088)**, $\Delta t_{\text{crit}}$:
$$
\Delta t_{\text{crit}} = \frac{2}{\omega_{\max}}
$$
Here, $\omega_{\max}$ is the highest natural frequency present in the entire system, determined by searching over all active contacts:
$$
\omega_{\max} = \max_{(i,j)} \left\{ \sqrt{\frac{k_n^{(ij)}}{m_{\text{eff}}^{(ij)}}}, \sqrt{\frac{k_t^{(ij)}}{m_{\text{eff}}^{(ij)}}} \right\}
$$
where $k_n$ and $k_t$ are the normal and tangential stiffnesses. In practice, a DEM simulation must use a time step that is a fraction (e.g., 20-30%) of this critical value to ensure both stability and accuracy. This stability constraint is a fundamental aspect of time-driven DEM, as it links the numerical parameter $\Delta t$ to the physical parameters of the particles (mass) and their interactions (stiffness) .

### Modeling Physical Complexity

While spherical particles are computationally convenient, many real-world [granular materials](@entry_id:750005) consist of non-spherical grains. Particle shape significantly influences packing, friction, and flow behavior. DEM can be extended to model non-spherical particles using several approaches.

*   **Clumps of Spheres (Multi-sphere Method):** A non-spherical particle is approximated as a rigid composite body formed by the union of several overlapping spheres. Contact detection between two clumps reduces to a series of sphere-sphere checks. This method is versatile, as it can represent complex and even concave shapes. However, the resulting surface is not smooth but consists of spherical patches, with non-differentiable "creases" at the junctions, which can introduce artifacts into the contact mechanics.

*   **Analytically Defined Shapes:** Some shapes can be described by a single mathematical formula. **Superquadrics** (or superellipsoids) are a family of shapes defined by an implicit equation that can represent forms from ellipsoidal to box-like, depending on shape exponents. For exponents greater than 2, the surface is smooth ($C^2$ [almost everywhere](@entry_id:146631)), which is advantageous for certain advanced numerical methods. **Spheropolyhedra**, formed by the Minkowski sum of a polyhedron and a sphere, have a $C^1$ smooth surface composed of planar, cylindrical, and spherical patches. These analytical shapes offer a good balance between geometric fidelity and computational efficiency for [contact detection](@entry_id:1122952).

*   **Rigid Polyhedra:** For applications where sharp edges and flat faces are critical, particles can be modeled directly as [polyhedra](@entry_id:637910). Contact detection for convex [polyhedra](@entry_id:637910) is often handled by algorithms like the Separating Axis Theorem (SAT) or the Gilbert-Johnson-Keerthi (GJK) algorithm. Unlike the other methods, the surface normals of [polyhedra](@entry_id:637910) are discontinuous at edges and vertices, which requires special care in the contact models. Representing concave [polyhedra](@entry_id:637910) typically involves decomposing them into a set of convex [polyhedra](@entry_id:637910) .

### From Micro-Mechanics to Macro-Phenomena

A primary goal of DEM is to predict macroscopic, continuum-level behavior from the underlying particle-scale physics. This involves a process of homogenization or volume-averaging.

#### Homogenization and the Stress Tensor

The **macroscopic Cauchy stress tensor**, $\boldsymbol{\sigma}$, is a key continuum quantity that represents the [internal forces](@entry_id:167605) within the granular assembly. It is computed by averaging the momentum flux over a representative volume $V$. For a granular system, the stress tensor has two contributions:
$$
\boldsymbol{\sigma} = \boldsymbol{\sigma}^c + \boldsymbol{\sigma}^k
$$
The **contact stress**, $\boldsymbol{\sigma}^c$, arises from the forces transmitted through the network of inter-particle contacts. It is given by the Love-Weber formula:
$$
\boldsymbol{\sigma}^c = \frac{1}{V} \sum_{c} \mathbf{f}_c \otimes \mathbf{d}_c
$$
where the sum is over all contacts $c$ in the volume, $\mathbf{f}_c$ is the [contact force](@entry_id:165079), and $\mathbf{d}_c$ is the branch vector connecting the centers of the two particles. The **kinetic stress**, $\boldsymbol{\sigma}^k$, arises from the transport of momentum by particles moving with fluctuating velocities $(\mathbf{v}_p - \langle\mathbf{v}\rangle)$ relative to the mean flow. In dense, slow flows, the contact stress dominates, while in rapid, dilute flows, the kinetic term becomes significant.

The structure of the contact network, which bears the stress, can be quantified by the **[fabric tensor](@entry_id:181734)**, $\mathbf{F}$. It is defined as the average of the [dyadic product](@entry_id:748716) of contact normal vectors:
$$
\mathbf{F} = \frac{1}{N_c} \sum_{c=1}^{N_c} \mathbf{n}_c \otimes \mathbf{n}_c
$$
where $N_c$ is the number of contacts. The trace of $\mathbf{F}$ is always 1, and for a perfectly [isotropic material](@entry_id:204616), $\mathbf{F} = \frac{1}{3}\mathbf{I}$, where $\mathbf{I}$ is the identity tensor. Deviations from this isotropic state indicate a preferential alignment of contacts, known as **structural anisotropy**. In many loading scenarios, the [principal directions](@entry_id:276187) of the stress tensor $\boldsymbol{\sigma}$ align with the [principal directions](@entry_id:276187) of the [fabric tensor](@entry_id:181734) $\mathbf{F}$, indicating that the material develops structural anisotropy to support applied loads. Indeed, the deviatoric (shear) part of the stress tensor is fundamentally linked to the anisotropy of the fabric and the force network .

#### Constitutive Behavior and Rheology

By simulating a granular assembly under controlled conditions (e.g., shear), DEM can be used as a "virtual laboratory" to derive macroscopic constitutive laws that relate stress to deformation. A landmark success in this area is the development of the **$\mu(I)$ rheology** for dense, dry granular flows.

This framework posits that for steady, homogeneous flows, the macroscopic friction coefficient, $\mu = \tau/P$ (the ratio of shear stress to pressure), is a function of a single dimensionless parameter, the **[inertial number](@entry_id:750626)**, $I$:
$$
I = \dot{\gamma} d \sqrt{\frac{\rho_p}{P}}
$$
where $\dot{\gamma}$ is the shear rate, $d$ is the particle diameter, and $\rho_p$ is the material density. The [inertial number](@entry_id:750626) represents the ratio of two timescales: a microscopic rearrangement time, $t_{\text{micro}} \sim d\sqrt{\rho_p/P}$, set by the confining pressure, and a macroscopic deformation time, $t_{\text{macro}} \sim 1/\dot{\gamma}$. A common empirical form for the [rheology](@entry_id:138671), observed in both simulations and experiments, is:
$$
\mu(I) = \mu_s + \frac{\Delta \mu}{1 + I_0/I}
$$
This law states that the friction coefficient increases monotonically from a quasi-static value $\mu_s$ (as $I \to 0$) to a higher asymptotic value $\mu_s + \Delta \mu$ in the rapid flow limit ($I \to \infty$). DEM simulations have been instrumental in establishing and parameterizing this powerful [constitutive model](@entry_id:747751), which connects microscopic particle properties directly to macroscopic flow behavior .

### Ensuring Model Fidelity: Verification and Validation

A DEM simulation is a complex piece of software implementing a mathematical model of a physical system. To ensure that its results are trustworthy, it must undergo rigorous **verification** and **validation**. These two activities are distinct and essential.

**Verification** addresses the question: "Are we solving the equations correctly?" It is the process of confirming that the code accurately solves the chosen mathematical model. Verification tests do not involve comparison to real-world experiments. Instead, they focus on numerical accuracy and correctness. Appropriate verification tests for DEM include:
*   Comparing simulation results for simple, analytically solvable problems. Examples include a single particle in free-fall , or a head-on collision of two particles with a linear contact law, whose motion is equivalent to a [damped harmonic oscillator](@entry_id:276848) .
*   Performing convergence studies, where the numerical error between the simulated result and an analytical solution is shown to decrease at the theoretically expected rate as the time step $\Delta t$ is refined .
*   Checking the conservation of fundamental quantities that should be preserved by the mathematical model, such as the total energy of a system with purely elastic contacts and no external work, or the total momentum of an isolated system .

**Validation** addresses the question: "Are we solving the right equations?" It is the process of assessing how well the chosen model (the equations and their parameters) represents the actual physical system. Validation requires comparing simulation outputs to data from laboratory experiments. Appropriate validation tests for DEM involve comparing emergent, macroscopic phenomena that are not direct inputs to the model:
*   Comparing the simulated [angle of repose](@entry_id:175944) of a granular pile to the experimentally measured value for the same material .
*   Simulating the compaction or vibration of a particle assembly and comparing the final [packing fraction](@entry_id:156220) to experimental results, such as the [random close packing](@entry_id:143300) limit of $\phi \approx 0.64$ for monodisperse spheres .
*   Comparing simulated rheological data, such as the scaling of shear stress with shear rate in a chute flow, to established experimental laws like Bagnold scaling .

Only a model that has been both verified and validated can be used with confidence for scientific prediction and engineering design.