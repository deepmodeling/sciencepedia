## Introduction
The transport of momentum and energy are cornerstones in the study of [fluid mechanics](@entry_id:152498), dictating the behavior of nearly every flow imaginable. These [transport phenomena](@entry_id:147655) are quantified by **momentum flux** and **energy flux**, concepts that provide a powerful bridge between the microscopic dynamics of a fluid and the macroscopic forces and energy transfers that shape our world. While fundamental, the full power of these concepts is revealed when their connections are explored across different [flow regimes](@entry_id:152820) and disciplines, from the frictionless glide of an ideal fluid to the chaotic energy transfer in a turbulent cascade. This article addresses the need for a unified perspective, demonstrating how the careful accounting of energy and momentum provides a robust framework for analyzing a vast array of physical systems.

Over the next three chapters, you will embark on a comprehensive exploration of these critical concepts. The journey begins with a deep dive into the core **Principles and Mechanisms**, where we will derive the concepts from first principles in ideal flows, extend them to real fluids to understand forces and dissipation, and unpack their crucial role in the complex energetics of turbulence. Following this theoretical foundation, we will survey the remarkable breadth of **Applications and Interdisciplinary Connections**, showcasing how engineers and scientists use momentum and energy flux to design [turbomachinery](@entry_id:276962), predict [aerodynamic sound](@entry_id:191122), and model phenomena from ocean currents to the evolution of the cosmos. Finally, a series of **Hands-On Practices** will provide you with the opportunity to apply these principles to classic problems, solidifying your understanding of how flux-based analysis is put into practice.

## Principles and Mechanisms

In the study of [fluid mechanics](@entry_id:152498), the transport of momentum and energy are central themes that dictate the behavior of flows, from the silent glide of a glider to the chaotic churning of a river rapid. These transport phenomena are quantified by the concepts of **[momentum flux](@entry_id:199796)** and **[energy flux](@entry_id:266056)**, which represent the rate at which momentum and energy are carried across a given surface. This chapter delves into the fundamental principles and mechanisms governing these fluxes, exploring their role in ideal fluids, their connection to macroscopic forces and energy losses in real fluids, and their critical function in the [complex dynamics](@entry_id:171192) of turbulence.

### The Interplay of Momentum and Energy in Ideal Flows

The foundational link between momentum and energy flux is most elegantly revealed in the study of ideal fluids—those that are incompressible and inviscid (frictionless). The motion of such a fluid is governed by the Euler equation, which is a statement of Newton's second law applied to a fluid element. For a steady flow in a uniform gravitational field, the Euler equation can be integrated along a [streamline](@entry_id:272773), a path traced by a fluid particle. This integration yields one of the most celebrated results in fluid dynamics: the Bernoulli equation.

Consider an incompressible, [inviscid fluid](@entry_id:198262) of constant density $\rho$. Integrating the steady Euler equation along a streamline gives:

$$
\frac{p}{\rho} + \frac{1}{2}v^2 + gz = \text{Constant}
$$

Here, $p$ is the fluid pressure, $v$ is the fluid speed, and $z$ is the vertical height. While derived from the momentum equation, each term in the Bernoulli equation has a distinct energy interpretation. A [dimensional analysis](@entry_id:140259) confirms that each term has units of energy per unit mass (e.g., $m^2/s^2$).

-   The term $\frac{1}{2}v^2$ is immediately recognizable as the **kinetic energy** per unit mass.
-   The term $gz$ is the **gravitational potential energy** per unit mass.
-   The term $\frac{p}{\rho}$ is often called the **[flow work](@entry_id:145165)** or **[pressure potential](@entry_id:154481) energy** per unit mass. It represents the work done by pressure forces to move a unit mass of fluid into or out of a region.

Therefore, the constant in the Bernoulli equation represents the **total mechanical energy per unit mass** of the fluid [@problem_id:1746420]. This principle implies that in a steady, [ideal flow](@entry_id:261917), mechanical energy is conserved along a [streamline](@entry_id:272773). As the fluid accelerates, its kinetic energy increases, which must be balanced by a decrease in its pressure or potential energy. This inverse relationship between speed and pressure is the underlying principle for [aerodynamic lift](@entry_id:267070) and the operation of devices like venturi meters.

### Momentum Flux and Macroscopic Forces

While the Bernoulli equation provides a local, streamline-based view, the concept of [momentum flux](@entry_id:199796) is exceptionally powerful when applied in an integral sense to a finite [control volume](@entry_id:143882). The [net force](@entry_id:163825) exerted on an object by a fluid is equal to the net rate at which momentum flows out of a [control volume](@entry_id:143882) surrounding the object.

A classic application of this principle is the calculation of drag on a submerged body from measurements of the [velocity deficit](@entry_id:269642) in its wake [@problem_id:496618]. Consider a stationary body in a uniform stream of velocity $U_\infty$. The body imparts a force on the fluid, slowing it down and creating a region of reduced velocity known as the wake. To calculate the drag force, $D'$, per unit span, we can define a large rectangular [control volume](@entry_id:143882) enclosing the body. The upstream boundary is in the undisturbed flow, the top and bottom boundaries are far from the body where the flow is also undisturbed, and the downstream boundary is located far behind the body, cutting through the wake.

By applying the [integral momentum theorem](@entry_id:201053), the drag force exerted by the fluid on the body is found to be equal and opposite to the force exerted by the body on the fluid. This force manifests as a reduction in the [momentum flux](@entry_id:199796) at the downstream boundary compared to the upstream boundary. If we assume the pressure far downstream has recovered to the upstream free-stream pressure $p_\infty$, the drag force is solely due to this momentum deficit. For a two-dimensional wake with a [velocity profile](@entry_id:266404) $u(y)$, the drag per unit span is given by:

$$
D' = \int_{\text{wake}} \rho (U_\infty - u(y)) u(y) \, dy
$$

This equation states that the drag is the integral of the mass flux through an element of the wake, $\rho u(y) dy$, multiplied by the [velocity deficit](@entry_id:269642) at that location, $(U_\infty - u(y))$. For a hypothetical wake profile given by $u(y) = U_\infty - \Delta U \cos^2(\frac{\pi y}{2\delta})$ for $|y| \leq \delta$, where $\Delta U$ is the maximum velocity defect at the centerline, this integral can be evaluated to yield a precise expression for the drag force:

$$
D' = \rho \delta \Delta U \left(U_\infty - \frac{3}{4}\Delta U\right)
$$

This result powerfully demonstrates that a macroscopic force like drag can be determined entirely by measuring the fluid's momentum flux in the [far-field](@entry_id:269288), without needing to know the complex details of the pressure and [shear stress distribution](@entry_id:197453) on the body's surface.

### Extensions of the Momentum Flux Concept

The classical definition of momentum flux, dominated by the inertial term $\rho u^2$, can be extended to more complex flow scenarios.

#### Compressible Flow and Shock Waves

In high-speed [compressible flows](@entry_id:747589), sharp discontinuities known as **shock waves** can form. Across a [normal shock wave](@entry_id:268490), the fluid properties (pressure, density, velocity, temperature) change almost instantaneously. Despite this abrupt change, the fundamental conservation laws must hold. In a frame of reference moving with the shock, the [integral momentum equation](@entry_id:272259) applied across the shock reveals that a specific combination of pressure and momentum flux is conserved. This quantity, often denoted as the [momentum flux](@entry_id:199796) parameter $I$, is:

$$
I = p + \rho u^2
$$

Thus, for a flow transitioning from a pre-shock state (1) to a post-shock state (2), the [momentum conservation](@entry_id:149964) law is succinctly expressed as $p_1 + \rho_1 u_1^2 = p_2 + \rho_2 u_2^2$ [@problem_id:496626]. This invariant is a cornerstone of [gas dynamics](@entry_id:147692), allowing for the algebraic calculation of post-shock conditions from pre-shock conditions.

#### Viscoelastic Flows and Elastic Thrust

In Newtonian fluids, the stress tensor is related linearly to the [rate of strain](@entry_id:267998). However, many materials, such as polymer melts and solutions, are **viscoelastic** and exhibit both viscous and elastic characteristics. When these fluids are sheared, they can develop **[normal stress differences](@entry_id:191914)** in addition to shear stresses. These normal stresses can generate forces perpendicular to the direction of shear.

A fascinating consequence of this behavior is the phenomenon of **elastic thrust** [@problem_id:496541]. When a viscoelastic fluid is extruded from a pipe, the total thrust exerted by the jet is not just the conventional [momentum flux](@entry_id:199796), $\int \rho v_z^2 dA$. The elastic stresses stored in the fluid as it flows through the pipe are released at the exit, contributing an additional [thrust](@entry_id:177890). The elastic thrust, $T_E$, is due to the integral of the axial normal stress over the exit plane.

For a fully developed [pipe flow](@entry_id:189531), it can be shown that this elastic [thrust](@entry_id:177890) is directly related to the first [normal stress difference](@entry_id:199507), $N_1 = \tau_{zz} - \tau_{rr}$, where $\tau_{zz}$ and $\tau_{rr}$ are the axial and radial deviatoric [normal stresses](@entry_id:260622). Under the simplifying Weissenberg hypothesis (which posits that the second [normal stress difference](@entry_id:199507), $N_2 = \tau_{rr} - \tau_{\theta\theta}$, is zero), the elastic thrust simplifies to the integral of $N_1$ over the exit area. If $N_1$ follows a power-law profile $N_1(r) = N_{1w} (r/R)^k$, where $N_{1w}$ is the wall value, the total elastic thrust can be calculated as:

$$
T_E = \int_0^R N_1(r) \, 2\pi r \, dr = \frac{2\pi N_{1w}R^2}{k+2}
$$

This result highlights that in complex fluids, the momentum flux concept must be expanded to include contributions from elastic stresses, which can generate significant forces.

### Energy Flux, Dissipation, and Irreversibility

While total energy (including thermal energy) is always conserved, **mechanical energy** is only conserved in the idealized case of [inviscid flow](@entry_id:273124). In any real fluid flow with viscosity, and in flows with abrupt changes like jumps or shocks, mechanical energy is irreversibly converted into thermal energy, a process known as **dissipation**.

#### Macroscopic Dissipation in Discontinuous Flows

A dramatic example of macroscopic [energy dissipation](@entry_id:147406) occurs in a **hydraulic jump** in an [open channel flow](@entry_id:272098) [@problem_id:496532]. This phenomenon involves a rapid transition from a high-velocity, shallow (supercritical) flow to a low-velocity, deep (subcritical) flow. Across the jump, mass and momentum are conserved, but the intense turbulence and mixing within the jump cause a significant loss of [mechanical energy](@entry_id:162989).

The [specific energy](@entry_id:271007) of the flow, a measure of mechanical energy per unit weight, is defined as $E = h + v^2/(2g)$. The energy loss across the jump is $\Delta E = E_1 - E_2$. By combining the mass and [momentum conservation](@entry_id:149964) equations, one can derive a relationship for this energy loss. A more insightful quantity is the fractional energy loss, $\eta_{loss} = (E_1 - E_2)/E_1$, which can be expressed solely in terms of the upstream Froude number, $Fr_1 = v_1/\sqrt{gh_1}$:

$$
\eta_{loss} = \frac{\left(\sqrt{1+8Fr_1^2}-3\right)^3}{8\left(\sqrt{1+8Fr_1^2}-1\right)\left(2+Fr_1^2\right)}
$$

This expression quantifies the jump's inefficiency, showing that a stronger jump (larger $Fr_1$) leads to a greater fractional loss of [mechanical energy](@entry_id:162989). A similar loss of [mechanical energy](@entry_id:162989) occurs across a gas dynamic shock wave, where the work done by pressure forces across the shock compresses and heats the gas [@problem_id:496626].

#### The Microscopic Origin of Dissipation

The macroscopic energy loss observed in real flows has its origin at the microscopic level in the action of viscosity. Viscosity creates internal friction as layers of fluid slide past one another. The rate at which mechanical energy is converted into internal energy (heat) per unit volume is given by the **[viscous dissipation](@entry_id:143708) function**, $\Phi$. For an incompressible Newtonian fluid with [dynamic viscosity](@entry_id:268228) $\mu$, this function is given by the full contraction of the viscous stress tensor with the [velocity gradient tensor](@entry_id:270928):

$$
\Phi = 2\mu \mathbf{S}:\mathbf{S} = 2\mu S_{ij}S_{ij}
$$

where $\mathbf{S}$ is the symmetric [rate-of-strain tensor](@entry_id:260652), $S_{ij} = \frac{1}{2}(\frac{\partial v_i}{\partial x_j} + \frac{\partial v_j}{\partial x_i})$. Since $\mathbf{S}:\mathbf{S}$ is a sum of squares, $\Phi$ is always non-negative, confirming that viscosity is always a dissipative process.

To make this concept concrete, consider a two-dimensional spiral [vortex flow](@entry_id:271366) with velocity field $\vec{v} = (-\frac{q}{2\pi r}) \hat{e}_r + (\frac{\Gamma}{2\pi r}) \hat{e}_\theta$ [@problem_id:496635]. By calculating the components of the [rate-of-strain tensor](@entry_id:260652) in [cylindrical coordinates](@entry_id:271645), one finds the dissipation function for this flow to be:

$$
\Phi(r) = \frac{\mu(q^2+\Gamma^2)}{\pi^2r^4}
$$

The total rate of [energy dissipation](@entry_id:147406) in an annular region between radii $r_1$ and $r_2$ is found by integrating $\Phi$ over the volume. The result, $\dot{E}_{diss} = \frac{\mu(q^2+\Gamma^2)}{\pi}(\frac{1}{r_1^2}-\frac{1}{r_2^2})$, explicitly connects the rate of energy loss to the [fluid viscosity](@entry_id:261198) $\mu$ and the kinematic parameters of the flow ($q$, $\Gamma$).

### The Energetics of Turbulent Flows

Turbulence is characterized by chaotic, fluctuating velocity and pressure fields. To analyze such flows, we employ Reynolds decomposition, splitting the instantaneous velocity $u_i$ into a mean component $\overline{u_i}$ and a fluctuating component $u'_i$. This decomposition, when applied to the Navier-Stokes equations, reveals a rich interplay of energy and momentum fluxes between the mean flow and the turbulent fluctuations.

#### Reynolds Stresses as Turbulent Momentum Flux

Averaging the Navier-Stokes equations gives rise to the Reynolds-Averaged Navier-Stokes (RANS) equations. The non-[linear advection](@entry_id:636928) term $u_j \frac{\partial u_i}{\partial x_j}$ generates a new term, $-\rho\overline{u'_i u'_j}$, known as the **Reynolds stress tensor**. This tensor acts as an additional stress on the mean flow, representing the transport of mean momentum by the turbulent fluctuations. For example, the term $-\rho\overline{u'v'}$ in a [shear flow](@entry_id:266817) represents a turbulent flux of $x$-momentum in the $y$-direction.

In a fully developed [turbulent channel flow](@entry_id:756232) driven by a mean pressure gradient $\frac{d\overline{P}}{dx}$, the mean momentum equation simplifies dramatically. Integrating this equation with respect to the wall-normal coordinate $y$ reveals an exact and remarkably simple result for the total shear stress profile [@problem_id:496540]:

$$
\tau_{total}(y) = \mu \frac{d\overline{u}}{dy} - \rho\overline{u'v'} = \left(\frac{d\overline{P}}{dx}\right)y
$$

This linear stress profile shows that the sum of the [viscous stress](@entry_id:261328) (molecular momentum flux) and the Reynolds stress (turbulent momentum flux) must balance the [pressure gradient force](@entry_id:262279) at every point in the flow. Near the walls, [viscous stress](@entry_id:261328) dominates, while in the core of the flow, the Reynolds stress is the primary mechanism for transporting momentum.

#### The Energy Cascade

A central concept in turbulence is the **[energy cascade](@entry_id:153717)**, which describes the flow of energy from the large scales of the mean motion down to the smallest scales where it is dissipated by viscosity. This cascade can be understood by examining the energy budgets for the mean flow and the turbulent fluctuations separately.

1.  **Mean-Flow Kinetic Energy Budget:**
    One can derive a [transport equation](@entry_id:174281) for the kinetic energy of the mean flow, $K = \frac{1}{2}\overline{u_i}\overline{u_i}$ [@problem_id:496622]. This equation takes the form:
    $$
    \frac{D K}{D t} = \text{Transport Terms} - \varepsilon_K - \mathcal{P}_K
    $$
    Here, $DK/Dt$ is the material derivative of the mean kinetic energy, the transport terms describe the spatial redistribution of $K$ by pressure and stresses, and $\varepsilon_K = \nu (\partial_j \overline{u_i})(\partial_j \overline{u_i})$ is the direct [viscous dissipation](@entry_id:143708) of mean-flow energy. The most crucial term is $\mathcal{P}_K = -\overline{u'_i u'_j} \frac{\partial \overline{u_i}}{\partial x_j}$, which represents the rate of [energy transfer](@entry_id:174809) from the mean flow to the turbulent fluctuations. This term is almost always positive in shear flows, acting as a sink of energy for the mean flow. It quantifies the rate at which the mean flow does work against the Reynolds stresses, thereby feeding energy into the turbulence. For a channel flow with a given [velocity profile](@entry_id:266404) and Reynolds stress model, the total power transferred to turbulence can be calculated by integrating $\rho \mathcal{P}_K$ over the channel volume [@problem_id:496622].

2.  **Turbulent Kinetic Energy Budget:**
    Similarly, a [transport equation](@entry_id:174281) can be derived for the turbulent kinetic energy (TKE) per unit mass, $k = \frac{1}{2}\overline{u'_i u'_i}$ [@problem_id:496566]. Its general form is:
    $$
    \frac{D k}{D t} = P - \epsilon + \text{Transport Terms}
    $$
    The key terms are the production rate $P$ and the dissipation rate $\epsilon$.
    -   The **production term** is $P = -\overline{u'_i u'_j} \frac{\partial \overline{u_i}}{\partial x_j}$. This is precisely the same as $\mathcal{P}_K$. The energy drained from the mean flow acts as the source, or production, of [turbulent kinetic energy](@entry_id:262712).
    -   The **[dissipation rate](@entry_id:748577)**, $\epsilon = \nu \overline{\frac{\partial u'_i}{\partial x_j} \frac{\partial u'_i}{\partial x_j}}$, represents the rate at which TKE is converted into internal energy by viscous action. This occurs predominantly at the smallest scales of motion where velocity gradients are largest.

    For the idealized case of homogeneous [shear flow](@entry_id:266817), where all statistical quantities are spatially uniform, the transport terms vanish. The TKE budget simplifies to a direct balance between production and dissipation: $\frac{dk}{dt} = P - \epsilon = -S\overline{u'_1 u'_2} - \epsilon$, where $S$ is the constant mean shear rate [@problem_id:496566].

In summary, the [energy cascade in turbulence](@entry_id:186829) is a story told by fluxes. Energy is supplied to the large-scale mean flow. The mean flow transfers this energy to the largest [turbulent eddies](@entry_id:266898) via the production mechanism, which is a correlation between the Reynolds stress (a turbulent [momentum flux](@entry_id:199796)) and the mean [velocity gradient](@entry_id:261686). This energy then cascades through eddies of decreasing size without significant loss, until it reaches the smallest, Kolmogorov-scale eddies, where it is finally dissipated into heat by viscosity. This continuous flux of energy from large to small scales is the defining characteristic of turbulent [fluid motion](@entry_id:182721).