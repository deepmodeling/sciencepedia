## Introduction
The analysis and simulation of magnetically [confined plasmas](@entry_id:1122875) in devices like tokamaks and stellarators are fundamentally tied to the geometry of the system. While the laws of physics are universal, their mathematical expression becomes tractable and insightful only when cast in a coordinate system that respects the underlying toroidal symmetry and the complex structure of the magnetic field. The use of simple Cartesian coordinates is inadequate for describing phenomena on nested, toroidal magnetic surfaces. This creates a critical need for a sophisticated framework of curvilinear coordinate transformations tailored to fusion science.

This article provides a comprehensive guide to these essential mathematical tools. It bridges the gap between abstract differential geometry and its practical application in plasma physics. Over the course of three chapters, you will gain a deep understanding of this crucial topic. The first chapter, **Principles and Mechanisms**, lays the mathematical foundation, progressing from simple geometric [toroidal coordinates](@entry_id:1133250) to advanced magnetic [flux coordinates](@entry_id:1125149) like Boozer and Hamada systems. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates how these [coordinate systems](@entry_id:149266) are used to formulate physical laws, analyze MHD equilibrium, study plasma transport, and build powerful computational models. Finally, the **Hands-On Practices** chapter allows you to solidify your understanding by applying these concepts to solve practical problems in fusion code development and analysis.

## Principles and Mechanisms

The analysis of toroidal plasma equilibria and the numerical modeling of transport and stability within them depend critically on the choice of coordinate system. While Cartesian coordinates are fundamental, the [toroidal geometry](@entry_id:756056) of devices like tokamaks and stellarators necessitates the use of specialized [curvilinear coordinates](@entry_id:178535) that conform to the device's shape and, more importantly, to the structure of the magnetic field itself. This chapter elucidates the principles and mechanisms underlying the construction and application of these coordinate systems, progressing from simple geometric descriptions to sophisticated magnetic [flux coordinates](@entry_id:1125149).

### Geometric Toroidal Coordinates and the Metric Tensor

The simplest idealization of a [toroidal plasma](@entry_id:202484) volume is a standard geometric torus. We can describe this shape using a set of intuitive [curvilinear coordinates](@entry_id:178535) $(r, \theta, \phi)$. Here, $R_0$ is the major radius from the device's [axis of symmetry](@entry_id:177299) to the center of the toroidal tube, $r$ is the minor radius measuring the distance from that center within a poloidal cross-section, $\theta$ is the poloidal angle measured around the minor radius, and $\phi$ is the toroidal angle measured around the major [axis of symmetry](@entry_id:177299).

The mapping from these [toroidal coordinates](@entry_id:1133250) to a standard Cartesian system $(x, y, z)$ is given by:
$$
x = (R_0 + r \cos\theta) \cos\phi \\
y = (R_0 + r \cos\theta) \sin\phi \\
z = r \sin\theta
$$
where we assume the torus is non-self-intersecting, i.e., $R_0 > r$. This transformation allows us to apply the full machinery of [differential geometry](@entry_id:145818).

The fundamental quantities that describe the local geometry of any coordinate system are the **metric coefficients**, which define how distances are measured. They are the components of the **metric tensor**, $g_{ij}$, defined as the inner product of the [covariant basis](@entry_id:198968) vectors $\mathbf{e}_i = \partial\mathbf{x}/\partial q^i$, where $\mathbf{x}$ is the [position vector](@entry_id:168381) and $q^i$ are the coordinates. Thus, $g_{ij} = \mathbf{e}_i \cdot \mathbf{e}_j$.

An alternative and powerful method to find the metric tensor is by transforming the [line element](@entry_id:196833), $ds^2$. In [cylindrical coordinates](@entry_id:271645) $(R, \phi, Z)$, the [line element](@entry_id:196833) is $ds^2 = dR^2 + R^2 d\phi^2 + dZ^2$. Our [toroidal coordinates](@entry_id:1133250) are related to the cylindrical ones by $R = R_0 + r \cos\theta$ and $Z = r \sin\theta$. By computing the [differentials](@entry_id:158422) $dR = \cos\theta dr - r \sin\theta d\theta$ and $dZ = \sin\theta dr + r \cos\theta d\theta$, we find that $dR^2 + dZ^2 = dr^2 + r^2 d\theta^2$. Substituting this and the expression for $R$ into the cylindrical [line element](@entry_id:196833) yields the [line element](@entry_id:196833) in [toroidal coordinates](@entry_id:1133250) :
$$
ds^2 = dr^2 + r^2 d\theta^2 + (R_0 + r \cos\theta)^2 d\phi^2
$$
The [line element](@entry_id:196833) has the general form $ds^2 = \sum_{i,j} g_{ij} dq^i dq^j$. By comparing the two expressions, we can directly identify the components of the metric tensor. The diagonal components are:
$$
g_{rr} = 1, \quad g_{\theta\theta} = r^2, \quad g_{\phi\phi} = (R_0 + r \cos\theta)^2
$$
Since there are no cross-terms (like $dr d\theta$), all off-diagonal components are zero: $g_{r\theta} = g_{r\phi} = g_{\theta\phi} = 0$. A system with a diagonal metric tensor is called an **orthogonal coordinate system**. In such a system, the coordinate lines intersect at right angles.

The square roots of the diagonal metric components are known as the **[scale factors](@entry_id:266678)**:
$$
h_r = \sqrt{g_{rr}} = 1, \quad h_\theta = \sqrt{g_{\theta\theta}} = r, \quad h_\phi = \sqrt{g_{\phi\phi}} = R_0 + r \cos\theta
$$
These [scale factors](@entry_id:266678) determine the infinitesimal arc length along each coordinate direction: $dl_r = h_r dr = dr$, $dl_\theta = h_\theta d\theta = r d\theta$, and $dl_\phi = h_\phi d\phi = (R_0 + r \cos\theta) d\phi$.

The scale factors are essential for expressing physical operators. For instance, the **gradient** of a [scalar field](@entry_id:154310) $f(r, \theta, \phi)$ in a general [orthogonal system](@entry_id:264885) is given by :
$$
\nabla f = \frac{\hat{\mathbf{e}}_r}{h_r} \frac{\partial f}{\partial r} + \frac{\hat{\mathbf{e}}_\theta}{h_\theta} \frac{\partial f}{\partial \theta} + \frac{\hat{\mathbf{e}}_\phi}{h_\phi} \frac{\partial f}{\partial \phi} = \hat{\mathbf{e}}_r \frac{\partial f}{\partial r} + \frac{\hat{\mathbf{e}}_\theta}{r} \frac{\partial f}{\partial \theta} + \frac{\hat{\mathbf{e}}_\phi}{R_0 + r \cos\theta} \frac{\partial f}{\partial \phi}
$$
where $\hat{\mathbf{e}}_i$ are the [unit vectors](@entry_id:165907) in the coordinate directions.

Similarly, the infinitesimal **[volume element](@entry_id:267802)**, $dV$, is the product of the infinitesimal arc lengths: $dV = dl_r dl_\theta dl_\phi = h_r h_\theta h_\phi dr d\theta d\phi$. For our toroidal system, this becomes :
$$
dV = r(R_0 + r \cos\theta) dr d\theta d\phi
$$
This [volume element](@entry_id:267802) can also be derived from the **Jacobian determinant** of the [coordinate transformation](@entry_id:138577). The Jacobian $J$ is the determinant of the matrix of [partial derivatives](@entry_id:146280) $\partial(x,y,z)/\partial(r,\theta,\phi)$. A direct calculation yields $J = -r(R_0 + r \cos\theta)$ . The volume element is then given by $dV = |J| dr d\theta d\phi$. For an [orthogonal system](@entry_id:264885), it is always true that $|J| = h_r h_\theta h_\phi$. The negative sign of the Jacobian simply indicates that the coordinate system $(r,\theta,\phi)$ is left-handed relative to the Cartesian $(x,y,z)$ system.

### Magnetic Flux Coordinates

While geometric coordinates are useful, the physics of a magnetized plasma is dominated by the structure of the magnetic field, $\mathbf{B}$. It is therefore advantageous to use coordinates that are adapted to the field itself. In many fusion devices, the magnetic field lines lie on a set of nested toroidal surfaces called **magnetic flux surfaces**. A coordinate system built upon these surfaces is known as a **flux coordinate system**.

A scalar function $\psi$ is chosen to label these surfaces, such that each surface is a [level set](@entry_id:637056) $\psi = \text{constant}$. The defining property of a flux surface is that the magnetic field is everywhere tangent to it. This means the magnetic field has no component normal to the surface. Since the gradient vector $\nabla\psi$ is everywhere normal to the surface $\psi = \text{constant}$, this [tangency condition](@entry_id:173083) is expressed mathematically as:
$$
\mathbf{B} \cdot \nabla\psi = 0
$$
This single equation has a profound physical consequence. If we follow a magnetic field line, its [position vector](@entry_id:168381) $\mathbf{r}(l)$ changes with arclength $l$ according to $d\mathbf{r}/dl = \mathbf{B}/|\mathbf{B}|$. The change in $\psi$ along the field line is then given by the [chain rule](@entry_id:147422): $d\psi/dl = \nabla\psi \cdot (d\mathbf{r}/dl) = (\nabla\psi \cdot \mathbf{B}) / |\mathbf{B}|$. Since $\mathbf{B} \cdot \nabla\psi = 0$, we find that $d\psi/dl = 0$. This proves that magnetic field lines are constrained to lie entirely within a single flux surface .

The label $\psi$ is not just an arbitrary index; it is a physically meaningful quantity related to magnetic flux. There are two fundamental types of magnetic flux in a torus: **toroidal flux** and **[poloidal flux](@entry_id:753562)**.
- The **toroidal flux**, $\Phi$, is the flux passing through a poloidal cross-section of the torus (a surface bounded by a poloidal loop, $C_{\text{pol}}$).
- The **[poloidal flux](@entry_id:753562)**, $\psi$, is the flux passing through the "hole" of the torus, linking the plasma (a surface bounded by a toroidal loop, $C_{\text{tor}}$).

Mathematically, these are defined by [surface integrals](@entry_id:144805) :
$$
\Phi = \int_{\Sigma_{\text{pol}}} \mathbf{B} \cdot d\mathbf{S}, \quad \text{where } \partial\Sigma_{\text{pol}} = C_{\text{pol}} \subset S_\psi
$$
$$
\psi = \int_{\Sigma_{\text{tor}}} \mathbf{B} \cdot d\mathbf{S}, \quad \text{where } \partial\Sigma_{\text{tor}} = C_{\text{tor}} \subset S_\psi
$$
(Note: Normalization factors like $1/(2\pi)$ are often included by convention). For these definitions to be useful, the value of the flux must depend only on the flux surface $S_\psi$, not on the specific choice of integration surface $\Sigma$ or the specific loop $C$ on that surface. This is guaranteed by two fundamental properties of the magnetic field:
1.  **Independence of Spanning Surface**: The Maxwell equation $\nabla \cdot \mathbf{B} = 0$, via the [divergence theorem](@entry_id:145271), ensures that the flux through any two surfaces sharing the same boundary loop is identical.
2.  **Independence of Loop on a Flux Surface**: The condition $\mathbf{B} \cdot \nabla\psi = 0$ ensures that the flux through the ribbon-like area on the flux surface connecting two different loops of the same class is zero.

Therefore, $\psi$ and $\Phi$ are single-valued functions on each flux surface, known as **flux functions**. Because the flux surfaces are nested, $\psi$ (or $\Phi$) varies monotonically from the magnetic axis outward, making it an excellent choice for a "radial" coordinate. This holds true even in fully three-dimensional, non-axisymmetric equilibria, as long as [nested flux surfaces](@entry_id:752411) exist .

The two conditions $\nabla \cdot \mathbf{B} = 0$ and $\mathbf{B} \cdot \nabla\psi = 0$ can be elegantly satisfied by writing the magnetic field in a **Clebsch representation**. A theorem of vector calculus states that a field satisfying these conditions can be written as :
$$
\mathbf{B} = \nabla\psi \times \nabla\alpha
$$
for some scalar function $\alpha(\psi, \theta, \zeta)$. This form is automatically [divergence-free](@entry_id:190991) ($\nabla \cdot (\nabla f \times \nabla g) = 0$) and automatically satisfies $\mathbf{B} \cdot \nabla\psi = 0$. The scalar $\alpha$ is a field-line label; its level sets on a flux surface trace out the magnetic field lines.

### Straight-Field-Line Coordinates and Non-Orthogonality

Once we have a radial coordinate $\psi$, we need two angle coordinates, a poloidal angle $\theta$ and a toroidal angle $\zeta$, to complete our flux coordinate system $(\psi, \theta, \zeta)$. A natural first choice for these angles might be the geometric angles from our initial example. However, in such a coordinate system, the magnetic field lines, when viewed on an "unwrapped" $(\theta, \zeta)$ plane, will generally follow curved, winding paths. This is because the local pitch of the field line, given by the ratio of its contravariant components, $d\theta/d\zeta = (\mathbf{B} \cdot \nabla\theta) / (\mathbf{B} \cdot \nabla\zeta)$, is not constant but varies with position on the flux surface .

To simplify the description of the field topology, it is highly desirable to find a set of coordinates in which the field lines become straight. This is achieved by constructing a **straight-field-line poloidal angle**, which we will denote $\Theta$. This special angle is defined by a transformation from a geometric angle $\theta_g$, i.e., $\Theta = \Theta(\psi, \theta_g, \zeta)$, such that the field [line equation](@entry_id:177883) becomes:
$$
\frac{d\Theta}{d\zeta} = \iota(\psi)
$$
Here, $\iota(\psi)$ is a flux function known as the **rotational transform**. It is the inverse of the safety factor, $\iota = 1/q$, and represents the average number of poloidal transits a field line makes for each toroidal transit. In these $(\Theta, \zeta)$ coordinates, the field lines are straight lines with a constant slope $\iota(\psi)$ on each flux surface  . The field line label becomes simply $\alpha = \Theta - \iota(\psi)\zeta$, and the condition $\mathbf{B} \cdot \nabla\alpha = 0$ is equivalent to the straight-field-line condition.

This coordinate choice is extremely powerful for analyzing [plasma stability](@entry_id:197168). For example, a resonant perturbation with a helical phase dependence $m\Theta - n\zeta$ is most dangerous on a flux surface where its helicity matches that of the field lines. In [straight-field-line coordinates](@entry_id:1132468), the derivative of the phase along the field line is $\mathbf{B} \cdot \nabla(m\Theta - n\zeta) = (m\iota(\psi) - n)(\mathbf{B} \cdot \nabla\zeta)$. This derivative, proportional to the parallel wavenumber $k_\parallel$, vanishes everywhere on a flux surface that satisfies the [resonance condition](@entry_id:754285) $\iota(\psi) = n/m$ (or $q(\psi) = m/n$). This simplifies the analysis of magnetic islands and other instabilities immensely .

An important feature of these advanced [coordinate systems](@entry_id:149266) is that they are generally **non-orthogonal**. Recall that orthogonality requires the off-diagonal metric components to be zero. Let's examine $g_{\theta\zeta} = (\partial_\theta \mathbf{x}) \cdot (\partial_\zeta \mathbf{x})$. A general derivation shows that this component is given by :
$$
g_{\theta\zeta} = (\partial_{\theta} R)(\partial_{\zeta} R) + R^2 (\partial_{\theta} \phi)(\partial_{\zeta} \phi) + (\partial_{\theta} Z)(\partial_{\zeta} Z)
$$
In a simple axisymmetric system where $\zeta$ is the geometric toroidal angle $\phi$, and $R$ and $Z$ depend only on $(\psi, \theta)$, this term vanishes, yielding an [orthogonal system](@entry_id:264885). However, [non-orthogonality](@entry_id:192553) ($g_{\theta\zeta} \neq 0$) arises in two key situations:
1.  **Three-Dimensional Shaping**: In a non-axisymmetric device like a stellarator, the poloidal cross-section's shape (described by $R$ and $Z$) varies with the toroidal angle $\zeta$. Thus, $\partial_\zeta R$ and $\partial_\zeta Z$ are non-zero, leading to a non-zero $g_{\theta\zeta}$.
2.  **Coordinate Remapping**: Even in an axisymmetric system, if we define our coordinate $\zeta$ differently from the geometric angle $\phi$, for example through a remapping $\phi = \zeta + \sigma(\psi, \theta)$, the term $R^2(\partial_\theta\phi)(\partial_\zeta\phi)$ can become non-zero, introducing non-orthogonality.

Straight-field-line coordinates, Boozer coordinates, and Hamada coordinates are all examples of systems that are generally non-orthogonal in the interest of simplifying the representation of the magnetic field and associated physics.

### Advanced Systems: Boozer and Hamada Coordinates

Among the various types of [straight-field-line coordinates](@entry_id:1132468), two have found widespread use in fusion theory and computation: **Boozer coordinates** and **Hamada coordinates**. Their distinction lies in which representation of the magnetic field they simplify. On a flux surface, $\mathbf{B}$ can be written in a **covariant form** using the gradient basis, or a **contravariant form** using the tangent vector basis. As $\mathbf{B} \cdot \nabla\psi=0$, these take the form:
$$
\text{Covariant: } \mathbf{B} = B_\psi \nabla\psi + B_\theta \nabla\theta + B_\zeta \nabla\zeta = B_\theta \nabla\theta + B_\zeta \nabla\zeta
$$
$$
\text{Contravariant: } \mathbf{B} = B^\psi \frac{\partial\mathbf{r}}{\partial\psi} + B^\theta \frac{\partial\mathbf{r}}{\partial\theta} + B^\zeta \frac{\partial\mathbf{r}}{\partial\zeta} = B^\theta \frac{\partial\mathbf{r}}{\partial\theta} + B^\zeta \frac{\partial\mathbf{r}}{\partial\zeta}
$$
In any straight-field-line system, the condition $\nabla \cdot \mathbf{B}=0$ requires that the contravariant components can be written as $B^\theta = \iota(\psi) / J$ and $B^\zeta = 1 / J$, where $J$ is the Jacobian of the coordinate system. The key difference between Boozer and Hamada coordinates is the constraint placed on this Jacobian :

- **Hamada Coordinates**: These coordinates are defined by the constraint that the Jacobian is a flux function, $J = J(\psi)$. This makes the coordinate system "equal volume," meaning equal ranges of $(\theta, \zeta)$ correspond to equal volumes on any given flux surface. As a direct consequence, the contravariant components $B^\theta = \iota(\psi)/J(\psi)$ and $B^\zeta = 1/J(\psi)$ become flux functions.

- **Boozer Coordinates**: These coordinates are defined by the constraint that the *covariant* components of the field are flux functions: $B_\theta = I(\psi)$ and $B_\zeta = G(\psi)$. Here $I(\psi)$ is related to the toroidal current within the flux surface, and $G(\psi)$ to the poloidal current outside it. This choice leads to a particularly simple form for particle guiding-center drift trajectories.

In Boozer coordinates, a remarkable property emerges relating the Jacobian to the magnetic field strength $B=|\mathbf{B}|$. By calculating $B^2 = \mathbf{B} \cdot \mathbf{B}$ using both the [covariant and contravariant](@entry_id:189600) forms, one can derive the relation :
$$
J B^2 = G(\psi) + \iota(\psi) I(\psi)
$$
Since the right-hand side is a flux function, the product $J B^2$ must be constant on a given flux surface. This means the Jacobian varies on the surface as $J \propto 1/B^2$. This property ensures that regions of strong magnetic field are associated with smaller coordinate volumes, and vice-versa. This "uniform weighting" greatly simplifies the calculation of flux-surface-averaged quantities, which are central to [transport theory](@entry_id:143989).

### Practical Issue: The Magnetic Axis Singularity

A final, crucial principle in applying [toroidal coordinates](@entry_id:1133250) relates to a [coordinate singularity](@entry_id:159160) at the **magnetic axis**. The magnetic axis is the degenerate flux surface at the center of the nested tori, where the minor radius $r$ (or $\sqrt{\psi}$) goes to zero.

At this location, the poloidal angle $\theta$ becomes ill-defined. Geometrically, the circle around which $\theta$ is measured shrinks to a point. This manifests mathematically as a singularity in the metric tensor . The length of the [basis vector](@entry_id:199546) $\mathbf{e}_\theta = \partial\mathbf{x}/\partial\theta$ scales with $r$, so the metric component $g_{\theta\theta} = |\mathbf{e}_\theta|^2$ vanishes as $r^2$ at the axis. The corresponding contravariant component, which appears in operators like the gradient, is $g^{\theta\theta} \approx 1/g_{\theta\theta}$ and therefore diverges as $1/r^2$. This divergence renders any numerical scheme based on $(\psi, \theta, \zeta)$ coordinates ill-behaved at and near the magnetic axis.

To overcome this, a standard **regularization** technique is employed. Instead of using the flux coordinate system all the way to the axis, a small region around the axis is treated using a different, non-singular coordinate system. A regular cylindrical system $(R, \phi, Z)$ is perfectly well-behaved at the magnetic axis, since the major radius $R$ approaches $R_0 > 0$.

The strategy involves defining a patch around the axis (e.g., for $\psi  \psi_{core}$) where calculations are performed in [cylindrical coordinates](@entry_id:271645). Physical fields are represented not as functions of $(r, \theta)$, but as smooth Taylor series expansions in the Cartesian-like variables $(R-R_0, Z)$. For instance, a [scalar field](@entry_id:154310) $f$ would be approximated as $f(R,Z) \approx c_0 + c_1(R-R_0) + c_2 Z + \dots$. This approach completely removes the problematic angular coordinate $\theta$ from the description near the axis, ensuring that all [differential operators](@entry_id:275037) remain finite and well-defined throughout the entire plasma volume . This hybrid coordinate approach is a cornerstone of many modern computational codes for fusion science.