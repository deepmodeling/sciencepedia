## Introduction
Magnetic Resonance Imaging (MRI) stands as a pillar of modern diagnostic medicine, prized for its ability to produce high-contrast images of soft tissues without using ionizing radiation. The quality of these images, however, is contingent on a complex interplay of physics and engineering, and is susceptible to various artifacts that can obscure pathology or mimic disease. Among the most common and fundamental of these is the **wrap-around artifact**, also known as aliasing. While frequently encountered, the underlying principles that govern its appearance and the sophisticated methods used to correct it are often misunderstood.

This article addresses this knowledge gap by providing a definitive guide to the wrap-around artifact. We will demystify this phenomenon, moving from its mathematical foundations to its practical consequences and clinical management. The article is structured to build a complete and actionable understanding across three chapters. In "Principles and Mechanisms," you will learn how the process of converting MRI signals into an image via the Fourier transform inevitably creates the conditions for aliasing. "Applications and Interdisciplinary Connections" will explore how this artifact manifests in clinical scans and examine the array of strategies—from simple parameter changes to advanced technologies like [parallel imaging](@entry_id:753125)—used to diagnose and eliminate it. Finally, "Hands-On Practices" will solidify your understanding with targeted exercises. By the end, you will not only be able to recognize wrap-around but will also grasp the physics and engineering principles required to master it.

## Principles and Mechanisms

The formation of an image in Magnetic Resonance Imaging (MRI) is a masterful application of Fourier analysis, translating signals encoded in the spatial frequency domain (k-space) back into a spatial representation of the object. However, the practical necessity of acquiring a finite number of discrete samples from k-space, rather than the complete, continuous signal, introduces specific and predictable deviations from a [perfect reconstruction](@entry_id:194472). The most fundamental of these is the **wrap-around artifact**, also known as **aliasing** or **fold-over**. This chapter will dissect the physical and mathematical principles that give rise to this artifact, distinguish it from other common artifacts, and explore its manifestations and mitigation strategies across different imaging contexts.

### The Fourier Basis of Aliasing: From Continuous to Discrete

The foundational relationship in MRI is that the acquired k-space signal, $S(\mathbf{k})$, is the Fourier transform of the object's spatial [spin density](@entry_id:267742), $\rho(\mathbf{x})$:
$$
S(\mathbf{k}) = \int \rho(\mathbf{x}) e^{-i 2\pi \mathbf{k} \cdot \mathbf{x}} d\mathbf{x}
$$
In theory, one could recover the image perfectly by performing the inverse Fourier transform. In practice, the MRI scanner samples the continuous signal $S(\mathbf{k})$ at discrete locations. In standard Cartesian imaging, these samples are taken on a uniform grid. Let us consider the one-dimensional case for clarity. Here, k-space is sampled at uniform intervals of $\Delta k$.

This sampling process can be modeled as multiplying the true, continuous k-space signal $S(k)$ by an infinite train of Dirac delta functions, known as a Dirac comb or Shah function, with spacing $\Delta k$. The convolution theorem of Fourier analysis dictates that multiplication in one domain is equivalent to convolution in the conjugate domain. The inverse Fourier transform of a Dirac comb in the frequency domain is another Dirac comb in the spatial domain, but with a spacing of $1/\Delta k$.

Consequently, the reconstructed image is not the true object profile $\rho(x)$, but rather a convolution of $\rho(x)$ with this spatial-domain comb. This convolution results in an infinite series of replicas of the true object, periodically repeated at intervals of $1/\Delta k$ [@problem_id:4532984]:
$$
\rho_{\text{recon}}(x) = \sum_{m=-\infty}^{\infty} \rho\left(x - \frac{m}{\Delta k}\right)
$$
This period of replication, $1/\Delta k$, defines the scanner's **Field of View (FOV)**. The fundamental relationship is thus:
$$
\mathrm{FOV} = \frac{1}{\Delta k}
$$
This mathematical inevitability is at the heart of the wrap-around artifact. The use of the **Discrete Fourier Transform (DFT)**, the computational engine of MRI reconstruction, codifies this behavior. The DFT, by its very definition, treats any finite sequence of $N$ points as a single period of an infinitely periodic sequence. Both the input k-space data and the output image data are implicitly assumed to be periodic with a period of $N$ samples [@problem_id:4920777]. This means that the right edge of the reconstructed image is mathematically adjacent to its left edge, setting the stage for aliasing.

If the physical extent of the object being imaged, $L_{\text{obj}}$, is larger than the FOV, the periodically replicated copies of the object will overlap. The parts of the object that lie outside the FOV will be "wrapped around" and superimposed onto the opposite side of the image. This is the wrap-around artifact. The condition to avoid aliasing, often called the imaging Nyquist criterion, is simply that the FOV must be large enough to contain the entire object:
$$
\mathrm{FOV} \ge L_{\text{obj}} \quad \implies \quad \frac{1}{\Delta k} \ge L_{\text{obj}} \quad \implies \quad \Delta k \le \frac{1}{L_{\text{obj}}}
$$
For example, if an object has a true extent of $L_{\text{obj}} = 30$ cm, but the acquisition is programmed with a k-space sampling step that yields an FOV of only $24$ cm, wrap-around is guaranteed to occur [@problem_id:4941738]. The $6$ cm of tissue outside the FOV ($3$ cm on each side) will appear folded into the image.

### Distinguishing Wrap-Around Aliasing from Gibbs Ringing

Students of MRI often confuse wrap-around aliasing with another common artifact: **Gibbs ringing**. While both are consequences of non-ideal k-space acquisition, their physical origins are entirely distinct and are governed by different acquisition parameters.

**Wrap-around aliasing** is an artifact of **sampling**. It is caused by the k-space sampling interval, $\Delta k$, being too large, which results in an FOV that is too small.

**Gibbs ringing**, in contrast, is an artifact of **truncation**. It arises because k-space is only sampled out to a finite maximum extent, $\pm k_{\text{max}}$. This truncation is equivalent to multiplying the true k-space signal by a [rectangular window](@entry_id:262826) function. The inverse Fourier transform of this [rectangular window](@entry_id:262826) is a sinc function ($\mathrm{sinc}(x) = \sin(\pi x) / (\pi x)$). By the convolution theorem, the reconstructed image is the true object profile convolved with this sinc-like [point-spread function](@entry_id:183154) (PSF). This convolution blurs the image, defining its spatial resolution, and produces characteristic oscillations or "ringing" near sharp intensity discontinuities (e.g., the edge of a phantom, or interfaces like bone-cortex or skull-fat) [@problem_id:4941765] [@problem_id:4941738].

The key distinctions are summarized below:
*   **Governing Parameter:** Aliasing depends on $\Delta k$ (FOV). Gibbs ringing depends on $k_{\text{max}}$ (resolution).
*   **Appearance:** Aliasing is a macroscopic folding of anatomy from one side of the image to the other. Gibbs ringing appears as fine, [parallel lines](@entry_id:169007) or oscillations adjacent to sharp edges.
*   **Mitigation:** Aliasing is corrected by increasing the FOV, which requires *decreasing* $\Delta k$. Gibbs ringing can only be mitigated, for example, by filtering the k-space data ([apodization](@entry_id:147798)) or by improving resolution (increasing $k_{\text{max}}$), which compresses the ringing closer to the edge but does not eliminate the fundamental overshoot.

A powerful thought experiment can cement this distinction. Imagine an initial acquisition where the object is larger than the FOV, resulting in both wrap-around and Gibbs ringing. Now, let's increase the FOV while keeping the spatial resolution constant. To achieve this, we must decrease $\Delta k$ (to increase the FOV) and hold $k_{\text{max}}$ constant (to maintain resolution). Since the total number of samples $N$ is related by $k_{\text{max}} \approx (N/2)\Delta k$, this requires increasing $N$. In this scenario, the wrap-around artifact will be reduced or eliminated because the FOV is now large enough to contain the object. However, because $k_{\text{max}}$ has not changed, the k-space truncation window is identical, the sinc-like PSF is unchanged, and the Gibbs [ringing artifact](@entry_id:166350) will remain essentially the same [@problem_id:4941750].

### Aliasing in Practice: Cartesian MRI

In standard 2D Cartesian MRI, k-space is sampled on a rectangular grid, but the acquisition process is asymmetric. One direction, the **frequency-encoding** or **readout** direction (typically designated $x$), is sampled rapidly during the application of a readout gradient. The other direction, the **phase-encoding** direction ($y$), is built up line-by-line, with each line acquired after a separate phase-encoding gradient pulse and subsequent RF excitation (in conventional spin echo) or as part of a single-shot trajectory (in EPI).

This asymmetry has profound implications for wrap-around. The artifact is most commonly encountered in the **phase-encoding direction**. The reason lies in how the FOV is determined for each axis [@problem_id:4941782]:
*   **Phase-Encode FOV ($\mathrm{FOV}_y$):** This is directly determined by the step size between phase-encoding gradients, which sets $\Delta k_y$. Thus, $\mathrm{FOV}_y = 1/\Delta k_y$. The operator explicitly chooses the phase-encode FOV, and if it is set smaller than the patient's dimension in that direction, wrap-around will occur. For instance, if $\Delta k_y$ is set to $6.0 \text{ m}^{-1}$, the resulting $\mathrm{FOV}_y$ is only $1/6.0 \approx 0.167$ m or $16.7$ cm. An object of size $22$ cm would certainly alias in this direction.

*   **Frequency-Encode FOV ($\mathrm{FOV}_x$):** This is determined by the readout gradient strength $G_x$ and the sampling rate of the [analog-to-digital converter](@entry_id:271548) (ADC), $f_s$, which sets the sampling time interval $\Delta t = 1/f_s$. The k-space step is $\Delta k_x = \gamma G_x \Delta t$. Therefore, $\mathrm{FOV}_x = 1/\Delta k_x = f_s / (\gamma G_x)$. Modern scanners often employ **[oversampling](@entry_id:270705)** in the readout direction, where the ADC samples much faster than required by the [image resolution](@entry_id:165161). This effectively makes $\Delta k_x$ very small and $\mathrm{FOV}_x$ very large, often twice the prescribed FOV. This provides a built-in [anti-aliasing](@entry_id:636139) mechanism in the frequency-encode direction at no extra time cost.

#### Strategies for Correcting Wrap-Around

When wrap-around is observed, the fundamental solution is to increase the FOV until it encompasses the object. This is achieved by decreasing the k-space sampling interval, $\Delta k$. It is crucial to understand what does, and does not, accomplish this. Consider an object of extent $L_{obj}=40$ cm imaged with an initial FOV of $32$ cm, which causes aliasing [@problem_id:4941776].
*   **Correct Strategy: Increase FOV.** By reducing $\Delta k$ from $1/32 \text{ cm}^{-1}$ to $1/48 \text{ cm}^{-1}$, the FOV is increased to $48$ cm. Since $48 \text{ cm} > 40 \text{ cm}$, the aliasing is resolved. This is the standard "no phase wrap" or "fold-over suppression" option on clinical scanners. Note that if the number of phase-encoding steps $N$ is kept constant, this change will decrease the k-space extent $k_{max} = (N/2)\Delta k$, thereby reducing spatial resolution. To maintain resolution, $N$ must be increased, which increases scan time.

*   **Incorrect Strategy: Increase Matrix Size at Fixed FOV.** A common misconception is that increasing the number of samples (the image matrix size, e.g., from $256$ to $512$) will fix aliasing. If the FOV (and thus $\Delta k$) is held constant, increasing $N$ does *not* solve the aliasing problem. The FOV remains unchanged at $32$ cm and continues to be smaller than the object. What this action *does* accomplish is an increase in spatial resolution, as the k-space coverage $k_{max}$ is increased. The image will appear sharper, but the wrap-around artifact will persist [@problem_id:4941776].

### Advanced Contexts and Related Artifacts

While the principles above form the core understanding of wrap-around, several related concepts and sequence-specific artifacts warrant discussion to provide a complete picture.

#### Chemical Shift Artifact vs. Wrap-Around

In the frequency-encoding direction, another source of spatial misregistration is **chemical shift**. Protons in fat resonate at a slightly lower frequency than those in water. The MRI scanner assumes frequency differences are due to position in the [gradient field](@entry_id:275893). This causes the fat signal to be systematically misplaced along the frequency-encoding axis. The magnitude of this displacement, $\Delta x$, can be derived from first principles and depends on the frequency shift $\Delta f$ and the frequency-encoding parameters [@problem_id:4941721]:
$$
\Delta x = \Delta f \frac{\mathrm{FOV}_x}{f_s}
$$
where $f_s$ is the total readout sampling bandwidth. For a 3T scanner, the fat-water frequency shift is about $440$ Hz. With a typical bandwidth of $100$ kHz and a $256$ mm FOV, the resulting displacement is only about $1.1$ mm. This appears as a small spatial offset of fat relative to water, not a full-image fold-over. Chemical shift can only cause true wrap-around if the readout bandwidth is made extremely low, a situation not encountered in standard practice.

#### Aliasing in Echo Planar Imaging (EPI)

In fast sequences like EPI, wrap-around in the phase-encode direction is a common concern. However, it must be distinguished from another characteristic EPI artifact: the **N/2 ghost** or **Nyquist ghost**.
*   **Wrap-Around in EPI** has the same origin as in conventional imaging: the phase-encode FOV ($1/\Delta k_y$) is smaller than the object. It is a true [spatial aliasing](@entry_id:275674) phenomenon.
*   **The N/2 Ghost** arises from systematic phase inconsistencies between k-space lines acquired with positive versus negative readout gradients. These errors cause a "ghost" of the main image to appear shifted by exactly half the field of view ($FOV_y/2$).

A key diagnostic difference is their behavior when the polarity of the phase-encoding gradient blips is reversed. True wrap-around is unaffected by this change. The N/2 ghost, however, will flip its position to the opposite side of the main image, a property exploited by many ghost correction algorithms [@problem_id:4941783].

#### Aliasing in Non-Cartesian Trajectories: The Case of Radial MRI

The classic fold-over artifact is a direct consequence of sampling on a regular Cartesian lattice. When k-space is sampled with different geometries, [undersampling](@entry_id:272871) leads to different types of aliasing artifacts. A prime example is **radial imaging**, where k-space is sampled along spokes emanating from the center.

In this case, the sampling pattern is not a Dirac comb on a lattice. The corresponding PSF is not a spatial Dirac comb but rather a star-like shape, with a central peak and radiating ridges or "blades." When convolved with the true image, this PSF produces **streaking artifacts** that emanate from high-contrast objects, rather than discrete, folded-over replicas of the image. Therefore, [undersampling](@entry_id:272871) in radial MRI—acquiring too few spokes for the desired resolution and FOV—manifests as streaks, not wrap-around. This demonstrates the crucial principle that the geometric form of an aliasing artifact is dictated by the geometry of the k-space sampling trajectory [@problem_id:4941755].