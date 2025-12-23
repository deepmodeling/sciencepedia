## Introduction
The successful confinement of a plasma at temperatures exceeding 100 million degrees is the central challenge of magnetic fusion energy. The tokamak, a toroidal device, accomplishes this feat by using a powerful and precisely shaped magnetic field to form a "magnetic bottle." Understanding the physics that governs this magnetic configuration is fundamental to designing, operating, and improving fusion reactors. This article addresses the essential question: how is the plasma held in a stable equilibrium by magnetic forces, and what are the properties of this magnetic cage?

This article provides a comprehensive overview of the principles, applications, and practical calculations related to the tokamak magnetic configuration.
*   The first chapter, **"Principles and Mechanisms"**, delves into the theoretical heart of the topic, deriving the Grad-Shafranov equation from first principles and introducing the core concepts of [magnetic flux surfaces](@entry_id:751623), the safety factor, and the forces that determine the plasma's position.
*   The second chapter, **"Applications and Interdisciplinary Connections"**, bridges theory and practice by exploring how the magnetic configuration dictates magnetohydrodynamic (MHD) stability, [plasma-wall interactions](@entry_id:187149), transport phenomena, and the design of control systems.
*   Finally, **"Hands-On Practices"** presents a series of targeted problems that allow you to apply these concepts to calculate key parameters and build a deeper, quantitative understanding.

We will begin by examining the foundational laws of [magnetostatics](@entry_id:140120) and force balance that give rise to the elegant structure of the [tokamak equilibrium](@entry_id:204576).

## Principles and Mechanisms

The confinement of a high-temperature plasma in a tokamak relies on a carefully structured magnetic field. In an ideal magnetohydrodynamic (MHD) framework, the plasma and magnetic field exist in a stationary equilibrium state, where the outward pressure force of the plasma is precisely balanced by the inward magnetic force. This chapter elucidates the fundamental principles governing this equilibrium magnetic configuration, from the foundational concept of [magnetic flux surfaces](@entry_id:751623) to the macroscopic forces that determine the plasma's position and stability.

### The Grad-Shafranov Equilibrium

The cornerstone of [tokamak equilibrium](@entry_id:204576) theory is the existence of nested [magnetic flux surfaces](@entry_id:751623). These surfaces arise as a direct consequence of the fundamental laws of [magnetostatics](@entry_id:140120) coupled with the toroidal symmetry of the tokamak device. The governing equations for a static, ideal MHD equilibrium are the force balance equation, Ampere's law, and the [solenoidal constraint](@entry_id:755035) on the magnetic field:

$\nabla p = \mathbf{J} \times \mathbf{B}$

$\nabla \times \mathbf{B} = \mu_0 \mathbf{J}$

$\nabla \cdot \mathbf{B} = 0$

Here, $p$ is the scalar plasma pressure, $\mathbf{J}$ is the electric current density, and $\mathbf{B}$ is the magnetic field.

In an axisymmetric system, such as an idealized tokamak, all physical quantities are independent of the toroidal angle, $\phi$. Expressed in [cylindrical coordinates](@entry_id:271645) $(R, \phi, Z)$, this symmetry implies $\partial/\partial\phi = 0$. Under this condition, the [divergence-free](@entry_id:190991) nature of the magnetic field, $\nabla \cdot \mathbf{B} = 0$, simplifies to:

$$
\frac{1}{R}\frac{\partial (RB_R)}{\partial R} + \frac{\partial B_Z}{\partial Z} = 0
$$

This equation states that the vector field $(RB_R, RB_Z)$ in the poloidal $(R, Z)$ plane is divergenceless. For any such two-dimensional vector field, we can define a scalar [stream function](@entry_id:266505), which in this context is known as the **[poloidal magnetic flux](@entry_id:1129914) function**, $\psi(R, Z)$. It is defined such that its derivatives give the poloidal magnetic field components:

$$
B_R = -\frac{1}{R}\frac{\partial \psi}{\partial Z} \quad \text{and} \quad B_Z = \frac{1}{R}\frac{\partial \psi}{\partial R}
$$

A crucial property emerges directly from this definition. The dot product of the magnetic field and the gradient of the flux function is identically zero:

$$
\mathbf{B} \cdot \nabla\psi = (B_R \hat{\mathbf{R}} + B_Z \hat{\mathbf{Z}}) \cdot \left(\frac{\partial \psi}{\partial R} \hat{\mathbf{R}} + \frac{\partial \psi}{\partial Z} \hat{\mathbf{Z}}\right) = \left(-\frac{1}{R}\frac{\partial \psi}{\partial Z}\right)\frac{\partial \psi}{\partial R} + \left(\frac{1}{R}\frac{\partial \psi}{\partial R}\right)\frac{\partial \psi}{\partial Z} = 0
$$

This mathematical identity has a profound physical meaning: magnetic field lines are everywhere tangent to the surfaces of constant $\psi$. These surfaces, $\psi(R, Z) = \text{constant}$, are the **magnetic flux surfaces**. Due to axisymmetry, each surface forms a nested torus. 

The MHD [force balance](@entry_id:267186) equation imposes further constraints. Taking the dot product of $\nabla p = \mathbf{J} \times \mathbf{B}$ with $\mathbf{B}$ yields $\mathbf{B} \cdot \nabla p = 0$. This implies that the plasma pressure $p$ must be constant along a magnetic field line. Since magnetic field lines in a tokamak are generally ergodic, densely covering a flux surface, the pressure must be constant over the entire surface. Consequently, pressure is a function of $\psi$ alone: $p = p(\psi)$. A similar argument, stemming from the $\phi$-component of the force balance equation, demonstrates that the quantity $F = R B_\phi$ is also a flux function: $F = F(\psi)$.  

By substituting the expressions for $\mathbf{B}$ and $\mathbf{J}$ (from Ampere's law) into the [force balance](@entry_id:267186) equation, all terms can be expressed in terms of $\psi$ and its derivatives. This process culminates in a single, powerful partial differential equation for the poloidal flux function, known as the **Grad-Shafranov (GS) equation**:

$$
R \frac{\partial}{\partial R}\left(\frac{1}{R}\frac{\partial \psi}{\partial R}\right) + \frac{\partial^2 \psi}{\partial Z^2} = - \mu_0 R^2 \frac{dp}{d\psi} - F \frac{dF}{d\psi}
$$

The operator on the left, $\Delta^* \equiv R \frac{\partial}{\partial R}(\frac{1}{R}\frac{\partial}{\partial R}) + \frac{\partial^2}{\partial Z^2}$, is the Grad-Shafranov operator. The terms on the right-hand side are the sources that determine the equilibrium structure. The term involving $dp/d\psi$ represents the effect of the pressure-driven [diamagnetic current](@entry_id:201627), while the term involving $F dF/d\psi$ represents the effect of the poloidal current that modifies the [toroidal magnetic field](@entry_id:756057). The GS equation demonstrates that for given pressure and poloidal current profiles, $p(\psi)$ and $F(\psi)$, the magnetic equilibrium configuration is uniquely determined, subject to boundary conditions. Inversely, a given flux surface geometry $\psi(R,Z)$ uniquely determines the necessary source profiles required to sustain it. 

### Topological Features of the Magnetic Configuration

The solutions to the Grad-Shafranov equation describe the topology of the magnetic field in the poloidal plane. The level sets of the function $\psi(R,Z)$ define the [magnetic flux surfaces](@entry_id:751623). The geometry of these surfaces is determined by the [critical points](@entry_id:144653) of $\psi$, where the [poloidal magnetic field](@entry_id:753563) vanishes. A critical point is defined by the condition $\nabla\psi = \mathbf{0}$.

The nature of a critical point is determined by the Hessian matrix of second derivatives of $\psi$:
$$
H = \begin{pmatrix} \frac{\partial^2\psi}{\partial R^2} & \frac{\partial^2\psi}{\partial R \partial Z} \\ \frac{\partial^2\psi}{\partial Z \partial R} & \frac{\partial^2\psi}{\partial Z^2} \end{pmatrix}
$$

There are two primary types of [critical points](@entry_id:144653) relevant to tokamak equilibria:

1.  **O-point**: A critical point that is a [local minimum](@entry_id:143537) or maximum of $\psi$. Here, the eigenvalues of the Hessian matrix have the same sign, and its determinant is positive ($\det(H) > 0$). An O-point corresponds to the **magnetic axis**, a single flux surface that is a line running in the toroidal direction. It forms the center of the nested toroidal flux surfaces that constitute the confined plasma.

2.  **X-point**: A critical point that is a saddle point of $\psi$. Here, the Hessian has one positive and one negative eigenvalue, and its determinant is negative ($\det(H) < 0$).  The flux surfaces in the vicinity of an X-point have a hyperbolic, crossed shape.

The special flux surface that passes through an X-point is called a **separatrix**. The [separatrix](@entry_id:175112) is of immense practical importance as it defines the boundary between different topological regions. In a diverted tokamak, the [separatrix](@entry_id:175112) separates the core confined plasma from the "[scrape-off layer](@entry_id:182765)," where field lines are open and terminate on material surfaces called divertor plates. The last closed flux surface (LCFS) is either the [separatrix](@entry_id:175112) itself or the last surface before the plasma touches a material limiter.

### Characterizing the Helical Field Lines: Safety Factor and Rotational Transform

While flux surfaces describe the nested toroidal structure, a complete picture requires characterizing the helical path of individual magnetic field lines upon these surfaces. This is quantified by two related parameters: the safety factor and the rotational transform.

The **safety factor**, denoted by $q(\psi)$, is defined as the number of times a magnetic field line transits in the toroidal direction for every one transit in the poloidal direction. It measures the pitch of the helical field lines. A high $q$ value corresponds to a field line that is mostly toroidal, while a low $q$ value indicates a more tightly wound helix. Mathematically, it is the derivative of the toroidal flux, $\Phi$, with respect to the [poloidal flux](@entry_id:753562), $\psi$:

$$
q(\psi) = \frac{d\Phi}{d\psi} = \frac{1}{2\pi} \oint_{\psi} \frac{B_\phi}{R B_p} dl_p
$$

where the integral is taken along a poloidal contour $dl_p$ on the flux surface $\psi$.

Conversely, the **[rotational transform](@entry_id:200017)**, $\iota(\psi)$, is defined as the number of poloidal turns per toroidal turn. It is simply the reciprocal of the safety factor :

$$
\iota(\psi) = \frac{1}{q(\psi)}
$$

The [safety factor profile](@entry_id:1131171), $q(\psi)$, is a fundamental property of a [tokamak equilibrium](@entry_id:204576). Typically, $q$ is just below 1 on the magnetic axis ($q_0 \approx 0.9$) and increases monotonically towards the plasma edge. For example, a plausible profile might be modeled by a polynomial in $\psi$, such as $q(\psi) = q_0 + a\psi + b\psi^2$. 

Flux surfaces where $q$ is a rational number, $q = m/n$ (with integers $m, n$), are called **rational surfaces**. On these surfaces, a magnetic field line closes back on itself after $m$ toroidal turns and $n$ poloidal turns. These surfaces are particularly sensitive to [resonant magnetic perturbations](@entry_id:754290) and are often the location where magnetohydrodynamic (MHD) instabilities, such as [tearing modes](@entry_id:194294), can grow.

A critical feature of diverted tokamaks is the behavior of $q$ near the [separatrix](@entry_id:175112). As a flux surface approaches the X-point on the [separatrix](@entry_id:175112), the poloidal field strength $B_p = |\nabla\psi|/R$ goes to zero. From the integral definition of $q$, it is clear that the integrand diverges, causing the safety factor to become infinite at the [separatrix](@entry_id:175112). A more detailed analysis shows that as the separatrix is approached from within the confined region ($\psi \to \psi_X^-$), the safety factor diverges logarithmically with the flux difference, $q \propto -\ln(\psi_X - \psi)$. This implies that the shear, $dq/d\psi$, diverges as $1/(\psi_X-\psi)$, a key characteristic that strongly influences edge plasma stability and transport. 

### Global Force Balance and Radial Equilibrium

While the Grad-Shafranov equation describes the local force balance at every point within the plasma, we can also consider the global forces acting on the plasma torus as a whole. The [toroidal plasma](@entry_id:202484), carrying a large current $I_p$, behaves like a current loop that tends to expand. This outward force, known as the **hoop force**, has two main components: an [electromagnetic force](@entry_id:276833) from the current itself (parallel currents repel) and a kinetic force from the plasma pressure acting like an inflated tire tube.

To quantify these effects, two [dimensionless parameters](@entry_id:180651) are essential:

*   **Poloidal Beta ($\beta_p$)**: This parameter compares the average plasma kinetic pressure to the magnetic pressure of the [poloidal field](@entry_id:188655) at the edge. It is a measure of the efficiency of magnetic confinement.
    $$
    \beta_p = \frac{\langle p \rangle}{B_p(a)^2 / (2\mu_0)}
    $$
    where $\langle p \rangle$ is the volume-averaged pressure and $B_p(a)$ is the poloidal field at the plasma edge (minor radius $r=a$).

*   **Normalized Internal Inductance ($l_i$)**: This parameter characterizes the shape of the toroidal current [density profile](@entry_id:194142), $j_\phi(r)$. It represents the poloidal magnetic energy stored within the plasma, normalized to the value it would have if all current flowed on the surface.
    $$
    l_i = \frac{\langle B_p^2 \rangle}{B_p(a)^2}
    $$
    A peaked current profile (high current on-axis) leads to a larger value of $l_i$, while a flat or hollow profile leads to a smaller value. For instance, a flat current profile $j_\phi(r) = j_0$ yields $l_i=0.5$, whereas a specific hollow profile like $j_\phi(r) \propto (r/a)(1-r/a)$ gives $l_i \approx 0.73$.  

For a large-aspect-ratio tokamak ($R_0 \gg a$), the total outward force per unit length in the major radius direction is given by the famous **Shafranov formula** for the force per unit toroidal angle, $F'_H$:

$$
F'_H = \frac{\mu_0 I_p^2}{4\pi} \left( \ln\frac{8R_0}{a} + \beta_p + \frac{l_i}{2} - \frac{3}{2} \right)
$$

To prevent the plasma from expanding outwards and hitting the vessel wall, this force must be counteracted by an inward force. This is achieved by applying an external **vertical magnetic field**, $B_v$. This field crosses the [toroidal plasma](@entry_id:202484) current $I_p$ to produce an inward Lorentz force, $F_{in} = 2\pi R_0 I_p B_v$ over the full torus. By equating the outward and inward forces, we can determine the precise vertical field required to maintain the plasma in radial equilibrium :

$$
B_v = \frac{\mu_0 I_p}{4\pi R_0} \left[ \ln\left(\frac{8R_0}{a}\right) + \beta_p + \frac{l_i}{2} - \frac{3}{2} \right] = \frac{\mu_0 I_p}{4\pi R_0} \left[ \ln\left(\frac{8R_0}{a}\right) + \Lambda - \frac{3}{2} \right]
$$

Here, $\Lambda = \beta_p + l_i/2$ is a convenient combined parameter, often called the **Shafranov parameter**. This equation is fundamental to tokamak operation, as it dictates the external field required from the [poloidal field](@entry_id:188655) coils to control the plasma's radial position.

### Physical Consequences of Toroidal Geometry

The toroidal, or doughnut-shaped, geometry of a tokamak introduces several important physical effects not present in a simple cylindrical plasma.

#### Pfirsch-Schlüter Current

In a torus, the magnetic field strength is not uniform on a flux surface; it is stronger on the inboard side (small $R$) and weaker on the outboard side (large $R$), with $B \approx B_0(1 - (r/R_0)\cos\theta)$. This variation has a direct impact on the plasma currents. The pressure gradient $\nabla p$ drives a [diamagnetic current](@entry_id:201627) $\mathbf{j}_\perp = (\mathbf{B} \times \nabla p) / B^2$ that is perpendicular to the magnetic field. Due to the variation of $B$ with the poloidal angle $\theta$, this perpendicular current has a non-zero divergence, $\nabla \cdot \mathbf{j}_\perp \neq 0$.

However, for a [steady-state equilibrium](@entry_id:137090), the total current must be divergence-free, $\nabla \cdot \mathbf{J} = 0$. To satisfy this condition, a current must flow parallel to the magnetic field lines to cancel the divergence of the perpendicular current, such that $\nabla \cdot \mathbf{j}_\parallel = -\nabla \cdot \mathbf{j}_\perp$. This necessary parallel current is known as the **Pfirsch-Schlüter current**. A detailed derivation shows that its magnitude varies along the poloidal direction as :

$$
j_{PS} = -\frac{2r}{R_0 B_\theta} \frac{dp}{dr} \cos\theta
$$

This current flows from the outboard side ($\theta=0$) to the inboard side ($\theta=\pi$) on the top of the torus, and back on the bottom, adding a helical component to the Ohmically-driven toroidal current. This demonstrates that even in equilibrium, the current is not purely toroidal but possesses a complex three-dimensional structure dictated by [force balance](@entry_id:267186) and [charge conservation](@entry_id:151839) in [toroidal geometry](@entry_id:756056).

#### The Shafranov Shift

Another key consequence of toroidicity is the outward shift of the magnetic flux surfaces relative to the geometric center of the vacuum vessel. The forces associated with toroidal curvature effectively "push" the plasma outward. As a result, the magnetic axis is not located at the geometric center $(R_0, Z=0)$ but is displaced horizontally outward by an amount $\Delta$, known as the **Shafranov shift**. The flux surfaces are compressed on the high-field (inboard) side and expanded on the low-field (outboard) side.

The magnitude of this shift can be calculated by solving the Grad-Shafranov equation using a [perturbative expansion](@entry_id:159275) in the inverse aspect ratio $\epsilon = a/R_0$. For a plasma with an elliptical cross-section (with [ellipticity](@entry_id:199972) $\kappa$), the shift depends on both the plasma pressure and the [internal inductance](@entry_id:270056), reflecting the contributions from both kinetic and magnetic forces . A higher plasma pressure (larger $\beta_p$) or a more peaked current profile (larger $l_i$) leads to a larger outward shift. The Shafranov shift is a directly measurable quantity that provides valuable information about the internal energy and current distribution of the plasma.