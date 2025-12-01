## Introduction
Single Photon Emission Computed Tomography (SPECT) is a cornerstone of [nuclear medicine](@entry_id:138217), offering unique insights into physiological function by imaging the distribution of radiotracers within the body. However, the diagnostic value of a SPECT image is profoundly dependent on the quality of the raw data acquired. The journey from photon emission to final image is fraught with challenges, including severe signal loss, physical blurring, and artifacts from patient motion, creating a complex optimization problem for imaging scientists. This article addresses this challenge by providing a structured guide to the strategies that govern effective SPECT [data acquisition](@entry_id:273490). The following chapters will navigate this topic methodically. First, "Principles and Mechanisms" will deconstruct the fundamental physics and mathematics, from the creation of a single count to the assembly of a complete tomographic dataset. Next, "Applications and Interdisciplinary Connections" will demonstrate how these principles are applied in the real world to optimize clinical protocols for cardiology, oncology, and hybrid SPECT/CT imaging. Finally, "Hands-On Practices" will provide an opportunity to apply these concepts to solve practical problems in imaging physics. By the end, you will have a comprehensive understanding of how to strategically design and execute a SPECT acquisition for maximal image quality and quantitative accuracy.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms that govern Single Photon Emission Computed Tomography (SPECT) [data acquisition](@entry_id:273490). We will deconstruct the process, starting from the generation of a single photon signal and culminating in the assembly of a complete tomographic dataset. Our focus will be on the physical phenomena, the mathematical models that describe them, and the strategic decisions that an imaging scientist must make to optimize data quality for clinical and research applications.

### The SPECT Signal: From Photon Emission to Detected Count

The entire SPECT imaging chain begins with a single physical event: the decay of a radionuclide within a patient, leading to the emission of a gamma photon. The journey of this photon from its origin to its registration by the detector is a probabilistic process, and understanding the factors that govern its success is key to comprehending SPECT sensitivity and quantitative accuracy.

The expected rate of detected counts, $C$, from a source of activity is determined by a cascade of sequential factors. Let us consider a [point source](@entry_id:196698) of activity $A$ (measured in Becquerels, or decays per second) embedded within tissue.

1.  **Photon Yield**: Not every [nuclear decay](@entry_id:140740) produces a gamma photon suitable for imaging. The **photon yield**, denoted by $p$, is the fraction of decays that result in the emission of a photon in the desired energy range. The rate of photon emission is therefore $A \cdot p$.

2.  **Attenuation**: As a photon travels from its point of origin to the edge of the body, it may be absorbed or scattered by the intervening tissue. This process, known as **attenuation**, is the dominant factor limiting signal in SPECT. According to the Beer-Lambert law, the probability that a photon survives transit through a path of length $L$ in a uniform medium with a linear attenuation coefficient $\mu$ is given by $\exp(-\mu L)$. Photons originating deeper within the body are thus much less likely to be detected.

3.  **Collimation and Detection**: For a photon that successfully exits the patient, it must still pass through a **collimator** and be registered by the detector crystal. The collimator provides directional information by physically blocking photons that are not traveling along a desired trajectory. The **geometric efficiency**, $\eta_g$, represents the very small fraction of emitted photons that have the correct trajectory to pass through the collimator holes. Finally, of the photons that do strike the detector crystal, only a fraction, known as the **intrinsic efficiency** $\eta_d$, will successfully produce a detectable signal.

Combining these factors, we can formulate a model for the expected count rate $C$ from a [point source](@entry_id:196698) at depth $L$ [@problem_id:4926974]:

$C = A \cdot p \cdot \exp(-\mu L) \cdot \eta_g \cdot \eta_d$

For instance, for a hypothetical $20 \, \text{MBq}$ source with a photon yield $p=0.89$ at a depth of $8 \, \text{cm}$ in tissue with $\mu = 0.15 \, \text{cm}^{-1}$, imaged with a system having $\eta_g = 3.0 \times 10^{-4}$ and $\eta_d = 0.85$, the expected count rate would be approximately $1.37 \times 10^3$ counts per second. This calculation underscores the dramatic signal loss in SPECT; of the $20$ million photons emitted per second, only a tiny fraction contribute to the final image, highlighting the "photon-starved" nature of nuclear imaging.

### Forming Projections: The Role of Collimation and Spatial Resolution

The central challenge in single-photon imaging is that, unlike a camera using a lens to focus light, there is no practical way to focus the high-energy gamma rays. Instead, SPECT relies on **mechanical collimation** to form a projection. The collimator is typically a thick plate of a dense material like lead or tungsten, perforated with thousands of precisely aligned holes. Its function is purely geometric: it enforces **angular selection** by absorbing photons that are not traveling nearly parallel to the axis of the holes.

Let us model a single cylindrical hole in a **parallel-hole collimator** as having a diameter $d$ and a length $L$. For a gamma ray to pass through this hole, its trajectory must not intersect the side walls. Geometrically, this constrains the [angle of incidence](@entry_id:192705) $\theta$ relative to the hole's central axis. The maximum acceptance half-angle, $\theta_{\max}$, is determined by the ray that just grazes the entrance and exit edges of the hole [@problem_id:4927032]. This gives the relation:

$\tan(\theta_{\max}) = \frac{d}{2L}$

For typical collimator dimensions (e.g., $L=40 \, \text{mm}$, $d=2 \, \text{mm}$), $\theta_{\max}$ is very small, on the order of $1-2$ degrees. This severe restriction means that the detector bin at a given location predominantly "sees" activity along a narrow set of nearly [parallel lines](@entry_id:169007) extending into the patient. The resulting measurement thus approximates a **[line integral](@entry_id:138107)** of the activity distribution, which is the mathematical definition of a **projection**. By orienting the holes differently, such as making them converge towards a focal line or point, one can create fan-beam or cone-beam projections, respectively.

This geometric selection mechanism directly impacts two critical performance metrics: spatial resolution and sensitivity. The **geometric resolution**, $R_g$, describes the blurring introduced by the collimator itself. For a parallel-hole collimator, a point source at a distance $b$ from the collimator face will be blurred on the detector. The width of this blur can be approximated using similar triangles [@problem_id:4926976]:

$R_g \approx d \frac{L+b}{L} = d \left(1 + \frac{b}{L}\right)$

This crucial relationship shows that resolution degrades (i.e., $R_g$ increases) with increasing distance from the collimator. It also depends directly on the hole diameter $d$.

The **sensitivity**, or efficiency, of a collimator is proportional to the fraction of photons it allows to pass. This is related to the [solid angle](@entry_id:154756) of acceptance of each hole and the total open area of the collimator face. For a given hole, the sensitivity scales approximately with the square of its acceptance angle, leading to the scaling law [@problem_id:4926976]:

$S \propto \frac{d^2}{L^2}$

These two relationships encapsulate the fundamental **resolution-sensitivity trade-off** in SPECT collimator design. To improve resolution (decrease $R_g$), one must either decrease the hole diameter $d$ or increase the hole length $L$. Both actions, however, cause a sharp decrease in sensitivity. A collimator designed for high resolution will be inefficient and require longer scan times or higher injected doses, while a high-sensitivity collimator will produce blurrier images. The choice of collimator is therefore a critical strategic decision based on the specific clinical task.

### Tomographic Acquisition: Sampling the Projections

A single projection provides a 2D, shadow-like view of the 3D radiotracer distribution. To reconstruct the full 3D distribution, we must acquire projections from many different angles around the patient. This process of collecting data to reconstruct cross-sectional images is known as **[tomography](@entry_id:756051)**.

The theoretical foundation for this process is the **Fourier Slice Theorem** (or Projection-Slice Theorem). It states that the 1D Fourier transform of a parallel-beam projection at a given angle $\theta$ is identical to a "slice" through the 2D Fourier transform of the object itself, taken at the same angle $\theta$. By acquiring projections at a sufficient number of angles, we can sample the object's Fourier space and then perform an inverse transform to recover the image.

This leads directly to the concept of **angular sampling**. Since the detector rotates to discrete angular positions, we must choose the number of projection views, $M$, to be large enough to adequately sample the object's Fourier representation and avoid **angular aliasing artifacts**, which manifest as streaks emanating from sharp features in the image. The required number of views depends on the size of the object and its [spatial frequency](@entry_id:270500) content (i.e., its resolution). A common rule of thumb, derived from the Nyquist sampling criterion, states that for an object of diameter $D$ to be reconstructed with a resolution that resolves features up to a maximum [spatial frequency](@entry_id:270500) $f_c$, the number of views $M$ over a 180° arc should be [@problem_id:4926974]:

$M \ge \pi D f_c$

Alternatively, if the object is represented on a digital grid of $N$ pixels across its diameter, the minimum number of views over 180° is given by [@problem_id:4927000]:

$M \ge \frac{\pi N}{2}$

For a typical clinical scan reconstructed on a $128 \times 128$ matrix ($N=128$), this implies a minimum of $M \approx (\pi \cdot 128) / 2 \approx 201$ views. In practice, SPECT systems often acquire 64 or 128 views over 360° (or 32/64 over 180° for cardiac scans), which may be undersampled according to this criterion, representing a compromise between acquisition time and potential for aliasing artifacts.

### Strategies for Optimizing Data Quality

Beyond the choice of collimator and sampling parameters, several acquisition strategies can be employed to enhance the quality of the collected data.

#### Detector Orbits

As established previously, the geometric resolution of a parallel-hole collimator degrades with increasing distance between the source and the detector. Therefore, a primary strategy for improving image quality is to keep the detector as close as possible to the patient at all projection angles. This minimizes the average source-to-collimator distance, $\langle z \rangle$, and thus optimizes resolution.

Three main orbit types are used [@problem_id:4926984]:
1.  **Circular Orbit**: The simplest strategy, where the detector maintains a constant radius of rotation. This is inefficient for non-circular body [cross-sections](@entry_id:168295) (like the torso), as large air gaps will exist at the narrower aspects of the patient.
2.  **Elliptical Orbit**: The detector follows a fixed elliptical path that better approximates the patient's general shape, reducing the average air gap compared to a circular orbit.
3.  **Body-Contoured Orbit**: The most advanced strategy, where the detector-to-patient distance is actively adjusted at each projection angle to maintain a minimal, constant clearance. This minimizes $\langle z \rangle$ and provides the best possible geometric resolution that the system can achieve. For example, in a study of an elliptical phantom, switching from a [circular orbit](@entry_id:173723) with an average standoff of $8.75 \, \text{cm}$ to a body-contoured orbit with a constant standoff of $3.0 \, \text{cm}$ could improve the system's geometric resolution by approximately $45\%$.

#### Data Acquisition Modes

The raw output of a gamma camera is a stream of individual photon detection events. There are two primary modes for recording this information:

-   **Histogram Mode**: In this traditional mode, the acquisition system sorts events in real-time into pre-defined bins. For a tomographic scan, this means accumulating counts into a series of projection images, each corresponding to a specific angular range. Any additional information, such as the precise time of arrival or energy of each photon, is discarded once the event is binned.

-   **List-Mode**: In this mode, the system records the attributes of each individual detected event as an entry in a list. Each entry typically contains the detector coordinates $(\mathbf{x}_i)$, the measured energy $(E_i)$, and a high-precision timestamp $(t_i)$ [@problem_id:4926956]. This method preserves the maximal amount of information from the acquisition.

The key advantage of list-mode is its profound flexibility. Because the full event history is saved, binning decisions can be made retrospectively. This is invaluable for **gated imaging**, where physiological signals (e.g., ECG for cardiac motion, bellows for respiratory motion) are recorded alongside the SPECT data. With list-mode data, one can retrospectively sort the detected photons into different phases of the cardiac or respiratory cycle to generate a set of motion-corrected or motion-resolved images. Similarly, for **dynamic studies** that track tracer uptake over time, list-mode allows the user to define and redefine time frames after the acquisition to best characterize the observed kinetics. This flexibility comes from a fundamental property of the underlying Poisson statistics of detection: retrospectively selecting events from a list is statistically equivalent to having applied the same selection criteria prospectively during the acquisition [@problem_id:4926956].

### Managing Physical and Physiological Non-idealities

A raw SPECT dataset is an imperfect representation of the true radiotracer distribution, corrupted by several physical and physiological effects. Accurate reconstruction requires that these effects be modeled and compensated.

#### Photon Attenuation

As previously mentioned, attenuation is a dominant degrading factor. The photons detected in a given projection bin have originated from various depths along the corresponding line of sight, and each has been attenuated differently. This depth-dependent signal loss means that simple correction methods are often inaccurate. An attempt to apply a single multiplicative correction factor to each projection bin, a technique known as **pre-correction**, is fundamentally a heuristic approximation [@problem_id:4926957]. This is because no single factor can correctly account for the different attenuation paths experienced by all photons contributing to that bin.

The most accurate and widely accepted method for **attenuation correction** is to incorporate it directly into the system model used by **iterative reconstruction** algorithms (like MLEM or OSEM). In this approach, the system matrix, which models the probability of a photon from source voxel $j$ being detected in bin $i$, includes the path-dependent survival probability term, $\exp(-\int \mu(\mathbf{s}) d\mathbf{s})$. This allows the reconstruction algorithm to solve for the underlying activity distribution that, when attenuated according to the physical model, best matches the measured data. This model-based approach is statistically consistent with the Poisson nature of the data and is considered the state-of-the-art for quantitative SPECT [@problem_id:4926957].

#### Collimator-Detector Response (Image Blur)

The finite resolution of the imaging system, arising from both the collimator geometry and the intrinsic resolution of the detector crystal, causes blurring in the image. This effect is captured by the **[point spread function](@entry_id:160182) (PSF)**, which describes the image of an ideal point source. In SPECT, this PSF is strongly **depth-dependent**, becoming wider for sources farther from the detector. This complete system blur is often termed the **collimator-detector response (CDR)**, denoted $h(\boldsymbol{\rho}; z)$, where $\boldsymbol{\rho}$ is the spatial offset on the detector and $z$ is the source depth.

Similar to attenuation correction, the most accurate way to handle this non-ideality is to incorporate it into the system model for iterative reconstruction. The system matrix element $a_{ij}$, representing the contribution of source voxel $j$ at location $(\mathbf{u}_j, z_j)$ to detector bin $i$, is calculated by integrating the depth-dependent PSF over the area of the detector bin, $B_i$ [@problem_id:4927015]:

$a_{ij} \propto \int_{B_i} h(\mathbf{u} - \mathbf{u}_j; z_j) \, d\mathbf{u}$

By including this resolution model, the reconstruction algorithm can partially reverse the blurring effects, a process often called resolution recovery, leading to sharper and more quantitatively accurate images.

#### Detector Dead-Time

Scintillation detectors and their associated electronics require a small but finite amount of time, $\tau$, to process each detected photon. During this **[dead time](@entry_id:273487)**, the system is unable to process another incoming event. This leads to a loss of counts, which becomes increasingly severe at high activity levels. The relationship between the true event rate, $n$, and the measured event rate, $m$, depends on the detector's behavior.

Two standard models describe this phenomenon [@problem_id:4926959]:
1.  **Non-paralyzable Model**: An event arriving during the [dead time](@entry_id:273487) is simply ignored, and the system becomes live again once the initial dead-time period $\tau$ is over. The measured rate is given by $m = \frac{n}{1+n\tau}$. In this model, the measured rate monotonically increases and saturates at a maximum value of $1/\tau$.
2.  **Paralyzable Model**: An event arriving during the [dead time](@entry_id:273487) is not only lost but also re-triggers and extends the dead-time interval. An event is only recorded if no other event arrives for a full interval $\tau$ before it. This leads to the relationship $m = n \exp(-n\tau)$. In this case, the measured rate peaks at a true rate of $n=1/\tau$ and then paradoxically decreases towards zero as the true rate increases further—the system becomes "paralyzed" by the constant stream of events.

At low count rates, both models approximate to $m \approx n - n^2\tau$. Understanding and correcting for dead-time is essential for quantitative applications, such as [dosimetry](@entry_id:158757) or dynamic studies, where accurate measurement of activity is required.

#### Patient Motion

Patient motion during the long duration of a SPECT scan is a major source of image degradation. If the patient moves, the projections acquired at different angles will no longer correspond to a single, static object distribution. This data inconsistency leads to significant artifacts.

We can model a rigid in-plane translation of the object by an angle-dependent [shift vector](@entry_id:754781), $\Delta\mathbf{r}(\theta)$. A key result from the mathematics of the Radon transform is that a translation of the object in physical space results in a corresponding shift of its projection [@problem_id:4926961]. Specifically, the projection profile is shifted along the detector axis by an amount equal to the component of the translation vector perpendicular to the lines of integration: $p'(\theta, s) = p(\theta, s - \Delta\mathbf{r}(\theta) \cdot \mathbf{n}(\theta))$ where $\mathbf{n}(\theta)$ is the normal vector to the projection direction. When these misaligned projections are fed into a standard reconstruction algorithm like Filtered Backprojection (FBP), the result is a blurred and distorted image. If the motion is random and uncorrelated from view to view, its effect on average is to convolve the true image with a blurring kernel. For random, zero-mean motion with equal variance in all directions, this results in an isotropic blurring of the final reconstructed image, reducing its effective resolution [@problem_id:4926961]. Motion correction techniques, which often rely on tracking patient movement and either correcting the projection data or incorporating the motion model into the reconstruction, are an active area of research aimed at mitigating this common and deleterious artifact.