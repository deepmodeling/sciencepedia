## Introduction
When mechanical components are pushed beyond their elastic limits, a new realm of behavior emerges, governed by the principles of plasticity. The plastic torsion of shafts is a classic and vital topic in [materials mechanics](@entry_id:189503), providing critical insights into how structures respond under extreme loading. Designing components to remain strictly within the elastic regime is often overly conservative and fails to exploit the full strength of ductile materials. This article addresses this gap by providing a comprehensive analysis of post-yield torsional behavior, offering a framework for more efficient and robust engineering design.

Over the next three chapters, you will build a deep understanding of this phenomenon. We will begin with the **Principles and Mechanisms** of plastic torsion, developing the theory from fundamental [kinematics](@entry_id:173318) to the analysis of elasto-plastic response, limit states, and residual stresses. Next, we will explore **Applications and Interdisciplinary Connections**, showing how these concepts are applied in [structural design](@entry_id:196229), advanced [materials modeling](@entry_id:751724), and coupled physical problems like [thermomechanics](@entry_id:180251). Finally, you will solidify your knowledge through **Hands-On Practices**, applying the theory to solve challenging engineering problems. Our exploration starts with the foundational mechanics that govern this complex process.

## Principles and Mechanisms

This chapter delineates the fundamental principles governing the plastic torsion of shafts. We will systematically develop the mechanics of this process, beginning with the [kinematics of deformation](@entry_id:189142), proceeding through the elastic and plastic constitutive responses, and culminating in an analysis of advanced topics such as limit states and residual stresses. Our focus will be on shafts with solid circular cross-sections, which, due to their [axial symmetry](@entry_id:173333), permit a clear and direct analytical treatment.

### Kinematics of Torsion in Circular Shafts

To understand the stresses that develop within a twisted shaft, we must first characterize its deformation. Consider a straight, circular, prismatic shaft of radius $R$ and length $L$. When subjected to a pure torque, we observe that the shaft twists about its longitudinal axis. Under the classical assumptions of Saint-Venant torsion, for a circular cross-section, a key kinematic simplification arises: plane [cross-sections](@entry_id:168295) perpendicular to the axis of the shaft remain plane and do not warp. They merely rotate as rigid disks relative to one another.

This absence of warping for a circular section is a direct consequence of its [axial symmetry](@entry_id:173333). Any out-of-plane displacement (warping) would have to be a function of the [angular position](@entry_id:174053), which would violate the physical symmetry of the problem where the geometry, material, and loading are all axisymmetric. Therefore, the displacement field for a point at an initial position $(r, \vartheta, z)$ in a [cylindrical coordinate system](@entry_id:266798) is purely tangential [@problem_id:2909474].

Let $\varphi(z)$ be the angle of rotation of the cross-section at an axial position $z$. The tangential displacement $u_\vartheta$ of a point at radius $r$ is given by the arc length formula, $u_\vartheta = r \varphi(z)$. For a uniform twist along the shaft, the rate of twist, which we will denote as $\phi$, is constant: $\phi = \frac{d\varphi}{dz}$. If the shaft is fixed at $z=0$ and twisted by an angle $\theta$ at $z=L$, then the rate of twist is simply $\phi = \theta/L$.

The deformation is captured by the engineering shear strain, which represents the change in angle between initially orthogonal line elements. The only non-zero strain component in pure torsion is the shear strain $\gamma_{\vartheta z}$, which we denote simply as $\gamma$. It is derived from the [displacement field](@entry_id:141476) as follows:
$$
\gamma(r, z) = \frac{\partial u_\vartheta}{\partial z} = \frac{\partial}{\partial z} (r \varphi(z)) = r \frac{d\varphi}{dz}
$$
For a uniform twist, this gives the fundamental kinematic relationship for torsion:
$$
\gamma(r) = r \phi
$$
This elegantly simple result reveals a crucial characteristic of torsional deformation: the **shear strain is zero at the center of the shaft ($r=0$) and increases linearly with the radial distance**, reaching its maximum value at the outer surface ($r=R$) [@problem_id:2909474]. This linear strain distribution is the kinematic foundation upon which the entire analysis of elastic and plastic torsion is built.

### Elastic Torsion and the Onset of Yielding

In the purely elastic regime, the relationship between shear stress $\tau$ and shear strain $\gamma$ is governed by Hooke's Law for shear: $\tau = G\gamma$, where $G$ is the shear modulus. Combining this constitutive law with the kinematic relation $\gamma(r) = r\phi$, we obtain the elastic [shear stress distribution](@entry_id:197453):
$$
\tau_{el}(r) = G \gamma(r) = G r \phi
$$
Like the strain, the **elastic shear stress is also zero at the center and increases linearly with the radius**. The external torque $T$ required to produce this stress distribution is the resultant moment of the stresses integrated over the cross-sectional area $A$.
$$
T = \int_{A} r \tau_{el}(r) \, dA = \int_{A} r (G r \phi) \, dA = G\phi \int_{A} r^2 \, dA
$$
The integral $\int_{A} r^2 \, dA$ is the **polar moment of area**, denoted by $J$. For a solid circular shaft of radius $R$, $J = \frac{\pi R^4}{2}$. This yields the familiar elastic torque-twist relationship:
$$
T = G J \phi
$$
We can now express the stress in terms of the applied torque by substituting $\phi = T/(GJ)$ back into the stress equation:
$$
\tau_{el}(r) = G r \left(\frac{T}{GJ}\right) = \frac{Tr}{J}
$$
This is the classic elastic [torsion formula](@entry_id:274909). Yielding begins when the stress at some point in the material reaches its limit. Since the stress is maximum at the outer surface ($r=R$), [plastic deformation](@entry_id:139726) will initiate there. Let the shear yield stress of the material be denoted by $k$. The onset of yielding occurs when $\tau_{\text{max}} = \tau_{el}(R) = k$. The torque at which this first occurs is the **yield torque**, $T_y$.
$$
k = \frac{T_y R}{J} \implies T_y = \frac{kJ}{R}
$$
For a solid circular shaft, substituting the expression for $J$ gives:
$$
T_y = k \frac{(\pi R^4 / 2)}{R} = \frac{\pi}{2} k R^3
$$
This torque represents the limit of purely elastic behavior [@problem_id:2909521] [@problem_id:2909520].

### Yield Criteria and the Shear Yield Stress, $k$

Thus far, we have treated the shear [yield stress](@entry_id:274513) $k$ as a given material property. However, in [plasticity theory](@entry_id:177023), material yield is typically characterized by tests under simpler stress states, most commonly the [uniaxial tension test](@entry_id:195375), which provides the uniaxial [yield stress](@entry_id:274513) $\sigma_y$. The value of $k$ is not an independent parameter but is related to $\sigma_y$ through a **yield criterion**, which defines the boundary of the elastic domain in a multi-axial [stress space](@entry_id:199156). For ductile metals, two criteria are prevalent [@problem_id:2909449].

1.  **Tresca (Maximum Shear Stress) Criterion**: This criterion posits that yielding occurs when the maximum shear stress at a point, $\tau_{\text{max}}$, reaches a critical value. In a [uniaxial tension test](@entry_id:195375) at yield, the [principal stresses](@entry_id:176761) are $(\sigma_y, 0, 0)$, giving $\tau_{\text{max}} = (\sigma_y - 0)/2 = \sigma_y/2$. This calibrates the criterion. In a state of pure shear, the stress tensor has components $\tau_{xy} = k$ and the principal stresses are $(k, 0, -k)$. The maximum shear stress is $\tau_{\text{max}} = (k - (-k))/2 = k$. Equating the two conditions at yield gives the relationship:
    $$
    k_{\text{Tresca}} = \frac{\sigma_y}{2}
    $$

2.  **Von Mises (Distortional Strain Energy) Criterion**: This more modern criterion states that yielding initiates when the second invariant of the [deviatoric stress tensor](@entry_id:267642), $J_2$, reaches a critical value. The criterion is formulated as $\sqrt{3J_2} = \sigma_y$. For [uniaxial tension](@entry_id:188287), $J_2 = \frac{1}{3}\sigma_y^2$, which satisfies the criterion. For pure shear, the [deviatoric stress tensor](@entry_id:267642) is identical to the stress tensor, and $J_2 = k^2$. Applying the von Mises criterion gives $\sqrt{3k^2} = \sigma_y$, which leads to:
    $$
    k_{\text{von Mises}} = \frac{\sigma_y}{\sqrt{3}} \approx 0.577 \sigma_y
    $$
The von Mises criterion is generally in better agreement with experimental data for ductile metals. For the remainder of this chapter, $k$ will refer to the shear [yield stress](@entry_id:274513) as defined by the appropriate criterion.

### Elasto-Plastic Torsion

When the applied torque $T$ exceeds the yield torque $T_y$, the outer region of the shaft becomes plastic. Since strain continues to increase linearly from the center, there will be an outer [annulus](@entry_id:163678) where the strain is large enough to induce [plastic flow](@entry_id:201346), and an inner core that remains elastic. Let the radius of this elastic core be $a$.

-   **Elastic Core ($0 \le r \le a$)**: In this region, the stress-strain relationship is still elastic, $\tau = G\gamma$. The stress remains linear with radius.
-   **Plastic Annulus ($a  r \le R$)**: In this region, the material has yielded. For an elastic-perfectly plastic material, the shear stress cannot exceed the yield stress $k$. Thus, throughout this annulus, the stress is constant: $\tau(r) = k$.

At the interface $r=a$, the stress must be continuous. The stress at the edge of the elastic core must therefore be equal to the yield stress: $\tau(a) = k$. Using the linear elastic relation in the core, $\tau(r) = Gr\phi$, we have $\tau(a) = Ga\phi = k$. This allows us to express the twist rate in terms of the elastic core radius: $\phi = k/(Ga)$. The stress distribution across the entire shaft can now be written solely in terms of $k$ and $a$ [@problem_id:2909495]:
$$
\tau(r) =
\begin{cases}
    k \frac{r}{a}   \text{ for } 0 \le r \le a \\
    k   \text{ for } a  r \le R
\end{cases}
$$
The total torque is found by integrating this stress distribution over the cross-section, summing the contributions from the elastic core ($T_{el}$) and the plastic [annulus](@entry_id:163678) ($T_{pl}$):
$$
T = T_{el} + T_{pl} = \int_{0}^{a} 2\pi r^2 \left(k \frac{r}{a}\right) dr + \int_{a}^{R} 2\pi r^2 (k) dr
$$
Evaluating these integrals yields:
$$
T = \frac{\pi k a^3}{2} + \frac{2\pi k}{3} (R^3 - a^3) = \frac{2\pi k R^3}{3} - \frac{\pi k a^3}{6}
$$
This equation can be rearranged into a more insightful form [@problem_id:2909490]:
$$
T = \frac{\pi k}{6} (4 R^3 - a^3)
$$
This fundamental relationship shows how the torque [carrying capacity](@entry_id:138018) increases as the elastic core radius $a$ shrinks. Conversely, for a given torque $T$ in the elasto-plastic range, we can determine the extent of the [plastic zone](@entry_id:191354) by solving for $a$ [@problem_id:2909495]:
$$
a = \left( 4R^3 - \frac{6T}{\pi k} \right)^{\frac{1}{3}}
$$

### Fully Plastic Torsion and the Shape Factor

As the applied torque continues to increase, the elastic core radius $a$ shrinks. The theoretical limit of this process is when the entire cross-section has yielded, i.e., when $a \to 0$. The torque at this limit is the **[fully plastic torque](@entry_id:192111)**, $T_p$. We can find it by setting $a=0$ in the elasto-plastic torque equation:
$$
T_p = \lim_{a \to 0} \frac{\pi k}{6} (4 R^3 - a^3) = \frac{4\pi k R^3}{6} = \frac{2\pi}{3} k R^3
$$
This state corresponds to a stress distribution where the shear stress is equal to the [yield stress](@entry_id:274513) $k$ at every point in the cross-section. The [fully plastic torque](@entry_id:192111) represents the ultimate torsional moment a shaft made of an elastic-perfectly plastic material can withstand under monotonic loading.

A useful dimensionless parameter is the **[shape factor](@entry_id:149022)**, $S$, which is the ratio of the [fully plastic torque](@entry_id:192111) to the yield torque. It quantifies the reserve strength available in the cross-section after yielding has initiated, owing to the redistribution of stress. For a solid circular shaft:
$$
S = \frac{T_p}{T_y} = \frac{\frac{2\pi}{3} k R^3}{\frac{\pi}{2} k R^3} = \frac{4}{3}
$$
A shape factor of $4/3$ means that the shaft can carry 33% more torque beyond the initial yield before it reaches its ultimate capacity [@problem_id:2909447] [@problem_id:2909520]. This reserve strength is a key benefit of using ductile materials in structural applications.

### Advanced Formulation: The Prandtl Stress Function

For non-circular [cross-sections](@entry_id:168295), the "planes remain plane" assumption is invalid, and the analysis becomes more complex. A powerful and general approach for both elastic and plastic torsion is the **Prandtl stress function**, $\phi(x,y)$. This scalar function is defined such that the shear stresses are given by its partial derivatives:
$$
\tau_{xz} = \frac{\partial \phi}{\partial y}, \qquad \tau_{yz} = - \frac{\partial \phi}{\partial x}
$$
This formulation ingeniously ensures that the stress-[equilibrium equations](@entry_id:172166) are automatically satisfied for any twice-differentiable function $\phi$. The plastic yield criterion can be expressed as a condition on the gradient of the stress function. For a von Mises material, the criterion $\tau_{xz}^2 + \tau_{yz}^2 \le k^2$ becomes [@problem_id:2909505]:
$$
\left(\frac{\partial \phi}{\partial x}\right)^2 + \left(\frac{\partial \phi}{\partial y}\right)^2 = |\nabla \phi|^2 \le k^2 \implies |\nabla \phi| \le k
$$
This means that in a plastic analysis, the magnitude of the gradient of the stress function must not exceed the shear [yield stress](@entry_id:274513) $k$. In regions where [plastic flow](@entry_id:201346) occurs, the equality $|\nabla \phi| = k$ holds.

The torque $T$ can also be expressed in terms of $\phi$. For a cross-section with a boundary on which $\phi$ is set to zero (which satisfies the traction-free condition on the outer surface), the torque is given by twice the volume under the surface defined by $\phi(x,y)$:
$$
T = 2 \int_A \phi \, dA
$$
This leads to the elegant "sand-hill" analogy. Imagine a mound of sand piled on the cross-section $A$, where the slope of the mound is constant and equal to the yield stress $k$. The shape of this mound is the stress function $\phi$, and its volume is proportional to the [fully plastic torque](@entry_id:192111). For a circular section, this mound is a cone. The function is $\phi(r) = k(R-r)$. Calculating the volume of this cone gives the [fully plastic torque](@entry_id:192111) [@problem_id:2909505]:
$$
T_p = 2 \int_0^{2\pi} \int_0^R k(R-r) r \, dr \, d\theta = 4\pi k \left[ \frac{Rr^2}{2} - \frac{r^3}{3} \right]_0^R = \frac{2\pi}{3} k R^3
$$
This confirms our previous result. This approach is underpinned by the **Lower Bound Theorem of plastic [limit analysis](@entry_id:188743)**, which can be formulated as an optimization problem: the [fully plastic torque](@entry_id:192111) is the result of maximizing $T = 2\int_A \phi \, dA$ over all admissible functions $\phi$ that satisfy $|\nabla \phi| \le k$ inside $A$ and $\phi = 0$ on the boundary of $A$ [@problem_id:2909482].

### Unloading and Residual Stresses

When a shaft that has been plastically deformed is unloaded, it does not return to a stress-free state. The plastic deformation is permanent, and upon removal of the external torque, a system of **residual stresses** remains locked in the material.

Consider the shaft twisted to the fully plastic state ($T=T_p$) and then unloaded to $T=0$. The unloading process is assumed to be purely elastic. We can model this by superimposing a reverse elastic stress distribution corresponding to a torque of $-T_p$. The stress change during unloading is:
$$
\Delta\tau_{unload}(r) = \frac{(-T_p) r}{J} = \frac{(-\frac{2\pi}{3} k R^3) r}{(\pi R^4 / 2)} = -\frac{4k}{3R} r
$$
The residual stress distribution, $\tau_{res}(r)$, is the sum of the fully plastic stress and this elastic unloading stress [@problem_id:2909458]:
$$
\tau_{res}(r) = \tau_{plastic}(r) + \Delta\tau_{unload}(r) = k - \frac{4k}{3R} r
$$
This [residual stress](@entry_id:138788) field is self-equilibrating (it produces zero net torque). It is compressive at the surface, with a value of $-\frac{1}{3}k$ at $r=R$, and becomes positive toward the center, approaching a value of $+k$ as $r \to 0$.

This [residual stress](@entry_id:138788) has a profound effect on subsequent reloading. If we now apply a torque in the reverse (negative) direction, the new stress state will be the sum of the [residual stress](@entry_id:138788) and the new applied elastic stress. Yielding will re-initiate when the total stress somewhere reaches the yield limit, which will be $-k$ for reverse loading. Since the [residual stress](@entry_id:138788) is already negative at the surface, yielding will start there again, but at a much lower applied torque. The total stress at the surface is:
$$
\tau_{total}(R) = \tau_{res}(R) + \frac{T_{rev} R}{J} = -\frac{1}{3}k + \frac{T_{rev} R}{J}
$$
Setting this to $-k$ at the point of re-yield gives the magnitude of the reverse yield torque, $|T_{rev, y}|$:
$$
-k = -\frac{1}{3}k - \frac{|T_{rev, y}| R}{J} \implies \frac{|T_{rev, y}| R}{J} = \frac{2}{3}k
$$
Solving for $|T_{rev, y}|$:
$$
|T_{rev, y}| = \frac{2k J}{3R} = \frac{2k}{3R} \left(\frac{\pi R^4}{2}\right) = \frac{\pi}{3} k R^3
$$
Recalling that the initial yield torque was $T_y = \frac{\pi}{2} k R^3$, we find that $|T_{rev, y}| = \frac{2}{3}T_y$. The [plastic deformation](@entry_id:139726) has effectively reduced the elastic range of the shaft for reverse loading, a phenomenon related to [kinematic hardening](@entry_id:172077), demonstrating that the material's response is dependent on its deformation history.