## Introduction
In the study of fluid mechanics, the interaction between a moving fluid and a solid surface gives rise to one of its most fundamental concepts: the boundary layer. Due to viscosity, [fluid velocity](@entry_id:267320) at the surface is zero and increases to the freestream value over a short distance. This velocity reduction, or deficit, means that the mass flowing through the boundary layer is less than what an ideal, frictionless model would predict. This discrepancy poses a significant challenge, limiting the accuracy of inviscid theories in real-world engineering applications. The concept of **displacement thickness** provides the crucial bridge between these idealized models and viscous reality.

This article offers a detailed exploration of displacement thickness, a parameter that quantifies the "blocking" effect of the boundary layer. By understanding and calculating this quantity, we can make powerful first-order corrections to predict the behavior of real flows with remarkable accuracy. Across the following sections, you will gain a robust understanding of this vital concept.

-   The first section, **Principles and Mechanisms**, will establish the formal definition of displacement thickness from the principle of [mass flow deficit](@entry_id:276648). You will learn how to calculate it for various velocity profiles and interpret its physical significance, including its relationship to the "fullness" of a profile.

-   Next, **Applications and Interdisciplinary Connections** will demonstrate the practical utility of displacement thickness. We will see how it is used to define an "effective body" in aerodynamics, correct [lift and drag](@entry_id:264560) predictions, design wind tunnels and high-speed nozzles, and how it connects to advanced topics like [viscous-inviscid interaction](@entry_id:273025).

-   Finally, **Hands-On Practices** will provide a series of guided problems. These exercises will allow you to apply the integral formulas and solidify your understanding by calculating displacement thickness for common [laminar and turbulent flow](@entry_id:261113) models.

## Principles and Mechanisms

The presence of a solid boundary in a fluid flow fundamentally alters the velocity field in its vicinity. Due to the [no-slip condition](@entry_id:275670), fluid velocity is zero at the surface and gradually increases to the freestream velocity, $U_\infty$, across a thin region known as the boundary layer. This [velocity gradient](@entry_id:261686), a direct consequence of viscosity, means that the mass flow rate within the boundary layer is less than what it would be if the flow were inviscid and uniform. The concept of **displacement thickness** provides a rigorous way to quantify this deficit in mass flow and its effect on the surrounding flow field.

### The Concept of Mass Flow Deficit

Imagine a steady, incompressible, [two-dimensional flow](@entry_id:266853) over a flat plate. Far from the plate, the velocity is a uniform $U_\infty$. Within the boundary layer of thickness $\delta$, the velocity profile $u(y)$ describes the retardation of the flow, where $y$ is the coordinate normal to the surface.

The reduction in velocity within this layer leads to a **[mass flow rate](@entry_id:264194) deficit**. To quantify this, let us compare the actual [mass flow rate](@entry_id:264194) per unit width, $\dot{m}_{\text{actual}}$, to that of a hypothetical ideal (inviscid) flow, $\dot{m}_{\text{ideal}}$, occupying the same height $H$ (where $H > \delta$).

The actual [mass flow rate](@entry_id:264194) is given by the integral of the mass flux $\rho u(y)$ over the cross-section:
$$
\dot{m}_{\text{actual}} = \int_{0}^{H} \rho u(y) \,dy
$$

For the [ideal flow](@entry_id:261917), the velocity would be $U_\infty$ everywhere, so the mass flow rate would be:
$$
\dot{m}_{\text{ideal}} = \int_{0}^{H} \rho U_\infty \,dy = \rho U_\infty H
$$

The total deficit in mass flow rate is the difference between these two quantities:
$$
\text{Mass Flow Deficit} = \dot{m}_{\text{ideal}} - \dot{m}_{\text{actual}} = \int_{0}^{H} \rho U_\infty \,dy - \int_{0}^{H} \rho u(y) \,dy = \rho \int_{0}^{H} (U_\infty - u(y)) \,dy
$$

The **displacement thickness**, denoted by the symbol $\delta^*$, is defined as the distance by which the solid boundary would have to be displaced outwards (into the flow) to produce an equivalent [mass flow deficit](@entry_id:276648) in an [ideal flow](@entry_id:261917). If we imagine a layer of fluid of thickness $\delta^*$ being brought to a complete stop (i.e., its mass flow rate reduced to zero), the [mass flow deficit](@entry_id:276648) would be $\rho U_\infty \delta^*$. Equating this to the actual deficit gives the formal definition:
$$
\rho U_\infty \delta^* = \rho \int_{0}^{\infty} (U_\infty - u(y)) \,dy
$$
Note that the upper limit of integration has been extended to infinity for generality, which is permissible because the integrand $(U_\infty - u(y))$ becomes zero for $y > \delta$. Dividing by $\rho U_\infty$ yields the standard integral definition for the displacement thickness:
$$
\delta^* = \int_{0}^{\infty} \left(1 - \frac{u(y)}{U_\infty}\right) \,dy
$$

This equation reveals a critical insight: the displacement thickness is the integral of the dimensionless [velocity deficit](@entry_id:269642) over the entire boundary layer. It is not a physical length that can be measured with a ruler at a specific coordinate $y=h$. Instead, it is an integrated quantity, an area on the plot of $(1 - u/U_\infty)$ versus $y$, which has units of length. It represents a theoretical thickness that quantifies the "blockage" effect of the boundary layer on the [external flow](@entry_id:274280) [@problem_id:1749717].

A powerful way to visualize this is to consider flow in a channel [@problem_id:1749659]. If [boundary layers](@entry_id:150517) of displacement thickness $\delta^*$ form on the top and bottom walls of a channel of height $H$, the central, inviscid core flow behaves as if it were flowing through a narrower, "effective" channel of height $H_{\text{eff}} = H - 2\delta^*$. The displacement thickness, therefore, defines the effective geometry that the outer, [inviscid flow](@entry_id:273124) "sees."

### Calculation from Velocity Profiles

The value of the displacement thickness is directly determined by the shape of the [velocity profile](@entry_id:266404) within the boundary layer. For a given [boundary layer thickness](@entry_id:269100) $\delta$, different profile shapes will yield different displacement thicknesses. Let us examine several common approximations for velocity profiles to see how $\delta^*$ is calculated.

#### Polynomial Approximations

Polynomials are frequently used to model boundary layer velocity profiles because they can be easily tailored to satisfy key physical boundary conditions.

Consider a [parabolic velocity profile](@entry_id:270592) that satisfies the [no-slip condition](@entry_id:275670) $u(0)=0$, matches the freestream at the edge $u(\delta)=U_\infty$, and has zero shear at the edge $\frac{du}{dy}|_{y=\delta}=0$. These conditions lead to the profile [@problem_id:1749664]:
$$
\frac{u(y)}{U_\infty} = 2\left(\frac{y}{\delta}\right) - \left(\frac{y}{\delta}\right)^2
$$
The displacement thickness for this profile is:
$$
\delta^* = \int_{0}^{\delta} \left(1 - \left[2\frac{y}{\delta} - \left(\frac{y}{\delta}\right)^2\right]\right) \,dy = \left[y - \frac{y^2}{\delta} + \frac{y^3}{3\delta^2}\right]_{0}^{\delta} = \delta - \delta + \frac{\delta}{3} = \frac{1}{3}\delta
$$

Now, consider a slightly different cubic profile that satisfies an additional constraint related to the pressure gradient, specifically $\frac{d^2u}{dy^2}|_{y=0}=0$ [@problem_id:1749702]. This leads to the profile:
$$
\frac{u(y)}{U_\infty} = \frac{3}{2}\left(\frac{y}{\delta}\right) - \frac{1}{2}\left(\frac{y}{\delta}\right)^3
$$
Calculating the displacement thickness for this profile gives:
$$
\delta^* = \int_{0}^{\delta} \left(1 - \left[\frac{3}{2}\frac{y}{\delta} - \frac{1}{2}\left(\frac{y}{\delta}\right)^3\right]\right) \,dy = \left[y - \frac{3y^2}{4\delta} + \frac{y^4}{8\delta^3}\right]_{0}^{\delta} = \delta - \frac{3\delta}{4} + \frac{\delta}{8} = \frac{3}{8}\delta
$$
This result, $\delta^* = 0.375\delta$, is slightly larger than the $\delta/3 \approx 0.333\delta$ from the parabolic profile, demonstrating how the specific shape of the [velocity profile](@entry_id:266404) directly influences the magnitude of the displacement effect.

#### Non-Polynomial Profiles

Velocity profiles are not limited to polynomials. For instance, a sinusoidal profile can also be used as a model [@problem_id:1740936] [@problem_id:1749720]:
$$
\frac{u(y)}{U_\infty} = \sin\left(\frac{\pi y}{2\delta}\right) \quad \text{for } 0 \le y \le \delta
$$
The corresponding displacement thickness is:
$$
\delta^* = \int_{0}^{\delta} \left(1 - \sin\left(\frac{\pi y}{2\delta}\right)\right) \,dy = \left[y + \frac{2\delta}{\pi}\cos\left(\frac{\pi y}{2\delta}\right)\right]_{0}^{\delta} = \left(\delta + 0\right) - \left(0 + \frac{2\delta}{\pi}\right) = \delta\left(1 - \frac{2}{\pi}\right)
$$
This gives $\delta^* \approx 0.363\delta$, a value intermediate to our two polynomial examples.

In some cases, the [boundary layer thickness](@entry_id:269100) $\delta$ is not sharply defined, and the velocity approaches $U_\infty$ asymptotically. The definition of $\delta^*$ remains robust. Consider a profile given by [@problem_id:1749697]:
$$
u(y) = U_\infty \tanh\left(\frac{y}{L}\right)
$$
where $L$ is a characteristic length scale. Here, we must integrate to infinity:
$$
\delta^* = \int_{0}^{\infty} \left(1 - \tanh\left(\frac{y}{L}\right)\right) \,dy
$$
Using the substitution $t = y/L$, this becomes:
$$
\delta^* = L \int_{0}^{\infty} (1 - \tanh t) \,dt = L \left[t - \ln(\cosh t)\right]_{0}^{\infty}
$$
Evaluating the limit at infinity, we find that $t - \ln(\cosh t) \to \ln 2$. At the lower limit, the expression is zero. Thus, the displacement thickness is finite:
$$
\delta^* = L \ln 2
$$
This demonstrates that $\delta^*$ is a well-defined and finite quantity that captures the integrated [velocity deficit](@entry_id:269642), even when the [boundary layer thickness](@entry_id:269100) itself is not a clearly bounded dimension.

### Physical Significance and Interpretation

The numerical value of $\delta^*$ carries significant physical meaning beyond its mathematical definition. It is a key parameter that links the viscous boundary layer to the behavior of the outer [inviscid flow](@entry_id:273124).

#### The "Fullness" of a Velocity Profile

The ratio $\delta^*/\delta$ is often used to characterize the boundary layer **shape**. This ratio depends on how "full" the velocity profile is. A fuller profile is one where the fluid accelerates to the freestream velocity more rapidly, meaning the velocity is higher, on average, throughout the boundary layer.

Let's compare a simple linear profile, $\frac{u}{U_\infty} = \frac{y}{\delta}$, with a "fuller" 1/7th power-law profile, $\frac{u}{U_\infty} = (\frac{y}{\delta})^{1/7}$, which is a common approximation for turbulent boundary layers [@problem_id:1749714].
For the linear profile, calculation yields $\delta^*_1 = \delta/2$.
For the fuller, power-law profile, the calculation is:
$$
\delta^*_2 = \int_{0}^{\delta} \left(1 - \left(\frac{y}{\delta}\right)^{1/7}\right) \,dy = \delta \left[ \frac{y}{\delta} - \frac{7}{8}\left(\frac{y}{\delta}\right)^{8/7} \right]_0^\delta = \delta \left(1 - \frac{7}{8}\right) = \frac{\delta}{8}
$$
The fuller profile results in a significantly smaller displacement thickness ($\delta/8$) compared to the linear profile ($\delta/2$). This makes intuitive sense: a fuller profile has a smaller [velocity deficit](@entry_id:269642), which implies a smaller [mass flow deficit](@entry_id:276648), and therefore a smaller displacement thickness. Turbulent boundary layers typically have much fuller profiles than laminar ones, and consequently, a smaller displacement thickness for the same overall [boundary layer thickness](@entry_id:269100) $\delta$.

#### Growth Along a Surface

The boundary layer does not have a constant thickness; it grows with increasing downstream distance $x$ from the leading edge of a body. For a [laminar flow](@entry_id:149458) over a flat plate, theory and experiment show that $\delta(x)$ is proportional to the square root of the distance, $\delta(x) \propto \sqrt{x}$.

Since the displacement thickness $\delta^*$ is directly proportional to $\delta$ (with the constant of proportionality depending on the profile shape), $\delta^*(x)$ must also grow with downstream distance [@problem_id:1749688]. For the cubic profile where $\delta^* = 3\delta/8$, if we know that $\delta(x) = C \sqrt{\frac{\nu x}{U_\infty}}$ for some constant $C$, then the displacement thickness grows as:
$$
\delta^*(x) = \frac{3}{8} \delta(x) = \frac{3C}{8} \sqrt{\frac{\nu x}{U_\infty}}
$$
This means that the effective shape of the body, as perceived by the outer flow, is not the flat plate itself, but a surface defined by $y = \delta^*(x)$. This thickening "effective body" displaces the outer [streamlines](@entry_id:266815) and can induce a pressure gradient, a crucial effect in aerodynamics and other applications.

#### The Case of Negative Displacement Thickness

The definition $\delta^* = \int (1 - u/U_\infty) dy$ is based on the assumption of a velocity *deficit* ($u \le U_\infty$). However, what if a flow has a velocity *overshoot*, where the velocity inside the boundary layer temporarily exceeds the freestream velocity ($u > U_\infty$)? Such profiles can occur, for instance, in the near-wake of a body or in flows with localized heating.

In regions where $u > U_\infty$, the integrand $(1 - u/U_\infty)$ becomes negative. If the integral of this negative portion outweighs the positive portion from regions of [velocity deficit](@entry_id:269642), the total displacement thickness can be negative [@problem_id:1749655]. For a hypothetical profile like $\frac{u(y)}{U} = 5(\frac{y}{\delta}) - 4(\frac{y}{\delta})^2$, which exhibits a significant velocity overshoot, the calculation yields:
$$
\delta^* = \int_{0}^{\delta} \left[1 - 5\left(\frac{y}{\delta}\right) + 4\left(\frac{y}{\delta}\right)^2\right] \,dy = \delta\left(1 - \frac{5}{2} + \frac{4}{3}\right) = -\frac{\delta}{6}
$$
A **negative displacement thickness** signifies a **mass flow surplus**. The boundary layer region is carrying more [mass flow](@entry_id:143424) than an equivalent region of the freestream. Physically, this means the outer flow [streamlines](@entry_id:266815) are displaced *towards* the wall, as if the wall itself were acting as a sink or had been thinned. This illustrates the robust and comprehensive nature of the displacement thickness concept, capable of describing both mass flow deficits and surpluses with a single, consistent definition.