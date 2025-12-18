## Introduction
In the quest for fusion energy, controlling the transport of particles and energy within a tokamak is of paramount importance. While turbulent transport often dominates headlines, a more [fundamental class](@entry_id:158335) of transport mechanisms, known as neoclassical transport, arises from the complex particle orbits in the toroidal magnetic geometry. One of the most significant and counterintuitive of these is the Ware pinch—an inward particle flux driven by the very toroidal electric field used to sustain the plasma current. This phenomenon presents a critical challenge, as it can lead to the undesirable accumulation of impurities in the plasma core, but it also provides a key to understanding and shaping the [plasma density profile](@entry_id:193964).

This article provides a systematic exploration of [inductive transport](@entry_id:1126465) and the Ware pinch. It bridges the gap between the foundational principles of classical mechanics and their practical consequences in high-performance fusion plasmas. Across three chapters, you will gain a multi-faceted understanding of this crucial transport mechanism. The journey begins in **Principles and Mechanisms**, where we will deconstruct the physics from first principles, deriving the pinch velocity from the conservation of [canonical toroidal momentum](@entry_id:1122015) and examining the distinct roles of trapped and passing particles. Next, **Applications and Interdisciplinary Connections** will broaden our perspective, illustrating how the Ware pinch influences density profiles, [impurity accumulation](@entry_id:1126432), dynamic MHD events, and the design of future fusion reactors. Finally, **Hands-On Practices** will offer a chance to apply this theoretical knowledge through targeted computational exercises, reinforcing the connection between theory and predictive modeling.

## Principles and Mechanisms

The existence of an inductive toroidal electric field, a necessary component for driving and sustaining the plasma current in a tokamak, has a profound and somewhat counterintuitive consequence on particle transport. Beyond simply accelerating charged particles along the magnetic field lines, this toroidal electric field, in concert with the specific geometry of the toroidal magnetic field, gives rise to a net radial [particle flux](@entry_id:753207). This phenomenon, known as the **Ware pinch**, is a convective, inward-directed transport mechanism that affects a specific sub-population of particles. It is a cornerstone of **[neoclassical transport theory](@entry_id:1128497)**, which describes particle and [energy transport](@entry_id:183081) in toroidal systems arising from particle-orbit effects and collisions, distinct from transport driven by micro-instabilities. This chapter will systematically deconstruct the principles and mechanisms governing this [inductive transport](@entry_id:1126465) phenomenon.

### The Conservation of Canonical Toroidal Momentum

The foundational principle underlying the Ware pinch is the conservation of [canonical toroidal momentum](@entry_id:1122015) in an axisymmetric system. To understand this, we begin with the Lagrangian, $L$, for a single particle of mass $m$ and charge $q$ moving in an electromagnetic field described by a scalar potential $\Phi$ and a vector potential $\mathbf{A}$:

$$
L = \frac{1}{2}m v^2 + q\mathbf{A} \cdot \mathbf{v} - q\Phi
$$

In a toroidally axisymmetric system like a tokamak, it is natural to use a [cylindrical coordinate system](@entry_id:266798) $(R, \phi, Z)$, where $\phi$ is the toroidal angle. Due to axisymmetry, the magnetic and electric fields, and thus their potentials, are independent of $\phi$. This makes $\phi$ an **ignorable coordinate** in the Lagrangian formulation of mechanics. A fundamental theorem of classical mechanics states that the canonical momentum conjugate to an ignorable coordinate is a conserved quantity.

The canonical momentum conjugate to the toroidal angle $\phi$, denoted $P_\phi$, is given by:

$$
P_\phi = \frac{\partial L}{\partial \dot{\phi}}
$$

Expressing the Lagrangian in [cylindrical coordinates](@entry_id:271645) and performing the differentiation yields:

$$
P_\phi = m R^2 \dot{\phi} + q R A_\phi
$$

Here, $A_\phi$ is the toroidal component of the [magnetic vector potential](@entry_id:141246). The term $R\dot{\phi}$ is simply the particle's toroidal velocity, $v_\phi$. The first term, $m R v_\phi$, is the familiar **mechanical angular momentum** of the particle about the Z-axis. The second term, $q R A_\phi$, is the **[electromagnetic momentum](@entry_id:268129)** contribution from the particle's interaction with the magnetic field.

In an axisymmetric tokamak, it is convenient to relate the [vector potential](@entry_id:153642) to a more physically intuitive quantity: the **[poloidal magnetic flux](@entry_id:1129914)**, $\psi$. The poloidal flux per radian, $\psi$, is defined such that it serves as a flux surface label and satisfies the relation $\psi = R A_\phi$. This allows us to express the [canonical toroidal momentum](@entry_id:1122015) in a more transparent form :

$$
P_\phi = m R v_\phi + q \psi
$$

Since $\phi$ is an ignorable coordinate, the Euler-Lagrange equation for this coordinate is simply:

$$
\frac{d P_\phi}{dt} = \frac{\partial L}{\partial \phi} = 0
$$

This equation states that the [canonical toroidal momentum](@entry_id:1122015) of a charged particle is an exact constant of motion in a collisionless, perfectly axisymmetric system. This conservation law holds true even if the fields are changing slowly in time, such as in the presence of an inductive toroidal electric field, as long as axisymmetry (i.e., independence from $\phi$) is maintained. It is this powerful constraint that orchestrates the radial [pinch effect](@entry_id:267341) .

### The Role of Trapped Particles

The conservation of $P_\phi$ has dramatically different implications for the two distinct populations of particles in a tokamak: **passing particles** and **trapped particles**. This distinction arises from the [toroidal geometry](@entry_id:756056) itself. The magnetic field strength in a tokamak is not uniform, varying approximately as the inverse of the major radius, $B \propto 1/R$. The field is weaker on the outboard side (large $R$) and stronger on the inboard side (small $R$).

Particles with sufficient velocity parallel to the magnetic field can overcome this [magnetic mirror effect](@entry_id:171262) and circulate continuously around the torus; these are the passing particles. However, particles with low parallel velocity are reflected by the high-field region on the inboard side, confining their motion to the low-field, outboard side. These are the trapped particles, and their orbits, when projected onto a poloidal cross-section, trace a characteristic "banana" shape.

A crucial feature of a trapped particle's orbit is that its parallel velocity, and consequently its toroidal velocity $v_\phi$, reverses direction during each bounce. As a result, the **bounce-averaged toroidal velocity** of a [trapped particle](@entry_id:756144) is nearly zero: $\langle v_\phi \rangle_b \approx 0$. While there is a slow toroidal precession drift, the mechanical momentum associated with this motion is small.

In contrast, passing particles have a large, non-zero average toroidal velocity as they circulate around the torus. This distinction is the key to understanding why the inductive electric field drives a radial drift for trapped particles but primarily accelerates passing particles.

When an inductive toroidal electric field $E_\phi$ is applied, it exerts a toroidal force $qE_\phi$. For a **passing particle**, this force does work, leading to a continuous change in its toroidal velocity $v_\phi$. The change in mechanical momentum, $\frac{d}{dt}(m R v_\phi)$, is large and primarily balances the effect of the electric field within the constraint of $P_\phi$ conservation. Consequently, the particle's flux surface label, $\psi$, need not change significantly, and the particle experiences little to no net radial drift .

For a **trapped particle**, the situation is entirely different. Since its bounce-averaged mechanical momentum $\langle m R v_\phi \rangle_b$ is constrained to be small, it cannot simply accelerate toroidally to respond to the electric field. The conservation law, applied in a bounce-averaged sense, $\frac{d}{dt}\langle P_\phi \rangle = 0$, dictates that if the [electromagnetic fields](@entry_id:272866) are changing, something else must give way. The particle must drift radially, changing its flux surface $\psi$, to maintain the conservation of its canonical toroidal momentum .

The physical asymmetry that allows the uniform field $E_\phi$ to produce this net effect lies in the banana orbit itself. A trapped particle spends a disproportionately long time near its bounce points, which are on the outboard side of the torus where the magnetic field is weak and the major radius $R$ is large. The toroidal torque, $q R E_\phi$, is therefore applied more effectively on this outboard part of the orbit. To balance this net bounce-averaged torque and maintain the invariants of motion, the orbit center must shift radially inward, which manifests as a decrease in its flux label $\psi$ .

### Quantitative Derivation of the Ware Pinch Velocity

We can make this argument quantitative to derive an expression for the inward drift velocity. The derivation elegantly combines Faraday's law of induction with the conservation of canonical momentum.

First, Faraday's law applied to a toroidal loop at a major radius $R$ gives a relationship between the [loop voltage](@entry_id:1127453) and the rate of change of the total [poloidal magnetic flux](@entry_id:1129914) $\Psi_p = 2\pi\psi$.

$$
\oint \mathbf{E} \cdot d\mathbf{l} = E_\phi (2\pi R) = - \frac{d\Psi_p}{dt} = - \frac{d(2\pi\psi)}{dt}
$$

This relation connects the local toroidal electric field to the time rate of change of the [poloidal flux](@entry_id:753562) per radian:

$$
\frac{\partial \psi}{\partial t} = -R E_\phi
$$

Next, we consider the [total time derivative](@entry_id:172646) of $\psi$ as experienced by a guiding center moving with a radial velocity $V_r$:

$$
\frac{d\psi}{dt} = \frac{\partial\psi}{\partial t} + V_r \frac{\partial\psi}{\partial r}
$$

The radial gradient of the [poloidal flux](@entry_id:753562) is related to the [poloidal magnetic field](@entry_id:753563), $B_\theta$. Depending on the sign convention, one common form is $B_\theta \approx -\frac{1}{R}\frac{\partial\psi}{\partial r}$. Therefore, $\frac{\partial\psi}{\partial r} \approx -R B_\theta$.

The conservation of bounce-averaged [canonical momentum](@entry_id:155151) for a [trapped particle](@entry_id:756144), $\frac{d}{dt}\langle P_\phi \rangle = 0$, implies that the bounce-average of the [total time derivative](@entry_id:172646) of $\psi$ must be effectively zero, as the mechanical momentum term is negligible: $\langle \frac{d\psi}{dt} \rangle_b \approx 0$. Applying this to the expression for the [total derivative](@entry_id:137587):

$$
\left\langle \frac{\partial\psi}{\partial t} \right\rangle_b + \left\langle V_r \frac{\partial\psi}{\partial r} \right\rangle_b \approx 0
$$

Since the fields and geometric factors vary slowly over a single [banana orbit](@entry_id:192144), they can be treated as constants during the bounce-averaging process. The bounce-averaged [radial velocity](@entry_id:159824) is the Ware pinch velocity, $V_W = \langle V_r \rangle_b$. Substituting our relations for the partial derivatives of $\psi$:

$$
(-R E_\phi) + V_W (-R B_\theta) \approx 0
$$

Solving for $V_W$ yields the expression for the **Ware pinch velocity**:

$$
V_W = -\frac{E_\phi}{B_\theta}
$$

The sign of the velocity depends on the sign conventions chosen for the fields and fluxes. The negative sign here indicates that for a standard tokamak discharge (where $E_\phi$ and $B_\theta$ are positive), the drift is directed inward (negative radial velocity)  . This result is remarkable: the inward drift velocity depends only on the local values of the toroidal electric field and the [poloidal magnetic field](@entry_id:753563), and is independent of the particle's charge, mass, or energy.

As a concrete example, consider a tokamak with a loop voltage of $1.0\,\text{V}$ and a major radius of $3.0\,\text{m}$. The toroidal electric field is $E_\phi = V_{\text{loop}}/(2\pi R) \approx 0.053\,\text{V/m}$. If the [poloidal magnetic field](@entry_id:753563) at a minor radius of $0.5\,\text{m}$ is $B_\theta = 0.8\,\text{T}$ (corresponding to a plasma current of $2.0\,\text{MA}$), the Ware pinch speed is $|V_W| = |E_\phi/B_\theta| \approx 0.066\,\text{m/s}$. The characteristic time to pinch a particle across the entire minor radius of, say, $1.0\,\text{m}$ would be $\tau_W = a / |V_W| \approx 15.1\,\text{s}$ . This indicates that the Ware pinch is a relatively slow but persistent effect that can significantly influence the long-term particle [density profile](@entry_id:194142).

### Theoretical Context and Classification

To fully appreciate the Ware pinch, it is essential to place it within the broader framework of [plasma transport theory](@entry_id:188550).

#### Neoclassical Origin

The Ware pinch is a quintessential **neoclassical** effect. Classical transport theory considers [particle transport](@entry_id:1129401) due to collisions in a simple, straight magnetic field. Neoclassical theory extends this by incorporating the complex guiding-center orbits that arise in a toroidal magnetic geometry. The existence of trapped-particle [banana orbits](@entry_id:202619) is a purely geometrical effect. The Ware pinch arises directly from the interplay between these orbits and the inductive electric field. It is a fundamental transport mechanism in an idealized, quiescent, axisymmetric torus and does not require turbulence or other [microinstabilities](@entry_id:751966) to exist. Collisions play a secondary but crucial role: they scatter particles between the trapped and passing populations, allowing a steady-state inward flux to be established and preventing an unrealistic pile-up of particles at the plasma center .

#### Distinction from the E×B Drift

It is crucial to distinguish the Ware pinch from the more familiar $\mathbf{E}\times\mathbf{B}$ drift. Given a toroidal electric field $\mathbf{E} = E_\phi \hat{\boldsymbol{\phi}}$ and a poloidal magnetic field $\mathbf{B}_p = B_\theta \hat{\boldsymbol{\theta}}$, the $\mathbf{E}\times\mathbf{B}$ drift is directed radially:

$$
\mathbf{v}_E = \frac{\mathbf{E} \times \mathbf{B}_p}{B^2} = -\frac{E_\phi B_\theta}{B^2}\hat{\mathbf{r}}
$$

The Ware pinch velocity, $V_W \propto E_\phi/B_\theta$, has a different functional dependence and is typically much larger in magnitude. For typical tokamak parameters where $B_\phi \gg B_\theta$, the total field strength is $B \approx B_\phi$. Therefore, the ratio of the Ware pinch to the $\mathbf{E}\times\mathbf{B}$ drift is approximately:

$$
\frac{|V_W|}{|v_E|} = \frac{|E_\phi/B_\theta|}{|E_\phi B_\theta / B^2|} = \left(\frac{B}{B_\theta}\right)^2 \gg 1
$$

For instance, in a tokamak with a total field $B=5\,\text{T}$ and a [poloidal field](@entry_id:188655) $B_\theta=0.5\,\text{T}$, this ratio is $(5/0.5)^2 = 100$. This large difference underscores that the Ware pinch is not an $\mathbf{E}\times\mathbf{B}$ drift, but a distinct neoclassical phenomenon arising from the global constraint of canonical momentum conservation .

#### Kinetic Picture and Collisionality Dependence

From a kinetic theory perspective, the effect of the inductive electric field enters the [drift-kinetic equation](@entry_id:1123982) for the [particle distribution function](@entry_id:753202), $f$, through the energy change term. The rate of energy change is $\dot{\mathcal{E}} = q \mathbf{v} \cdot \mathbf{E} \approx q v_\parallel E_\phi$. This modifies the kinetic equation with a drive term of the form $q v_\parallel E_\phi (\partial f / \partial \mathcal{E})$, which ultimately gives rise to the pinch flux when the equation is solved for trapped particles .

The magnitude of the Ware pinch is also strongly dependent on the plasma's **collisionality**. Collisionality is characterized by the dimensionless parameter $\nu^*$, which is the ratio of the effective collision frequency to the particle bounce frequency. This parameter delineates three [neoclassical transport](@entry_id:188243) regimes:

1.  **Banana Regime** ($\nu^* \ll 1$): Collisions are infrequent. Trapped particles complete many bounce orbits before being scattered. Banana orbits are well-defined, and the Ware pinch mechanism is fully effective. The pinch velocity is at its maximum in this regime.

2.  **Plateau Regime** ($\nu^* \sim 1$): The [collision frequency](@entry_id:138992) is comparable to the bounce frequency. Collisions begin to disrupt [banana orbits](@entry_id:202619), reducing the effectiveness of the coherent motion required for the pinch.

3.  **Pfirsch-Schlüter Regime** ($\nu^* \gg 1$): Collisions are so frequent that the concept of a banana orbit is lost. A particle's trajectory is randomized before it can complete a bounce. This collisional decorrelation of the trapped-particle orbits causes the Ware pinch mechanism to become ineffective, and the pinch velocity vanishes.

Therefore, the Ware pinch is largest at low collisionality (the [banana regime](@entry_id:746654)) and monotonically decreases as collisionality increases, becoming negligible in the highly collisional Pfirsch-Schlüter regime . This dependence highlights its nature as an effect rooted in the specific, collisionless orbit topology of a toroidal magnetic field.