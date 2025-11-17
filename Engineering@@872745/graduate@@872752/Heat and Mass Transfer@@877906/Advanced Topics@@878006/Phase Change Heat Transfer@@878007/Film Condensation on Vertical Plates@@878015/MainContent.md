## Introduction
Condensation, the phase transition from vapor to liquid, is a fundamental process in heat transfer, underpinning the operation of power plants, refrigeration systems, and [thermal management](@entry_id:146042) technologies. Among its various modes, filmwise condensation on a cooled surface represents a classic and crucial scenario. Understanding the intricate interplay between fluid dynamics and heat transport within the forming liquid film is essential for designing and optimizing these systems. However, predicting the rate of condensation is not trivial, as it depends on a coupled relationship between the film's flow under gravity and the heat conducted through it.

This article provides a graduate-level exploration of [film condensation](@entry_id:153396), beginning with the foundational model developed by Wilhelm Nusselt. It aims to bridge the gap between idealized theory and practical complexity. Across the following chapters, you will gain a deep understanding of this important phenomenon.

The journey begins in **Principles and Mechanisms**, where we will systematically derive Nusselt's classical theory for a vertical plate. We will dissect the momentum and energy balances, clarify the core assumptions, and interpret the resulting celebrated solution for the heat transfer coefficient. Following this, **Applications and Interdisciplinary Connections** extends the analysis to the real world. We will explore how performance is affected by different geometries, flow instabilities like waves and turbulence, and crucial multi-physics effects such as the presence of [non-condensable gases](@entry_id:154454) and non-isothermal walls. Finally, **Hands-On Practices** will challenge you to apply these concepts through guided problems, reinforcing your understanding of the theory's implications and limitations.

## Principles and Mechanisms

### The Nusselt Model of Laminar Film Condensation

The condensation of a quiescent, pure vapor onto a surface held at a temperature below the [saturation point](@entry_id:754507) is a cornerstone problem in heat transfer. When the resulting liquid condensate wets the surface, a continuous liquid layer, or film, forms and flows under the influence of gravity. The seminal analysis of this phenomenon was developed by Nusselt in 1916. This section will systematically derive the foundational principles of this classical model for a vertical plate, which, despite its idealizations, provides profound insight into the governing physics.

#### The Physical Picture and Governing Balances

We consider a vertical plate of height $L$ maintained at a uniform temperature $T_w$. This plate is exposed to a pure, saturated vapor at temperature $T_{sat}$, where $T_{sat} > T_w$. The vapor condenses on the plate, forming a [liquid film](@entry_id:260769) that flows downward. Let $x$ be the coordinate measured vertically downward from the leading edge of the plate ($x=0$), and let $y$ be the coordinate normal to the plate, extending into the [liquid film](@entry_id:260769). The local thickness of the film at position $x$ is denoted by $\delta(x)$.

The analysis rests on a coupled solution of the momentum and energy conservation equations within the [liquid film](@entry_id:260769). The rate of film growth is dictated by the energy balance: heat transferred from the liquid-vapor interface to the wall releases the latent heat necessary for condensation. The rate at which the film flows downward is governed by the momentum balance: a competition between the [gravitational force](@entry_id:175476) pulling the film down and the [viscous shear stress](@entry_id:270446) resisting this motion.

#### The Driving Force for Film Motion

A crucial first step in formulating the momentum balance is to correctly identify the net driving force acting on the liquid film. One might intuitively assume the force is simply the weight of the liquid, given by a volumetric term $\rho_l g$, where $\rho_l$ is the liquid density and $g$ is the gravitational acceleration. However, the liquid film is immersed in the surrounding vapor, which exerts a hydrostatic pressure. This gives rise to a [buoyant force](@entry_id:144145) that counteracts the liquid's weight.

To formalize this, we consider the [momentum equation](@entry_id:197225) for the liquid in the streamwise ($x$) direction. For a steady, slow-moving film (where inertia is negligible), the equation simplifies to a balance between the pressure gradient, gravity, and viscous forces:
$$ \mu_l \frac{\partial^2 u}{\partial y^2} - \frac{\partial p_l}{\partial x} + \rho_l g = 0 $$
where $u$ is the liquid velocity, $\mu_l$ is the liquid viscosity, and $p_l$ is the pressure within the liquid.

To determine the pressure gradient $\frac{\partial p_l}{\partial x}$, we invoke two conditions. First, for a thin film, the pressure variation across its thickness is negligible, so $p_l$ is a function of $x$ only. Second, at the planar liquid-vapor interface ($y = \delta(x)$), pressure must be continuous. Therefore, the pressure in the liquid film at any given $x$ is equal to the pressure in the vapor at that same location, $p_l(x) = p_v(x)$. This implies their gradients are also equal: $\frac{\partial p_l}{\partial x} = \frac{\partial p_v}{\partial x}$.

Since the vapor is quiescent, it is in hydrostatic equilibrium, where its own weight is balanced by a pressure gradient. With the $x$-axis pointing downward, this balance is $\frac{\partial p_v}{\partial x} = \rho_v g$, where $\rho_v$ is the vapor density. Substituting this back into the liquid [momentum equation](@entry_id:197225) yields:
$$ \mu_l \frac{\partial^2 u}{\partial y^2} + (\rho_l - \rho_v) g = 0 $$
This confirms that the effective volumetric driving force for the film is not merely the liquid weight, but the **[buoyancy force](@entry_id:154088)**, $(\rho_l - \rho_v)g$ [@problem_id:2485285]. For most [condensation](@entry_id:148670) scenarios, the vapor density is much smaller than the liquid density ($\rho_v \ll \rho_l$), so this term is often approximated as $\rho_l g$. However, the $(\rho_l - \rho_v)$ form is more rigorous and essential for near-critical conditions.

#### Derivation of the Velocity Profile

With the momentum equation established, we can solve for the [velocity profile](@entry_id:266404) $u(y)$ by integrating twice. The boundary conditions are:
1.  **No-slip condition** at the wall: $u(y=0) = 0$.
2.  **Negligible interfacial shear** at the liquid-vapor interface: $\frac{\partial u}{\partial y}|_{y=\delta} = 0$. This assumes the quiescent vapor exerts no drag on the film.

Integrating the momentum equation once gives:
$$ \frac{\partial u}{\partial y} = -\frac{(\rho_l - \rho_v)g}{\mu_l} y + C_1 $$
Applying the zero-shear condition at $y=\delta$ determines the constant $C_1 = \frac{(\rho_l - \rho_v)g}{\mu_l}\delta$. Integrating a second time gives:
$$ u(y) = \frac{(\rho_l - \rho_v)g}{\mu_l} \left( \delta y - \frac{y^2}{2} \right) + C_2 $$
The no-slip condition at $y=0$ yields $C_2=0$. The final [velocity profile](@entry_id:266404) is parabolic:
$$ u(y) = \frac{(\rho_l - \rho_v)g}{\mu_l} \left( \delta(x) y - \frac{y^2}{2} \right) $$
From this, we can calculate the total mass flow rate per unit width of the plate, $\dot{m}'(x)$, by integrating the mass flux $\rho_l u(y)$ across the film thickness:
$$ \dot{m}'(x) = \int_0^{\delta(x)} \rho_l u(y) dy = \frac{\rho_l (\rho_l - \rho_v)g}{3\mu_l} \delta(x)^3 $$
This result elegantly links the hydrodynamic aspect of the problem ([mass flow rate](@entry_id:264194)) to the geometric property of the film (its thickness).

#### The Energy Balance and Film Growth

The film grows as vapor condenses at the interface. This [phase change](@entry_id:147324) releases an amount of energy equal to the [latent heat of vaporization](@entry_id:142174), $h_{fg}$. For the film to remain at a steady thickness at any given $x$, this released energy must be transported away from the interface, through the [liquid film](@entry_id:260769), and into the cooled wall.

The Nusselt model assumes that heat transfer across the thin film is dominated by pure conduction in the transverse ($y$) direction. The local heat flux, $q''(x)$, is therefore given by Fourier's law:
$$ q''(x) = k_l \frac{T_{sat} - T_w}{\delta(x)} $$
where $k_l$ is the thermal conductivity of the liquid.

Now, consider a differential control volume along the plate of length $dx$. The increase in mass flow rate over this length is $d\dot{m}'$. The [latent heat](@entry_id:146032) released due to this mass addition is $h_{fg} d\dot{m}'$. This must be balanced by the heat conducted into the wall over the area $dx \times 1$. Thus, we have the crucial energy balance:
$$ \frac{d\dot{m}'}{dx} h_{fg} = q''(x) = k_l \frac{T_{sat} - T_w}{\delta(x)} $$
This equation connects the rate of film growth (hydrodynamics) to the rate of heat removal (thermodynamics). By substituting our previously derived expression for $\dot{m}'(\delta)$, we can formulate a single differential equation for the film thickness $\delta(x)$.

### The Core Assumptions of Nusselt Theory

The elegant simplicity of the Nusselt analysis is enabled by a series of judicious assumptions. It is critical for the student and practitioner to understand these idealizations and the conditions under which they are justified [@problem_id:2485289].

#### The Hydrodynamic Assumptions

1.  **Laminar Flow and Negligible Inertia:** The theory assumes the film flow is laminar and that inertial forces within the film are negligible compared to viscous and gravitational forces. This is the "[creeping flow](@entry_id:263844)" or Stokes flow approximation. Its validity can be assessed by comparing the magnitude of an inertial term, like $\rho_l u \frac{\partial u}{\partial x} \sim \rho_l u_*^2/L$, to a viscous term, $\mu_l \frac{\partial^2 u}{\partial y^2} \sim \mu_l u_*/\delta^2$. The ratio of these forces scales with the film Reynolds number $\mathrm{Re}_\delta = \rho_l u_* \delta / \mu_l$ and the [aspect ratio](@entry_id:177707) $\delta/L$, as $\mathrm{Re}_\delta (\delta/L)$. For thin films where this product is much less than unity, the assumption is justified. For typical condensation of water, this condition holds well within the laminar regime [@problem_id:2485289].

2.  **Negligible Interfacial Shear:** The model assumes the liquid-vapor interface is free of shear stress ($\tau_i = \mu_l \frac{\partial u}{\partial y}|_{y=\delta} = 0$). This is an excellent approximation when the vapor is quiescent (not flowing parallel to the plate) and its density $\rho_v$ is much lower than the liquid density $\rho_l$. The drag exerted by the low-density vapor is insignificant compared to the internal shear driven by the film's own weight, which scales as $\rho_l g \delta$ [@problem_id:2485289].

#### The Thermodynamic and Heat Transfer Assumptions

1.  **Pure, Saturated Vapor and Negligible Interfacial Resistance:** The theory assumes the vapor is pure (free of [non-condensable gases](@entry_id:154454)) and saturated. Under the principle of [local thermodynamic equilibrium](@entry_id:139579) at the interface, this fixes the interfacial temperature $T_i$ to be exactly the saturation temperature corresponding to the system pressure, $T_{sat}(P)$. This implies there is no thermal resistance on the vapor side of the interface; the entire temperature drop occurs across the liquid film [@problem_id:2485327].

2.  **Negligible Condensate Subcooling:** Condensate forms at the interface at $T_{sat}$ and cools as it travels down the plate towards the wall temperature $T_w$. This change in the liquid's sensible heat is neglected in the classical theory. The validity of this assumption is measured by the **Jakob number**, $\mathrm{Ja}$:
    $$ \mathrm{Ja} = \frac{c_{p,l} (T_{sat} - T_w)}{h_{fg}} $$
    The Jakob number represents the ratio of the maximum sensible heat that can be absorbed by the liquid to the latent heat released during condensation. For most applications involving water and other common fluids, $\mathrm{Ja} \ll 1$, indicating that the [energy transport](@entry_id:183081) is overwhelmingly dominated by [latent heat](@entry_id:146032). For water condensing at [atmospheric pressure](@entry_id:147632) with a $20\,\mathrm{K}$ temperature difference, $\mathrm{Ja} \approx 0.037$, confirming this is an excellent assumption [@problem_id:2485289].

3.  **Dominance of Transverse Conduction:** The [energy equation](@entry_id:156281) in the film simplifies to pure one-dimensional conduction, $k_l \frac{d^2T}{dy^2} = 0$, leading to a linear temperature profile. This requires neglecting heat advection in the flow direction ($x$) and heat conduction in the flow direction. An [order-of-magnitude analysis](@entry_id:184866) shows that the ratio of streamwise advection to transverse conduction scales as $\mathrm{Pe}_\delta (\delta/L)$, where $\mathrm{Pe}_\delta$ is the film Peclet number. This ratio can be shown to be proportional to the Jakob number. Therefore, the condition $\mathrm{Ja} \ll 1$ simultaneously justifies neglecting both condensate [subcooling](@entry_id:142766) and streamwise advection in the [energy balance](@entry_id:150831) [@problem_id:2485289].

#### Why the Prandtl Number is Absent

A notable feature of the Nusselt solution is the absence of the liquid Prandtl number, $\mathrm{Pr}_l = \mu_l c_{p,l} / k_l$. The Prandtl number represents the ratio of [momentum diffusivity](@entry_id:275614) to [thermal diffusivity](@entry_id:144337) and is a key parameter in most [convective heat transfer](@entry_id:151349) problems where the velocity and temperature fields are coupled.

The reason for its absence in this specific model lies in the profound decoupling of the momentum and energy equations afforded by the core assumptions [@problem_id:2485331].
- The momentum equation is solved independently of temperature because the assumption of constant properties (or negligible dependence on temperature) is made, and more importantly, inertia is neglected, which removes the convective terms that would link it to the energy equation. The resulting velocity profile depends only on $\mu_l$ and $\rho_l$.
- The [energy equation](@entry_id:156281), by neglecting advection (justified by $\mathrm{Ja} \ll 1$), reduces to pure conduction. This simplified equation contains the thermal conductivity $k_l$, but it entirely eliminates the specific heat $c_{p,l}$.

Since the [specific heat](@entry_id:136923) $c_{p,l}$ does not appear in either of the simplified governing equations, the dimensionless group $\mathrm{Pr}_l$ cannot be formed and plays no role in the final solution. This is a direct consequence of treating the problem as a pure conduction problem superimposed on a viscosity-gravity driven flow, rather than a true convection problem.

### The Nusselt Solution and Its Implications

By combining the hydrodynamic and thermodynamic balances, we can derive the explicit solution for the film's evolution and the resulting heat transfer.

#### The Film Thickness and Heat Transfer Coefficient

We start by equating the two expressions for the derivative of the mass flow rate, $\frac{d\dot{m}'}{dx}$:
$$ \frac{d\dot{m}'}{dx} = \frac{d}{dx} \left( \frac{\rho_l (\rho_l - \rho_v)g}{3\mu_l} \delta^3 \right) = \frac{\rho_l (\rho_l - \rho_v)g}{\mu_l} \delta^2 \frac{d\delta}{dx} $$
$$ \frac{d\dot{m}'}{dx} = \frac{k_l (T_{sat} - T_w)}{h_{fg}\delta} $$
Equating and rearranging these gives a separable [ordinary differential equation](@entry_id:168621) for $\delta(x)$:
$$ \delta^3 \frac{d\delta}{dx} = \frac{\mu_l k_l (T_{sat} - T_w)}{\rho_l (\rho_l - \rho_v)g h_{fg}} $$
We integrate this equation from the top of the plate, where the film begins to form.

#### The Leading Edge Condition ($\delta(0)=0$)

The choice of the integration constant is determined by the physical condition at the leading edge of the plate, $x=0$. Since no condensate flows onto the plate from above, the mass flow rate at the starting point must be zero: $\dot{m}'(0) = 0$. From our expression relating mass flow to film thickness, $\dot{m}' \propto \delta^3$, this directly implies the boundary condition $\mathbf{\delta(0) = 0}$.

This mathematical condition has a deep physical meaning and withstands scrutiny even when considering microscopic effects [@problem_id:2485306]. On a perfectly [wetting](@entry_id:147044) surface, [intermolecular forces](@entry_id:141785) may create a nanometer-scale "precursor film" ahead of the main hydrodynamic film. However, at the macroscopic scale of the Nusselt theory, this precursor thickness is asymptotically negligible, making $\delta(0)=0$ the correct macroscopic boundary condition. On partially [wetting](@entry_id:147044) surfaces, [condensation](@entry_id:148670) begins as discrete droplets that coalesce to form a continuous film at some distance $x_0 > 0$. In this case, the Nusselt analysis applies for $x > x_0$ with a "virtual origin," where the boundary condition becomes $\delta(x_0)=0$.

With $\delta(0)=0$, integration yields:
$$ \frac{\delta(x)^4}{4} = \frac{\mu_l k_l (T_{sat} - T_w) x}{\rho_l (\rho_l - \rho_v)g h_{fg}} $$
Solving for the film thickness:
$$ \delta(x) = \left[ \frac{4 \mu_l k_l (T_{sat} - T_w) x}{\rho_l (\rho_l - \rho_v)g h_{fg}} \right]^{1/4} $$
The local heat transfer coefficient, $h_x = q''(x)/(T_{sat}-T_w)$, is then:
$$ h_x = \frac{k_l}{\delta(x)} = \left[ \frac{\rho_l (\rho_l - \rho_v)g h_{fg} k_l^3}{4 \mu_l (T_{sat} - T_w) x} \right]^{1/4} $$
The average heat transfer coefficient over the entire plate length $L$, $\bar{h}_L$, is found by integrating $h_x$ from $0$ to $L$:
$$ \bar{h}_L = \frac{1}{L} \int_0^L h_x dx = \frac{4}{3} h_L = 0.943 \left[ \frac{\rho_l (\rho_l - \rho_v)g h_{fg} k_l^3}{\mu_l (T_{sat} - T_w) L} \right]^{1/4} $$
This celebrated result is the cornerstone of [film condensation](@entry_id:153396) analysis.

#### Parametric Dependence and Physical Interpretation

The Nusselt solution reveals how material properties influence the condensation process [@problem_id:2485305]. The film thickness $\delta(x)$ scales as:
-   $\delta \propto k_l^{1/4}$: A higher thermal conductivity ($k_l$) enhances heat removal through the film. This allows for a higher rate of [condensation](@entry_id:148670) to be sustained, which in turn leads to a **thicker** film.
-   $\delta \propto \mu_l^{1/4}$: A higher liquid viscosity ($\mu_l$) means the fluid is more resistant to flow. To drain the same amount of condensate, the film must become slower and consequently **thicker**.
-   $\delta \propto h_{fg}^{-1/4}$: A higher latent heat ($h_{fg}$) means that more energy is released for each unit of mass that condenses. To balance a given heat flux conducted through the film, a smaller mass of vapor needs to condense, resulting in a **thinner** film.

These relationships provide valuable physical intuition for how different fluids will behave during condensation. For example, fluids with low viscosity and high [latent heat](@entry_id:146032) are conducive to forming thin films and thus achieving high heat transfer coefficients.

### Refinements and Regimes of Validity

The classical Nusselt theory provides a powerful baseline, but its range of applicability is limited by its assumptions.

#### Flow Regimes and the Film Reynolds Number

The theory assumes a smooth, laminar film. In reality, as the film flows down the plate, it accumulates mass, increases in thickness, and accelerates. At a certain point, the flow can become unstable. To characterize the state of the flow, a film Reynolds number is defined. The standard definition uses the [hydraulic diameter](@entry_id:152291) ($D_h = 4\delta$) as the characteristic length:
$$ \mathrm{Re}_\delta = \frac{\rho_l \bar{u} D_h}{\mu_l} = \frac{4 \rho_l \bar{u} \delta}{\mu_l} = \frac{4\dot{m}'}{\mu_l} $$
Since the mass flow rate $\dot{m}'$ increases with $x$, the Reynolds number is largest at the bottom of the plate, $x=L$. The flow regime is therefore determined by $\mathrm{Re}_L$. Experimental observations have established the following criteria [@problem_id:2485318]:
-   **$\mathrm{Re}_L \lesssim 30$**: The film is smooth and laminar. The Nusselt theory is highly accurate.
-   **$30 \lesssim \mathrm{Re}_L \lesssim 1800$**: The film becomes wavy, but the underlying flow remains laminar. These waves create additional mixing near the interface, enhancing heat transfer by 10-20% above the Nusselt prediction. The classical theory is no longer exact but serves as a good conservative estimate.
-   **$\mathrm{Re}_L \gtrsim 1800$**: The flow transitions to turbulence. The mechanisms of momentum and [heat transport](@entry_id:199637) change dramatically, and the laminar Nusselt theory is no longer applicable. Turbulent film correlations must be used instead.

#### The Effect of Variable Properties: The Film Temperature

The classical theory assumes all [fluid properties](@entry_id:200256) are constant. In reality, properties like viscosity $\mu_l$ and thermal conductivity $k_l$ can vary significantly with temperature across the film (from $T_w$ to $T_{sat}$). A common engineering practice is to use the Nusselt correlation but evaluate all properties at a single, representative **film temperature**, defined as the [arithmetic mean](@entry_id:165355):
$$ T_f = \frac{T_w + T_{sat}}{2} $$
A more rigorous analysis reveals the level of accuracy of this simplification [@problem_id:2485281]. Because the temperature profile across the film is nearly linear, evaluating $k_l$ at the midpoint $T_f$ is a very accurate approximation for the integral-average conductivity, with an error that is second-order in the temperature difference $\Delta T = T_{sat} - T_w$. However, the [effective viscosity](@entry_id:204056) is part of a weighted integral, and the latent heat is properly evaluated at the interface temperature $T_{sat}$. Using $T_f$ for these properties introduces errors that are first-order in $\Delta T$. Nonetheless, for moderate temperature differences, evaluation at the film temperature provides a convenient and reasonably accurate correction for property variations.

### Beyond the Ideal Model: Complicating Effects

#### The Influence of Non-Condensable Gases

The assumption of a pure vapor is critical. The presence of even a small amount of a [non-condensable gas](@entry_id:155037) (like air in steam) can drastically reduce the [condensation heat transfer](@entry_id:156405) rate. As the vapor flows towards the cold surface to condense, the [non-condensable gas](@entry_id:155037), which cannot pass into the liquid phase, accumulates at the interface. This forms a diffusion boundary layer.

For the vapor to reach the interface, it must diffuse through this stagnant layer of [non-condensable gas](@entry_id:155037). This introduces a significant **[mass transfer resistance](@entry_id:151498)**. The consequence is that the [partial pressure](@entry_id:143994) of the vapor at the interface, $p_{v,i}$, becomes lower than the total system pressure, $P$. According to the principle of [local thermodynamic equilibrium](@entry_id:139579), the interfacial temperature $T_i$ is the saturation temperature corresponding to this lower [partial pressure](@entry_id:143994), $T_i = T_{sat}(p_{v,i})$. Therefore, the presence of non-condensables forces the interfacial temperature to drop below the bulk saturation temperature, $T_i  T_{sat}(P)$ [@problem_id:2485327]. This reduces the effective temperature difference across the liquid film, $(T_i - T_w)$, thereby lowering the heat flux and the overall condensation rate.

#### A More General Model: Coupled Heat, Mass, and Kinetic Resistances

A complete model for condensation in the presence of non-condensables must account for a series of resistances [@problem_id:2485308]:
1.  **Gas Film Diffusion Resistance:** The resistance to vapor diffusing through the [non-condensable gas](@entry_id:155037) layer.
2.  **Interfacial Kinetic Resistance:** A microscopic resistance to [phase change](@entry_id:147324) at the molecular level, which can be significant at low pressures or for very high [condensation](@entry_id:148670) rates.
3.  **Liquid Film Conduction Resistance:** The thermal resistance of the [liquid film](@entry_id:260769), as described by Nusselt theory.

The problem becomes one of coupled [heat and mass transfer](@entry_id:154922). The interfacial temperature $T_i$ and the vapor concentration at the interface are no longer known a priori but must be found by simultaneously satisfying the heat balance and the [mass balance](@entry_id:181721) across all three resistance domains. The resulting system of equations is typically implicit and must be solved iteratively.

#### Dropwise versus Filmwise Condensation: The Role of Wettability

The entire framework discussed in this chapter applies to **filmwise [condensation](@entry_id:148670)**, which occurs on surfaces that are well-wetted by the condensate. The mode of [condensation](@entry_id:148670) is fundamentally determined by the [surface wettability](@entry_id:151424), which is governed by [interfacial thermodynamics](@entry_id:203339) and quantified by the [contact angle](@entry_id:145614) $\theta_e$ [@problem_id:2485319].
-   **Filmwise Condensation:** Occurs on high-energy, hydrophilic surfaces where the liquid readily spreads ($\theta_e  90^\circ$). A continuous film forms, providing a stable but growing thermal resistance.
-   **Dropwise Condensation:** Occurs on low-energy, [hydrophobic surfaces](@entry_id:148780) where the liquid does not spread ($\theta_e > 90^\circ$). Condensate forms as discrete droplets.

The mechanisms of [dropwise condensation](@entry_id:152329) are entirely different. Heat transfer occurs via conduction through a dynamic population of droplets. As droplets grow and coalesce, they are shed from the surface by gravity, sweeping a path and exposing fresh, highly effective condensing area. This cycle of nucleation, growth, and renewal is inherently transient and three-dimensional.

Because there is no steady, continuous film, the fundamental assumptions of the Nusselt theory are violated, and it is completely inapplicable to [dropwise condensation](@entry_id:152329). Critically, due to the efficient heat transfer through small droplets and the rapid surface renewal, the heat transfer coefficients in [dropwise condensation](@entry_id:152329) are typically an [order of magnitude](@entry_id:264888) **higher** than in filmwise condensation under the same conditions. This has motivated extensive research into creating durable [hydrophobic surfaces](@entry_id:148780) to promote this highly efficient mode of heat transfer.