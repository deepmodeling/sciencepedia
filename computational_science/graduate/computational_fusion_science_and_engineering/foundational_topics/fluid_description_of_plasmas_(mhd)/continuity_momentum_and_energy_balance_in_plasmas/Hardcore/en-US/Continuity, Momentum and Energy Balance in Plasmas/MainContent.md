## Introduction
Plasma, the fourth state of matter, governs phenomena from laboratory fusion reactors to the vastness of interstellar space. Its complex behavior is underpinned by a set of universal rules: the conservation of particles, momentum, and energy. These fundamental balance equations form the language of plasma fluid dynamics, providing a tractable framework to analyze and predict how plasmas evolve, flow, and transport energy.

While a plasma is a collection of individual particles, describing it from a purely kinetic standpoint is often computationally intractable. This article addresses the critical step of transitioning from the microscopic particle description to the macroscopic fluid model, revealing both the power and the inherent approximations of this approach. The reader will embark on a journey from first principles to practical application. This structured approach will build a comprehensive understanding, starting with the theoretical foundation and practical use of these laws as laid out in the upcoming chapters: "Principles and Mechanisms," "Applications and Interdisciplinary Connections," and "Hands-On Practices."

## Principles and Mechanisms

The behavior of a plasma, whether in a laboratory fusion device or a distant star, is governed by fundamental conservation laws. These laws—for particles, momentum, and energy—form the bedrock of plasma physics. In this chapter, we will develop these balance equations from first principles, explore the physical mechanisms they represent, and understand the assumptions and approximations inherent in the fluid models commonly used to describe [plasma dynamics](@entry_id:185550).

### From Kinetic Theory to Fluid Models: The Moment Hierarchy

A plasma is a collection of charged particles whose dynamics are fully described by a [velocity distribution function](@entry_id:201683), $f_s(\mathbf{x}, \mathbf{v}, t)$, for each species $s$. This function evolves according to a kinetic equation, such as the Vlasov–Fokker–Planck equation. While this kinetic description is fundamental, solving it is often computationally prohibitive. A more tractable approach is to derive a set of fluid equations by taking [velocity moments](@entry_id:1133763) of the kinetic equation. This process generates a hierarchy of equations for macroscopic quantities.

The zeroth moment, obtained by integrating the kinetic equation over all velocities, yields the **continuity equation**, which governs the evolution of the [number density](@entry_id:268986) $n_s = \int f_s \, \mathrm{d}^3\mathbf{v}$. The first moment, weighted by momentum $m_s\mathbf{v}$, yields the **momentum balance equation**, which describes the evolution of the mean flow velocity $\mathbf{u}_s$. The second moment, weighted by energy $m_s v^2/2$, yields the **[energy balance equation](@entry_id:191484)**.

A critical feature of this process is the **closure problem**. When we derive the evolution equation for the $N$-th moment, a term involving the $(N+1)$-th moment inevitably appears. For example, to derive the equation for the [second central moment](@entry_id:200758), the **[pressure tensor](@entry_id:147910)** $\mathsf{P}_s$, we multiply the kinetic equation by $m_s\mathbf{c}\mathbf{c}$ (where $\mathbf{c} = \mathbf{v} - \mathbf{u}_s$ is the random velocity) and integrate over [velocity space](@entry_id:181216). The resulting equation for $\mathsf{P}_s$ contains a term involving the divergence of the third central moment, the **heat flux tensor** $\mathsf{Q}_s \equiv m_s \int \mathbf{c}\mathbf{c}\mathbf{c} f_s \, \mathrm{d}^3\mathbf{v}$. Specifically, the full equation for the [pressure tensor](@entry_id:147910) takes the form :
$$
\partial_t \mathsf{P}_s + \nabla\cdot\big(\mathbf{u}_s\,\mathsf{P}_s + \mathsf{Q}_s\big) + \mathsf{P}_s\cdot\nabla \mathbf{u}_s + \big(\mathsf{P}_s\cdot\nabla \mathbf{u}_s\big)^{\mathsf{T}} = \frac{q_s}{m_s}\Big[\mathsf{P}_s\times\mathbf{B} + \big(\mathsf{P}_s\times\mathbf{B}\big)^{\mathsf{T}}\Big] + \mathsf{C}_{P_s}
$$
Here, the term $\nabla\cdot\mathsf{Q}_s$ couples the evolution of the second moment to the third. Deriving an equation for $\mathsf{Q}_s$ would, in turn, introduce the fourth moment. This infinite hierarchy means that a fluid model can never be exact unless it is truncated. This truncation is achieved by postulating a **[closure relation](@entry_id:747393)**—an expression that relates the highest-order moment in the system to lower-order moments (e.g., expressing heat flux in terms of the temperature gradient). The validity of a fluid model rests entirely on the accuracy of its chosen [closures](@entry_id:747387).

### Particle Balance: The Continuity Equation

The continuity equation expresses the conservation of particles. In its local, or differential, form, it states that the rate of change of particle number density $n_s$ at a point is balanced by the divergence of the [particle flux](@entry_id:753207) $n_s \mathbf{u}_s$ and any local particle sources or sinks $S_s$ (e.g., ionization and recombination):
$$
\frac{\partial n_s}{\partial t} + \nabla \cdot (n_s \mathbf{u}_s) = S_s
$$

While this local law is fundamental, it is often more practical to consider a global balance over a finite control volume $V(t)$, which may be moving or deforming. To relate the change in the total number of particles within this volume, $N_s(t) = \int_{V(t)} n_s \, \mathrm{d}V$, to the fluxes across its boundary $\partial V(t)$, we use the **Reynolds [transport theorem](@entry_id:176504)**. If the boundary moves with a velocity field $\mathbf{w}(\mathbf{x}, t)$, the theorem connects the [total time derivative](@entry_id:172646) of the integral to the integral of the [local time](@entry_id:194383) derivative. Combining this with the local continuity equation and the [divergence theorem](@entry_id:145271) yields the global [particle balance](@entry_id:753197) law :
$$
\frac{\mathrm{d}N_s}{\mathrm{d}t} = \frac{\mathrm{d}}{\mathrm{d}t}\int_{V(t)} n_{s}\,\mathrm{d}V = \int_{V(t)} S_{s}\,\mathrm{d}V - \oint_{\partial V(t)} n_{s}(\mathbf{u}_{s}-\mathbf{w})\cdot \hat{\mathbf{n}}\,\mathrm{d}A
$$
This equation provides a powerful insight: the flux of particles across the boundary of a [moving control volume](@entry_id:265261) is governed by the **relative velocity** of the fluid with respect to the boundary, $\mathbf{u}_s - \mathbf{w}$.

This has profound consequences. If we choose a **material volume** that moves exactly with the fluid (a Lagrangian frame, where $\mathbf{w} = \mathbf{u}_s$), the [surface integral](@entry_id:275394) vanishes. In the absence of sources ($S_s=0$), the total number of particles within the volume is conserved, $\mathrm{d}N_s/\mathrm{d}t = 0$. In contrast, for a fixed Eulerian grid ($\mathbf{w}=\mathbf{0}$), the change in particle number is determined solely by the net flux of particles flowing across the stationary boundaries. This distinction is critical in [computational plasma physics](@entry_id:198820), where **Arbitrary Lagrangian-Eulerian (ALE)** methods use moving meshes, and correctly calculating [numerical fluxes](@entry_id:752791) requires using the [relative velocity](@entry_id:178060) $(\mathbf{u}_s - \mathbf{w})$ .

### Momentum Balance and the Structure of Forces

The [momentum balance](@entry_id:1128118) equation for a plasma fluid describes how the flow velocity $\mathbf{u}$ changes in response to forces. In its most general form for a single fluid with mass density $\rho$, it is an expression of Newton's second law:
$$
\rho \left( \frac{\partial \mathbf{u}}{\partial t} + \mathbf{u} \cdot \nabla \mathbf{u} \right) = \mathbf{F}_{\text{total}}
$$
The total force density $\mathbf{F}_{\text{total}}$ in a plasma is dominated by pressure gradients and [electromagnetic forces](@entry_id:196024). A more precise form is $\rho \frac{D\mathbf{u}}{Dt} = -\nabla\cdot\mathsf{P} + \mathbf{J}\times\mathbf{B}$, where $\frac{D}{Dt}$ is the [convective derivative](@entry_id:262900).

#### The Pressure Tensor: Anisotropic Forces in a Plasma

The term $\nabla\cdot\mathsf{P}$ represents the force due to the transport of momentum by random particle motion. The [pressure tensor](@entry_id:147910) $\mathsf{P}_s$ is the [second central moment](@entry_id:200758) of the distribution function, representing the flux of momentum for species $s$. It is fundamentally **Galilean invariant**, as it is defined in terms of the random velocity $\mathbf{c} = \mathbf{v} - \mathbf{u}_s$, which is independent of the observer's [inertial frame](@entry_id:275504) .

In continuum mechanics, any [second-rank tensor](@entry_id:199780) can be decomposed into an isotropic part and a trace-free (deviatoric) part. For the pressure tensor $\mathsf{P}$, this decomposition is:
$$
\mathsf{P} = p\mathsf{I} + \boldsymbol{\pi}
$$
where $p = \frac{1}{3}\mathrm{Tr}(\mathsf{P})$ is the **scalar pressure**, $\mathsf{I}$ is the identity tensor, and $\boldsymbol{\pi}$ is the **[deviatoric stress tensor](@entry_id:267642)**, which satisfies $\mathrm{Tr}(\boldsymbol{\pi}) = 0$ . The scalar pressure represents the familiar omnidirectional force, while the [deviatoric stress](@entry_id:163323) describes anisotropic forces such as viscosity. For a plasma in [local thermodynamic equilibrium](@entry_id:139579), described by a Maxwellian distribution, the velocity distribution is isotropic, resulting in a purely [isotropic pressure](@entry_id:269937) tensor where $\boldsymbol{\pi} = \mathbf{0}$ .

In a strongly magnetized plasma, particles gyrate rapidly around magnetic field lines but move freely along them. This breaks the isotropy. The pressure tensor becomes **gyrotropic**, characterized by distinct pressures parallel ($p_\parallel$) and perpendicular ($p_\perp$) to the magnetic field unit vector $\mathbf{b}$:
$$
\mathsf{P}_{\text{gyro}} = p_{\perp} \mathsf{I} + (p_{\parallel} - p_{\perp}) \mathbf{b} \mathbf{b}
$$
In this case, the scalar pressure is the average $p = \frac{1}{3}(p_{\parallel} + 2p_{\perp})$, and the [deviatoric stress](@entry_id:163323) is nonzero if $p_\parallel \neq p_\perp$:
$$
\boldsymbol{\pi}_{\text{gyro}} = (p_{\parallel} - p_{\perp})\left(\mathbf{b}\mathbf{b} - \frac{1}{3}\mathsf{I}\right)
$$
This gyrotropic stress describes a tension or [excess pressure](@entry_id:140724) along the magnetic field direction.

#### The Lorentz Force and MHD Equilibrium

The [electromagnetic force density](@entry_id:1124311) on the plasma is the **Lorentz force**, $\mathbf{J} \times \mathbf{B}$. This force can be decomposed into two physically distinct components :
$$
\mathbf{J} \times \mathbf{B} = -\nabla\left(\frac{B^2}{2\mu_0}\right) + \frac{(\mathbf{B}\cdot\nabla)\mathbf{B}}{\mu_0}
$$
The first term, $-\nabla(B^2/2\mu_0)$, is a **magnetic pressure** gradient, which acts to push the plasma from regions of high magnetic field strength to regions of low field strength. The second term, $(\mathbf{B}\cdot\nabla)\mathbf{B}/\mu_0$, is the **magnetic tension** force, which acts to straighten curved magnetic field lines, much like the tension in a stretched rubber band.

In a static equilibrium, the outward push from the plasma's thermal pressure must be balanced by the inward-confining Lorentz force: $\nabla p = \mathbf{J} \times \mathbf{B}$. The relative importance of these forces is quantified by the dimensionless parameter **plasma beta**, $\beta$, defined as the ratio of thermal pressure to magnetic pressure:
$$
\beta \equiv \frac{p}{B^2 / (2\mu_0)}
$$
In a simple straight cylinder, equilibrium modification depends simply on $\beta$. However, in a torus with major radius $R$ and minor radius $a$, the curved magnetic field introduces a tension force that scales as $B^2/(\mu_0 R)$. The pressure [gradient force](@entry_id:166847) scales as $p/a$. Significant modification of the magnetic geometry occurs when the pressure force becomes comparable to this tension force, i.e., $p/a \gtrsim B^2/(\mu_0 R)$. Rewriting this in terms of $\beta$ reveals a crucial insight: pressure effects are amplified by the aspect ratio $R/a$. The criterion becomes :
$$
\beta \left(\frac{R}{a}\right) \gtrsim 1
$$
This shows that even a low-$\beta$ plasma can significantly distort its own magnetic confinement if the aspect ratio is large.

### Energy Balance: Heating, Cooling, and Transport

The [energy balance equation](@entry_id:191484) describes how the plasma's internal energy evolves due to heating, cooling, and [energy transport](@entry_id:183081). A change in the total internal energy, $W = \int \frac{3}{2} n T \, dV$, is balanced by power sources, sinks, and fluxes.

#### Energy Sources: Work and Heating

Energy is supplied to the plasma through mechanical work and heating processes. The primary terms appearing in the internal energy equation are the pressure-work term and the electromagnetic work term.

The **pressure-work term**, $\mathsf{P}:\nabla\mathbf{u}$, represents the rate of work done per unit volume by pressure forces on the flow, converting bulk kinetic energy into internal energy . For an isotropic fluid ($\mathsf{P}=p\mathsf{I}$), this reduces to the familiar **compressional work**, $p\nabla\cdot\mathbf{u}$. Energy is gained during compression ($\nabla\cdot\mathbf{u} \lt 0$) and lost during expansion. However, for an anisotropic, gyrotropic plasma, the story is more complex:
$$
\mathsf{P}_{\text{gyro}}:\nabla\mathbf{u} = p_\perp \nabla\cdot\mathbf{u} + (p_\parallel - p_\perp) \mathbf{b}\mathbf{b}:\nabla\mathbf{u}
$$
The new term, $(p_\parallel - p_\perp) \mathbf{b}\mathbf{b}:\nabla\mathbf{u}$, represents work done by stretching or squeezing the plasma along the magnetic field. This work can be nonzero even in an incompressible flow ($\nabla\cdot\mathbf{u}=0$), a purely anisotropic effect . Furthermore, the [deviatoric stress](@entry_id:163323) $\boldsymbol{\pi}$ gives rise to the **viscous heating** term, $\boldsymbol{\pi}:\nabla\mathbf{u}$, which is an irreversible dissipation of energy due to internal friction in collisional plasmas [@problem_id:3958904, 3958908].

The **electromagnetic work term**, $\mathbf{J}\cdot\mathbf{E}$, describes the rate of work done by the electric field on the charge carriers. By substituting the generalized Ohm's law for $\mathbf{E}$, this term can be decomposed into reversible work and irreversible heating. The most important irreversible component is **Ohmic or Joule heating**, $\eta J^2$ . Since resistivity $\eta$ and $J^2$ are both non-negative, this term is always a source of internal energy, representing the dissipation of [electromagnetic energy](@entry_id:264720) into heat through collisions.

#### Energy Fluxes: Convection and Conduction

Energy is transported through the plasma by both bulk motion and thermal gradients.

The **convective energy flux** is the transport of energy due to the [bulk flow](@entry_id:149773) $\mathbf{u}$. Critically, the quantity advected is not just the internal energy density ($u_s = \frac{3}{2}n_s T_s$) but the **enthalpy density** ($h_s = u_s + p_s$). For a simple ideal gas, $h_s = \frac{5}{2}n_s T_s$. The inclusion of the pressure term $p_s$ accounts for the "[flow work](@entry_id:145165)" done by the fluid as it moves into an adjacent [volume element](@entry_id:267802) .

The **conductive heat flux**, $\mathbf{q}$, is the transport of energy by random thermal motions, driven by a temperature gradient. This is a prime example of a [closure relation](@entry_id:747393). In a collisional, magnetized plasma, this flux is highly anisotropic, as described by the **Braginskii heat flux** relation :
$$
\mathbf{q}_s = -\kappa_{\parallel s}\nabla_{\parallel}T_s - \kappa_{\perp s}\nabla_{\perp}T_s - \kappa_{\wedge s}\hat{\mathbf{b}}\times\nabla T_s
$$
This expression reveals three distinct transport mechanisms:
1.  **Parallel Conduction ($\kappa_\parallel$):** Heat flows rapidly along magnetic field lines, largely unimpeded by the magnetic field. The conductivity $\kappa_{\parallel s} \sim n_s T_s \tau_s/m_s$ is large and independent of magnetic field strength $B$.
2.  **Perpendicular Conduction ($\kappa_\perp$):** Heat transport across field lines is strongly suppressed by particle gyromotion. A particle must undergo a collision to jump to an adjacent field line. Consequently, the perpendicular conductivity is much smaller, scaling as $\kappa_{\perp s} \sim \kappa_{\parallel s} / (1 + (\Omega_s\tau_s)^2)$, where $\Omega_s\tau_s$ is the magnetization parameter ([gyrofrequency](@entry_id:1125853) times [collision time](@entry_id:261390)).
3.  **Righi-Leduc (Cross) Flux ($\kappa_\wedge$):** The Lorentz force also creates a heat flux that is perpendicular to both the magnetic field and the temperature gradient. This "cross" flux has a coefficient that scales as $\kappa_{\wedge s} \sim \kappa_{\parallel s} (\Omega_s\tau_s) / (1 + (\Omega_s\tau_s)^2)$.

### Non-Ideal Effects and Broken Symmetries

An "ideal" plasma model often assumes perfect conductivity ($\eta=0$) and other simplifications. Real plasmas are non-ideal, and these effects break the [symmetries and conservation laws](@entry_id:168267) of the ideal system.

#### The Generalized Ohm's Law and the Hall Effect

The simple resistive Ohm's law, $\mathbf{E} + \mathbf{v}\times\mathbf{B} = \eta\mathbf{J}$, is itself a closure. A more complete expression, the **generalized Ohm's law**, is derived from the electron [momentum balance](@entry_id:1128118). Neglecting electron inertia but retaining other terms yields :
$$
\mathbf{E} + \mathbf{u} \times \mathbf{B} = \eta \mathbf{J} + \frac{\mathbf{J} \times \mathbf{B}}{ne} - \frac{\nabla p_e}{ne}
$$
The new term, $\frac{\mathbf{J} \times \mathbf{B}}{ne}$, is the **Hall term**. It arises because the current is predominantly carried by the light electrons, which are more strongly tied to magnetic field lines than the heavy ions. This term represents the decoupling of the electron fluid motion from the bulk (ion) fluid motion. The Hall term becomes significant compared to the ideal term when the characteristic length scale of the phenomenon, $L \sim 1/k$, becomes comparable to the **[ion skin depth](@entry_id:1126728)**, $d_i = c/\omega_{pi}$. The relevant ordering is thus $k d_i \sim \mathcal{O}(1)$ . When this condition is met, the simple MHD model breaks down and a two-fluid or Hall-MHD model is required.

#### Resistive Decay of Global Quantities

Resistivity breaks the "frozen-in flux" theorem of ideal MHD, allowing magnetic field lines to diffuse and reconnect. This has consequences for globally conserved quantities.

The total magnetic energy in a volume, $U_B = \int \frac{B^2}{2\mu_0} dV$, decays due to Ohmic dissipation at a rate given by :
$$
\frac{\mathrm{d}U_B}{\mathrm{d}t} \bigg|_{\text{resistive}} = -\int_V \eta J^2\, dV
$$
Simultaneously, this dissipated magnetic energy appears as a source in the plasma internal energy balance, $\frac{\mathrm{d}U_{\text{int}}}{\mathrm{d}t}|_{\text{resistive}} = +\int_V \eta J^2\, dV$.

Furthermore, resistivity breaks the conservation of **[magnetic helicity](@entry_id:751625)**, $K = \int_V \mathbf{A}\cdot\mathbf{B}\,dV$, which measures the knottedness and linkage of magnetic flux tubes. In resistive MHD, helicity decays according to :
$$
\frac{\mathrm{d}K}{\mathrm{d}t} = -2\int_V \eta \mathbf{J}\cdot\mathbf{B}\, dV
$$
For a [force-free field](@entry_id:1125202) where $\mathbf{J}$ is parallel to $\mathbf{B}$, this decay is nonzero, leading to a simplification of the magnetic field topology over time.

### Synthesis: Global Power Balance in a Burning Plasma

These fundamental principles can be integrated to form a global power balance for a system like a D-T burning plasma in a tokamak. Considering the plasma volume as a fixed control volume, the power balance equation states that the rate of change of stored thermal energy ($dW/dt$) plus all power losses must equal the total power input from heating sources :
$$
P_{\alpha} + P_{\text{aux}} = P_{\text{rad}} + P_{\text{cond}} + P_{\text{conv}} + \frac{dW}{dt}
$$
Each term represents a physical mechanism we have discussed:
- **Heating Sources:** $P_{\alpha}$ is the power from fusion-born alpha particles thermalizing in the plasma, and $P_{\text{aux}}$ is the power from external systems (e.g., radio-frequency waves).
- **Loss Channels:**
    - $P_{\text{rad}}$ is the power lost to volumetric radiation.
    - $P_{\text{cond}}$ and $P_{\text{conv}}$ are the power lost across the plasma boundary due to conduction and convection, respectively. They are [surface integrals](@entry_id:144805) of the heat [flux vector](@entry_id:273577) $\mathbf{q}$ and the enthalpy [flux vector](@entry_id:273577) $h\mathbf{v}$.
- **Energy Storage:** $dW/dt$ is the rate of change of the total plasma thermal energy, $W = \int_V \sum_s \frac{3}{2} n_s T_s \, dV$.

This global balance equation, while phenomenological, is directly built upon the local conservation laws and closure relations that govern the complex, multiscale physics of a plasma.