## Introduction
Simulating processes involving melting and [solidification](@entry_id:156052), known as Stefan problems, is a cornerstone of computational thermal engineering. The moving interface between solid and liquid phases presents significant numerical challenges, often requiring complex interface-tracking schemes. The [enthalpy-porosity technique](@entry_id:1124545) emerges as a powerful and widely adopted alternative, offering a robust fixed-grid approach that circumvents these complexities. This method reformulates the governing equations to be valid across the entire domain—solid, liquid, and the intermediate "mushy" zone—providing an elegant and efficient framework for tackling phase change. This article delves into this essential computational method, equipping you with a graduate-level understanding of its theory and application.

The following chapters will guide you through a comprehensive exploration of the [enthalpy-porosity technique](@entry_id:1124545). The first chapter, **Principles and Mechanisms**, lays the theoretical foundation, detailing how the "porosity" model damps momentum in the solid and how the "enthalpy" formulation implicitly handles latent heat to ensure energy conservation. Next, the **Applications and Interdisciplinary Connections** chapter demonstrates the method's remarkable versatility, showcasing its use in fields ranging from [additive manufacturing](@entry_id:160323) and [metallurgy](@entry_id:158855) to energy systems and [geosciences](@entry_id:749876). Finally, the **Hands-On Practices** section bridges theory and practice, outlining key exercises in nondimensionalization, solver architecture, and code verification that are fundamental to implementing and validating a phase-change solver.

## Principles and Mechanisms

The simulation of melting and [solidification](@entry_id:156052) processes presents a significant challenge in computational physics and engineering due to the presence of a moving and deforming interface between phases. This class of problems, often referred to as **Stefan problems**, requires methodologies that can accurately capture both the transport phenomena (heat and momentum) in the bulk phases and the specific physics of phase transformation at the interface. While methods that explicitly track the interface, such as **[front-tracking](@entry_id:749605)** or **[level-set methods](@entry_id:913252)**, offer high fidelity in representing the interface geometry, they can be complex to implement, particularly for problems involving intricate interfacial topologies in three dimensions .

The **enthalpy–porosity technique** offers a powerful and robust alternative. It is a **fixed-grid method** that circumvents the need for explicit [interface tracking](@entry_id:750734) by reformulating the governing equations to be valid over the entire computational domain, encompassing solid, liquid, and the phase-change region. This is achieved through two core mechanisms: a "porosity" model to handle momentum transport and an "enthalpy" model for [energy transport](@entry_id:183081).

### The "Porosity" Mechanism: Momentum Transport in the Mushy Zone

A central feature of the [enthalpy-porosity technique](@entry_id:1124545) is its treatment of the momentum equations. The method models the region where solid and liquid coexist—the **[mushy zone](@entry_id:147943)**—as a porous medium. The solid phase is treated as the porous matrix, and the liquid phase is the fluid flowing through it. The key insight is to relate the local porosity of this fictitious medium directly to the local liquid [volume fraction](@entry_id:756566), denoted by $f_l$.

Porosity, $\varepsilon$, is defined as the fraction of a [representative elementary volume](@entry_id:152065) (REV) that is available for fluid motion. In a melting or solidifying system, this volume is precisely the liquid portion. Therefore, the fundamental identification is made: $\varepsilon = f_l$ . This single assumption unifies the description of the flow domain:
- In the fully liquid region, $f_l = 1$, corresponding to a medium with full porosity (no obstruction).
- In the fully solid region, $f_l = 0$, corresponding to a medium with zero porosity (complete obstruction).
- In the [mushy zone](@entry_id:147943), $0  f_l  1$, representing a partially obstructed flow.

To incorporate this physical analogy into the governing equations, the standard **Navier-Stokes equations** for fluid motion are augmented with a momentum sink term, $\mathbf{S}_{\mathbf{u}}$. This term acts as a body force that represents the drag exerted by the solid matrix on the fluid. The volume-averaged momentum equation for an [incompressible fluid](@entry_id:262924) then takes the form:
$$
\rho \left( \frac{\partial \mathbf{u}}{\partial t} + \mathbf{u} \cdot \nabla \mathbf{u} \right) = -\nabla p + \mu \nabla^2 \mathbf{u} + \rho \mathbf{g} + \mathbf{S}_{\mathbf{u}}
$$
where $\rho$ is the fluid density, $\mathbf{u}$ is the velocity, $p$ is the pressure, $\mu$ is the [dynamic viscosity](@entry_id:268228), and $\mathbf{g}$ is the gravitational acceleration.

The sink term $\mathbf{S}_{\mathbf{u}}$ must be modeled such that it enforces the correct physical behavior at the phase limits. The drag should vanish in the pure liquid and become infinitely large in the pure solid to suppress motion. This behavior is captured by **Darcy's law** for [flow in porous media](@entry_id:1125104), which states that the drag force per unit volume is proportional to the fluid velocity and inversely proportional to the medium's permeability, $K$:
$$
\mathbf{S}_{\mathbf{u}} = -\frac{\mu}{K} \mathbf{u}
$$
The permeability $K$ is a measure of the ability of a porous medium to allow fluid to pass through it. In the context of solidification, $K$ must be a strong function of the liquid fraction, $f_l$. It must approach infinity (or a very large value) as $f_l \to 1$ and approach zero as $f_l \to 0$ .

A widely used model for the permeability, based on the microstructure of dendritic solids, is the **Carman-Kozeny equation**. This relation models the permeability as a function of porosity, $\varepsilon = f_l$:
$$
K(f_l) = K_0 \frac{f_l^3}{(1-f_l)^2}
$$
where $K_0$ is a constant related to the [morphology](@entry_id:273085) of the [mushy zone](@entry_id:147943). To avoid division by zero as $f_l \to 0$ in numerical implementations, a small [regularization parameter](@entry_id:162917), $\epsilon$, is often added to the denominator. Combining this with the Darcy sink term, we arrive at the most common form of the momentum sink used in the [enthalpy-porosity technique](@entry_id:1124545)  :
$$
\mathbf{S}_{\mathbf{u}} = -C \frac{(1-f_l)^2}{f_l^3 + \epsilon} \mathbf{u}
$$
Here, the constant $C$ is known as the **mushy zone constant**. By comparing this form to the Darcy drag term, we can deduce the physical meaning of $C$. If we define a permeability function as $K(f_l) = K_{\text{ref}} \frac{f_l^3+\epsilon}{(1-f_l)^2}$, then consistency requires that $C = \mu / K_{\text{ref}}$. Thus, $C$ represents a baseline viscous [drag coefficient](@entry_id:276893), incorporating the fluid viscosity and a reference permeability of the mushy zone structure .

In practice, the value of $C$ must be chosen large enough to effectively immobilize the solid phase. A practical strategy is to require that in the solid limit ($f_l \to 0$), even the maximum possible driving force in the system, $F_{\max}$ (e.g., from buoyancy or pressure gradients), results in a velocity no greater than a small tolerance, $U_{\text{solid,max}}$. In the limit $f_l \to 0$, the [momentum balance](@entry_id:1128118) approximates to $\mathbf{F} + \mathbf{S}_{\mathbf{u}} \approx 0$, which yields $|\mathbf{F}| \approx (C/\epsilon)|\mathbf{u}|$. This leads to the conservative selection criterion:
$$
C \ge \frac{F_{\max} \epsilon}{U_{\text{solid,max}}}
$$
This ensures that the velocity in nominally solid regions is suppressed to negligible levels .

### The "Enthalpy" Mechanism: Energy Transport and Latent Heat

The second core component of the method addresses the energy transport, particularly the challenge of accounting for the latent heat of fusion. Instead of treating latent heat as a source term or an explicit boundary condition at a moving interface, the method embeds it directly into the definition of the [thermodynamic state](@entry_id:200783) variable. The chosen variable is the **total [specific enthalpy](@entry_id:140496)**, $h$.

The [total enthalpy](@entry_id:197863) is defined as the sum of the **sensible enthalpy**, $h_s$, which is associated with temperature change, and the **latent heat content**, which is associated with [phase change](@entry_id:147324). For a material with specific heat $c_p$ and latent heat of fusion $L$, the total specific enthalpy is given by :
$$
h(T) = h_s(T) + L f_l(T) = \left( h_{\text{ref}} + \int_{T_{\text{ref}}}^T c_p(\xi) d\xi \right) + L f_l(T)
$$
where $f_l(T)$ is the liquid fraction, which is itself a function of temperature. This definition is distinct from the specific internal energy, $u$. For an incompressible substance with constant density $\rho$, the two are related by $h = u + p/\rho$ .

The liquid fraction function, $f_l(T)$, defines how the [phase change](@entry_id:147324) occurs with respect to temperature. For a [pure substance](@entry_id:150298) undergoing an isothermal phase change at a single melting temperature $T_m$, this function is a discontinuous Heaviside [step function](@entry_id:158924):
$$
f_l(T) = H(T - T_m) = \begin{cases} 0  \text{if } T  T_m \\ 1  \text{if } T > T_m \end{cases}
$$
In this case, the total enthalpy $h(T)$ exhibits a jump of magnitude $L$ at $T=T_m$. Numerically, this discontinuity is challenging to handle. It is therefore common, even for [pure substances](@entry_id:140474), to regularize the phase change by spreading it over a small, non-zero temperature interval $\Delta T = T_l - T_s$, where $T_s$ and $T_l$ are the solidus and liquidus temperatures. Within this interval, the liquid fraction varies smoothly from $0$ to $1$. A simple and common choice is a [piecewise linear function](@entry_id:634251) :
$$
f_l(T) = \begin{cases} 0  \text{if } T \le T_s \\ \frac{T - T_s}{T_l - T_s}  \text{if } T_s  T  T_l \\ 1  \text{if } T \ge T_l \end{cases}
$$
This function is continuous and bounded, making it amenable to numerical computation. As the mushy interval width approaches zero ($\Delta T \to 0$), this function converges pointwise to the Heaviside [step function](@entry_id:158924), and its derivative converges in the sense of distributions to the Dirac [delta function](@entry_id:273429), $\delta(T-T_s)$, correctly recovering the physics of isothermal [phase change](@entry_id:147324) .

By defining enthalpy in this way, the energy conservation equation can be written in a single, universal form that is valid everywhere:
$$
\rho \left( \frac{\partial h}{\partial t} + \mathbf{u} \cdot \nabla h \right) = \nabla \cdot (k \nabla T)
$$
This is a **conservation law** for the quantity $\rho h$. This "[divergence form](@entry_id:748608)" is critical because, when discretized using a **Finite Volume Method**, it naturally leads to schemes where the total energy of the system is conserved to machine precision, a property not easily achieved with alternative formulations . The latent heat is not an explicit source term; it is implicitly accounted for as the system's enthalpy changes within the phase-change temperature range. This elegant approach is a key reason for the method's robustness and popularity. The Stefan condition at the interface is not enforced explicitly; rather, it is satisfied implicitly in an averaged sense over the control volumes that constitute the mushy zone .

### The Complete Governing Equations

Combining the momentum and energy formulations yields a complete, coupled set of equations for modeling convection-driven melting and [solidification](@entry_id:156052). For an incompressible Newtonian fluid under the assumptions discussed, the system is :

1.  **Mass Conservation (Continuity):**
    $$
    \nabla \cdot \mathbf{u} = 0
    $$

2.  **Momentum Conservation:**
    $$
    \rho \left( \frac{\partial \mathbf{u}}{\partial t} + \mathbf{u} \cdot \nabla \mathbf{u} \right) = -\nabla p + \mu \nabla^2 \mathbf{u} + \rho \mathbf{g} - C \frac{(1-f_l)^2}{f_l^3 + \epsilon} \mathbf{u}
    $$

3.  **Energy Conservation:**
    $$
    \rho \left( \frac{\partial h}{\partial t} + \mathbf{u} \cdot \nabla h \right) = \nabla \cdot (k \nabla T)
    $$

This system is closed by the [constitutive relations](@entry_id:186508) that link enthalpy, temperature, and liquid fraction:
$$
h = h_s(T) + L f_l \quad \text{and} \quad f_l = f_l(T)
$$
These relations introduce a strong, non-linear coupling. The energy equation is solved for the enthalpy field, $h$. From the local value of $h$, the corresponding temperature $T$ and liquid fraction $f_l$ are determined. This liquid fraction then directly modifies the momentum sink term, influencing the velocity field $\mathbf{u}$. In turn, the velocity field advects enthalpy via the term $\mathbf{u} \cdot \nabla h$ in the energy equation, closing the feedback loop.

### Numerical Considerations and Implementation

While the enthalpy-porosity framework is conceptually elegant, its numerical implementation requires care.

A key parameter is the width of the mushy zone, $\Delta T = T_l - T_s$. The choice of $\Delta T$ has significant consequences. The effective specific heat capacity, $c_{\text{eff}} = dh/dT = c_p + L \frac{df_l}{dT}$, can become very large within the mushy zone, especially for small $\Delta T$, as $\frac{df_l}{dT}$ scales as $1/\Delta T$. A large $c_{\text{eff}}$ introduces severe **[numerical stiffness](@entry_id:752836)** into the time-dependent [energy equation](@entry_id:156281), potentially forcing the use of very small time steps in explicit integration schemes . Physically, $\Delta T$ is also related to the spatial thickness of the mushy region, $\delta_m$, by $\delta_m \approx \Delta T / G$, where $G$ is the local temperature gradient. A smaller $\Delta T$ thus corresponds to a physically and numerically sharper interface.

Another critical aspect of implementation is ensuring that the physical constraints on the liquid fraction, $0 \le f_l \le 1$, are respected at all times. Due to numerical discretization errors, a solver might produce a provisional temperature update that, if naively used to compute $f_l$, would yield an unphysical value (e.g., $f_l > 1$). Simply "clipping" the temperature or liquid fraction to their physical bounds will violate the strict energy conservation that is a hallmark of the method. The correct procedure is an **enthalpy-conserving update**: the updated [specific enthalpy](@entry_id:140496) $h^{n+1}$ from the solver is treated as inviolable. One then inverts the $h(T)$ relationship to find the unique, physically-consistent state $(T^{n+1}, f_l^{n+1})$ that corresponds to that enthalpy. For example, if $h^{n+1}$ is greater than the [specific enthalpy](@entry_id:140496) at the liquidus temperature, $h(T_l)$, then the final state must be fully liquid ($f_l^{n+1}=1$) with a temperature $T^{n+1} > T_l$ calculated from the excess [specific enthalpy](@entry_id:140496). This procedure guarantees both physical [boundedness](@entry_id:746948) and energy conservation .

In summary, the [enthalpy-porosity technique](@entry_id:1124545) provides a powerful and versatile framework for simulating complex phase-change phenomena. By treating the entire domain with a single set of equations and embedding the physics of latent heat and solid-phase momentum damping into constitutive relations for enthalpy and porosity, it avoids the complexities of [interface tracking](@entry_id:750734) while maintaining robustness and inherent energy conservation.