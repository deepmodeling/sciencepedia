## Introduction
Grain boundaries, the interfaces between crystalline grains in a polycrystalline material, are fundamental microstructural features that exert profound control over material behavior. From the strength of structural metals to the performance of superconducting wires, the properties of these interfaces are critical. To engineer materials with desired performance, we must first develop a rigorous understanding of the geometry, structure, and energetics of grain boundaries. This article provides a comprehensive journey into the science of these interfaces, structured across three core chapters. The first chapter, **Principles and Mechanisms**, lays the mathematical and physical foundation, detailing how to describe misorientation and modeling the structure and energy of interfaces. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates how these principles govern real-world phenomena, including mechanical properties, transport, and microstructural evolution across various scientific fields. Finally, the **Hands-On Practices** section offers practical exercises to reinforce these complex concepts. We begin by establishing the essential language needed to describe any grain boundary: the mathematical framework of crystalline orientation and [misorientation](@entry_id:1127952).

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms governing grain boundaries. We will begin by establishing a rigorous mathematical framework to describe crystalline orientation and misorientation, the essential geometric variables defining an interface. Subsequently, we will explore the profound impact of [crystal symmetry](@entry_id:138731) on this description. With this foundation, we will then examine the static properties of grain boundaries, including their geometric character, energetic landscapes, and atomistic structure. Finally, we will turn our attention to the dynamic behavior of these interfaces, exploring the principles of [grain boundary](@entry_id:196965) motion, mobility, and the intriguing phenomenon of shear-coupled migration.

### The Mathematical Description of Crystalline Orientation and Misorientation

The properties and behavior of a [grain boundary](@entry_id:196965) are fundamentally dictated by its geometry. To quantify this geometry, we must first develop a precise language for describing the orientation of a crystal and the relative orientation—or [misorientation](@entry_id:1127952)—between two adjacent crystals.

#### The Concept of Orientation

In a polycrystalline specimen, it is customary to define a global, fixed coordinate system known as the **specimen frame**. This is a right-handed orthonormal basis, which we can denote as $\{\mathbf{e}_1, \mathbf{e}_2, \mathbf{e}_3\}$. Each crystalline grain within the specimen also possesses its own intrinsic coordinate system, tied to its [crystal lattice structure](@entry_id:185398), known as the **crystal frame**. For cubic crystals, this frame is naturally aligned with the cube axes, e.g., $[100]$, $[010]$, and $[001]$. We can also represent this as a right-handed [orthonormal basis](@entry_id:147779), $\{\mathbf{c}_1, \mathbf{c}_2, \mathbf{c}_3\}$.

The **crystallographic orientation** of a grain is the transformation that aligns the specimen frame with the crystal frame. This transformation must be a rotation, as it must preserve both the lengths of vectors (e.g., [lattice parameters](@entry_id:191810)) and the handedness of the coordinate system. Such transformations are mathematically described by elements of the **Special Orthogonal Group in three dimensions**, denoted as $\mathrm{SO}(3)$. An orientation is thus represented by a $3 \times 3$ matrix $g \in \mathrm{SO}(3)$ which satisfies $g^T g = I$ (where $I$ is the identity matrix) and $\det(g) = 1$. This matrix $g$ can be interpreted as an active rotation that takes the crystal from a reference state (where its axes are aligned with the specimen frame) to its current orientation. Equivalently, it can be viewed as a passive transformation that changes the coordinates of a vector from the crystal frame to the specimen frame . If a physical vector $\mathbf{v}$ has coordinates $v_c$ in the crystal frame and $v_s$ in the specimen frame, their relationship is $v_s = g v_c$.

#### Representing Rotations

While a $3 \times 3$ matrix is a complete representation of a rotation, it is not always the most intuitive or computationally convenient. Two other representations are particularly important in [materials simulation](@entry_id:176516): the axis-angle pair and the unit quaternion.

A rotation can be uniquely described by a [unit vector](@entry_id:150575) $\hat{n}$ representing the **[axis of rotation](@entry_id:187094)** and a scalar $\theta$ representing the **angle of rotation** in a right-handed sense about that axis. This $(\hat{n}, \theta)$ pair is geometrically intuitive. To find the corresponding matrix $g \in \mathrm{SO}(3)$, we can use the **Rodrigues' rotation formula**. The derivation follows from decomposing an arbitrary vector $\mathbf{v}$ into components parallel ($v_{\parallel}$) and perpendicular ($v_{\perp}$) to the rotation axis $\hat{n}$. The parallel component remains unchanged by the rotation, while the perpendicular component is rotated by $\theta$ in the plane normal to $\hat{n}$. This geometric reasoning leads to the expression for the rotated vector $\mathbf{v}' = g\mathbf{v}$:

$$
\mathbf{v}' = \mathbf{v}\cos(\theta) + (\hat{n} \times \mathbf{v})\sin(\theta) + \hat{n}(\hat{n} \cdot \mathbf{v})(1-\cos(\theta))
$$

By expressing the [cross product](@entry_id:156749) and [outer product](@entry_id:201262) as matrix operations, one can derive the explicit [rotation matrix](@entry_id:140302) $g(\hat{n}, \theta)$ . A more compact form of this is:

$$
g(\hat{n}, \theta) = \mathbf{I} + \sin(\theta)[\hat{n}]_{\times} + (1-\cos(\theta))[\hat{n}]_{\times}^2
$$

where $[\hat{n}]_{\times}$ is the skew-symmetric matrix representation of the [cross product](@entry_id:156749) with $\hat{n}$. The final matrix expression is:
$$
g = \begin{pmatrix}
\cos(\theta) + n_x^2(1-\cos(\theta)) & n_x n_y(1-\cos(\theta)) - n_z\sin(\theta) & n_x n_z(1-\cos(\theta)) + n_y\sin(\theta) \\
n_y n_x(1-\cos(\theta)) + n_z\sin(\theta) & \cos(\theta) + n_y^2(1-\cos(\theta)) & n_y n_z(1-\cos(\theta)) - n_x\sin(\theta) \\
n_z n_x(1-\cos(\theta)) - n_y\sin(\theta) & n_z n_y(1-\cos(\theta)) + n_x\sin(\theta) & \cos(\theta) + n_z^2(1-\cos(\theta))
\end{pmatrix}
$$

An alternative and often superior representation for computation is the **unit [quaternion](@entry_id:1130460)**. A unit [quaternion](@entry_id:1130460) $q$ is a four-component entity $q = (q_0, q_1, q_2, q_3)$ where $q_0^2 + q_1^2 + q_2^2 + q_3^2 = 1$. The relationship to the [axis-angle representation](@entry_id:186186) is particularly elegant:

$$
q = (\cos(\theta/2), \hat{n} \sin(\theta/2)) = (\cos(\theta/2), n_x \sin(\theta/2), n_y \sin(\theta/2), n_z \sin(\theta/2))
$$

Here, $q_0$ is the scalar part and $(q_1, q_2, q_3)$ is the vector part. The composition of two rotations corresponds to [quaternion multiplication](@entry_id:154753), which is computationally more efficient and numerically more stable than [matrix multiplication](@entry_id:156035). This representation also avoids the singularities ([gimbal lock](@entry_id:171734)) that can plague other three-parameter representations like Euler angles.

#### The Concept of Misorientation

The central quantity describing a grain boundary is the **[misorientation](@entry_id:1127952)**, which is the relative rotation between the two adjacent grains. Given two grains with absolute orientations $g_1$ and $g_2$, the [misorientation](@entry_id:1127952) $g_{\Delta}$ is the rotation that maps the crystal frame of grain 1 onto the crystal frame of grain 2. This composition of rotations is expressed as $g_2 = g_{\Delta} g_1$. The misorientation is therefore found by:

$$
g_{\Delta} = g_2 g_1^{-1}
$$

Since the inverse of a [rotation matrix](@entry_id:140302) is its transpose ($g_1^{-1} = g_1^T$), this is straightforward to compute. In the [quaternion representation](@entry_id:753974), the inverse of a unit quaternion $q$ is its conjugate $q^* = (q_0, -q_1, -q_2, -q_3)$. The [misorientation](@entry_id:1127952) quaternion is then given by the [quaternion](@entry_id:1130460) product $q_{\Delta} = q_2 q_1^*$. From the resulting misorientation [quaternion](@entry_id:1130460) $q_{\Delta} = (q_{\Delta,0}, \mathbf{q}_{\Delta})$, the [misorientation](@entry_id:1127952) angle $\Theta$ can be extracted directly from the scalar part: $\Theta = 2 \arccos(q_{\Delta,0})$ .

An essential property of [misorientation](@entry_id:1127952) is its behavior under a change of the arbitrary specimen frame. If the specimen frame is rotated by a matrix $R \in \mathrm{SO}(3)$, the new absolute orientations become $g'_1 = R g_1$ and $g'_2 = R g_2$. The new misorientation, $g'_{\Delta}$, is:

$$
g'_{\Delta} = g'_2 (g'_1)^{-1} = (R g_2) (R g_1)^{-1} = R g_2 g_1^{-1} R^{-1} = R g_{\Delta} R^{-1}
$$

This type of transformation, known as a **conjugation** or [similarity transformation](@entry_id:152935), is fundamentally different from the left-multiplication that transforms absolute orientations. A key consequence is that the trace of the [misorientation](@entry_id:1127952) matrix is invariant under changes of the specimen frame: $\mathrm{Tr}(g'_{\Delta}) = \mathrm{Tr}(R g_{\Delta} R^{-1}) = \mathrm{Tr}(g_{\Delta})$. Since the rotation angle $\theta$ is related to the trace by $\mathrm{Tr}(g_{\Delta}) = 1 + 2\cos(\theta)$, this proves that the misorientation angle is an **intrinsic, frame-independent property** of the grain boundary. The same is true for the [misorientation](@entry_id:1127952) axis. This is physically crucial, as the properties of an interface must depend on its intrinsic nature, not on the arbitrary coordinate system chosen by the observer .

### The Role of Crystal Symmetry

The mathematical description of [misorientation](@entry_id:1127952) is further refined by considering the inherent symmetry of the crystal lattice.

#### The Misorientation Equivalence Class

A crystal lattice is left unchanged by a set of [symmetry operations](@entry_id:143398) (rotations, reflections) that form its **[point group](@entry_id:145002)**. For the purpose of orientation, we are concerned with the rotational symmetries, which form a subgroup of $\mathrm{SO}(3)$. For cubic crystals, this is the **octahedral group**, which has 24 distinct rotational symmetries.

If $s$ is a symmetry rotation of a crystal, then an orientation $g$ is physically indistinguishable from the orientation $g s$, since the latter simply corresponds to applying a symmetry operation to the crystal's own frame, which leaves the lattice invariant. This has a profound implication for [misorientation](@entry_id:1127952). Given a misorientation $g_{\Delta} = g_2 g_1^{-1}$, we can apply any symmetry operation $s_1$ to grain 1 and any symmetry operation $s_2$ to grain 2 without changing their physical state. The misorientation between these symmetrically-related orientations is:

$$
g'_{\Delta} = (g_2 s_2) (g_1 s_1)^{-1} = g_2 s_2 s_1^{-1} g_1^{-1}
$$

This expression is not quite right. A symmetry operation $s$ is defined in the crystal frame. If an orientation $g$ maps the crystal frame to the specimen frame, the same symmetry operation expressed in the specimen frame is $g s g^{-1}$. However, a more direct approach is to consider the equivalence from first principles. A misorientation $g_\Delta$ relates the frames of grain 1 and 2. Any [misorientation](@entry_id:1127952) $g'_\Delta$ that relates the frame of grain 1 (under symmetry $s_1$) to the frame of grain 2 (under symmetry $s_2$) is physically equivalent. This leads to the correct expression for the set of equivalent misorientations  :

$$
[g_{\Delta}] = \{ s_2 g_{\Delta} s_1^{-1} \mid s_1, s_2 \in S \}
$$

where $S$ is the crystal's [rotational symmetry](@entry_id:137077) group. This set is called the **[misorientation](@entry_id:1127952) [equivalence class](@entry_id:140585)**. All rotations in this set describe the same physical grain boundary. For cubic crystals, there are $24 \times 24 = 576$ such symmetrically equivalent rotations for a general misorientation.

In practice, we select a single, unique representative from this large set, known as the **canonical misorientation**. By convention, this is the rotation with the minimum possible angle, $\theta_{\min}$. A powerful illustration of this principle arises when the misorientation itself is a symmetry operation . For instance, consider two cubic grains where the calculated [misorientation](@entry_id:1127952) is a $90^{\circ}$ rotation about the $[001]$ axis. Since a $90^{\circ}$ rotation about a cube axis is a symmetry operation of the cubic group, let's call it $s_{90}$. This means $g_\Delta = s_{90} \in S$. We can then find an equivalent [misorientation](@entry_id:1127952) by choosing $s_1 = I$ (identity) and $s_2 = s_{90}^{-1}$ (the inverse, which is also in $S$). The equivalent [misorientation](@entry_id:1127952) is:

$$
g'_{\Delta} = s_2 g_{\Delta} s_1^{-1} = (s_{90}^{-1}) (s_{90}) (I^{-1}) = I
$$

The identity matrix corresponds to a rotation angle of $0^{\circ}$. Thus, even though the nominal [misorientation](@entry_id:1127952) was $90^{\circ}$, the minimal, physically meaningful [misorientation](@entry_id:1127952) angle is $0^{\circ}$. This signifies that the two [crystal lattices](@entry_id:148274) are, in fact, perfectly aligned after accounting for symmetry.

#### The Misorientation Fundamental Zone

The set of all canonical misorientations (i.e., all minimum-angle representatives) for a given [crystal symmetry](@entry_id:138731) forms a compact region in the space of all rotations called the **misorientation fundamental zone (MFZ)**. This zone contains exactly one representative for every possible distinct physical [misorientation](@entry_id:1127952) between two crystals of a given symmetry.

For cubic symmetry, the MFZ has a well-defined, though complex, shape in axis-angle space .
1.  The rotation axis $\hat{n}$ is confined to a single standard stereographic triangle on the unit sphere, typically the one with vertices at the high-symmetry directions $[001]$, $[011]$, and $[111]$.
2.  For each axis direction $\hat{n}$ within this triangle, the misorientation angle $\theta$ is limited to a range $[0, \theta_{\text{max}}(\hat{n})]$. The maximum angle $\theta_{\text{max}}$ is not constant but varies with the axis direction, reaching specific values along the high-symmetry directions that bound the triangle. For instance, for an axis along $[001]$, the $4$-fold symmetry limits the maximum unique angle to $45^{\circ}$, so $\theta_{\text{max}}([001]) = \pi/4$. For an axis along $[111]$, the $3$-fold symmetry limits $\theta_{\text{max}}([111]) = \pi/3$.

It is crucial to distinguish this 3D [misorientation](@entry_id:1127952) fundamental zone from the 2D **orientation fundamental zone (OFZ)**. The OFZ is simply the standard stereographic triangle itself (e.g., the $[001]-[011]-[111]$ triangle). It is a region of *directions* on the unit sphere, used to represent a single unique crystal direction (like a [pole figure](@entry_id:260961)). In contrast, the MFZ is a region of *rotations*—a 3D volume in rotation space representing unique relative orientations between two crystals. The OFZ can be thought of as the "base" of the MFZ in axis space, upon which the angle coordinate is built up to a varying height $\theta_{\text{max}}(\hat{n})$ .

### Geometric and Energetic Characterization of Grain Boundaries

With a full understanding of misorientation, we can now characterize the grain boundary itself, which requires knowledge of both the misorientation and the boundary plane's orientation.

#### The Five Degrees of Freedom of a Grain Boundary

On a macroscopic scale, a planar grain boundary is fully described by **five degrees of freedom (DOF)** . These are:
1.  **Three degrees of freedom for misorientation**: These parameters specify the relative rotation between the two grains (e.g., the three components of an axis-angle or [quaternion representation](@entry_id:753974)).
2.  **Two degrees of freedom for the boundary plane normal**: These parameters specify the orientation of the interface plane itself. The plane's orientation is defined by its [unit normal vector](@entry_id:178851), $\mathbf{\hat{n}}$, which, being a point on the unit sphere, can be described by two angles (e.g., polar and azimuthal angles).

Note that this 5-DOF description is macroscopic. At the atomic scale, additional microscopic degrees of freedom, such as rigid-body translations of one crystal relative to the other parallel to the boundary plane, also exist.

Based on the relationship between the misorientation axis $\mathbf{\hat{a}}$ and the boundary plane normal $\mathbf{\hat{n}}$, we can define two special, high-symmetry boundary types :
-   A **pure twist boundary** is one where the misorientation axis is perpendicular to the boundary plane (i.e., $\mathbf{\hat{a}}$ is parallel to $\mathbf{\hat{n}}$). This corresponds to rotating one crystal relative to the other "in the plane" of the boundary.
-   A **pure tilt boundary** is one where the misorientation axis lies within the boundary plane (i.e., $\mathbf{\hat{a}}$ is perpendicular to $\mathbf{\hat{n}}$, so $\mathbf{\hat{a}} \cdot \mathbf{\hat{n}} = 0$).

For example, a boundary in a cubic crystal with a misorientation axis along $[001]$ and a boundary plane normal to $[010]$ is a pure tilt boundary, since the dot product of these two orthogonal directions is zero. General boundaries have a mixed tilt and twist character.

#### Grain Boundary Energy

The **[grain boundary energy](@entry_id:136501)**, $\gamma$, is the excess free energy per unit area of the interface. It is a fundamental property that dictates microstructural stability and evolution. The energy $\gamma$ is a complex function of all five macroscopic DOFs, as well as temperature. Its dependence on [misorientation](@entry_id:1127952) angle $\theta$ is particularly characteristic .

For **[low-angle grain boundaries](@entry_id:196592)** (typically $\theta \lesssim 15^\circ$), the interface structure can be modeled as a periodic array of crystal dislocations. According to the **Read-Shockley model**, the boundary energy is proportional to the density of these dislocations. Since dislocation spacing is inversely proportional to $\theta$ for small angles, the energy increases with [misorientation](@entry_id:1127952), following a relation of the form $\gamma(\theta) \approx E_0 \theta (A - \ln \theta)$, where $E_0$ and $A$ are material constants.

For **high-angle grain boundaries** ($\theta \gtrsim 15^\circ$), the dislocation cores overlap, and this model breaks down. The boundary is a more complex, disordered region. In general, the energy is high and relatively insensitive to small changes in $\theta$. However, this high-energy "plateau" is punctuated by sharp, deep energy minima or **cusps** at specific misorientations. These special misorientations correspond to the formation of a **Coincidence Site Lattice (CSL)**.

#### Special Boundaries: CSL and Structural Units

A **Coincidence Site Lattice (CSL)** is a superlattice formed by the [lattice points](@entry_id:161785) that are common to both interpenetrating [crystal lattices](@entry_id:148274) at a specific [misorientation](@entry_id:1127952) . The fraction of coincident sites is given by $1/\Sigma$, where $\Sigma$ is the **CSL index**. Boundaries with low $\Sigma$ values (e.g., $\Sigma 3, \Sigma 5, \Sigma 11$ in cubic crystals) can achieve a high degree of atomic fit and [periodic structure](@entry_id:262445), resulting in exceptionally low [grain boundary energy](@entry_id:136501).

As a concrete example, consider a [misorientation](@entry_id:1127952) in a [simple cubic](@entry_id:150126) crystal generated by a rotation about the $[001]$ axis such that $\cos\theta = 3/5$ . A lattice vector $(x,y,z)$ with integer components belongs to the CSL if its rotated counterpart is also an integer vector. This condition leads to a system of [linear congruences](@entry_id:150485), which in this case reduces to $3x+4y \equiv 0 \pmod 5$ and $-4x+3y \equiv 0 \pmod 5$. The solution to this system is a sublattice of the parent lattice. The volume of the CSL unit cell relative to the parent lattice unit cell defines $\Sigma$. For this [specific rotation](@entry_id:175970), we find that the CSL is spanned by vectors like $(2,1,0)$, $(1,3,0)$, and $(0,0,1)$ in the parent basis. The determinant of the [transformation matrix](@entry_id:151616) formed by these vectors gives $\Sigma = 5$. This is the well-known $\Sigma 5$ CSL boundary.

While the CSL model is powerful for explaining energy cusps, a more general framework is the **Structural Unit Model (SUM)** . This model proposes that the structure of any grain boundary can be described as a specific periodic arrangement, or "tiling," of a small number of fundamental **structural units**. These units are small, characteristic [atomic clusters](@entry_id:193935). For a given CSL misorientation, there can exist different low-energy boundary planes. For example, for the $\Sigma 11$ misorientation about a $[110]$ tilt axis in FCC crystals, two prominent [symmetric tilt boundary](@entry_id:187640) planes are the $\{113\}$ and $\{332\}$ planes. These are known as **conjugate boundary planes** because they share the same [misorientation](@entry_id:1127952) but have different boundary plane inclinations. According to the SUM, they are composed of the same fundamental structural units but arranged in different sequences. The $\{113\}$ boundary might be a simple tiling of one type of unit, while the $\{332\}$ boundary might have a more complex tiling involving the same unit interspersed with steps or segments of perfect crystal. The specific Burgers vectors of the dislocations that compose these boundaries are drawn from the **Displacement Shift Complete (DSC) lattice**, which is the lattice of vectors that translate the entire bicrystal structure back into registry.

### Grain Boundary Kinetics

Beyond static structure, the dynamic behavior of grain boundaries is critical to processes like [grain growth](@entry_id:157734), [recrystallization](@entry_id:158526), and [phase transformations](@entry_id:200819).

#### Grain Boundary Motion: Mobility and Driving Forces

Grain boundary motion is a [thermally activated process](@entry_id:274558) that occurs in response to a thermodynamic **driving pressure**, $P$. This pressure can arise from various sources. A common intrinsic source is [capillarity](@entry_id:144455), where a curved boundary segment with curvature $\kappa$ and energy $\gamma$ experiences a pressure to flatten, given by the **Laplace pressure** $P = \gamma \kappa$.

In many regimes, the boundary's normal velocity, $v_n$, is linearly proportional to the [driving pressure](@entry_id:893623). This relationship defines the **[grain boundary mobility](@entry_id:192363)**, $M$:

$$
v_n = M P
$$

The mobility $M$ is an intrinsic kinetic property of the interface. It is not a universal constant but depends strongly on temperature (often following an Arrhenius law), boundary character (all 5 DOFs), and impurity content. However, within the [linear response](@entry_id:146180) regime, it is considered independent of the magnitude of the driving pressure $P$ itself .

#### Shear-Coupled Motion

For a long time, it was assumed that a normal driving force would only produce normal boundary motion. However, it is now well-established that for many boundaries, normal motion is intrinsically coupled to a tangential translation of one grain relative to the other. This phenomenon is known as **shear-coupled grain boundary motion**.

This coupling is quantified by the **shear-coupling factor**, $\beta$, defined as the ratio of the tangential velocity ($v_t$) to the normal velocity ($v_n$):

$$
\beta = \frac{v_t}{v_n} = \frac{\Delta x}{\Delta h}
$$

where $\Delta x$ and $\Delta h$ are the tangential and normal displacements over a time interval.
-   If $\beta = 0$, the boundary exhibits **pure migration** (non-coupled motion).
-   If $\beta \neq 0$, the boundary exhibits **shear-coupled motion**.

The profound consequence of shear coupling is that a purely normal driving force, like [capillarity](@entry_id:144455), can cause the grains to shear relative to one another, generating macroscopic shear strain in the material *even in the complete absence of any externally applied shear stress* ($\tau=0$) . This is a classic example of cross-phenomena in [non-equilibrium thermodynamics](@entry_id:138724). For instance, given a boundary with $\gamma=0.5\,\mathrm{J/m^2}$ and $\kappa=1.0\times 10^6\,\mathrm{m^{-1}}$, the [driving pressure](@entry_id:893623) is $P=5.0 \times 10^5\,\mathrm{J/m^3}$. If this boundary is observed to move with $v_n=1.0\times 10^{-8}\,\mathrm{m/s}$ while producing a tangential displacement of $\Delta x = 5.0\times 10^{-9}\,\mathrm{m}$ for every normal displacement of $\Delta h = 1.0\times 10^{-8}\,\mathrm{m}$, we can directly calculate its kinetic coefficients. The mobility is $M = v_n/P = 2.0 \times 10^{-14}\,\mathrm{m^4/(J\cdot s)}$, and the shear-coupling factor is $\beta = \Delta x / \Delta h = 0.5$.

The microscopic mechanism for shear coupling is the motion of line defects within the [grain boundary](@entry_id:196965) known as **disconnections**. These defects possess both a step character (a height component normal to the boundary) and a dislocation character (a Burgers vector component parallel to the boundary). The glide of a population of such disconnections across the interface necessarily causes the boundary to migrate (due to the step motion) and the grains to shear (due to the transport of the Burgers vectors).