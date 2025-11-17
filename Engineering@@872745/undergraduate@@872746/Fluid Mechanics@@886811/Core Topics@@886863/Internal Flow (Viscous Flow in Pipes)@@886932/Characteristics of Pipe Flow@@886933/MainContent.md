## Introduction

The transport of fluids within enclosed conduits, known as internal or [pipe flow](@entry_id:189531), is a cornerstone of modern engineering and a fundamental process in the natural world. From the vast networks of pipelines that deliver water and fuel to our cities, to the delicate system of arteries and veins that sustain life, understanding the behavior of fluid in a pipe is essential. The effective design of these systems hinges on the ability to predict pressure changes, determine power requirements for pumps, and manage the inevitable energy losses that occur due to friction. This article provides a comprehensive exploration of these critical characteristics, addressing the core challenge of quantifying and predicting the behavior of internal flows under various conditions.

Through a structured exploration, this article will equip you with the tools to analyze and design [pipe flow](@entry_id:189531) systems. We will begin by dissecting the core physics in **Principles and Mechanisms**, establishing foundational concepts like the Reynolds number, [flow regimes](@entry_id:152820), velocity profiles, and the crucial equations for energy loss. Building upon this foundation, **Applications and Interdisciplinary Connections** will demonstrate how these theories are applied to solve real-world problems in [hydraulic engineering](@entry_id:184767), [process control](@entry_id:271184), and even biology. Finally, **Hands-On Practices** will offer a chance to apply your knowledge to solve representative engineering problems, solidifying the connection between theory and practice. Let us begin by examining the fundamental principles and mechanisms that govern all pipe flows.

## Principles and Mechanisms

The motion of a fluid confined within a conduit, such as a pipe or duct, is known as **[internal flow](@entry_id:155636)**. This class of flows is fundamental to a vast array of engineering and biological systems, from the transport of water and oil in large-scale pipelines to the circulation of coolant in advanced electronics and the flow of blood through arteries. Understanding the principles governing [pipe flow](@entry_id:189531) is essential for designing and analyzing these systems, predicting pressure changes, determining power requirements, and managing energy losses. This chapter systematically explores the core principles and mechanisms that characterize [pipe flow](@entry_id:189531), building from fundamental concepts to more advanced applications.

### Flow Regimes: Laminar, Transitional, and Turbulent Flow

The single most important parameter for characterizing the nature of [pipe flow](@entry_id:189531) is the dimensionless **Reynolds number**, denoted $Re_D$. It represents the ratio of [inertial forces](@entry_id:169104) to viscous forces within the fluid. For a circular pipe of diameter $D$, the Reynolds number is defined as:

$$
\mathrm{Re}_D = \frac{\rho V D}{\mu} = \frac{V D}{\nu}
$$

Here, $\rho$ is the fluid density, $V$ is the average velocity of the flow across the pipe's cross-section, $\mu$ is the dynamic viscosity, and $\nu = \mu/\rho$ is the kinematic viscosity of the fluid. The Reynolds number provides a criterion to distinguish between two fundamentally different [flow regimes](@entry_id:152820): laminar and turbulent.

**Laminar flow**, which occurs at low Reynolds numbers, is characterized by smooth, orderly [fluid motion](@entry_id:182721). The fluid moves in parallel layers, or laminae, with no significant mixing between them. Any disturbances introduced into the flow are damped out by [viscous forces](@entry_id:263294).

**Turbulent flow**, which occurs at high Reynolds numbers, is characterized by chaotic, irregular, and three-dimensional fluid motion. It is dominated by eddies and vortices that lead to rapid mixing of the fluid. Inertial forces are dominant, and they amplify any small disturbances, leading to a perpetually unsteady and random state.

Between these two regimes lies a **transitional flow** regime, where the flow can exhibit intermittent bursts of turbulent behavior within a generally laminar flow.

For flow in a circular pipe, it has been experimentally established that:
- If $\mathrm{Re}_D \lesssim 2300$, the flow is generally **laminar**.
- If $\mathrm{Re}_D \gtrsim 4000$, the flow is generally **turbulent**.
- If $2300 \lesssim \mathrm{Re}_D \lesssim 4000$, the flow is **transitional**.

These threshold values are approximate and can be influenced by factors such as [pipe roughness](@entry_id:270388) and the level of disturbance at the pipe inlet. However, they serve as a reliable guide for most engineering applications.

Consider the practical task of assessing the flow in a [hydraulic system](@entry_id:264924). A specialized oil with density $\rho = 870 \text{ kg/m}^3$ and [dynamic viscosity](@entry_id:268228) $\mu = 0.052 \text{ Pa}\cdot\text{s}$ flows through a pipe of diameter $D = 0.0250 \text{ m}$ at a [volumetric flow rate](@entry_id:265771) of $Q = 0.00120 \text{ m}^3/\text{s}$ [@problem_id:1808368]. To classify the flow, we first calculate the average velocity $V$. The cross-sectional area is $A = \frac{\pi D^2}{4}$, so $V = Q/A = \frac{4Q}{\pi D^2}$. Substituting this into the Reynolds number definition gives an expression independent of the average velocity:

$$
\mathrm{Re}_D = \frac{\rho D}{\mu} \left( \frac{4Q}{\pi D^2} \right) = \frac{4 \rho Q}{\pi \mu D}
$$

Plugging in the values yields $\mathrm{Re}_D \approx 1.02 \times 10^3$. Since this value is well below the critical threshold of 2300, the flow is definitively laminar.

The flow regime can change dramatically within the same physical system if the flow rate changes. For instance, in a building's rainwater drainage system with a downspout of diameter $D=0.10 \text{ m}$, a light drizzle might produce a very low flow rate, while a heavy thunderstorm produces a much higher one [@problem_id:1741243]. For a light drizzle corresponding to a rainfall rate of $1.00 \text{ mm/hr}$ over a $150 \text{ m}^2$ roof, the Reynolds number might be approximately $530$. This indicates a smooth, [laminar flow](@entry_id:149458). In contrast, a heavy thunderstorm with a rainfall rate of $50.0 \text{ mm/hr}$ increases the flow rate fifty-fold, resulting in a Reynolds number of about $2.65 \times 10^4$. This value is far above the 4000 threshold, signifying a highly [turbulent flow](@entry_id:151300). This example highlights that the flow regime is not a property of the pipe alone but of the specific flow conditions within it.

### The Hydrodynamic Entrance Region and Fully Developed Flow

When a fluid enters a pipe from a large reservoir, its [velocity profile](@entry_id:266404) is typically nearly uniform across the pipe's cross-section. However, due to the **[no-slip condition](@entry_id:275670)**, the fluid in direct contact with the pipe wall must have zero velocity. This forces a velocity gradient to develop, and a **boundary layer** begins to grow from the wall into the center of the flow. The region of the pipe where this velocity profile is still changing is known as the **hydrodynamic [entrance region](@entry_id:269854)** or developing flow region.

Within this [entrance region](@entry_id:269854), the fluid in the central core, which has not yet been affected by the [viscous forces](@entry_id:263294) from the wall, accelerates to conserve mass as the boundary layer grows. Once the boundary layer has grown to fill the entire pipe, the velocity profile no longer changes with distance along the pipe. At this point, the flow is said to be **fully developed**. The length of pipe required to achieve this state is called the **[hydrodynamic entrance length](@entry_id:260628)**, $L_e$.

The entrance length depends on the flow regime. For laminar flow ($Re_D \lt 2300$), the entrance length can be estimated by the empirical relation:

$$
\frac{L_e}{D} \approx 0.06 \mathrm{Re}_D \quad (\text{Laminar})
$$

For turbulent flow ($Re_D \gt 4000$), the [entrance region](@entry_id:269854) is typically shorter due to enhanced mixing, and can be approximated by:

$$
\frac{L_e}{D} \approx 4.4 (\mathrm{Re}_D)^{1/6} \quad (\text{Turbulent})
$$

These correlations are important in practice. For very long pipes, the [entrance region](@entry_id:269854) may constitute a negligible fraction of the total length, and one can assume [fully developed flow](@entry_id:151791) throughout. However, in shorter conduits, the flow might never become fully developed. For example, consider sipping water through a drinking straw of length $L = 20.0 \text{ cm}$ and diameter $D = 6.00 \text{ mm}$ at a flow rate of $Q = 2.00 \text{ cm}^3/\text{s}$ [@problem_id:1741215]. Calculating the Reynolds number gives $\mathrm{Re}_D \approx 423$, indicating [laminar flow](@entry_id:149458). Using the laminar correlation, the entrance length is $L_e \approx 0.06 \times 423 \times (0.006 \text{ m}) \approx 0.152 \text{ m}$, or $15.2 \text{ cm}$. The fraction of the straw's length occupied by this developing flow is $\frac{L_e}{L} = \frac{15.2}{20.0} \approx 0.76$. This means that for over three-quarters of its length, the flow profile is still evolving. Assuming [fully developed flow](@entry_id:151791) for the entire straw would be a significant error.

### Analysis of Fully Developed Laminar Flow

For fully developed, steady, incompressible, laminar flow in a horizontal circular pipe, the Navier-Stokes equations can be solved exactly. This leads to a precise mathematical description of the flow, often called **Hagen-Poiseuille flow**.

The analysis begins with a force balance on a cylindrical fluid element. The pressure force driving the flow is balanced by the viscous shear force resisting it at the element's surface. This balance leads to a [parabolic velocity profile](@entry_id:270592):

$$
u(r) = u_{max} \left( 1 - \frac{r^2}{R^2} \right)
$$

where $R$ is the pipe radius, $r$ is the radial distance from the centerline, and $u_{max}$ is the maximum velocity, which occurs at the centerline ($r=0$). This parabolic shape is a hallmark of fully developed [laminar pipe flow](@entry_id:263514).

A crucial relationship exists between the maximum velocity, which is relatively easy to measure (e.g., with a Pitot tube or laser Doppler velocimetry), and the average velocity $V$, which determines the total flow rate. The average velocity is found by integrating the [velocity profile](@entry_id:266404) over the cross-sectional area:

$$
V = \frac{1}{A} \int_A u(r) dA = \frac{1}{\pi R^2} \int_0^R u_{max} \left( 1 - \frac{r^2}{R^2} \right) 2\pi r dr
$$

Evaluating this integral reveals a simple and powerful result:

$$
V = \frac{1}{2} u_{max}
$$

This means that for laminar flow, the [average velocity](@entry_id:267649) is exactly half the centerline velocity. Consequently, the [volumetric flow rate](@entry_id:265771), $Q = V A = V (\pi R^2)$, can be directly determined from a single measurement of the centerline velocity [@problem_id:1741225]:

$$
Q = \frac{\pi R^2}{2} u_{max}
$$

Furthermore, the full derivation connects the flow rate to the pressure gradient, $-\frac{dP}{dx}$, that drives the flow. This relationship is the celebrated **Hagen-Poiseuille equation**:

$$
Q = \frac{\pi R^4}{8\mu} \left( -\frac{dP}{dx} \right) = \frac{\pi R^4 \Delta P}{8\mu L}
$$

where $\Delta P$ is the pressure drop over a pipe of length $L$. This equation is rich with physical insight. It shows that the flow rate is directly proportional to the pressure drop but is incredibly sensitive to the pipe radius, scaling with $R^4$. It also shows that the flow rate is inversely proportional to the fluid's dynamic viscosity $\mu$. This inverse relationship has direct practical consequences. For instance, in a [hydraulic system](@entry_id:264924) operating with a constant pressure pump, if the fluid's temperature drops such that its viscosity doubles (i.e., $\mu_2 = 2\mu_1$), the flow rate will be halved ($Q_2 = \frac{1}{2} Q_1$), assuming the flow remains laminar [@problem_id:1741213].

### Analysis of Fully Developed Turbulent Flow

Unlike [laminar flow](@entry_id:149458), [turbulent flow](@entry_id:151300) lacks an exact analytical solution due to its inherent complexity and chaos. Our understanding relies instead on a combination of [dimensional analysis](@entry_id:140259), semi-empirical theories, and experimental data.

The velocity profile of a [turbulent flow](@entry_id:151300) is markedly different from the laminar parabola. It is much fuller or "flatter" across the pipe's core and exhibits a very steep gradient near the wall. This is because turbulent eddies transport momentum very efficiently across the flow, tending to homogenize the velocity away from the walls. A simple yet effective model for the time-averaged [turbulent velocity profile](@entry_id:265164) is the **power-law profile**:

$$
u(r) = u_{max} \left(1 - \frac{r}{R}\right)^{1/n}
$$

The exponent $n$ is a function of the Reynolds number, but for a wide range of common turbulent flows (e.g., $Re_D \approx 10^5$), $n=7$ is a good approximation, leading to the "one-seventh power-law."

We can find the relationship between the average velocity $V_{avg}$ and the centerline velocity $u_{max}$ for this profile by integration, just as we did for laminar flow. For the one-seventh power-law, this integration yields [@problem_id:1741258]:

$$
\frac{V_{avg}}{u_{max}} = \frac{2n^2}{(n+1)(2n+1)} = \frac{2(7^2)}{(7+1)(2 \cdot 7+1)} = \frac{98}{120} \approx 0.817
$$

This result, $V_{avg} \approx 0.82 u_{max}$, contrasts sharply with the laminar result of $0.5 u_{max}$. The ratio is much closer to 1, quantitatively confirming the "fuller" nature of the turbulent profile.

A more sophisticated description of the [turbulent velocity profile](@entry_id:265164) near the wall is the **law of the wall**. This theory divides the near-wall region into layers and uses [dimensional analysis](@entry_id:140259) to describe the velocity. In the **logarithmic layer**, which covers a significant portion of the pipe, the dimensionless velocity $u^+ = u/u_*$ is related to the dimensionless distance from the wall $y^+ = yu_*/\nu$ by:

$$
u^+ = A \ln(y^+) + B
$$

where $u_* = \sqrt{\tau_w/\rho}$ is the **[friction velocity](@entry_id:267882)**, a velocity scale based on the [wall shear stress](@entry_id:263108) $\tau_w$. The constants $A$ and $B$ are determined empirically (commonly $A \approx 2.5$ and $B \approx 5.5$ for smooth pipes). By integrating this logarithmic profile across the entire pipe section (an approximation valid at high Reynolds numbers), it is possible to derive a relationship between the [bulk flow](@entry_id:149773) parameters: the Darcy [friction factor](@entry_id:150354) $f$ and the Reynolds number $Re_D$ [@problem_id:1741222]. This procedure leads to the **Prandtl universal law of friction** for smooth pipes:

$$
\frac{1}{\sqrt{f}} = C_1 \log_{10}(\mathrm{Re}_D\sqrt{f}) + C_2
$$

The derivation shows that the constant $C_1$ is related to the law-of-the-wall constant $A$ by $C_1 = \frac{A \ln(10)}{\sqrt{8}}$. Using $A=2.5$, we find $C_1 \approx 2.04$, which is remarkably close to the experimentally fitted value of $2.0$. This demonstrates how semi-empirical theories of the velocity structure can successfully predict macroscopic engineering quantities like the [friction factor](@entry_id:150354).

### Energy Losses in Pipe Systems

Flowing fluid possesses mechanical energy in the form of pressure energy, kinetic energy, and potential energy. The **energy equation**, an extension of the Bernoulli equation, accounts for the changes in these forms of energy between two points in a flow system. For a real fluid with viscosity, some mechanical energy is irreversibly converted into thermal energy due to friction. This is termed **head loss**, $h_L$. The [energy equation](@entry_id:156281) for steady, [incompressible flow](@entry_id:140301) between points 1 and 2 is:

$$
\frac{P_1}{\rho g} + \frac{V_1^2}{2g} + z_1 = \frac{P_2}{\rho g} + \frac{V_2^2}{2g} + z_2 + h_L
$$

where $P$ is pressure, $V$ is [average velocity](@entry_id:267649), $z$ is elevation, and $g$ is the [acceleration due to gravity](@entry_id:173411). Head losses are categorized into two types:

1.  **Major Losses ($h_{L,major}$)**: These are due to frictional effects in straight sections of pipe. They are calculated using the **Darcy-Weisbach equation**:
    $$
    h_{L,major} = f \frac{L}{D} \frac{V^2}{2g}
    $$
    where $f$ is the Darcy friction factor, which depends on the Reynolds number and the pipe's [relative roughness](@entry_id:264325).

2.  **Minor Losses ($h_{L,minor}$)**: These occur due to components that disrupt the flow, such as valves, bends, elbows, and changes in pipe area (expansions or contractions). They are typically expressed using a dimensionless **[loss coefficient](@entry_id:276929)**, $K_L$:
    $$
    h_{L,minor} = K_L \frac{V^2}{2g}
    $$
    The velocity $V$ used in this formula is conventionally the average velocity in the smaller-diameter section of the component.

A classic example of a [minor loss](@entry_id:269477) is a **sudden expansion**, where the pipe diameter abruptly increases. As the fluid enters the larger pipe, the flow cannot follow the sharp corner and separates, creating a recirculation zone with significant turbulence. This [turbulent mixing](@entry_id:202591) dissipates energy. For a sudden expansion from velocity $V_1$ to $V_2$, the [head loss](@entry_id:153362) is well-approximated by $h_L = \frac{(V_1 - V_2)^2}{2g}$.

Interestingly, despite the energy loss, the pressure can *increase* across a sudden expansion. Applying the [energy equation](@entry_id:156281) to a horizontal expansion from diameter $D_1$ to $D_2$ [@problem_id:1741217], we can solve for the downstream pressure $P_2$:

$$
P_2 = P_1 + \frac{\rho}{2} \left( V_1^2 - V_2^2 \right) - \rho g h_L = P_1 + \frac{\rho}{2} \left( V_1^2 - V_2^2 - (V_1 - V_2)^2 \right)
$$

Simplifying this expression leads to the Borda-Carnot equation: $P_2 = P_1 + \rho V_2 (V_1 - V_2)$. Since $V_1 > V_2$ (by continuity), the term $\rho V_2 (V_1 - V_2)$ is positive, meaning $P_2 > P_1$. This phenomenon is known as **[pressure recovery](@entry_id:270791)**. The deceleration of the fluid converts some of its kinetic energy into pressure energy, and this conversion more than compensates for the pressure drop associated with the frictional head loss.

### The Influence of Pipe Roughness in Turbulent Flow

In [laminar flow](@entry_id:149458), the velocity at the wall is zero, and the smooth, layered motion is not significantly affected by small surface imperfections. In turbulent flow, however, the situation is different. The interaction between the flow and the pipe's surface roughness can dramatically affect the friction factor and, therefore, the head loss.

The key to understanding this interaction lies in the thin layer of fluid adjacent to the wall where viscous effects remain dominant even in a turbulent flow: the **viscous sublayer**. The thickness of this sublayer, $\delta_{\nu}$, is not constant; it decreases as the Reynolds number (and thus the [wall shear stress](@entry_id:263108)) increases. The effect of roughness depends on the size of the [absolute roughness](@entry_id:260619) elements, $e$, relative to the thickness of this sublayer.

-   **Hydraulically Smooth Flow**: If the roughness elements are much smaller than the sublayer thickness ($e \ll \delta_{\nu}$), they are completely submerged within it and do not disturb the outer turbulent flow. The pipe "behaves" as if it were perfectly smooth, and the [friction factor](@entry_id:150354) $f$ is a function of $Re_D$ only.

-   **Fully Rough Flow**: If the roughness elements are much larger than the sublayer thickness ($e \gg \delta_{\nu}$), they protrude into the main [turbulent flow](@entry_id:151300), creating significant [form drag](@entry_id:152368). In this regime, viscous effects become negligible compared to the drag on the roughness elements. The friction factor $f$ becomes independent of $Re_D$ and depends only on the **[relative roughness](@entry_id:264325)**, $e/D$.

-   **Transitional Roughness**: In the intermediate case where $e \approx \delta_{\nu}$, both viscous effects and roughness contribute to the friction. The friction factor $f$ depends on both $Re_D$ and $e/D$.

The **Colebrook-White equation** is a comprehensive empirical formula that correctly models all three of these turbulent regimes:

$$
\frac{1}{\sqrt{f}} = -2.0 \log_{10} \left( \frac{e/D}{3.7} + \frac{2.51}{\mathrm{Re}_D \sqrt{f}} \right)
$$

The first term in the logarithm, involving $e/D$, dominates in the fully rough regime, while the second term, involving $\mathrm{Re}_D$, dominates in the [hydraulically smooth](@entry_id:260663) regime.

The transition from smooth to transitionally rough behavior can be quantified using the **roughness Reynolds number**, $Re_e = \frac{u_* e}{\nu}$. This dimensionless group compares the roughness height $e$ to the viscous length scale $\nu/u_*$, which is proportional to the sublayer thickness. The transition is typically considered to begin when $Re_e \approx 5$. We can use this criterion to find the specific flow velocity at which a given pipe begins to behave as rough [@problem_id:1785499]. For a given pipe ($e, D$) and fluid ($\nu$), one can solve the system of equations (the transition criterion, the Colebrook equation, and the definitions of $u_*$ and $Re_D$) to find the threshold [average velocity](@entry_id:267649) $V$. This calculation shows that a pipe is not inherently "smooth" or "rough"; rather, its hydraulic behavior depends on the flow conditions.

### An Introduction to Non-Newtonian Pipe Flow

The discussion so far has assumed a **Newtonian fluid**, where the shear stress is linearly proportional to the [rate of strain](@entry_id:267998) (e.g., water, oil, air). However, many fluids encountered in industrial and biological processes are **non-Newtonian**. Examples include slurries, pastes, [polymer solutions](@entry_id:145399), and blood.

One important class of non-Newtonian fluid is the **Bingham plastic**. This material behaves like a rigid solid until a certain minimum shear stress, the **[yield stress](@entry_id:274513)** $\tau_y$, is exceeded. Once yielded, it flows like a viscous fluid with a constant **[plastic viscosity](@entry_id:267041)**, $\mu_p$.

Consider the task of initiating the flow of a Bingham plastic in a pipe. Unlike a Newtonian fluid, which will move under an infinitesimally small pressure gradient, a Bingham plastic will not flow until the shear stress at some point in the fluid reaches the yield stress $\tau_y$. In [pipe flow](@entry_id:189531), the shear stress is zero at the centerline and maximum at the wall ($r=R$). Therefore, flow can only begin when the [wall shear stress](@entry_id:263108), $\tau_w$, reaches the yield stress.

For a pipe inclined at an angle $\theta$ to the horizontal, a [force balance](@entry_id:267186) on a cylindrical fluid element shows that the [wall shear stress](@entry_id:263108) must balance both the pressure gradient and the component of gravity acting along the pipe. The condition to just initiate upward flow is [@problem_id:1741233]:

$$
\tau_w = \tau_y
$$

The [wall shear stress](@entry_id:263108) is given by $\tau_w = \frac{R}{2} (G - \rho g \sin\theta)$, where $G = -dP/dx$ is the pressure gradient. Therefore, the minimum pressure gradient, $G_{min}$, required to start the flow is:

$$
G_{min} = \rho g \sin\theta + \frac{2\tau_y}{R}
$$

This expression shows that the required pressure gradient must first overcome the fluid's weight (the $\rho g \sin\theta$ term) and then provide an additional component sufficient to overcome the fluid's yield stress at the wall (the $2\tau_y/R$ term). This is a critical design consideration in systems pumping materials like clay slurries, drilling muds, or certain food products. If the applied pressure gradient is less than $G_{min}$, the fluid will remain stationary in the pipe.