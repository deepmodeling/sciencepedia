## Introduction
In the quest for [fusion energy](@entry_id:160137), understanding and controlling the transport of particles within a tokamak is paramount. A long-standing observation in these devices is the tendency for plasma density to peak at the core, even when particle fueling occurs at the edge. This points to the existence of an inward "pinch" mechanism that actively transports particles against their density gradient. The Ware pinch, a cornerstone of [neoclassical transport](@entry_id:188243) theory, provides a powerful explanation for this phenomenon, revealing a subtle yet profound consequence of a tokamak's fundamental design. It addresses the key knowledge gap of how a toroidal electric field, primarily intended to drive the plasma current, can simultaneously induce a significant radial [particle flux](@entry_id:753207).

This article provides a graduate-level exploration of the Ware pinch, bridging fundamental theory with practical implications. Over the following chapters, you will gain a deep understanding of this crucial transport mechanism.
- The **Principles and Mechanisms** chapter will deconstruct the physics from first principles. We will start with the conservation of canonical toroidal momentum in an axisymmetric system and show how the interplay between the toroidal electric field and [trapped particle](@entry_id:756144) orbits gives rise to a secular inward drift.
- The **Applications and Interdisciplinary Connections** chapter explores the real-world consequences. We will examine how the Ware pinch shapes density profiles, drives impurity accumulation, competes with [turbulent transport](@entry_id:150198), and how its existence is fundamentally tied to the [magnetic symmetry](@entry_id:186579) that distinguishes tokamaks from stellarators.
- Finally, the **Hands-On Practices** section will allow you to solidify your understanding by working through problems that connect the theoretical concepts to [quantitative analysis](@entry_id:149547) of plasma behavior.

## Principles and Mechanisms

This chapter elucidates the fundamental principles and mechanisms governing the neoclassical inward [particle flux](@entry_id:753207) known as the **Ware pinch**. We will begin by establishing the foundational concept of canonical toroidal momentum in an axisymmetric system, then explore how a toroidal electric field interacts with different particle populations to produce a secular inward drift. Finally, we will situate this phenomenon within the broader context of [neoclassical transport](@entry_id:188243) theory, defining its regimes of validity and contrasting it with other transport mechanisms.

### Canonical Toroidal Momentum in Axisymmetric Systems

The dynamics of a charged particle in a [magnetic confinement](@entry_id:161852) device are profoundly influenced by the symmetries of the magnetic field. In a tokamak, the assumption of toroidal axisymmetry—invariance under rotation about the central axis of the torus—is a powerful simplifying principle that gives rise to a fundamental constant of motion.

To identify this constant, we turn to the Lagrangian formulation of mechanics. The Lagrangian $L$ for a particle of mass $m$ and charge $q$ moving in an electromagnetic field described by a [vector potential](@entry_id:153642) $\mathbf{A}$ and a scalar potential $\Phi_E$ is given in SI units by:
$L = \frac{1}{2} m v^2 + q\,\mathbf{A}\cdot\mathbf{v} - q\,\Phi_E$

In the [cylindrical coordinate system](@entry_id:266798) $(R, \phi, Z)$ natural to a tokamak, the toroidal angle $\phi$ is the coordinate corresponding to the toroidal symmetry. When the system is axisymmetric, the Lagrangian $L$ has no explicit dependence on $\phi$. Such a coordinate is termed **cyclic** or **ignorable**, and by Noether's theorem, its corresponding [canonical momentum](@entry_id:155151) is a conserved quantity. The [canonical momentum](@entry_id:155151) conjugate to the toroidal angle $\phi$, denoted $P_\phi$, is defined as:
$P_\phi = \frac{\partial L}{\partial \dot{\phi}}$

Executing this differentiation on the Lagrangian yields:
$P_\phi = m R^2 \dot{\phi} + q R A_\phi = m R v_\phi + q R A_\phi$
where $v_\phi = R\dot{\phi}$ is the particle's toroidal velocity component and $A_\phi$ is the toroidal component of the vector potential $\mathbf{A}$. This expression reveals that the **canonical toroidal momentum** $P_\phi$ is composed of two parts: a mechanical momentum term, $m R v_\phi$, and an [electromagnetic momentum](@entry_id:268129) term, $q R A_\phi$.

A crucial step is to relate the [vector potential](@entry_id:153642) to a more physically intuitive quantity. The magnetic flux functions are central to this task. In an axisymmetric [tokamak](@entry_id:160432), two primary flux functions are defined: the toroidal flux $\Phi$, which is the magnetic flux passing through the poloidal cross-section of a magnetic surface, and the [poloidal flux](@entry_id:753562) $\Psi_p$, which is the flux passing through the "hole" of the torus, bounded by a given magnetic surface. Via Stokes' theorem, the [poloidal flux](@entry_id:753562) $\Psi_p$ is related to the line integral of $\mathbf{A}$ around a toroidal loop: $\Psi_p = \oint \mathbf{A} \cdot d\mathbf{l} = 2\pi R A_\phi$. It is conventional to work with the [poloidal flux](@entry_id:753562) per radian, denoted $\psi$, where $\psi = \Psi_p / (2\pi) = R A_\phi$. It is this **[poloidal flux](@entry_id:753562) function** $\psi$, not the toroidal flux $\Phi$, which appears in the expression for $P_\phi$.  This is a direct consequence of $\phi$ being the ignorable coordinate, which singles out the conjugate component of the vector potential, $A_\phi$. 

Thus, the canonical toroidal momentum is given by:
$P_\phi = m R v_\phi + q \psi$

In a perfectly axisymmetric system free of external toroidal forces or collisions, $P_\phi$ is an exact constant of the particle's motion. This conservation law is the bedrock upon which the mechanism of the Ware pinch is built.

### The Toroidal Electric Field as a Driver of Radial Transport

In a [tokamak](@entry_id:160432), a steady [plasma current](@entry_id:182365) is typically driven by a toroidal electric field, $E_\phi$, which is induced by a central transformer (or [solenoid](@entry_id:261182)). This electric field is related to the **loop voltage**, $V_{\text{loop}}$, the [electromotive force](@entry_id:203175) around a complete toroidal circuit. For a circular path at the major radius $R$, this relationship is approximately:
$E_\phi \approx \frac{V_{\text{loop}}}{2\pi R}$

The presence of this toroidal electric field introduces a non-conservative toroidal force, $F_\phi = q E_\phi$, which breaks the exact conservation of $P_\phi$. The equation of motion for the canonical toroidal momentum becomes:
$\frac{d P_\phi}{dt} = q R E_\phi$

This simple but powerful equation dictates that the canonical momentum of any charged particle must change secularly in time. By substituting the definition of $P_\phi$, we obtain the central equation for our analysis:
$\frac{d}{dt} (m R v_\phi + q \psi) = q R E_\phi$

At first glance, this equation appears to describe only the acceleration of particles in the toroidal direction. However, its implications are far more profound when we consider the distinct [orbital dynamics](@entry_id:161870) of trapped and passing particles in the [toroidal geometry](@entry_id:756056).

### The Emergence of the Ware Pinch from Bounce-Averaged Dynamics

The magnetic field in a tokamak is stronger on the inboard side ($R  R_0$) and weaker on the outboard side ($R > R_0$), varying approximately as $B \propto 1/R$. This magnetic well gives rise to two distinct particle populations:
- **Passing particles**, which have sufficient parallel velocity to overcome the [magnetic mirror](@entry_id:204158) force and circulate continuously around the torus.
- **Trapped particles**, which have low parallel velocity and are reflected by the strong magnetic field on the inboard side. Their trajectories, when projected onto the poloidal plane, trace out "banana" shapes confined to the outboard side of the torus.

A crucial difference between these populations lies in their response to the toroidal electric field. Passing particles are free to be accelerated by $E_\phi$, and it is their net motion that constitutes the plasma current. For [trapped particles](@entry_id:756145), the situation is different. Their parallel velocity reverses direction at each bounce point, and their average toroidal velocity over a complete bounce orbit is nearly zero.

This constraint on [trapped particles](@entry_id:756145) is the key to the Ware pinch. To analyze the slow, secular drift that occurs over many fast bounce oscillations, we employ the technique of **bounce-averaging**. We average the equation of motion for $P_\phi$ over one bounce period, $\tau_b$. For a [trapped particle](@entry_id:756144), the bounce-averaged rate of change of its mechanical momentum must be zero if it is to remain trapped: $\langle \frac{d}{dt}(m R v_\phi) \rangle_b \approx 0$. Applying this to our central equation gives: 

$q \left\langle \frac{d\psi}{dt} \right\rangle_b \approx q \langle R E_\phi \rangle_b$

Since $E_\phi$ and $R$ are approximately constant over a single [banana orbit](@entry_id:192144), this simplifies to:
$\left\langle \frac{d\psi}{dt} \right\rangle_b \approx R E_\phi$

The quantity $\frac{d\psi}{dt}$ represents the rate at which a particle's [guiding center](@entry_id:189730) crosses surfaces of constant [poloidal flux](@entry_id:753562), which is directly related to its [radial velocity](@entry_id:159824), $v_r$. The [poloidal magnetic field](@entry_id:753563), $B_p$, is defined by the gradient of the flux function: $|\nabla \psi| = R B_p$. Therefore, the rate of change of $\psi$ is $\frac{d\psi}{dt} = \mathbf{v} \cdot \nabla\psi = v_r |\nabla \psi| = v_r R B_p$. Taking the bounce average, we find $\langle \frac{d\psi}{dt} \rangle_b = \langle v_r R B_p \rangle_b \approx \langle v_r \rangle_b R B_p$.

Equating our two expressions for $\langle \frac{d\psi}{dt} \rangle_b$ yields the bounce-averaged [radial velocity](@entry_id:159824) of [trapped particles](@entry_id:756145):
$\langle v_r \rangle_b R B_p \approx R E_\phi$

This result needs to be treated with care regarding sign conventions. In a standard [tokamak](@entry_id:160432) configuration where the [plasma current](@entry_id:182365) and [toroidal field](@entry_id:194478) are positive, the [poloidal field](@entry_id:188655) $B_p$ is positive and is driven by a positive $E_\phi$. A flux surface label $\psi$ that increases with minor radius $r$ is a common convention. The inward direction corresponds to $v_r  0$. A rigorous derivation considering these conventions yields the definitive formula for the **Ware pinch velocity**:
$v_W = \langle v_r \rangle_b = -\frac{E_\phi}{B_p}$

This expression encapsulates the core features of the Ware pinch: 
1.  It is an **inward** drift (a pinch) for a standard current-driving electric field.
2.  The velocity is remarkably independent of the particle's mass and charge sign. Trapped ions and electrons are both pinched inward at the same speed.
3.  The velocity is inversely proportional to the [poloidal magnetic field](@entry_id:753563), $B_p$.

The physical intuition behind this result is that [trapped particles](@entry_id:756145), being confined to the outboard side where the major radius $R$ is larger, spend their entire bounce orbit in a region where the toroidal electric field exerts a torque.  Since they cannot undergo sustained toroidal acceleration and remain trapped, the system enforces the conservation of $P_\phi$ on a bounce-averaged timescale by forcing the particle's [guiding center](@entry_id:189730) to drift radially inward.

### The Ware Pinch in the Landscape of Plasma Transport

The Ware pinch is a quintessential **neoclassical** effect. It is not predicted by [classical transport theory](@entry_id:747370), which considers only binary collisions in a uniform magnetic field. The pinch is a direct consequence of particle orbits in the [toroidal geometry](@entry_id:756056) of the tokamak. Furthermore, it is a **convective** flux (a drift at a specific velocity) that arises in a quiescent, axisymmetric plasma, making it fundamentally different from transport driven by turbulent fluctuations. 

It is also crucial to distinguish the Ware pinch from the familiar $\mathbf{E} \times \mathbf{B}$ drift. The same toroidal electric field $E_\phi$ also generates an $\mathbf{E} \times \mathbf{B}$ drift, given by $\mathbf{v}_E = (\mathbf{E} \times \mathbf{B}) / B^2$. The radial component of this drift is $v_{E,r} = -E_\phi B_p / B^2$. A direct comparison reveals the profound difference: 

- **Target Population:** The Ware pinch is specific to **[trapped particles](@entry_id:756145)**, whereas the $\mathbf{E} \times \mathbf{B}$ drift acts on all charged particles, trapped and passing alike.
- **Magnitude:** The Ware pinch velocity scales as $v_W \propto 1/B_p$. The $\mathbf{E} \times \mathbf{B}$ drift scales as $v_{E,r} \propto B_p/B^2$. In a typical [tokamak](@entry_id:160432) where $B_p \ll B_\phi \approx B$, the ratio of the two velocities is approximately $|v_W / v_{E,r}| \approx (B/B_p)^2 \gg 1$. The Ware pinch is a much larger effect. This ratio is related to the [safety factor](@entry_id:156168) $q$ via $q \approx (r/R)(B_\phi/B_p)$, highlighting the strong influence of the magnetic geometry. 

The total inward [particle flux](@entry_id:753207) due to the Ware pinch is obtained by multiplying the pinch velocity by the density of [trapped particles](@entry_id:756145). Since the fraction of [trapped particles](@entry_id:756145), $f_t$, in a large-aspect-ratio [tokamak](@entry_id:160432) scales as $\sqrt{\epsilon}$ (where $\epsilon = r/R$ is the inverse aspect ratio), the net inward velocity for the entire plasma population scales as $|V_W| \sim (E_\phi/B_p)\sqrt{\epsilon}$. 

### Collisionality and the Regimes of Neoclassical Transport

The bounce-averaging procedure used to derive the Ware pinch velocity is only valid if a [trapped particle](@entry_id:756144) can complete many bounce orbits before a collision significantly alters its trajectory. This requirement introduces a crucial dependence on **collisionality**. Neoclassical theory is stratified into different regimes based on the relationship between the [collision time](@entry_id:261390) and the characteristic orbital times.

The validity of the bounce-averaged model rests on a clear hierarchy of timescales:
$\Omega^{-1} \ll \tau_b \ll \tau_c$

Here, $\Omega^{-1}$ is the [gyromotion](@entry_id:204632) timescale (inverse of the gyrofrequency), $\tau_b$ is the bounce time for a [trapped particle](@entry_id:756144), and $\tau_c$ is the characteristic [collision time](@entry_id:261390). The first inequality, $\Omega^{-1} \ll \tau_b$, allows for the use of the [guiding-center approximation](@entry_id:750090). The second, $\tau_b \ll \tau_c$, ensures that [banana orbits](@entry_id:202619) are well-defined and that bounce-averaging is a valid procedure. 

These relationships are systematized using the dimensionless **collisionality parameter**, $\nu_*$, which is the ratio of the effective collision frequency for detrapping a particle ($\nu_{eff} \sim \nu/\epsilon$) to the bounce frequency ($\omega_b \sim 1/\tau_b \sim v_{th}\sqrt{\epsilon}/(qR)$). This gives the scaling: 
$\nu_* \sim \frac{\nu q R}{\epsilon^{3/2} v_{th}}$

Based on the value of $\nu_*$, we define three primary neoclassical regimes: 
1.  **Banana Regime ($\nu_* \ll 1$):** This is the low-collisionality regime where $\tau_b \ll \tau_c$. Trapped particles complete many stable [banana orbits](@entry_id:202619). The Ware pinch mechanism is fully effective in this regime.
2.  **Plateau Regime ($\nu_* \sim 1$):** In this intermediate regime, the [collision frequency](@entry_id:138992) is comparable to the bounce frequency. The resonance between collisional and orbital effects leads to a distinct scaling of transport coefficients. The Ware pinch is still present, though its efficiency begins to decrease as collisionality increases.
3.  **Pfirsch-Schlüter Regime ($\nu_* \gg 1$):** This is the high-collisionality regime where collisions are so frequent that a particle cannot complete a bounce orbit ($\tau_c \ll \tau_b$). The distinction between trapped and passing particles is lost, and the plasma behaves more like a collisional fluid. The mechanism for the Ware pinch is suppressed, and transport is dominated by different fluid-like processes.

In a typical [tokamak](@entry_id:160432) discharge, the core plasma, being hot and relatively low in density, resides in the [banana regime](@entry_id:746654). Moving toward the colder, denser plasma edge, the [collision frequency](@entry_id:138992) rises dramatically. As a result, the outer regions of the plasma typically transition through the [plateau regime](@entry_id:753520) into the highly collisional Pfirsch-Schlüter regime. Consequently, while the Ware pinch can be a significant factor in shaping the density profile in the plasma core, its direct influence diminishes towards the edge where the condition $\tau_b \ll \tau_c$ is violated.  This transition underscores the importance of understanding the local plasma parameters to correctly model [transport phenomena](@entry_id:147655) across the entire plasma radius.