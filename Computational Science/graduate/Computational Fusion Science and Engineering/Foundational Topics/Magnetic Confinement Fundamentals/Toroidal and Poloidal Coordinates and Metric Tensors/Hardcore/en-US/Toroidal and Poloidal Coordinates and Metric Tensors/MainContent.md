## Introduction
The quest for fusion energy hinges on our ability to confine and control extremely hot plasma within complex magnetic fields, typically inside [toroidal devices](@entry_id:188972) like tokamaks and stellarators. Effectively analyzing and simulating the behavior of this plasma requires a mathematical language that is adapted to the underlying geometry. While fundamental, Cartesian coordinates fail to capture the toroidal topology and the nested structure of magnetic flux surfaces that are central to plasma confinement. This necessitates the use of specialized [curvilinear coordinate systems](@entry_id:172561).

This article provides a comprehensive guide to the essential [coordinate systems](@entry_id:149266) and mathematical tools used in modern [computational fusion science](@entry_id:1122784). It addresses the knowledge gap between abstract geometric concepts and their practical application in plasma physics. By mastering this material, you will gain the ability to translate physical laws into a framework suitable for the toroidal environment.

The journey begins in the "Principles and Mechanisms" chapter, where we will build the mathematical foundation, starting with simple geometric [toroidal coordinates](@entry_id:1133250) and advancing to sophisticated magnetic [flux coordinates](@entry_id:1125149). You will learn to derive and interpret the metric tensor, the cornerstone for all geometric measurements. Next, the "Applications and Interdisciplinary Connections" chapter will demonstrate how this formalism is applied to solve critical problems in [plasma equilibrium](@entry_id:184963), stability, and transport, illustrating the indispensable link between geometry and plasma behavior. Finally, "Hands-On Practices" will provide you with the opportunity to solidify your understanding by working through guided problems that bridge theory with computational practice.

## Principles and Mechanisms

The analysis of plasmas within toroidal confinement devices necessitates the use of [coordinate systems](@entry_id:149266) adapted to the underlying geometry. While Cartesian coordinates $(x, y, z)$ provide a fundamental description of the embedding Euclidean space, they are poorly suited to the toroidal topology and the nested structure of magnetic flux surfaces. This chapter introduces the principles and mechanisms of toroidal and [poloidal coordinates](@entry_id:1129913), beginning with their geometric foundation and culminating in the sophisticated flux coordinate systems essential for modern [computational fusion science](@entry_id:1122784).

### The Standard Toroidal Coordinate System

The most intuitive starting point is a simple geometric torus defined by a major radius $R_0$ and a minor radius $r$. The major radius measures the distance from the [axis of symmetry](@entry_id:177299) to the center of the toroidal tube, while the minor radius is the radius of the tube's circular cross-section. A point on the surface of such a torus can be parameterized using two angles: a **poloidal angle** $\theta$ that specifies the position "the short way around" the circular cross-section, and a **toroidal angle** $\phi$ that specifies the position "the long way around" the main axis of the torus.

A standard mapping from these surface coordinates $(\theta, \phi)$ to Cartesian coordinates $(x,y,z)$ is given by:
$$
\boldsymbol{\mathcal{R}}(\theta,\phi) = \big( (R_0 + r\cos\theta)\cos\phi,\ (R_0 + r\cos\theta)\sin\phi,\ r\sin\theta \big)
$$
This parameterization can be extended to describe the entire volume of the torus by allowing the minor radius $r$ to vary from $0$ (at the center of the tube, or the "magnetic axis") to a maximum value $a$. This creates a full three-dimensional coordinate system $(r, \theta, \phi)$ described by the [position vector](@entry_id:168381):
$$
\boldsymbol{x}(r, \theta, \phi) = \big( (R_0 + r \cos\theta)\cos\phi,\ (R_0 + r \cos\theta)\sin\phi,\ r \sin\theta \big)
$$

To quantify geometric properties such as distance, area, and volume in this curvilinear system, we must first define the [local basis vectors](@entry_id:163370). The **[covariant basis](@entry_id:198968) vectors**, denoted $\boldsymbol{e}_i$, are tangent to the coordinate lines and are found by taking the partial derivative of the [position vector](@entry_id:168381) $\boldsymbol{x}$ with respect to each coordinate $q^i \in \{r, \theta, \phi\}$. For the standard toroidal system, these are :
$$
\boldsymbol{e}_r = \frac{\partial\boldsymbol{x}}{\partial r} = (\cos\theta\cos\phi)\,\hat{\boldsymbol{i}} + (\cos\theta\sin\phi)\,\hat{\boldsymbol{j}} + (\sin\theta)\,\hat{\boldsymbol{k}}
$$
$$
\boldsymbol{e}_\theta = \frac{\partial\boldsymbol{x}}{\partial \theta} = (-r\sin\theta\cos\phi)\,\hat{\boldsymbol{i}} - (r\sin\theta\sin\phi)\,\hat{\boldsymbol{j}} + (r\cos\theta)\,\hat{\boldsymbol{k}}
$$
$$
\boldsymbol{e}_\phi = \frac{\partial\boldsymbol{x}}{\partial \phi} = -(R_0 + r \cos\theta)\sin\phi\,\hat{\boldsymbol{i}} + (R_0 + r \cos\theta)\cos\phi\,\hat{\boldsymbol{j}}
$$
where $\hat{\boldsymbol{i}}, \hat{\boldsymbol{j}}, \hat{\boldsymbol{k}}$ are the [unit vectors](@entry_id:165907) of the Cartesian system.

The fundamental tool for measuring distances is the **metric tensor**. The components of the covariant metric tensor, $g_{ij}$, are defined by the inner products of the [covariant basis](@entry_id:198968) vectors: $g_{ij} = \boldsymbol{e}_i \cdot \boldsymbol{e}_j$. For the simple toroidal system defined above, a direct calculation shows that the basis vectors are mutually orthogonal, meaning their dot products are zero for $i \neq j$. This leads to a diagonal metric tensor [@problem_id:4056537, @problem_id:4056519]:
$$
g_{rr} = \boldsymbol{e}_r \cdot \boldsymbol{e}_r = 1
$$
$$
g_{\theta\theta} = \boldsymbol{e}_\theta \cdot \boldsymbol{e}_\theta = r^2
$$
$$
g_{\phi\phi} = \boldsymbol{e}_\phi \cdot \boldsymbol{e}_\phi = (R_0 + r \cos\theta)^2
$$
$$
g_{r\theta} = g_{r\phi} = g_{\theta\phi} = 0
$$

The infinitesimal square of the distance between two nearby points, the **[line element](@entry_id:196833)** $ds^2$, is given by $ds^2 = g_{ij} dq^i dq^j$. For this [orthogonal system](@entry_id:264885), it simplifies to a [sum of squares](@entry_id:161049):
$$
ds^2 = g_{rr} dr^2 + g_{\theta\theta} d\theta^2 + g_{\phi\phi} d\phi^2 = dr^2 + r^2 d\theta^2 + (R_0 + r \cos\theta)^2 d\phi^2
$$
This expression transparently reveals the geometric meaning of the diagonal metric components. The square root of each component, $\sqrt{g_{ii}}$, acts as a **[scale factor](@entry_id:157673)** that converts an infinitesimal coordinate displacement $dq^i$ into a physical length $ds_i = \sqrt{g_{ii}} dq^i$.
For example, the length of a poloidal loop (at constant $r$ and $\phi$) is $L_{\mathrm{pol}} = \int_0^{2\pi} \sqrt{g_{\theta\theta}} d\theta = \int_0^{2\pi} r d\theta = 2\pi r$. The length of a toroidal loop (at constant $r$ and $\theta$) is $L_{\mathrm{tor}} = \int_0^{2\pi} \sqrt{g_{\phi\phi}} d\phi = \int_0^{2\pi} (R_0 + r\cos\theta) d\phi = 2\pi(R_0+r\cos\theta)$ . Note that the toroidal circumference depends on the poloidal position $\theta$; it is largest on the outboard side ($\theta=0$) and smallest on the inboard side ($\theta=\pi$).

Finally, the differential volume element $dV$ is given by $dV = \sqrt{g} dr d\theta d\phi$, where $\sqrt{g}$ is the **Jacobian** of the coordinate transformation, defined as the square root of the determinant of the metric tensor, $g = \det(g_{ij})$. For a diagonal metric, this is simply the product of the diagonal elements.
$$
g = g_{rr} g_{\theta\theta} g_{\phi\phi} = 1 \cdot r^2 \cdot (R_0 + r \cos\theta)^2
$$
Thus, the Jacobian is [@problem_id:4056507, @problem_id:4056519]:
$$
\sqrt{g} = r(R_0 + r \cos\theta)
$$
This term accounts for the variation in volume occupied by a coordinate cell $(dr, d\theta, d\phi)$ at different locations within the torus.

### Magnetic Flux Coordinates

While the simple geometric coordinates $(r, \theta, \phi)$ provide a useful introduction, they are inadequate for describing realistic magnetic confinement equilibria. The magnetic field $\mathbf{B}$ in a tokamak or stellarator is confined to a set of nested **[magnetic flux surfaces](@entry_id:751623)**. The shape of these surfaces is determined by the balance between plasma pressure and magnetic forces (the Grad-Shafranov equilibrium in axisymmetry) and is generally not composed of simple, concentric circles.

For both theoretical analysis and numerical simulation, it is vastly more convenient to use a coordinate system that is aligned with the magnetic geometry. In such a **flux coordinate system**, one of the coordinates is chosen to be a label for the flux surfaces themselves. This "radial" coordinate is typically denoted by $\psi$.

In an axisymmetric system, the poloidal flux function $\psi$ is an ideal choice for this role . It can be defined from the toroidal component of the [magnetic vector potential](@entry_id:141246), $\mathbf{A} = A_\phi(R, Z) \hat{\mathbf{e}}_\phi$, as $\psi(R,Z) = R A_\phi$. A key property of this function is that magnetic field lines are everywhere tangent to its [level surfaces](@entry_id:196027), a condition mathematically expressed as $\mathbf{B} \cdot \nabla\psi = 0$. This proves that surfaces of constant $\psi$ are indeed [magnetic flux surfaces](@entry_id:751623). Furthermore, $\psi$ has a direct physical meaning: $2\pi\psi$ is the total [poloidal magnetic flux](@entry_id:1129914) (the flux of $\mathbf{B}_p = B_R \hat{\mathbf{e}}_R + B_Z \hat{\mathbf{e}}_Z$) enclosed by the flux surface $\psi$. Thus, $\psi$ can be interpreted as the **[poloidal flux](@entry_id:753562) per radian**. By adopting $\psi$ as a coordinate, we replace the geometric radius $r$ with a physically meaningful quantity that naturally labels the fundamental surfaces of the magnetic structure, creating the coordinate system $(\psi, \theta, \phi)$.

With this more abstract coordinate system, we must introduce the full machinery of [tensor calculus](@entry_id:161423). A vector field $\mathbf{A}$ can be expressed in two complementary ways: using its **contravariant components** $A^i$ or its **covariant components** $A_i$.
$$
\mathbf{A} = A^i \boldsymbol{e}_i = A_i \boldsymbol{a}^i
$$
Here, $\boldsymbol{e}_i = \partial\boldsymbol{x}/\partial q^i$ are the familiar [covariant basis](@entry_id:198968) vectors, tangent to the coordinate lines. The new set of vectors, $\boldsymbol{a}^i = \nabla q^i$, are the **contravariant basis vectors** (also called the reciprocal basis). They are normal to the surfaces of constant coordinate value. The two bases are related by the duality condition $\boldsymbol{e}_i \cdot \boldsymbol{a}^j = \delta_i^j$.

The metric tensor also has two forms. The covariant metric tensor $g_{ij} = \boldsymbol{e}_i \cdot \boldsymbol{e}_j$ and the **contravariant metric tensor** $g^{ij} = \boldsymbol{a}^i \cdot \boldsymbol{a}^j$. The matrix $[g^{ij}]$ is the inverse of the matrix $[g_{ij}]$. These tensors act as the machinery for converting between the two types of components, a process known as **[raising and lowering indices](@entry_id:161292)**:
$$
A_i = g_{ij} A^j \quad \text{and} \quad A^i = g^{ij} A_j
$$
(summation over repeated indices is implied). These relationships are fundamental to performing vector and tensor operations in [curvilinear coordinates](@entry_id:178535). For instance, the [scalar product](@entry_id:175289) of two vectors $\mathbf{A}$ and $\mathbf{B}$ can be computed in several ways, including the particularly useful form $\mathbf{A} \cdot \mathbf{B} = A_i B^i = g_{ij} A^i B^j = g^{ij} A_i B_j$.

As an example, consider a model where the minor radius is related to the poloidal flux via $r(\psi) = \sqrt{2\psi}$ . Through a calculation analogous to the one for geometric coordinates, one finds that the metric in $(\psi, \theta, \phi)$ coordinates is diagonal, with components:
$$
g_{\psi\psi} = \frac{1}{2\psi}, \quad g_{\theta\theta} = 2\psi, \quad g_{\phi\phi} = (1+\sqrt{2\psi}\cos\theta)^2
$$
The contravariant metric tensor is then simply the matrix of reciprocals:
$$
g^{\psi\psi} = 2\psi, \quad g^{\theta\theta} = \frac{1}{2\psi}, \quad g^{\phi\phi} = \frac{1}{(1+\sqrt{2\psi}\cos\theta)^2}
$$
Given a vector field with contravariant components, say $A^\psi=a\psi, A^\theta=b\cos\theta, A^\phi=c$, the [scalar invariant](@entry_id:159606) $S = \mathbf{A} \cdot \mathbf{A} = g_{ij}A^i A^j$ can be computed. This quantity represents the squared magnitude of the vector, a physical scalar that must be independent of the coordinate system used to calculate it. The calculation yields:
$$
S(\psi, \theta, \phi) = g_{\psi\psi}(A^\psi)^2 + g_{\theta\theta}(A^\theta)^2 + g_{\phi\phi}(A^\phi)^2 = \frac{1}{2}a^2\psi + 2\psi b^2\cos^2\theta + c^2(1+\sqrt{2\psi}\cos\theta)^2
$$
This demonstrates how the metric tensor is the essential link between the components of a vector and its intrinsic physical properties.

### Advanced Concepts and Specialized Coordinates

#### Orthogonality
A coordinate system is **orthogonal** if its basis vectors are mutually perpendicular at every point. This corresponds to a diagonal metric tensor, $g_{ij}=0$ for $i \neq j$. While the simple toroidal model is orthogonal, general flux [coordinate systems](@entry_id:149266) are not. It is important to distinguish different types of orthogonality :
1.  **Orthogonality on the flux surface**: The poloidal and toroidal coordinate lines are orthogonal to each other within each flux surface. This is true if and only if $g_{\theta\phi} = \boldsymbol{e}_\theta \cdot \boldsymbol{e}_\phi = 0$.
2.  **Orthogonality of the [radial coordinate](@entry_id:165186) to the surface**: The radial-like coordinate lines (e.g., $\psi$-lines) are everywhere normal to the flux surfaces. This is true if and only if the [tangent vector](@entry_id:264836) to the $\psi$-line, $\boldsymbol{e}_\psi = \partial\boldsymbol{x}/\partial\psi$, is parallel to the surface normal, $\boldsymbol{a}^\psi = \nabla\psi$. This condition is equivalent to requiring $g_{\psi\theta} = 0$ and $g_{\psi\phi} = 0$.

These two types of orthogonality are independent. A coordinate system can have one property without the other. For example, it is common to construct coordinates where the radial direction is orthogonal to the flux surfaces, but the angular coordinates are not orthogonal to each other.

#### The Magnetic Axis Singularity
The magnetic axis, located at $r=0$, represents a **[coordinate singularity](@entry_id:159160)**. At this location, the poloidal angle $\theta$ becomes undefined, as an entire circle of points in coordinate space $(r=0, \theta \in [0, 2\pi))$ maps to a single physical point in space. This is analogous to the singularity at the origin of a [polar coordinate system](@entry_id:174894).

This physical reality is reflected in the metric tensor . As $r \to 0$, the metric component associated with the degenerate angle must vanish. For the poloidal angle, this means $g_{\theta\theta} \to 0$. The specific scaling required for a smooth, locally Euclidean geometry near the axis is $g_{\theta\theta} \sim r^2$. At the same time, a toroidal loop at the axis is simply the circle of the magnetic axis itself, of radius $R_0$. This requires the toroidal [scale factor](@entry_id:157673) to be finite, so $g_{\phi\phi} \to R_0^2$ as $r \to 0$. The Jacobian $\sqrt{g} \approx rR_0$ vanishes at the axis, which is the hallmark of a [coordinate singularity](@entry_id:159160) where a volume in coordinate space collapses to a line or point in physical space. These scalings are critical for the development of well-behaved [numerical schemes](@entry_id:752822) near the magnetic axis.

#### Straight-Field-Line Coordinates
A primary goal of fusion research is to understand phenomena that occur along magnetic field lines, such as wave propagation and particle motion. The operator describing variation along the field, $\mathbf{B} \cdot \nabla$, is therefore of central importance. In a general coordinate system $(\psi, \theta, \phi)$, a field line traces a curve in the $(\theta, \phi)$ plane, as the ratio $d\theta/d\phi = B^\theta/B^\phi$ varies with position. This complicates the action of the $\mathbf{B} \cdot \nabla$ operator, particularly when using Fourier analysis, as it couples different poloidal modes.

To simplify this, specialized **[straight-field-line coordinates](@entry_id:1132468)** are constructed . A straight-field-line poloidal angle, $\theta_{\mathrm{sf}}$, is one chosen such that the ratio of poloidal to toroidal progress along a field line is constant on each flux surface. This constant is the **rotational transform** $\iota(\psi)$:
$$
\frac{d\theta_{\mathrm{sf}}}{d\phi} = \iota(\psi)
$$
In these coordinates, a magnetic field line appears as a straight line with a constant slope $\iota(\psi)$ when plotted in the $(\theta_{\mathrm{sf}}, \phi)$ plane. The primary benefit is computational: the parallel derivative operator acting on a Fourier mode $\exp[i(m\theta_{\mathrm{sf}} - n\phi)]$ simplifies dramatically, becoming algebraic. This greatly enhances the efficiency and accuracy of spectral codes used for stability and transport analysis. It is crucial to note that these coordinates are generally *not* orthogonal; the simplification of the parallel derivative is the overriding goal, often at the expense of metric simplicity.

#### Boozer Coordinates
Among the most powerful straight-field-line systems are **Boozer coordinates** $(\psi, \theta_B, \phi_B)$. They are defined by two key properties :
1.  They are [straight-field-line coordinates](@entry_id:1132468).
2.  The covariant components of the magnetic field, $B_{\theta_B} = \mathbf{B} \cdot \boldsymbol{e}_{\theta_B}$ and $B_{\phi_B} = \mathbf{B} \cdot \boldsymbol{e}_{\phi_B}$, are functions of $\psi$ only. Let $B_{\theta_B} = I(\psi)$ and $B_{\phi_B} = G(\psi)$.

A remarkable consequence of these properties, combined with the fundamental law $\nabla \cdot \mathbf{B} = 0$, is a simple and elegant form for the coordinate Jacobian:
$$
\sqrt{g} = \frac{G(\psi) + \iota(\psi) I(\psi)}{B^2}
$$
This relation connects the coordinate system's [volume element](@entry_id:267802) $\sqrt{g}$ directly to the magnetic field strength $B^2 = \mathbf{B} \cdot \mathbf{B}$ and a small number of flux functions. This seemingly abstract result is of immense practical importance, as it provides a way to represent the complex 3D geometry of a stellarator or non-ideal tokamak in terms of the local magnetic field strength. This property makes Boozer coordinates indispensable for many advanced theoretical calculations, such as those for neoclassical transport and gyrokinetic stability.