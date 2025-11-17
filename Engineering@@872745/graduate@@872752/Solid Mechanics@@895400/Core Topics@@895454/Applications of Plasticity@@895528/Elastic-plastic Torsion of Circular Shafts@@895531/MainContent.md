## Introduction
The torsional response of circular shafts is a cornerstone of [mechanical engineering](@entry_id:165985), critical for the design of countless rotating components like axles and drivetrains. While elastic analysis provides a baseline for operation, it fails to capture the full picture of a component's strength and behavior under extreme loads. Relying solely on the [elastic limit](@entry_id:186242) can lead to overly conservative and inefficient designs, ignoring the significant reserve capacity inherent in ductile materials. This article addresses this gap by providing a comprehensive exploration of [elastic-plastic torsion](@entry_id:182269). Across three chapters, you will build a complete mechanical model from first principles, apply it to complex real-world scenarios, and engage in practical exercises to master its application. The journey begins in **Principles and Mechanisms**, where we will dissect the [kinematics](@entry_id:173318), stress distributions, and torque-twist relationships from initial yielding to full [plastic collapse](@entry_id:191981) and the formation of residual stresses. Next, **Applications and Interdisciplinary Connections** will demonstrate how these principles are used to analyze stress concentrations, combined loading, advanced materials, and predict [fatigue life](@entry_id:182388). Finally, **Hands-On Practices** will offer a chance to apply this knowledge through guided computational and analytical problems, bridging theory with practical engineering skill.

## Principles and Mechanisms

This chapter delineates the fundamental principles governing the behavior of circular shafts under [elastic-plastic torsion](@entry_id:182269). We will build, from first principles, a comprehensive mechanical model that describes the progression from initial [elastic deformation](@entry_id:161971) to full [plastic collapse](@entry_id:191981), and finally to the state of residual stress upon unloading.

### The Kinematics of Torsion in Circular Shafts

The analysis of torsion is greatly simplified for members with a circular cross-section, a consequence of their [axial symmetry](@entry_id:173333). The foundational kinematic assumption, validated by both theory and experiment for Saint-Venant torsion, is that cross-sections remain plane and rotate as rigid disks about the shaft's axis. This implies a specific and simple form for the [displacement field](@entry_id:141476).

Consider a prismatic circular shaft aligned with the $x$-axis. A point at a radial distance $r$ within a cross-section at an axial position $x$ experiences a purely circumferential displacement $u_{\theta}$ due to the rotation of that cross-section by an angle $\phi(x)$. This is expressed as:
$$ u_{\theta}(r, x) = r \phi(x) $$
The radial displacement $u_r$ is zero. A key feature of circular shafts is the absence of **warping**, meaning the axial displacement $u_x$ is also zero (or at most a uniform constant representing [rigid body motion](@entry_id:144691), which we can neglect). This is not an assumption but a direct consequence of axisymmetry. For the physical state (strains and stresses) to be axisymmetric, any potential warping displacement $u_x(r, \theta)$ must be independent of the angle $\theta$. Kinematic compatibility (ensuring single-valued displacements) and equilibrium then force the [warping function](@entry_id:187475) to be zero [@problem_id:2634766]. This holds true for both solid and hollow circular shafts and, critically, is independent of the material's constitutive law. Therefore, this kinematic model is valid for both elastic and elastic-plastic responses [@problem_id:2634760].

From this [displacement field](@entry_id:141476), we derive the only non-zero strain component. Under the assumption of small strains, the engineering shear strain $\gamma_{\theta x}$ is given by:
$$ \gamma_{\theta x} = \frac{\partial u_{\theta}}{\partial x} = r \frac{d\phi}{dx} $$
It is conventional to denote the rate of twist, or twist per unit length, as $\theta' = \frac{d\phi}{dx}$. The fundamental kinematic relationship for the [torsion of circular shafts](@entry_id:187981) is thus:
$$ \gamma(r) = r \theta' $$
This equation is central to our entire analysis. It states that the [shear strain](@entry_id:175241) is distributed linearly across the radius, being zero at the center ($r=0$) and maximum at the outer surface ($r=R$).

This linearized strain-displacement relation is an approximation valid for small displacement gradients. For finite, or large, rotations, the exact relationship between the shear angle $\varphi$ (the true angle of shear deformation) and the twist gradient is $\tan(\varphi) = r\theta'$. For small gradients, we use the approximation $\tan(\varphi) \approx \varphi$, letting $\gamma = \varphi$, which recovers the linear relation. The full theory also predicts a second-order axial stretch of material fibers, $\lambda_z = \sqrt{1 + (r\theta')^2}$, a phenomenon known as the Poynting effect. In the context of small strain theory, these higher-order terms are neglected, so we assume no change in length [@problem_id:2634717].

### Elastic Torsion and the Onset of Yielding

As long as the shaft material behaves elastically, the shear stress $\tau$ is proportional to the shear strain $\gamma$ through the [shear modulus](@entry_id:167228) $G$, according to Hooke's Law: $\tau = G\gamma$. Combining this with the kinematic relation gives the elastic stress distribution:
$$ \tau(r) = G \gamma(r) = G r \theta' $$
Like the strain, the elastic shear stress is zero at the center and increases linearly to a maximum at the outer surface.

Yielding initiates when the stress state at some point in the body first satisfies a chosen yield criterion. For pure shear, both the Tresca and von Mises criteria simplify to a condition on the magnitude of the shear stress, $|\tau|$, reaching a critical value, the shear [yield stress](@entry_id:274513) $\tau_y$. Since the shear stress is maximal at the outer radius $r=R$, yielding must begin at the surface of the shaft [@problem_id:2634740].

The torque corresponding to this initiation of yielding is known as the **[elastic limit](@entry_id:186242) torque**, $T_e$. We can derive it by relating the stress distribution to the applied torque $T$ through equilibrium. The torque is the integral of the moment produced by the shear stress over the cross-sectional area $A$:
$$ T = \int_A r \tau(r) dA = \int_0^R r (G r \theta') (2\pi r dr) = G \theta' \int_0^R 2\pi r^3 dr $$
The integral term is the polar [second moment of area](@entry_id:190571), $J = \frac{\pi R^4}{2}$ for a solid circular section. Thus, we have the famous elastic [torsion formula](@entry_id:274909):
$$ T = G J \theta' $$
First yield occurs when $\tau_{max} = \tau(R) = \tau_y$. From the stress distribution, $\tau(R) = G R \theta'$, so at yield, $\tau_y = G R \theta'_e$, where $\theta'_e$ is the twist rate at the [elastic limit](@entry_id:186242). Substituting this into the torque equation gives the [elastic limit](@entry_id:186242) torque [@problem_id:2634762]:
$$ T_e = G J \left( \frac{\tau_y}{GR} \right) = \frac{J}{R} \tau_y = \frac{\pi R^3}{2} \tau_y $$
The dependence $T_e \propto R^3$ arises physically because the torque capacity scales with both the area over which stress acts ($R^2$) and the average lever arm of that stress ($R$).

### Partially Plastic Torsion

When the applied torque $T$ exceeds the [elastic limit](@entry_id:186242) $T_e$, a plastic region develops. Assuming a perfectly plastic material (one that cannot sustain stress greater than $\tau_y$), the stress in the yielded region remains constant at $\tau_y$. Since yielding starts at the surface, the plastic zone forms as an outer annulus that propagates inward as the torque increases. This leaves an **elastic core** in the center, which still follows the laws of elasticity.

For a torque $T$ such that $T_e  T  T_p$ (where $T_p$ is the [fully plastic torque](@entry_id:192111)), the cross-section is partially plastic. Let the radius of the elastic-plastic interface be $c$. The stress distribution is now piecewise:

1.  **Elastic Core ($0 \le r \le c$)**: The material is elastic. The stress is still linear with radius, $\tau(r) = G r \theta'$. At the interface $r=c$, the stress must equal the yield stress, so $\tau(c) = G c \theta' = \tau_y$. This provides a crucial link: $\theta' = \frac{\tau_y}{Gc}$. Substituting this back, the stress profile in the core is $\tau_{el}(r) = \tau_y \frac{r}{c}$.

2.  **Plastic Annulus ($c  r \le R$)**: The material has yielded. The stress is constant at the yield value: $\tau_{pl}(r) = \tau_y$.

The total torque is the sum of the contributions from the elastic core and the plastic [annulus](@entry_id:163678):
$$ T = \int_0^c \tau_{el}(r) (2\pi r^2 dr) + \int_c^R \tau_{pl}(r) (2\pi r^2 dr) $$
$$ T = \int_0^c \left(\tau_y \frac{r}{c}\right) 2\pi r^2 dr + \int_c^R \tau_y (2\pi r^2 dr) $$
Evaluating these integrals gives the relationship between the applied torque and the elastic core radius:
$$ T = 2\pi \tau_y \left[ \frac{c^3}{4} + \frac{R^3-c^3}{3} \right] = 2\pi \tau_y \left( \frac{R^3}{3} - \frac{c^3}{12} \right) $$
This equation shows how the torque is carried by the partially plastic section. We can invert this expression to find the elastic core radius $c$ for a given applied torque $T$ [@problem_id:2634767] [@problem_id:2634734]:
$$ c = \left( 4R^3 - \frac{6T}{\pi \tau_y} \right)^{\frac{1}{3}} $$
As torque $T$ increases from $T_e$ towards $T_p$, the elastic core radius $c$ shrinks from $R$ towards $0$. Even as plasticity spreads, the torque-carrying capacity continues to increase, meaning there is no load drop at first yield. This progressive yielding provides a stable, ductile response [@problem_id:2634740].

### Fully Plastic Torsion and Limit Torque

The ultimate torque capacity of the shaft is reached when the entire cross-section becomes plastic. This corresponds to the elastic core radius shrinking to zero, $c=0$. This state defines the **[fully plastic torque](@entry_id:192111)**, $T_p$. We can find $T_p$ by setting $c=0$ in the torque equation for the partially plastic section, or by directly integrating the fully plastic stress distribution, $\tau(r) = \tau_y$ for all $r \in [0, R]$:
$$ T_p = \int_0^R \tau_y (2\pi r^2 dr) = 2\pi \tau_y \left[ \frac{r^3}{3} \right]_0^R = \frac{2\pi R^3}{3} \tau_y $$
For a [rigid-perfectly plastic](@entry_id:195711) material, once the torque reaches $T_p$, the shaft can undergo unlimited twisting at this constant torque, forming a "[plastic hinge](@entry_id:200267)." The stress profile cannot increase further, and thus the resultant torque is capped at $T_p$ [@problem_id:2634733].

A very useful quantity in plastic design is the **[shape factor](@entry_id:149022)**, which is the ratio of the [fully plastic torque](@entry_id:192111) to the [elastic limit](@entry_id:186242) torque. For a solid circular shaft in torsion:
$$ \frac{T_p}{T_e} = \frac{\frac{2}{3}\pi R^3 \tau_y}{\frac{1}{2}\pi R^3 \tau_y} = \frac{4}{3} $$
This ratio, being greater than one, quantifies the reserve strength of the member beyond its [elastic limit](@entry_id:186242). It implies that a design based on preventing first yield is conservative; the shaft has an additional $33.3\%$ of torque capacity before it reaches catastrophic failure by [plastic collapse](@entry_id:191981). This plastic reserve capacity is a key reason for the use of ductile materials in structures designed to withstand extreme loads [@problem_id:2634738]. It is important to note, however, that real metals exhibit **[strain hardening](@entry_id:160233)**, where the [flow stress](@entry_id:198884) increases with plastic strain. For such materials, the torque-twist curve will continue to rise beyond the idealized $T_p$, providing even greater resistance [@problem_id:2634733].

### Unloading and Residual Stresses

If the shaft is unloaded after being twisted into the plastic range, it will not return to its original state. The process of unloading from a torque $T^{(1)} > T_e$ is assumed to be purely elastic. The change in stress during unloading is therefore linear with radius, $\Delta \tau_{unload}(r) = -G r \Delta \theta'$. The total change in torque is $-T^{(1)}$, so the unloading stress distribution is identical in form to a purely elastic loading:
$$ \Delta \tau_{unload}(r) = -\frac{T^{(1)} r}{J} $$
The final stress state upon removal of the external torque is the **[residual stress](@entry_id:138788)**, found by superposing the stress at peak load, $\tau_{load}(r)$, with the elastic unloading stress change:
$$ \tau_{res}(r) = \tau_{load}(r) + \Delta \tau_{unload}(r) $$
Since the unloading stress change is largest at the outer surface, it "over-compensates" for the stress there. This results in a characteristic residual stress profile:
*   Near the surface ($r=R$), the residual stress is compressive (opposite in sign to the original applied torque).
*   In the core, the [residual stress](@entry_id:138788) is tensile (same sign as the original torque).

This distribution is self-equilibrating, meaning the [net torque](@entry_id:166772) resulting from it is zero. The shaft is left in a state of [internal stress](@entry_id:190887) even with no external load. Concurrently, the shaft retains a **permanent twist**, a consequence of the non-recoverable plastic strains.

These residual stresses have profound implications for subsequent loading, particularly under cyclic conditions. When a new torque is applied, the local stress is the sum of the [residual stress](@entry_id:138788) and the new applied stress. At the surface, the compressive residual stress acts as a local mean stress. If the shaft is subjected to fully reversed cyclic torsion, this residual stress will increase the magnitude of the total shear stress during the reverse-loading half-cycle. This can lead to earlier re-yielding in the reverse direction and accelerate fatigue crack initiation [@problem_id:2634763].

This effect is compounded by the **Bauschinger effect**, a material phenomenon where [plastic deformation](@entry_id:139726) in one direction reduces the yield strength in the reverse direction. In plasticity models with **[kinematic hardening](@entry_id:172077)**, this is represented by a "backstress" that shifts the [yield surface](@entry_id:175331). The combination of detrimental residual stresses at the surface and a reduced reverse [yield strength](@entry_id:162154) significantly impacts the [low-cycle fatigue](@entry_id:161555) life of components that have been previously overloaded [@problem_id:2634763]. While the residual stress in the core may be beneficial for a subsequent positive loading cycle, fatigue cracks in torsion almost always initiate at the surface, where the combination of strain amplitude, residual stress, and environmental exposure is most severe [@problem_id:2634763].