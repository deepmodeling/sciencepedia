## Introduction
As wind energy becomes a cornerstone of global power generation, maximizing the efficiency and reliability of wind farms is paramount. A central challenge in this endeavor is understanding and mitigating wind turbine [wake effects](@entry_id:1133931)—the regions of slower, more turbulent airflow that form behind operating turbines. These wakes reduce the power production of downstream turbines and increase their structural fatigue, making accurate modeling essential for the technical and financial success of any wind energy project. This article addresses the need for a systematic understanding of wake phenomena, from first principles to practical application, bridging the gap between fundamental fluid dynamics and the engineering tools used daily in the wind industry.

The reader will embark on a structured journey through this complex topic. The "Principles and Mechanisms" chapter will lay the theoretical groundwork, starting with the idealized [actuator disk model](@entry_id:1120757) to explain *why* wakes form, progressing to analytical models like the Jensen and Gaussian frameworks that describe *how* they evolve, and incorporating the profound influence of the atmospheric environment. Next, the "Applications and Interdisciplinary Connections" chapter will demonstrate how this knowledge is applied in the real world, from optimizing wind farm layouts and predicting energy yield to ensuring structural integrity and implementing advanced, farm-level control strategies like wake steering. Finally, the "Hands-On Practices" section will offer concrete exercises to translate theory into practical skills, reinforcing the core concepts of wake modeling, analysis, and control.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms that govern the formation, evolution, and interaction of wind turbine wakes. We will begin by establishing the foundational physics of a single turbine wake using idealized models, then progress to more sophisticated analytical descriptions, incorporate the critical influence of the atmospheric environment, and finally, address the complexities of modeling wake interactions within a full wind farm.

### The Physics of an Idealized Wind Turbine Wake

To understand the complex fluid dynamics of a wind farm, we first simplify the problem to that of a single, isolated turbine operating in a uniform flow. This allows us to derive the core physical principles that form the basis of all wake modeling.

#### The Actuator Disk Model: A Momentum Sink

The most fundamental idealization of a wind turbine in fluid dynamics is the **[actuator disk theory](@entry_id:181421)**. In this model, the complex, rotating blades of the turbine are replaced by a simple, permeable disk of area $A$. This disk is conceptualized as an energy-extracting device that exerts a uniform [thrust](@entry_id:177890) force on the fluid passing through it. To make the problem analytically tractable, several key assumptions are made about the flow: it is considered **steady**, **incompressible**, and **inviscid**, and the analysis is simplified to be **one-dimensional** along the axis of the [streamtube](@entry_id:182650) that contains the flow passing through the disk .

The actuator disk acts as a **momentum sink**. As the uniform upstream flow with velocity $U_{\infty}$ approaches the disk, it decelerates. A crucial insight from the model is that the velocity field, $u$, must be continuous as it passes through the infinitesimally thin disk to conserve mass. However, the [static pressure](@entry_id:275419), $p$, is discontinuous. A finite pressure drop occurs across the disk, which is the source of the [thrust](@entry_id:177890) force, $T$, exerted on the disk. Mathematically, $T = A \cdot (p_{d^-} - p_{d^+})$, where $p_{d^-}$ and $p_{d^+}$ are the pressures immediately upstream and downstream of the disk, respectively.

Because the flow is assumed to be inviscid, Bernoulli's equation holds along [streamlines](@entry_id:266815) upstream and downstream of the disk, but not across the disk itself, where energy is extracted. This energy extraction manifests as a decrease in the [stagnation pressure](@entry_id:265293) ($p_0 = p + \frac{1}{2}\rho u^2$) across the disk. Furthermore, as the turbine extracts kinetic energy from the flow, the wind speed continues to decrease into the far wake. To satisfy the principle of mass conservation for an incompressible fluid ($\dot{m} = \rho A u = \text{constant}$), the [streamtube](@entry_id:182650) must expand downstream of the turbine. This wake expansion is a hallmark of energy-extracting devices. The [thrust](@entry_id:177890) can also be expressed as the total rate of momentum change in the fluid between the far upstream and far downstream planes, $T = \dot{m}(U_{\infty} - u_w)$, where $u_w$ is the final wake velocity  .

#### Quantifying Turbine Performance and Wake Strength: $C_T$ and $C_p$

To generalize the performance of a turbine beyond specific flow conditions, we use dimensionless coefficients. The two most important are the **[thrust](@entry_id:177890) coefficient ($C_T$)** and the **power coefficient ($C_p$)**. They are defined by normalizing the [thrust](@entry_id:177890) force and extracted power by quantities representative of the incoming wind's momentum and energy fluxes, respectively :

$$
C_T = \frac{T}{\frac{1}{2}\rho A U_{\infty}^2}
$$

$$
C_p = \frac{P}{\frac{1}{2}\rho A U_{\infty}^3}
$$

Here, $T$ is the [thrust](@entry_id:177890), $P$ is the power extracted, $\rho$ is the air density, $A$ is the rotor swept area, and $U_{\infty}$ is the free-stream wind speed. The term $\frac{1}{2}\rho A U_{\infty}^2$ represents a characteristic force scale of the inflow, while $\frac{1}{2}\rho A U_{\infty}^3$ is the total kinetic power available in the wind passing through area $A$.

Within the framework of [actuator disk theory](@entry_id:181421), these coefficients can be expressed in terms of a single parameter: the **axial induction factor**, $a$. This factor quantifies the fractional velocity reduction at the disk itself: $a = (U_{\infty} - U_d)/U_{\infty}$, where $U_d$ is the velocity at the disk. A fundamental result of the theory is that the velocity in the far wake is $U_w = U_{\infty}(1-2a)$. Using these relationships, the coefficients can be derived as:

$$
C_T = 4a(1-a)
$$

$$
C_p = 4a(1-a)^2
$$

It is of paramount importance for wake modeling to recognize the distinct roles of these two coefficients. The power coefficient, $C_p$, measures the turbine's aerodynamic efficiency in converting wind power to [mechanical power](@entry_id:163535). The thrust coefficient, $C_T$, quantifies the magnitude of the momentum extracted from the flow. Since the wake is fundamentally a region of momentum deficit, **it is the [thrust](@entry_id:177890) coefficient, $C_T$, that directly governs the strength and initial velocity deficit of the wake**. Analytical wake models therefore use $C_T$ as a primary input to characterize the wake-generating turbine, not $C_p$ .

#### A General Definition: The Wake as a Momentum Deficit Region

Moving beyond the simplified 1D [actuator disk model](@entry_id:1120757), we can define a wind turbine wake in more general, physical terms based on the fundamental conservation laws of fluid motion. A wake is fundamentally a downstream region characterized by a **momentum deficit** relative to the undisturbed flow. This means the mean streamwise velocity, $u_x$, within the wake is lower than the free-stream velocity, $U_{\infty}$ .

This definition can be formalized by applying the integral form of the [conservation of linear momentum](@entry_id:165717) to a control volume enclosing the turbine. The Reynolds [transport theorem](@entry_id:176504) for a [steady flow](@entry_id:264570) states that the sum of all forces acting on the fluid within the control volume equals the net flux of momentum out of the control volume. For the streamwise direction, this balance is:

$$
- T + \int_{\mathcal{S}} (- p \mathbf{n} + \boldsymbol{\tau}\cdot\mathbf{n})\cdot \mathbf{e}_x \, \mathrm{d}A = \int_{\mathcal{S}} \rho u_x (\mathbf{u} \cdot \mathbf{n}) \, \mathrm{d}A
$$

Here, $T$ is the [thrust](@entry_id:177890) force from the turbine on the fluid (a negative value), the [first integral](@entry_id:274642) represents the net force from pressure ($p$) and viscous stresses ($\boldsymbol{\tau}$) on the control surface $\mathcal{S}$, and the second integral is the net flux of streamwise momentum ($u_x$) out of the control volume. This equation forms the basis for all wake analysis, explicitly linking the force exerted by the turbine to the resulting momentum deficit in the flow field .

### Analytical Models of Wake Structure and Recovery

While the [actuator disk model](@entry_id:1120757) explains *why* a wake forms, practical engineering requires analytical models that describe the wake's structure and how it recovers with downstream distance.

#### The Mechanism of Wake Recovery: Advection and Turbulent Diffusion

A wake does not persist indefinitely. The [velocity deficit](@entry_id:269642) recovers to the free-stream velocity due to **turbulent mixing**. The shear layer between the low-speed wake and the high-speed ambient flow is inherently unstable, generating turbulence that entrains higher-momentum fluid into the wake.

In the far-wake region, this recovery process can be modeled as a **[convective-diffusion](@entry_id:1123020) process** . The [velocity deficit](@entry_id:269642), $\delta U$, is advected downstream by the mean flow and simultaneously spreads (diffuses) in the lateral and vertical directions due to turbulent transport. By simplifying the Reynolds-Averaged Navier-Stokes (RANS) equations with slender wake approximations and using an eddy viscosity closure ($\nu_t$) to model the turbulent stresses, we can derive a [parabolic partial differential equation](@entry_id:272879) for an [axisymmetric wake](@entry_id:204811) deficit $\delta U(x,r)$:

$$
U_\infty \frac{\partial \delta U}{\partial x} = \nu_t \left( \frac{\partial^2 \delta U}{\partial r^2} + \frac{1}{r} \frac{\partial \delta U}{\partial r} \right)
$$

This equation is analogous to the heat equation, with downstream distance $x$ playing the role of time. The solutions to this equation are "self-similar," meaning the shape of the deficit profile remains the same while its width and depth change with distance. A key finding is that the wake width squared ($\sigma^2$) grows linearly with $x$, and to conserve the total momentum deficit, the centerline [velocity deficit](@entry_id:269642) ($\delta U_c$) must decay as $x^{-1}$ . This provides a strong theoretical basis for the functional forms used in many wake models.

#### Kinematic Models I: The Jensen Top-Hat Model

The earliest and simplest analytical wake model is the **Jensen model** (or Park model). It is a kinematic model that makes two strong simplifying assumptions based on empirical observations :

1.  The wake expands linearly with downstream distance $x$. The wake radius is given by $R(x) = R_0 + kx$, where $R_0$ is the initial wake radius (often taken as the rotor radius, $D/2$) and $k$ is the **wake expansion coefficient**.
2.  The velocity within the wake is uniform (a "top-hat" profile) at any given distance $x$. Outside the wake, the velocity is the undisturbed free-stream velocity $U_\infty$.

By applying conservation of momentum between the turbine disk and a downstream plane, we can derive the velocity $U(x)$ inside the wake. The result is a simple expression for the [velocity deficit](@entry_id:269642), which shows that the deficit decreases as the inverse square of the wake radius:

$$
\frac{U(x)}{U_\infty} = 1 - \frac{1 - \sqrt{1 - C_T}}{\left(1 + \frac{2kx}{D}\right)^2}
$$

Despite its simplicity, the Jensen model is widely used for its [computational efficiency](@entry_id:270255), particularly in initial [wind farm layout optimization](@entry_id:1134090) studies.

#### Kinematic Models II: The Gaussian Wake Model

Experimental measurements show that the "top-hat" velocity profile is unrealistic. The actual [velocity deficit](@entry_id:269642) profile is smooth and is well-approximated by a **Gaussian function**. This observation, consistent with the [self-similar solutions](@entry_id:164839) to the advection-diffusion equation, forms the basis of Gaussian wake models .

In this framework, the [velocity deficit](@entry_id:269642) $\Delta U$ at a downstream location $(x,y,z)$ is given by:

$$
\Delta U(x,y,z) = \Delta U_c(x) \exp\left(-\frac{1}{2}\left(\frac{y^2}{\sigma_y^2(x)} + \frac{(z-z_h)^2}{\sigma_z^2(x)}\right)\right)
$$

where $\Delta U_c(x)$ is the centerline deficit at hub height $z_h$, and $\sigma_y(x)$ and $\sigma_z(x)$ are the wake standard deviations (widths) in the lateral and vertical directions, which grow with distance $x$.

To close the model, the centerline deficit $\Delta U_c(x)$ must be related to the turbine's thrust. Applying the integral momentum conservation principle (without making small-deficit approximations) yields a relationship between $C_T$, the wake widths, and the centerline deficit. For a circular Gaussian wake ($\sigma_y=\sigma_z=\sigma$), the relationship is:

$$
\Delta U_{c}(x)=U_{\infty}\left(1-\sqrt{1-\frac{C_{T}}{8 (\sigma(x)/D)^{2}}}\right)
$$

This formulation ensures that the model is physically consistent by conserving momentum. Gaussian models offer a significant improvement in accuracy over the Jensen model and are a cornerstone of modern wind farm simulation tools.

### The Influence of the Atmospheric Environment

So far, our discussion has assumed a simplified, uniform background flow. In reality, a wind turbine operates within the complex, ever-changing atmospheric boundary layer. The characteristics of this layer profoundly impact wake behavior.

#### Characterizing Atmospheric Stability: The Monin-Obukhov Similarity Theory

The most critical atmospheric factor influencing wake recovery is **turbulent mixing**, which is largely governed by **[atmospheric stability](@entry_id:267207)**. In the [atmospheric surface layer](@entry_id:1121210) (the lowest ~100-200 meters), the interplay between turbulence generated by wind shear and turbulence generated or suppressed by buoyancy (due to surface heating or cooling) is described by **Monin-Obukhov Similarity Theory (MOST)** .

MOST introduces two key scaling parameters:
1.  The **[friction velocity](@entry_id:267882) ($u_*$)**: $u_* = \sqrt{\tau_0/\rho}$, where $\tau_0$ is the surface shear stress. It is a velocity scale representing shear-generated turbulence.
2.  The **Monin-Obukhov length ($L$)**: $L = -\dfrac{u_*^3}{\kappa g \left(\overline{w'\theta_v'}/\theta_v\right)}$, where the term in the denominator represents the [buoyancy flux](@entry_id:261821) due to the surface [virtual potential temperature](@entry_id:1133825) flux $\overline{w'\theta_v'}$. $L$ is the height at which buoyancy effects become as important as shear effects.

The sign of $L$ defines the stability regime, which is neatly captured by the dimensionless **stability parameter $\zeta = z/L$**, where $z$ is the height above the ground.

-   **Unstable Conditions**: Surface heating leads to an upward heat flux ($\overline{w'\theta_v'} > 0$), causing $L  0$ and $\zeta  0$. Buoyancy enhances vertical motions, generating turbulence. This leads to **low wind shear** and **high turbulence intensity**.
-   **Stable Conditions**: Surface cooling leads to a downward heat flux ($\overline{w'\theta_v'}  0$), causing $L > 0$ and $\zeta > 0$. The colder, denser air near the ground stratifies the atmosphere, suppressing vertical motions and damping turbulence. This leads to **high wind shear** and **low turbulence intensity**.
-   **Neutral Conditions**: No heat flux ($\overline{w'\theta_v'} \approx 0$), causing $|L| \to \infty$ and $\zeta \to 0$. Turbulence is produced only by mechanical shear.

These conditions have a direct and dramatic effect on wake recovery. The enhanced mixing in unstable conditions leads to **rapid wake recovery**, while the suppressed mixing in stable conditions leads to **slow wake recovery** and long, persistent wakes.

#### Incorporating Turbulence and Stability into Wake Models

To be effective, engineering wake models must account for these atmospheric effects. This is typically done by making the model parameters dependent on atmospheric conditions.

For the **Jensen model**, the wake expansion coefficient $k$ is not a universal constant. It is strongly correlated with the ambient **turbulence intensity** ($I = \sigma_u/\overline{U}$) at hub height. Higher turbulence intensity leads to more rapid entrainment and thus a larger value of $k$. This dependence can be calibrated from measurement data, often using a simple linear relationship of the form $k = \alpha I + \beta$ . For instance, analysis of LiDAR data might yield a best-fit model like $k = 0.323 I + 0.0137$, capturing the trend of increasing wake expansion with increasing turbulence.

For more advanced models like the **Gaussian model**, the link to the atmosphere can be made more physically direct using MOST . The wake spread rates are directly related to the eddy diffusivities ($K_y$, $K_z$). MOST prescribes how the eddy viscosity for momentum, $K_m$, varies with stability via a stability correction function, $\phi_m(\zeta)$. Specifically, $K_m(z) \sim \kappa u_* z / \phi_m(\zeta)$. In stable conditions ($\zeta > 0$), $\phi_m > 1$, which reduces $K_m$ and suppresses mixing. In unstable conditions ($\zeta  0$), $\phi_m  1$, which increases $K_m$ and enhances mixing. By assuming that the wake spread rates $k_y$ and $k_z$ are proportional to the eddy diffusivity, we can make them functions of the stability parameter $\zeta = z_h/L$. This allows the Gaussian model to predict faster wake spreading in unstable conditions and slower spreading in stable conditions, in line with physical reality. Because buoyancy acts most directly on vertical motion, the stability correction is typically stronger for the vertical spread rate, $k_z(\zeta)$, than for the lateral one, $k_y(\zeta)$ .

### Modeling Wake Interactions in Wind Farms

A wind farm is a collective system where the wakes of upstream turbines interact with each other and with downstream turbines. A critical challenge is to determine the effective wind speed at a downstream turbine that is impacted by one or more wakes. This is the problem of **wake superposition**.

#### The Challenge of Wake Superposition

Simple analytical models describe a single wake in an undisturbed flow. When multiple wakes overlap, their combined effect is not a simple sum due to the non-linear nature of fluid dynamics. Various **superposition models** have been proposed to approximate this interaction, balancing physical fidelity with computational cost.

#### Methods of Wake Superposition

Let's consider a point in space that is affected by the wakes of two upstream turbines. If turbine 1 alone would produce a local velocity $u_1$ and turbine 2 alone would produce $u_2$ (from a free-stream $U_\infty$), what is the combined velocity $u$? Three common hypotheses are :

1.  **Linear Velocity Superposition**: This model assumes that the velocity deficits, $\Delta U = U_\infty - u$, add linearly.
    $$ \Delta U_{total} = \sum_i \Delta U_i \implies (U_\infty - u) = (U_\infty - u_1) + (U_\infty - u_2) $$
    This is the simplest approach and is a reasonable [first-order approximation](@entry_id:147559) when deficits are small. For a scenario with $U_\infty = 10 \text{ m/s}$, $u_1=8 \text{ m/s}$, and $u_2=9 \text{ m/s}$, the individual deficits are $2 \text{ m/s}$ and $1 \text{ m/s}$. The combined deficit is $3 \text{ m/s}$, yielding a local velocity of $u = 7 \text{ m/s}$.

2.  **Energy (or Squared Deficit) Superposition**: This heuristic model assumes that a quantity related to the kinetic energy of the turbulence, which can be taken as proportional to the square of the [velocity deficit](@entry_id:269642), is what adds linearly.
    $$ (\Delta U_{total})^2 = \sum_i (\Delta U_i)^2 \implies (U_\infty - u)^2 = (U_\infty - u_1)^2 + (U_\infty - u_2)^2 $$
    In our example, $(10-u)^2 = 2^2 + 1^2 = 5$, which gives $u = 10 - \sqrt{5} \approx 7.76 \text{ m/s}$. This method tends to predict smaller combined deficits than the linear model.

3.  **Momentum-Consistent Superposition**: This approach is based on the local momentum deficit flux density, $u(U_\infty - u)$, a key term in the momentum equation. It postulates that this quantity is additive.
    $$ u(U_\infty - u) = \sum_i u_i(U_\infty - u_i) $$
    For our example, $u(10-u) = 8(10-8) + 9(10-9) = 16 + 9 = 25$. This gives the quadratic equation $u^2 - 10u + 25 = 0$, which has the solution $u = 5 \text{ m/s}$. This method is more physically grounded but can predict very large deficits.

The choice of superposition model has a significant impact on predicted power production, and none of them perfectly represents the underlying physics. However, they provide essential tools for engineering analysis.

#### A Momentum-Consistent Approach to Partial Waking

The problem is further complicated when wakes only **partially cover** a downstream rotor. A naive application of superposition, such as calculating a local deficit at the rotor center and applying it uniformly, can violate the conservation of momentum. A more rigorous method is required .

The total momentum flux deficit at the downstream rotor plane should be the sum of the [momentum flux](@entry_id:199796) deficits from each impinging wake. Under a small-deficit approximation, the integrated momentum flux deficit from a wake $i$ with deficit $\Delta U_i$ covering an area $A_i$ on the rotor is proportional to $\Delta U_i A_i$. To find a momentum-consistent rotor-averaged deficit, $\overline{\Delta U}_{corr}$, we must conserve this total momentum flux:

$$
\overline{\Delta U}_{corr} \cdot A_r = \sum_i (\Delta U_i \cdot A_i)
$$

This leads to a corrected rotor-mean deficit that is an **area-weighted average of the individual deficits**:

$$
\overline{\Delta U}_{corr} = \frac{\sum_i \Delta U_i A_i}{A_r} = \sum_i \Delta U_i f_i
$$

where $f_i = A_i/A_r$ is the fraction of the rotor area covered by wake $i$. This approach correctly accounts for the fact that each wake deficit only acts on the portion of the rotor it physically covers, thus providing a momentum-conserving estimate of the effective inflow for the downstream turbine . This method avoids the over-prediction of deficit that occurs when summing local deficits and applying them over the entire rotor, providing a more robust basis for wind farm power assessment.