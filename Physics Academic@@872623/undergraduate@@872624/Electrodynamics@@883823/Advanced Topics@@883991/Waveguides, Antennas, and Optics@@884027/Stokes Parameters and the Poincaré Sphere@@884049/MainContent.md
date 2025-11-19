## Introduction
The [polarization of light](@entry_id:262080) is a fundamental property that carries a wealth of information about its source and the medium through which it has traveled. While some formalisms, like the Jones calculus, elegantly describe perfectly [polarized light](@entry_id:273160), they fall short when faced with the ubiquitous reality of partially polarized or completely unpolarized light. This gap necessitates a more universal framework. This article introduces the Stokes parameters and the Poincaré sphere, a powerful and intuitive system developed to provide a complete description for any possible state of polarization. We will first delve into the foundational **Principles and Mechanisms**, defining the Stokes parameters through measurable intensities and exploring their geometric representation on the Poincaré sphere. Next, we will witness the framework's power in **Applications and Interdisciplinary Connections**, from designing optical systems to decoding celestial signals in astrophysics. Finally, you will have the opportunity to solidify your understanding through **Hands-On Practices**, applying these concepts to solve real-world problems. Let us begin by establishing the principles that make this formalism so effective.

## Principles and Mechanisms

While the Jones calculus provides an elegant description of perfectly polarized light using [complex vectors](@entry_id:192851), it cannot readily accommodate partially polarized or unpolarized light. To provide a complete and universal description of any state of polarization, we turn to a powerful formalism developed by Sir George Gabriel Stokes in 1852. This approach is based on four real, measurable intensity parameters, known as the **Stokes parameters**.

### The Stokes Parameters: An Empirical Framework

The power of the Stokes formalism lies in its direct connection to experiment. The four parameters, denoted $S_0, S_1, S_2,$ and $S_3$, are defined in terms of intensities—quantities that can be measured directly with a photodetector after passing a light beam through specific [polarizing filters](@entry_id:263130).

Let us consider a beam of light propagating along the z-axis. We can define the Stokes parameters based on six fundamental intensity measurements:
1.  $I_H$: Intensity after a horizontal [linear polarizer](@entry_id:195509) (transmission axis at $0^\circ$).
2.  $I_V$: Intensity after a vertical [linear polarizer](@entry_id:195509) (transmission axis at $90^\circ$).
3.  $I_{45}$: Intensity after a [linear polarizer](@entry_id:195509) at $+45^\circ$.
4.  $I_{135}$: Intensity after a [linear polarizer](@entry_id:195509) at $-45^\circ$ (or $+135^\circ$).
5.  $I_R$: Intensity after a right-circular [polarizer](@entry_id:174367).
6.  $I_L$: Intensity after a left-circular polarizer.

From these measurable quantities, the Stokes parameters are defined as:

$S_0 = I_H + I_V$

$S_1 = I_H - I_V$

$S_2 = I_{45} - I_{135}$

$S_3 = I_R - I_L$

The parameter $S_0$ is the most straightforward; it represents the **total intensity** of the light beam, as an ideal polarizer pair oriented orthogonally (like horizontal and vertical) will pass all incident light when their individual transmitted intensities are summed. The remaining three parameters describe the polarization character of the light.

*   $S_1$ quantifies the preponderance of horizontal linear polarization over vertical [linear polarization](@entry_id:273116). A positive $S_1$ indicates a horizontal tendency, a negative $S_1$ indicates a vertical tendency, and $S_1=0$ indicates no preference between the two.

*   $S_2$ similarly quantifies the preference for $+45^\circ$ linear polarization over $-45^\circ$ [linear polarization](@entry_id:273116).

*   $S_3$ quantifies the preference for right-circular polarization over left-[circular polarization](@entry_id:261702). The sign convention for $S_3$ is a matter of definition; here we adopt the standard where positive $S_3$ corresponds to a predominance of right-circularly polarized (RHC) light.

These definitions provide a direct operational procedure for determining the polarization state of any light source. For instance, by measuring $I_H$ and $I_V$, one can immediately find both the total intensity $S_0 = I_H + I_V$ and the parameter $S_1 = I_H - I_V$. If an engineer measures $I_H = 15.8 \, \text{W/m}^2$ and $I_V = 6.20 \, \text{W/m}^2$, they would find $S_0 = 22.0 \, \text{W/m}^2$ and $S_1 = 9.60 \, \text{W/m}^2$. This reveals a beam with a significant preference for horizontal polarization. The four parameters are often grouped into a column vector, the **Stokes vector**, $S = \begin{pmatrix} S_0 & S_1 & S_2 & S_3 \end{pmatrix}^T$.

### Decomposition of Light and the Degree of Polarization

A remarkable feature of the Stokes formalism is its ability to handle any state of polarization—perfectly polarized, partially polarized, or completely unpolarized. This is achieved by recognizing that any arbitrary beam of light can be treated as an incoherent superposition of a completely polarized component and a completely unpolarized component.

For a **completely polarized** beam of light, the Stokes parameters are not independent and satisfy the identity:

$S_1^2 + S_2^2 + S_3^2 = S_0^2$

For a **completely unpolarized** beam, there is no preferred polarization state. This means that passing it through any ideal [polarizer](@entry_id:174367) (linear or circular) will always reduce its intensity by exactly half. Consequently, $I_H = I_V = I_{45} = I_{135} = I_R = I_L = S_0/2$. Applying the definitions, we find that for [unpolarized light](@entry_id:176162):

$S_1 = S_2 = S_3 = 0$

The corresponding Stokes vector is simply $(S_0, 0, 0, 0)$. This state can arise, for example, from the [time-averaging](@entry_id:267915) of many [light quanta](@entry_id:148679) whose polarization axes are oriented randomly and uniformly over all possible angles. An observer measuring such a beam would detect no net polarization.

For the general case of **[partially polarized light](@entry_id:267467)**, the Stokes parameters obey the inequality:

$S_1^2 + S_2^2 + S_3^2 \le S_0^2$

This observation leads to a powerful decomposition. We can express the total intensity $S_0$ as the sum of the intensity of the polarized part, $I_{\text{pol}}$, and the unpolarized part, $I_{\text{unpol}}$:

$S_0 = I_{\text{pol}} + I_{\text{unpol}}$

The polarized component carries all of the "polarized character" of the beam, such that its intensity is given by the portion of the Stokes parameters that satisfy the equality for [polarized light](@entry_id:273160):

$I_{\text{pol}} = \sqrt{S_1^2 + S_2^2 + S_3^2}$

This allows us to isolate the intensity of the unpolarized component from a set of measurements. By rearranging the equations, we find an expression for the unpolarized intensity solely in terms of the measurable Stokes parameters:

$I_{\text{unpol}} = S_0 - I_{\text{pol}} = S_0 - \sqrt{S_1^2 + S_2^2 + S_3^2}$

This decomposition is not merely a mathematical trick; it has profound physical meaning, for instance in astrophysics, where it can be used to distinguish between starlight that has been polarized by scattering and the unpolarized component that has traveled unimpeded.

To quantify the "amount" of polarization, we define the **Degree of Polarization (DoP)**, denoted by $P$, as the ratio of the intensity of the polarized component to the total intensity:

$P = \frac{I_{\text{pol}}}{S_0} = \frac{\sqrt{S_1^2 + S_2^2 + S_3^2}}{S_0}$

The value of $P$ ranges from $P=1$ for completely polarized light to $P=0$ for completely unpolarized light, with intermediate values for partially polarized states. For example, if a beam is an incoherent mixture of unpolarized light of intensity $I_u$ and left-circularly polarized (LCP) light of intensity $I_c$, the total Stokes vector would be the sum of the individual vectors: $S_{\text{unpol}} = (I_u, 0, 0, 0)$ and $S_{\text{LCP}} = (I_c, 0, 0, -I_c)$. The resulting beam has the Stokes vector $S = (I_u+I_c, 0, 0, -I_c)$. Its [degree of polarization](@entry_id:276690) is therefore $P = \frac{\sqrt{0^2+0^2+(-I_c)^2}}{I_u+I_c} = \frac{I_c}{I_u+I_c}$. This shows that the [degree of polarization](@entry_id:276690) is precisely the fraction of the total intensity that is in the polarized form.

As a practical application, consider a partially polarized beam with a measured Stokes vector of $S = (10, 3, 4, 5\sqrt{2})$ in units of W/m². The intensity of the polarized component is $I_{\text{pol}} = \sqrt{3^2 + 4^2 + (5\sqrt{2})^2} = \sqrt{9+16+50} = \sqrt{75} = 5\sqrt{3}$ W/m². The total intensity is $S_0 = 10$ W/m². Thus, the intensity of the unpolarized component is $I_{\text{unpol}} = 10 - 5\sqrt{3}$ W/m². The ratio of polarized to unpolarized intensity is $\frac{5\sqrt{3}}{10-5\sqrt{3}}$, which simplifies to $3 + 2\sqrt{3}$.

### The Poincaré Sphere: A Geometric Visualization

The algebraic relations between the Stokes parameters find a beautiful and powerful geometric interpretation in the **Poincaré sphere**. This construction provides a visual map of all possible [polarization states](@entry_id:175130).

To construct this map, we first define a set of **normalized Stokes parameters**:

$s_1 = \frac{S_1}{S_0}, \quad s_2 = \frac{S_2}{S_0}, \quad s_3 = \frac{S_3}{S_0}$

These parameters are dimensionless and independent of the total beam intensity. For any state of light, the [degree of polarization](@entry_id:276690) is given by $P = \sqrt{s_1^2 + s_2^2 + s_3^2}$.

We can now interpret the triplet $(s_1, s_2, s_3)$ as the Cartesian coordinates of a point in a three-dimensional space. From the definition of $P$, it is clear that any polarization state corresponds to a point located at a distance $P$ from the origin.

For **fully [polarized light](@entry_id:273160)** ($P=1$), the coordinates satisfy $s_1^2+s_2^2+s_3^2 = 1$. This is the [equation of a sphere](@entry_id:177405) of unit radius. This unit sphere is the Poincaré sphere, and every point on its surface represents a unique state of complete polarization.

The mapping of states to the sphere's surface is highly intuitive:
*   The **North Pole** $(0, 0, 1)$ corresponds to $s_3=1$. This means $S_3=S_0$, or $I_R-I_L = I_R+I_L$, which implies $I_L=0$. This is pure **Right-Hand Circular (RHC)** polarization.
*   The **South Pole** $(0, 0, -1)$ corresponds to $s_3=-1$, which by the same logic is pure **Left-Hand Circular (LHC)** polarization.
*   The **Equator**, where $s_3=0$, represents all states of **linear polarization**. Specific points on the equator are:
    *   $(1, 0, 0)$: $s_1=1 \implies I_H-I_V=I_H+I_V \implies I_V=0$. This is horizontal linear polarization.
    *   $(-1, 0, 0)$: $s_1=-1 \implies I_H=0$. This is vertical [linear polarization](@entry_id:273116).
    *   $(0, 1, 0)$: $s_2=1 \implies I_{135}=0$. This is linear polarization at $+45^\circ$.
    *   $(0, -1, 0)$: $s_2=-1 \implies I_{45}=0$. This is [linear polarization](@entry_id:273116) at $-45^\circ$.

All other points on the sphere represent **[elliptical polarization](@entry_id:270497)**, with the northern hemisphere corresponding to right-handed [ellipticity](@entry_id:199972) and the southern hemisphere to left-handed [ellipticity](@entry_id:199972). **Partially [polarized light](@entry_id:273160)**, for which $P  1$, is represented by points *inside* the Poincaré sphere. The origin $(0,0,0)$ represents completely [unpolarized light](@entry_id:176162) ($P=0$).

The position of a state on the sphere can also be described using [spherical coordinates](@entry_id:146054). The longitude is given by $2\psi$ and the latitude by $2\chi$, where:

$s_1 = \cos(2\chi) \cos(2\psi)$

$s_2 = \cos(2\chi) \sin(2\psi)$

$s_3 = \sin(2\chi)$

The angle $\psi$ represents the orientation of the major axis of the polarization ellipse, while $\chi$ represents its [ellipticity](@entry_id:199972). For linear polarizations, the state lies on the equator, so the latitude $2\chi=0$. The longitude $2\psi$ is then directly related to the physical orientation angle $\alpha$ of the [linear polarization](@entry_id:273116) with respect to the horizontal axis by the simple relation $2\psi = 2\alpha$. For instance, a linear polarization at $\alpha = 60^\circ$ is found at longitude $2\psi = 120^\circ$ on the equator. The factor of two is crucial; a physical rotation of $180^\circ$ returns a [linear polarizer](@entry_id:195509) to its original state, corresponding to a full $360^\circ$ trip around the equator.

### Geometric Relationships on the Poincaré Sphere

The true power of the Poincaré sphere lies in its ability to visualize relationships between [polarization states](@entry_id:175130) and the effects of optical elements.

#### Orthogonal States

Two [polarization states](@entry_id:175130) are said to be **orthogonal** if a filter that completely blocks one state completely transmits the other. For example, horizontal and vertical linear polarizations are orthogonal. On the Poincaré sphere, a remarkable and fundamental rule emerges: **two mutually orthogonal [polarization states](@entry_id:175130) always lie at [antipodal points](@entry_id:151589)**. If a state is represented by the normalized Stokes vector $\vec{s}_A$, its orthogonal counterpart is represented by $\vec{s}_B = -\vec{s}_A$.

This is immediately evident for the cardinal points:
*   Horizontal ($s_1=1$) is antipodal to Vertical ($s_1=-1$).
*   $+45^\circ$ ($s_2=1$) is antipodal to $-45^\circ$ ($s_2=-1$).
*   RHC ($s_3=1$) is antipodal to LHC ($s_3=-1$).

This relationship holds for any pair of orthogonal states, such as a right-elliptical state and its orthogonal left-elliptical counterpart. The distance between them on the sphere is always 2, the diameter of the sphere.

#### Incoherent Addition

When two beams of light are combined **incoherently**, their respective Stokes vectors add. Let two beams, A and B, have intensities $I_A$ and $I_B$ and normalized Stokes vectors $\vec{s}_A$ and $\vec{s}_B$. The Stokes vector of the mixed beam is $S_{mix} = S_A + S_B = (I_A, I_A\vec{s}_A) + (I_B, I_B\vec{s}_B)$. The normalized Stokes vector of the mixture is then:

$\vec{s}_{mix} = \frac{I_A \vec{s}_A + I_B \vec{s}_B}{I_A + I_B}$

This is the formula for a weighted average. Geometrically, this means that the point representing the mixed state, $P_{mix}$, lies on the straight line segment connecting the points $P_A$ and $P_B$ that represent the constituent beams. The exact position of $P_{mix}$ on this line is determined by the relative intensities, following a "[lever rule](@entry_id:136701)": the ratio of the distance from $P_{mix}$ to $P_A$ to the distance from $P_{mix}$ to $P_B$ is equal to $I_B / I_A$. This provides a beautiful geometric picture for how [partial polarization](@entry_id:187644) arises from mixing. For example, mixing any two fully polarized states (points on the surface) will result in a partially polarized state (a point inside the sphere), unless the two states are identical.

### Connection to the Jones Calculus

For fully polarized light, the Stokes parameters can be derived directly from the components of the Jones vector $\vec{J} = \begin{pmatrix} E_x \\ E_y \end{pmatrix}$, where $E_x$ and $E_y$ are the complex amplitudes of the electric field. The relations are:

$S_0 = |E_x|^2 + |E_y|^2$

$S_1 = |E_x|^2 - |E_y|^2$

$S_2 = 2 \Re(E_x^* E_y)$

$S_3 = -2 \Im(E_x^* E_y)$

Note: The sign convention for $S_3$ is chosen here to be consistent with the definition $S_3 = I_R - I_L$ and the common Jones vector representation of RHC as $\frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ -i \end{pmatrix}$. Different conventions exist, so care must be taken when consulting various sources.

As an example, consider a wave described by the Jones vector $\vec{J} = \begin{pmatrix} A \\ A \exp(i\pi/4) \end{pmatrix}$, where $A$ is a real amplitude. We can compute the Stokes parameters:

$S_0 = |A|^2 + |A \exp(i\pi/4)|^2 = A^2 + A^2 = 2A^2$

$S_1 = |A|^2 - |A \exp(i\pi/4)|^2 = A^2 - A^2 = 0$

To find $S_2$ and $S_3$, we compute the cross-term $E_x^* E_y = A^* (A \exp(i\pi/4)) = A^2 \exp(i\pi/4) = A^2(\cos(\pi/4) + i\sin(\pi/4)) = A^2(\frac{\sqrt{2}}{2} + i\frac{\sqrt{2}}{2})$.

$S_2 = 2 \Re(A^2(\frac{\sqrt{2}}{2} + i\frac{\sqrt{2}}{2})) = 2 \cdot A^2 \frac{\sqrt{2}}{2} = \sqrt{2}A^2$

$S_3 = -2 \Im(A^2(\frac{\sqrt{2}}{2} + i\frac{\sqrt{2}}{2})) = -2 \cdot A^2 \frac{\sqrt{2}}{2} = -\sqrt{2}A^2$

The resulting Stokes vector is $(2A^2, 0, \sqrt{2}A^2, -\sqrt{2}A^2)$. This describes a state of [elliptical polarization](@entry_id:270497), as expected. This connection provides a formal bridge between the two major formalisms for describing [polarized light](@entry_id:273160).