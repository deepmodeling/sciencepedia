## Introduction
Turbomachinery—devices that transfer energy between a rotor and a fluid—are the powerhouse of modern engineering, driving everything from jet aircraft to hydroelectric power plants. Understanding their operation is a cornerstone of fluid mechanics, yet it requires a specialized set of principles that go beyond standard energy equations to account for work done by a rotating component. This article bridges that gap by providing a comprehensive exploration of the physics governing these complex machines. We will begin by dissecting the fundamental principles and mechanisms, starting with the universal Euler turbomachine equation and the crucial role of velocity triangles. From there, we will explore a wide range of applications and interdisciplinary connections, showing how these principles are applied in system design, machine selection, and in conjunction with fields like thermodynamics and materials science. Finally, a series of hands-on practices will allow you to solidify your understanding and apply these concepts to practical engineering scenarios.

## Principles and Mechanisms

Turbomachinery encompasses a diverse family of devices that transfer energy between a rotating element and a continuously flowing fluid. Despite their varied forms—from colossal hydroelectric turbines to miniature pumps in cooling systems—their operation is governed by a common set of fundamental fluid dynamic principles. This chapter will elucidate these core principles, beginning with the universal law of [energy transfer](@entry_id:174809), exploring the kinematic relationships that describe the flow, and finally examining the specific mechanisms and performance characteristics of pumps and turbines.

### The Euler Turbomachine Equation: A Unified View of Energy Transfer

The cornerstone of [turbomachinery](@entry_id:276962) analysis is the **Euler turbomachine equation**. This powerful relationship connects the work done by or on the fluid to the change in the fluid's angular momentum as it passes through the rotor. To understand this, we consider a control volume that encloses the rotating part of the machine, known as the **rotor** or **impeller**.

The principle of angular momentum states that the [net torque](@entry_id:166772) exerted on the fluid within the control volume equals the net rate of flow of angular momentum out of the [control volume](@entry_id:143882). For steady flow, this torque, $\tau$, which is equal and opposite to the torque required to drive the shaft, is given by the [mass flow rate](@entry_id:264194), $\dot{m}$, multiplied by the change in the specific angular momentum of the fluid between the outlet (station 2) and the inlet (station 1).

The specific angular momentum of a fluid particle at a radius $r$ is the product of its radius and the tangential component of its absolute velocity, $V_{\theta}$. This tangential velocity component is also frequently referred to as the **swirl velocity**. Therefore, the rate of angular momentum entering the rotor is $\dot{L}_{in} = \dot{m} r_1 V_{\theta 1}$, and the rate leaving is $\dot{L}_{out} = \dot{m} r_2 V_{\theta 2}$ [@problem_id:1735328]. The net torque on the fluid is thus:

$$\tau = \dot{m} (r_2 V_{\theta 2} - r_1 V_{\theta 1})$$

The power transferred, $\dot{W}$, is the product of this torque and the angular velocity of the rotor, $\omega$. Recognizing that the tangential speed of the blade is $U = \omega r$, we can write $U_1 = \omega r_1$ and $U_2 = \omega r_2$. Substituting these into the power equation yields the celebrated Euler turbomachine equation:

$$\dot{W} = \tau \omega = \dot{m} (\omega r_2 V_{\theta 2} - \omega r_1 V_{\theta 1}) = \dot{m} (U_2 V_{\theta 2} - U_1 V_{\theta 1})$$

This equation is remarkably general. By convention, $\dot{W}$ is positive for machines that add energy to the fluid (pumps, fans, compressors) and negative for machines that extract energy from the fluid (turbines). The term $(U_2 V_{\theta 2} - U_1 V_{\theta 1})$ represents the work done per unit mass of fluid. For an incompressible fluid, this work manifests as a change in the fluid's total pressure, often expressed as the **head** ($H$), which is the work per unit weight of fluid:

$$H_e = \frac{\dot{W}}{\dot{m}g} = \frac{U_2 V_{\theta 2} - U_1 V_{\theta 1}}{g}$$

Here, $g$ is the [acceleration due to gravity](@entry_id:173411), and $H_e$ is known as the **theoretical head** or **Euler head**.

### The Language of Flow: Velocity Triangles

The Euler equation highlights the central importance of the fluid's absolute tangential velocity, $V_{\theta}$. However, this velocity is the result of a complex interaction between the moving blades and the fluid. To dissect this interaction, we employ a crucial analytical tool: the **[velocity triangle](@entry_id:268727)**.

At any point within the turbomachine, we must distinguish between two [frames of reference](@entry_id:169232). The **absolute velocity**, denoted by $\vec{V}$, is the velocity of a fluid particle as seen by a stationary observer. The **[relative velocity](@entry_id:178060)**, denoted by $\vec{W}$, is the velocity of the fluid particle as seen by an observer rotating with the impeller. These two velocities are linked by the velocity of the blade itself, $\vec{U}$. The fundamental kinematic relationship is:

$\vec{V} = \vec{U} + \vec{W}$

This vector sum forms a closed triangle, the [velocity triangle](@entry_id:268727), which is indispensable for analyzing flow at the inlet and outlet of the rotor. The blade velocity $\vec{U}$ is always purely tangential, with magnitude $U = \omega r$. The vectors $\vec{V}$ and $\vec{W}$ can have both tangential and through-flow (radial or axial) components.

Consider, for example, the flow exiting the impeller of a [centrifugal pump](@entry_id:264566) [@problem_id:1735355]. The blade at the outlet radius $r_2$ moves at a speed $U_2 = \omega r_2$. The fluid leaves the blade with a relative velocity $\vec{W}_2$ at an angle $\beta_2$ determined by the blade's geometry. The resulting absolute velocity $\vec{V}_2$ is the vector sum $\vec{U}_2 + \vec{W}_2$. By decomposing this vector sum into components, we can determine the absolute tangential velocity $V_{\theta 2}$ needed for the Euler equation. If we align our coordinate system with the tangential direction, the tangential component of the vector equation becomes:

$V_{\theta 2} = U_2 + W_{\theta 2}$

In many pumps, the blades are **backward-curved**, meaning the relative velocity has a tangential component that opposes the direction of rotation. In this common configuration, the relation simplifies to $V_{\theta 2} = U_2 - W_{\theta 2}$, where $W_{\theta 2}$ is the magnitude of the relative tangential velocity. The velocity triangles at both the inlet (station 1) and outlet (station 2) provide the complete kinematic picture needed to apply the Euler equation.

### Mechanisms of Energy Addition in Pumps

Pumps and compressors add energy to a fluid, typically increasing its pressure. The Euler equation quantifies the total energy added, but the physical mechanisms responsible for this [energy transfer](@entry_id:174809) are rooted in the fluid dynamics within the impeller.

#### The Centrifugal Effect

In radial-flow machines like centrifugal pumps, a primary mechanism for pressure rise is the centrifugal force field created by the impeller's rotation. As fluid is forced to rotate with the impeller, it experiences an outward centrifugal acceleration. To a first approximation, we can model the fluid within the impeller passages as a rotating rigid body [@problem_id:1735350]. In this simplified view, the radial pressure gradient must balance the centrifugal force:

$$\frac{dp}{dr} = \rho \omega^2 r$$

Integrating this expression from an inner radius $r_1$ to an outer radius $r_2$ gives the pressure rise due solely to the centrifugal effect:

$$p_2 - p_1 = \int_{r_1}^{r_2} \rho \omega^2 r \, dr = \frac{1}{2} \rho \omega^2 (r_2^2 - r_1^2) = \frac{1}{2} \rho (U_2^2 - U_1^2)$$

This equation clearly shows that a significant pressure increase is achieved simply by slinging the fluid from a small radius to a large radius at high rotational speed.

#### Static Pressure Rise and the Role of Diffusion

The Euler equation gives the change in **[stagnation pressure](@entry_id:265293)** (or total head), which includes both [static pressure](@entry_id:275419) and kinetic energy. The ultimate goal of a pump, however, is usually to increase the [static pressure](@entry_id:275419) of the fluid. The total energy added by the impeller is partitioned between an increase in the fluid's [static pressure](@entry_id:275419) and an increase in its kinetic energy. The [static pressure](@entry_id:275419) rise, $P_2 - P_1$, across the impeller can be found by applying the [steady flow energy equation](@entry_id:142220):

$$P_2 - P_1 = \rho (U_2 V_{\theta 2} - U_1 V_{\theta 1}) - \frac{1}{2} \rho (V_2^2 - V_1^2)$$

This equation reveals a critical insight: to maximize the [static pressure](@entry_id:275419) gain across the impeller itself, the increase in the fluid's absolute kinetic energy ($V_2^2 - V_1^2$) should be minimized relative to the Euler work input [@problem_id:1735343].

Furthermore, within the rotating passages, the flow often decelerates in the relative frame (i.e., $W_1 > W_2$). This deceleration, or diffusion, of the relative flow converts some of the relative kinetic energy into a [static pressure](@entry_id:275419) rise, a mechanism that complements the centrifugal effect.

#### The Volute: Recovering Kinetic Energy

A significant portion of the energy imparted to the fluid by the impeller exists as kinetic energy at the outlet. The absolute velocity $V_2$ can be very high. Simply discharging this high-velocity fluid into a large chamber would dissipate most of this kinetic energy into heat through turbulence. To improve efficiency, centrifugal pumps are encased in a spiral-shaped casing called a **volute**, or are fitted with a ring of stationary vanes called a **diffuser**.

The primary function of the volute is to act as a diffuser: it has a progressively increasing cross-sectional area that efficiently decelerates the flow, converting the kinetic energy at the impeller exit into a further increase in [static pressure](@entry_id:275419) [@problem_id:1735356]. The pressure rise achieved in the volute can be a substantial fraction of the total pressure rise of the pump. The effectiveness of this conversion is described by a volute efficiency, $\eta_v$, such that the additional pressure gained is $\Delta P_{\text{volute}} = \eta_v (\frac{1}{2} \rho V_2^2)$. A well-designed volute is therefore crucial for achieving high overall pump efficiency.

### Mechanisms of Energy Extraction in Turbines

Turbines operate in reverse to pumps: they extract energy from the fluid, converting fluid power into mechanical shaft power. The Euler equation, with $\dot{W}$ being negative, still governs this process:

$$P_{\text{extracted}} = -\dot{W} = \dot{m} (U_1 V_{\theta 1} - U_2 V_{\theta 2})$$

For a turbine to produce power, the term $(U_1 V_{\theta 1} - U_2 V_{\theta 2})$ must be positive. This means the angular momentum of the fluid must decrease as it passes through the runner.

#### Creating Inlet Swirl and Removing Exit Swirl

To maximize power extraction, designers aim to have a large angular momentum at the inlet ($r_1 V_{\theta 1}$) and a very small angular momentum at the outlet ($r_2 V_{\theta 2}$). The high inlet swirl is achieved using stationary components upstream of the runner. In reaction turbines like the Francis turbine, these are adjustable **guide vanes** (or wicket gates). In impulse turbines, they are fixed **nozzles**. These devices accelerate the flow and direct it onto the runner blades at an optimal angle, generating a large tangential velocity component $V_{\theta 1}$ [@problem_id:1735341].

Conversely, the ideal condition at the turbine outlet (or **draft tube** inlet) is to have zero residual swirl, i.e., $V_{\theta 2} = 0$. If the fluid exits with residual swirl, its kinetic energy has not been fully extracted by the runner, representing a loss of efficiency. Achieving near-zero exit swirl is a primary design goal for high-efficiency turbines [@problem_id:1735341].

#### Impulse vs. Reaction: The Degree of Reaction

Turbines are fundamentally classified by the mechanism through which they extract energy, a concept quantified by the **Degree of Reaction**, $R$. The total energy extracted from the fluid corresponds to a drop in its [stagnation pressure](@entry_id:265293). This drop is composed of a change in [static pressure](@entry_id:275419) and a change in kinetic energy. The Degree of Reaction is defined as the fraction of the total energy transfer that is due to the change in [static pressure](@entry_id:275419) across the runner [@problem_id:1735315]:

$$R = \frac{\text{Energy transfer from static pressure change}}{\text{Total energy transfer}} = \frac{P_1 - P_2}{(P_1 - P_2) + \frac{1}{2}\rho(V_1^2 - V_2^2)}$$

*   **Impulse Turbines ($R \approx 0$):** In a pure impulse turbine, there is no change in [static pressure](@entry_id:275419) across the moving blades ($P_1 = P_2$). The entire [energy transfer](@entry_id:174809) comes from the change in the fluid's kinetic energy as the blades redirect the high-velocity jet. The passages are open to the atmosphere, and the runner essentially acts as a set of moving buckets. The Pelton wheel is the classic example.

*   **Reaction Turbines ($R > 0$):** In a reaction turbine, the [fluid pressure](@entry_id:270067) drops significantly as it flows through the runner. The runner passages are shaped like converging nozzles, so as the fluid expands and accelerates in the relative frame, it pushes on the blades, causing them to rotate. Both the [static pressure](@entry_id:275419) and the kinetic energy of the fluid decrease. Francis and Kaplan turbines are common examples of reaction turbines, often having a high degree of reaction (e.g., $R > 0.5$) [@problem_id:1735315].

### System Performance and Operational Limits

The principles discussed so far describe the idealized behavior of a turbomachine. In practice, performance is affected by losses and the interaction with the larger fluid system.

#### Head, Losses, and Efficiency

The Euler head, $H_e$, represents the theoretical maximum head a pump can deliver. However, internal fluid dynamic losses due to friction on blade surfaces, [flow separation](@entry_id:143331), and turbulence mean that the actual head delivered by the pump is always lower. The **manometric head**, $H_m$, is the actual useful head gain measured across the pump's inlet and outlet flanges. It is the head that is available to overcome the demands of the external piping system, which consist of the static elevation change ($h_{geo}$) and all frictional head losses ($h_f$) [@problem_id:1735311].

The **[hydraulic efficiency](@entry_id:266461)**, $\eta_h$, quantifies these internal losses and is defined as the ratio of the manometric head to the Euler head:

$$\eta_h = \frac{H_m}{H_e}$$

A typical [hydraulic efficiency](@entry_id:266461) for a well-designed pump might be in the range of $0.75$ to $0.95$.

#### Off-Design Operation: Stall and Surge

A turbomachine is designed to operate most efficiently at a specific **design point** (a particular flow rate and rotational speed). When operating conditions deviate from this point (**off-design operation**), performance degrades and potentially destructive instabilities can arise.

*   **Stall:** This is an aerodynamic phenomenon that occurs at the blade level. The flow relative to the blade, $\vec{W}_1$, must approach the blade's leading edge at an appropriate angle. This angle is related to the **angle of attack**, which is the angle between the [relative velocity](@entry_id:178060) vector and the blade's chord line. If the flow rate through an axial fan or [compressor](@entry_id:187840) is reduced while the rotational speed is held constant, the axial velocity component decreases. This changes the inlet [velocity triangle](@entry_id:268727), causing the angle of attack to increase. If the [angle of attack](@entry_id:267009) exceeds a critical value, the flow will separate from the suction surface of the blade, a condition known as **stall**. Stalling leads to a sharp drop in pressure-generating capability, increased noise, and severe vibrations [@problem_id:1735346].

*   **Surge:** This is a macroscopic, system-level instability that primarily affects compressors and pumps. A pump's performance is described by its characteristic curve, which plots head ($H_p$) versus flow rate ($Q$). The piping system also has a [system curve](@entry_id:276345), $H_{sys}(Q)$. The **operating point** is where these two curves intersect. Most pump curves have a negative slope, meaning that as flow rate increases, the head produced decreases. However, at very low flow rates, the curve may reach a peak and then exhibit a region of positive slope. Operating in this positively-sloped region is unstable. If a small disturbance causes the flow rate to decrease, the head produced by the pump also decreases, falling below the head required by the system. This imbalance causes the flow in the entire system to decelerate and even reverse, leading to violent, low-frequency oscillations of flow and pressure known as **surge**. Surge can cause catastrophic damage and must be avoided by ensuring the system's [operating point](@entry_id:173374) remains in the stable, negatively-sloped region of the [pump curve](@entry_id:261367) [@problem_id:1735369].