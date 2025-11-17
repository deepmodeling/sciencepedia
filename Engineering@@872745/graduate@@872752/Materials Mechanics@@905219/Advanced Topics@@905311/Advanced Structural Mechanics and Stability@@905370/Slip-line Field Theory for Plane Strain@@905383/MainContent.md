## Introduction
In the realm of [materials mechanics](@entry_id:189503), understanding the behavior of ductile metals under large, permanent deformation is paramount for designing robust structures and efficient manufacturing processes. While elastic analysis describes a material's initial response, it falls short when plastic flow begins to dominate. Slip-line field theory emerges as a powerful analytical framework specifically developed to tackle these complex scenarios under plane strain conditions. It provides a bridge between abstract plasticity principles and tangible engineering solutions, addressing the challenge of predicting stress and velocity fields in fully plastic regions. This article will guide you through this classic yet potent theory. The "Principles and Mechanisms" chapter will establish the foundational concepts, from the [rigid-perfectly plastic](@entry_id:195711) material model to the derivation of Hencky’s equations. Following this, the "Applications and Interdisciplinary Connections" chapter will demonstrate the theory's use in solving practical problems like indentation and extrusion, while also linking it to the broader principles of [limit analysis](@entry_id:188743). Finally, the "Hands-On Practices" section offers guided problems to translate theoretical knowledge into practical analytical skill. We begin by exploring the core principles that make this theory a cornerstone of plasticity analysis.

## Principles and Mechanisms

This chapter delineates the fundamental principles and mathematical mechanisms that constitute [slip-line field theory](@entry_id:181917). We will begin by establishing the idealizations concerning the material and deformation state that render the problem tractable. Subsequently, we will formulate the governing equations by combining principles of static equilibrium with appropriate [yield criteria](@entry_id:178101). The analysis will reveal the profound connection between the physical concept of slip-lines and the mathematical characteristics of the governing equations, culminating in the derivation of Hencky's equations, the primary tool for solving problems with this theory.

### Idealizations of Plane Strain Plastic Flow

Slip-line [field theory](@entry_id:155241) is built upon a set of simplifying assumptions that capture the essential physics of large plastic deformation in ductile metals while maintaining mathematical tractability.

#### The Rigid-Perfectly Plastic Material Model

The first idealization is the **[rigid-perfectly plastic](@entry_id:195711) material model**. This model posits a material that exhibits no deformation whatsoever as long as the stresses within it remain below a certain threshold. When the stress state reaches this threshold—defined by a [yield criterion](@entry_id:193897)—the material flows plastically at a constant stress level. This model has two critical implications:

1.  **Neglect of Elastic Strains**: All elastic deformation is considered to be zero. The material is assumed to be infinitely stiff (rigid) prior to yielding. This is a reasonable approximation for many [metal forming](@entry_id:188560) processes where plastic strains are orders of magnitude larger than elastic strains. A direct consequence is that the material's [elastic constants](@entry_id:146207), such as Young's modulus $E$ and Poisson's ratio $\nu$, play no role in the analysis of the fully plastic region.

2.  **No Work Hardening**: The [yield stress](@entry_id:274513) of the material is assumed to remain constant during plastic flow. This "perfectly plastic" behavior ignores the phenomenon of strain hardening, where a material becomes stronger as it deforms. This idealization is most accurate for materials that have been previously cold-worked to saturation or for deformations occurring at high temperatures where recovery processes mitigate hardening.

Within this framework, regions of a body can exist in one of two states: **rigid**, where the stress is below the yield limit and no deformation occurs, or **plastic**, where the stress is on the yield surface and flow is taking place. Slip-line field theory is the study of these plastic regions.

#### Kinematic and Static Conditions of Plane Strain

The second core idealization is that of **plane strain deformation**. This is a kinematic constraint that confines all material movement to a single plane, which we will take as the $xy$-plane. For this to occur, the [displacement field](@entry_id:141476) $\mathbf{u}$ must be of the form $u_x = u_x(x,y)$, $u_y = u_y(x,y)$, and the out-of-plane displacement $u_z$ must be zero everywhere.

Based on the [small-strain tensor](@entry_id:754968) definition, $\varepsilon_{ij} = \frac{1}{2}(u_{i,j} + u_{j,i})$, these displacement constraints lead to the following strain conditions:
- The out-of-plane [normal strain](@entry_id:204633) is zero: $\varepsilon_{zz} = \frac{\partial u_z}{\partial z} = 0$.
- The out-of-plane shear strains are zero: $\varepsilon_{xz} = \frac{1}{2}(\frac{\partial u_x}{\partial z} + \frac{\partial u_z}{\partial x}) = 0$ and $\varepsilon_{yz} = \frac{1}{2}(\frac{\partial u_y}{\partial z} + \frac{\partial u_z}{\partial y}) = 0$.

Physically, the plane strain condition is an excellent approximation for the deformation in the central portion of a long, prismatic body subjected to loading that is uniform along its length (the $z$-axis). Examples include the rolling of a wide sheet, the indentation of a large block, or the analysis of a long dam or retaining wall.

A further fundamental property of [metal plasticity](@entry_id:176585) is **[plastic incompressibility](@entry_id:183440)**, meaning the volume of the material is conserved during plastic flow. This is expressed by stating that the trace of the plastic [strain rate tensor](@entry_id:198281), $\dot{\boldsymbol{\varepsilon}}^p$, is zero:
$$ \mathrm{tr}(\dot{\boldsymbol{\varepsilon}}^p) = \dot{\varepsilon}_{xx}^p + \dot{\varepsilon}_{yy}^p + \dot{\varepsilon}_{zz}^p = 0 $$
Since in our idealized model all strain is plastic, and the plane strain condition $\varepsilon_{zz}=0$ must hold for all time (implying $\dot{\varepsilon}_{zz}=0$), the [incompressibility](@entry_id:274914) condition simplifies to:
$$ \dot{\varepsilon}_{xx} + \dot{\varepsilon}_{yy} = 0 $$
It is crucial to distinguish the kinematic constraint of [plane strain](@entry_id:167046) from the static condition of [plane stress](@entry_id:172193). To enforce the condition $\varepsilon_{zz}=0$ against the material's tendency to contract or expand in the $z$-direction (Poisson's effect), a stress is generally required. This is the out-of-plane normal stress, $\sigma_{zz}$, which is generally non-zero. For an isotropic material, the [associated flow rule](@entry_id:201731) dictates that $\sigma_{zz}$ is the intermediate [principal stress](@entry_id:204375), taking the value $\sigma_{zz} = \frac{1}{2}(\sigma_{xx} + \sigma_{yy})$ for a von Mises material.

### Yield Criteria in Plane Strain

To solve for the stress distribution in a deforming body, the equations of static equilibrium must be supplemented by a constitutive law that describes the material's yield behavior. In a [rigid-perfectly plastic](@entry_id:195711) material, this law is the **yield criterion**. For [slip-line field theory](@entry_id:181917), we consider pressure-insensitive criteria, such as the Tresca and von Mises criteria, which are appropriate for ductile metals.

#### The Tresca and von Mises Criteria

The yield behavior is characterized by a single parameter, the **shear yield stress**, denoted by $k$. This parameter is defined as the value of shear stress at which yielding occurs in a state of [simple shear](@entry_id:180497).

The **Tresca [yield criterion](@entry_id:193897)**, also known as the maximum shear stress theory, postulates that yielding occurs when the maximum shear stress at any point, $\tau_{\max}$, reaches the value $k$. In terms of the [principal stresses](@entry_id:176761) $\sigma_1, \sigma_2, \sigma_3$, this is expressed as:
$$ \tau_{\max} = \frac{1}{2} \max(|\sigma_1-\sigma_2|, |\sigma_2-\sigma_3|, |\sigma_3-\sigma_1|) = k $$
This is often written in the form of a [yield function](@entry_id:167970), $f_T(\boldsymbol{\sigma}) = 0$, as:
$$ f_T(\boldsymbol{\sigma}) = \max(|\sigma_1-\sigma_2|, |\sigma_2-\sigma_3|, |\sigma_3-\sigma_1|) - 2k = 0 $$

The **von Mises yield criterion**, or [distortion energy theory](@entry_id:186622), posits that yielding occurs when the second invariant of the [deviatoric stress tensor](@entry_id:267642), $J_2$, reaches a critical value. Calibrating this with the [simple shear](@entry_id:180497) test shows that yielding occurs when $J_2 = k^2$. In terms of [principal stresses](@entry_id:176761), the von Mises [yield function](@entry_id:167970), $f_M(\boldsymbol{\sigma}) = 0$, is:
$$ f_M(\boldsymbol{\sigma}) = \sqrt{J_2} - k = \sqrt{\frac{1}{6} \left[ (\sigma_1 - \sigma_2)^2 + (\sigma_2 - \sigma_3)^2 + (\sigma_3 - \sigma_1)^2 \right]} - k = 0 $$

It is common practice to relate $k$ to the material's yield stress in [uniaxial tension](@entry_id:188287), $\sigma_y$. By analyzing the stress state of a [uniaxial tension test](@entry_id:195375) at yield ($\sigma_1 = \sigma_y, \sigma_2 = \sigma_3 = 0$), we find the following relationships:
- For Tresca: $\sigma_y = 2k$
- For von Mises: $\sigma_y = \sqrt{3}k$

#### Simplification for Plane Strain

A remarkable simplification occurs when these criteria are applied to the plane strain condition. For an [isotropic material](@entry_id:204616), the [associated flow rule](@entry_id:201731) implies that the out-of-plane [principal stress](@entry_id:204375), $\sigma_z$, is intermediate to the two in-plane [principal stresses](@entry_id:176761), $\sigma_x$ and $\sigma_y$. Let the in-plane [principal stresses](@entry_id:176761) be $\sigma_1$ and $\sigma_2$. The intermediate nature of the out-of-plane stress means that the maximum shear stress in the material occurs in the plane of deformation.

Consequently, for both the Tresca and von Mises criteria under these conditions, the governing yield condition for [plane strain](@entry_id:167046) can be expressed in the same mathematical form:
$$ |\sigma_1 - \sigma_2| = 2k $$
While the two criteria are not identical, this common form for [plane strain](@entry_id:167046) analysis, where $k$ is the material's shear yield stress under [plane strain](@entry_id:167046) conditions, is the cornerstone of classical [slip-line field theory](@entry_id:181917). For the Tresca criterion, this is an exact representation. For the von Mises criterion, this form is also exact, with the value of $k$ being related to the uniaxial yield stress $\sigma_y$ as $k = \sigma_y/\sqrt{3}$.

### The Stress Field and its Geometric Representation

With the [equilibrium equations](@entry_id:172166) and the [yield criterion](@entry_id:193897) established, we can now develop a complete description of the stress field.

#### Parameterization of the Stress State

In a two-dimensional plastic zone, the state of stress is defined by three components: $\sigma_{xx}$, $\sigma_{yy}$, and $\tau_{xy}$. We have two [equilibrium equations](@entry_id:172166) and one yield criterion, forming a determined system. It is highly advantageous to re-parameterize the stress state. Instead of three stress components, we can describe the state of stress using just two variables:
1.  The **mean compressive stress**, or hydrostatic pressure, defined as $p = -\frac{1}{2}(\sigma_{xx} + \sigma_{yy})$.
2.  An angle, $\theta$, representing the orientation of the principal stress axes. We define $\theta$ as the angle measured counter-clockwise from the $x$-axis to the direction of the major (most tensile) in-plane [principal stress](@entry_id:204375), $\sigma_1$.

This parameterization has a direct geometric interpretation via **Mohr's circle** for stress. For any point in the plastic zone, the yield condition $|\sigma_1 - \sigma_2| = 2k$ means that the diameter of the Mohr's circle is fixed at $2k$, so its radius is $k$. The center of the circle is the average normal stress, $\frac{1}{2}(\sigma_{xx} + \sigma_{yy})$, which is equal to $-p$.

From the geometry of the Mohr's circle, we can directly write the Cartesian stress components in terms of $p$ and $\theta$:
$$ \sigma_{xx} = -p + k \cos(2\theta) $$
$$ \sigma_{yy} = -p - k \cos(2\theta) $$
$$ \tau_{xy} = k \sin(2\theta) $$
This powerful parameterization automatically satisfies the yield criterion, leaving us with the task of finding the two [scalar fields](@entry_id:151443), $p(x,y)$ and $\theta(x,y)$, that also satisfy equilibrium.

#### Slip-Lines as Directions of Maximum Shear

The concept of **slip-lines** is central to the theory. Physically, these are imaginary lines drawn in the deforming body that are everywhere tangent to the directions of maximum shear stress. From basic [stress analysis](@entry_id:168804), we know that the planes of maximum shear stress are oriented at angles of $\pm 45^{\circ}$ (or $\pm \pi/4$ [radians](@entry_id:171693)) to the principal stress planes.

Since the major principal stress direction makes an angle $\theta$ with the $x$-axis, the two directions of maximum shear will make angles of $\theta + \pi/4$ and $\theta - \pi/4$ with the $x$-axis. The two families of [integral curves](@entry_id:161858) tangent to these directions are the slip-lines. By convention:
-   The family of **$\alpha$-lines** is tangent to the direction at angle $\theta + \pi/4$ from the $x$-axis.
-   The family of **$\beta$-lines** is tangent to the direction at angle $\theta - \pi/4$ from the $x$-axis.

#### Orthogonality of the Slip-Line Families

A fundamental geometric property of the slip-line field is that the two families are always mutually orthogonal. The angle between an $\alpha$-line and a $\beta$-line at any point of intersection is $(\theta + \pi/4) - (\theta - \pi/4) = \pi/2$.

This can also be verified algebraically. The slopes of the lines are $m_\alpha = \tan(\theta + \pi/4)$ and $m_\beta = \tan(\theta - \pi/4)$. Their product is:
$$ m_\alpha m_\beta = \tan\left(\theta + \frac{\pi}{4}\right) \tan\left(\theta - \frac{\pi}{4}\right) = \left(\frac{\tan\theta + 1}{1 - \tan\theta}\right) \left(\frac{\tan\theta - 1}{1 + \tan\theta}\right) = -1 $$
Since the product of their slopes is $-1$, the two families of curves form an orthogonal network throughout the plastic region.

### Hencky's Equations and the Method of Characteristics

The final step is to combine our parameterized stress state with the [equations of equilibrium](@entry_id:193797) to derive the governing equations for $p$ and $\theta$.

#### The Hyperbolic Nature of the Stress Problem

If we substitute the expressions for $\sigma_{xx}$, $\sigma_{yy}$, and $\tau_{xy}$ in terms of $p$ and $\theta$ into the two-dimensional [equilibrium equations](@entry_id:172166) (assuming zero [body forces](@entry_id:174230)),
$$ \frac{\partial \sigma_{xx}}{\partial x} + \frac{\partial \tau_{xy}}{\partial y} = 0 $$
$$ \frac{\partial \tau_{xy}}{\partial x} + \frac{\partial \sigma_{yy}}{\partial y} = 0 $$
we obtain a system of two coupled, first-order, quasi-[linear partial differential equations](@entry_id:171085) (PDEs) for the unknown fields $p(x,y)$ and $\theta(x,y)$.

A detailed [mathematical analysis](@entry_id:139664) of this system reveals that it is of the **hyperbolic** type. This is a profound result. Hyperbolic systems possess special curves in the solution domain, known as **characteristics**, along which information propagates and along which the PDEs can be simplified into ordinary differential equations. For the [plane strain plasticity](@entry_id:201004) problem, these mathematical characteristics are precisely the physical slip-lines. This beautiful correspondence between the physical mechanism of shear and the mathematical structure of the equations is the key to solving problems with this theory.

#### Derivation of the Hencky Relations

We can derive the relations that hold along the characteristics directly. Substituting the parameterized stress expressions into the [equilibrium equations](@entry_id:172166) yields:
$$ \frac{\partial p}{\partial x} + 2k \left( \sin(2\theta)\frac{\partial \theta}{\partial x} - \cos(2\theta)\frac{\partial \theta}{\partial y} \right) = 0 $$
$$ \frac{\partial p}{\partial y} - 2k \left( \cos(2\theta)\frac{\partial \theta}{\partial x} + \sin(2\theta)\frac{\partial \theta}{\partial y} \right) = 0 $$
Through a process known as the [method of characteristics](@entry_id:177800), we seek [linear combinations](@entry_id:154743) of these equations that simplify along specific directions. It can be shown that along a curve whose slope is $dy/dx = \tan(\theta + \pi/4)$ (an $\alpha$-line), the following relationship holds:
$$ dp - 2k \, d\theta = 0 $$
And along a curve whose slope is $dy/dx = \tan(\theta - \pi/4)$ (a $\beta$-line), the relationship is:
$$ dp + 2k \, d\theta = 0 $$
These two ordinary differential equations are known as **Hencky's equations** or the stress relations. They are the cornerstone of [slip-line field theory](@entry_id:181917).

#### Hencky's Theorems

Integrating Hencky's equations along the slip-lines leads to a powerful set of invariants. We can define quantities based on $p$ and $\theta$:

1.  Along any given $\alpha$-line, the quantity $p - 2k\theta$ is constant.
2.  Along any given $\beta$-line, the quantity $p + 2k\theta$ is constant.

These statements are known as **Hencky's theorems**. They provide a practical method for determining the stress state throughout a plastic region. If the values of $p$ and $\theta$ are known along some initial curve, Hencky's theorems allow us to "propagate" this information along the slip-line network to find the stress state at other points. A geometric interpretation of these theorems is that the gradient of the invariant for one family is everywhere parallel to the direction of the other family. This confirms that the invariants are constant only along their designated characteristic family.

In summary, the combination of equilibrium and yield in [plane strain plasticity](@entry_id:201004) leads to a hyperbolic system whose characteristics are the physically intuitive slip-lines. Along these lines, the stress variables $p$ and $\theta$ are linked by the simple ordinary differential relations of Hencky, providing a powerful framework for solving complex problems in plastic deformation.