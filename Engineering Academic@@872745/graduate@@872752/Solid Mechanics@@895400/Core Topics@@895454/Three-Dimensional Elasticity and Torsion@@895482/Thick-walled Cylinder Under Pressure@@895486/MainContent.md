## Introduction
The analysis of stresses in a pressurized [thick-walled cylinder](@entry_id:189222) represents a cornerstone problem in solid mechanics, with profound implications for the design of countless engineering components, from high-pressure pipelines and hydraulic actuators to cannon barrels and [nuclear reactor](@entry_id:138776) vessels. While seemingly simple, determining the internal stress distribution is not trivial; the problem is statically indeterminate, meaning that the principles of equilibrium alone are insufficient. A complete solution requires a rigorous application of continuum mechanics, integrating kinematic and constitutive relationships to fully capture the material's response. This article provides a comprehensive exploration of this classic problem, structured to build understanding from fundamental theory to practical application. The first chapter, **Principles and Mechanisms**, develops the celebrated Lamé solution from first principles, dissecting the stress and displacement fields. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates the versatility of this theory by extending it to analyze complex loading, material failure, and its role in diverse fields from materials science to biomechanics. Finally, the **Hands-On Practices** chapter offers practical exercises to reinforce these theoretical concepts. We begin by establishing the fundamental governing equations in an axisymmetric system, laying the groundwork for deriving the complete elastic solution.

## Principles and Mechanisms

This chapter develops the classical theory of elasticity for a [thick-walled cylinder](@entry_id:189222) subjected to axisymmetric pressure. We will begin by establishing the governing equations from first principles—equilibrium, kinematics, and [constitutive relations](@entry_id:186508)—specialized to the [cylindrical coordinate system](@entry_id:266798). We will then derive the celebrated Lamé solution, providing a complete description of the stress and displacement fields. The analysis of this solution will reveal key mechanical behaviors, such as [stress concentration](@entry_id:160987), and will allow for a quantitative comparison with the simplified [membrane theory](@entry_id:184090) used for thin-walled vessels. Finally, we will explore the nuances of applying this two-dimensional solution to three-dimensional problems, discussing the important idealizations of [plane stress and plane strain](@entry_id:172357), and justifying the solution's applicability using Saint-Venant’s principle.

### Governing Equations in an Axisymmetric System

The analysis of a pressurized [thick-walled cylinder](@entry_id:189222) is a canonical problem in [solid mechanics](@entry_id:164042) that beautifully illustrates the application of the fundamental principles of [continuum mechanics](@entry_id:155125). We consider a long, hollow cylinder of inner radius $a$ and outer radius $b$. The loading consists of a uniform [internal pressure](@entry_id:153696) $p_i$ and a uniform external pressure $p_o$. Due to the rotational symmetry of both the geometry and the loading, we can assume the resulting stress and strain fields are also **axisymmetric**, meaning they are independent of the circumferential coordinate $\theta$.

#### Equilibrium

The starting point for any static problem in [solid mechanics](@entry_id:164042) is the [balance of linear momentum](@entry_id:193575), which, in the absence of [body forces](@entry_id:174230), requires that the divergence of the stress tensor be zero: $\nabla \cdot \boldsymbol{\sigma} = \mathbf{0}$. In a [cylindrical coordinate system](@entry_id:266798) $(r, \theta, z)$, this vector equation resolves into three scalar component equations. Under the assumption of axisymmetry ($\partial(\cdot)/\partial\theta = 0$) and for a state where shear stresses are zero ($\sigma_{r\theta} = \sigma_{\theta z} = \sigma_{rz} = 0$), these general equations simplify considerably [@problem_id:2702698].

The [equilibrium equations](@entry_id:172166) in the circumferential ($\theta$) and axial ($z$) directions are identically satisfied ($0=0$ and $\partial\sigma_{zz}/\partial z = 0$, respectively). The only non-trivial equation that remains is the one for radial equilibrium:

$$
\frac{d\sigma_{r}}{dr} + \frac{\sigma_{r} - \sigma_{\theta}}{r} = 0
$$

Here, $\sigma_r$ is the [radial stress](@entry_id:197086) and $\sigma_\theta$ is the circumferential, or **hoop**, stress. This single differential equation contains two unknown stress components, $\sigma_r(r)$ and $\sigma_\theta(r)$. This indicates that the problem is **statically indeterminate**; equilibrium alone is insufficient to determine the stress field. We must therefore introduce kinematic and [constitutive relations](@entry_id:186508).

#### Kinematics: Strain-Displacement Relations

For an axisymmetric deformation without torsion, the displacement of any material point is purely radial and depends only on the initial radial position. We denote this [displacement field](@entry_id:141476) as $u_r = u(r)$. The classical Lamé solution is developed within the framework of **[linear elasticity](@entry_id:166983)**, which presupposes that strains and displacements are small. This **small-strain** assumption allows for the use of linearized [strain-displacement relations](@entry_id:173321). In cylindrical coordinates, the non-zero strain components are the radial strain $\epsilon_r$ and the [hoop strain](@entry_id:174548) $\epsilon_\theta$:

$$
\epsilon_r = \frac{du}{dr}, \qquad \epsilon_\theta = \frac{u(r)}{r}
$$

The radial strain, $\epsilon_r$, measures the stretching of a material element in the radial direction, while the [hoop strain](@entry_id:174548), $\epsilon_\theta$, measures the fractional change in circumference. The existence of a single-valued, continuous displacement function $u(r)$ ensures that the derived strains are **compatible**—that is, they describe a physically possible deformation without creating gaps or overlaps in the material.

It is crucial to distinguish this from **finite-strain** kinematics, which would be required if pressures were large enough to cause displacements comparable to the cylinder's radius. In a finite-strain context, the [hoop strain](@entry_id:174548) would be described by more [complex measures](@entry_id:184377), such as the [logarithmic strain](@entry_id:751438) $\ln(1 + u/r)$. The classical Lamé solution, however, is strictly a small-strain formulation [@problem_id:2702768].

#### Constitutive Law: Hooke's Law

The final component required is a [constitutive law](@entry_id:167255) that relates stress to strain. For a homogeneous, isotropic, and linearly elastic material, this relationship is given by the generalized Hooke's Law. In [cylindrical coordinates](@entry_id:271645), the normal stresses are related to the normal strains by:

$$
\epsilon_r = \frac{1}{E} [ \sigma_r - \nu (\sigma_\theta + \sigma_z) ]
$$

$$
\epsilon_\theta = \frac{1}{E} [ \sigma_\theta - \nu (\sigma_r + \sigma_z) ]
$$

$$
\epsilon_z = \frac{1}{E} [ \sigma_z - \nu (\sigma_r + \sigma_\theta) ]
$$

Here, $E$ is the Young's modulus, $\nu$ is the Poisson's ratio, and $\sigma_z$ is the axial stress. These equations can be inverted to express stresses in terms of strains. The specific form of these inverted relations depends on the assumptions made about the axial dimension, a topic we will explore in detail later in this chapter [@problem_id:2702700].

### The Lamé Solution for Stress and Displacement

With the three pillars of equilibrium, [kinematics](@entry_id:173318), and constitutive law in place, we can now solve for the stress and displacement fields.

#### Boundary Conditions

First, we must translate the physical application of pressure into mathematical boundary conditions. A fluid pressure $p$ exerts a traction (force per unit area) on a solid surface that is compressive and normal to that surface. By Cauchy's traction theorem, the traction vector $\mathbf{t}$ on a surface with outward unit normal $\mathbf{n}$ is given by $\mathbf{t} = \boldsymbol{\sigma} \cdot \mathbf{n}$. The traction exerted by the pressure is $\mathbf{t} = -p\mathbf{n}$.

For the [thick-walled cylinder](@entry_id:189222), we must be careful with the direction of the outward normal of the solid.
- At the inner surface (bore) $r=a$, the outward normal of the solid points into the cavity, so $\mathbf{n}(a) = -\mathbf{e}_r$.
- At the outer surface $r=b$, the outward normal of the solid points away from the cylinder, so $\mathbf{n}(b) = +\mathbf{e}_r$.

Applying the pressure boundary condition at both surfaces yields [@problem_id:2925533]:
- At $r=a$: $\boldsymbol{\sigma} \cdot (-\mathbf{e}_r) = -p_i(-\mathbf{e}_r)$. Projecting onto the radial direction gives $\sigma_r(a) = -p_i$.
- At $r=b$: $\boldsymbol{\sigma} \cdot (+\mathbf{e}_r) = -p_o(+\mathbf{e}_r)$. Projecting onto the radial direction gives $\sigma_r(b) = -p_o$.

Note the negative signs, which arise because we adopt the standard convention that tensile stresses are positive, while pressure is inherently compressive.

#### Derivation and General Form of the Solution

By substituting the kinematic relations into the [constitutive law](@entry_id:167255), and then substituting the resulting stress expressions into the [equilibrium equation](@entry_id:749057), one obtains a single governing differential equation for the [displacement field](@entry_id:141476) $u(r)$. For the case of plane strain ($\epsilon_z = 0$, a common idealization), this procedure leads to a Cauchy-Euler equation of the form [@problem_id:2702700]:

$$
r^2 \frac{d^2u}{dr^2} + r \frac{du}{dr} - u = 0
$$

The general solution to this equation is:

$$
u(r) = C_1 r + \frac{C_2}{r}
$$

where $C_1$ and $C_2$ are constants of integration. This elegant form reveals that the radial displacement is a superposition of two terms: a term proportional to $r$, which corresponds to a uniform scaling of the cylinder's cross-section, and a term proportional to $1/r$.

Having found the displacement field, we can now determine the strains and, subsequently, the stresses. Differentiating $u(r)$ gives the strains:
$$
\epsilon_r = C_1 - \frac{C_2}{r^2}, \qquad \epsilon_\theta = C_1 + \frac{C_2}{r^2}
$$
Substituting these into the inverted Hooke's law (e.g., for plane strain) yields expressions for the radial and hoop stresses. Regardless of the specific axial constraint (plane strain or plane stress), the stresses invariably take the following general form, known as the **Lamé equations**:

$$
\sigma_r(r) = A - \frac{B}{r^2}
$$

$$
\sigma_\theta(r) = A + \frac{B}{r^2}
$$

The constants $A$ and $B$ are related to the displacement constants $C_1$ and $C_2$ through the material properties. For instance, under plane strain conditions, it can be shown that $C_1 = \frac{A(1+\nu)(1-2\nu)}{E}$ and $C_2 = \frac{B(1+\nu)}{E}$ [@problem_id:2702726].

Applying the boundary conditions $\sigma_r(a) = -p_i$ and $\sigma_r(b) = -p_o$ to the expression for $\sigma_r(r)$ allows us to solve for $A$ and $B$:

$$
A = \frac{p_i a^2 - p_o b^2}{b^2 - a^2}
$$

$$
B = \frac{(p_i - p_o) a^2 b^2}{b^2 - a^2}
$$

With these constants determined, the stress and displacement fields are fully specified. One of the remarkable features of the Lamé solution is that the stress field for this problem is independent of the material's elastic properties ($E$ and $\nu$). However, the displacement field, which depends on $C_1$ and $C_2$, is not.

### Analysis and Interpretation

The Lamé equations provide a complete picture of the mechanical state within the cylinder wall. A careful analysis of these equations reveals critical design insights.

#### Stress Distribution and Concentration

Let's consider the common case of [internal pressure](@entry_id:153696) only ($p_i > 0, p_o = 0$). In this scenario, both constants $A$ and $B$ are positive.
- The [radial stress](@entry_id:197086) $\sigma_r(r) = A - B/r^2$ is always compressive (or zero). It is most compressive at the inner surface, with $\sigma_r(a) = -p_i$, and becomes zero at the outer surface, $\sigma_r(b) = 0$, as required by the boundary conditions.
- The [hoop stress](@entry_id:190931) $\sigma_\theta(r) = A + B/r^2$ is always tensile. Because the $B/r^2$ term is positive and decreases as $r$ increases, the [hoop stress](@entry_id:190931) is always greatest where the radius is smallest.

This leads to a crucial conclusion: for a cylinder under internal pressure, the **maximum [hoop stress](@entry_id:190931) occurs at the inner surface**, $r=a$ [@problem_id:2702740]. Its value is:

$$
\sigma_{\theta, \max} = \sigma_\theta(a) = A + \frac{B}{a^2} = \frac{p_i(a^2 + b^2)}{b^2 - a^2}
$$

This phenomenon, where stress is highest at the inner radius, is a form of **[stress concentration](@entry_id:160987)**. As the wall becomes thicker (i.e., $b/a$ increases), the maximum [hoop stress](@entry_id:190931) at the inner surface approaches a limiting value of $p_i$, while the [hoop stress](@entry_id:190931) at the outer surface approaches zero. This indicates that adding material to the outside of a very thick cylinder does little to reduce the peak stress at the bore.

#### Comparison with Thin-Walled Membrane Theory

For cylinders where the wall thickness $t = b - a$ is small compared to the radius, a simplified model known as **[membrane theory](@entry_id:184090)** is often used. This theory makes two key assumptions based on the cylinder's "thinness":
1. The [radial stress](@entry_id:197086) $\sigma_r$ is negligible compared to the hoop stress $\sigma_\theta$.
2. The [hoop stress](@entry_id:190931) $\sigma_\theta$ is approximately uniform across the wall thickness.

Under these assumptions, the problem becomes statically determinate. A simple [force balance](@entry_id:267186) on a half-cylinder section yields the membrane hoop stress $\sigma_m$:

$$
\sigma_m = \frac{p_i a}{t}
$$

The Lamé solution allows us to precisely quantify when these assumptions are valid [@problem_id:2925571]. We can assess the error introduced by the membrane assumptions by comparing them to the "exact" elasticity solution. For the case of [internal pressure](@entry_id:153696) only, the magnitude of the [radial stress](@entry_id:197086) is at most $p_i$. The variation in [hoop stress](@entry_id:190931) across the wall is $\Delta\sigma_\theta = \sigma_\theta(a) - \sigma_\theta(b) = p_i$.

By comparing these quantities to the characteristic stress scale of the [membrane theory](@entry_id:184090), $\sigma_m = p_i a/t$, we find that the relative errors associated with both assumptions scale with the dimensionless parameter $t/a$:

$$
\frac{|\sigma_r|_{\max}}{\sigma_m} = \frac{p_i}{p_i a / t} = \frac{t}{a} \qquad \text{and} \qquad \frac{\Delta\sigma_\theta}{\sigma_m} = \frac{p_i}{p_i a / t} = \frac{t}{a}
$$

A common engineering rule of thumb considers [membrane theory](@entry_id:184090) to be acceptable if the error is within approximately 10%. This leads to the quantitative criterion for a "thin" wall [@problem_id:2702720]:

$$
\frac{t}{a} \le 0.1 \quad \text{or} \quad \frac{b}{a} \le 1.1
$$

If this condition is not met, the cylinder must be treated as "thick-walled," and the full Lamé solution is required for an accurate analysis.

### Axial Constraints and Three-Dimensional Effects

The solution derived thus far is two-dimensional, assuming the fields do not vary along the cylinder's axis $z$. This is a powerful idealization, but its application to real, finite-length cylinders requires careful consideration of the axial boundary conditions.

#### Plane Strain vs. Plane Stress

For a long cylinder with uniform loading, the state of strain far from the ends will be independent of the axial coordinate $z$. This leads to a state of **[generalized plane strain](@entry_id:182960)**, where the [axial strain](@entry_id:160811) $\epsilon_z$ is a constant. The value of this constant is determined by the specific axial constraints on the cylinder. Two special cases are of particular importance [@problem_id:2702758]:

1.  **Plane Strain**: If the cylinder is very long and fixed at its ends by rigid, immovable platens, it cannot expand or contract axially. This physical constraint imposes the mathematical condition $\boldsymbol{\epsilon_z = 0}$. From Hooke's Law, this requires the presence of a non-zero axial stress to suppress the Poisson effect:
    $$
    \sigma_z = \nu(\sigma_r + \sigma_\theta) = 2\nu A
    $$
    This axial stress is uniform across the wall section and is sustained by reaction forces from the end constraints.

2.  **Plane Stress**: If the cylinder is free to expand or contract axially and no force is applied to its ends (an "open-ended" condition), then the net axial force on any cross-section must be zero. This requires the axial stress to be zero everywhere, $\boldsymbol{\sigma_z = 0}$. In this case, there will be a corresponding [axial strain](@entry_id:160811) due to the Poisson effect:
    $$
    \epsilon_z = -\frac{\nu}{E}(\sigma_r + \sigma_\theta) = -\frac{2\nu A}{E}
    $$
    This condition is a good approximation for a thin slice of a long, unconstrained cylinder.

A common scenario, the **closed-end cylinder**, where internal pressure acts on end caps, fits neither of these idealizations. The pressure on the end caps creates an axial tensile force that must be balanced by a uniform axial stress $\sigma_z = p_i a^2 / (b^2 - a^2)$. Since both $\sigma_z$ and $\epsilon_z$ are non-zero, this is a case of [generalized plane strain](@entry_id:182960).

#### Applicability to Finite-Length Cylinders: Saint-Venant's Principle

The Lamé solution is formally derived for an infinitely long cylinder. How, then, can it be applied to a real cylinder of finite length $L$? The justification lies in **Saint-Venant's principle**.

Consider a finite-length, closed-end cylinder. The exact distribution of forces where the end caps are joined to the cylinder wall is complex and creates a fully three-dimensional stress state near the ends. However, Saint-Venant's principle states that if we replace this complex force distribution with a simpler, **statically equivalent** one, the effect of this change on the stress field is localized. The "statically equivalent" load for a closed-end cylinder is a uniform axial stress $\bar{\sigma}_z$ that produces the same total axial force as the pressure on the end caps.

The difference between the actual end loading and this equivalent uniform stress is a **self-equilibrated** force system. According to the principle, the stresses produced by such a system decay rapidly with distance from the region of application. The [characteristic decay length](@entry_id:183295) is on the order of the cylinder's largest cross-sectional dimension (e.g., the outer radius $b$).

Therefore, in a cylinder that is sufficiently long compared to its radius ($L \gg b$), there is a large central region "far from the ends" where the localized end effects are negligible. In this interior region, the stress state is accurately described by the [generalized plane strain](@entry_id:182960) solution: the Lamé field for $\sigma_r(r)$ and $\sigma_\theta(r)$, augmented by the uniform axial stress $\sigma_z = p_i a^2 / (b^2 - a^2)$ [@problem_id:2702762]. This powerful principle allows us to use an elegant, idealized two-dimensional solution to accurately predict the state of stress in a significant portion of a real-world, three-dimensional component.