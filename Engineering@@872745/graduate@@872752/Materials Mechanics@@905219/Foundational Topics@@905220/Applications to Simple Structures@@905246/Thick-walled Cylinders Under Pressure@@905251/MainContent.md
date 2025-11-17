## Introduction
The design of components capable of withstanding high pressure is a fundamental challenge in mechanical and [structural engineering](@entry_id:152273). Thick-walled cylinders, used as pressure vessels, hydraulic actuators, and high-pressure piping, are ubiquitous in critical applications where failure is not an option. While simplified models exist for thin-walled structures, they become dangerously inaccurate as wall thickness increases, necessitating a more rigorous approach. This article addresses this need by providing a comprehensive analysis of the mechanical behavior of thick-walled cylinders based on the principles of [elasticity theory](@entry_id:203053).

Across the following chapters, you will gain a deep, systematic understanding of this essential topic. We will begin in **Principles and Mechanisms** by deriving the celebrated Lamé equations from the ground up, exploring the governing [equations of equilibrium](@entry_id:193797), kinematics, and constitutive behavior that define the stress and displacement fields. Next, in **Applications and Interdisciplinary Connections**, we will bridge theory and practice by applying these principles to solve real-world problems in [structural integrity](@entry_id:165319), including failure prediction, [fatigue analysis](@entry_id:191624), and advanced manufacturing techniques like autofrettage. Finally, **Hands-On Practices** will provide guided problems to reinforce these concepts, allowing you to build proficiency in analyzing and designing these critical components. This journey starts with the foundational mechanics that govern how these structures respond to pressure.

## Principles and Mechanisms

The analysis of stresses and deformations in thick-walled cylinders under pressure is a cornerstone of engineering design, with applications ranging from pressure vessels and piping in chemical plants to gun barrels and hydraulic actuators. This chapter systematically develops the theoretical framework for understanding the mechanical behavior of such components, starting from the fundamental principles of continuum mechanics and culminating in the celebrated Lamé solution. We will explore not only the derivation of the stress and displacement fields but also the critical role of boundary conditions and the subtleties of different axial constraints.

### The Governing Equations of an Axisymmetric Cylinder

Our analysis begins by considering a long, hollow cylinder of inner radius $a$ and outer radius $b$, made of a homogeneous and isotropic material. When subjected to uniform internal and external pressures, the problem exhibits a high degree of symmetry. If we assume the loading and geometry are identical along the cylinder's length and around its circumference, we can simplify the problem by adopting a [cylindrical coordinate system](@entry_id:266798) $(r, \theta, z)$ and imposing the condition of **axisymmetry**. This powerful assumption stipulates that all field quantities—such as stress and displacement—are independent of the circumferential coordinate $\theta$. Consequently, derivatives with respect to $\theta$ vanish, i.e., $\partial(\cdot)/\partial\theta = 0$.

Under static conditions and in the absence of body forces (like gravity or [electromagnetic forces](@entry_id:196024)), the general three-dimensional [equations of equilibrium](@entry_id:193797), $\nabla \cdot \boldsymbol{\sigma} = \mathbf{0}$, simplify considerably. For an axisymmetric state with no torsion, all shear stress components ($\sigma_{r\theta}$, $\sigma_{\theta z}$, $\sigma_{rz}$) are zero. Applying these conditions to the [equilibrium equations](@entry_id:172166) in cylindrical coordinates reveals that the circumferential ($\theta$) and axial ($z$) equations are identically satisfied (or reduce to trivial statements, like $\partial \sigma_{zz}/\partial z = 0$), leaving a single, non-trivial governing equation for equilibrium in the radial direction [@problem_id:2702698]:

$$
\frac{d\sigma_{r}}{dr} + \frac{\sigma_{r} - \sigma_{\theta}}{r} = 0
$$

Here, $\sigma_{r}$ is the [radial stress](@entry_id:197086) (acting normal to a cylindrical surface) and $\sigma_{\theta}$ is the circumferential or **hoop stress** (acting tangentially around the cylinder). This equation establishes a fundamental relationship between the rate of change of [radial stress](@entry_id:197086) and the difference between the radial and hoop stresses. It is a single equation with two unknown stress fields, $\sigma_r(r)$ and $\sigma_\theta(r)$. This indicates that the problem is **statically indeterminate**; equilibrium alone is insufficient to determine the stresses.

To resolve this indeterminacy, we must introduce two additional sets of principles: [kinematics](@entry_id:173318) (the geometry of deformation) and [constitutive relations](@entry_id:186508) (the material's stress-strain behavior) [@problem_id:2925571].

For the [kinematics](@entry_id:173318), axisymmetry dictates that the displacement must be purely radial. Every point on a given cylindrical surface moves only in the radial direction, and the magnitude of this movement, $u$, depends only on the initial radius $r$. Thus, the displacement field is described by $u_r = u(r)$. Within the framework of **small strain theory**, which is appropriate for most engineering materials below their [elastic limit](@entry_id:186242), the radial and hoop strains ($\epsilon_r$ and $\epsilon_\theta$) are related to the [displacement field](@entry_id:141476) by:

$$
\epsilon_r = \frac{du}{dr}
$$
$$
\epsilon_\theta = \frac{u(r)}{r}
$$

The existence of a single-valued, continuous displacement function $u(r)$ ensures that the resulting strains are **compatible**, meaning they correspond to a physically possible deformation without creating gaps or overlaps in the material [@problem_id:2925571].

Finally, for a **linear elastic [isotropic material](@entry_id:204616)**, the stresses and strains are linearly related through **Hooke's Law**. The specific form of this [constitutive law](@entry_id:167255) will be introduced as we develop the complete solution. It is the mandatory inclusion of both compatibility (via the [displacement field](@entry_id:141476)) and the [constitutive law](@entry_id:167255) that distinguishes this rigorous elasticity solution from simplified models like the [membrane theory](@entry_id:184090) for thin-walled cylinders, which determines stresses from equilibrium alone under highly restrictive geometric assumptions [@problem_id:2925571].

### The Lamé Solution: Structure and Derivation

The complete solution for the stress and displacement fields is obtained by systematically combining the three pillars of [solid mechanics](@entry_id:164042): equilibrium, [kinematics](@entry_id:173318), and [constitutive relations](@entry_id:186508). This process leads to a governing differential equation for the radial displacement $u(r)$.

By expressing the stresses $\sigma_r$ and $\sigma_\theta$ in terms of the strains $\epsilon_r$ and $\epsilon_\theta$ using Hooke's Law, and then substituting the kinematic relations $\epsilon_r = du/dr$ and $\epsilon_\theta = u/r$, we can write the stresses entirely as functions of the displacement $u(r)$ and its derivative. When these expressions are substituted back into the radial [equilibrium equation](@entry_id:749057), we obtain a second-order linear ordinary differential equation for $u(r)$ [@problem_id:2702700]:

$$
\frac{d^2u}{dr^2} + \frac{1}{r}\frac{du}{dr} - \frac{u}{r^2} = 0
$$

This is a form of the **Cauchy-Euler equation**. Its general solution provides the radial displacement field and has the characteristic form:

$$
u(r) = C_1 r + \frac{C_2}{r}
$$

where $C_1$ and $C_2$ are constants of integration. This elegant result shows that the complex deformation of the cylinder can be described as a superposition of two basic modes: a uniform radial expansion (or contraction), proportional to $r$, and a deformation that decays inversely with the radius.

From this [displacement field](@entry_id:141476), we can work backward to find the stresses. By first calculating the strains and then using Hooke's Law, we arrive at the general form of the stress distribution, famously known as the **Lamé equations**:

$$
\sigma_r(r) = A - \frac{B}{r^2}
$$
$$
\sigma_\theta(r) = A + \frac{B}{r^2}
$$

The constants $A$ and $B$ are new constants related to $C_1$ and $C_2$ and the material properties. For example, under the condition of plane strain ($\epsilon_z=0$), it can be shown that the constants are related by $C_1 = \frac{A(1+\nu)(1-2\nu)}{E}$ and $C_2 = \frac{B(1+\nu)}{E}$, where $E$ is Young's modulus and $\nu$ is Poisson's ratio [@problem_id:2702726]. The stress solution is thus a superposition of a constant stress state, $A$, and a stress state that varies as $1/r^2$. Notably, the sum of the radial and hoop stresses is constant across the wall: $\sigma_r + \sigma_\theta = 2A$.

### Solving the Boundary Value Problem

The general solutions for displacement and stress contain unknown constants ($C_1, C_2$ or $A, B$). To find their specific values for a given problem, we must apply **boundary conditions**. Since the governing equation for displacement is a second-order ordinary differential equation, two boundary conditions are required to obtain a unique solution for the radial problem [@problem_id:2925580].

For a cylinder with inner radius $a$ and outer radius $b$ subjected to internal pressure $p_i$ and external pressure $p_o$, these conditions are specified on the traction, or stress, at the surfaces. Pressure acts normal to the surface, corresponding to the [radial stress](@entry_id:197086) component. Adopting the sign convention that tensile stress is positive, the boundary conditions are:

1.  At the inner surface, $r=a$: $\sigma_r(a) = -p_i$
2.  At the outer surface, $r=b$: $\sigma_r(b) = -p_o$

These are known as **natural** or **[traction boundary conditions](@entry_id:167112)**. It is important to recognize that one cannot prescribe the hoop stress $\sigma_\theta$ as a boundary condition, as it is an [internal stress](@entry_id:190887), not a [surface traction](@entry_id:198058). Furthermore, for a [well-posed problem](@entry_id:268832), it is generally inadmissible to prescribe both displacement ($u_r$) and traction ($\sigma_r$) independently on the same boundary surface [@problem_id:2925580].

Applying these two conditions to the general solution for $\sigma_r(r) = A - B/r^2$ gives a system of two linear equations for $A$ and $B$:

$$
A - \frac{B}{a^2} = -p_i
$$
$$
A - \frac{B}{b^2} = -p_o
$$

Solving this system yields the explicit expressions for the Lamé constants [@problem_id:2925624]:

$$
A = \frac{p_i a^2 - p_o b^2}{b^2 - a^2}
$$
$$
B = \frac{(p_i - p_o) a^2 b^2}{b^2 - a^2}
$$

With $A$ and $B$ determined, the stress distribution throughout the cylinder wall is fully defined. This completes the solution to the radial [boundary value problem](@entry_id:138753).

### Stress Analysis and Design Implications

The Lamé equations are not merely a mathematical curiosity; they provide profound insights for engineering design. Of particular interest is the [hoop stress](@entry_id:190931), $\sigma_\theta$, as it is often the largest tensile stress in a [pressure vessel](@entry_id:191906) and thus governs its failure.

Let's analyze the hoop stress distribution: $\sigma_\theta(r) = A + B/r^2$. Consider the common case of a cylinder under [internal pressure](@entry_id:153696) only ($p_i > 0, p_o = 0$), or more generally, where [internal pressure](@entry_id:153696) dominates ($p_i > p_o$). In this scenario, the constant $B$ is positive. Since $B>0$, the term $B/r^2$ is always positive and decreases as the radius $r$ increases. Therefore, the hoop stress $\sigma_\theta(r)$ is a monotonically decreasing function of the radius [@problem_id:2702740].

This leads to a critical conclusion: **For a [thick-walled cylinder](@entry_id:189222) subjected to a net internal pressure, the maximum [hoop stress](@entry_id:190931) always occurs at the inner surface of the cylinder ($r=a$)**. This inner surface is the most critical location for crack initiation and [fatigue failure](@entry_id:202922).

The value of this maximum [hoop stress](@entry_id:190931) can be calculated by substituting $r=a$ into the hoop stress equation, or more simply, by evaluating $\sigma_\theta(a) = A + B/a^2$ using our expressions for $A$ and $B$ [@problem_id:2925624], [@problem_id:2702740]. The result simplifies to:

$$
\sigma_{\theta, \max} = \sigma_\theta(a) = \frac{p_i (a^2 + b^2) - 2p_o b^2}{b^2 - a^2}
$$

For the case of [internal pressure](@entry_id:153696) only ($p_o=0$), this becomes $\sigma_\theta(a) = p_i \frac{a^2 + b^2}{b^2 - a^2}$. Since the geometric factor is always greater than 1, the [hoop stress](@entry_id:190931) at the bore is always greater in magnitude than the internal pressure itself. As the wall becomes thinner ($b \to a$), this [stress concentration](@entry_id:160987) effect becomes dramatically more pronounced, highlighting the danger of applying thin-wall formulas to even moderately thick cylinders.

### The Crucial Role of Axial Constraints

Thus far, our analysis has focused on the radial and circumferential directions. However, the cylinder is a three-dimensional object, and its behavior is also influenced by what happens in the axial ($z$) direction. For a long cylinder, **Saint-Venant's principle** allows us to assume that far from the ends, the state of [stress and strain](@entry_id:137374) is independent of $z$. A rigorous application of the elasticity framework reveals that this implies the [axial strain](@entry_id:160811), $\epsilon_z$, must be constant throughout any given cross-section [@problem_id:2925568]. This condition, $\epsilon_z = \text{constant}$, is known as **[generalized plane strain](@entry_id:182960)**.

The axial stress $\sigma_z$ is related to this strain by Hooke's Law: $\sigma_z = E\epsilon_z + \nu(\sigma_r + \sigma_\theta)$. Since $\sigma_r + \sigma_\theta = 2A$ is a constant, and $\epsilon_z$ is constant, it follows that **the axial stress $\sigma_z$ must be uniform (constant with respect to $r$) across the cylinder wall** in the region far from the ends.

The specific value of this constant $\sigma_z$ (and the corresponding $\epsilon_z$) depends entirely on the axial boundary conditions of the cylinder [@problem_id:2925632], [@problem_id:2925568]. Three primary cases are of interest:

1.  **Open Ends (Plane Stress):** If the cylinder ends are free and carry no axial load (e.g., an open pipe), the net axial force on the wall must be zero. Since $\sigma_z$ is uniform, this implies $\sigma_z = 0$. This condition is known as **plane stress**.

2.  **Fixed Ends (Plane Strain):** If the cylinder is rigidly fixed at its ends, preventing any axial elongation, the [axial strain](@entry_id:160811) must be zero: $\epsilon_z = 0$. This is the condition of **[plane strain](@entry_id:167046)**. This induces a non-zero axial stress $\sigma_z = \nu(\sigma_r + \sigma_\theta) = 2\nu A$ due to the Poisson effect, as the material is prevented from expanding or contracting axially in response to the in-plane stresses.

3.  **Closed Ends:** This case represents a typical pressure vessel with end caps. The pressure acting on the end caps creates a net axial force that must be balanced by the axial stress in the cylinder wall. A global [force balance](@entry_id:267186) shows that the required uniform axial stress is [@problem_id:2925619], [@problem_id:2925568]:
    $$
    \sigma_z = \frac{p_i a^2 - p_o b^2}{b^2 - a^2}
    $$
    This value is, remarkably, identical to the Lamé constant $A$.

A final, subtle, and fundamentally important point must be made. While the axial condition determines the value of $\sigma_z$, does this axial stress influence the radial and hoop stresses, $\sigma_r$ and $\sigma_\theta$? Intuitively, one might expect a Poisson coupling effect. However, a careful examination of the derivation shows that for this specific [boundary value problem](@entry_id:138753) where tractions (pressures) are prescribed, the governing differential equations for $\sigma_r$ and $\sigma_\theta$ are independent of $\sigma_z$. The constant $\sigma_z$ term, when carried through the compatibility and [constitutive relations](@entry_id:186508), cancels out [@problem_id:2925619].

Therefore, **the radial and [hoop stress](@entry_id:190931) distributions, $\sigma_r(r)$ and $\sigma_\theta(r)$, are independent of the axial end conditions of the cylinder.** The formulas we derived for $A$, $B$, $\sigma_r$, and $\sigma_\theta$ are valid for open ends, fixed ends, and closed ends alike. The axial condition does, however, determine the axial stress $\sigma_z$ and the strain components ($\epsilon_r, \epsilon_\theta, \epsilon_z$), making it essential for a complete analysis of the cylinder's deformation and for failure theories that depend on the full three-dimensional stress state, such as the von Mises or Tresca criteria.