## Introduction
The Stefan problem, the classical mathematical model for heat transfer during a phase change, is fundamental to countless phenomena in science and engineering, from the solidification of alloys to the melting of glaciers. However, its defining feature—a moving boundary whose position is unknown and must be solved for—poses significant computational challenges that standard numerical methods cannot easily address. This article provides a comprehensive guide to the numerical discretization of the Stefan problem, bridging theory and practical application.

The first chapter, **Principles and Mechanisms**, lays the theoretical groundwork, detailing the mathematical formulation and introducing the three primary families of numerical methods: interface-tracking, fixed-domain, and diffuse-interface approaches. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates the versatility of these methods by exploring their use in complex, real-world scenarios across [thermal engineering](@entry_id:139895), materials science, and [geophysics](@entry_id:147342). Finally, the **Hands-On Practices** section offers targeted exercises to solidify your understanding of key concepts like [numerical stability](@entry_id:146550) and energy conservation in practical implementations.

## Principles and Mechanisms

This chapter delves into the fundamental principles that govern heat transfer during phase change and the primary mechanisms by which these principles are translated into computational models. We begin by establishing the classical mathematical formulation of the Stefan problem, detailing the governing equations and the crucial conditions at the moving interface. We then explore common physical simplifications and their domains of validity. Finally, we survey the three principal families of numerical methods for discretizing and solving these complex moving-boundary problems: interface-tracking, fixed-domain, and diffuse-interface methods.

### The Mathematical Formulation of the Classical Stefan Problem

The Stefan problem is the canonical mathematical model for the [thermal evolution](@entry_id:755890) of a material undergoing a phase transition, such as melting or [solidification](@entry_id:156052). Its formulation consists of differential equations governing heat transfer within the bulk phases, coupled with specific algebraic and differential conditions at the moving [phase boundary](@entry_id:172947).

#### Governing Equations in Bulk Phases

Within any region of a single, pure phase (either solid or liquid), where no phase change occurs, the evolution of the temperature field $T(\mathbf{x}, t)$ is governed by the conservation of energy. For a material at rest (no advection), where heat transfer is solely by conduction, the local energy balance dictates that the rate of change of internal energy per unit volume is equal to the negative divergence of the heat [flux vector](@entry_id:273577), $\mathbf{q}$. According to **Fourier's law of conduction**, the heat flux is proportional to the negative gradient of the temperature: $\mathbf{q} = -k \nabla T$, where $k$ is the thermal conductivity of the material.

Combining these principles, and assuming constant [thermophysical properties](@entry_id:1133078) (density $\rho$, specific heat $c$, and thermal conductivity $k$) within each phase, we arrive at the standard **heat equation**. For a phase denoted by the subscript $\alpha$ (where $\alpha$ can be $s$ for solid or $\ell$ for liquid), the governing partial differential equation (PDE) is:
$$
\rho_\alpha c_\alpha \frac{\partial T_\alpha}{\partial t} = k_\alpha \nabla^2 T_\alpha
$$
This equation describes how temperature evolves and diffuses through the bulk solid and liquid regions, away from the interface where the phase transformation takes place .

#### Conditions at the Sharp Interface

The defining feature of the Stefan problem is the moving interface, a boundary whose position is unknown *a priori* and must be solved for as part of the problem. This "free boundary" necessitates additional conditions that are not present in standard heat conduction problems. These conditions are imposed at the infinitesimally thin, or "sharp," interface separating the phases.

##### Thermodynamic Equilibrium and Temperature Continuity

In the classical formulation, the interface is assumed to be in a state of **[local thermodynamic equilibrium](@entry_id:139579) (LTE)**. For a [pure substance](@entry_id:150298) at a given pressure, solid-liquid equilibrium occurs at a single, sharply defined temperature: the [melting temperature](@entry_id:195793), $T_m$. The LTE assumption posits that the temperature of the material precisely at the interface must be this equilibrium temperature. Since the interface is in simultaneous contact with both the solid and liquid phases, the temperatures of both phases must match $T_m$ as they approach the interface. This gives rise to the condition of temperature continuity :
$$
T_s(\mathbf{x}, t) = T_\ell(\mathbf{x}, t) = T_m \quad \text{for } \mathbf{x} \in \Gamma(t)
$$
where $\Gamma(t)$ is the surface representing the interface at time $t$. This condition serves as a moving Dirichlet boundary condition for the heat equations in the respective bulk domains. It is important to recognize that this continuity is an assumption of the classical model. Physical phenomena such as rapid, non-equilibrium [phase changes](@entry_id:147766) or the presence of a [thermal boundary resistance](@entry_id:152481) (e.g., Kapitza resistance) can lead to a temperature jump or a shift in the interface temperature, which we will discuss in a later section .

##### The Stefan Condition: Interfacial Energy Balance

While temperature is continuous across the interface, the heat flux is generally discontinuous. This discontinuity is the source of energy that drives the phase change. The phase transformation from solid to liquid requires the absorption of a specific amount of energy, known as the **[latent heat of fusion](@entry_id:144988)**, $L$ (in units of J/kg), without any change in temperature. Conversely, solidification releases this same amount of energy.

An energy balance on an infinitesimal control volume encompassing a segment of the interface reveals that the net rate of heat energy flowing into the interface must equal the rate at which energy is consumed or released by the phase change. The rate of energy consumption per unit area is $\rho L V_n$, where $V_n$ is the normal velocity of the interface. This balance gives rise to the **Stefan condition** :
$$
\rho L V_n = \mathbf{q}_s \cdot \mathbf{n} - \mathbf{q}_\ell \cdot \mathbf{n}
$$
Here, $\mathbf{n}$ is the [unit normal vector](@entry_id:178851) to the interface (conventionally pointing from solid to liquid), and $\mathbf{q}_s$ and $\mathbf{q}_\ell$ are the heat fluxes at the interface evaluated from the solid and liquid sides, respectively. Substituting Fourier's law, $\mathbf{q}_\alpha = -k_\alpha \nabla T_\alpha$, the Stefan condition becomes:
$$
\rho L V_n = (-k_s \nabla T_s) \cdot \mathbf{n} - (-k_\ell \nabla T_\ell) \cdot \mathbf{n} = k_\ell \nabla T_\ell \cdot \mathbf{n} - k_s \nabla T_s \cdot \mathbf{n}
$$
This crucial equation links the motion of the interface ($V_n$) to the jump in the normal component of the heat flux across it. It is an [ordinary differential equation](@entry_id:168621) that governs the evolution of the interface's position, $\Gamma(t)$.

For instance, consider a one-dimensional [solidification](@entry_id:156052) problem where a solid phase exists for $x \in [0, s(t)]$ and a liquid phase for $x \in [s(t), L]$. The [normal vector](@entry_id:264185) is in the $+x$ direction, and $V_n = \frac{ds}{dt}$. The Stefan condition simplifies to:
$$
\rho L \frac{ds}{dt} = k_\ell \left. \frac{\partial T_\ell}{\partial x} \right|_{x=s(t)^+} - k_s \left. \frac{\partial T_s}{\partial x} \right|_{x=s(t)^-}
$$
If, at a given instant, we can estimate the temperature gradients on both sides of the interface, we can directly compute the interface speed. Suppose in a numerical simulation with $T_m=0\,^{\circ}\text{C}$, the temperature at a far-field solid boundary is $T_w=-10\,^{\circ}\text{C}$ and at a [far-field](@entry_id:269288) liquid boundary is $T_R=20\,^{\circ}\text{C}$. Using simple linear approximations for the gradients, we can calculate the fluxes and, consequently, the interface velocity, providing a direct application of this fundamental principle .

#### One-Phase Versus Two-Phase Models

The complete formulation, involving solving the heat equation in both the solid and liquid domains coupled by the full Stefan condition, is known as the **two-phase Stefan model**. This approach is necessary when temperature variations in both phases are significant and contribute to the heat balance at the interface .

In many practical scenarios, a simplification is possible. If one phase has a very high thermal conductivity, is subject to vigorous convection that keeps it well-mixed, or is only slightly superheated or subcooled, its temperature can be assumed to be uniform and equal to the melting temperature, $T_m$. For example, in the melting of ice in warm water, the water temperature may remain nearly uniform. In such a case, the temperature gradient in that phase is negligible ($\nabla T_\ell \approx 0$). This reduces the problem to a **one-phase Stefan model**, where the heat equation is solved in only one domain (the non-isothermal one). The Stefan condition simplifies accordingly, with the flux from the isothermal phase vanishing. For solidification where the liquid is assumed to be at $T_m$, the condition becomes :
$$
\rho L V_n = - k_s \nabla T_s \cdot \mathbf{n}
$$

The validity of this one-[phase reduction](@entry_id:1129588) can be rigorously assessed through scaling analysis . The key parameter is the **Stefan number**, $\text{Ste} = c \Delta T / L$, which compares the sensible heat in a phase to the latent heat of transition. The one-phase approximation is generally justified when the Stefan number of the neglected phase is much less than one ($\text{Ste}_\ell \ll 1$), indicating that the sensible heat stored in the liquid is small compared to the latent heat. However, the accuracy also depends on the rate of heat extraction, often characterized by the **Biot number**, $\text{Bi} = h \ell_{char} / k$, which compares convective heat transfer to conductive heat transfer. A formal analysis shows that the relative error introduced by the one-phase assumption scales with the ratio of Stefan numbers, $\text{Ste}_\ell / \text{Ste}_s$, and also depends on the Biot number. The approximation becomes poor if the Biot number is very small ([conduction-limited regime](@entry_id:747673)) .

### Beyond the Classical Model: Advanced Interfacial Physics

The classical assumption of an interface at a constant [melting temperature](@entry_id:195793) $T_m$ is an idealization. For many real-world phenomena, especially those involving curved interfaces or rapid phase changes, this condition must be modified to account for additional thermodynamic and kinetic effects.

#### The Gibbs-Thomson Effect: Curvature-Dependent Temperature

The interface between two phases possesses an excess free energy per unit area, known as the **surface tension** or interfacial energy. For a system to remain in equilibrium, the temperature at a curved interface must differ from that of a flat interface ($T_m$). This phenomenon is known as the **Gibbs-Thomson effect**. For a convex solid particle growing into a liquid, the surface tension acts to increase the solid's chemical potential, making it less stable. To restore equilibrium, the temperature must be lowered. The change in equilibrium temperature is proportional to the local [mean curvature](@entry_id:162147) of the interface, $\kappa$:
$$
T_{eq} = T_m - \Gamma \kappa
$$
where $\Gamma$ is the Gibbs-Thomson coefficient, a positive material constant related to the surface tension and latent heat. The sign convention is critical: if the [normal vector](@entry_id:264185) points into the liquid, a convex solid has [positive curvature](@entry_id:269220) ($\kappa > 0$), leading to a depressed melting point ($T_{eq}  T_m$). Conversely, a concave solid interface ($\kappa  0$) has an elevated [melting point](@entry_id:176987) .

#### Interface Kinetics: Velocity-Dependent Temperature

A phase transformation is a physical process that takes time. For the atoms or molecules at an interface to rearrange themselves from a liquid to a solid structure (or vice versa), a thermodynamic driving force is required. This driving force is a deviation of the actual interface temperature, $T_\Gamma$, from the local equilibrium temperature, $T_{eq}$. This deviation is known as **kinetic [undercooling](@entry_id:162134)** (for solidification) or **kinetic [superheating](@entry_id:147261)** (for melting). For many materials, especially at high growth rates, the interface velocity $V_n$ is approximately proportional to this deviation. This leads to a linear kinetic law:
$$
V_n \propto (T_{eq} - T_\Gamma)
$$
Rearranging this, the kinetic effect introduces a velocity-dependent term into the interface temperature condition. Combining this with the Gibbs-Thomson effect, we arrive at the more general **Gibbs-Thomson-kinetic relation** :
$$
T_\Gamma = T_{eq} - \mu V_n = T_m - \Gamma \kappa - \mu V_n
$$
where $\mu$ is a positive kinetic coefficient. During solidification ($V_n  0$), the term $-\mu V_n$ represents the necessary kinetic [undercooling](@entry_id:162134). During melting ($V_n  0$), it represents kinetic [superheating](@entry_id:147261).

### Fundamental Approaches to Discretization

Solving the Stefan problem numerically is challenging due to the moving boundary, which must be tracked or otherwise accounted for. Several distinct families of methods have been developed to tackle this challenge.

#### Interface-Tracking and Front-Fixing Methods

This class of methods explicitly represents the interface and follows its evolution in time. The computational domain is often divided into subdomains corresponding to each phase, and the grid may be adapted to conform to the interface.

A classic example is the **Landau transformation**, a front-fixing technique applicable to one-dimensional problems . Consider a one-[phase problem](@entry_id:146764) on a moving domain $x \in [0, s(t)]$. The Landau transform introduces a new, dimensionless coordinate $\xi = x/s(t)$, which maps the moving physical domain to a fixed computational domain $\xi \in [0, 1]$. When the original PDE is rewritten in terms of $(\xi, t)$, the time-dependence of the [coordinate transformation](@entry_id:138577) introduces new terms. The original heat equation, $\rho c \frac{\partial T}{\partial t} = k \frac{\partial^2 T}{\partial x^2}$, transforms into a new equation for $\theta(\xi, t) = T(x,t)$:
$$
\rho c \frac{\partial \theta}{\partial t} = \frac{k}{s(t)^2} \frac{\partial^2 \theta}{\partial \xi^2} + \rho c \frac{\xi \dot{s}}{s(t)} \frac{\partial \theta}{\partial \xi}
$$
The motion of the boundary manifests as a **pseudo-convective term** (the last term on the right), where the "velocity" depends on the interface speed $\dot{s}$ and the position $\xi$. The problem is now solved on a fixed grid, but at the cost of a more complex PDE coupled to an ODE for $s(t)$ derived from the transformed Stefan condition.

Other powerful interface-tracking methods include the **level-set method**, where the interface is implicitly represented as the zero contour of a higher-dimensional function. This approach is particularly well-suited for handling complex [topological changes](@entry_id:136654) and for incorporating curvature-dependent physics, as the curvature can be readily computed from the [level-set](@entry_id:751248) function .

#### Fixed-Domain Methods: The Enthalpy Formulation

Instead of explicitly tracking the interface, fixed-domain methods reformulate the problem as a single equation valid over the entire physical domain (solid, liquid, and interface). The most prominent of these is the **enthalpy method**  .

The key idea is to define a total **volumetric enthalpy**, $H$, which includes both the sensible heat (related to temperature) and the latent heat (related to phase). The enthalpy is defined as a function of temperature, $H(T)$:
$$
H(T) = \int_0^T \rho c_p(\theta) \, d\theta + \rho L \chi(T)
$$
Here, the first term represents the sensible heat, and the second term represents the latent heat. $\chi(T)$ is the **liquid fraction** or **phase [indicator function](@entry_id:154167)**, which varies from $0$ (pure solid) to $1$ (pure liquid). For a [pure substance](@entry_id:150298) melting at $T_m$, $\chi(T)$ is a Heaviside [step function](@entry_id:158924). For alloys melting over a range $[T_s, T_l]$, it can be a smooth [ramp function](@entry_id:273156).

With this definition, the energy conservation equation for the entire domain becomes a single, nonlinear PDE:
$$
\frac{\partial H}{\partial t} = \nabla \cdot (k(T) \nabla T)
$$
This equation is solved for the single field variable $H$ on a fixed grid. The interface is never explicitly tracked; its location is implicitly defined by the region where the temperature is at or near $T_m$ and the enthalpy is changing due to latent heat absorption/release. The Stefan condition is not imposed explicitly but is automatically satisfied in a weak (integral) sense by this formulation.

Numerically, [conservative schemes](@entry_id:747715) like the Finite Volume Method (FVM) are a natural fit. In each time step, one first updates the cell-averaged enthalpy based on the heat fluxes across cell faces, and then inverts the nonlinear $H(T)$ relationship to find the new cell temperature. This approach is robust and easily handles complex geometries and [topological changes](@entry_id:136654) .

#### Diffuse-Interface Methods: The Phase-Field Approach

A third major paradigm, the **[phase-field method](@entry_id:191689)**, regularizes the infinitesimally sharp interface into a thin but finite transition layer. This is achieved by introducing a continuous **order parameter**, $\psi(\mathbf{x}, t)$, which smoothly varies between distinct values in the bulk phases (e.g., $\psi=+1$ in solid, $\psi=-1$ in liquid). The evolution of $\psi$ is governed by a PDE, typically derived from a [free energy functional](@entry_id:184428), which drives the system towards minimizing its total free energy.

A common phase-field model for solidification couples an evolution equation for $\psi$ with the heat equation for temperature $T$ :
$$
\frac{\partial \psi}{\partial t} = M \left( \epsilon^2 \nabla^2 \psi - f'(\psi) \right) + \lambda (T - T_m)
$$
$$
c \frac{\partial T}{\partial t} = k \nabla^2 T + \frac{\ell}{2} \frac{\partial \psi}{\partial t}
$$
The first equation (an Allen-Cahn type) describes the relaxation of the order parameter. The term $f'(\psi)$ comes from a double-well potential that favors the bulk phase values, the term $\epsilon^2 \nabla^2 \psi$ represents the interfacial energy cost, and the term $\lambda(T-T_m)$ provides the thermodynamic driving force for [phase change](@entry_id:147324). The second equation is the energy conservation equation, where the term $\frac{\ell}{2} \frac{\partial \psi}{\partial t}$ models the release or absorption of latent heat ($\ell$ is latent heat per unit volume).

The great advantage of this approach is that all the complex [interface conditions](@entry_id:750725) are naturally incorporated into the system of PDEs, which can be solved on a fixed grid. Through a formal procedure called **matched [asymptotic analysis](@entry_id:160416)**, it can be shown that in the [sharp-interface limit](@entry_id:1131545) (as the interface thickness $\epsilon \to 0$), this model rigorously converges to the Stefan problem, automatically recovering not only the Stefan condition but also the advanced Gibbs-Thomson-kinetic relation for the interface temperature . This makes phase-field models exceptionally powerful for simulating complex pattern formation in [solidification](@entry_id:156052), such as [dendritic growth](@entry_id:155385).