## Introduction
The bending of beams is a cornerstone of solid mechanics and structural engineering, forming the basis for designing everything from microscopic cantilevers to colossal bridges. Among the various loading scenarios, the state of [pure bending](@entry_id:202969) provides the ideal theoretical foundation from which more complex behaviors can be understood. By isolating the effects of [bending moment](@entry_id:175948) from shear forces, we can derive elegant and powerful relationships that govern stress, strain, and deformation. This article bridges the gap between fundamental theory and advanced application, providing a comprehensive exploration of [pure bending](@entry_id:202969) for the graduate-level student and practicing engineer.

This article systematically builds your understanding across three interconnected chapters. We begin in **Principles and Mechanisms** by deriving the core theory from first principles, establishing the kinematic assumptions and equilibrium conditions that lead to the celebrated [flexure formula](@entry_id:183093). Next, in **Applications and Interdisciplinary Connections**, we extend this foundational model to tackle real-world complexities, including inelastic material behavior, composite structures, time-dependent effects, and stability phenomena. Finally, **Hands-On Practices** will challenge you to apply these concepts to solve practical problems, reinforcing the connection between theoretical knowledge and engineering analysis.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanics governing the behavior of prismatic beams under [pure bending](@entry_id:202969). We will proceed from the [static equilibrium](@entry_id:163498) conditions that define this loading state, through the kinematic assumptions that describe the geometry of deformation, to the final derivation of the [stress and strain](@entry_id:137374) distributions within the beam. The chapter concludes by exploring the boundaries of this classical theory, considering asymmetric bending, the localized effects of load application, and a comparison with more advanced beam models.

### Defining the State of Pure Bending

In the analysis of beams, the internal stress distribution at any cross-section can be resolved into a set of force and moment resultants. For planar bending in the $x-y$ plane, the most significant of these are the transverse **shear force**, $V(x)$, and the **[bending moment](@entry_id:175948)**, $M(x)$. These internal resultants are not independent but are linked through the principles of [static equilibrium](@entry_id:163498).

Consider a differential element of a beam of length $dx$. The equilibrium of forces and moments on this element, in a region with no externally applied distributed transverse load, leads to two fundamental differential relationships [@problem_id:2677803] [@problem_id:2677807]:

1.  **Force Equilibrium**: The sum of vertical forces yields $\frac{dV}{dx} = 0$. This implies that in any segment of a beam not subjected to a distributed load, the shear force $V(x)$ must be constant.

2.  **Moment Equilibrium**: The sum of moments about a point on the element yields $\frac{dM}{dx} = V(x)$. This crucial relationship states that the rate of change of the [bending moment](@entry_id:175948) along the beam's axis is equal to the transverse shear force.

From these two equations, we can precisely define the state of **[pure bending](@entry_id:202969)**. A segment of a beam is said to be in a state of [pure bending](@entry_id:202969) if it is subjected to a constant bending moment, which necessarily implies that the transverse [shear force](@entry_id:172634) is zero throughout that segment. Formally, for a segment between $x=a$ and $x=b$:

Pure Bending $\iff V(x) = 0$ for all $x \in [a, b]$.

From the moment [equilibrium equation](@entry_id:749057), if $V(x) = 0$, then $\frac{dM}{dx} = 0$, which mathematically requires that $M(x)$ be a constant. This state is distinct from the more general case of *non-uniform bending*, where the absence of a distributed load ($q(x)=0$) still results in a constant, but non-zero, shear force ($V(x) = V_0$), leading to a linearly varying bending moment ($M(x) = V_0 x + C$) [@problem_id:2677803].

### Realizing Pure Bending in Practice

While a theoretical idealization, the state of [pure bending](@entry_id:202969) can be closely approximated in practical engineering and laboratory settings. Two common loading arrangements are used to create a region of [pure bending](@entry_id:202969) in a beam [@problem_id:2677834]:

1.  **End Couples**: The canonical example involves applying equal and opposite couples, $M_0$, to the ends of a beam with no other supports or forces. Since there are no transverse forces, a [free-body diagram](@entry_id:169635) of any segment of the beam reveals that the internal [shear force](@entry_id:172634) $V(x)$ must be zero everywhere to maintain vertical equilibrium. Consequently, the internal [bending moment](@entry_id:175948) $M(x)$ must be constant and equal to $M_0$ along the entire span of the beam.

2.  **Four-Point Bending**: A more common experimental setup involves a simply supported beam subjected to two equal and symmetrically placed concentrated loads. Let a beam of span $L$ be supported at its ends, and two forces of magnitude $P$ be applied at a distance $a$ from each support. By symmetry, the support reactions are each equal to $P$. An analysis of the internal forces reveals that the shear force is constant and equal to $P$ in the outer segments (from a support to the first load) but is identically zero ($V(x) = P - P = 0$) in the central segment between the two applied loads. Consequently, this central portion of the beam is in a state of [pure bending](@entry_id:202969), with a constant moment of magnitude $M = P \times a$.

Other common loading cases, such as a [cantilever beam](@entry_id:174096) with an end load or a simply supported beam under a uniform distributed load, do not produce any region of [pure bending](@entry_id:202969), as the shear force is non-zero over any finite interval [@problem_id:2677834].

### Kinematics of Bending: The Strain Distribution

To understand the internal state of the beam, we must first describe its geometry of deformation. The classical theory of bending rests on a fundamental kinematic assumption known as the **Euler-Bernoulli hypothesis**: plane cross-sections that are initially normal to the beam's longitudinal axis remain plane and normal to the deformed longitudinal axis after bending.

In a state of [pure bending](@entry_id:202969), a prismatic beam deforms into a circular arc. Let us define a coordinate $y$ measured from the beam's longitudinal axis, positive upwards. The Euler-Bernoulli hypothesis implies that the axial displacement $u_x$ of any point $(x,y)$ can be expressed as $u_x(x,y) = u_0(x) - y\theta(x)$, where $u_0(x)$ is the axial displacement of the longitudinal axis itself and $\theta(x)$ is the rotation of the cross-section.

The axial [normal strain](@entry_id:204633) is given by the derivative $\varepsilon_x = \frac{\partial u_x}{\partial x}$. Applying this to our [displacement field](@entry_id:141476) gives:
$\varepsilon_x(x,y) = \frac{du_0}{dx} - y\frac{d\theta}{dx}$.

The term $\frac{du_0}{dx}$ represents the [axial strain](@entry_id:160811) of the longitudinal axis. The line of material points within the beam that experiences no [axial strain](@entry_id:160811) is called the **neutral axis**. By definition, $\varepsilon_x = 0$ along this axis. For [pure bending](@entry_id:202969) without any net axial force, we can place our coordinate origin on this axis, so that $y=0$ corresponds to the neutral axis. The inextensibility of this axis means $\frac{du_0}{dx} = 0$.

The term $\frac{d\theta}{dx}$ represents the rate of change of the cross-section's rotation, which defines the curvature of the deformed beam. For small deflections, this is denoted by $\kappa$. Therefore, the strain distribution simplifies to a beautifully simple [linear relationship](@entry_id:267880) [@problem_id:2677784]:

$$ \varepsilon_x(y) = -\kappa y $$

This equation is the kinematic heart of [beam theory](@entry_id:176426). It states that the [axial strain](@entry_id:160811) at any point in the cross-section is directly proportional to its distance $y$ from the neutral axis. The negative sign is a convention indicating that for a [positive curvature](@entry_id:269220) $\kappa$ (beam bends concave up), fibers above the neutral axis ($y>0$) are compressed ($\varepsilon_x  0$), while fibers below it ($y0$) are stretched ($\varepsilon_x  0$).

### Kinetics of Bending: The Flexure Formula

With the strain field established, we can now determine the resulting stress field by incorporating the material's constitutive behavior. For a homogeneous, linearly elastic material obeying **Hooke's Law**, the axial stress $\sigma_x$ is related to the [axial strain](@entry_id:160811) by $\sigma_x = E \varepsilon_x$, where $E$ is the Young's modulus. Substituting our kinematic result, we find that the stress also varies linearly across the cross-section:

$$ \sigma_x(y) = -E \kappa y $$

This stress distribution must be statically equivalent to the internal resultants on the cross-section: a zero axial force $N$ and a pure bending moment $M$.

First, we enforce the condition of zero net axial force [@problem_id:2677759] [@problem_id:2677786]:
$$ N = \int_A \sigma_x dA = \int_A (-E \kappa y) dA = -E \kappa \int_A y dA = 0 $$
Since for non-trivial bending $E \neq 0$ and $\kappa \neq 0$, this equilibrium condition requires that the [first moment of area](@entry_id:184665) about the neutral axis, $\int_A y dA$, must be zero. This is the definition of the **centroidal axis**. Thus, for a homogeneous beam in [pure bending](@entry_id:202969), the neutral axis must pass through the centroid of the cross-section.

Next, we enforce [moment equilibrium](@entry_id:752138). The [internal stress](@entry_id:190887) distribution must produce the internal bending moment $M$. Summing the moments of the differential forces $\sigma_x dA$ about the neutral axis (the z-axis):
$$ M = \int_A (-y) \sigma_x dA = \int_A (-y)(-E \kappa y) dA = E \kappa \int_A y^2 dA $$
The integral $\int_A y^2 dA$ is a purely geometric property of the cross-section known as the **[second moment of area](@entry_id:190571)**, or more colloquially, the area moment of inertia, denoted by $I$. This property quantifies the efficiency with which the area is distributed away from the neutral axis to resist bending [@problem_id:2677824]. The equation becomes:

$$ M = EI\kappa $$

This is the fundamental **[moment-curvature relationship](@entry_id:180260)**. The product $EI$ is called the **[flexural rigidity](@entry_id:168654)** or **flexural stiffness** of the beam, representing the combined material ($E$) and geometric ($I$) resistance to bending deformation.

Finally, we can combine our equations to derive an expression for stress in terms of the applied moment, a quantity an engineer typically knows or can calculate. By substituting $\kappa = M/(EI)$ into the stress equation $\sigma_x = -E\kappa y$, we arrive at the celebrated **[flexure formula](@entry_id:183093)** [@problem_id:2677759]:

$$ \sigma_x(y) = -\frac{My}{I} $$

This formula is a cornerstone of structural mechanics. It allows for the direct calculation of the bending stress at any point within a beam's cross-section. For a positive (sagging) bending moment $M$, fibers above the neutral axis ($y0$) experience negative (compressive) stress, while fibers below the neutral axis ($y0$) experience positive (tensile) stress. The maximum stress magnitudes occur at the extreme fibers, farthest from the neutral axis [@problem_id:2677786].

### Extensions and Limitations of the Theory

The classical theory of [pure bending](@entry_id:202969) provides a powerful and elegant framework, but its application requires an understanding of its underlying assumptions and limitations.

#### Asymmetric Bending

The derivation above assumes bending occurs about a principal axis of the cross-section. If a beam is subjected to [bending moments](@entry_id:202968) that do not align with a principal axis, or if the cross-section itself lacks symmetry, the simple [flexure formula](@entry_id:183093) is insufficient. This is the case of **asymmetric or biaxial bending**.

Let's maintain the coordinate system where the $x$-axis is the longitudinal axis of the beam, and the cross-section lies in the $y-z$ plane. A general bending moment vector $\mathbf{M}$ can be resolved into components $M_y$ and $M_z$. The linear strain assumption still implies a linear stress distribution: $\sigma_x(y,z) = C_1 y + C_2 z$. Enforcing [moment equilibrium](@entry_id:752138) yields:
$M_y = \int_A z \sigma_x dA = C_1 I_{yz} + C_2 I_y$
$M_z = \int_A -y \sigma_x dA = -C_1 I_z - C_2 I_{yz}$
Here, $I_y$, $I_z$ are the second moments of area about the y and z axes, and $I_{yz} = \int_A yz dA$ is the **[product of inertia](@entry_id:193969)**. Solving this system for $C_1$ and $C_2$ and substituting back gives the general formula for bending stress [@problem_id:2677820]:

$$ \sigma_x(y,z) = \frac{(M_y I_z + M_z I_{yz})z - (M_z I_y + M_y I_{yz})y}{I_y I_z - I_{yz}^2} $$

This formula shows that [bending moments](@entry_id:202968) about one axis can induce stresses that vary along the other axis if the [product of inertia](@entry_id:193969) is non-zero. For any cross-section, one can always find a set of orthogonal **principal axes** for which the [product of inertia](@entry_id:193969) is zero ($I_{y'z'} = 0$). If the moments and geometry are expressed in this principal coordinate system $(y', z')$, the formula simplifies to a superposition of two separate bending actions:

$$ \sigma_x(y',z') = \frac{M_{y'}z'}{I_{y'}} - \frac{M_{z'}y'}{I_{z'}} $$

#### The Principle of Saint-Venant

The [flexure formula](@entry_id:183093) $\sigma_x = -My/I$ represents an exact solution to the 3D equations of elasticity only under the very specific condition that the end couples are applied as a traction field that varies linearly with $y$. In any real application, the loads are applied in a different, more concentrated manner.

**Saint-Venant's principle** addresses this discrepancy. It states that the stress field far from the region of load application depends only on the static resultant (the [net force](@entry_id:163825) and moment) of the applied loads, not on the specific details of their distribution. The difference between the actual stress state and the statically equivalent flexure solution is a complex, three-dimensional stress field that decays rapidly with distance from the end. This region of complex stress is a boundary layer whose size is on the order of the characteristic cross-section dimension (e.g., the beam height $h$), not the overall beam length $L$. Therefore, for a slender beam where $L \gg h$, the simple [pure bending](@entry_id:202969) solution is highly accurate throughout the vast interior of the beam, and deviations are confined to small regions near the applied loads [@problem_id:2677792].

#### Comparison with Shear-Deformable Beam Theory

The Euler-Bernoulli theory, with its assumption that [cross-sections](@entry_id:168295) remain normal to the deformed axis, neglects the effects of [transverse shear deformation](@entry_id:176673). **Timoshenko beam theory** is a more refined model that relaxes this constraint, allowing for an average transverse shear angle $\gamma(x)$. This shear angle is related to the [shear force](@entry_id:172634) by the [constitutive law](@entry_id:167255) $k_s G A \gamma(x) = V(x)$, where $k_s G A$ is the shear rigidity.

In the specific case of [pure bending](@entry_id:202969), the internal [shear force](@entry_id:172634) $V(x)$ is identically zero. According to the Timoshenko constitutive law, this forces the shear angle $\gamma(x)$ to be zero everywhere. This means the cross-sections do, in fact, remain normal to the deformed axis. As a result, for the special case of [pure bending](@entry_id:202969), the kinematic distinction of Timoshenko theory vanishes, and its predictions for rotation and displacement become identical to those of the simpler Euler-Bernoulli theory [@problem_id:2677805]. It is also important to note that neither of these 1D beam theories accounts for the out-of-plane deformation of the cross-section known as **warping**, which is a 3D effect.