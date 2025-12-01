## Introduction
Magnetic susceptibility is a fundamental property of all matter, but in Magnetic Resonance Imaging (MRI), its variation is the source of some of the most common and challenging image artifacts. These artifacts, manifesting as signal voids, [image distortion](@entry_id:171444), and spatial misregistration, can obscure pathology and compromise diagnostic confidence. However, understanding susceptibility is a double-edged sword; it is crucial not only for troubleshooting poor image quality but also for harnessing it as a powerful source of diagnostic contrast. This article bridges the gap between the underlying physics of susceptibility and its profound practical consequences in clinical and research imaging.

First, we will delve into the **Principles and Mechanisms**, exploring the physics of how [material interfaces](@entry_id:751731) disrupt the magnetic field and how this translates into signal changes and image artifacts. Next, in **Applications and Interdisciplinary Connections**, we will examine how these effects present challenges in clinical practice—from neurosurgery to radiotherapy—and how the same principles form the basis for advanced techniques like fMRI and Susceptibility-Weighted Imaging. Finally, **Hands-On Practices** will solidify this knowledge through practical problems, allowing you to calculate and model the impact of susceptibility artifacts firsthand.

## Principles and Mechanisms

The presence of any material within the main magnetic field of an MRI scanner alters that field, albeit typically by a very small amount. This phenomenon, known as [magnetic susceptibility](@entry_id:138219), is the origin of a class of significant and ubiquitous artifacts in magnetic resonance imaging. Understanding the principles of [magnetic susceptibility](@entry_id:138219) and the mechanisms by which it generates image artifacts is crucial for both interpreting MR images and optimizing acquisition protocols. This chapter delineates these fundamental principles, beginning with the physics of magnetism in matter and culminating in the specific image distortions and signal losses observed in clinical practice.

### The Physics of Magnetic Susceptibility

In the macroscopic description of electromagnetism, the magnetic field within a material is described by three interrelated vector fields: the **[magnetic flux density](@entry_id:194922)** $\mathbf{B}$ (often colloquially called the magnetic field), the **[magnetic field intensity](@entry_id:197932)** $\mathbf{H}$ (also known as the [auxiliary field](@entry_id:140493)), and the **magnetization** $\mathbf{M}$. The magnetization $\mathbf{M}$ represents the density of [magnetic dipole moments](@entry_id:158175) induced within the material in response to an external field. In the International System of Units (SI), these quantities are fundamentally related by the expression:

$$
\mathbf{B} = \mu_0 (\mathbf{H} + \mathbf{M})
$$

Here, $\mu_0$ is the [vacuum permeability](@entry_id:186031), a fundamental constant. In SI units, both $\mathbf{M}$ and $\mathbf{H}$ are measured in amperes per meter ($\mathrm{A}/\mathrm{m}$), while $\mathbf{B}$ is measured in tesla ($\mathrm{T}$) [@problem_id:4899041].

For most biological tissues and other non-[ferromagnetic materials](@entry_id:261099) subjected to the magnetic fields typical of MRI, the induced magnetization $\mathbf{M}$ is directly proportional to the [magnetic field intensity](@entry_id:197932) $\mathbf{H}$. This observation allows for the definition of a simple, linear constitutive relation governed by a dimensionless quantity called the **magnetic volume susceptibility**, denoted by $\chi$:

$$
\mathbf{M} = \chi \mathbf{H}
$$

This linear relationship is an excellent approximation in the context of MRI because the magnetic response of biological tissues is far from saturation at clinical field strengths (e.g., $1.5\,\mathrm{T}$ to $7\,\mathrm{T}$). Furthermore, for most tissues, the response is **isotropic**, meaning it is independent of direction, allowing $\chi$ to be treated as a scalar. In such cases, the vectors $\mathbf{M}$ and $\mathbf{H}$ are parallel. For certain tissues with highly ordered microstructures, such as the white matter of the brain, the magnetic response can be **anisotropic**. In these cases, the direction of $\mathbf{M}$ may not be parallel to $\mathbf{H}$, and the susceptibility must be described by a [second-rank tensor](@entry_id:199780), $\boldsymbol{\chi}$, where the relationship is $M_i = \sum_j \chi_{ij} H_j$ [@problem_id:4899041]. For the majority of this chapter, we will assume an isotropic response.

By substituting the linear constitutive relation into the fundamental equation for $\mathbf{B}$, we obtain a direct relationship between $\mathbf{B}$ and $\mathbf{H}$ for a linear, isotropic medium:

$$
\mathbf{B} = \mu_0 (\mathbf{H} + \chi \mathbf{H}) = \mu_0 (1 + \chi) \mathbf{H}
$$

For biological tissues, the magnitude of susceptibility is very small, typically on the order of $|\chi| \sim 10^{-6}$ to $10^{-5}$, meaning $|\chi| \ll 1$. This weak response is the foundation for classifying materials into distinct magnetic categories based on the sign and magnitude of $\chi$ [@problem_id:4899088].

*   **Diamagnetism**: In [diamagnetic materials](@entry_id:264470), the induced magnetization opposes the applied magnetic field, resulting in a negative susceptibility ($\chi  0$). This is a universal quantum mechanical effect arising from the perturbation of electron orbitals by the external field. The effect is very weak, with typical values around $\chi \sim -10^{-5}$. Water, and by extension most soft tissues, are predominantly diamagnetic.

*   **Paramagnetism**: In paramagnetic materials, the constituent atoms or molecules possess permanent [magnetic dipole moments](@entry_id:158175), usually due to unpaired electrons. In an external field, these moments tend to align with the field, producing a magnetization in the same direction as the field. This results in a positive susceptibility ($\chi > 0$). While also a weak effect, paramagnetism is generally stronger than [diamagnetism](@entry_id:148741), with typical values in the range of $\chi \sim 10^{-5}$ to $10^{-3}$. Important paramagnetic substances in MRI include deoxyhemoglobin (the basis of BOLD fMRI) and gadolinium-based contrast agents.

*   **Ferromagnetism**: In [ferromagnetic materials](@entry_id:261099) like iron, cobalt, and nickel, quantum mechanical exchange interactions cause electron spins to align spontaneously in macroscopic regions called domains. An external field can cause these domains to align, producing a very large magnetization that enhances the applied field. This corresponds to a large, positive, and highly [nonlinear susceptibility](@entry_id:136819), with effective values of $\chi \gg 1$. Ferromagnetic materials are not naturally present in the body but may be introduced as surgical clips, implants, or accidental foreign bodies. Their extremely high susceptibility causes profound local field distortions, leading to severe artifacts and posing significant safety risks in MRI [@problem_id:4899088].

### Generation of Field Inhomogeneities

The uniformity of the main magnetic field, $B_0$, is paramount for accurate [spatial encoding](@entry_id:755143) and high-quality imaging in MRI. Magnetic susceptibility creates artifacts precisely because it disrupts this uniformity. A perfectly homogeneous object with uniform susceptibility $\chi$ placed in a uniform field $\mathbf{B}_0$ would result in a uniform internal field, which would not cause artifacts. The problem arises at the **interface** between materials with different susceptibilities.

Consider an interface separating two media with susceptibilities $\chi_1$ and $\chi_2$. The principles of magnetostatics dictate the behavior of the magnetic fields across this boundary. In the absence of free surface currents, two boundary conditions must be met:
1.  The component of the [magnetic flux density](@entry_id:194922) $\mathbf{B}$ normal (perpendicular) to the interface is continuous.
2.  The component of the [magnetic field intensity](@entry_id:197932) $\mathbf{H}$ tangential (parallel) to the interface is continuous.

These boundary conditions force the magnetic field lines to bend at the interface, creating local variations in the magnitude and direction of the $\mathbf{B}$ field. The magnitude of this perturbation depends critically on the **susceptibility difference**, $\Delta\chi = \chi_1 - \chi_2$, and the geometry of the interface with respect to the main field $\mathbf{B}_0$.

A classic and illustrative example is an infinite planar interface between two materials, where the normal to the plane makes an angle $\theta$ with the main field $\mathbf{B}_0$. By applying the boundary conditions, one can derive the perturbation in the magnetic field component parallel to $\mathbf{B}_0$. To first order in the small susceptibility values, this perturbation, $\Delta B_{\parallel}$, is given by:

$$
\Delta B_{\parallel} \approx B_0 \, \Delta\chi \, \sin^2\theta
$$
[@problem_id:4899075]

This simple expression reveals a profound insight: the field perturbation is maximal when the interface is perpendicular to the main field ($\theta = 90^\circ$, so $\sin^2\theta = 1$) and is nonexistent when the interface is parallel to the field ($\theta = 0^\circ$, so $\sin^2\theta = 0$). This explains why susceptibility artifacts are most pronounced at air-tissue interfaces in regions like the sinuses or the ear canals, particularly on surfaces oriented perpendicular to the scanner's $B_0$ field.

The geometry of the object causing the susceptibility difference dictates the spatial pattern of the field perturbation. While a planar interface creates a uniform shift on either side, a spherical object creates a more complex **dipolar** field pattern outside the sphere, where the field perturbation scales with the second Legendre polynomial, $(3\cos^2\theta - 1)$, where $\theta$ is the angle relative to the $B_0$ axis. In another illustrative case, an infinitely long cylinder with its axis aligned *parallel* to the $B_0$ field produces a uniform [field shift](@entry_id:165702) *inside* the cylinder but, remarkably, **no field perturbation at all outside** the cylinder [@problem_id:4899057]. This highlights the strong dependence of the resulting artifact on both the object's shape and its orientation relative to the main magnetic field.

### From Field Perturbation to Signal Alteration

The [local field](@entry_id:146504) perturbations, denoted $\Delta B(\mathbf{r})$, directly impact the [nuclear magnetic resonance](@entry_id:142969) signal by altering the precession frequency of spins.

#### Larmor Frequency Shift and Phase Accrual

The fundamental Larmor equation states that the precession frequency, $\omega$, of a nuclear spin is directly proportional to the magnetic field it experiences: $\omega = \gamma B$, where $\gamma$ is the gyromagnetic ratio. In the presence of a susceptibility-induced perturbation $\Delta B(\mathbf{r})$, the [local field](@entry_id:146504) becomes $B(\mathbf{r}) = B_0 + \Delta B(\mathbf{r})$. Consequently, the local Larmor frequency is shifted by an amount:

$$
\Delta\omega(\mathbf{r}) = \gamma \Delta B(\mathbf{r})
$$

This is often expressed in Hertz as $\Delta f(\mathbf{r}) = \frac{\gamma}{2\pi} \Delta B(\mathbf{r})$. This frequency shift may seem small, but its effect accumulates over time. For example, a modest [field shift](@entry_id:165702) of $\Delta B = 20\,\mu\mathrm{T}$ for protons (with $\gamma/2\pi \approx 42.58\,\mathrm{MHz/T}$) results in a frequency shift of $\Delta f = 851.6\,\mathrm{Hz}$ [@problem_id:4899063].

In the [rotating frame of reference](@entry_id:171514) used for MRI analysis, this off-[resonance frequency](@entry_id:267512) causes the transverse magnetization to accumulate a phase shift, $\phi(\mathbf{r}, t)$, over time. For a static field perturbation, the phase accumulated by time $t$ is simply:

$$
\phi(\mathbf{r}, t) = \Delta\omega(\mathbf{r}) \cdot t = \gamma \Delta B(\mathbf{r}) \cdot t
$$
[@problem_id:4899052]

Continuing our example, at an echo time of $TE = 15\,\mathrm{ms}$, the accumulated phase would be $\Delta\phi = 2\pi \Delta f \cdot TE \approx 80.26$ radians [@problem_id:4899063]. This large phase shift demonstrates how even tiny field perturbations can have a dramatic effect on the MR signal.

The consequences of this phase accrual depend on the [pulse sequence](@entry_id:753864) used.

*   In a **Gradient-Recalled Echo (GRE)** sequence, the phase evolves freely until the echo time, $TE$. The phase of the measured complex signal at each voxel is therefore directly proportional to the local field perturbation: $\phi(\mathbf{r}, TE) = \gamma \Delta B(\mathbf{r}) TE$. The resulting phase image is effectively a map of the underlying field inhomogeneity (modulo $2\pi$ wrapping). This principle is the basis for quantitative susceptibility mapping (QSM) and other field mapping techniques [@problem_id:4899052].

*   In a **Spin-Echo (SE)** sequence, a $180^\circ$ refocusing pulse is applied at time $TE/2$. This pulse reverses the accumulated phase. In the second half of the echo period (from $TE/2$ to $TE$), the spins continue to precess under the same static off-resonance, but this evolution now cancels out the phase accrued during the first half. The net phase due to static field inhomogeneity at the echo time $TE$ is therefore zero. Spin-echo sequences are thus inherently robust to the effects of static susceptibility-induced [phase shifts](@entry_id:136717) [@problem_id:4899052].

### Manifestations as Image Artifacts

The phase evolution described above translates into three primary types of image artifacts: signal loss, geometric distortion, and signal pile-up.

#### Signal Loss: Intravoxel Dephasing and T2* Decay

The most common susceptibility artifact is signal loss, particularly in GRE images. This occurs when the susceptibility-induced field perturbation, $\Delta B(\mathbf{r})$, is not uniform *within a single voxel*.

Imagine a voxel where the field perturbation varies spatially, creating a gradient of Larmor frequencies across it. At the time of excitation ($t=0$), all spins within the voxel are in phase. As they evolve, spins at different locations accumulate phase at different rates. By the time the echo is measured at $TE$, there is a distribution of phase angles among the spins in the voxel. The total signal from the voxel is the vector sum (integral) of the magnetization from all these spins. This spread of phases leads to destructive interference, causing the net signal magnitude to be significantly reduced. This phenomenon is known as **intravoxel dephasing**.

A simple model illustrates this effect clearly. Consider a voxel of width $\Delta x$ with a linear frequency gradient $g_f = \partial(\Delta f)/\partial x$ across it. The net signal at time $TE$ can be shown to decay according to a [sinc function](@entry_id:274746), $S(TE) \propto \text{sinc}(g_f \cdot TE \cdot \Delta x)$ [@problem_id:4899007]. The argument of the sinc function is proportional to the total phase dispersion across the voxel, $\Delta \phi = 2\pi g_f \Delta x TE$. The greater this phase dispersion—caused by stronger field gradients, larger voxels, or longer echo times—the more severe the signal loss.

This concept is crucial for distinguishing between a bulk phase shift and intravoxel [dephasing](@entry_id:146545). If a voxel experiences a uniform off-resonance (i.e., the field gradient is zero), all spins within it precess together. They will have a net phase shift, but their vector sum will not decrease in magnitude. In this idealized case, the signal magnitude decay is governed purely by intrinsic relaxation, and the signal from a GRE and an SE sequence would be identical [@problem_id:4899062]. It is the *gradient* of the susceptibility field within the voxel that causes signal loss in GRE imaging.

This leads to the distinction between two important transverse relaxation times:

*   **T2 Relaxation**: This is the "intrinsic" or "true" transverse relaxation time, reflecting irreversible signal decay due to random, fluctuating microscopic magnetic fields from spin-spin interactions. It is a fundamental property of the tissue. An ideal spin-echo sequence, by refocusing static [dephasing](@entry_id:146545), measures $T2$.

*   **T2* Relaxation**: This is the "apparent" transverse relaxation time observed in a GRE sequence. The decay is faster because it includes both the irreversible $T2$ processes and the dephasing from static, macroscopic field inhomogeneities. The relationship between the rates is additive:
    $$
    \frac{1}{T_2^*} = \frac{1}{T_2} + \frac{1}{T_2'}
    $$
    where $1/T_2' = \gamma \Delta B_{\text{static}}$ represents the rate of dephasing from static field variations within the voxel.

The Bloch-Torrey equation provides a more rigorous physical model for these phenomena, describing the evolution of magnetization density $m(\mathbf{r}, t)$ under intrinsic relaxation, static [dephasing](@entry_id:146545), and diffusion [@problem_id:4899083]. While a spin-echo refocuses dephasing from truly static fields, the effect of [molecular diffusion](@entry_id:154595) complicates the picture. As spins diffuse through a field gradient, the field they experience is no longer static from their perspective. This leads to incomplete refocusing in a spin-echo sequence, causing an additional signal loss that makes the measured *apparent* $T2$ shorter. This effect becomes more pronounced at higher main field strengths ($B_0$) where susceptibility gradients are stronger [@problem_id:4899083].

#### Geometric Distortion

In rapid imaging sequences like Echo Planar Imaging (EPI), which are essential for applications like fMRI and diffusion-weighted imaging, susceptibility-induced off-resonance primarily manifests as **geometric distortion**.

In a standard single-shot EPI acquisition, all the lines of k-space in one direction (the phase-encoding direction) are acquired sequentially after a single excitation. This process takes a finite amount of time, known as the total readout time, which is equal to the number of phase-encode lines ($N_{pe}$) multiplied by the time between lines, or echo spacing (ESP).

An off-[resonance frequency](@entry_id:267512) $\Delta f$ causes a continuous phase accrual during this readout period. Since the acquisition time is linearly mapped to position in k-space along the phase-encode direction, the off-resonance introduces an unwanted [linear phase](@entry_id:274637) ramp onto the k-space data. According to the Fourier shift theorem, a [linear phase](@entry_id:274637) ramp in k-space corresponds to a spatial shift in the reconstructed image. The magnitude of this shift, in pixels, along the phase-encode direction is given by:

$$
|\Delta y|_{\text{pixels}} = |\Delta f \cdot N_{pe} \cdot \text{ESP}|
$$
[@problem_id:4899042]

The product $N_{pe} \cdot \text{ESP}$ is the total readout time. The distortion is therefore equal to the frequency shift multiplied by the total time over which the phase-encoding is performed. For typical EPI parameters, this can result in shifts of many pixels, causing significant warping and spatial compression or stretching of the anatomy. For instance, an off-resonance of $120\,\mathrm{Hz}$ with an ESP of $0.7\,\mathrm{ms}$ and $128$ phase-encode lines would cause a spatial shift of approximately $10.8$ pixels [@problem_id:4899042].

This formula immediately suggests strategies for mitigating geometric distortion: one must reduce the total readout time. This can be achieved by:
1.  Reducing the number of acquired phase-encode lines ($N_{pe}$) through techniques like **[parallel imaging](@entry_id:753125)**.
2.  Reducing the echo spacing (ESP) by using stronger and faster imaging gradients.

In summary, [magnetic susceptibility](@entry_id:138219) is a fundamental property of matter that gives rise to a rich set of phenomena in MRI. While it can be harnessed as a source of contrast (e.g., in BOLD fMRI and SWI), the field perturbations it creates are also responsible for some of the most challenging artifacts, including signal loss and geometric distortion, which must be understood and accounted for in modern [magnetic resonance imaging](@entry_id:153995).