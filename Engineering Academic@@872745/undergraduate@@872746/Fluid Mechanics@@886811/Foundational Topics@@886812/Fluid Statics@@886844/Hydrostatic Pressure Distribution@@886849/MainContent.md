## Introduction
The study of [fluids at rest](@entry_id:187621), or **[hydrostatics](@entry_id:273578)**, forms a foundational pillar of fluid mechanics, essential for understanding the forces that shape our world, from the pressure at the bottom of the ocean to the stability of a floating ship. This article addresses the core principles governing the behavior of static fluids, providing a bridge from basic [fluid properties](@entry_id:200256) to complex real-world applications. The reader will learn to derive and apply the laws that govern [pressure distribution](@entry_id:275409), [buoyancy](@entry_id:138985), and the forces exerted on [submerged surfaces](@entry_id:273729). This exploration will proceed through three distinct chapters. **Principles and Mechanisms** will derive the fundamental equations of [fluid statics](@entry_id:268932), including Pascal's and Archimedes' principles. **Applications and Interdisciplinary Connections** will demonstrate how these concepts are applied in fields ranging from civil engineering and [naval architecture](@entry_id:268009) to geophysics and biology. Finally, **Hands-On Practices** will offer the opportunity to solve practical problems and solidify understanding. We begin by examining the core principles that dictate [pressure distribution](@entry_id:275409) in a [static fluid](@entry_id:265831).

## Principles and Mechanisms

The previous chapter introduced the fundamental properties of fluids. We now turn our attention to the behavior of [fluids at rest](@entry_id:187621), a state known as **[hydrostatic equilibrium](@entry_id:146746)**. In this state, there are no shear stresses within the fluid; the only [internal stress](@entry_id:190887) is pressure, which acts normal to any surface. The study of [hydrostatics](@entry_id:273578) is foundational to fluid mechanics, with profound implications in fields ranging from [naval architecture](@entry_id:268009) and dam design to meteorology and astrophysics. This chapter will derive the core principles governing [pressure distribution](@entry_id:275409) in static fluids and explore the mechanisms through which hydrostatic forces manifest.

### The Fundamental Equation of Fluid Statics

Consider an infinitesimal fluid element of volume $dV = dx \, dy \, dz$ within a larger fluid body at rest. The forces acting on this element are [surface forces](@entry_id:188034) (due to pressure) and a body force (due to gravity). For the fluid to be in [static equilibrium](@entry_id:163498), the net force on the element must be zero. Let us analyze the forces in the vertical direction, $z$, assuming gravity acts in the $-z$ direction.

The pressure at the center of the element is $P$. The pressure on the bottom face (at $z - dz/2$) is $P - \frac{\partial P}{\partial z} \frac{dz}{2}$, and the pressure on the top face (at $z + dz/2$) is $P + \frac{\partial P}{\partial z} \frac{dz}{2}$. The net pressure force in the $z$-direction is:

$dF_{P,z} = \left(P - \frac{\partial P}{\partial z} \frac{dz}{2}\right) dx\,dy - \left(P + \frac{\partial P}{\partial z} \frac{dz}{2}\right) dx\,dy = -\frac{\partial P}{\partial z} dx\,dy\,dz = -\frac{\partial P}{\partial z} dV$

The body force due to gravity is the weight of the element, acting downward:

$dF_{B,z} = - \rho g \, dV$

where $\rho$ is the fluid density and $g$ is the [acceleration due to gravity](@entry_id:173411). For equilibrium, the sum of these forces is zero:

$-\frac{\partial P}{\partial z} dV - \rho g \, dV = 0$

Dividing by the volume $dV$, we arrive at the fundamental differential equation for [hydrostatics](@entry_id:273578):

$\frac{dP}{dz} = -\rho g$

This equation states that the rate of change of pressure with vertical position is proportional to the local fluid density. The negative sign indicates that pressure increases as we move downward (decreasing $z$). In its more general vector form, where the gravitational acceleration is represented by the vector $\mathbf{g}$, the pressure gradient is given by $\nabla P = \rho \mathbf{g}$. An important consequence is that for a continuous fluid at rest, the pressure is constant across any horizontal plane, regardless of the shape of the container.

For a fluid with constant density $\rho$ (an [incompressible fluid](@entry_id:262924)), we can integrate this equation between two points with vertical separation $h = z_1 - z_2$:

$\int_{P_2}^{P_1} dP = -\int_{z_2}^{z_1} \rho g \, dz = -\rho g \int_{z_2}^{z_1} dz$

$P_1 - P_2 = -\rho g (z_1 - z_2) = \rho g h$

This is the well-known **hydrostatic pressure equation**, which states that the pressure in a continuous, [incompressible fluid](@entry_id:262924) increases linearly with depth. Pressure can be expressed as either **[absolute pressure](@entry_id:144445)**, which is measured relative to a perfect vacuum, or **[gauge pressure](@entry_id:147760)**, which is measured relative to the local atmospheric pressure.

This principle of linear pressure increase allows us to calculate the pressure at the bottom of a container holding multiple, stacked, immiscible liquids. For instance, in a calibration setup involving a sealed cylinder containing layers of oil, water, and a glycerin solution under pressurized gas [@problem_id:1763113], the [absolute pressure](@entry_id:144445) at the bottom is the sum of the gas pressure at the top surface and the pressure contributions from each fluid column. If the gas pressure is $P_{gas}$ and the layers have heights $h_i$ and densities $\rho_i$, the total pressure at the bottom is:

$P_{bottom} = P_{gas} + \sum_i \rho_i g h_i$

This demonstrates the additive nature of [hydrostatic pressure](@entry_id:141627). Starting from a known pressure at a reference point, one can determine the pressure at any other depth by summing the $\rho g h$ terms for all fluids traversed.

### Pascal's Principle: Transmission of Pressure

A profound consequence of the hydrostatic equations for an enclosed, continuous fluid is **Pascal's Principle**. Named after the French physicist Blaise Pascal, it states that a pressure change applied to any part of an enclosed, incompressible fluid is transmitted undiminished to every portion of the fluid and to the walls of the containing vessel.

This principle is the basis for [hydraulic systems](@entry_id:269329), which use fluids to transmit and multiply force. A classic example is the [hydraulic press](@entry_id:270434) or lift, consisting of two connected cylinders of different areas, $A_1$ and $A_2$, filled with a hydraulic fluid. If a force $F_1$ is applied to the smaller piston (area $A_1$), it creates a pressure change $\Delta P = F_1/A_1$. This pressure change is transmitted throughout the fluid, exerting an upward force on the larger piston given by $F_2 = \Delta P \cdot A_2$. This leads to the famous force-multiplication relationship:

$F_2 = F_1 \frac{A_2}{A_1}$

Since $A_2 > A_1$, the output force $F_2$ is larger than the input force $F_1$.

In practical applications, the elevation difference between the pistons must also be considered. Suppose the smaller piston is at a height $h$ above the larger piston, as might be found in a [materials testing](@entry_id:196870) press [@problem_id:1763135]. The pressure at the level of the larger piston, $P_2$, is related to the pressure at the smaller piston, $P_1$, by the hydrostatic equation: $P_2 = P_1 + \rho g h$. The pressures under the pistons are $P_1 = F_1/A_1$ and $P_2 = F_2/A_2$. Combining these gives:

$\frac{F_2}{A_2} = \frac{F_1}{A_1} + \rho g h$

This equation shows that the force required at the small piston, $F_1$, must overcome not only the load on the large piston but also the hydrostatic pressure head due to the elevation difference. The term $\rho g h A_2$ represents the weight of a fluid column of height $h$ and area $A_2$, which contributes to the [force balance](@entry_id:267186).

### Buoyancy and Archimedes' Principle

When an object is partially or fully submerged in a fluid, it experiences an upward force from the surrounding fluid. This force, known as the **[buoyant force](@entry_id:144145)**, arises because the pressure on the bottom surface of the object is greater than the pressure on its top surface.

**Archimedes' Principle** provides a beautifully simple and powerful quantification of this force: a body wholly or partially submerged in a fluid is buoyed up by a force equal to the weight of the fluid it displaces.

$F_B = \rho_{fluid} g V_{sub}$

Here, $\rho_{fluid}$ is the density of the fluid and $V_{sub}$ is the volume of the object that is submerged. The net force on the object is the difference between this [buoyant force](@entry_id:144145) and the object's weight, $W = m_{obj} g = \rho_{obj} g V_{tot}$.

For a **floating object**, it is in static equilibrium, so the net force is zero. The buoyant force exactly balances its weight: $F_B = W$. This leads to a simple and useful relationship. For a uniform object like a wooden log floating in a lake [@problem_id:1763115]:

$\rho_{fluid} g V_{sub} = \rho_{obj} g V_{tot}$

$\frac{V_{sub}}{V_{tot}} = \frac{\rho_{obj}}{\rho_{fluid}}$

This shows that the fraction of the object's volume that is submerged is equal to the ratio of its average density to the fluid's density. If the object's density is greater than the fluid's, it cannot float and will sink.

This principle is not limited to liquids. Any object immersed in any fluid, including gases, experiences a buoyant force. A hot air balloon provides a classic example [@problem_id:1763144]. The balloon displaces a large volume of the cooler, denser ambient air, creating an upward buoyant force $F_B = \rho_{out} g V$. The total weight of the system is the sum of the weight of the balloon's envelope and equipment ($m_{env} g$) and the weight of the less dense hot air inside ($m_{in} g = \rho_{in} g V$). The net lifting force is therefore:

$F_{net} = F_B - W_{total} = (\rho_{out} - \rho_{in}) g V - m_{env} g$

The densities can be related to temperature and pressure using the [ideal gas law](@entry_id:146757) ($\rho = PM/(\mathcal{R}T)$). Since the hot air inside is hotter ($T_{in} > T_{out}$), its density is lower ($\rho_{in}  \rho_{out}$), creating a net positive [buoyancy](@entry_id:138985) that can lift the balloon.

Archimedes' principle can also be generalized to fluids with non-uniform density, such as a stratified ocean where density varies with depth [@problem_id:1763111]. In this case, the buoyant force is still the weight of the displaced fluid, but this weight must be found by integrating the variable density over the submerged volume:

$F_B = g \int_{V_{sub}} \rho_{fluid}(z) \, dV$

For a fully submerged cylinder resting on the seabed in a fluid where density varies linearly with depth, $\rho_{fluid}(z) = \rho_s(1 + \alpha z)$, the buoyant force can be calculated using this integral. The final equilibrium of the cylinder is determined by the balance of its weight, the [buoyant force](@entry_id:144145), and the normal force from the seabed.

### Hydrostatic Forces on Submerged Surfaces

Engineers must often calculate the total force exerted by a fluid on a submerged surface, such as a dam, a lock gate, or a viewing port in an underwater vehicle [@problem_id:1763143]. This force is the result of the [pressure distribution](@entry_id:275409) acting over the area.

For a **submerged plane surface**, the pressure is not uniform; it increases with depth. The total resultant force, $F_R$, is found by integrating the pressure over the area:

$F_R = \int_A P \, dA$

For an incompressible fluid, where $P = \rho g h$, and $h$ is the vertical depth to a point on the surface. It can be shown that the resultant force is equal to the pressure at the **[centroid](@entry_id:265015)** of the surface multiplied by the total area of the surface:

$F_R = P_c A = (\rho g h_c) A$

Here, $h_c$ is the vertical depth to the [centroid](@entry_id:265015) (geometric center) of the area $A$.

While the magnitude of the force is determined by the pressure at the centroid, the force does not, in general, act at the centroid. The point of application of the resultant force is called the **[center of pressure](@entry_id:275898) (CP)**. Because pressure increases with depth, the lower portions of the surface are subjected to greater forces than the upper portions. Consequently, the [center of pressure](@entry_id:275898) is always located vertically below the centroid for any non-horizontal surface.

The location of the [center of pressure](@entry_id:275898) is found by taking moments of the pressure force about an axis. Let $y$ be a coordinate in the plane of the surface, measured downwards from the point where the plane intersects the free surface. The vertical depth is then $h = y \sin \theta$, where $\theta$ is the inclination angle of the plane from the horizontal. The location of the CP, $y_p$, is given by:

$y_p F_R = \int_A y P \, dA = \int_A y (\rho g y \sin \theta) \, dA = \rho g \sin \theta \int_A y^2 \, dA$

The integral $\int_A y^2 \, dA$ is the [second moment of area](@entry_id:190571) of the surface, $I_x$, about the free-surface axis. By the [parallel axis theorem](@entry_id:168514), $I_x = I_{xc} + A y_c^2$, where $I_{xc}$ is the [second moment of area](@entry_id:190571) about the centroidal axis parallel to the free-surface axis. Substituting and simplifying leads to the formula for the location of the [center of pressure](@entry_id:275898):

$y_p = y_c + \frac{I_{xc}}{y_c A}$

This explicitly shows that $y_p > y_c$, meaning the [center of pressure](@entry_id:275898) is always deeper than the centroid. For an underwater circular viewing port of radius $R$ [@problem_id:1763143], the centroidal [second moment of area](@entry_id:190571) is $I_{xc} = \pi R^4 / 4$. The vertical separation between the [center of pressure](@entry_id:275898) and the centroid can be shown to be $\Delta h = (y_p - y_c) \sin \theta = \frac{I_{xc} \sin^2\theta}{h_c A} = \frac{R^2 \sin^2\theta}{4 h_c}$. This separation decreases as the depth of [submersion](@entry_id:161795), $h_c$, increases.

### Hydrostatics in Non-Inertial Systems

The hydrostatic principles discussed so far assume the fluid is in an inertial (non-accelerating) reference frame. If the fluid and its container are undergoing acceleration, these principles must be modified. The effect of a [constant acceleration](@entry_id:268979) $\mathbf{a}$ is to create an additional "inertial force" throughout the fluid. This is conveniently handled by defining an **[effective gravity](@entry_id:188792) vector**, $\mathbf{g}_{eff} = \mathbf{g} - \mathbf{a}$. The pressure gradient then aligns with this effective gravity: $\nabla P = \rho \mathbf{g}_{eff}$.

A common case is **uniform linear acceleration**. Consider a tank of liquid propellant in a rocket accelerating vertically upwards with acceleration $a$ [@problem_id:1763101]. Here, $\mathbf{g} = -g \hat{\mathbf{k}}$ and $\mathbf{a} = a \hat{\mathbf{k}}$. The [effective gravity](@entry_id:188792) is $\mathbf{g}_{eff} = (-g-a)\hat{\mathbf{k}}$. The pressure gradient becomes:

$\frac{dP}{dz} = -\rho(g+a)$

The pressure now increases with depth at a faster rate than in the stationary case. The pressure at the bottom of a tank of height $H$ is $P_{bottom} = P_{top} + \rho(g+a)H$. This increased pressure is responsible for the sensation of feeling "heavier" in an accelerating elevator.

Another important case is **[rigid-body rotation](@entry_id:268623)**. When a container of fluid is spun at a constant [angular velocity](@entry_id:192539) $\omega$ about a vertical axis, the fluid eventually rotates as a solid body. In a reference frame rotating with the fluid, each fluid particle experiences an outward centrifugal acceleration $\mathbf{a} = -\omega^2 r \hat{\mathbf{r}}$. The effective body force per unit mass is $\mathbf{g}_{eff} = \mathbf{g} - \mathbf{a} = -g\hat{\mathbf{k}} + \omega^2 r \hat{\mathbf{r}}$. The pressure gradient must balance this effective body force:

$\nabla P = \rho(-g\hat{\mathbf{k}} + \omega^2 r \hat{\mathbf{r}})$

This leads to the pressure field $P(r,z) = P_0 - \rho g z + \frac{1}{2} \rho \omega^2 r^2$. Surfaces of constant pressure (isobars), including the free surface, are no longer flat. The free surface takes on a parabolic shape, with the fluid level rising at the edges and dipping in the center [@problem_id:1763148]. The equation for the free surface height $z_s(r)$ is $z_s(r) = z_c + \frac{\omega^2 r^2}{2g}$, where $z_c$ is the height at the center. The volume of the fluid must be conserved to determine the value of $z_c$ relative to the initial fill height.

### Pressure Variation in Compressible Fluids

Our analysis has primarily assumed [incompressible fluids](@entry_id:181066), where density $\rho$ is constant. For gases, such as in Earth's atmosphere, density varies significantly with pressure and temperature, and the [incompressibility](@entry_id:274914) assumption is invalid. To analyze [pressure distribution](@entry_id:275409) in a [compressible fluid](@entry_id:267520), the hydrostatic equation $\frac{dP}{dz} = -\rho g$ must be solved simultaneously with an equation of state that relates density to pressure and temperature.

A common simplified model for the atmosphere is the **isothermal model**, which assumes the temperature $T$ is constant [@problem_id:1763116]. Treating air as an ideal gas, its density is given by $\rho = \frac{P M}{R T}$, where $M$ is the [molar mass](@entry_id:146110) and $R$ is the [universal gas constant](@entry_id:136843). Substituting this into the hydrostatic equation gives:

$\frac{dP}{dz} = - \left(\frac{M g}{R T}\right) P$

This is a first-order differential equation for $P(z)$. Separating variables and integrating from sea level (where $z=0$ and $P=P_0$) yields the **[barometric formula](@entry_id:261774)**:

$P(z) = P_0 \exp\left(-\frac{M g}{R T} z\right)$

This result shows that, under isothermal conditions, atmospheric pressure decreases exponentially with altitude. The quantity $H = RT/Mg$ is known as the **[scale height](@entry_id:263754)**, which represents the vertical distance over which the pressure decreases by a factor of $e \approx 2.718$. For example, the altitude at which the pressure drops to one-quarter of its sea-level value can be found by solving $1/4 = \exp(-z/H)$, which gives $z = H \ln 4$.

### Stability of Floating and Submerged Bodies

A final critical concept in [hydrostatics](@entry_id:273578) is the **stability** of a body in a fluid. A body in equilibrium is stable if it returns to its original position after a small [angular displacement](@entry_id:171094). It is unstable if it continues to move away, and neutrally stable if it remains in the new position.

For a fully submerged body, stability is straightforward. The two forces acting on it are its weight ($W$), acting through its **[center of gravity](@entry_id:273519) (G)**, and the [buoyant force](@entry_id:144145) ($F_B$), acting through the **[center of buoyancy](@entry_id:265838) (B)**, which is the centroid of the displaced volume. For stable equilibrium, the [center of gravity](@entry_id:273519) G must be below the [center of buoyancy](@entry_id:265838) B. If disturbed, the torque created by the couple of $W$ and $F_B$ will restore the body to its original orientation.

For a floating body, the situation is more complex. When a floating body, such as a pontoon or ship [@problem_id:1763104], is tilted, the shape of the displaced volume changes, causing the [center of buoyancy](@entry_id:265838) B to shift. The weight $W$ still acts through the fixed center of gravity G, while the [buoyant force](@entry_id:144145) $F_B$ now acts through the new [center of buoyancy](@entry_id:265838), B'. The vertical line extending upward from B' intersects the original centerline of the body at a point called the **[metacenter](@entry_id:266729) (M)**.

The stability of the floating body depends on the [relative position](@entry_id:274838) of M and G.
- If M is above G, the couple formed by $W$ and $F_B$ creates a restoring torque that brings the body back to its upright position. The body is stable.
- If M is below G, the couple creates an overturning torque that capsizes the body. The body is unstable.
- If M coincides with G, there is no restoring or overturning torque. The body is neutrally stable.

The distance from the [center of gravity](@entry_id:273519) to the [metacenter](@entry_id:266729), known as the **[metacentric height](@entry_id:267540) (GM)**, is the primary quantitative measure of a floating body's [initial stability](@entry_id:181141). A positive $GM$ indicates stability. The position of the [metacenter](@entry_id:266729) is calculated using the formula:

$KM = KB + BM$

where $K$ is the keel (bottom of the vessel), $KB$ is the vertical distance from the keel to the [center of buoyancy](@entry_id:265838), and $BM$ is the metacentric radius. $BM$ is given by:

$BM = \frac{I_T}{V}$

Here, $V$ is the submerged volume of the hull, and $I_T$ is the [second moment of area](@entry_id:190571) of the waterplane (the cross-sectional area of the hull at the water's surface) about the axis of rotation (e.g., the longitudinal axis for rolling). A wide, flat waterplane (large $I_T$) increases $BM$ and enhances stability. The stability condition is then $GM = KB + BM - KG > 0$, where $KG$ is the height of the center of gravity above the keel. Determining the maximum height at which equipment can be placed on a pontoon [@problem_id:1763104] is a direct application of this principle, involving a trade-off between the destabilizing effect of a high [center of gravity](@entry_id:273519) and the stabilizing effect of the hull's shape.