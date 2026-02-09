## Introduction
Internal convective heat transfer is a fundamental process at the heart of countless engineering systems, from compact heat exchangers and electronic cooling solutions to large-scale power generation plants. A critical aspect of designing these systems is understanding how a fluid's temperature evolves as it flows through a heated duct. This article focuses on a specific but widely applicable scenario: fully developed internal flow subjected to a constant heat flux at the wall. This condition provides a powerful analytical framework for predicting thermal performance and understanding the interplay between fluid motion and heat transport.

This article aims to bridge the gap between abstract theory and practical application by providing a detailed exploration of the constant heat flux model. Readers will gain a robust understanding of the underlying physics and the mathematical tools used for analysis.

The journey begins in the **Principles and Mechanisms** chapter, where we will derive the signature characteristics of this flow regime, including the linear temperature rise and the constant Nusselt number for laminar flow. Next, the **Applications and Interdisciplinary Connections** chapter broadens our perspective, contrasting this model with other boundary conditions and extending its principles to complex geometries, turbulent flows, and frontier areas like microfluidics and liquid metal cooling. Finally, the **Hands-On Practices** chapter solidifies this knowledge through a series of guided problems, translating theoretical concepts into tangible analytical skills. Together, these chapters offer a complete guide to mastering the theory and application of fully developed convection with constant heat flux.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms governing convective heat transfer in internal flows that have reached a **thermally fully developed** state. We will focus on a specific, and analytically tractable, boundary condition: the application of a **uniform and constant heat flux** at the duct wall. This condition, often abbreviated as **CHF** and mathematically known as a Neumann-type boundary condition, is an excellent model for processes like electrical resistance heating, radiative heating, or any scenario where the rate of heat addition per unit area to the fluid is constant along the flow direction.

### The Thermally Fully Developed Condition for Constant Heat Flux

As a fluid enters a heated duct, its temperature profile evolves with axial distance. The region over which this evolution occurs is known as the **thermal entrance region**. In this region, the shape of the temperature profile changes at each cross-section. However, sufficiently far from the inlet, the influence of the initial temperature profile diminishes, and the temperature profile approaches a characteristic shape that remains constant in a dimensionless sense. This downstream region is termed the **thermally fully developed region**.

The specific definition of this state depends on the thermal boundary condition. For a constant wall heat flux, the thermally fully developed condition is formally defined by the invariance of a dimensionless temperature profile [@problem_id:2473398]. If we define a dimensionless temperature $\theta$ that captures the shape of the profile relative to local characteristic temperatures, such as the wall temperature $T_w(x)$ and the bulk mean temperature $T_b(x)$:

$$
\theta(y,z) = \frac{T_w(x) - T(x,y,z)}{T_w(x) - T_b(x)}
$$

where $x$ is the axial coordinate and $(y,z)$ are the transverse coordinates, the condition for a thermally fully developed field is that this shape no longer changes with $x$:

$$
\frac{\partial \theta}{\partial x} = 0
$$

This seemingly abstract definition has profound and practical consequences. One of the most important is that the local **convective heat transfer coefficient**, $h$, becomes constant and independent of the axial position $x$. Recall that $h$ is defined by Newton's law of cooling:

$$
q'' = h (T_w - T_b)
$$

Since the wall heat flux $q''$ is constant by definition of the boundary condition, and $h$ becomes constant in the fully developed region, it directly implies that the temperature difference between the wall and the bulk fluid, $T_w - T_b$, must also be a constant, independent of $x$ [@problem_id:2490102]. This is a cornerstone property of the CHF fully developed state.

The transition from a developing to a fully developed state is governed by the competition between axial convection and radial heat diffusion. This is quantified by the **Graetz number**, $Gz$, a dimensionless parameter defined as [@problem_id:2490101]:

$$
Gz = \mathrm{Re}_D \mathrm{Pr} \frac{D}{x}
$$

where $\mathrm{Re}_D$ is the Reynolds number, $\mathrm{Pr}$ is the Prandtl number, $D$ is the duct diameter, and $x$ is the axial distance from the start of heating. The thermal entrance region is associated with large values of $Gz$, while the fully developed region corresponds to small values of $Gz$. For engineering purposes, the flow is often considered nearly fully developed when $Gz$ drops below a certain value, for example, $Gz \approx 10$ [@problem_id:2490101].

### Macroscopic Energy Balance: The Linear Rise in Temperature

To understand how the fluid temperature evolves along the duct, we apply the first law of thermodynamics to a differential control volume of the fluid, extending across the duct's cross-sectional area $A$ and having an infinitesimal length $dx$. For steady flow, the rate of energy entering the control volume must equal the rate of energy leaving it. Energy enters through advection at position $x$ and through the wall surface. Energy leaves through advection at $x+dx$.

The rate of heat transfer from the wall is the product of the constant heat flux $q''$ and the surface area $P \cdot dx$, where $P$ is the wetted perimeter of the duct. The net rate of energy gain by advection is the change in the enthalpy flow rate. For an incompressible fluid with constant specific heat $c_p$, the enthalpy flow rate is given by $\dot{m} c_p T_b(x)$, where $\dot{m}$ is the mass flow rate and $T_b(x)$ is the **bulk mean temperature** (also called the mixed-mean temperature). This temperature represents the average enthalpy of the fluid, properly weighted by the velocity profile. The energy balance is therefore:

$$
(\dot{m} c_p T_b)|_x + q'' P dx = (\dot{m} c_p T_b)|_{x+dx}
$$

Rearranging and taking the limit as $dx \to 0$ gives a simple differential equation for the bulk mean temperature [@problem_id:2490099, @problem_id:2490092]:

$$
\dot{m} c_p \frac{dT_b}{dx} = q'' P
$$

Solving for the axial temperature gradient, we find:

$$
\frac{dT_b}{dx} = \frac{q'' P}{\dot{m} c_p}
$$

Since $q''$, $P$, $\dot{m}$, and $c_p$ are all constants, the axial gradient of the bulk mean temperature is also constant. This means that **the bulk mean temperature $T_b(x)$ increases linearly with axial position $x$**. It is crucial to recognize that this result stems directly from the macroscopic energy balance and is valid everywhere along the heated length, including the thermal entrance region [@problem_id:2490092].

Combining our findings, we have two key behaviors in the thermally fully developed region:
1. $T_b(x)$ increases linearly with $x$.
2. $T_w(x) - T_b(x)$ is constant.

It logically follows that the wall temperature, $T_w(x)$, must also increase linearly with $x$ and, importantly, at the *same rate* as the bulk mean temperature [@problem_id:2490088]. Every point in the fluid cross-section sees its temperature rise linearly and identically with axial distance, a state that can be pictured as the entire temperature profile shifting uniformly upward in temperature as it moves down the duct. This leads to a fundamental characteristic of the fully developed CHF state: the axial temperature gradient is uniform across the cross-section, i.e., $\frac{\partial T}{\partial x} = \frac{dT_b}{dx} = \text{constant}$ [@problem_id:2490102].

As a practical application of this linear temperature rise, consider a scenario where water flows through a heated tube. Given a mass flow rate $\dot{m} = 0.200 \text{ kg/s}$, a specific heat $c_p = 4180 \text{ J/(kg K)}$, a tube diameter $D = 0.020 \text{ m}$, and a constant wall heat flux $q'' = 8000 \text{ W/m}^2$, we can calculate the temperature rise over a length $L = 8.00 \text{ m}$. The perimeter is $P = \pi D$. Integrating the energy balance equation from inlet to outlet gives [@problem_id:2490099]:

$$
T_{b,out} - T_{b,in} = \frac{q'' P L}{\dot{m} c_p} = \frac{(8000 \text{ W/m}^2) (\pi \cdot 0.020 \text{ m}) (8.00 \text{ m})}{(0.200 \text{ kg/s}) (4180 \text{ J/(kg K)})} \approx 4.81 \text{ K}
$$
If the water enters at $300.0 \text{ K}$, it will exit at approximately $304.8 \text{ K}$.

### The Governing Equation and the Nusselt Number for Laminar Flow

To determine the value of the constant heat transfer coefficient $h$ (and thus the Nusselt number), we must solve for the shape of the temperature profile. This requires moving from the macroscopic energy balance to the local, differential energy equation. For steady, hydrodynamically fully developed flow in a straight duct with constant properties and negligible axial conduction, the energy equation is [@problem_id:2473398]:

$$
\rho c_p u(y,z) \frac{\partial T}{\partial x} = k \left( \frac{\partial^2 T}{\partial y^2} + \frac{\partial^2 T}{\partial z^2} \right)
$$

This equation states that the energy transported into a point by fluid motion (advection) is balanced by the energy diffusing away via conduction in the transverse directions. The assumption of negligible axial conduction is typically justified for flows with a high Péclet number ($\mathrm{Pe} = \mathrm{Re} \cdot \mathrm{Pr}$), which is common in many engineering applications. However, a deeper insight reveals that for the strictly defined thermally fully developed state under CHF, the axial conduction term, $k \frac{\partial^2 T}{\partial x^2}$, is identically zero anyway, because $\frac{\partial T}{\partial x}$ is constant [@problem_id:2490097]. Therefore, neglecting it is not just an approximation but becomes an exact feature of this idealized state.

Let us now solve this equation for the canonical case: steady, laminar flow in a circular tube of radius $R$. The velocity profile is the well-known parabolic Poiseuille profile, $u(r) = 2 u_m (1 - r^2/R^2)$, where $u_m$ is the mean velocity. The energy equation in cylindrical coordinates becomes [@problem_id:2490083]:

$$
\rho c_p \left[ 2 u_m \left(1 - \frac{r^2}{R^2}\right) \right] \frac{\partial T}{\partial x} = \frac{k}{r} \frac{\partial}{\partial r} \left( r \frac{\partial T}{\partial r} \right)
$$

We replace the axial temperature gradient $\frac{\partial T}{\partial x}$ with the constant expression we derived from the energy balance, $\frac{dT_b}{dx} = \frac{q'' (2\pi R)}{\rho c_p u_m (\pi R^2)} = \frac{2q''}{\rho c_p u_m R}$. This transforms the partial differential equation into an ordinary differential equation for the radial temperature profile:

$$
\frac{d}{dr} \left( r \frac{dT}{dr} \right) = \frac{4 q''}{k R} \left( r - \frac{r^3}{R^2} \right)
$$

Integrating this equation twice with respect to $r$ and applying the boundary conditions of symmetry at the centerline ($\frac{dT}{dr}|_{r=0}=0$) and constant flux at the wall ($k \frac{dT}{dr}|_{r=R}=q''$) yields the temperature profile relative to the wall temperature, $T_w$. The next step is to compute the wall-to-bulk temperature difference, $T_w - T_b$, by integrating the product of the velocity and temperature profiles over the cross-section. After performing this integration, a remarkably simple result emerges [@problem_id:2490083]:

$$
T_w - T_b = \frac{11}{24} \frac{q'' R}{k}
$$

With this temperature difference, we can find the heat transfer coefficient:

$$
h = \frac{q''}{T_w - T_b} = \frac{q''}{\frac{11}{24} \frac{q'' R}{k}} = \frac{24k}{11R}
$$

Finally, we calculate the Nusselt number, $\mathrm{Nu}$, using the tube diameter $D=2R$ as the characteristic length:

$$
\mathrm{Nu} = \frac{hD}{k} = \frac{(\frac{24k}{11R})(2R)}{k} = \frac{48}{11} \approx 4.364
$$

This is a classic result in convective heat transfer. It shows that for fully developed laminar flow in a circular tube with constant wall heat flux, the **Nusselt number is a constant**, independent of the Reynolds number and Prandtl number [@problem_id:2490102, @problem_id:2490088]. This constant value is a function only of the duct's cross-sectional geometry (a circle) and the type of thermal boundary condition (CHF). It is essential to distinguish this from the result for a constant wall temperature (CWT) boundary condition, for which the Nusselt number is $\mathrm{Nu} = 3.66$ [@problem_id:2490102]. The different boundary conditions produce different temperature profile shapes, leading to different constant values for $\mathrm{Nu}$.

### Extensions and Practical Considerations

#### Non-Circular Ducts

For ducts with non-circular cross-sections, the principles remain the same, but the resulting Nusselt number changes. The value of $\mathrm{Nu}$ is highly dependent on the specific geometry in the laminar flow regime. For instance, for flow between two infinite parallel plates (a 2D channel), the fully developed Nusselt number for CHF on both walls is approximately $8.235$. The notion that a single Nusselt number applies to all duct shapes with the same hydraulic diameter is incorrect for laminar flow [@problem_id:2490102]. However, the **hydraulic diameter**, $D_h = 4A/P$, remains the standard and conventional characteristic length used for defining the Reynolds and Nusselt numbers for non-circular ducts, allowing for a consistent basis of comparison [@problem_id:2490088, @problem_id:2473398].

#### Relating Theory to Experiment

The theoretical framework can be directly connected to experimental measurements. Imagine an experiment where a fluid flows through a tube with a known diameter $D$, wrapped in an electrical heater that provides a known heat input per unit length, $q'$. This linear heat rate can be converted to a surface heat flux via $q'' = q' / (\pi D)$. If thermocouples are used to measure the wall temperature $T_w$ and the bulk fluid temperature $T_b$ in the fully developed region, the difference $T_w-T_b$ will be constant. The heat transfer coefficient can then be inferred directly [@problem_id:2490098]:

$$
h = \frac{q''}{T_w - T_b}
$$

From this, the experimental Nusselt number, $\mathrm{Nu} = hD/k$, can be computed and compared to theoretical predictions.

#### Effects of Viscous Dissipation and Internal Heat Generation

The classic derivation assumes that heat is added only at the wall. In some scenarios, other thermal effects can be important.

**Viscous Dissipation:** For highly viscous fluids or flows with very high velocity gradients, the work done by viscous forces can be significant, converting mechanical energy into thermal energy throughout the fluid. This effect is known as **viscous dissipation** or viscous heating. When included in the energy equation, it adds a source term proportional to the square of the velocity gradient. The relative importance of viscous heating is quantified by the **Brinkman number**, $Br$. For flow between parallel plates with viscous heating, the Nusselt number is no longer constant but becomes a function of the Brinkman number. A detailed derivation shows that for this case [@problem_id:2490096]:

$$
\mathrm{Nu} = \frac{140}{17 + 27 Br}
$$

This demonstrates that as viscous heating becomes more significant (increasing $Br$), the temperature difference between the wall and the bulk fluid is altered, leading to a decrease in the effective Nusselt number.

**Internal Heat Generation:** Similarly, if the fluid itself generates heat, for example, through a chemical reaction or nuclear process, this must be included as a volumetric source term, $q'''$, in the energy equation. For laminar flow in a circular tube with both a constant wall heat flux $q''$ and uniform internal generation $q'''$, the resulting Nusselt number, which is defined based on the wall heat flux alone ($h=q''/(T_w-T_m)$), becomes a function of the relative strength of the two heat sources [@problem_id:2490095]:

$$
\mathrm{Nu} = \frac{192 q''}{44 q'' + 3 q''' D} = \frac{192}{44 + 3 \frac{q''' D}{q''}}
$$

If there is no internal generation ($q'''=0$), this expression correctly reduces to the classic result $\mathrm{Nu} = 192/44 = 48/11$. If internal generation is present, it changes the temperature profile and thus the relationship between the wall flux and the wall-to-bulk temperature difference.

These extensions illustrate the power and flexibility of the fundamental principles. By starting with the conservation laws, we can systematically account for additional physical phenomena and derive precise predictions for how they influence convective heat transfer.