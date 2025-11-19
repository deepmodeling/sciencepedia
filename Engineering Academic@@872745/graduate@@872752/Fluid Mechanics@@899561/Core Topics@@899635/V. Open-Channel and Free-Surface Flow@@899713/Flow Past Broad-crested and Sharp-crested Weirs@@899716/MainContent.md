## Introduction
The study of flow past broad-crested and sharp-crested weirs is a foundational topic in [open-channel hydraulics](@entry_id:273093), offering essential tools for flow measurement and control. While both structures serve a similar purpose, they operate on distinct physical principles that are often simplified in introductory treatments. This article addresses the gap between [ideal theory](@entry_id:184127) and real-world complexity by systematically exploring the governing dynamics of weir flow. The reader will first delve into the core **Principles and Mechanisms**, starting with the concept of [critical flow](@entry_id:275258) on broad-crested weirs and incorporating refinements for real-fluid effects like friction, curvature, and surface tension. Subsequently, the discussion will expand to cover the diverse **Applications and Interdisciplinary Connections**, showcasing how these hydraulic principles are applied in fields ranging from [civil engineering](@entry_id:267668) and sediment transport to [magnetohydrodynamics](@entry_id:264274) and [aeroacoustics](@entry_id:266763). Finally, the **Hands-On Practices** section will provide opportunities to apply these concepts to practical problems, solidifying the theoretical understanding gained. This structured journey provides a comprehensive graduate-level understanding of weir hydraulics.

## Principles and Mechanisms

The analysis of flow over weirs constitutes a cornerstone of [open-channel hydraulics](@entry_id:273093), providing both a practical means for flow measurement and a rich context for understanding fundamental fluid dynamics principles. Broad-crested and sharp-crested weirs, while serving similar purposes, operate on distinct physical mechanisms and are subject to different real-fluid corrections. This chapter systematically deconstructs the principles governing these flows, beginning with the [ideal theory](@entry_id:184127) of the [broad-crested weir](@entry_id:200852) and progressively incorporating the complexities of real-world phenomena.

### The Broad-Crested Weir: Critical Flow as a Control Mechanism

The defining characteristic of a [broad-crested weir](@entry_id:200852) is its ability to establish **[critical flow](@entry_id:275258)** on its crest. This phenomenon serves as a hydraulic control, creating a unique relationship between the upstream water level and the discharge. To understand this, we must first examine the concept of **[specific energy](@entry_id:271007)**.

For a rectangular channel, the [specific energy](@entry_id:271007), $E$, is the energy head per unit weight of fluid measured relative to the channel bed:

$$E = y + \frac{V^2}{2g}$$

where $y$ is the flow depth, $V$ is the [mean velocity](@entry_id:150038), and $g$ is the [acceleration due to gravity](@entry_id:173411). Using the discharge per unit width, $q = Vy$, we can express the [specific energy](@entry_id:271007) as a function of depth for a constant discharge:

$$E(y) = y + \frac{q^2}{2gy^2}$$

A plot of this function reveals that for any given $q$, there exists a minimum [specific energy](@entry_id:271007), $E_{min}$, required to pass the flow. The depth at which this minimum occurs is the **[critical depth](@entry_id:275576)**, $y_c$. At this point, the **Froude number**, $Fr = V/\sqrt{gy}$, is exactly unity. Differentiating the energy equation with respect to $y$ and setting $dE/dy = 0$ yields the conditions for [critical flow](@entry_id:275258):

$$y_c = \left(\frac{q^2}{g}\right)^{1/3}$$

$$E_{min} = \frac{3}{2}y_c$$

A [broad-crested weir](@entry_id:200852) functions by forcing the flow to pass through this critical state. As the fluid accelerates from a subcritical state ($Fr  1$) upstream to flow over the elevated crest, it passes through the [critical depth](@entry_id:275576). The structure acts as a choke, compelling the flow to adopt the most efficient state (minimum energy) to overcome the obstacle.

Alternatively, consider the scenario where the upstream [specific energy](@entry_id:271007), $E$, is fixed. The discharge $q$ can be expressed as a function of depth $h$:

$$q(h) = h \sqrt{2g(E-h)}$$

Maximizing this function by setting $dq/dh=0$ reveals that the maximum possible discharge for a given specific energy also occurs at the [critical depth](@entry_id:275576), $h_c = \frac{2}{3}E$. This principle of **maximum discharge** is what makes the weir a reliable measuring device. The flow naturally adjusts to the state that maximizes throughput for the available energy.

The stability of this [critical flow](@entry_id:275258) state is a subtle but profound concept. While it represents a maximum of the discharge function, this very property implies an inherent sensitivity. A dimensionless stability parameter, $\mathcal{S}$, can be defined to quantify the curvature of the discharge function at the critical point [@problem_id:507245]. By taking the second derivative of $q(h)$ and evaluating it at $h_c$, we find:

$$\mathcal{S} = \frac{h_c^2}{q_c} \left. \frac{d^2q}{dh^2} \right|_{h=h_c} = -3$$

The negative value indicates that the discharge function has a sharp, downward-curving maximum at the critical point. This sharpness is what "pins" the flow to the [critical state](@entry_id:160700), but it also signifies that the state is marginally stable, a characteristic feature of transitions between [flow regimes](@entry_id:152820).

### The Ideal Discharge Relationship

For an idealized [broad-crested weir](@entry_id:200852), we can derive a simple and elegant discharge formula. Consider a weir of height $P$ with an upstream head $H$ measured above the crest. The total energy upstream, relative to the crest, is $H$ (assuming negligible approach velocity, $V_1 \approx 0$). If this energy is conserved, it must equal the [specific energy](@entry_id:271007) at the crest, where flow is critical.

$$H = E_{min} = \frac{3}{2}y_c$$

This directly gives the [critical depth](@entry_id:275576) on the crest as $y_c = \frac{2}{3}H$. Substituting this into the [critical flow](@entry_id:275258) equation $q = \sqrt{gy_c^3}$ yields the ideal discharge formula:

$$q_{ideal} = \sqrt{g} \left(\frac{2}{3}H\right)^{3/2} = \left(\frac{2}{3}\right)^{3/2} \sqrt{g} H^{3/2}$$

In practice, this is often written with a **[discharge coefficient](@entry_id:276642)**, $C_d$, to account for the simplifying assumptions made:

$$q = C_d \left(\frac{2}{3}\right)^{3/2} \sqrt{g} H^{3/2}$$

For an ideal, frictionless, long-crested weir with a uniform approach flow, $C_d = 1$. The following sections explore phenomena that cause $C_d$ to deviate from unity.

### Refinements to the Broad-Crested Weir Theory

The ideal formula provides a valuable baseline, but real-world applications require accounting for several additional physical effects.

#### Effect of Upstream Velocity Profile

The assumption of a uniform upstream velocity profile, where the kinetic energy head is simply $V_1^2/(2g)$, is a significant simplification. Real velocity profiles in open channels are non-uniform due to boundary friction. To account for this, we introduce the **[kinetic energy correction factor](@entry_id:263759)**, $\alpha$, defined as:

$$\alpha = \frac{\int_A u^3 dA}{V^3 A}$$

where $u$ is the local velocity, $A$ is the cross-sectional area, and $V$ is the [mean velocity](@entry_id:150038). For [uniform flow](@entry_id:272775), $\alpha=1$; for any non-uniform profile, $\alpha  1$. The upstream specific energy is more accurately written as $E_1 = y_1 + \alpha_1 V_1^2/(2g)$.

The influence of this factor can be significant. For instance, consider a flow with a power-law velocity profile upstream of a weir [@problem_id:507172]. The value of $\alpha_1$ can be calculated directly from the profile shape. Applying the [energy conservation](@entry_id:146975) principle between the upstream section and the critical section on the crest, the equation for the required weir height $P$ becomes dependent on $\alpha_1$ and the upstream Froude number. This demonstrates that an accurate energy audit, which includes the effects of the velocity distribution, is essential for precise predictions.

#### Effect of Streamline Curvature

The [ideal theory](@entry_id:184127) assumes that streamlines over the weir crest are parallel and straight, which implies a hydrostatic pressure distribution. This is only true for very long weirs. On weirs of moderate length, streamlines are curved (concave downwards), inducing a centripetal acceleration that reduces the pressure below the hydrostatic value.

This effect can be modeled using a first-order correction based on the **Boussinesq approximation** [@problem_id:507126]. The [specific energy](@entry_id:271007) equation is modified to include a term related to the [streamline](@entry_id:272773) [radius of curvature](@entry_id:274690), $R$:

$$E = y + \frac{V^2}{2g} - \frac{y^2}{3R}$$

For streamlines curving downwards, $R$ is negative, so this term effectively adds energy. By modeling the curvature as being proportional to the local depth ($R = -\beta y$, where $\beta$ is a geometric constant), one can re-derive the discharge relationship by maximizing $q$ for a given total head $H$. This analysis yields a [discharge coefficient](@entry_id:276642) that is a function of the curvature parameter:

$$C_d = \frac{3\beta}{3\beta + 1}$$

Since $\beta$ is finite for any curved flow, this result shows that streamline curvature always leads to a [discharge coefficient](@entry_id:276642) less than one. This correction is crucial for accurate gauging with shorter broad-crested weirs where the flow does not have sufficient length to achieve parallel [streamlines](@entry_id:266815).

#### Frictional Effects on Long Crests

While short weirs are dominated by curvature effects, very long weirs are influenced by friction along the crest. Here, the [specific energy](@entry_id:271007) is not constant, but decreases along the direction of flow. The water surface is not level but follows a profile described by the **Gradually Varied Flow (GVF)** equation. For a horizontal crest ($S_0=0$), this equation is:

$$\frac{dy}{dx} = \frac{-S_f}{1 - Fr^2}$$

where $S_f$ is the [friction slope](@entry_id:265665), which can be modeled by empirical laws like the Chezy or Manning equations. A common scenario involves a weir that is long enough for friction to be important but ends in a free overfall, which forces the flow to be critical ($Fr=1$) at the downstream edge. This provides a critical boundary condition to solve the GVF equation [@problem_id:507151]. By integrating the ODE from the known [critical depth](@entry_id:275576) at the end of the weir, one can determine the entire [water surface profile](@entry_id:270649) along the crest, providing a detailed picture of how friction modifies the flow and highlighting the interplay between [critical flow](@entry_id:275258) control and frictional resistance.

#### The Weir as a Hydraulic Control

A weir only functions as a control structure if it is the dominant hydraulic feature governing the flow. In a long channel with a mild slope, the flow might initially be a uniform [subcritical flow](@entry_id:276823) at its **[normal depth](@entry_id:265980)**, $y_n$. To act as a control, a weir must be high enough to force the flow through the [critical state](@entry_id:160700) at its crest.

The minimum weir height, $P_{min}$, required to achieve this can be determined by an [energy balance](@entry_id:150831) [@problem_id:507223]. The [specific energy](@entry_id:271007) of the approaching [uniform flow](@entry_id:272775), including its kinetic energy component calculated from Manning's equation, must be just sufficient to provide the minimum energy required for [critical flow](@entry_id:275258) over the weir crest. The condition is:

$$E_{upstream} = y_n + \frac{V_n^2}{2g} = P_{min} + E_{min} = P_{min} + \frac{3}{2}y_c$$

Solving for $P_{min}$ provides a criterion for designing weirs that will reliably control the flow in a given channel, ensuring that the upstream depth is uniquely related to discharge and not influenced by downstream conditions.

#### Complex Geometries and Multiple Controls

The principle of [energy conservation](@entry_id:146975) and [critical flow](@entry_id:275258) can be extended to analyze flow over weirs with complex geometries, such as those with varying width and multiple crests. In such cases, the control section will form at the location that presents the greatest "choke" to the flow—that is, the location which requires the highest upstream energy to pass a given discharge.

A fascinating thought experiment involves a weir with two crests of height $z_c$ and width $B_c$, separated by a trough of height $z_t$ and width $B_t$ [@problem_id:507209]. A unique upstream energy exists where the flow can become critical at all three locations simultaneously. This requires the total energy head, $E_{up}$, to be equal at each point:

$$E_{up} = z_c + \frac{3}{2}y_c = z_t + \frac{3}{2}y_t$$

Using the continuity of discharge and the [critical flow](@entry_id:275258) condition, the depths $y_c$ and $y_t$ can be related through the width ratio. Solving this system yields the specific upstream energy required for this tripartite [critical state](@entry_id:160700). This example powerfully illustrates how both bed elevation and channel width contribute to establishing hydraulic control.

### The Sharp-Crested Weir

In contrast to a [broad-crested weir](@entry_id:200852), a **[sharp-crested weir](@entry_id:262463)** is a thin vertical plate that forces the flow to spring free as a jet, known as the **nappe**. The underside of the nappe is typically ventilated to the atmosphere. The flow field is complex, featuring significant [streamline](@entry_id:272773) curvature and a contraction of the nappe as it passes over the crest.

Due to this complexity, a purely theoretical derivation of the discharge is not feasible. Instead, the discharge formula takes a similar form to the ideal [broad-crested weir](@entry_id:200852) equation, but relies on an empirically determined [discharge coefficient](@entry_id:276642), $C_d$:

$$q = C_d \frac{2}{3} \sqrt{2g} H^{3/2}$$

For a standard, high, well-ventilated weir with negligible approach velocity, $C_d$ is approximately 0.61-0.62. This coefficient implicitly accounts for the energy losses and the contraction of the nappe.

### Real-Fluid Effects in Sharp-Crested Weirs

The performance of sharp-crested weirs is sensitive to several real-fluid effects that are often negligible in other contexts.

#### Nappe Ventilation

The standard [discharge coefficient](@entry_id:276642) assumes the pressure in the cavity beneath the nappe is atmospheric. If the cavity is unventilated, the moving nappe will entrain and eject air. This reduces the pressure in the cavity below atmospheric, creating a pressure difference $\Delta p$. This suction effect pulls the nappe downwards, altering its trajectory and increasing the effective head driving the flow, thus increasing the discharge.

A simple first-order model treats this effect as an additional effective head, $h_{eff} = \kappa \Delta p / (\rho g)$, where $\kappa$ is a constant [@problem_id:507157]. For a small pressure drop, a [binomial expansion](@entry_id:269603) of the discharge formula shows that the [discharge coefficient](@entry_id:276642) increases linearly with the [pressure drop](@entry_id:151380):

$$\Delta C_d \approx \frac{3}{2} \kappa \frac{\Delta p}{\rho g H}$$

A more sophisticated analysis models the entire system at equilibrium, where the rate of air [entrainment](@entry_id:275487), $Q_{air,out}$, equals the rate of air leakage into the cavity, $Q_{air,in}$ [@problem_id:507216]. This can involve complex feedback loops. For example, the entrainment rate depends on the [interfacial friction](@entry_id:201343), which may itself be a function of the [pressure drop](@entry_id:151380). This can lead to a quadratic equation for the equilibrium pressure difference. In some cases, for a sufficiently strong feedback, no stable real solution for the pressure difference may exist, predicting a "runaway" condition where the nappe becomes unstable and collapses against the weir face. This advanced model demonstrates the rich [system dynamics](@entry_id:136288) that can arise from the coupling of fluid flow and pressure feedback.

#### Surface Tension

At low heads, when the depth of flow over the weir is small, surface tension can become a dominant physical effect. The high curvature of the free surface as it bends over the sharp crest induces a pressure difference across the liquid-air interface (the Laplace pressure). This acts as a resistance to the flow.

One way to model this is to conceptualize a **capillary [head loss](@entry_id:153362)**, $h_\sigma$, which effectively reduces the driving head to $H_{eff} = H - h_\sigma$ [@problem_id:507166]. This head loss is proportional to the surface tension coefficient $\sigma$ and inversely proportional to the radius of curvature of the nappe. Assuming the curvature scales with the upstream head $H$, the first-order relative correction to the discharge can be derived:

$$\frac{q - q_0}{q_0} \approx -\frac{3}{2 \beta Bo}$$

where $Bo = \rho g H^2 / \sigma$ is the **Bond number**, representing the ratio of gravitational forces to surface tension forces. The negative sign confirms that surface tension reduces the discharge, and the inverse dependence on $Bo$ correctly shows that the effect becomes more pronounced at lower heads (smaller $Bo$).

A more fundamental approach incorporates the surface tension effect directly into the specific energy equation [@problem_id:507121]. An effective pressure term is added to account for the capillary effects, modifying the energy at the crest. Minimizing this new [specific energy](@entry_id:271007) function to find the [critical state](@entry_id:160700) no longer yields $Fr=1$. Instead, it results in a new criterion that relates the **Weber number**, $We = \rho q^2 / (\sigma h_0)$, which is the ratio of inertial to surface tension forces, to a parameter $\zeta = \rho g h_0^2 / (\alpha \sigma)$, which compares gravitational to surface tension energies. This approach reveals that surface tension alters the very nature of the critical condition at the crest, providing a deeper insight into low-head weir flows.