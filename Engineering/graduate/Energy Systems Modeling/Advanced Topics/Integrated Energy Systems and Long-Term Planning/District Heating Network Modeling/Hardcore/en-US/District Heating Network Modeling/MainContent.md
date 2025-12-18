## Introduction
Modeling district heating networks (DHNs) is a cornerstone of modern energy [systems engineering](@entry_id:180583), essential for designing efficient infrastructure, optimizing daily operations, and enabling the transition to a sustainable energy future. The complexity of these large-scale, coupled thermal-[hydraulic systems](@entry_id:269329) presents a significant challenge: how to translate fundamental physical laws into robust, predictive, and computationally tractable models. This article addresses this challenge by providing a comprehensive guide to the principles and practices of DHN modeling. First, the **"Principles and Mechanisms"** section will deconstruct the network into its core components, deriving the governing algebraic and differential equations for fluid dynamics and [heat transport](@entry_id:199637) from first principles. Next, **"Applications and Interdisciplinary Connections"** will explore how these foundational models are applied to solve real-world problems, from component characterization and operational control to analyzing the role of DHNs in broader [multi-energy systems](@entry_id:1128259). Finally, the **"Hands-On Practices"** chapter will offer targeted exercises to reinforce the theoretical concepts, bridging the gap between theory and practical implementation.

## Principles and Mechanisms

The modeling of district heating networks rests upon the fundamental principles of mass, momentum, and energy conservation applied to a fluid system. A comprehensive model must capture the interplay between two distinct yet coupled subsystems: the **hydraulic subsystem**, which governs the flow rates and pressures of the water circulating through the network, and the **thermal subsystem**, which governs the transport and distribution of thermal energy, manifested as the temperature of the water. This chapter elucidates the core principles and component models that form the foundation of modern district heating network simulation. We will build these models from first principles, justifying key assumptions and deriving the governing equations for each component before integrating them into a coherent system-level framework.

### Fundamental Principles and Simplifying Assumptions

The behavior of fluid flow and heat transfer is described by a complex set of partial differential equations. To create tractable models for large-scale networks, we must introduce simplifying assumptions that are physically justified for the specific context of district heating.

#### The Incompressibility Assumption

The most significant simplification in hydraulic modeling is treating liquid water as an **[incompressible fluid](@entry_id:262924)**. This implies that the fluid's density, $\rho$, is constant throughout the network, regardless of variations in pressure and temperature. While the density of water does, in fact, vary with temperature, the magnitude of this variation is typically small enough that its effect on mass balance calculations is negligible.

To illustrate this, consider a practical scenario where a model must justify this assumption . Imagine a mixing junction in a network operating at a constant pressure of $8 \ \mathrm{bar}$. Two streams enter: one at a flow rate of $Q_1 = 0.6 \ \mathrm{m^3/s}$ with a temperature of $T_1 = 60^\circ\mathrm{C}$, and another at $Q_2 = 0.4 \ \mathrm{m^3/s}$ with $T_2 = 100^\circ\mathrm{C}$. The reference temperature is $T_0 = 80^\circ\mathrm{C}$. The isobaric volumetric [thermal expansion coefficient](@entry_id:150685) of water, $\alpha$, which describes how volume changes with temperature, is approximately $\alpha \approx 3.0 \times 10^{-4} \ \mathrm{K^{-1}}$ in this range. The relationship between density and temperature can be approximated by $\rho(T) = \rho_0 \exp(-\alpha(T-T_0))$, where $\rho_0$ is the density at the reference temperature $T_0$.

The true total mass inflow rate is $\dot{m}_{\mathrm{in}} = \rho(T_1)Q_1 + \rho(T_2)Q_2$. A simplified model assuming constant density $\rho_0$ would calculate the [mass flow](@entry_id:143424) as $\dot{m}_{\mathrm{approx}} = \rho_0 (Q_1 + Q_2)$. The [relative error](@entry_id:147538) introduced by this assumption is $e = |\dot{m}_{\mathrm{approx}} - \dot{m}_{\mathrm{in}}| / \dot{m}_{\mathrm{in}}$. By substituting the temperature-dependent density expressions, we find that for this considerable temperature difference of $40 \ \mathrm{K}$, the [relative error](@entry_id:147538) is only about $0.0012$, or $0.12\%$. This remarkably small error validates the use of a constant density model for satisfying mass conservation laws in the hydraulic analysis of most district heating networks. While temperature-dependent density is crucial for accurately calculating heat content, its variation is too small to significantly impact the calculation of [mass flow](@entry_id:143424) distribution.

#### Conservation of Mass: Pipes and Nodes

With the incompressibility assumption established, we can formulate the laws of mass conservation.

For a single pipe segment, we can derive the one-dimensional continuity equation by considering a differential slice of the pipe of length $\mathrm{d}x$ . The general principle of mass conservation states that the rate of change of mass within this control volume equals the net rate of mass flowing in, plus any mass added by a source. This leads to the general 1D continuity equation:
$$ \frac{\partial(\rho A)}{\partial t} + \frac{\partial(\rho u A)}{\partial x} = s_m $$
where $\rho$ is the density, $A$ is the cross-sectional area, $u$ is the fluid velocity, and $s_m$ is a distributed mass source per unit length (e.g., leakage). The volumetric flow rate is defined as $q = uA$.

In the context of district heating [network modeling](@entry_id:262656), we apply a standard set of assumptions:
1.  **Incompressible Fluid**: As justified above, $\rho$ is constant.
2.  **Rigid, Fully Filled Pipe**: The pipe geometry is fixed, so the area $A$ does not change with time ($\partial A / \partial t = 0$).
3.  **No Distributed Sources/Sinks**: For a simple transport pipe between two nodes, we assume no leakage or continuous offtakes along its length, so $s_m = 0$.

Under these conditions, the general continuity equation simplifies dramatically. The time derivative term vanishes because $\rho$ and $A$ are constant in time. The equation becomes:
$$ \rho \frac{\partial(uA)}{\partial x} = 0 \implies \frac{\partial q}{\partial x} = 0 $$
This crucial result states that for an [incompressible fluid](@entry_id:262924) in a rigid pipe without intermediate sources, the volumetric flow rate $q$ is uniform along the length of the pipe at any given instant in time. This is true for both steady and transient flow; if the flow rate changes, it changes uniformly along the entire pipe segment simultaneously. This reduces the problem of finding the flow in a pipe link to determining a single value, $q(t)$, for that entire link.

At the **nodes** (junctions) where pipes connect, the principle of mass conservation requires that the total mass flowing into the node must equal the total mass flowing out. For a steady-[state mixing](@entry_id:148060) node with multiple inlets (indexed by $i$) and a single outlet (o), this is expressed as :
$$ \sum_i \dot{m}_i = \dot{m}_o \implies \sum_i \rho_i q_i = \rho_o q_o $$
If we apply the incompressibility assumption with a uniform density $\rho$ for all streams, this [mass balance](@entry_id:181721) simplifies to a **volume balance**:
$$ \sum_i q_i = q_o $$
These nodal balance equations, applied at every junction in the network, form a system of algebraic equations that, together with the component characteristics, determine the distribution of flow rates.

### Hydraulic Component Modeling

The hydraulic subsystem is modeled as a set of algebraic equations that relate pressures and flow rates. These equations arise from applying the principles of fluid momentum and energy to the network's key components: pipes, pumps, and valves. In steady-state or quasi-steady hydraulic models, this system can be solved independently of the thermal dynamics.

#### Pipe Head Loss and Friction

As water flows through a pipe, it loses [mechanical energy](@entry_id:162989) due to friction with the pipe walls. This energy loss manifests as a pressure drop, or **[head loss](@entry_id:153362)**. The most common model for this phenomenon is the **Darcy-Weisbach equation**, which relates the pressure drop $\Delta p$ over a pipe of length $L$ and diameter $D$ to the mean flow velocity $u_m$:
$$ \Delta p = f \frac{L}{D} \frac{\rho u_m^2}{2} $$
Here, $f$ is the dimensionless **Darcy [friction factor](@entry_id:150354)**, which encapsulates all the complex physics of the flow within the pipe. The value of $f$ depends on the flow regime, characterized by the **Reynolds number** $\mathrm{Re} = \frac{\rho u_m D}{\mu}$, where $\mu$ is the dynamic viscosity of the fluid .

In **[laminar flow](@entry_id:149458)** (typically $\mathrm{Re}  2300$), the flow is smooth and orderly. An exact analytical solution to the Navier-Stokes equations for fully developed [pipe flow](@entry_id:189531) yields the relationship:
$$ f = \frac{64}{\mathrm{Re}} $$
This shows that in the laminar regime, friction is dominated by [viscous forces](@entry_id:263294).

In **turbulent flow** (typically $\mathrm{Re} > 4000$), which is the prevalent regime in the main pipes of a district heating network, the flow is chaotic and characterized by eddies and vortices. In this regime, the [friction factor](@entry_id:150354) depends not only on the Reynolds number but also on the **[relative roughness](@entry_id:264325)** of the pipe's inner surface, $\varepsilon/D$, where $\varepsilon$ is the mean height of the roughness protrusions. The most widely accepted correlation for $f$ in the turbulent regime is the empirical **Colebrook-White equation**:
$$ \frac{1}{\sqrt{f}} = -2.0 \log_{10} \left( \frac{\varepsilon/D}{3.7} + \frac{2.51}{\mathrm{Re}\sqrt{f}} \right) $$
This equation has several important features:
-   It is **implicit**, as $f$ appears on both sides, requiring an iterative numerical solution.
-   It correctly blends the behavior of [hydraulically smooth](@entry_id:260663) pipes (where friction depends only on $\mathrm{Re}$) and fully rough pipes.
-   At very high Reynolds numbers, the viscous term becomes negligible, and the equation approaches a **fully rough asymptote** where $f$ depends only on the [relative roughness](@entry_id:264325) $\varepsilon/D$. This is characteristic of many large-scale DHN mains.

#### Pump Characteristics

Centrifugal pumps provide the necessary energy to overcome the total [head loss](@entry_id:153362) in the network and drive the circulation of water. The performance of a pump is described by its **[pump curve](@entry_id:261367)**, which relates the head $H$ (energy per unit weight of fluid, measured in meters) it delivers to the [volumetric flow rate](@entry_id:265771) $q$ passing through it.

A common and effective model for a constant-speed [centrifugal pump](@entry_id:264566)'s [characteristic curve](@entry_id:1122276) is a quadratic equation :
$$ H(q) = H_0 - a q^2 $$
This form can be justified from first principles. The ideal head delivered by a pump is determined by the impeller geometry and rotational speed (from the Euler turbomachine equation) and decreases linearly with flow. However, the fluid passing through the pump also experiences hydraulic losses due to friction and turbulence, which scale approximately with the square of the flow rate. The combination of these effects leads to the characteristic drooping quadratic curve.

The coefficients have clear physical interpretations:
-   $H_0$: The **shutoff head**, which is the head produced at zero flow ($q=0$). It represents the maximum pressure difference the pump can generate.
-   $a$: A positive coefficient representing the aggregated internal hydraulic losses within the pump. Its units in the SI system are $\mathrm{s^2/m^5}$.

For example, if a pump has a measured shutoff head of $32 \ \mathrm{m}$ and delivers a head of $30 \ \mathrm{m}$ at a flow of $0.04 \ \mathrm{m^3/s}$, we can determine the coefficient $a$ as $a = (32 - 30) / (0.04)^2 = 1250 \ \mathrm{s^2/m^5}$. The full [pump curve](@entry_id:261367) would then be $H(q) = 32 - 1250 q^2$.

#### Valve Characteristics

Control valves are essential components used to regulate flow to consumers or between different parts of the network. A valve acts as a localized hydraulic restriction, creating a pressure drop to throttle the flow.

The relationship between flow rate $q$ and the pressure drop $\Delta p$ across a valve can be derived from the mechanical energy balance (extended Bernoulli equation) . The [head loss](@entry_id:153362) across the valve is modeled as being proportional to the kinetic energy of the flow, $h_L = K \frac{v^2}{2g}$, where $K$ is a dimensionless [loss coefficient](@entry_id:276929) that depends on the valve's design and opening position. By equating this [head loss](@entry_id:153362) to the pressure head drop $\Delta p / (\rho g)$, we can solve for the flow rate $q$:
$$ q = \left(A \sqrt{\frac{2}{K}}\right) \sqrt{\frac{\Delta p}{\rho}} $$
where $A$ is the pipe cross-sectional area. This equation is typically written in a more compact form:
$$ q = C_v \sqrt{\frac{\Delta p}{\rho}} $$
Here, $C_v \equiv A \sqrt{2/K}$ is the **valve flow coefficient**, defined in SI units. It has units of area ($\mathrm{m^2}$) and can be interpreted as the **effective flow area** of the valve. It conveniently lumps all the geometric properties of the valve and its installation into a single parameter that characterizes its capacity at a given opening. This relationship is fundamental for modeling control actions but is valid only for non-choked, single-phase liquid flow. It fails if **cavitation** occurs, which happens when the pressure inside the valve drops to the water's vapor pressure, causing it to boil.

### Thermal Component and System Modeling

The thermal subsystem describes how thermal energy is transported and exchanged within the network. Unlike the hydraulics, which are often treated as quasi-steady, the thermal behavior is inherently dynamic due to the finite time it takes for water to travel through the pipes. This leads to a system of differential equations governing the network's temperatures.

#### Energy Transport and Heat Loss in Pipes

The temperature of the water in a pipe changes due to two primary effects: it is carried along by the bulk motion of the fluid (**advection**), and it loses heat to the surroundings (e.g., the ground in which it is buried). An energy balance on a differential fluid element of length $\mathrm{d}x$ yields the one-dimensional advection-loss equation for the temperature field $T(x,t)$ :
$$ \frac{\partial T}{\partial t} + v \frac{\partial T}{\partial x} = -\frac{U P}{\rho c_p A} (T - T_g) $$
Let's analyze the terms of this fundamental equation:
-   $\frac{\partial T}{\partial t}$: The **local accumulation term**, representing the rate of temperature change at a fixed point $x$ in space.
-   $v \frac{\partial T}{\partial x}$: The **advective transport term**, representing the transport of the temperature gradient along the pipe by the bulk flow at velocity $v$. The sum of these two terms is the [material derivative](@entry_id:266939), describing the temperature change of a moving fluid parcel.
-   $-\frac{U P}{\rho c_p A} (T - T_g)$: The **heat loss term**. Here, $U$ is the [overall heat transfer coefficient](@entry_id:151993) from the fluid to the surroundings, $P$ is the [wetted perimeter](@entry_id:268581) of the pipe, $c_p$ is the specific heat capacity, and $T_g$ is the temperature of the surroundings (ground). The negative sign ensures that the temperature decreases when the fluid is hotter than the ground ($T > T_g$).

This model relies on the **[plug-flow assumption](@entry_id:1129834)**, which neglects the effects of axial [thermal conduction](@entry_id:147831) and dispersion within the fluid. This assumption is highly justified in typical district heating pipes. We can quantify this by comparing the magnitude of axial heat transport by advection to that by conduction using the dimensionless **Péclet number**, $\mathrm{Pe}$ . The Péclet number is defined as:
$$ \mathrm{Pe} = \frac{\text{Rate of Advection}}{\text{Rate of Conduction}} = \frac{v D_h}{\alpha} $$
where $D_h$ is the [hydraulic diameter](@entry_id:152291) of the pipe (equal to the inner diameter for a circular pipe) and $\alpha = k/(\rho c_p)$ is the fluid's [thermal diffusivity](@entry_id:144337). For a typical DHN supply main with $v=1.2 \ \mathrm{m/s}$ and $D_h=0.3 \ \mathrm{m}$, the Péclet number is on the order of $2 \times 10^6$. This extremely large value indicates that advection is the overwhelmingly dominant mechanism for axial heat transport, and neglecting axial conduction introduces a negligible error.

#### Energy Balance at Mixing Nodes

At nodes where streams of water at different temperatures mix, we apply the [first law of thermodynamics](@entry_id:146485). For a steady-[state mixing](@entry_id:148060) node, the rate of energy entering the node must equal the rate of energy leaving. Assuming the node is adiabatic (no heat exchange with the surroundings), no work is done, and changes in kinetic and potential energy are negligible, the energy balance is written in terms of specific enthalpy, $h$ :
$$ \sum_i \dot{m}_i h_i = \dot{m}_o h_o \implies \sum_i \rho_i q_i h_i = \rho_o q_o h_o $$
The key assumption here is **perfect mixing**, which implies that the properties of the outlet stream are uniform and represent a complete mixture of the inlet streams. For an incompressible liquid with constant specific heat $c_p$, the change in [specific enthalpy](@entry_id:140496) is approximately $dh = c_p dT$. This allows the energy balance to be expressed directly in terms of temperatures, forming the basis for temperature mixing calculations at network junctions.

### Integrated System Modeling and Solution Strategies

A complete network model combines the hydraulic and thermal principles into a single mathematical framework. This framework takes the form of a system of Differential-Algebraic Equations (DAEs).

#### The DAE Formulation

The DAE formulation provides a structured and powerful way to represent the entire network's behavior . The system is composed of:
1.  **Algebraic Equations**: These describe the parts of the system that are assumed to respond instantaneously. The hydraulic subsystem, governed by nodal mass balances and component [head loss](@entry_id:153362)/gain relationships (for pipes, pumps, and valves), forms a large system of nonlinear algebraic equations. The variables in this system are typically the nodal pressures and the flow rates in each pipe.
2.  **Differential Equations**: These describe the parts of the system with memory or inertia. The thermal subsystem is inherently dynamic due to the finite time required for heat to advect through the pipes. The pipe energy balance equations, often discretized into a set of Ordinary Differential Equations (ODEs) for lumped segments of the pipe, form the dynamic part of the DAE system. The state variables are the temperatures at various points in the network.

For example, a simple single-loop network can be modeled with algebraic variables for the loop flow rate $q(t)$ and consumer outlet temperature $T_c^{\mathrm{out}}(t)$, and [state variables](@entry_id:138790) for the pipe outlet temperatures $T_s(t)$ and $T_r(t)$. The hydraulic equation is the algebraic loop head balance, while the thermal dynamics are described by two coupled ODEs for the rate of change of $T_s(t)$ and $T_r(t)$.

#### Sequential Decoupling and Convergence Challenges

Solving the fully coupled DAE system simultaneously can be computationally intensive. A common and intuitive approach is **sequential decoupling**. In this method, the hydraulic and thermal systems are solved alternately:
1.  At a given time or iteration, solve the algebraic hydraulic equations to find all flow rates in the network.
2.  Holding these flow rates fixed, solve the dynamic thermal equations (e.g., advance them over a time step) to update all temperatures in the network.
3.  Repeat for the next time step or iteration.

While this approach is conceptually simple, it can face numerical challenges due to the underlying coupling between the two subsystems. A [critical coupling](@entry_id:268248) often arises from consumer behavior. For instance, if a consumer has a fixed heat demand $Q_d$, the required mass flow rate is given by $q = Q_d / (c_p(T_{\text{in}} - T_{\text{ret}}))$. Here, the flow rate $q$ (a hydraulic variable) depends directly on the inlet temperature $T_{\text{in}}$ (a thermal variable).

This coupling can lead to [numerical oscillations](@entry_id:163720) or even divergence in a sequential solver. Consider the iterative process where the flow rate for the next iteration, $q^{k+1}$, is calculated based on the temperature $T_{\text{in}}(q^k)$ computed using the flow from the current iteration . This defines a [fixed-point iteration](@entry_id:137769) $q^{k+1} = f(q^k)$. Local convergence requires that the absolute value of the derivative of the mapping, $|f'(q^\star)|$, be less than 1 at the solution point $q^\star$.

A detailed analysis shows that this condition depends on the physical parameters of the system:
$$ |f'(q^\star)| = \frac{h_\ell L}{\rho c_p q^\star} \frac{T_{\text{in}}(q^\star) - T_g}{T_{\text{in}}(q^\star) - T_{\text{ret}}} $$
This inequality reveals that convergence is not guaranteed. It is promoted by a high flow rate $q^\star$, low pipe heat losses (small $h_\ell L$), and a large temperature drop across the consumer ($T_{\text{in}} - T_{\text{ret}}$). This demonstrates a profound link between the physical characteristics of a district heating system and the stability of the numerical methods used to simulate it. A thorough understanding of these underlying principles is therefore not only essential for building accurate models but also for developing robust and efficient solution algorithms.