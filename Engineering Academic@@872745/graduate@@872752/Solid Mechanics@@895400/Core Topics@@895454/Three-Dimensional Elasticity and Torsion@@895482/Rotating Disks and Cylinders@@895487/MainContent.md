## Introduction
The analysis of stresses within rotating components such as disks, flywheels, and turbines is a cornerstone of mechanical and aerospace engineering. As these parts spin at high angular velocities, the resulting inertial forces generate complex internal stress fields that can compromise [structural integrity](@entry_id:165319) and lead to catastrophic failure. A rigorous understanding of these stresses is therefore not just an academic exercise, but a fundamental requirement for the safe and efficient design of countless modern technologies. This article addresses the classical problem of determining the stress and displacement in rotating disks and cylinders, bridging the gap between abstract theory and practical application by systematically developing the governing principles from the ground up.

We will begin in "Principles and Mechanisms" by deriving the foundational equations from [kinematics](@entry_id:173318), equilibrium, and constitutive laws, culminating in solutions for solid and annular disks. Next, "Applications and Interdisciplinary Connections" will demonstrate how these core principles are applied to solve complex design challenges, from shrink-fitted flywheels to [thermoelastic analysis](@entry_id:199630), and how they inform failure prediction. Finally, "Hands-On Practices" will offer a series of guided problems to reinforce these concepts and build practical analytical skills. This structured journey will equip you with the essential tools to analyze and design rotating mechanical components.

## Principles and Mechanisms

The [stress analysis](@entry_id:168804) of rotating bodies, such as disks, cylinders, and shafts, is a classical problem in [solid mechanics](@entry_id:164042) with profound importance in mechanical engineering, aerospace design, and materials science. The steady rotation of a body generates inertial forces that induce a state of internal stress, which can lead to deformation and potential failure. This chapter delineates the fundamental principles and mechanisms governing the elastic behavior of rotating disks and cylinders. We will systematically build the theoretical framework from first principles, combining [kinematics](@entry_id:173318), equilibrium, and constitutive laws to derive the stress and displacement fields for [canonical geometries](@entry_id:747105).

### Governing Physical Principles

The analysis of stresses in a rotating elastic body rests on three foundational pillars: the characterization of [inertial forces](@entry_id:169104), the [kinematics of deformation](@entry_id:189142), and the laws of [mechanical equilibrium](@entry_id:148830). We will address each in turn for an axisymmetric rotating body.

#### The Inertial Body Force

When a body rotates at a constant angular velocity $\omega$, each of its constituent material particles undergoes [uniform circular motion](@entry_id:178264). From the perspective of an inertial (non-accelerating) frame of reference, a particle at a radial distance $r$ from the [axis of rotation](@entry_id:187094) experiences a [centripetal acceleration](@entry_id:190458), $\boldsymbol{a}$, directed radially inward. For a particle with [position vector](@entry_id:168381) $\boldsymbol{r}$, the velocity is given by $\boldsymbol{v} = \boldsymbol{\omega} \times \boldsymbol{r}$, where $\boldsymbol{\omega}$ is the [angular velocity vector](@entry_id:172503). The [material acceleration](@entry_id:270992), which is the [total time derivative](@entry_id:172646) of velocity following the particle, is:

$$ \boldsymbol{a} = \frac{D\boldsymbol{v}}{Dt} = \boldsymbol{\omega} \times (\boldsymbol{\omega} \times \boldsymbol{r}) $$

For rotation about the $z$-axis, $\boldsymbol{\omega} = \omega \boldsymbol{e}_z$, and for a point at a radial position $r$ in the plane of rotation, this acceleration simplifies to $\boldsymbol{a} = -\omega^2 r \boldsymbol{e}_r$. The negative sign indicates the acceleration vector points towards the center of rotation.

According to Cauchy's first law of motion, the divergence of the stress tensor $\boldsymbol{\sigma}$ balances the product of mass density $\rho$ and acceleration $\boldsymbol{a}$ (in the absence of other body forces): $\nabla \cdot \boldsymbol{\sigma} = \rho \boldsymbol{a}$. A common and powerful technique in [engineering mechanics](@entry_id:178422) is to transpose the inertial term to the left-hand side of the equation, creating a quasi-[static equilibrium](@entry_id:163498) problem:

$$ \nabla \cdot \boldsymbol{\sigma} - \rho \boldsymbol{a} = \boldsymbol{0} $$

This allows us to treat the term $-\rho \boldsymbol{a}$ as an **effective [body force](@entry_id:184443) density**, often called the **[centrifugal force](@entry_id:173726) density**. Substituting the expression for [centripetal acceleration](@entry_id:190458), we obtain the effective [body force](@entry_id:184443), $\boldsymbol{b}_{\text{eff}}$:

$$ \boldsymbol{b}_{\text{eff}} = - \rho \boldsymbol{a} = - \rho (-\omega^2 r \boldsymbol{e}_r) = \rho \omega^2 r \boldsymbol{e}_r $$

This result establishes the fundamental loading condition for a rotating body: it is equivalent to a static body subjected to a fictitious [body force](@entry_id:184443) that acts radially outward, with a magnitude proportional to the radial distance $r$ from the axis of rotation [@problem_id:2914813]. This force is what tends to pull the material of the disk apart.

#### Kinematics of Axisymmetric Deformation

Under the influence of the centrifugal body force, the rotating disk will deform. For a perfectly balanced, homogeneous disk, the deformation will be **axisymmetric**; that is, the displacement of any point will depend only on its [radial coordinate](@entry_id:165186), $r$. Furthermore, the displacement will be purely radial, so the displacement field $\boldsymbol{u}$ can be described by a single scalar function, $u(r)$, such that $u_r = u(r)$, $u_\theta = 0$, and $u_z = 0$.

The deformation of the material is quantified by the [infinitesimal strain tensor](@entry_id:167211), $\boldsymbol{\epsilon}$. For the prescribed axisymmetric [displacement field](@entry_id:141476), we can derive the relevant strain components. The **radial strain**, $\epsilon_r$, represents the stretching of a line element in the radial direction. It is defined as the gradient of the radial displacement:

$$ \epsilon_r = \frac{du}{dr} $$

The **circumferential strain** or **[hoop strain](@entry_id:174548)**, $\epsilon_\theta$, represents the stretching of a circumferential [line element](@entry_id:196833). A circular fiber of initial radius $r$ has an initial circumference of $2\pi r$. After deformation, its radius becomes $r + u(r)$, and its new circumference is $2\pi(r + u(r))$. The [hoop strain](@entry_id:174548) is the fractional change in circumference:

$$ \epsilon_\theta = \frac{2\pi(r + u(r)) - 2\pi r}{2\pi r} = \frac{u(r)}{r} $$

These two equations, $\epsilon_r = du/dr$ and $\epsilon_\theta = u/r$, are the fundamental **kinematic relations** for axisymmetric problems. They connect the geometry of deformation (strains) to the displacement field [@problem_id:2914767]. It is crucial to recognize that these relations are purely geometric and independent of the forces or material properties involved.

#### Equilibrium and Symmetry Considerations

The final piece of the puzzle is the condition of [mechanical equilibrium](@entry_id:148830). In [cylindrical coordinates](@entry_id:271645), the divergence of the stress tensor leads to a set of three scalar [equilibrium equations](@entry_id:172166). A key simplification arises from the axisymmetry of the problem. For a perfectly balanced disk, all geometric properties, material properties, and loading conditions are independent of the angular coordinate $\theta$. Due to this symmetry, the resulting stress field must also be axisymmetric.

This has a powerful consequence for the in-plane shear stress, $\sigma_{r\theta}$. One can argue from symmetry (Neumann's Principle) that since the system is invariant under a reflection across any meridional plane (a plane containing the $z$-axis), the physical state must also be invariant. Such a reflection reverses the sign of the [basis vector](@entry_id:199546) $\boldsymbol{e}_\theta$ while leaving $\boldsymbol{e}_r$ unchanged. A shear stress component like $\sigma_{r\theta}$ would change sign under this operation. For the state to be invariant, the component must be equal to its negative, which is only possible if it is zero. Alternatively, one can use the $\theta$-component of the [equilibrium equation](@entry_id:749057), which, under axisymmetry and steady rotation (no [tangential acceleration](@entry_id:173884)), reduces to a simple differential equation whose only physically plausible solution (one that is regular at the center and satisfies [traction-free boundary](@entry_id:197683) conditions) is $\sigma_{r\theta}(r,z) = 0$ everywhere [@problem_id:2914758].

With all shear stresses involving the $\theta$-direction being zero, the only non-trivial [equilibrium equation](@entry_id:749057) is the one for the radial direction:

$$ \frac{d\sigma_r}{dr} + \frac{\sigma_r - \sigma_\theta}{r} + b_r = 0 $$

Substituting the expression for the centrifugal body force, we arrive at the **radial [equilibrium equation](@entry_id:749057)** for a rotating disk:

$$ \frac{d\sigma_r}{dr} + \frac{\sigma_r - \sigma_\theta}{r} + \rho \omega^2 r = 0 $$

This equation provides a differential relationship between the [radial stress](@entry_id:197086) $\sigma_r$ and the [hoop stress](@entry_id:190931) $\sigma_\theta$.

### Material Behavior and Idealized Models

To solve the [equilibrium equation](@entry_id:749057), we need a relationship between the stresses ($\sigma_r, \sigma_\theta$) and the strains ($\epsilon_r, \epsilon_\theta$). This is provided by the material's **[constitutive law](@entry_id:167255)**. For most metals and many other engineering materials under typical operating conditions, we can assume the behavior is **isotropic** and **linearly elastic**, governed by Hooke's Law.

The general 3D Hooke's Law in cylindrical coordinates relates all six independent components of stress and strain. However, for many practical geometries, we can employ simplifying idealizations that reduce the dimensionality of the problem. The two most common are [plane stress and plane strain](@entry_id:172357).

#### Plane Stress and Plane Strain Idealizations

The choice between a [plane stress](@entry_id:172193) and a [plane strain](@entry_id:167046) model is dictated by the geometry of the component and the constraints on its out-of-plane deformation [@problem_id:2682035].

A state of **plane stress** is assumed when one of the [principal stresses](@entry_id:176761) is zero. For a thin disk with thickness $t$ much smaller than its radius $R$ ($t \ll R$), whose flat faces are not subjected to any external forces (traction-free), the stress component normal to these faces, $\sigma_z$, is zero at the surfaces. Because the disk is thin, it is an excellent approximation to assume that $\sigma_z = 0$ throughout the entire thickness. This does not mean the out-of-[plane strain](@entry_id:167046) $\epsilon_z$ is zero; in fact, the disk is free to contract or expand in the thickness direction due to the Poisson effect, resulting in a non-zero $\epsilon_z = -(\nu/E)(\sigma_r + \sigma_\theta)$.

A state of **[plane strain](@entry_id:167046)** is assumed when the strain component in one direction is zero. This model is appropriate for bodies that are very long in one direction and are constrained from deforming in that direction. For example, a long rotating cylinder or shaft whose ends are fixed by rigid plates will experience negligible [axial strain](@entry_id:160811) ($\epsilon_z \approx 0$) in regions far from the ends. In this case, an axial stress, $\sigma_z = \nu(\sigma_r + \sigma_\theta)$, develops to enforce this kinematic constraint.

For the remainder of this chapter, we will focus on the **plane stress** model, which is appropriate for thin rotating disks.

#### Constitutive Relations for Plane Stress

Under the [plane stress assumption](@entry_id:184389) ($\sigma_z = 0$), the general 3D Hooke's law simplifies significantly. The in-plane strains are given by:

$$ \epsilon_r = \frac{1}{E} (\sigma_r - \nu \sigma_\theta) $$
$$ \epsilon_\theta = \frac{1}{E} (\sigma_\theta - \nu \sigma_r) $$

where $E$ is the Young's modulus and $\nu$ is the Poisson's ratio. To solve our problem, it is more convenient to express stresses in terms of strains. By solving this system of two linear equations for $\sigma_r$ and $\sigma_\theta$, we obtain the inverted plane stress [constitutive relations](@entry_id:186508) [@problem_id:2914731]:

$$ \sigma_r = \frac{E}{1-\nu^2} (\epsilon_r + \nu \epsilon_\theta) $$
$$ \sigma_\theta = \frac{E}{1-\nu^2} (\epsilon_\theta + \nu \epsilon_r) $$

These equations provide the missing link between the kinetics (stresses) and the kinematics (strains) for our specific material model.

### The Master Equation for a Rotating Disk

We now possess all the necessary components to formulate a single governing differential equation for the displacement in a rotating disk. The procedure is as follows:

1.  Start with the inverted [plane stress](@entry_id:172193) [constitutive relations](@entry_id:186508).
2.  Substitute the kinematic relations ($\epsilon_r = du/dr$, $\epsilon_\theta = u/r$) to express stresses in terms of the radial displacement function $u(r)$:
    $$ \sigma_r(r) = \frac{E}{1-\nu^2} \left( \frac{du}{dr} + \nu \frac{u}{r} \right) $$
    $$ \sigma_\theta(r) = \frac{E}{1-\nu^2} \left( \frac{u}{r} + \nu \frac{du}{dr} \right) $$
3.  Substitute these expressions for $\sigma_r$ and $\sigma_\theta$ into the radial [equilibrium equation](@entry_id:749057).

After carrying out the differentiation and algebraic simplification, we arrive at the master governing equation for the radial displacement $u(r)$ in a thin rotating disk under plane stress [@problem_id:2682056]:

$$ \frac{d^2u}{dr^2} + \frac{1}{r}\frac{du}{dr} - \frac{u}{r^2} = - \frac{\rho \omega^2 (1-\nu^2)}{E} r $$

This can be rewritten by multiplying by $r^2$ to reveal its structure more clearly:

$$ r^2 \frac{d^2u}{dr^2} + r \frac{du}{dr} - u = - \frac{\rho \omega^2 (1-\nu^2)}{E} r^3 $$

This is a non-homogeneous **Cauchy-Euler equation**. Its solution consists of two parts: a general solution to the homogeneous equation, $u_h(r)$, and a particular solution to the non-homogeneous equation, $u_p(r)$. The [homogeneous solution](@entry_id:274365) is found to be $u_h(r) = C_1 r + C_2/r$, and a [particular solution](@entry_id:149080) is $u_p(r) = A r^3$. The full general solution for the displacement is:

$$ u(r) = C_1 r + \frac{C_2}{r} - \frac{\rho \omega^2 (1-\nu^2)}{8E} r^3 $$

From this, we can find the general solutions for the radial and hoop stresses by substituting back into the stress-displacement relations:

$$ \sigma_r(r) = \frac{E}{1-\nu} C_1 - \frac{E}{1+\nu} \frac{C_2}{r^2} - \frac{3+\nu}{8} \rho \omega^2 r^2 $$
$$ \sigma_\theta(r) = \frac{E}{1-\nu} C_1 + \frac{E}{1+\nu} \frac{C_2}{r^2} - \frac{1+3\nu}{8} \rho \omega^2 r^2 $$

The constants of integration, $C_1$ and $C_2$, are determined by applying boundary conditions specific to the geometry of the disk.

### Application to Specific Geometries

We now apply the general solution to two fundamentally important cases: the solid disk and the annular disk (a disk with a central hole).

#### The Solid Rotating Disk

Consider a solid disk of outer radius $a$. The material extends to the center at $r=0$. To find the specific solution, we must impose two boundary conditions.

1.  **Regularity at the Center:** The displacement and stresses must remain finite at the center of the disk ($r=0$). In the general solutions, the terms involving $C_2/r$ and $C_2/r^2$ would become singular as $r \to 0$. Physical plausibility demands that we set $C_2=0$.
2.  **Traction-Free Outer Rim:** The outer cylindrical surface at $r=a$ is not in contact with anything, so the [radial stress](@entry_id:197086) must vanish there: $\sigma_r(a) = 0$.

Applying $C_2=0$ to the general solution for $\sigma_r(r)$ gives $\sigma_r(r) = \frac{E}{1-\nu} C_1 - \frac{3+\nu}{8} \rho \omega^2 r^2$. Applying the second boundary condition allows us to solve for $C_1$. Substituting this constant back yields the final stress distributions [@problem_id:2682039]:

$$ \sigma_r(r) = \frac{3+\nu}{8} \rho \omega^2 (a^2 - r^2) $$

$$ \sigma_\theta(r) = \frac{\rho \omega^2}{8} \left[ (3+\nu)a^2 - (1+3\nu)r^2 \right] $$

These equations reveal several key features. Both stresses are tensile throughout the disk ($\sigma_r \ge 0$, $\sigma_\theta \ge 0$). The [radial stress](@entry_id:197086) is maximum at the center ($r=0$) and falls to zero at the free edge ($r=a$). The hoop stress is also maximum at the center. At $r=0$, both stresses are equal:

$$ \sigma_{r, \max} = \sigma_{\theta, \max} = \sigma_r(0) = \sigma_\theta(0) = \frac{3+\nu}{8} \rho \omega^2 a^2 $$

This equality is required by axisymmetry; at the origin, the radial and circumferential directions are indistinguishable. The maximum stress in a solid rotating disk occurs at its center.

#### The Annular Rotating Disk

Now consider an annular disk with inner radius $b$ and outer radius $a$. The material exists only in the domain $b \le r \le a$. The boundary conditions are different from the solid disk case:

1.  **Traction-Free Inner Rim:** The inner surface at $r=b$ is traction-free, so $\sigma_r(b) = 0$.
2.  **Traction-Free Outer Rim:** The outer surface at $r=a$ is traction-free, so $\sigma_r(a) = 0$.

Here, the regularity condition at $r=0$ is irrelevant as the origin is not part of the material. Both constants $C_1$ and $C_2$ will be non-zero. Applying these two conditions to the general expression for $\sigma_r(r)$ gives a system of two [linear equations](@entry_id:151487) for the two integration constants. Solving this system and substituting the constants back into the general stress expressions yields the solution for the annular disk [@problem_id:2682064]:

$$ \sigma_r(r) = \frac{3+\nu}{8} \rho \omega^2 \left( a^2 + b^2 - \frac{a^2 b^2}{r^2} - r^2 \right) $$

$$ \sigma_\theta(r) = \frac{\rho \omega^2}{8} \left[ (3+\nu) \left( a^2 + b^2 + \frac{a^2b^2}{r^2} \right) - (1+3\nu)r^2 \right] $$

While more complex, these expressions allow for a complete analysis of the stress state. One of the most important findings from analyzing these equations is that the hoop stress $\sigma_\theta(r)$ is a monotonically decreasing function of $r$ in the domain $[b, a]$. Therefore, the maximum [hoop stress](@entry_id:190931) in an annular disk always occurs at the **inner radius**, $r=b$.

### Key Phenomena and Interpretations

The mathematical solutions derived above reveal critical physical phenomena that are paramount in engineering design.

#### Stress Concentration in Annular Disks

A comparison between the solid and annular disk solutions reveals a startling and fundamentally important effect. In the solid disk, the maximum stress is at the center. In the annular disk, the maximum stress moves to the inner boundary. Let's compare the magnitude of the peak hoop stress in both cases [@problem_id:2682042].

Peak stress in solid disk (at $r=0$): $\sigma_{\theta, \max}^{\text{solid}} = \frac{3+\nu}{8} \rho \omega^2 a^2$.

Peak stress in annular disk (at $r=b$): $\sigma_{\theta, \max}^{\text{annular}} = \sigma_\theta(b) = \frac{\rho \omega^2}{4} \left[ (3+\nu)a^2 + (1-\nu)b^2 \right]$.

Notice that the peak stress in the annular disk is always greater than in the solid disk. To see the dramatic effect of introducing a hole, let's consider the limit as the hole becomes infinitesimally small, i.e., $b \to 0$:

$$ \lim_{b\to 0} \sigma_{\theta, \max}^{\text{annular}} = \frac{\rho \omega^2}{4} (3+\nu)a^2 = 2 \left( \frac{3+\nu}{8} \rho \omega^2 a^2 \right) = 2 \cdot \sigma_{\theta, \max}^{\text{solid}} $$

This is a remarkable result: introducing a vanishingly small hole at the center of a rotating disk **doubles** the maximum stress. The stress that was at the center is forced to redistribute around the new free surface, and in doing so, it concentrates at the edge of the hole. This phenomenon is a classic example of **[stress concentration](@entry_id:160987)**. Any small hole, notch, or geometric discontinuity can act as a stress raiser, creating a local stress that is significantly higher than the [nominal stress](@entry_id:201335) in the surrounding material. This is a primary consideration in the design of mechanical components to prevent fatigue and fracture initiation.

#### The Role of Poisson's Ratio

The material properties, particularly Poisson's ratio $\nu$, play a subtle but important role in the stress distribution. We can investigate this by examining the difference between the principal stresses, $\sigma_\theta - \sigma_r$, for the solid disk case [@problem_id:2682003]. Using the derived stress expressions:

$$ \sigma_\theta(r) - \sigma_r(r) = \frac{\rho \omega^2}{8} \left[ \left((3+\nu)a^2 - (1+3\nu)r^2\right) - \left((3+\nu)a^2 - (3+\nu)r^2\right) \right] $$
$$ \sigma_\theta(r) - \sigma_r(r) = \frac{\rho \omega^2 r^2}{8} [ (3+\nu) - (1+3\nu) ] = \frac{\rho \omega^2 r^2}{8} [2 - 2\nu] $$

$$ \sigma_\theta(r) - \sigma_r(r) = \frac{(1-\nu)\rho \omega^2 r^2}{4} $$

This simple expression shows that the difference between the hoop and [radial stress](@entry_id:197086) is directly proportional to $(1-\nu)$. As Poisson's ratio increases (i.e., the material becomes more resistant to volume change), the difference between the two [principal stresses](@entry_id:176761) decreases. In the theoretical limit of $\nu \to 0.5$ (the incompressibility limit for an elastic solid), the stress difference does not vanish but approaches a finite value of $\frac{\rho \omega^2 r^2}{8}$. This demonstrates how the material's tendency to deform laterally under stress directly influences the anisotropy of the stress state induced by rotation.