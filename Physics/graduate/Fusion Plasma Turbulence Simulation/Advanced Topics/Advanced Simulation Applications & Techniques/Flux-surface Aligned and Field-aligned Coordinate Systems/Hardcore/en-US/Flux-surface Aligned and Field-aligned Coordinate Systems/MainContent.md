## Introduction
In the quest for fusion energy, understanding and controlling the turbulent behavior of plasma within magnetic confinement devices like tokamaks and [stellarators](@entry_id:1132371) is a paramount challenge. The complex, three-dimensional magnetic field geometries that confine the hot plasma necessitate a sophisticated mathematical framework. Standard coordinate systems, such as Cartesian or cylindrical, are ill-suited to describe the physics, which is dominated by the extreme difference between particle and [energy transport](@entry_id:183081) along and across magnetic field lines. This anisotropy poses a significant barrier to both theoretical analysis and efficient numerical simulation.

This article introduces the indispensable tools used to overcome this challenge: flux-surface aligned and field-aligned [coordinate systems](@entry_id:149266). By adapting the mathematical description of space to the underlying [magnetic topology](@entry_id:751637), these coordinates provide a natural and powerful way to simplify the governing equations of [plasma dynamics](@entry_id:185550). Over the next three chapters, you will learn the fundamental concepts that underpin this approach. We will begin by exploring the principles and mechanisms behind the construction of these coordinates, from the definition of magnetic flux surfaces to the properties of straight-field-line systems. Next, we will examine their critical applications in computational modeling, including the [flux-tube](@entry_id:1125141) paradigm for gyrokinetic simulations and the implementation of magnetic shear. Finally, hands-on practices will allow you to apply these concepts to concrete problems, solidifying your understanding of how geometry shapes the physics of fusion plasmas.

## Principles and Mechanisms

In the study of magnetically [confined plasmas](@entry_id:1122875), the geometry of the magnetic field is of paramount importance. The complex three-dimensional structure of [toroidal devices](@entry_id:188972) like tokamaks and [stellarators](@entry_id:1132371) necessitates the use of specialized coordinate systems that are adapted to the magnetic field topology. This chapter delineates the principles and construction of these [coordinate systems](@entry_id:149266), which are foundational to both the theoretical analysis and numerical simulation of plasma behavior. We will begin by defining [magnetic flux surfaces](@entry_id:751623), proceed to the geometric tools used to describe them, explore the properties of field-line trajectories, introduce the powerful concept of [field-aligned coordinates](@entry_id:1124929), and conclude with an examination of the limitations of this paradigm.

### The Concept of Magnetic Flux Surfaces

The cornerstone of magnetic confinement in [toroidal devices](@entry_id:188972) is the concept of the **[magnetic flux surface](@entry_id:751622)**. A [magnetic flux surface](@entry_id:751622) is a two-dimensional surface that is everywhere tangent to the magnetic field vector $\mathbf{B}$. If we can describe such a surface as a level set of some scalar function, $\psi(\mathbf{x}) = \text{constant}$, then its [normal vector](@entry_id:264185) is parallel to $\nabla\psi$. The [tangency condition](@entry_id:173083) thus translates into the fundamental mathematical definition of a flux surface:

$$
\mathbf{B} \cdot \nabla\psi = 0
$$

This equation states that magnetic field lines lie within these surfaces and do not cross them in an ideal, time-independent equilibrium.

In systems with a high degree of symmetry, such as an axisymmetric tokamak, the existence and structure of these surfaces can be derived from first principles . In an axisymmetric system, where physical quantities are independent of the toroidal angle $\phi$, the [divergence-free](@entry_id:190991) nature of the magnetic field, $\nabla \cdot \mathbf{B} = 0$, imposes a strong constraint. In [cylindrical coordinates](@entry_id:271645) $(R, \phi, Z)$, this constraint simplifies to $\frac{\partial(R B_R)}{\partial R} + \frac{\partial(R B_Z)}{\partial Z} = 0$ for the poloidal components of the field $(B_R, B_Z)$. This structure allows us to define a [scalar potential](@entry_id:276177), the **poloidal flux function** $\psi(R,Z)$, such that:

$$
R B_R = -\frac{\partial \psi}{\partial Z} \quad \text{and} \quad R B_Z = \frac{\partial \psi}{\partial R}
$$

With this definition, the condition $\mathbf{B} \cdot \nabla\psi = 0$ is automatically satisfied for the [poloidal field](@entry_id:188655) components, confirming that surfaces of constant $\psi(R,Z)$ are indeed [magnetic flux surfaces](@entry_id:751623). The function $\psi$ is directly related to the [poloidal magnetic flux](@entry_id:1129914), which is the flux of $\mathbf{B}$ passing through a ribbon extending from the magnetic axis to a given radius $R$ and encircling the torus once toroidally. Specifically, the total [poloidal flux](@entry_id:753562) $\Phi_p$ is given by $\Phi_p = 2\pi\psi$. This can also be related to the [vector potential](@entry_id:153642) $\mathbf{A}$, where $\mathbf{B} = \nabla \times \mathbf{A}$. In axisymmetry, $\psi$ is proportional to $R A_{\phi}$, where $A_{\phi}$ is the toroidal component of the vector potential.

In an ideal equilibrium without magnetic islands or stochastic regions, the field line equations are integrable. Consequently, the flux surfaces form a set of nested, non-intersecting tori, filling the confinement volume from the central magnetic axis out to the plasma edge . This nested topology is the foundation of the coordinate systems we will now develop.

### General Curvilinear Coordinates on Flux Surfaces

To describe positions within the plasma volume, we use a **flux-surface aligned coordinate system** $(\psi, \theta, \phi)$. Here, $\psi$ serves as a radial-like coordinate labeling the flux surfaces. The coordinates $\theta$ and $\phi$ are angle-like variables that parameterize positions on a given flux surface. The **toroidal angle** $\phi$ is typically the geometric angle of rotation about the main symmetry axis of the torus. The **poloidal angle** $\theta$ is a coordinate that parameterizes the closed path in the poloidal cross-section (the R-Z plane) . Both $\theta$ and $\phi$ are usually taken to be $2\pi$-periodic.

The mapping from these [curvilinear coordinates](@entry_id:178535) to a Cartesian or cylindrical representation in physical space is given by a [position vector](@entry_id:168381), $\mathbf{r}(\psi, \theta, \phi)$. To make these abstract concepts concrete, let us consider a simplified model for a large-aspect-ratio tokamak with concentric circular flux surfaces . The [position vector](@entry_id:168381) can be written as:

$$
\mathbf{r}(\psi,\theta,\phi) = \bigl( (R_0 + r(\psi)\cos\theta)\cos\phi, \; (R_0 + r(\psi)\cos\theta)\sin\phi, \; r(\psi)\sin\theta \bigr)
$$

where $R_0$ is the constant major radius of the torus and $r(\psi)$ is the minor radius of the flux surface labeled by $\psi$.

From the [position vector](@entry_id:168381), we can derive the fundamental geometric objects. The **[covariant basis](@entry_id:198968) vectors** are defined as the partial derivatives of the [position vector](@entry_id:168381) with respect to the coordinates:

$$
\mathbf{e}_\psi = \frac{\partial \mathbf{r}}{\partial \psi}, \quad \mathbf{e}_\theta = \frac{\partial \mathbf{r}}{\partial \theta}, \quad \mathbf{e}_\phi = \frac{\partial \mathbf{r}}{\partial \phi}
$$

These vectors are tangent to the coordinate lines. The geometry of the space is encoded in the **metric tensor**, $g_{ij} = \mathbf{e}_i \cdot \mathbf{e}_j$. For our circular tokamak model, a direct calculation shows that the off-diagonal components of the metric tensor are zero ($g_{ij} = 0$ for $i \neq j$), meaning these specific coordinates are orthogonal. The diagonal components are:

$$
g_{\psi\psi} = \left(\frac{dr}{d\psi}\right)^2, \quad g_{\theta\theta} = r(\psi)^2, \quad g_{\phi\phi} = (R_0 + r(\psi)\cos\theta)^2
$$

The volume element in this coordinate system is $dV = J\,d\psi\,d\theta\,d\phi$, where $J$ is the **Jacobian** of the transformation, given by $J = \sqrt{\det(g)}$. For our [orthogonal system](@entry_id:264885), this is the product of the square roots of the diagonal metric components:

$$
J = \sqrt{g_{\psi\psi} g_{\theta\theta} g_{\phi\phi}} = \left| \frac{dr}{d\psi} \right| r(\psi) (R_0 + r(\psi)\cos\theta)
$$

This Jacobian, representing the volume of an infinitesimal coordinate parallelepiped, varies with position, reflecting the toroidal geometry. This general framework of differential geometry is essential for writing physical equations, such as those of fluid dynamics or electromagnetism, in a form that is valid in any coordinate system.

### The Winding of Magnetic Field Lines

On any given flux surface, a magnetic field line winds helically. The pitch of this winding is a crucial parameter that governs plasma stability and transport. This pitch is quantified by the **safety factor**, denoted by $q(\psi)$ . It is defined as the average ratio of the rate of change of the toroidal angle to the poloidal angle along a field line:

$$
q(\psi) \equiv \frac{1}{2\pi} \oint \frac{d\phi}{d\theta} \,d\theta
$$

where the integral is taken over one full poloidal circuit (from $\theta$ to $\theta+2\pi$) along the field line. Physically, $q(\psi)$ represents the number of toroidal transits a field line makes for every one poloidal transit.

The nature of the field line trajectory depends critically on whether $q(\psi)$ is a rational or irrational number .
- If $q(\psi) = m/n$ is a **rational number** (with $m, n$ coprime integers), a field line will close upon itself after completing $n$ poloidal turns and $m$ toroidal turns. Such surfaces are called rational surfaces and are populated by periodic field lines.
- If $q(\psi)$ is an **irrational number**, a field line will never close on itself. Instead, it will ergodically cover the entire flux surface, passing arbitrarily close to every point.

The radial variation of the safety factor is known as **magnetic shear**. A common dimensionless measure of shear is $\hat{s} = (r/q) \, dq/dr$, where $r$ is a minor-radius-like coordinate . Positive magnetic shear ($\hat{s} > 0$) means that the field line pitch increases with radius, a property that is generally stabilizing for many [plasma instabilities](@entry_id:161933).

In non-axisymmetric systems like [stellarators](@entry_id:1132371), the same concept is described by the **[rotational transform](@entry_id:200017)**, $\iota(\psi)$, which is simply the inverse of the safety factor, $\iota(\psi) = 1/q(\psi)$ . It represents the number of poloidal transits per toroidal transit. Stellarators are designed with complex 3D coil systems specifically to generate a non-zero [rotational transform](@entry_id:200017), which is essential for confinement in the absence of a large plasma-driven current.

### Field-Aligned Coordinates: Simplifying the Parallel Direction

#### Motivation: The Challenge of Anisotropy

One of the most profound challenges in simulating magnetized plasmas arises from the extreme anisotropy of transport processes. Particles and heat travel much more freely along magnetic field lines than across them. This is modeled by a transport equation with highly disparate parallel and perpendicular diffusivities, $\chi_{\parallel} \gg \chi_{\perp}$. For instance, in a tokamak, the ratio for [electron heat transport](@entry_id:748911) can be $\chi_{\parallel}/\chi_{\perp} \sim 10^6$ or even larger .

Consider an anisotropic diffusion equation:
$$
\frac{\partial T}{\partial t} = \nabla \cdot \left[ \chi_{\parallel} \,\mathbf{b}\,\mathbf{b} \cdot \nabla T + \chi_{\perp} \,(\mathbf{I} - \mathbf{b}\,\mathbf{b}) \cdot \nabla T \right]
$$
where $\mathbf{b} = \mathbf{B}/|\mathbf{B}|$ is the [unit vector](@entry_id:150575) along the magnetic field. If this equation is discretized on a standard grid (e.g., Cartesian), the parallel operator $\mathbf{b} \cdot \nabla$ will involve derivatives along multiple coordinate axes. This leads to large mixed-derivative terms in the discretized equations and, more critically, to extreme **[numerical stiffness](@entry_id:752836)**. The maximum allowable time step in an explicit numerical scheme is dictated by the fastest process, which is parallel diffusion. The stability limit scales as $\Delta t \lesssim (\Delta x)^2/\chi$, leading to a prohibitively small time step due to the large value of $\chi_{\parallel}$.

The solution is to adopt a coordinate system that is aligned with the magnetic field. By choosing one coordinate, say $s$, to be aligned with $\mathbf{b}$, the diffusion tensor becomes diagonal. The equation simplifies to a form like $\frac{\partial T}{\partial t} \approx \chi_{\parallel} \frac{\partial^2 T}{\partial s^2} + \chi_{\perp} \nabla_{\perp}^2 T$. The stiffness can then be mitigated by using an [anisotropic grid](@entry_id:746447), with a very long grid spacing $\Delta s$ along the field line and a short spacing $\Delta_{\perp}$ across it. To balance the time-step limitations from parallel and perpendicular diffusion, the grid aspect ratio must be chosen to match the transport anisotropy, with the [optimal scaling](@entry_id:752981) being:

$$
\frac{\Delta s}{\Delta_{\perp}} \approx \sqrt{\frac{\chi_{\parallel}}{\chi_{\perp}}}
$$

For a typical electron anisotropy of $10^6$, this implies a grid aspect ratio of $\sim 1000$. This demonstrates that constructing and using [field-aligned coordinates](@entry_id:1124929) is not merely a convenience but a computational necessity.

#### Construction: Straight-Field-Line Coordinates

A **field-aligned coordinate system** is constructed to simplify the representation of the parallel direction. A key class of such systems is **[straight-field-line coordinates](@entry_id:1132468)**, where the poloidal angle $\theta$ and toroidal angle $\phi$ are chosen such that the magnetic field lines become straight lines in the $(\theta, \phi)$ plane of a flux surface. In such a system, the ratio of the contravariant field components is constant on a flux surface and equals the safety factor:

$$
\frac{d\phi}{d\theta} = \frac{B^\phi}{B^\theta} = q(\psi)
$$

This is in contrast to a general coordinate system, where this ratio varies with position on the flux surface. To complete the coordinate system, we replace one of the angular coordinates with a **field-line label**, often denoted by $\alpha$. For an axisymmetric system, a convenient choice is :

$$
\alpha = \phi - q(\psi)\theta
$$

By construction, this coordinate $\alpha$ is constant along a magnetic field line, since $\mathbf{B} \cdot \nabla\alpha = B^\phi - q(\psi) B^\theta = 0$. The resulting coordinate system is $(\psi, \alpha, \theta)$, where $\psi$ labels the flux surface, $\alpha$ labels the field line on that surface, and $\theta$ measures distance along the field line.

In this system, the parallel gradient operator $\nabla_\| = \mathbf{b} \cdot \nabla$ takes on a much simpler form. Since $\mathbf{b} \cdot \nabla\psi=0$ and $\mathbf{b} \cdot \nabla\alpha=0$, the operator acts only on the coordinate along the field line:

$$
\nabla_\| = (\mathbf{b} \cdot \nabla\theta) \frac{\partial}{\partial\theta}
$$

While the metric factor $(\mathbf{b} \cdot \nabla\theta)$ generally varies along the field line, the operator is now aligned with a single coordinate direction, $\partial/\partial\theta$. This is the fundamental simplification that motivates the use of these coordinates in turbulence and transport simulations.

### Specialized Field-Aligned Systems: Boozer Coordinates

For advanced theoretical and computational work, even more specialized coordinate systems are desirable. Among the most important are **Boozer coordinates** $(\psi, \theta_B, \phi_B)$ . These coordinates are defined by two key properties:
1.  They are [straight-field-line coordinates](@entry_id:1132468).
2.  The covariant components of the magnetic field, $B_{\theta_B} = \mathbf{B} \cdot \mathbf{e}_{\theta_B}$ and $B_{\phi_B} = \mathbf{B} \cdot \mathbf{e}_{\phi_B}$, are flux functions, depending only on $\psi$.

This second property has profound consequences. In a general coordinate system, the magnetic field strength $B^2$ and the Jacobian $J$ vary in a complicated way on a flux surface. In Boozer coordinates, the choice of angles is made such that the product $J B^2$ becomes a flux function. This greatly simplifies many calculations, particularly those involving [guiding-center motion](@entry_id:202625) and [neoclassical transport](@entry_id:188243).

A prime example of this simplification is the representation of the $\mathbf{E} \times \mathbf{B}$ drift. For a purely radial electric field, which arises from an electrostatic potential that is a flux function, $\Phi = \Phi(\psi)$, the drift velocity is $\mathbf{v}_E = (c/B^2) \mathbf{B} \times \nabla\Phi$. In generic coordinates, the contravariant components of this velocity, $v_E^\theta$ and $v_E^\phi$, would vary with position on the flux surface due to the variation in $B^2$ and the metric elements. In Boozer coordinates, however, the contravariant components become:

$$
v_{E}^{\theta_{B}} = c\,\Phi'(\psi)\,(J B^2)^{-1}\,B_{\phi_{B}}(\psi)
$$
$$
v_{E}^{\phi_{B}} = -c\,\Phi'(\psi)\,(J B^2)^{-1}\,B_{\theta_{B}}(\psi)
$$

Since every term on the right-hand side is a function of $\psi$ only, the velocity components $v_{E}^{\theta_{B}}$ and $v_{E}^{\phi_{B}}$ are constant on a flux surface. This means the $\mathbf{E} \times \mathbf{B}$ flow corresponds to a [rigid-body rotation](@entry_id:268623) in the Boozer angles $(\theta_B, \phi_B)$ on each flux surface. This elegant result dramatically simplifies the analysis of plasma flows.

### Boundaries and Breakdowns: The Limits of the Flux Coordinate Paradigm

The powerful paradigm of [flux-surface aligned coordinates](@entry_id:1125139) is built on the assumption of a well-behaved magnetic geometry with smooth, [nested flux surfaces](@entry_id:752411). This assumption breaks down in several important regions of a fusion plasma, leading to coordinate singularities  .

-   **The Magnetic Axis**: At the center of the plasma, the flux surface degenerates into a line. The minor radius $r \to 0$, and the poloidal angle $\theta$ becomes ill-defined. This creates a [coordinate singularity](@entry_id:159160), analogous to the singularity at the pole in [spherical coordinates](@entry_id:146054).

-   **The Separatrix and X-Point**: In modern diverted tokamaks, the core plasma is bounded by a **[separatrix](@entry_id:175112)**, a special flux surface that separates the closed, [nested flux surfaces](@entry_id:752411) of the core from the open field lines in the scrape-off layer. The [separatrix](@entry_id:175112) contains one or more **X-points**, which are null points of the poloidal magnetic field. At an X-point, the gradient of the flux function vanishes: $\nabla\psi = \mathbf{0}$. This has two severe consequences for our [coordinate systems](@entry_id:149266):
    1.  The inverse Jacobian of the $(\psi, \theta, \phi)$ transformation, $J^{-1} = \nabla\psi \cdot (\nabla\theta \times \nabla\phi)$, becomes zero. This implies the Jacobian $J$ is infinite, and the coordinate system is singular.
    2.  The Clebsch representation $\mathbf{B} = \nabla\psi \times \nabla\alpha$ fails. At the X-point, this would imply $\mathbf{B}=\mathbf{0}$, which is generally not true (only the [poloidal field](@entry_id:188655) is zero, not the toroidal field). A finite magnetic field cannot be represented by the [cross product](@entry_id:156749) if one of the gradients is zero and the other is finite.

-   **Stochastic Regions**: In some regions of a plasma, particularly at the edge or in the presence of large-scale instabilities, the magnetic field lines may become chaotic or **stochastic**. In such a region, the very concept of a flux surface is lost. Field lines are no longer confined to 2D surfaces but instead wander through a 3D volume. Since the flux function $\psi$ cannot be defined, the entire framework of flux-surface aligned and [field-aligned coordinates](@entry_id:1124929) breaks down.

These limitations mean that while flux-aligned coordinates are indispensable for describing the well-confined plasma core, they cannot provide a single, global description of the entire device. The edge and scrape-off-layer regions, which include open field lines, separatrices, and potentially stochastic layers, require different modeling approaches and coordinate systems. Understanding the domain of validity of [flux coordinates](@entry_id:1125149) is therefore as crucial as understanding their construction.