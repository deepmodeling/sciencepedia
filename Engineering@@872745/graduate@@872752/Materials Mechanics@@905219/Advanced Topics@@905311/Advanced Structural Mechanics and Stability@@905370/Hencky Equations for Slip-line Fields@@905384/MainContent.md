## Introduction
The analysis of large plastic deformations is fundamental to many engineering disciplines, from the design of manufacturing processes like forging and [extrusion](@entry_id:157962) to the assessment of structural integrity and geological stability. While complex numerical methods can provide detailed solutions, a deep understanding of the underlying mechanics is often best achieved through powerful analytical frameworks. Slip-line [field theory](@entry_id:155241) stands as one of the most elegant and effective of these frameworks, offering exact solutions for a wide class of problems involving plastic flow under [plane strain](@entry_id:167046) conditions.

This article provides a comprehensive exploration of [slip-line field theory](@entry_id:181917), focusing on the derivation and application of the celebrated Hencky equations. It addresses the challenge of solving the [non-linear equations](@entry_id:160354) of plasticity by introducing a set of simplifying idealizations—namely, the [rigid-perfectly plastic](@entry_id:195711) material model—that unlock a powerful solution method based on characteristics. Over the course of three chapters, you will gain a thorough understanding of this theory, from its mathematical origins to its practical implementation.

The journey begins in **Principles and Mechanisms**, where we will lay the theoretical groundwork. This chapter derives the governing equations of [plane strain plasticity](@entry_id:201004), introduces the concept of slip-lines as characteristics of the stress field, and culminates in the formulation of the Hencky equations. Next, in **Applications and Interdisciplinary Connections**, we will see the theory in action, applying it to classic problems in [metal forming](@entry_id:188560), such as indentation and [extrusion](@entry_id:157962), and exploring its reach into fields like [geomechanics](@entry_id:175967) and [rotational dynamics](@entry_id:267911). Finally, the **Hands-On Practices** section provides a set of targeted problems designed to solidify your understanding and build practical skills in applying the concepts you have learned. We begin by establishing the fundamental principles upon which this entire methodology is built.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mathematical mechanisms that govern the behavior of [rigid-perfectly plastic](@entry_id:195711) materials under [plane strain](@entry_id:167046) conditions. We will derive the governing equations, explore the geometric structure of the resulting stress fields, and establish the powerful analytical framework known as [slip-line field theory](@entry_id:181917), culminating in the Hencky equations.

### Foundations of Plane Strain Plasticity

The analysis of many metal-forming processes, such as rolling, drawing, and forging, can be greatly simplified by adopting a set of well-justified idealizations. The theory of slip-lines is built upon this foundation.

The primary idealization is the **[rigid-perfectly plastic](@entry_id:195711) material model**. This model assumes that the material does not deform elastically. It remains perfectly rigid until the stress state at a point satisfies a specific [yield criterion](@entry_id:193897). Once yielding occurs, the material flows plastically under a constant stress state, meaning there is no work hardening. This approximation is highly effective for problems involving large plastic deformations, where elastic strains are negligible in comparison to plastic strains.

A second crucial assumption for [metal plasticity](@entry_id:176585) is **[plastic incompressibility](@entry_id:183440)**. The process of [plastic deformation](@entry_id:139726), which occurs via dislocation slip, is volume-preserving to a very high degree of accuracy. Mathematically, this implies that the trace of the plastic [strain-rate tensor](@entry_id:266108), $\dot{\boldsymbol{\varepsilon}}^p$, is zero:
$$ \text{tr}(\dot{\boldsymbol{\varepsilon}}^p) = \dot{\varepsilon}_{11}^p + \dot{\varepsilon}_{22}^p + \dot{\varepsilon}_{33}^p = 0 $$

The third foundational element is the kinematic constraint of **[plane strain](@entry_id:167046)**. In a [plane strain](@entry_id:167046) problem, it is assumed that deformation is confined to a single plane (e.g., the $x-y$ plane), and there is no strain in the out-of-plane direction (the $z$-direction). Within the rigid-plastic framework, this translates to the condition that the out-of-plane plastic strain rate components are zero: $\dot{\varepsilon}_{33}^p = 0$, $\dot{\varepsilon}_{13}^p = 0$, and $\dot{\varepsilon}_{23}^p = 0$.

Under these conditions, the governing [yield criteria](@entry_id:178101) take on a particularly simple and powerful form. For [isotropic materials](@entry_id:170678), both the **von Mises** and **Tresca** [yield criteria](@entry_id:178101), when specialized to the case of [plane strain](@entry_id:167046), reduce to the same fundamental relationship between the in-plane [principal stresses](@entry_id:176761), $\sigma_1$ and $\sigma_2$. It can be shown that for yielding to occur, the difference between the in-plane principal stresses must equal twice the material's yield stress in pure shear, denoted by $k$:
$$ |\sigma_1 - \sigma_2| = 2k $$
This elegant result forms the cornerstone of [slip-line theory](@entry_id:184792). The parameter $k$ is a material constant. It is related to the uniaxial tensile [yield stress](@entry_id:274513), $\sigma_y$, but the specific relationship depends on the chosen [yield criterion](@entry_id:193897) [@problem_id:2891703]. For the Tresca (maximum shear stress) criterion, $k = \sigma_y / 2$. For the von Mises (distortional energy) criterion, the relationship is $k = \sigma_y / \sqrt{3}$. For the remainder of this chapter, we will proceed using the general form $|\sigma_1 - \sigma_2| = 2k$, which is applicable to both criteria in plane strain.

### The Stress Field: Parameterization and Governing Equations

In a two-dimensional problem, the state of stress at a point is generally described by three independent components (e.g., $\sigma_x$, $\sigma_y$, $\tau_{xy}$). However, for a material that has yielded, the yield condition itself provides an additional constraint. This reduces the number of independent unknowns describing the stress state from three to two.

A convenient choice for these two parameters is the **mean stress**, $p$, and the **orientation of the [principal stresses](@entry_id:176761)**, $\theta$. We define the [mean stress](@entry_id:751819) as the average of the in-plane principal stresses:
$$ p = \frac{\sigma_1 + \sigma_2}{2} $$
The orientation $\theta$ is defined as the angle measured counter-clockwise from a fixed reference axis (e.g., the $x$-axis) to the direction of the major principal stress, $\sigma_1$.

Assuming $\sigma_1 \ge \sigma_2$, the yield condition becomes $\sigma_1 - \sigma_2 = 2k$. Combining this with the definition of [mean stress](@entry_id:751819), we can express the [principal stresses](@entry_id:176761) entirely in terms of $p$ and $k$:
$$ \sigma_1 = p + k $$
$$ \sigma_2 = p - k $$

This relationship can be powerfully visualized using **Mohr's circle** for stress [@problem_id:2917593]. For any point in a plastic state, the Mohr's circle representing the in-[plane stress](@entry_id:172193) has its center at the [mean stress](@entry_id:751819), $\sigma = p$, and a constant radius equal to the shear [yield stress](@entry_id:274513), $k$. The Cartesian components of stress $(\sigma_x, \sigma_y, \tau_{xy})$ can be read directly from this circle using the standard [stress transformation](@entry_id:184474) equations, which involve a rotation through an angle of $2\theta$:
$$ \sigma_x = p + k \cos(2\theta) $$
$$ \sigma_y = p - k \cos(2\theta) $$
$$ \tau_{xy} = k \sin(2\theta) $$
This parameterization elegantly embeds the yield criterion into the description of the stress state. The problem of finding the three stress components is now reduced to finding the two [scalar fields](@entry_id:151443), $p(x,y)$ and $\theta(x,y)$.

The final step is to ensure that this stress field satisfies the equations of static equilibrium. In the absence of [body forces](@entry_id:174230), these are:
$$ \frac{\partial \sigma_x}{\partial x} + \frac{\partial \tau_{xy}}{\partial y} = 0 $$
$$ \frac{\partial \tau_{xy}}{\partial x} + \frac{\partial \sigma_y}{\partial y} = 0 $$
Substituting the parameterized expressions for the stress components into these [equilibrium equations](@entry_id:172166) and applying the chain rule (since $p$ and $\theta$ are functions of $x$ and $y$) results in a system of two first-order, quasi-[linear partial differential equations](@entry_id:171085) (PDEs) for $p(x,y)$ and $\theta(x,y)$ [@problem_id:2891724]. A [mathematical analysis](@entry_id:139664) of this system reveals that it is **hyperbolic**. This is a profound result, as it dictates the entire mathematical structure of the solution method.

### Slip-Line Fields and Hencky's Equations

Hyperbolic systems of PDEs are solved using the **[method of characteristics](@entry_id:177800)**. This involves finding families of curves in the solution domain along which the partial differential equations simplify into ordinary differential equations. For the system governing [plane strain plasticity](@entry_id:201004), these [characteristic curves](@entry_id:175176) have a direct and crucial physical meaning: they are the **slip-lines**.

A slip-line represents a direction of maximum shear stress at a point in the material. From basic [stress analysis](@entry_id:168804), we know that the planes of maximum shear stress are oriented at angles of $\pm \pi/4$ (or $\pm 45^\circ$) to the principal stress directions. Since the major principal stress direction is given by the angle $\theta$, the two families of slip-lines, designated as $\alpha$-lines and $\beta$-lines, have tangents oriented at angles $\phi_\alpha$ and $\phi_\beta$ relative to the $x$-axis. We will adopt the following common convention for their definition:
$$ \phi_\alpha = \theta - \frac{\pi}{4} \quad (\text{for } \alpha\text{-lines}) $$
$$ \phi_\beta = \theta + \frac{\pi}{4} \quad (\text{for } \beta\text{-lines}) $$

A fundamental geometric property of the slip-line field follows directly from this definition: the two families of slip-lines are mutually **orthogonal** at every point where they intersect [@problem_id:2917618]. The angle between an $\alpha$-line and a $\beta$-line at any point is $\phi_\beta - \phi_\alpha = (\theta + \pi/4) - (\theta - \pi/4) = \pi/2$. This orthogonality creates a curvilinear grid, often called a Hencky-Prandtl net, which maps out the stress field within the plastic region.

The true power of this framework is revealed when the governing PDEs are rewritten along the slip-lines. Along these [characteristic curves](@entry_id:175176), the system simplifies to two remarkable ordinary differential relations known as **Hencky's stress equations**:

Along an $\alpha$-line:
$$ dp - 2k \, d\theta = 0 \quad \implies \quad p - 2k\theta = \text{constant} $$

Along a $\beta$-line:
$$ dp + 2k \, d\theta = 0 \quad \implies \quad p + 2k\theta = \text{constant} $$

These equations state that as one moves along a specific slip-line, the change in the [mean stress](@entry_id:751819) is directly proportional to the change in the orientation of the principal stresses. The quantities $p - 2k\theta$ and $p + 2k\theta$ are Riemann invariants, each being constant along one family of characteristics.

The Hencky equations also have a beautiful geometric interpretation [@problem_id:2891732]. The term $d\phi_\alpha/ds_\alpha$ represents the curvature of the $\alpha$-line, where $s_\alpha$ is the arc length. Since $\phi_\alpha = \theta - \pi/4$, we have $d\phi_\alpha = d\theta$. The first Hencky equation can thus be rewritten as:
$$ \frac{dp}{ds_\alpha} = 2k \frac{d\theta}{ds_\alpha} = 2k \frac{d\phi_\alpha}{ds_\alpha} $$
This states that the rate of change of [mean stress](@entry_id:751819) along an $\alpha$-line is equal to $2k$ times the curvature of that line. A similar relation holds for $\beta$-lines. This links the geometry of the slip-line field directly to the variation of the stress state.

### Solving Boundary Value Problems

Hencky's equations provide a practical tool for constructing stress fields and solving [boundary value problems](@entry_id:137204) in plasticity. The general procedure is an application of the [method of characteristics](@entry_id:177800).

If the values of $p$ and $\theta$ are known along a boundary curve $\Gamma$ (that is not itself a slip-line), we can determine the stress state at any interior point $P$. The point $P$ is the intersection of a unique $\alpha$-line and a unique $\beta$-line. Let the $\alpha$-line through $P$ intersect the boundary $\Gamma$ at a point $A$, and the $\beta$-line through $P$ intersect $\Gamma$ at a point $B$. The values $(p_A, \theta_A)$ and $(p_B, \theta_B)$ are known from the boundary data.

From Hencky's equations, we know that the Riemann invariants are constant along these lines [@problem_id:2891695]:
- The value of the invariant $p - 2k\theta$ at point $P$ is the same as at point $A$.
- The value of the invariant $p + 2k\theta$ at point $P$ is the same as at point $B$.

This gives a system of two [linear equations](@entry_id:151487) for the two unknowns, $p_P$ and $\theta_P$, at the interior point $P$:
$$ p_P - 2k\theta_P = p_A - 2k\theta_A $$
$$ p_P + 2k\theta_P = p_B + 2k\theta_B $$
Solving this system yields the stress state at $P$:
$$ p_P = \frac{p_A + p_B}{2} + k(\theta_B - \theta_A) $$
$$ \theta_P = \frac{p_B - p_A}{4k} + \frac{\theta_A + \theta_B}{2} $$

For instance, consider a scenario where boundary data is available [@problem_id:2891691]. Let point $A$ on the boundary have $p_A = 500$ MPa and $\theta_A = 0.1$ rad. Let point $B$ on another boundary have $p_B = 560$ MPa and $\theta_B = 0.2$ rad. For a material with $k = 120$ MPa, the mean stress at the interior point $P$ where the corresponding slip-lines intersect would be:
$$ p_P = \frac{500 + 560}{2} + 120(0.2 - 0.1) = 530 + 120(0.1) = 542 \text{ MPa} $$

A particularly important type of slip-line field is the **centered plastic fan** [@problem_id:2646125]. This is a region of [plastic flow](@entry_id:201346) emanating from a [singular point](@entry_id:171198) (often a sharp corner). In a centered fan, one family of slip-lines consists of straight rays passing through the [singular point](@entry_id:171198), while the other family consists of concentric circular arcs. This specific geometry corresponds to a stress state where the mean stress $p$ varies linearly with the [polar angle](@entry_id:175682) $\varphi$ around the [singular point](@entry_id:171198). Specifically, if the $\alpha$-lines are rays and the $\beta$-lines are circles, then $p(\varphi) = p_0 - 2k\varphi$. Conversely, if the $\alpha$-lines are circles and the $\beta$-lines are rays, then $p(\varphi) = p_0 + 2k\varphi$. Centered fans are essential building blocks for constructing complex slip-line fields around geometric discontinuities.

### Kinematics and Non-Uniqueness

While Hencky's equations completely define the stress field, the full solution to a plasticity problem also requires determining the velocity field. The [velocity field](@entry_id:271461) is governed by the [plastic flow rule](@entry_id:189597) and incompressibility, which lead to a set of kinematic relations known as the **Geiringer equations**.

A common misconception is that material must flow along the slip-lines. In reality, **[streamlines](@entry_id:266815)** (curves tangent to the velocity vector) do not generally coincide with slip-lines [@problem_id:2891709]. The velocity vector at a point typically has components along both the $\alpha$ and $\beta$ directions. Coincidence is a special case that occurs only under specific conditions. A [streamline](@entry_id:272773) will coincide with a slip-line if and only if the curvature of the [streamline](@entry_id:272773), $\kappa_s$, is equal to the rate of change of the principal stress orientation, $d\theta/ds$, along that curve. Using Hencky's equations, this geometric condition is equivalent to the stress condition $dp/ds = \pm 2k\kappa_s$. A clear example where coincidence does occur is in homogeneous [simple shear](@entry_id:180497), where [streamlines](@entry_id:266815) are straight lines ($\kappa_s = 0$) and the stress field is uniform ($dp/ds = 0$), satisfying the condition.

Finally, a key feature of [slip-line theory](@entry_id:184792) is the potential for **non-uniqueness** of solutions [@problem_id:2917561]. Because the governing equations are hyperbolic, the uniqueness of a solution is sensitive to the nature of the boundary conditions. If boundary data are incomplete, or if they are prescribed on a boundary that is itself a characteristic (a slip-line), there may be multiple, or even infinitely many, valid slip-line fields that satisfy the given conditions. Furthermore, [geometric singularities](@entry_id:186127), such as sharp corners, can also lead to non-uniqueness. Classic problems like the indentation of a half-space by a flat punch and the [extrusion](@entry_id:157962) of material through a sharp-cornered die are well-known to admit multiple statically and kinematically admissible solutions. These different solutions correspond to the same external loads but predict different [internal flow](@entry_id:155636) patterns, often differing in the size and shape of the "dead-metal" zones of rigid material that form near the tooling. This non-uniqueness is not a flaw in the theory but rather a reflection of the complex physical [bifurcations](@entry_id:273973) that can occur in plastic flow.