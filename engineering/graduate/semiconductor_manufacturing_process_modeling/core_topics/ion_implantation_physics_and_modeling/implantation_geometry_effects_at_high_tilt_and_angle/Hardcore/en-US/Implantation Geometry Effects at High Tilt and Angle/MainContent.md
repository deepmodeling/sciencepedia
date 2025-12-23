## Introduction
High-tilt and high-angle ion implantation has become an indispensable technique in the fabrication of modern three-dimensional [semiconductor devices](@entry_id:192345), such as FinFETs. By precisely directing dopant atoms at non-normal angles, engineers can create the complex, conformal doping profiles required for these advanced architectures. However, moving away from simple vertical implants introduces a host of intricate geometric effects that are challenging to predict and control. Phenomena like crystallographic channeling, geometric shadowing, and dose variation due to local topography can profoundly alter the final dopant distribution, posing a significant problem for [process control](@entry_id:271184) and device performance.

This article addresses this knowledge gap by providing a rigorous examination of implantation geometry effects. It is designed to equip you with the theoretical understanding and practical knowledge needed to master this critical process step. The first chapter, "Principles and Mechanisms," establishes the fundamental mathematical and physical framework, from defining the beam vector to explaining the mechanics of [ion channeling](@entry_id:158839) and [backscattering](@entry_id:142561). The second chapter, "Applications and Interdisciplinary Connections," explores how these principles are applied in real-world scenarios, including TCAD [process modeling](@entry_id:183557), FinFET fabrication, and [materials characterization](@entry_id:161346) techniques. Finally, the "Hands-On Practices" chapter will allow you to apply this knowledge to solve practical engineering problems, bridging the gap between theory and application.

## Principles and Mechanisms

The orientation of an ion beam relative to a semiconductor wafer is a critical parameter in modern implantation [process design](@entry_id:196705). High-tilt and high-angle implants are indispensable for creating complex, three-dimensional doping profiles in advanced devices such as FinFETs. However, these non-[normal incidence](@entry_id:260681) angles introduce a host of geometric effects that profoundly influence the final dopant distribution. Understanding these effects from first principles is essential for accurate [process modeling](@entry_id:183557) and control. This chapter elucidates the fundamental principles and mechanisms governing implantation geometry, from the basic mathematical description of the beam's direction to its complex interactions with the crystalline target and device topography.

### Geometric Specification of the Ion Beam

To analyze the effects of implantation geometry, we must first establish a precise mathematical framework for describing the ion beam's direction relative to the wafer. We define a right-handed orthonormal coordinate system, or basis, fixed to the wafer: $\{\hat{\mathbf{e}}_{x}, \hat{\mathbf{e}}_{y}, \hat{\mathbf{e}}_{z}\}$. By convention, $\hat{\mathbf{e}}_{z}$ is the unit vector normal to the wafer's surface, pointing outwards. The axes $\hat{\mathbf{e}}_{x}$ and $\hat{\mathbf{e}}_{y}$ lie in the plane of the wafer. Often, $\hat{\mathbf{e}}_{x}$ is aligned with a primary crystallographic direction, such as $[100]$, to serve as a reference.

The direction of the incident ion beam is specified by two angles: the **tilt angle**, $\theta$, and the **[azimuthal angle](@entry_id:164011)** (or **twist angle**), $\phi$.

-   The **tilt angle** $\theta$ is the angle between the ion beam's direction and the positive wafer normal, $+\hat{\mathbf{e}}_{z}$. A tilt of $\theta=0$ corresponds to [normal incidence](@entry_id:260681).
-   The **[azimuthal angle](@entry_id:164011)** $\phi$ is the angle of the beam's in-plane projection, measured in the wafer plane from the $+\hat{\mathbf{e}}_{x}$ axis towards the $+\hat{\mathbf{e}}_{y}$ axis.

The direction of the ion beam can be represented by a unit vector, $\hat{\mathbf{k}}$. To determine the components of this vector in the wafer basis, we can use spherical [coordinate transformation](@entry_id:138577) principles . The component of $\hat{\mathbf{k}}$ along the $\hat{\mathbf{e}}_{z}$ axis, $k_z$, is found by the projection of $\hat{\mathbf{k}}$ onto $\hat{\mathbf{e}}_{z}$. By definition of the dot product and the tilt angle $\theta$, this component is simply:

$k_z = \hat{\mathbf{k}} \cdot \hat{\mathbf{e}}_{z} = |\hat{\mathbf{k}}| |\hat{\mathbf{e}}_{z}| \cos\theta = \cos\theta$

The projection of the beam vector onto the $xy$-plane, $\hat{\mathbf{k}}_{xy}$, has a magnitude of $\sin\theta$. This in-plane vector's direction is specified by the [azimuthal angle](@entry_id:164011) $\phi$. Resolving this planar vector into its components along $\hat{\mathbf{e}}_{x}$ and $\hat{\mathbf{e}}_{y}$ yields:

$k_x = |\hat{\mathbf{k}}_{xy}| \cos\phi = \sin\theta \cos\phi$

$k_y = |\hat{\mathbf{k}}_{xy}| \sin\phi = \sin\theta \sin\phi$

Combining these components, the complete unit [direction vector](@entry_id:169562) for the ion beam is expressed as:

$\hat{\mathbf{k}}(\theta, \phi) = (\sin\theta \cos\phi)\hat{\mathbf{e}}_{x} + (\sin\theta \sin\phi)\hat{\mathbf{e}}_{y} + (\cos\theta)\hat{\mathbf{e}}_{z}$

This vector, often represented by its components in a row matrix $\begin{pmatrix} \sin\theta \cos\phi  \sin\theta \sin\phi  \cos\theta \end{pmatrix}$, is the fundamental starting point for all geometric calculations in ion implantation modeling.

### First-Order Geometric Effects of Tilt

When an ion beam strikes a wafer at a non-zero tilt angle, several direct geometric consequences arise, even before considering the atomic nature of the target.

#### Effective Dose and Path Length

For a beam with a given flux density $J_{\perp}$ (ions per unit area per unit time, measured in a plane perpendicular to the beam), the effective flux density on the wafer surface, $J_{\mathrm{eff}}$, is reduced. A surface [area element](@entry_id:197167) $dA_{\mathrm{wafer}}$ on the wafer presents a smaller cross-sectional area, $dA_{\perp} = dA_{\mathrm{wafer}}\cos\theta$, to the beam. Since the same number of ions pass through both areas, the flux density on the wafer is lower. This is a manifestation of **Lambert's cosine law**.

The [effective dose](@entry_id:915570), $D_{\mathrm{eff}}$, which is the total number of ions implanted per unit area of the wafer, is related to the nominal beam dose parameter, $D$, by this same cosine factor . If $D$ is the time-integrated flux through a plane normal to the beam, then the dose received by the wafer is:

$D_{\mathrm{eff}} = D \cos\theta$

This relationship shows that for high-tilt implants, the machine dose $D$ must be increased by a factor of $1/\cos\theta$ to achieve a desired [effective dose](@entry_id:915570) on the wafer.

Concurrently, an ion incident at tilt $\theta$ must travel a longer path, $s$, to reach a given vertical depth, $z$, below the surface. The relationship is purely geometric: $s = z / \cos\theta$. This increased path length means the ion will experience more stopping interactions to reach the same depth, a crucial factor in determining the final implant profile.

#### Projection of Range Statistics

Ions do not all stop at the same depth. Their stopping is a [stochastic process](@entry_id:159502), leading to a distribution of path lengths, characterized by a mean projected range $R_p$ and a standard deviation known as the **longitudinal straggle**, $\Delta R_p$. When implanting at a tilt angle $\theta$, this longitudinal spread along the beam's path is projected onto the wafer's coordinate system.

A key consequence is the creation of a **tilt-induced [lateral straggle](@entry_id:1127099)** . Even if the ions had no intrinsic lateral deviation from the beam axis, the variation in their stopping distance, $\Delta R_p$, causes them to stop at different lateral positions on the wafer. A simple geometric projection shows that the standard deviation of the lateral positions in the plane of incidence, $\Delta R_{\parallel}$, is given by:

$\Delta R_{\parallel} = \Delta R_p \sin\theta$

For a normal-incidence implant ($\theta=0$), this effect vanishes. However, for a high-tilt implant, it becomes a significant source of lateral broadening. For example, at a tilt of $\theta=45^\circ$, the induced [lateral straggle](@entry_id:1127099) is $\Delta R_p \sin(45^\circ) = \Delta R_p / \sqrt{2}$, which can be substantial. This geometric effect is distinct from and adds to the intrinsic [lateral straggle](@entry_id:1127099) caused by scattering events.

### Interaction with the Crystal Lattice: Ion Channeling

While the geometric effects described above apply to any target, the ordered atomic structure of a crystalline wafer introduces a uniquely important phenomenon: **[ion channeling](@entry_id:158839)**.

#### The Phenomenon of Channeling

When an ion's trajectory is closely aligned with a major crystallographic direction, it can be gently steered by the collective, [repulsive potential](@entry_id:185622) of rows (strings) or planes of atoms. This guiding effect confines the ion to the open "channels" within the crystal lattice, significantly altering its path and energy loss mechanisms.

We distinguish between two main types of channeling :
-   **Axial Channeling**: Occurs when the ion's trajectory is aligned with a low-index crystallographic axis (e.g., $\langle 100 \rangle$ or $\langle 110 \rangle$). The ion is confined in two dimensions by the cylindrically symmetric potentials of the surrounding atomic strings.
-   **Planar Channeling**: Occurs when the ion's trajectory is aligned with a low-index crystallographic plane (e.g., $\{100\}$ or $\{110\}$). The ion is confined in one dimension, oscillating between two adjacent atomic planes.

The key to channeling is the concept of **transverse energy**, $E_{\perp}$. The total kinetic energy $E$ of an ion can be decomposed into a longitudinal component along the channel and a transverse component perpendicular to it. The transverse energy is the sum of the transverse kinetic energy and the potential energy from the continuum potential of the lattice, $U(\mathbf{r}_{\perp})$. For an ion entering the crystal at a small angle $\psi$ to the channel direction, its initial transverse energy is approximately $E_{\perp} \approx E\psi^2$.

For an ion to remain channeled, its transverse energy must be less than the potential energy barrier $U_{\max}$ presented by the atomic strings or planes. This leads to the concept of a **[critical angle](@entry_id:275431)**, $\psi_c$. An ion entering the crystal at an angle $\psi > \psi_c$ will have too much transverse energy to be confined and will not channel. From the condition $E\psi_c^2 \approx U_{\max}$, we find that [the critical angle](@entry_id:169189) scales with energy as:

$\psi_c \propto \sqrt{\frac{U_{\max}}{E}} \propto E^{-1/2}$

This means that channeling is more probable at lower energies where the acceptance angle is larger. For typical implant energies (e.g., $100$ keV), critical angles are small, on the order of a few degrees or less. For instance, for $100$ keV Boron ions in silicon, [the critical angle](@entry_id:169189) for [planar channeling](@entry_id:1129717) might be $\psi_c \approx 0.57^\circ$ .

#### Channeling and Energy Loss

An ion moving through a solid loses energy via two primary mechanisms, the sum of which defines the total **[stopping power](@entry_id:159202)**, $S(E) = -dE/dx$ :
-   **Electronic Stopping ($S_e$)**: Energy loss due to [inelastic collisions](@entry_id:137360) with the target's electrons, causing ionization and excitation. This is a quasi-continuous process involving many small energy transfers.
-   **Nuclear Stopping ($S_n$)**: Energy loss due to elastic Coulomb collisions with the target's atomic nuclei. These are [discrete events](@entry_id:273637) that can cause large-angle scattering and displace lattice atoms (creating damage).

Channeling has a profound impact on both stopping components. A channeled ion travels predominantly through the center of the channel, a region of low electron density and, crucially, very far from any atomic nuclei. This has two effects:
1.  $S_n$ is drastically reduced, often by orders of magnitude, because the close encounters required for nuclear stopping are almost entirely prevented.
2.  $S_e$ is also reduced, but more moderately (e.g., by a factor of $\approx 2$), as the ion traverses a region of lower-than-average electron density.

Because the reduction in $S_n$ is so dramatic, electronic stopping becomes the overwhelmingly dominant energy loss mechanism for a well-channeled ion. The total stopping power is significantly lower, causing channeled ions to penetrate much deeper into the crystal than they would in an amorphous target. This creates the undesirable "channeling tail" in doping profiles.

A quantitative example illustrates this change vividly . In a simplified model, [nuclear stopping power](@entry_id:1128948) can be related to the logarithm of the ratio of maximum to minimum impact parameters, $S_n \propto \ln(b_{max}/b_{min})$. For a dechanneled ("random") trajectory, the minimum impact parameter $b_{min}$ is on the order of the atomic [screening length](@entry_id:143797), $a$. For a channeled ion, conservation of transverse energy forces the ion to stay far from atomic strings, resulting in a much larger effective $b_{min}$. When an ion beam's tilt is changed from a channeled condition (e.g., $\psi  \psi_c$) to a dechanneled one ($\psi > \psi_c$), $b_{min}$ reverts from a large value (e.g., $a\sqrt{3}$) back to $a$. This sudden increase in the probability of close collisions results in a sharp increase in $S_n$ and thus in the total [stopping power](@entry_id:159202). For a system like Boron in Silicon, this change can be on the order of several eV/nm.

### Controlling Implantation Profiles through Geometric Alignment

The strong dependence of ion range on crystal alignment means that controlling the implantation geometry is paramount for achieving reproducible doping profiles. The primary goal is often to *suppress* channeling to make the crystalline target behave like a more predictable amorphous material.

The most common technique for channeling suppression is to tilt the wafer relative to the beam by an angle significantly larger than [the critical angle](@entry_id:169189) for the major axes. A standard industrial practice is to use a tilt angle of $\theta \approx 7^\circ$. Since $\psi_c$ is typically less than a few degrees, this large tilt ensures that the initial transverse energy of the ions is far too high to permit channeling along the surface-normal axis .

However, for high-tilt implants (e.g., $\theta = 30^\circ$ to $45^\circ$) used for doping sidewalls of 3D structures, the situation is more complex. While the beam is not aligned with the surface-normal axis, it may become aligned with other major crystallographic planes that are not parallel to the surface. For a (001)-oriented silicon wafer, the vertical $\{110\}$ planes are a primary concern.

To suppress this residual [planar channeling](@entry_id:1129717), a second rotation is employed: the azimuthal or twist angle, $\phi$. The effectiveness of this rotation is magnified by the high tilt angle in a "[lever arm](@entry_id:162693)" effect . The angle $\alpha$ between the beam direction and a vertical crystal plane depends on both the tilt $\theta$ and the azimuthal misalignment $\Delta\phi$ from a channeling direction. For small misalignments, the relationship is approximately:

$\alpha \approx \theta \cdot |\Delta\phi|$ (for angles in radians)

This shows that a large tilt angle $\theta$ amplifies the effect of a small azimuthal twist $\Delta\phi$. For a high tilt of $\theta=30^\circ$, an azimuthal offset of just $\Delta\phi = 4^\circ$ can be enough to create a beam-to-plane angle $\alpha$ greater than a typical planar acceptance angle of $\psi_p = 2^\circ$. By setting the wafer with a specific azimuthal rotation (e.g., $\phi \approx 7^\circ$ for (001) Si), one can ensure that the beam is sufficiently misaligned from all major vertical planes, thereby effectively suppressing [planar channeling](@entry_id:1129717) even during a high-tilt implant.

### Advanced Geometric Considerations in High-Tilt Implantation

Beyond the primary effects, several other geometric factors become important in high-tilt scenarios, requiring more sophisticated modeling.

#### Ion Backscattering and Reflection

Not all ions that strike the wafer are implanted. Some may re-emerge from the surface through scattering processes. We can distinguish between two such processes :
-   **Reflection**: Ions that are scattered back into the vacuum after undergoing only one or a few collisions very near the surface.
-   **Backscattering**: Ions that penetrate to a finite depth, undergo a sequence of collisions that reverses their trajectory, and escape back through the surface.

The probability of both events increases significantly with increasing tilt angle $\theta$. At high tilts (grazing incidence), an ion travels a long path very close to the surface, increasing its chance of being scattered back out before it can lose a substantial amount of energy. Conversely, both probabilities decrease with increasing ion energy $E$, as the cross-section for the large-angle scattering required to reverse an ion's path decreases with energy. For high-tilt, low-energy implants, this loss of dose due to backscattering can be a significant effect that must be accounted for.

#### Beam Divergence and Profile Broadening

An ion beam is not perfectly collimated; it has an intrinsic angular spread known as **[beam divergence](@entry_id:269956)**. This can be modeled as small, random deviations in the tilt ($\delta\theta$) and azimuthal ($\delta\phi$) angles of individual ions, typically described by standard deviations $\sigma_{\theta}$ and $\sigma_{\phi}$.

At high tilt, this small angular spread is geometrically projected into a significant lateral spatial spread that increases with depth . An angular deviation $\delta\theta$ in the tilt direction, for example, results in a lateral displacement at depth $z$ that is approximately $\delta x \approx z \sec^2\alpha \cdot \delta\theta$, where $\alpha$ is the nominal tilt angle. This leads to a variance in the lateral position that scales with the square of the depth and is strongly amplified by the tilt angle:

$\operatorname{Var}[x] \approx z^2 \sec^4\alpha \cdot \sigma_{\theta}^2$

Similarly, an azimuthal deviation $\delta\phi$ leads to a variance in the orthogonal lateral direction:

$\operatorname{Var}[y] \approx z^2 \tan^2\alpha \cdot \sigma_{\phi}^2$

This shows that [beam divergence](@entry_id:269956) causes a depth-dependent, anisotropic broadening of the implant profile, an effect that is especially pronounced at high tilt angles and near mask edges where geometric shadowing is critical.

#### Complex Surface and Wafer Geometries

Real wafers are not perfectly flat, and device surfaces contain complex topography. The local angle of incidence, $\theta_{\mathrm{loc}}$, which truly governs the implantation physics, can differ substantially from the nominal machine tilt angle $\theta$. Factors such as **wafer miscut** (a slight intentional tilt of the wafer surface relative to the crystallographic planes) and **local topography** (e.g., sloped trench sidewalls) must be considered.

To find the true local incidence angle, one must compute the dot product of the beam vector $\mathbf{b}$ and the local surface [normal vector](@entry_id:264185) $\mathbf{n}_{\ell}$. Consider a case where the wafer is miscut by an angle $\alpha$ and a local facet is tilted by an angle $\beta$, both in the same azimuthal plane as the beam tilt $\theta$ . In this co-planar scenario, the total tilt of the local surface normal from the nominal vertical is simply $\alpha + \beta$. The angle between the beam and this local normal, $\theta_{\mathrm{loc}}$, is then given by the angle between two vectors in a plane, which is the difference of their individual angles:

$\cos\theta_{\mathrm{loc}} = \cos(\theta - (\alpha + \beta))$

This simple result highlights a critical point: small, seemingly negligible variations in wafer orientation or surface topography can lead to significant changes in the effective incidence angle, especially when they add to or subtract from a large nominal tilt angle. Accurate TCAD modeling of advanced devices therefore requires careful characterization and inclusion of these detailed geometric effects.