## Introduction
Seismic [surface waves](@entry_id:755682), often the most prominent arrivals on seismograms from distant earthquakes, carry a wealth of information about the structure of the Earth's crust and upper mantle. The key to unlocking this information lies in **surface-wave [dispersion analysis](@entry_id:166353)**, a powerful technique that interprets how the speed of these waves varies with their frequency. This article provides a comprehensive guide to this fundamental geophysical method, addressing the central challenge of non-invasively imaging the subsurface by decoding the messages encoded in wave propagation. It is designed to take the reader from first principles to the frontiers of current research and application.

The journey begins in the "Principles and Mechanisms" chapter, where we will derive the existence of Rayleigh and Love waves from the equations of motion and boundary conditions. We will establish why these waves are non-dispersive in a uniform half-space but become dispersive in the layered Earth, and introduce the sensitivity kernels that link observed dispersion to subsurface structure. The second chapter, "Applications and Interdisciplinary Connections," transitions from theory to practice. It details advanced signal processing techniques like [ambient noise interferometry](@entry_id:746394) for measuring [dispersion curves](@entry_id:197598) and explores the intricacies of the inverse problem to convert these curves into velocity models, highlighting a wide array of applications in fields from geotechnical engineering to planetary seismology. Finally, the "Hands-On Practices" chapter provides a set of computational problems to solidify your understanding and build practical skills in modeling and inverting surface-wave data.

## Principles and Mechanisms

The existence and behavior of seismic [surface waves](@entry_id:755682) are a direct consequence of the interaction between [elastic waves](@entry_id:196203) and the Earth's free surface, as well as its internal layering. Unlike body waves, which can propagate throughout the entirety of a medium, surface waves are guided modes, with their energy trapped near the surface. This chapter elucidates the fundamental principles governing their formation, propagation, and dispersion, providing the theoretical foundation for their use in seismological analysis.

### The Genesis of Guided Waves in an Elastic Half-Space

The propagation of seismic waves in a linear, isotropic, elastic solid is governed by the Navier [equation of motion](@entry_id:264286):
$$
\rho \, \frac{\partial^2 \mathbf{u}}{\partial t^2} = (\lambda+\mu) \nabla \left( \nabla \cdot \mathbf{u} \right) + \mu \nabla^2 \mathbf{u}
$$
where $\mathbf{u}$ is the displacement vector, $\rho$ is the density, and $\lambda$ and $\mu$ are the Lamé parameters. In an unbounded medium, this equation admits two types of solutions: compressional (P) waves with speed $\alpha = \sqrt{(\lambda+2\mu)/\rho}$ and shear (S) waves with speed $\beta = \sqrt{\mu/\rho}$.

The introduction of a boundary, such as the Earth's surface, fundamentally alters the problem. At this interface, physical constraints must be satisfied. For the Earth's surface, which is in contact with the atmosphere, we impose the **[traction-free boundary](@entry_id:197683) condition**. This condition stipulates that no forces are exerted on the surface. Mathematically, this means that all components of the [traction vector](@entry_id:189429), $\mathbf{t} = \boldsymbol{\sigma} \cdot \mathbf{n}$ (where $\boldsymbol{\sigma}$ is the stress tensor and $\mathbf{n}$ is the normal to the surface), must vanish. For a horizontal surface at $z=0$, this requires the stress components $\sigma_{zz}$, $\sigma_{xz}$, and $\sigma_{yz}$ to be zero at $z=0$ .

To satisfy the governing equations and these boundary conditions simultaneously, a special class of solutions arises. These solutions, known as [surface waves](@entry_id:755682), are characterized by their **evanescence**: their amplitude decays exponentially with increasing depth from the surface. A wave is considered "guided" or "trapped" if its [displacement field](@entry_id:141476) $\mathbf{u}(x,z,t)$ decays to zero as $z \to \infty$ . This confinement of energy near the surface is the defining characteristic of a surface wave. For this to occur, the wave's horizontal [phase velocity](@entry_id:154045), $c$, must be less than the body-wave speeds of the medium it is propagating into at depth.

In a more complex Earth with internal layers, additional conditions must be met at each interface between layers. For a **welded contact**, which assumes the layers are perfectly bonded, both the displacement vector $\mathbf{u}$ and the [traction vector](@entry_id:189429) $\mathbf{t}$ must be continuous across the interface . These conditions ensure that the layers do not slip past or separate from one another, and that forces are transmitted realistically. It is the combination of the free-surface condition and these internal [interface conditions](@entry_id:750725) that gives rise to the rich variety of surface-wave phenomena.

### The Fundamental Wave Types: Rayleigh and Love Waves

In isotropic media, the displacement field can be decoupled into two independent systems: motion in the vertical plane of propagation (P-SV system) and motion transverse to the direction of propagation (SH system). This [decoupling](@entry_id:160890) gives rise to two distinct families of surface waves: Rayleigh waves and Love waves.

#### Rayleigh Waves

Rayleigh waves arise from the coupling of compressional (P) and vertically-polarized shear (SV) waves. A P-wave or an SV-wave alone cannot satisfy the [traction-free boundary](@entry_id:197683) conditions at the surface. However, a specific combination of the two can. We seek solutions that propagate horizontally with [wavenumber](@entry_id:172452) $k$ and [angular frequency](@entry_id:274516) $\omega$, and are evanescent with depth. This evanescence requires the horizontal phase velocity $c = \omega/k$ to be less than the bulk shear-[wave speed](@entry_id:186208), $c  \beta$ . When this condition is met, the vertical dependence of the P and SV potentials takes the form of exponentially decaying functions, $\exp(-q_\alpha z)$ and $\exp(-q_\beta z)$, where the decay rates are real and positive. The coupling of the two wave types results in a characteristic particle motion that is a retrograde ellipse in the vertical plane (the sagittal plane) .

For the simple case of a uniform, homogeneous half-space, the requirement that a non-[trivial solution](@entry_id:155162) exists leads to the **Rayleigh [secular equation](@entry_id:265849)**. This equation relates the [phase velocity](@entry_id:154045) $c$ to the material properties $\alpha$ and $\beta$. A common form of this equation is a cubic polynomial in $y = (c/\beta)^2$:
$$
y^3 - 8 y^2 + 8\bigl(3 - 2 r\bigr) y - 16\bigl(1 - r\bigr) = 0
$$
where $r = (\beta/\alpha)^2$ is the squared ratio of the body-wave speeds . The crucial insight from this equation is that the solution for $y$, and thus for the Rayleigh-wave [phase velocity](@entry_id:154045) $c$, depends only on the material properties, not on the frequency $\omega$ or wavenumber $k$. This means that in a homogeneous half-space, Rayleigh waves are **non-dispersive**: all frequencies travel at the same phase velocity.

#### Love Waves

Love waves are fundamentally different. They consist of purely Shear-Horizontal (SH) motion, with particles oscillating perpendicular to the direction of wave propagation. A key distinction is that **Love waves cannot exist in a simple homogeneous half-space** . An evanescent SH wave in a uniform half-space cannot by itself satisfy the [traction-free boundary](@entry_id:197683) condition; this forces the wave amplitude to be zero.

The existence of Love waves requires a specific type of vertical heterogeneity: a layer with a lower shear-[wave speed](@entry_id:186208) overlying a half-space with a higher shear-wave speed, i.e., $\beta_{\text{layer}}  \beta_{\text{half}}$ . This low-velocity layer acts as a [waveguide](@entry_id:266568). The physical mechanism for trapping is the [constructive interference](@entry_id:276464) of SH waves that are totally internally reflected at the interface with the faster material below. For this to occur, the wave's [phase velocity](@entry_id:154045) $c$ must be bracketed by the shear speeds of the two media:
$$
\beta_{\text{layer}}  c  \beta_{\text{half}}
$$
This condition ensures that the wave is oscillatory (trapped) within the low-velocity layer but evanescent (decaying) in the underlying half-space, thus forming a guided wave .

### Dispersion: The Signature of Structure

The non-dispersive nature of Rayleigh waves in a homogeneous half-space is a special case. The moment we introduce vertical structure, such as the low-velocity layer required for Love waves, or any stack of layers, a [characteristic length](@entry_id:265857) scale (the layer thickness) is introduced into the problem. This breaks the simple scaling relationship and causes the phase velocity to become dependent on frequency. This phenomenon is called **dispersion**.

The relationship between [angular frequency](@entry_id:274516) $\omega$ and [wavenumber](@entry_id:172452) $k$ for a given mode in a layered medium is encapsulated by the **[dispersion relation](@entry_id:138513)**, which is implicitly defined by the [secular equation](@entry_id:265849) $D(\omega,k)=0$. From this relation, two key velocities are defined :

1.  **Phase Velocity ($c(\omega) = \omega/k(\omega)$):** This is the speed at which a point of constant phase (e.g., a wave crest) on a single-frequency wave propagates.

2.  **Group Velocity ($U(\omega) = d\omega/dk$):** This is the speed of the envelope of a [wave packet](@entry_id:144436) composed of a narrow band of frequencies. In a lossless medium, it also represents the velocity of energy transport.

In a typical Earth model where seismic velocities increase with depth, dispersion exhibits a characteristic pattern. The penetration depth of a surface wave is proportional to its wavelength, and therefore inversely proportional to its frequency . Low-frequency (long-period) waves penetrate deeper, sampling the faster velocities of the deeper Earth, and thus exhibit a higher phase velocity. Conversely, high-frequency (short-period) waves are confined to the shallower, slower parts of the crust and have a lower phase velocity. This behavior, where phase velocity decreases with increasing frequency ($dc/d\omega  0$), is defined as **[normal dispersion](@entry_id:175792)** for [surface waves](@entry_id:755682) . The opposite case, where phase velocity increases with frequency ($dc/d\omega > 0$), is known as **[anomalous dispersion](@entry_id:270636)** and can occur in structures with significant low-velocity zones.

### The Complete Modal Solution: Overtones

For a given layered structure and a fixed frequency $\omega$, the [secular equation](@entry_id:265849) $D(\omega,k)=0$ generally does not have a single solution for the [wavenumber](@entry_id:172452) $k$. Instead, it has a [discrete set](@entry_id:146023) of solutions, $k_0, k_1, k_2, \dots$. Each solution corresponds to a distinct **mode** of propagation.

These modes are indexed by an integer $n=0, 1, 2, \dots$ which has a direct physical meaning: it corresponds to the number of **nodes** (zero-crossings) in the vertical displacement eigenfunction of the mode .

*   **Fundamental Mode ($n=0$):** This mode has no nodes in its depth eigenfunction. For a given frequency, it has the lowest [phase velocity](@entry_id:154045) ($c_0$) and largest wavenumber ($k_0$). Its energy is typically concentrated at the shallowest depths.

*   **Overtones ($n \ge 1$):** The first overtone ($n=1$) has one node, the second overtone ($n=2$) has two, and so on. To accommodate the more complex, oscillatory vertical structure, higher overtones must penetrate deeper into the medium. In a structure with increasing velocity with depth, this means higher [overtones](@entry_id:177516) have progressively higher phase velocities ($c_0  c_1  c_2  \dots$).

A crucial feature of overtones is the existence of **cutoff frequencies**. Because an overtone requires a certain vertical wavelength to "fit" its oscillations into the waveguide, it cannot be supported if the horizontal wavelength is too long (i.e., the frequency is too low). Consequently, each overtone ($n \ge 1$) has a specific cutoff frequency below which it cannot exist as a trapped guided wave .

### From Observation to Inference: Sensitivity Kernels

The analysis of surface-[wave dispersion](@entry_id:180230) is a powerful tool because the measured [dispersion curve](@entry_id:748553), $c(\omega)$, contains integrated information about the seismic velocity structure of the Earth, particularly the shear-wave speed profile $V_S(z)$. To invert the dispersion data for Earth structure, we must understand how a change in structure affects the observed wave speed. This relationship is formalized by **Fréchet sensitivity kernels**.

A Fréchet kernel, $K_{c,V_S}(z, \omega)$, quantifies the sensitivity of the phase velocity $c$ at a specific frequency $\omega$ to a small perturbation in the shear-wave speed $V_S$ at a specific depth $z$. The relationship is expressed through a linear integral:
$$
\delta \ln c(\omega) = \int_{0}^{\infty} K_{c,V_S}(z,\omega) \, \delta \ln V_S(z) \, \mathrm{d}z
$$
The kernel can be derived from the variational principles of [elastodynamics](@entry_id:175818) and is expressed in terms of the mode's eigenfunctions and energy. A common and insightful form for the kernel is :
$$
K_{c,V_S}(z,\omega) = \frac{ c(\omega) }{ U(\omega) } \, \frac{ e_s(z) }{ E }
$$
This expression reveals the physics of sensitivity:
*   The sensitivity at a depth $z$ is directly proportional to the **shear-[strain energy density](@entry_id:200085)**, $e_s(z)$, at that depth. A wave is most sensitive to the structure where its [strain energy](@entry_id:162699) is concentrated.
*   The sensitivity is inversely proportional to the **total energy of the mode**, $E$, integrated over all depths.
*   The factor $c(\omega)/U(\omega)$ is a crucial scaling term that converts the sensitivity from a fixed-[wavenumber](@entry_id:172452) framework, which is natural for theoretical derivations, to the fixed-frequency framework in which measurements are typically made.

By calculating these kernels for a range of frequencies, we can understand which parts of a dispersion curve are sensitive to which depth ranges, forming the basis for tomographic inversion.

### Surface Waves versus Body Waves: A Global Perspective

The principles outlined above explain why surface waves, despite being confined to a small fraction of the Earth's volume, are often the most prominent feature on seismograms recorded at large distances from an earthquake. Two primary factors contribute to their dominance :

1.  **Geometrical Spreading:** Body waves radiating from a point source spread their energy over a spherical [wavefront](@entry_id:197956), whose area grows with distance squared ($r^2$). Consequently, their amplitude decays as $r^{-1}$. Surface waves, trapped near the surface, spread their energy over a cylindrical wavefront, whose area grows linearly with distance ($r$). Their amplitude therefore decays much more slowly, as $r^{-1/2}$.

2.  **Anelastic Attenuation:** The Earth is not perfectly elastic, and seismic waves lose energy to friction as they propagate. This attenuation is strongly frequency-dependent, with high-frequency waves being attenuated much more severely than low-frequency waves.

At large epicentral distances, the combination of these two effects is profound. The slower amplitude decay due to cylindrical spreading means surface waves retain their energy far better than body waves. Furthermore, the long-period components of the surface-wave train are minimally affected by anelastic attenuation, allowing them to travel across entire oceans and continents while higher-frequency body waves are largely dissipated. The result is that at teleseismic distances, the largest-amplitude arrivals on a seismogram are almost invariably the long-period surface waves.