## Introduction
The transient heating of liquid droplets is a fundamental process that governs the performance and efficiency of numerous engineering systems, from internal combustion engines and gas turbines to industrial spray dryers. While simple models often treat droplets as isothermal spheres, this assumption breaks down under the intense conditions typical of combustion, where rapid heating creates significant temperature gradients within the liquid. The failure to account for this finite rate of internal heat conduction can lead to critical inaccuracies in predicting droplet vaporization rates, ignition delays, and the formation of pollutants.

This article provides a comprehensive exploration of finite-conductivity [droplet heating models](@entry_id:1123998), addressing the gap left by oversimplified approaches. By treating the droplet as a body with internal thermal resistance, we can develop a more physically accurate picture of its thermal behavior. Across three chapters, you will gain a rigorous understanding of this critical phenomenon. We will begin by establishing the mathematical and physical "Principles and Mechanisms" that govern internal heat transfer. Subsequently, we will explore the model's "Applications and Interdisciplinary Connections," showcasing its utility in fields ranging from materials science to forensic medicine. Finally, a series of "Hands-On Practices" will allow you to apply these concepts and develop your own computational tools. We begin by dissecting the core physics and mathematical formulation that define heat transfer within the droplet.

## Principles and Mechanisms

In this chapter, we transition from a general overview to a rigorous mathematical and physical description of heat transfer within a single liquid droplet. The focus is on the **finite-conductivity model**, which acknowledges that heat requires a finite amount of time to propagate through the liquid. This model is essential for accurately capturing the transient heating process, especially in scenarios relevant to combustion, where large temperature gradients can develop within the droplet, influencing its vaporization rate, ignition characteristics, and propensity for micro-explosions. We will systematically build the governing equations from first principles, explore the boundary conditions that couple the droplet to its environment, and discuss the [dimensionless parameters](@entry_id:180651) that dictate the appropriate level of modeling complexity.

### The Governing Equation for Internal Conduction

To model the temperature evolution inside a liquid droplet, we begin by applying the principle of energy conservation. For a stationary volume of liquid with no internal fluid motion (negligible internal circulation), the local rate of change of thermal energy must be balanced by the net rate at which heat is conducted into that volume.

Consider a spherically symmetric droplet where the temperature, $T$, is a function of only the [radial coordinate](@entry_id:165186), $r$, and time, $t$. The conservation of energy for a differential volume element, in the absence of internal heat generation, is expressed by the transient [heat conduction equation](@entry_id:1125966). For a liquid with constant [thermophysical properties](@entry_id:1133078)—namely density $\rho_{\ell}$, [specific heat](@entry_id:136923) at constant pressure $c_{p,\ell}$, and thermal conductivity $k_{\ell}$—the equation takes the form :

$$
\rho_{\ell} c_{p,\ell} \frac{\partial T}{\partial t} = k_{\ell} \nabla^2 T
$$

Here, $\nabla^2$ is the Laplacian operator. For the assumed [spherical symmetry](@entry_id:272852), the Laplacian simplifies significantly, yielding the governing Partial Differential Equation (PDE) for the temperature field $T(r,t)$ within the domain $0 \le r \le R(t)$, where $R(t)$ is the instantaneous droplet radius:

$$
\rho_{\ell} c_{p,\ell} \frac{\partial T}{\partial t} = \frac{k_{\ell}}{r^2} \frac{\partial}{\partial r} \left( r^2 \frac{\partial T}{\partial r} \right)
$$

This equation can also be written in an expanded form as:

$$
\rho_{\ell} c_{p,\ell} \frac{\partial T}{\partial t} = k_{\ell} \left( \frac{\partial^2 T}{\partial r^2} + \frac{2}{r} \frac{\partial T}{\partial r} \right)
$$

Let us dissect the physical meaning of each term in this fundamental equation . The left-hand side, $\rho_{\ell} c_{p,\ell} \frac{\partial T}{\partial t}$, represents the **transient storage of sensible energy** per unit volume. It quantifies how quickly the internal energy at a specific radial location is changing with time. The right-hand side, often written as the divergence of the conductive heat flux ($-\nabla \cdot \vec{q}$ where $\vec{q} = -k_{\ell} \nabla T$), represents the **net rate of heat gain per unit volume due to conduction**. The geometric factor $r^2$ inside the derivative accounts for the increasing surface area of spherical shells as the radius increases, a crucial feature of heat diffusion in a spherical geometry.

A complete formulation requires a boundary condition at the center of the droplet ($r=0$). Physical realism demands that the temperature profile be smooth and symmetric at the origin. A non-zero temperature gradient, $\partial T / \partial r$, at $r=0$ would imply a directional heat flux at a single point, which would require a singular heat source or sink. Therefore, for a spherically symmetric system without a central source, the heat flux at the center must be zero. This gives rise to the **[symmetry boundary condition](@entry_id:271704)** :

$$
\left. \frac{\partial T}{\partial r} \right|_{r=0} = 0
$$

This condition ensures that the solution to the PDE remains physically meaningful and finite at the origin.

### Regimes of Internal Heat Transfer: The Biot Number

Solving the full transient heat conduction PDE is computationally demanding. A critical question for any modeling effort is whether such a detailed approach is truly necessary. The answer lies in comparing the characteristic rate of heat transfer *within* the droplet to the rate of heat transfer *to* the droplet from its surroundings. This comparison is quantified by a dimensionless group called the **liquid-phase Biot number**, $\mathrm{Bi}_{\ell}$ .

The Biot number is defined as the ratio of the internal resistance to conduction to the external resistance to convection:

$$
\mathrm{Bi}_{\ell} = \frac{\text{Internal Conductive Resistance}}{\text{External Convective Resistance}} = \frac{R / k_{\ell}}{1 / h_e} = \frac{h_e R}{k_{\ell}}
$$

Here, $R$ is the droplet radius, $k_{\ell}$ is the liquid's thermal conductivity, and $h_e$ is an effective [convective heat transfer coefficient](@entry_id:151029) at the droplet surface. The value of $\mathrm{Bi}_{\ell}$ determines the appropriate internal heating model.

#### The Infinite-Conductivity Limit ($\mathrm{Bi}_{\ell} \to 0$)

When $\mathrm{Bi}_{\ell}$ is very small (typically $\mathrm{Bi}_{\ell}  0.1$), the internal conductive resistance is negligible compared to the external convective resistance. This means heat can diffuse through the droplet's interior much faster than it is supplied to the surface. As a result, any heat arriving at the surface is rapidly distributed throughout the entire volume, preventing the formation of significant internal temperature gradients. The droplet's temperature remains spatially uniform, though it changes with time: $T(r,t) \approx T(t)$.

In this limit, the detailed PDE collapses into a simple Ordinary Differential Equation (ODE) representing an energy balance on the entire droplet volume. This is known as the **lumped-capacitance** or **infinite-conductivity model** . The rate of change of the droplet's [total enthalpy](@entry_id:197863) is driven directly by the [net heat flux](@entry_id:155652) at the surface. While simpler, this model is only valid under the specific condition of a small Biot number.

#### The Finite-Conductivity Limit ($\mathrm{Bi}_{\ell} \gg 1$)

When $\mathrm{Bi}_{\ell}$ is large, the internal conductive resistance dominates. Heat is supplied to the surface much faster than it can be conducted into the droplet's core. Consequently, the surface temperature rises rapidly while the center remains cool, leading to the formation of strong radial temperature gradients. In this regime, the assumption of a uniform internal temperature is invalid. A **finite-conductivity model**, which involves solving the full transient heat conduction PDE, is required to accurately resolve the spatial and temporal evolution of the temperature field $T(r,t)$ .

### The Interfacial Boundary Condition: Coupling with the Environment

For the finite-conductivity model, the PDE for the interior must be coupled to the surrounding gas phase via a boundary condition at the moving interface, $r=R(t)$. This condition is a statement of energy conservation at the infinitesimally thin interface.

A fundamental principle at the interface is the continuity of temperature, assuming no [interfacial thermal resistance](@entry_id:156516). This means the temperature of the liquid at the surface is equal to the temperature of the gas at the surface :

$$
T_{\ell}(R(t)^-, t) = T_g(R(t)^+, t) \equiv T_s(t)
$$

where $T_s(t)$ is the interfacial temperature.

The more complex condition is the energy balance, which states that the flux of energy reaching the interface must equal the flux of energy leaving it. Let's consider the fluxes in the outward radial direction. Heat conducted from the liquid interior to the surface is an input to the interface. Heat conducted from the interface into the gas and the energy consumed by evaporation (latent heat) are outputs. The balance is:

$$
\text{Flux from liquid} = \text{Flux to gas} + \text{Flux for evaporation}
$$

The flux from the liquid is given by Fourier's law: $-k_{\ell} \left. \frac{\partial T_{\ell}}{\partial r} \right|_{r=R^-}$. The flux to the gas is similarly $-k_g \left. \frac{\partial T_g}{\partial r} \right|_{r=R^+}$. The flux for evaporation is the mass flux $\dot{m}''$ times the latent heat of vaporization $L_v$. This leads to the detailed energy balance :

$$
-k_{\ell} \left. \frac{\partial T_{\ell}}{\partial r} \right|_{r=R^-} = -k_g \left. \frac{\partial T_g}{\partial r} \right|_{r=R^+} + \dot{m}'' L_v
$$

This equation explicitly couples the internal liquid temperature field with the external gas-phase temperature field.

In many practical simulations, solving the full gas-[phase problem](@entry_id:146764) is avoided by modeling the heat transfer from the gas with an effective convective heat transfer coefficient, $h_g$. The heat flux from the far-field gas (at temperature $T_\infty$) to the surface is given by Newton's law of cooling, $q''_{g \to s} = h_g(T_\infty - T_s)$. The interfacial energy balance then involves three components: heat from the gas (source), heat conducted into the liquid interior (sink), and heat consumed by evaporation (sink). The balance is: (Source) = (Sink 1) + (Sink 2) .

$$
h_g(T_\infty - T_s) = \left( -k_{\ell} \left. \frac{\partial T_{\ell}}{\partial r} \right|_{r=R^-} \right) + \dot{m}'' L_v
$$

Rearranging this gives a **Robin-type (or mixed) boundary condition** for the liquid-phase PDE:

$$
-k_{\ell} \left. \frac{\partial T_{\ell}}{\partial r} \right|_{r=R^-} = h_g(T_\infty - T_s) - \dot{m}'' L_v
$$

The heat [transfer coefficient](@entry_id:264443) $h_g$ is not a constant; it is determined by the properties of the gas and the flow conditions. It is typically calculated from empirical correlations for the **Nusselt number**, $\mathrm{Nu}_g$, which is a dimensionless heat [transfer coefficient](@entry_id:264443). The relationship is :

$$
h_g = \frac{\mathrm{Nu}_g k_g}{D} = \frac{\mathrm{Nu}_g k_g}{2R}
$$

It is crucial to note that the characteristic length scale for external [flow over a sphere](@entry_id:263350) is conventionally its diameter, $D=2R$, not its radius.

### Advanced Interfacial Physics: The Effect of Stefan Flow

The convective model described above is an excellent approximation for low evaporation rates. However, in high-temperature combustion environments, the rate of evaporation can be significant. The outward flow of vapor from the droplet surface, known as **Stefan flow** or "blowing," acts as a convective shield, opposing the inward diffusion of heat from the hot gas. This effect effectively thickens the thermal boundary layer in the gas phase and reduces the net heat transfer to the droplet surface .

To account for this, the classical theory of droplet evaporation introduces the **Spalding heat transfer number**, $B_T$. This dimensionless number represents the ratio of the sensible heat available in the gas phase to drive evaporation to the latent heat required for the phase change :

$$
B_T = \frac{c_{p,g}(T_\infty - T_s)}{L_v}
$$

where $c_{p,g}$ is the [specific heat](@entry_id:136923) of the surrounding gas. A large $B_T$ indicates a strong thermal driving force for evaporation.

Film theory analysis shows that the Stefan flow modifies the gas-side heat flux by a correction factor that depends on $B_T$. The corrected heat flux, $q''_g$, is given by :

$$
q''_g = h_g (T_\infty - T_s) \frac{\ln(1 + B_T)}{B_T}
$$

Since the term $\ln(1+B_T)/B_T$ is always less than 1 for $B_T > 0$, this expression correctly captures the reduction in heat transfer due to blowing. This corrected flux then enters the interfacial energy balance, providing a more accurate model for high-temperature droplet heating and vaporization.

### The Complete Model: Nonlinearity and Time Scales

Assembling all these physical considerations, we can formulate a more complete and realistic model. A significant complexity arises because the [thermophysical properties](@entry_id:1133078) of the liquid, such as thermal conductivity $k_{\ell}$ and specific heat $c_{p,\ell}$, are generally functions of temperature.

When this dependence is included, the governing PDE becomes :

$$
\rho_{\ell} c_{p,\ell}(T) \frac{\partial T}{\partial t} = \frac{1}{r^2} \frac{\partial}{\partial r} \left( r^2 k_{\ell}(T) \frac{\partial T}{\partial r} \right)
$$

This equation is no longer linear. Because the coefficients of the derivatives, $c_{p,\ell}(T)$ and $k_{\ell}(T)$, depend on the solution $T$ itself, the PDE is classified as **quasilinear parabolic**. A major consequence of this nonlinearity is that the principle of superposition no longer applies. Solutions cannot be constructed by summing simpler solutions, and analytical methods are generally intractable. Furthermore, the boundary condition also becomes more strongly nonlinear, as $k_{\ell}(T_s)$ and the evaporation flux $\dot{m}''(T_s)$ are sensitive functions of the unknown surface temperature. This necessitates the use of robust numerical methods for solving the complete problem.

Finally, we consider the temporal behavior. The finite-conductivity model assumes the process is transient. However, under certain conditions, a further simplification is possible. We can compare the characteristic time for thermal diffusion inside the droplet, $t_{\ell} \sim R^2/\alpha_{\ell}$ (where $\alpha_{\ell} = k_{\ell}/\rho_{\ell} c_{p,\ell}$ is the thermal diffusivity), with the characteristic time for the droplet to evaporate, often called the droplet lifetime, $t_e$.

If the internal thermal diffusion time is much shorter than the evaporation time ($t_{\ell} \ll t_e$), the internal temperature profile can adjust almost instantaneously to the slowly changing boundary conditions (i.e., the shrinking radius and evolving surface temperature). In this case, the time derivative term $\partial T / \partial t$ in the heat equation becomes negligible compared to the spatial conduction terms. This is the **[quasi-steady assumption](@entry_id:1130452)** for the internal field. The governing equation simplifies to an ODE in space:

$$
\frac{1}{r^2} \frac{\partial}{\partial r} \left( r^2 k_{\ell}(T) \frac{\partial T}{\partial r} \right) \approx 0
$$

This does not imply the droplet is isothermal; it only implies that the *shape* of the temperature profile is determined by the steady-state balance of conduction at each instant. The criterion $t_{\ell} \ll t_e$ is equivalent to stating that the **Fourier number** based on the evaporation time, $Fo_{\ell} = \alpha_{\ell} t_e / R^2 = t_e / t_{\ell}$, is much greater than unity ($Fo_{\ell} \gg 1$) . This quasi-steady approximation, when valid, can significantly reduce the computational cost of droplet simulations while still retaining the essential physics of internal temperature gradients.