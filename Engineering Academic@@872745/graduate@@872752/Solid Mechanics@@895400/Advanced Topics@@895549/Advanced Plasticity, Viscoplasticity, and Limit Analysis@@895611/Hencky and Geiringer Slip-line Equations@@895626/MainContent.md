## Introduction
In the realms of [solid mechanics](@entry_id:164042) and engineering, understanding the behavior of materials undergoing large, permanent deformation is critical for predicting failure and designing robust processes. For phenomena such as metal forging, [extrusion](@entry_id:157962), and the [bearing capacity](@entry_id:746747) of foundations, where [plastic flow](@entry_id:201346) dominates, simplified models can provide profound insights. Slip-line [field theory](@entry_id:155241), built upon the mathematical framework of the Hencky and Geiringer equations, offers exactly such a model—a powerful analytical tool for analyzing the stress and velocity fields in [rigid-perfectly plastic](@entry_id:195711) materials under [plane strain](@entry_id:167046) conditions. This theory addresses the challenge of solving the nonlinear equations of plasticity by revealing a hidden geometric structure within the deforming material, enabling the exact calculation of limit loads for many important engineering problems.

This article provides a comprehensive exploration of [slip-line theory](@entry_id:184792), structured to build understanding from first principles to practical application. The first chapter, **Principles and Mechanisms**, derives the governing Hencky and Geiringer equations from the fundamentals of continuum plasticity, explaining their hyperbolic nature and the physical meaning of slip-lines as stress characteristics. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates how to apply the theory to solve canonical problems in geotechnical and mechanical engineering, and connects it to the broader concepts of [limit analysis](@entry_id:188743) and the [hodograph](@entry_id:195718) method. Finally, the **Hands-On Practices** section provides an opportunity to solidify this knowledge through guided computational and analytical exercises. By the end of this journey, you will be equipped to analyze and interpret complex plastic deformation patterns with confidence.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanics that govern the theory of slip-lines in [rigid-perfectly plastic](@entry_id:195711) materials under plane strain conditions. We will derive the governing equations from first principles, explore their physical and geometric interpretations, and place the theory within the broader context of continuum plasticity. The objective is to construct a rigorous and intuitive understanding of how stresses and velocities are distributed within a plastically deforming body.

### Foundations of the Plastic State in Plane Strain

The [slip-line theory](@entry_id:184792) is built upon the idealization of a material as **[rigid-perfectly plastic](@entry_id:195711)**. This model posits that the material does not deform elastically at all; it remains perfectly rigid until the stress state reaches a critical threshold, at which point it flows plastically without any increase in its resistance to deformation (i.e., no work hardening). While an idealization, this framework is exceptionally powerful for analyzing problems involving large plastic deformations, such as [metal forming](@entry_id:188560) processes, where elastic strains are negligible compared to plastic strains [@problem_id:2917575]. We shall confine our analysis to **plane strain** conditions, where deformation is restricted to a single plane.

#### Stress Representation and the Role of Pressure

In any [plasticity theory](@entry_id:177023), the state of stress is paramount. For a [material yielding](@entry_id:751736) under plane strain conditions, the stress state at any point can be fully described by three quantities: the **mean stress** $p$, the **maximum shear stress** in the plane of flow, which equals the material's shear yield strength $k$, and the **orientation of the principal stresses**, denoted by an angle $\theta$.

Let us define the mean stress as the average of the in-plane [principal stresses](@entry_id:176761), $\sigma_1$ and $\sigma_2$:
$$
p = \frac{\sigma_1 + \sigma_2}{2}
$$
The Tresca yield criterion, which is often employed in [slip-line theory](@entry_id:184792), states that yielding occurs when the maximum shear stress in the material reaches the shear yield strength $k$. For [plane strain](@entry_id:167046) in an [isotropic material](@entry_id:204616), the out-of-plane [principal stress](@entry_id:204375) $\sigma_3$ is the intermediate one, $\sigma_3 = (\sigma_1+\sigma_2)/2 = p$, so the [yield criterion](@entry_id:193897) simplifies to a condition on the in-plane stresses:
$$
\frac{|\sigma_1 - \sigma_2|}{2} = k \quad \text{or} \quad |\sigma_1 - \sigma_2| = 2k
$$
From these two relations, we can express the [principal stresses](@entry_id:176761) directly in terms of $p$ and $k$. Assuming $\sigma_1 \ge \sigma_2$:
$$
\sigma_1 = p + k
$$
$$
\sigma_2 = p - k
$$
If $\theta$ is the counter-clockwise angle from a fixed $x$-axis to the direction of the major principal stress $\sigma_1$, the components of the stress tensor in the $(x,y)$ coordinate system can be found via the standard [stress transformation](@entry_id:184474) equations:
$$
\sigma_{xx} = \frac{\sigma_1 + \sigma_2}{2} + \frac{\sigma_1 - \sigma_2}{2}\cos(2\theta) = p + k\cos(2\theta)
$$
$$
\sigma_{yy} = \frac{\sigma_1 + \sigma_2}{2} - \frac{\sigma_1 - \sigma_2}{2}\cos(2\theta) = p - k\cos(2\theta)
$$
$$
\sigma_{xy} = \frac{\sigma_1 - \sigma_2}{2}\sin(2\theta) = k\sin(2\theta)
$$
This [parameterization](@entry_id:265163) of the stress tensor is fundamental to the entire theory.

An essential feature of this model is the assumption of [plastic incompressibility](@entry_id:183440), meaning the volume of the material does not change during plastic flow ($\mathrm{tr}(\dot{\boldsymbol{\varepsilon}}^p) = 0$). From the principle of maximum [plastic dissipation](@entry_id:201273), this kinematic constraint has a profound consequence: the mean stress, or pressure, does no [plastic work](@entry_id:193085). Consequently, the value of $p$ is not determined by the material's [constitutive law](@entry_id:167255) in the same way the deviatoric stresses are. Instead, the mean stress $p$ acts as a **Lagrange multiplier** that enforces the [incompressibility constraint](@entry_id:750592). Its value is determined globally by the [equilibrium equations](@entry_id:172166) and the stress boundary conditions of the specific problem [@problem_id:2646127].

### The Governing Equations and Hyperbolic Structure

The stress field within the plastic region must satisfy the [equations of equilibrium](@entry_id:193797). In the absence of body forces, these are:
$$
\frac{\partial \sigma_{xx}}{\partial x} + \frac{\partial \sigma_{xy}}{\partial y} = 0
$$
$$
\frac{\partial \sigma_{xy}}{\partial x} + \frac{\partial \sigma_{yy}}{\partial y} = 0
$$
Substituting our [parameterization](@entry_id:265163) for the stress components in terms of the two scalar fields $p(x,y)$ and $\theta(x,y)$ into these [equilibrium equations](@entry_id:172166) yields a system of two coupled, first-order, quasi-[linear partial differential equations](@entry_id:171085) (PDEs) [@problem_id:2646131]:
$$
\frac{\partial p}{\partial x} - 2k\sin(2\theta)\frac{\partial \theta}{\partial x} + 2k\cos(2\theta)\frac{\partial \theta}{\partial y} = 0
$$
$$
\frac{\partial p}{\partial y} + 2k\cos(2\theta)\frac{\partial \theta}{\partial x} + 2k\sin(2\theta)\frac{\partial \theta}{\partial y} = 0
$$
A [mathematical analysis](@entry_id:139664) of this system reveals that it is of the **hyperbolic** type. This is a defining feature of [slip-line theory](@entry_id:184792). Hyperbolic systems possess real **[characteristic curves](@entry_id:175176)**, which are special paths in the $(x,y)$ plane along which information, and potential discontinuities in the derivatives of $p$ and $\theta$, can propagate.

In the context of [plane strain plasticity](@entry_id:201004), these [characteristic curves](@entry_id:175176) have a direct physical meaning: they are the curves whose tangents at every point coincide with the directions of maximum shear stress. These curves are known as **slip-lines**. For an [isotropic material](@entry_id:204616), the planes of maximum shear stress are oriented at $\pm 45^\circ$ to the [principal stress](@entry_id:204375) planes. Therefore, there are two families of slip-lines, conventionally denoted as $\alpha$-lines and $\beta$-lines, which are everywhere orthogonal to each other [@problem_id:2917575]. If the major [principal stress](@entry_id:204375) direction has angle $\theta$, the two slip-line families have tangent angles $\phi = \theta \pm \pi/4$.

### Hencky's Equations: The Stress Relations Along Slip-Lines

The power of the characteristic analysis is that the governing PDEs can be simplified into ordinary differential equations that hold along the [characteristic curves](@entry_id:175176). These simplified relations are known as **Hencky's equations**.

Let us adopt a common convention for the slip-line angles:
-   The **$\alpha$-line** has a tangent angle $\phi_\alpha = \theta - \pi/4$.
-   The **$\beta$-line** has a tangent angle $\phi_\beta = \theta + \pi/4$.

By transforming the governing PDEs to a coordinate system aligned with these characteristic directions, we find the following elegant relationships:
$$
dp - 2k\,d\theta = 0 \quad \text{along an } \alpha\text{-line}
$$
$$
dp + 2k\,d\theta = 0 \quad \text{along a } \beta\text{-line}
$$
These can be integrated to yield the famous **Hencky invariants**:
$$
p - 2k\theta = C_1 \quad (\text{constant along an } \alpha\text{-line})
$$
$$
p + 2k\theta = C_2 \quad (\text{constant along a } \beta\text{-line})
$$
These equations are the cornerstone of [slip-line field theory](@entry_id:181917). They state that as one moves along a slip-line, any change in the [mean stress](@entry_id:751819) $p$ must be accompanied by a proportional change in the orientation of the [principal stresses](@entry_id:176761) $\theta$. The constant of proportionality is simply twice the material's shear yield strength. Note that a different choice for the $\alpha$ and $\beta$ line definitions would swap the signs in these equations, but the underlying principle remains the same [@problem_id:2646131].

### Geometric Interpretation: The Stress-Curvature Relations

Hencky's equations acquire a powerful geometric meaning when related to the curvature of the slip-lines. The [signed curvature](@entry_id:273245) $\kappa$ of a [plane curve](@entry_id:271353) is defined as the rate of change of its tangent angle with respect to its arc length, $\kappa = d\phi/ds$. For our slip-line families, this gives:
-   Curvature of an $\alpha$-line: $\kappa_\alpha = \frac{d\phi_\alpha}{ds_\alpha} = \frac{d}{ds_\alpha}(\theta - \pi/4) = \frac{d\theta}{ds_\alpha}$
-   Curvature of a $\beta$-line: $\kappa_\beta = \frac{d\phi_\beta}{ds_\beta} = \frac{d}{ds_\beta}(\theta + \pi/4) = \frac{d\theta}{ds_\beta}$

The curvature of a slip-line is thus equal to the rate of change of the principal stress angle $\theta$ along that same line. We can now substitute these geometric relations into the [differential form](@entry_id:174025) of Hencky's equations:
$$
\frac{\partial p}{\partial s_\alpha} - 2k\frac{\partial \theta}{\partial s_\alpha} = 0 \implies \frac{\partial p}{\partial s_\alpha} = 2k\kappa_\alpha
$$
$$
\frac{\partial p}{\partial s_\beta} + 2k\frac{\partial \theta}{\partial s_\beta} = 0 \implies \frac{\partial p}{\partial s_\beta} = -2k\kappa_\beta
$$
The signed radius of curvature $R$ is the reciprocal of the curvature, $R = 1/\kappa$. The final relations are:
$$
\frac{\partial p}{\partial s_\alpha} = \frac{2k}{R_\alpha}
$$
$$
\frac{\partial p}{\partial s_\beta} = -\frac{2k}{R_\beta}
$$
These equations, which follow directly from Hencky's work, provide a profound connection between the stress state and the geometry of the flow. They state that a slip-line will be curved if and only if there is a gradient of [mean stress](@entry_id:751819) along it. A straight slip-line ($R \to \infty$) implies that the [mean stress](@entry_id:751819) is constant along that line.

The sign convention provides further physical insight [@problem_id:2646159]. If curvature is positive for a leftward turn, the equations tell us that for pressure to increase along an $\alpha$-line ($\partial p/\partial s_\alpha > 0$), the line must curve to the left ($\kappa_\alpha > 0$). Conversely, for pressure to increase along a $\beta$-line ($\partial p/\partial s_\beta > 0$), the line must curve to the right ($\kappa_\beta < 0$).

These relations can be used directly to analyze [plastic flow](@entry_id:201346). For instance, if local measurements of pressure gradients are available, one can immediately determine the local radii of curvature of the slip-line field [@problem_id:2646106]. As another example, in a region where the pressure gradient along all $\alpha$-lines is a non-zero constant, say $g_\alpha$, then their curvature $\kappa_\alpha = \frac{g_\alpha}{2k}$ must also be constant. A [plane curve](@entry_id:271353) of [constant curvature](@entry_id:162122) is a circular arc. Thus, such a region is composed of slip-lines that are arcs of circles with radius $R_\alpha = 2k/g_\alpha$ [@problem_id:2646148].

### Practical and Advanced Considerations

#### Yield Criteria and Mathematical Formulation

While the theory is often presented using the Tresca criterion, it applies more broadly. A remarkable result occurs when considering the **von Mises [yield criterion](@entry_id:193897)**. For an [associated flow rule](@entry_id:201731) under [plane strain](@entry_id:167046) conditions, the von Mises criterion reduces to an effective Tresca-like condition: the maximum in-plane shear stress is constant. The key difference lies in the value of the shear [yield strength](@entry_id:162154) $k$. If $\sigma_y$ is the uniaxial tensile [yield stress](@entry_id:274513), we find:
-   For Tresca: $k_T = \frac{\sigma_y}{2}$
-   For von Mises: $k_M = \frac{\sigma_y}{\sqrt{3}}$

This implies that for a given geometry, the slip-line *field* is identical for both Tresca and von Mises materials. The stress distribution is also geometrically identical, differing only by a scaling factor of $k_M / k_T \approx 1.155$. This allows solutions derived for one criterion to be readily adapted to the other [@problem_id:2646144].

For analytical and numerical work, it is often convenient to express the governing equations in a **characteristic coordinate system** $(\alpha, \beta)$, where constant values of the coordinates correspond to the slip-lines themselves. In such a system, the coupled Hencky and Geiringer equations take on an elegant, symmetric form reminiscent of the Cauchy-Riemann equations, facilitating advanced analysis and solution techniques [@problem_id:2646166]. The numerical construction of a slip-line field from boundary conditions involves integrating the ordinary differential equations that define the slip-line trajectories, a process that requires robust numerical methods to handle potential singularities like vertical tangents [@problem_id:2646145].

#### Broader Theoretical Context

It is crucial to recognize the assumptions underpinning the classical theory and its place within the wider landscape of plasticity.

**Associated vs. Non-Associated Flow:** The coincidence of the stress characteristics (slip-lines) and the velocity characteristics (lines of zero [extensional strain](@entry_id:183817) rate) is a direct consequence of the **[associated flow rule](@entry_id:201731)**, where the [plastic potential](@entry_id:164680) is the [yield function](@entry_id:167970) itself. If a material follows a **[non-associated flow rule](@entry_id:172454)**, with a [plastic potential](@entry_id:164680) $g$ distinct from the [yield function](@entry_id:167970) $f$, this coincidence is generally lost. The stress characteristics, being derived from equilibrium and the [yield surface](@entry_id:175331) $f$, remain unchanged. However, the velocity characteristics are determined by the geometry of the [plastic potential](@entry_id:164680) $g$. Thus, for non-associated materials, the directions of maximum shear stress are generally not the directions of zero extension [@problem_id:2646110].

**The Rigid-Plastic Limit:** The hyperbolic nature of the governing equations is an artifact of the [rigid-perfectly plastic](@entry_id:195711) idealization, which neglects both elasticity and rate-dependence. If one introduces a small amount of **rate sensitivity** ([viscoplasticity](@entry_id:165397)), the [deviatoric stress](@entry_id:163323) becomes a function of the [strain rate](@entry_id:154778). To obtain a closed system for stress, one must invoke the [strain compatibility](@entry_id:199659) equation, which is a second-order differential operator. This introduces second-order spatial derivatives of the stress field into the governing equations, fundamentally changing the PDE system from purely hyperbolic to a **mixed hyperbolic-parabolic type**. This process can be viewed as a [singular perturbation](@entry_id:175201): the small viscoplastic effect adds a diffusive term that smooths the sharp discontinuities allowed by the hyperbolic system. In the limit as the rate sensitivity vanishes, the solution to the viscoplastic problem converges (almost everywhere) to the rigid-plastic solution, and the Hencky invariants are recovered away from narrow internal layers [@problem_id:2646157]. This provides a deeper understanding of the slip-line model as a powerful, albeit idealized, limit of more complex material behavior.