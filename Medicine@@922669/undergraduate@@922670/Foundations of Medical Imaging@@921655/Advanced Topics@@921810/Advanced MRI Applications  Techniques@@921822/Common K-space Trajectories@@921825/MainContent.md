## Introduction
The ability of Magnetic Resonance Imaging (MRI) to produce detailed images of internal anatomy relies on a sophisticated process of [spatial encoding](@entry_id:755143). At the heart of this process lies the concept of k-space, the [spatial frequency](@entry_id:270500) domain of the image. The path taken to sample this domain, known as the k-space trajectory, is a fundamental design choice that dictates nearly every aspect of the final image, from scan time and resolution to artifact characteristics and sensitivity to motion. Understanding these trajectories is therefore essential for anyone seeking to master MRI physics and application.

This article provides a comprehensive overview of the most common k-space trajectories used in MRI. It addresses the crucial question of how different gradient modulation schemes are designed and why a specific trajectory is chosen for a particular clinical or research goal. By bridging theory with practice, this guide will equip you with the knowledge to appreciate the intricate link between hardware, physics, and diagnostic image quality.

Across three chapters, you will delve into the core principles of [spatial encoding](@entry_id:755143), explore a diverse range of clinical applications, and engage with practical problem-solving. In "Principles and Mechanisms," we will establish the mathematical foundation connecting gradients to k-space and detail the design of Cartesian, radial, and spiral trajectories. "Applications and Interdisciplinary Connections" will demonstrate how these trajectories are exploited to enable techniques like fMRI and diffusion imaging, and how they connect to advanced reconstruction methods. Finally, "Hands-On Practices" will offer concrete exercises to solidify your understanding of these critical concepts. We begin by examining the fundamental principles that govern how spatial information is encoded in the MR signal.

## Principles and Mechanisms

This chapter elucidates the fundamental principles governing the acquisition of spatial information in Magnetic Resonance Imaging (MRI) and the mechanisms by which different k-space trajectories are designed and implemented. We will begin by establishing the mathematical relationship between magnetic field gradients and the spatial frequency domain, or k-space. Subsequently, we will explore the critical trade-offs between imaging parameters such as field of view and resolution. Finally, we will survey the most common k-space trajectories, from the conventional Cartesian grid to more advanced non-Cartesian patterns, and discuss the practical challenges and hardware considerations associated with each.

### The Gradient-K-space Relationship: Spatial Encoding

The cornerstone of all imaging in MRI is the principle of **[spatial encoding](@entry_id:755143)**, which relies on the precise manipulation of magnetic field gradients to impart a unique, position-dependent phase onto the nuclear spins within an object. The precessional frequency of a spin, its Larmor frequency, is directly proportional to the local magnetic field strength. By superimposing a linear magnetic field gradient $\mathbf{G}(t)$ onto the main static field $B_0$, the magnetic field at a position $\mathbf{r}$ becomes $B(\mathbf{r}, t) = B_0 + \mathbf{G}(t) \cdot \mathbf{r}$.

After demodulating the received signal to remove the carrier frequency component $\gamma B_0$, the remaining phase of the signal from spins at position $\mathbf{r}$ is determined solely by the time integral of the gradient-induced frequency shift. This accumulated phase $\phi(\mathbf{r}, t)$ is given by:

$$ \phi(\mathbf{r}, t) = \gamma \int_{0}^{t} \mathbf{G}(\tau) \cdot \mathbf{r} \, d\tau = \left( \gamma \int_{0}^{t} \mathbf{G}(\tau) \, d\tau \right) \cdot \mathbf{r} $$

The total signal $S(t)$ detected by the receiver coil is the integral of the transverse magnetization, proportional to the spin density $\rho(\mathbf{r})$, over the entire volume:

$$ S(t) = \int \rho(\mathbf{r}) \exp(-i \phi(\mathbf{r}, t)) \, d\mathbf{r} = \int \rho(\mathbf{r}) \exp\left(-i \left( \gamma \int_{0}^{t} \mathbf{G}(\tau) \, d\tau \right) \cdot \mathbf{r}\right) \, d\mathbf{r} $$

This expression is profound; it reveals that the MRI signal $S(t)$ is the Fourier transform of the object's spin density $\rho(\mathbf{r})$. By comparing this to the standard definition of the multi-dimensional Fourier transform, $F(\mathbf{k}) = \int f(\mathbf{r}) \exp(-i 2\pi \mathbf{k} \cdot \mathbf{r}) \, d\mathbf{r}$, we can define a time-dependent vector $\mathbf{k}(t)$ that represents the spatial frequency being sampled at time $t$:

$$ 2\pi \mathbf{k}(t) = \gamma \int_{0}^{t} \mathbf{G}(\tau) \, d\tau $$

This leads to the fundamental definition of the **k-space trajectory**:

$$ \mathbf{k}(t) = \frac{\gamma}{2\pi} \int_{0}^{t} \mathbf{G}(\tau) \, d\tau $$

The vector $\mathbf{k}(t)$ has units of [spatial frequency](@entry_id:270500), typically cycles per meter (m⁻¹) [@problem_id:4869120]. This equation signifies that by controlling the time integral of the applied gradients, we can navigate through the [spatial frequency](@entry_id:270500) domain, or **k-space**, and sample the Fourier transform of the object. The path traced by $\mathbf{k}(t)$ is the **k-space trajectory**.

Differentiating this relationship with respect to time provides an equally important insight into the [instantaneous velocity](@entry_id:167797) in k-space [@problem_id:4897825] [@problem_id:4869046]:

$$ \dot{\mathbf{k}}(t) = \frac{d\mathbf{k}}{dt} = \frac{\gamma}{2\pi} \mathbf{G}(t) $$

This equation shows that the applied gradient vector $\mathbf{G}(t)$ is directly proportional to the velocity vector $\dot{\mathbf{k}}(t)$ in k-space. To move through k-space in a particular direction, one must apply a gradient in that same direction. To move faster, a stronger gradient is required. This simple but powerful relationship is the basis for designing all MRI pulse sequences.

### The Fourier Duality: Field of View and Resolution

The Fourier relationship between the image and k-space imposes a fundamental duality that governs the primary trade-offs in MRI. The way k-space is sampled dictates the properties of the reconstructed image. Two key parameters are the Field of View (FOV) and the spatial resolution.

The **Field of View (FOV)** is the spatial extent of the imaged region. According to the Nyquist-Shannon sampling theorem, to avoid aliasing (the folding or wrapping of the image), the signal must be sampled in the frequency domain at a rate determined by the spatial extent of the object. For MRI, this means the k-space sampling increment, $\Delta k$, determines the FOV. The relationship for a given dimension is:

$$ \text{FOV} = \frac{1}{\Delta k} $$

If samples in k-space are taken further apart (larger $\Delta k$), the resulting FOV becomes smaller, increasing the risk that anatomy outside this region will alias into the image [@problem_id:4869120].

The **spatial resolution** ($\Delta x$) refers to the smallest feature size that can be distinguished in the image. Intuitively, resolving fine details, which correspond to rapid spatial variations, requires information about high spatial frequencies. Therefore, the resolution is determined not by the spacing of k-space samples, but by the maximum extent of the sampled region. The boundary of the sampled k-space is defined by $k_{\max}$. The formal relationship can be derived by considering the **Point Spread Function (PSF)**, which is the image of an ideal [point source](@entry_id:196698) and is given by the inverse Fourier transform of the k-space sampling function. For a symmetric Cartesian acquisition covering the range $[-k_{\max}, k_{\max}]$, the PSF is a [sinc function](@entry_id:274746), whose width defines the resolution. The nominal spatial resolution is conventionally defined as half the period of the highest sampled spatial frequency, leading to the critical relationship:

$$ \Delta x = \frac{1}{2k_{\max}} $$

To achieve higher resolution (a smaller $\Delta x$), one must acquire data out to higher spatial frequencies (a larger $k_{\max}$) [@problem_id:4869120]. These two relationships, $\text{FOV} = 1/\Delta k$ and $\Delta x = 1/(2k_{\max})$, are the foundational rules for designing any MRI acquisition.

### Cartesian Trajectories: The Workhorse of MRI

The most straightforward and widely used method for sampling k-space is to acquire data on a uniform Cartesian grid. In a typical two-dimensional **spin-warp** acquisition, each line of k-space is acquired following a radiofrequency excitation pulse. A **phase-encoding gradient** is applied first to select a specific horizontal line (a particular $k_y$ value). Then, a **frequency-encoding** or **readout gradient** is applied along the horizontal direction while the signal is being recorded, traversing that line from, for example, $-k_{x, \max}$ to $+k_{x, \max}$. This process is repeated for a different phase-encoding gradient amplitude in each repetition time ($TR$) until all the required lines of k-space are filled.

The parameters of a Cartesian acquisition are tightly interwoven. Consider an acquisition with a desired FOV, $F_x$, and an image matrix size of $N_x$ pixels along the readout direction. This dictates a resolution of $\Delta x = F_x / N_x$ and a k-space sampling increment of $\Delta k_x = 1/F_x$. If a constant readout gradient $G_x$ is applied during data sampling with a dwell time (time between samples) of $\Delta t$, the k-space step is given by $\Delta k_x = (\gamma/2\pi) G_x \Delta t$. The receiver bandwidth, $BW$, is related to the dwell time by $BW = 1/\Delta t$. Combining these relationships allows for the calculation of the required gradient amplitude [@problem_id:4869046]:

$$ G_x = \frac{1}{(\gamma/2\pi) F_x \Delta t} = \frac{BW}{(\gamma/2\pi) F_x} $$

For instance, to acquire an image with a $320 \times 256$ matrix over a $0.256 \, \text{m}$ FOV using a receiver bandwidth of $200 \, \text{kHz}$, the required dwell time would be $\Delta t = 1/BW = 5 \, \mu\text{s}$. This in turn dictates a readout gradient amplitude of approximately $18.35 \, \text{mT/m}$ must be applied during the acquisition window.

The speed at which k-space can be traversed is ultimately limited by hardware constraints: the maximum gradient amplitude ($G_{\max}$) and the maximum [slew rate](@entry_id:272061) ($S_{\max}$), which is the rate at which gradients can be turned on and off. To reach a target $k_{\max}$ in the minimum possible time, one must use a time-optimal trapezoidal gradient waveform: ramp up at $S_{\max}$ to $G_{\max}$, hold at $G_{\max}$, and then ramp down. The time to reach $k_{\max}$ is therefore determined by the area under this trapezoidal shape, and it represents a fundamental limit on acquisition speed for a given resolution [@problem_id:4869123].

### Non-Cartesian Trajectories: Speed and Motion Robustness

While Cartesian imaging is robust and simple, alternative k-space trajectories offer significant advantages in terms of speed, efficiency, and robustness to motion and flow. The two most prominent non-Cartesian families are radial and spiral.

#### Radial Trajectories

A **radial trajectory** samples k-space along a series of straight lines, or "spokes," that pass through the origin, resembling the spokes of a wheel. Each spoke is acquired by applying a readout gradient with a constant direction and then electronically rotating the direction of the gradient for the next spoke [@problem_id:4897825]. A key feature of radial imaging is the repeated [oversampling](@entry_id:270705) of the center of k-space, which contains low-frequency information corresponding to image contrast. This [oversampling](@entry_id:270705) provides a degree of intrinsic robustness to motion.

The design of a radial acquisition requires careful consideration of the sampling density. To avoid significant aliasing artifacts, the circumferential spacing between adjacent spokes at the edge of k-space (at $k_{\max}$) should not exceed the Nyquist sampling interval, $\Delta k = 1/\text{FOV}$. This constraint leads to a condition on the minimum number of spokes, $N_{\theta}$, required for a given FOV, $L$, and resolution, $\Delta x$:

$$ N_{\theta} = \frac{\pi k_{\max}}{\Delta k} = \frac{\pi (1/(2\Delta x))}{1/L} = \frac{\pi L}{2\Delta x} $$

This means that to match the performance of a Cartesian scan with $N$ pixels across the FOV ($L=N\Delta x$), one needs approximately $N_{\theta} = \pi N / 2$ spokes. This is a fundamental design principle for radial MRI [@problem_id:4869088].

#### Spiral Trajectories

A **spiral trajectory** samples k-space along an Archimedean or similar spiral path, typically starting from the center and spiraling outwards. This is one of the most efficient ways to cover a 2D circular region of k-space, as it does so in a single, continuous shot. To generate a spiral path $\mathbf{k}(t) = r(t) \mathbf{e}_r(\theta(t))$, the gradient waveform must have both a radial and an azimuthal component, corresponding to the k-[space velocity](@entry_id:190294) vector $\dot{\mathbf{k}}(t) = \dot{r}(t) \mathbf{e}_r + r(t)\dot{\theta}(t) \mathbf{e}_{\theta}$. The required gradient is thus:

$$ \mathbf{G}(t) = \frac{2\pi}{\gamma} \left( \dot{r}(t) \mathbf{e}_r + r(t)\dot{\theta}(t) \mathbf{e}_{\theta} \right) $$

This requires continuously time-varying gradients on two physical axes (e.g., $G_x$ and $G_y$) simultaneously [@problem_id:4897825]. Spiral imaging is valued for its speed and for its unique motion properties, which tend to manifest as blurring rather than discrete "ghost" artifacts.

### The Challenge of Non-Uniform Sampling

The benefits of non-Cartesian trajectories come at a cost: the data are no longer on a uniform grid, which introduces significant challenges for image reconstruction and can lead to new classes of artifacts if not handled properly.

#### Sampling Density and Compensation

Non-Cartesian trajectories inherently sample k-space with a non-uniform density. For example, in a radial acquisition, the spokes are close together near the origin and spread far apart at the periphery. The local sampling density is inversely proportional to the radius, $\rho(\mathbf{k}) \propto 1/r$. To reconstruct an image correctly, the contribution of each sample must be weighted according to the area of k-space it represents. This weighting factor is known as the **Density Compensation Function (DCF)**. For radial imaging, the DCF must be proportional to the radius, $w(\mathbf{k}) \propto r$, to counteract the natural $1/r$ sampling density [@problem_id:4869053] [@problem_id:4897825].

The form of the DCF depends entirely on the trajectory geometry. For a "rings" trajectory, if the number of samples per ring is constant, the DCF must increase with radius. If, however, the number of samples per ring is increased proportionally to the radius (to maintain constant arc-length spacing), the DCF becomes approximately constant. Spiral trajectories, where the radial and angular positions are coupled, do not admit a simple, separable DCF; its calculation depends on the local velocity and spacing between [spiral arms](@entry_id:160156) [@problem_id:4869053].

#### Image Reconstruction: The NUFFT and Gridding

Since the k-space samples are not on a Cartesian grid, the highly efficient Fast Fourier Transform (FFT) algorithm cannot be applied directly. A direct reconstruction would require evaluating the discrete Fourier sum for each image pixel, a process known as the Non-uniform DFT (NUDFT). This has a computational cost of $\mathcal{O}(MN)$ for $M$ k-space samples and $N$ image pixels, which is prohibitively slow for typical image sizes.

The [standard solution](@entry_id:183092) is an approximation method known as **gridding**, which is a type of Non-uniform Fast Fourier Transform (NUFFT). This algorithm allows the use of the FFT by first interpolating the non-uniform k-space data onto a temporary, oversampled Cartesian grid. The key steps are as follows [@problem_id:4920813]:
1.  **Density Compensation:** Each raw k-space sample $s_m$ is multiplied by its corresponding DCF weight $w_m$.
2.  **Convolution/Gridding:** The weighted samples are "spread" onto a nearby neighborhood of points on an oversampled Cartesian grid. This is mathematically equivalent to convolving the non-uniform data with a small, compactly supported kernel. Oversampling (using a grid larger than required by the FOV) is crucial to mitigate aliasing artifacts that arise from this step.
3.  **Inverse FFT:** The standard inverse FFT is now applied to the gridded, oversampled data, producing an initial image.
4.  **Deapodization:** The convolution step in k-space corresponds to a multiplication in the image domain by the Fourier transform of the gridding kernel. This causes an intensity roll-off away from the image center ([apodization](@entry_id:147798)). This effect is corrected by dividing the image pointwise by the known kernel transform.
5.  **Cropping:** The final image is obtained by cropping the central portion of the oversampled grid, discarding the outer regions where aliasing artifacts were pushed by the [oversampling](@entry_id:270705).

#### Image Quality and Artifacts

The choice of k-space trajectory directly shapes the Point Spread Function (PSF) and thus determines the artifact characteristics of the acquisition. Any deviation from dense, uniform sampling of k-space will manifest as unwanted structure in the PSF. For example, in a radial acquisition where the number of spokes is insufficient for the desired resolution (angular [undersampling](@entry_id:272871)), the PSF will exhibit anisotropic side lobes. These side lobes appear as radial "streaking" artifacts emanating from bright objects in the image. This occurs because [undersampling](@entry_id:272871) in the angular dimension of k-space causes aliasing in the conjugate angular frequency domain, creating non-zero angular harmonics in the PSF [@problem_id:4869081].

### The Impact of Hardware Imperfections

Real MRI systems are subject to hardware imperfections that cause the actual k-space trajectory to deviate from the nominally prescribed one. Understanding these effects is critical for high-fidelity imaging.

#### Gradient Delays

A common imperfection is a small, constant timing delay, $\Delta t$, between the digital command to play a gradient and the actual response of the gradient coil and amplifier, or the timing of the [data acquisition](@entry_id:273490) clock. This delay causes the entire k-space trajectory to be shifted. For a readout with a constant gradient $G$, this results in a constant k-space shift of $\Delta k = (\gamma/2\pi) G \Delta t$. According to the Fourier shift theorem, a shift in k-space corresponds to the addition of a [linear phase](@entry_id:274637) ramp in the image domain. The slope of this phase ramp is $m = 2\pi \Delta k = \gamma G \Delta t$.

This effect can be precisely measured and calibrated. By acquiring two images with opposite readout gradient polarities ($+G$ and $-G$), two phase ramps with opposite slopes, $m_f = \gamma G \Delta t$ and $m_r = -\gamma G \Delta t$, are induced. The timing delay can then be robustly calculated from the difference of these measured slopes:

$$ \Delta t = \frac{m_f - m_r}{2 \gamma G} $$

For example, given measured phase slopes of $m_f = +18.6 \, \text{rad/m}$ and $m_r = -19.4 \, \text{rad/m}$ with a $20 \, \text{mT/m}$ gradient, a system timing delay of approximately $3.55 \, \mu\text{s}$ can be calculated and subsequently corrected for in the image reconstruction [@problem_id:4869083].

#### Gradient Nonlinearities

An ideal MRI scanner would produce perfectly linear magnetic field gradients throughout the entire imaging volume. In reality, physical constraints on coil design lead to **gradient nonlinearities**, where the gradient field strength deviates from this ideal linearity, particularly at positions far from the scanner's isocenter. These nonlinearities can be accurately described using a mathematical basis, such as **[spherical harmonics](@entry_id:156424)**.

A nonlinear gradient field means that the [spatial encoding](@entry_id:755143) is no longer uniform across the FOV. The effective gradient experienced by a spin at position $\mathbf{r}$ is different from the nominal gradient, leading to a position-dependent k-space encoding. This can be modeled as an effective, local k-space coordinate that is a distorted version of the nominal one: $k^{\mathrm{eff}}(\mathbf{r}, t) = (1 + \epsilon(\mathbf{r})) k^{\mathrm{nom}}(t)$, where $\epsilon(\mathbf{r})$ is a term describing the [local field](@entry_id:146504) deviation [@problem_id:4869110]. The consequence of this spatially varying encoding is geometric distortion in the final reconstructed image, where objects appear warped or scaled incorrectly. Advanced reconstruction algorithms can use pre-calibrated spherical harmonic models of the [gradient fields](@entry_id:264143) to correct for these distortions and recover geometrically accurate images.