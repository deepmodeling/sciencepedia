## Introduction
The geometry of a Positron Emission Tomography (PET) scanner is not merely a passive housing for its detectors; it is the active and defining framework that dictates the system's ultimate diagnostic power. From the path of a single photon pair to the final reconstructed image, every step in the PET imaging chain is governed by precise geometric principles. Understanding the direct link between the physical layout of the scanner and the quality of the resulting image is essential for grasping both the profound capabilities and the inherent limitations of modern nuclear medicine. This article addresses this crucial knowledge area by dissecting the geometric foundations of PET imaging.

Across the following chapters, you will gain a comprehensive understanding of this topic. The first chapter, **Principles and Mechanisms**, establishes the foundational concepts, from the coordinate systems used to define the scanner space to the physical effects like parallax error that arise from the gantry's construction. You will learn how raw event data is captured and organized. Next, the chapter on **Applications and Interdisciplinary Connections** reveals how these geometric principles are exploited to enhance performance through advanced techniques like Time-of-Flight (TOF) and are central to the function of [hybrid systems](@entry_id:271183) like PET/CT and PET/MR. Finally, a series of **Hands-On Practices** will allow you to apply these concepts, solidifying your understanding of how geometric calculations translate into quantitative measures of system performance and image quality.

## Principles and Mechanisms

The process of forming an image in Positron Emission Tomography (PET) is fundamentally geometric. It begins with the detection of a physical event at two distinct points in space and culminates in the reconstruction of a three-dimensional activity map. Understanding the geometry of the scanner, the paths of the detected photons, and the organization of the acquired data is therefore essential to comprehending the capabilities and limitations of PET imaging. This chapter details the core principles and mechanisms governing this geometric framework, from the macroscopic structure of the gantry down to the physical effects that define the ultimate performance of the system.

### Gantry Geometry and Coordinate Systems

The typical PET scanner gantry is constructed as a cylindrical assembly of detectors designed to completely surround the patient. For the purpose of geometric modeling, we begin by idealizing this gantry as a perfect cylinder. To describe events within this space, we establish a standard three-dimensional Cartesian coordinate system.

By convention, the origin $(0,0,0)$ is placed at the geometric center of the gantry. The axis of the cylinder, which corresponds to the direction of patient travel, is designated as the **axial direction** and aligns with the $z$-axis. The plane perpendicular to this axis (the $xy$-plane) is known as the **transaxial plane**. The basis vectors ${\hat{\mathbf{x}}, \hat{\mathbf{y}}, \hat{\mathbf{z}}}$ form a [right-handed system](@entry_id:166669). A point on the detector cylinder of radius $R$ can be described by its axial position $z$ and its [azimuthal angle](@entry_id:164011) $\phi$ in the transaxial plane. The corresponding Cartesian coordinates of such a detection point $\mathbf{p}$ are given by:
$$
\mathbf{p} = (R\cos\phi, R\sin\phi, z)
$$

A single PET event is recorded when two gamma photons, originating from a single [annihilation](@entry_id:159364), are detected in coincidence by two detector elements. These two detection points, let us call them $\mathbf{p}_1$ and $\mathbf{p}_2$, define a crucial geometric entity: the **Line of Response (LOR)**. In its idealized form, the LOR is the straight line passing through $\mathbf{p}_1$ and $\mathbf{p}_2$.

Mathematically, this line can be represented parametrically as $\mathbf{r}(l) = \mathbf{r}_0 + l\hat{\mathbf{u}}$, where $\hat{\mathbf{u}}$ is a [unit vector](@entry_id:150575) specifying the line's direction and $\mathbf{r}_0$ is a point on the line. A physically meaningful and robust parameterization, which is invariant to the arbitrary ordering of the two detection points, is essential for data processing. A standard choice is to define the [direction vector](@entry_id:169562) $\hat{\mathbf{u}}$ as the normalized vector connecting the points, and the base point $\mathbf{r}_0$ as their midpoint [@problem_id:4907370].
$$
\hat{\mathbf{u}} = \frac{\mathbf{p}_2 - \mathbf{p}_1}{\|\mathbf{p}_2 - \mathbf{p}_1\|} \quad \text{and} \quad \mathbf{r}_0 = \frac{\mathbf{p}_1 + \mathbf{p}_2}{2}
$$
With this definition, the line passes through both detection points (at $l = \pm \|\mathbf{p}_2 - \mathbf{p}_1\|/2$). If the labels of the points are swapped, $\mathbf{r}_0$ remains unchanged, while $\hat{\mathbf{u}}$ reverses its sign. This reversal merely corresponds to traversing the same geometric line in the opposite direction, leaving the physical LOR itself invariant.

### Detector Arrangement and Acceptance Angle

While the gantry can be modeled as a continuous cylinder, it is in fact composed of discrete components. Modern PET scanners arrange scintillation crystals into **detector blocks**, which are then assembled into rings. A single ring is composed of $B$ blocks, with each block containing an array of crystals. For instance, a block might contain $M$ crystals arranged tangentially.

To precisely locate any given crystal, we must account for the **crystal pitch** ($p$), which is the center-to-center distance between adjacent crystals within a block, and the **inter-block gap** ($g$), a non-sensitive space between neighboring blocks. Consider a ring of radius $R$ (measured to the crystal centers). Let us index the blocks by $b \in \{0, 1, \dots, B-1\}$ and the crystals within a block by $j \in \{0, 1, \dots, M-1\}$. If we set the center of crystal $(b=0, j=0)$ as our reference at an angle of $\theta=0$, the [angular position](@entry_id:174053) $\theta_{b,j}$ of any other crystal $(b,j)$ can be found by summing the arc lengths along the circle [@problem_id:4907378]. The total arc length from the reference to crystal $(b,j)$ is the sum of the distances across all traversed crystal pitches and all traversed inter-block gaps:
$$
s_{b,j} = \underbrace{p \cdot (bM + j)}_{\text{crystal pitches}} + \underbrace{g \cdot b}_{\text{inter-block gaps}}
$$
The [angular position](@entry_id:174053) in radians is then $\theta_{b,j} = s_{b,j} / R$. From this, the Cartesian coordinates of the crystal's center are found by the standard conversion:
$$
(x_{b,j}, y_{b,j}) = (R\cos(\theta_{b,j}), R\sin(\theta_{b,j}))
$$
This detailed mapping is fundamental for the system's calibration and for the accurate determination of LORs during [data acquisition](@entry_id:273490).

The physical dimensions of the detectors also define the gantry's ability to "see" or accept photons from a source. For a [point source](@entry_id:196698) at the center of the gantry, the **acceptance angle** quantifies the cone of emission that a single detector can intercept. Considering a detector of transaxial width $w$ and axial height $h$ at a radius $R$, the transaxial and axial acceptance half-angles, $\alpha_t$ and $\alpha_z$, can be found using basic trigonometry. From the center, the detector edges are at a transverse distance of $w/2$ and an axial distance of $h/2$. This forms two right triangles, giving the relations [@problem_id:4907416]:
$$
\tan(\alpha_t) = \frac{w/2}{R} \quad \text{and} \quad \tan(\alpha_z) = \frac{h/2}{R}
$$
These angles, which depend on the ratio of detector size to gantry radius, are directly related to the geometric sensitivity of the scanner. The radial thickness of the crystal, $t$, does not influence this idealized acceptance angle, though it has profound effects on spatial resolution, as we will see later.

### Organization of Acquired Data

A PET scan can generate billions of coincidence events. The method used to store and organize this data has significant implications for image reconstruction and data analysis.

#### List-Mode Data

The most fundamental format for storing PET data is **list-mode**. In this mode, each coincidence event is recorded individually as an entry in a list. Each entry, or tuple, typically contains the identities of the two detector crystals involved and the measured **[time-of-flight](@entry_id:159471) (TOF)** difference, $\Delta t$ [@problem_id:4907338]. The crystal identities directly provide the endpoints $(\mathbf{r}_1, \mathbf{r}_2)$ of the LOR.

The TOF difference, $\Delta t = t_1 - t_2$, where $t_1$ and $t_2$ are the photon arrival times, provides information about the probable location of the [annihilation](@entry_id:159364) along the LOR. The path length difference between the two photons is $c \cdot \Delta t$, where $c$ is the speed of light. This corresponds to a displacement, $\delta$, from the LOR's midpoint given by:
$$
\delta = \frac{c \cdot \Delta t}{2}
$$
For instance, a measured TOF difference of $\Delta t = 450 \text{ ps}$ implies a displacement of approximately $\delta = 67.5 \text{ mm}$ from the center of the LOR.

List-mode data is the most complete representation of the acquired information. It preserves the exact geometric LOR for every event and the continuous-valued TOF measurement, offering maximum flexibility for advanced reconstruction algorithms. Its primary drawback is the large file size.

#### Binned Data: Sinograms and Michelograms

For many reconstruction techniques, particularly filtered back-projection (FBP), and to manage data size, list-mode data is often histogrammed or "binned" into projection [data structures](@entry_id:262134). This process, however, involves a loss of information.

In a 2D scanner (or a single ring of a 3D scanner), LORs are organized into a **sinogram**. Each LOR in the transaxial plane can be uniquely parameterized by the pair $(s, \phi)$, where $\phi \in [0, \pi)$ is the angle of the LOR's normal vector, and $s$ is the signed [perpendicular distance](@entry_id:176279) from the origin to the LOR. To create a digital sinogram, this continuous $(s, \phi)$ space is discretized into a grid of bins. An event recorded between two crystals is first mapped to its continuous $(s, \phi)$ coordinates, and then assigned to a discrete bin index pair $(i_s, i_\phi)$ [@problem_id:4907372]. For example, an LOR along the $x$-axis passes through the origin, giving $s=0$. Its normal vector is along the $y$-axis, corresponding to an angle of $\phi = \pi/2$. This continuous pair is then mapped to the appropriate discrete bin indices according to the sinogram's dimensions and [binning](@entry_id:264748) rules. This [binning](@entry_id:264748) process means that multiple distinct LORs with similar geometric properties are grouped together, losing the specific detector-pair identity.

For a 3D scanner with multiple axial rings, this concept is extended. The full set of possible LORs is organized into a structure known as a **Michelogram** [@problem_id:4907330]. LORs are grouped based on two axial properties:

1.  **Segments:** LORs are grouped into *segments* based on their obliqueness. The segment index, $s$, is defined by the difference in the axial ring indices of the two detectors, $s = |r_2 - r_1|$. A segment $s=0$ contains all LORs connecting two detectors in the same ring (direct LORs), while segments with $s > 0$ contain increasingly oblique LORs.

2.  **Planes:** Within each segment, LORs are further grouped into *planes* based on their average axial position. The plane index, $p$, is defined by the average of the ring indices, $p = (r_1 + r_2)/2$. This value corresponds to the axial center of the LOR.

An interesting consequence of this indexing is the parity of the plane index $p$. Since $p = r_1 + s/2$, if the segment index $s$ is even, $p$ will be an integer. If $s$ is odd, $p$ will be a half-integer, meaning the axial centers of these LORs lie midway between the physical ring planes. Furthermore, for a scanner with $R$ rings, the number of planes in a segment $s$ is not constant; it is equal to $R-s$. This is because as the obliqueness $s$ increases, there are fewer pairs of rings that can form such an LOR while remaining within the scanner's axial field of view.

### Geometrical and Physical Effects on System Performance

The geometry of the PET gantry and its detectors is not just a passive framework; it actively influences the quality of the acquired data and the ultimate spatial resolution of the final image. Several key physical phenomena are direct consequences of this geometry.

#### Parallax Error and Depth of Interaction (DOI)

One of the most significant limitations on PET spatial resolution is **parallax error**, also known as the radial elongation effect. To understand this, we first define the directions for measuring resolution. For a [point source](@entry_id:196698), **radial resolution** refers to the image blur measured along the line from the scanner center through the source, while **tangential resolution** is the blur measured along the arc at that radius [@problem_id:4907353].

Parallax error primarily degrades radial resolution. It arises because PET detectors have a significant radial thickness $t$ (e.g., 10-20 mm) to ensure high photon [stopping power](@entry_id:159202). For an annihilation event occurring away from the center of the scanner, photons strike the detectors at an oblique angle. If the system cannot determine the **depth of interaction (DOI)**—the depth $z \in [0,t]$ within the crystal where the photon was detected—it must assign the LOR based on the crystal's front face or center. This uncertainty in depth translates into a significant uncertainty in the LOR's position, causing it to be blurred. The effect is negligible for sources at the gantry's center (where incidence is normal) but becomes progressively worse as the source moves towards the edge of the field of view. The resulting radial blur, $\sigma_r$, scales approximately in proportion to the source's radial offset $r$ and inversely with the gantry radius $R$:
$$
\sigma_r(r) \propto \frac{r}{R}
$$

To combat this resolution degradation, advanced PET detectors are designed with DOI-measuring capabilities. There are several major approaches to this [@problem_id:4907385]:
*   **Phoswich Detectors:** These detectors stack layers of different scintillator materials, each with a unique light decay time. By analyzing the shape of the light pulse, the system can identify which layer the interaction occurred in, providing a discrete (layered) estimate of DOI.
*   **Dual-Ended Readout:** A single long crystal is read out by photodetectors at both its front and back ends. The DOI can be estimated either from the difference in arrival times of the scintillation light at the two ends or from the ratio of light collected by each end (due to light attenuation within the crystal). This provides a continuous DOI measurement. For the timing-based method, the uncertainty in the DOI estimate, $\sigma_z$, is proportional to the timing uncertainty of the photodetectors, $\sigma_t$, and the speed of light in the crystal, $v=c/n$: $\sigma_z = \frac{v\sqrt{2}}{2}\sigma_t$.
*   **Monolithic Detectors:** A large, continuous block of scintillator is coupled to an array of photodetectors. The distribution of light across the [photodetector](@entry_id:264291) array depends on the 3D position of the interaction, including its depth. Using sophisticated calibration and statistical algorithms, the full 3D interaction position can be estimated, providing continuous DOI information.

#### Photon Non-Collinearity

A second, unavoidable physical limitation on resolution is **photon non-[collinearity](@entry_id:163574)**. While it is often assumed that the two annihilation photons are emitted in exactly opposite directions ($\pi$ radians apart), this is not precisely true. The annihilating electron-positron pair is not perfectly at rest; it has a small residual [center-of-mass momentum](@entry_id:171180). To conserve momentum, the two emitted photons must have a component of their momentum that cancels this residual, causing them to be emitted at an angle slightly different from $\pi$ [radians](@entry_id:171693).

This angular deviation is random, following a nearly Gaussian distribution. The standard deviation of this distribution is related to the root-mean-square momentum of the pair, and for annihilations in tissue, the Full Width at Half Maximum (FWHM) of the angular deviation is approximately $0.0023$ [radians](@entry_id:171693) (about $0.13^\circ$). This small angular error translates into a spatial error in the LOR's position at the detector ring. The magnitude of this spatial blur is directly proportional to the distance the photons travel. Therefore, the FWHM of the non-[collinearity](@entry_id:163574) blur, $FWHM_{nc}$, is proportional to the scanner's radius, $R$ [@problem_id:4907386]. A widely used approximation, with $R$ in millimeters, is:
$$
FWHM_{nc} \approx 0.0022 D = 0.0044 R
$$
This shows that larger scanners, while offering more space for patients, will inherently suffer from greater blurring due to non-[collinearity](@entry_id:163574). This effect is independent of detector properties and represents a fundamental limit of PET physics.

#### The System Matrix: Modeling Geometric Sensitivity

The final step in linking geometry to the image is the mathematical model used for reconstruction. Iterative reconstruction algorithms rely on a **[forward model](@entry_id:148443)**, which predicts the measured data for a given estimate of the [radioisotope](@entry_id:175700) distribution. This is expressed as a linear system $y \approx Ax$, where $x$ is a vector of activity values in image voxels, $y$ is a vector of counts in LOR bins, and $A$ is the **system matrix**.

Each element $A_{ji}$ of the [system matrix](@entry_id:172230) represents the probability that an emission from voxel $i$ will be detected along LOR $j$. This probability is fundamentally a geometric quantity, representing the spatial overlap between the voxel and the sensitivity region of the LOR [@problem_id:4907334]. Two common models are:

*   **Ray-Driven Model:** This is the simplest model, where each LOR is treated as an infinitely thin line. The [matrix element](@entry_id:136260) $A_{ji}$ is then proportional to the length of the intersection of this line with the volume of voxel $i$.
*   **Tube-of-Response (TOR) Model:** This is a more realistic model that accounts for the finite size of the detector crystals, as well as blurring effects like positron range and non-[collinearity](@entry_id:163574). The LOR is modeled not as a line but as a "tube" (e.g., a cylinder) with a finite cross-sectional area. The matrix element $A_{ji}$ is then proportional to the volume of the intersection of this tube with the volume of voxel $i$. For a cylindrical tube of radius $r$ passing through the center of a cubic voxel of side length $a$, this volume is $\pi r^2 a$.

By incorporating these geometric and physical realities into the [system matrix](@entry_id:172230), iterative reconstruction algorithms can produce images of significantly higher quality and quantitative accuracy than was possible with simpler models. The geometry of the PET scanner is thus woven into every stage of the imaging chain, from the initial detection of photons to the final reconstruction of the diagnostic image.