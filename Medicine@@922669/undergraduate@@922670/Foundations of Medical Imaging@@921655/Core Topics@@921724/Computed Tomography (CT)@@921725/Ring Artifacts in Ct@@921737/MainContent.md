## Introduction
Computed [tomography](@entry_id:756051) (CT) is a cornerstone of modern medical diagnosis, providing detailed cross-sectional images that enable quantitative analysis of anatomical structures. However, the integrity of CT images can be compromised by various artifacts, which are systematic discrepancies between the CT numbers in the reconstructed image and the true attenuation coefficients of the object. Among these, ring artifacts—concentric circles superimposed on the image—are a common and distinct form of degradation. Their presence not only detracts from image quality but can also obscure pathology or corrupt quantitative data, leading to diagnostic errors or flawed research conclusions. This article addresses the critical need for a deep, first-principles understanding of how these artifacts form, their consequences, and how they can be mitigated.

This article will guide you through a comprehensive exploration of ring artifacts. The first chapter, "Principles and Mechanisms," will deconstruct the artifact's origin, tracing its path from a single faulty detector element through the mathematics of data processing and [image reconstruction](@entry_id:166790). The second chapter, "Applications and Interdisciplinary Connections," will broaden the scope to examine the profound impact of these artifacts on clinical [quality assurance](@entry_id:202984), quantitative analysis in fields like radiomics, and the development of robust artificial intelligence models. Finally, the "Hands-On Practices" chapter will provide practical problems to reinforce these theoretical concepts, bridging the gap between theory and real-world application.

## Principles and Mechanisms

Ring artifacts in [computed tomography](@entry_id:747638) (CT) are a distinct class of image degradations characterized by one or more concentric circular or annular patterns superimposed on the reconstructed image, typically centered at the scanner's isocenter. Understanding their origin is paramount for accurate diagnosis and for developing effective quality control and correction procedures. While several phenomena can degrade CT images, such as patient motion, scatter, or beam hardening, ring artifacts have a specific and traceable etiology rooted in the detector system and the mathematics of image reconstruction. Before delving into the specific mechanisms, it is essential to distinguish ring artifacts from other common image distortions. For instance, **beam hardening artifacts**, which arise from the polychromatic nature of the X-ray source, typically manifest as "cupping" (an artificial decrease in CT numbers toward the center of a uniform object) or as dark streaks between highly attenuating materials. **Scatter-induced artifacts** also produce broad, low-frequency shading and cupping. In contrast, ring artifacts are typically sharp, high-frequency features whose origin lies not in the beam-matter interaction but in imperfections within the [data acquisition](@entry_id:273490) hardware [@problem_id:4866092].

### The Physical Origin: Detector System Imperfections

The foundation of quantitative CT imaging rests on the Beer-Lambert law, which relates the incident X-ray intensity, $I_0$, to the transmitted intensity, $I$, after passing through an object. For a monoenergetic beam, this relationship is given by:
$$
I = I_0 \exp(-p)
$$
where $p$ is the [line integral](@entry_id:138107) of the material's linear attenuation coefficient, $\mu$, along the ray path. The goal of CT reconstruction is to recover the spatial map of $\mu$ from a set of projection measurements, $p$. To do this, the system first computes $p$ from the measured intensities via a logarithmic transformation:
$$
p = -\ln\left(\frac{I}{I_0}\right)
$$
This idealized model assumes a perfect detector system. In reality, each of the hundreds or thousands of detector elements in a CT scanner has its own electronic characteristics. The raw signal, $S$, from a single detector channel is more accurately described by a [linear response](@entry_id:146180) model that includes a channel-specific **gain**, $G$, and an **offset**, $O$:
$$
S = G I + O
$$
The offset, or [dark current](@entry_id:154449), is the baseline signal present even with no X-ray exposure, while the gain represents the channel's amplification of the photon-induced signal. To produce accurate projection data, these channel-to-channel variations must be meticulously calibrated out. This is achieved through routine [quality assurance](@entry_id:202984) procedures, primarily a **dark scan** (X-rays off) to measure the offsets $O_k$ for each channel $k$, and an **air scan** or **flood-field scan** (X-rays on, no object) to measure the response to the unattenuated beam, which is used to normalize the gains and account for the incident intensity profile $I_0$ [@problem_id:4828904].

Ring artifacts are the direct consequence of a failure or drift in this calibration process for one or more detector channels.

### From Detector Error to Sinogram Stripe

The mechanism by which a detector fault transforms into a ring artifact begins with its effect on the calculated projection data, which is visualized in a **sinogram**. A sinogram is a 2D plot where the vertical axis represents the projection angle, $\theta$, and the horizontal axis represents the spatial position of the detector element, $s$. An error in a single, stationary detector channel will therefore affect the same horizontal position $s_k$ for every projection angle $\theta$.

The nature of the resulting error in the [sinogram](@entry_id:754926) depends critically on whether the miscalibration is in the gain or the offset term. Let us analyze these two cases separately [@problem_id:4920439] [@problem_id:4920423].

#### Multiplicative Gain Errors

Suppose a single detector channel, $k$, has an erroneous gain. After an ideal offset correction, its measured intensity, $\tilde{I}$, is a multiple of the true intensity, $I$:
$$
\tilde{I}(\theta, s_k) = g_k I(\theta, s_k)
$$
where $g_k$ is the erroneous gain factor. When the system computes the log-projection for this channel, the error propagates as follows:
$$
p_{\text{meas}}(\theta, s_k) = -\ln\left(\frac{\tilde{I}(\theta, s_k)}{I_0(\theta, s_k)}\right) = -\ln\left(\frac{g_k I(\theta, s_k)}{I_0(\theta, s_k)}\right)
$$
Using the properties of logarithms, this becomes:
$$
p_{\text{meas}}(\theta, s_k) = -\ln(g_k) - \ln\left(\frac{I(\theta, s_k)}{I_0(\theta, s_k)}\right) = p_{\text{true}}(\theta, s_k) - \ln(g_k)
$$
This result is fundamental: a multiplicative gain error, $g_k$, introduces a constant **additive bias** of $-\ln(g_k)$ to the true projection data for that channel. Since this bias is independent of the projection angle $\theta$, it manifests in the sinogram as a **straight vertical line** or **stripe** at the position $s=s_k$ [@problem_id:4828904]. It is this characteristic signature in the sinogram that is the direct precursor to a ring artifact.

In more complex scenarios, a detector's response may be nonlinear. For instance, its measured intensity might follow a power law, $I_m = a_k I_t^{\alpha_k} + b_k$. However, by linearizing this response around a typical operating intensity (e.g., the air-scan intensity $I_0$), one can show that the behavior can be approximated by an effective gain and offset. Deviations in the nonlinear parameters $a_k$ or $\alpha_k$ will thus lead to an effective gain error, which in turn generates the additive [sinogram](@entry_id:754926) stripe responsible for rings [@problem_id:4920452].

#### Additive Offset Errors

In contrast, consider an uncorrected additive offset error, $\beta$. The measured intensity would be $\tilde{I} = I + \beta$. The error in the log-projection data becomes:
$$
\Delta p = p_{\text{meas}} - p_{\text{true}} = -\ln\left(\frac{I+\beta}{I_0}\right) - \left(-\ln\left(\frac{I}{I_0}\right)\right) = -\ln\left(1 + \frac{\beta}{I}\right)
$$
Substituting $I = I_0 \exp(-p_{\text{true}})$, the error becomes:
$$
\Delta p = -\ln\left(1 + \frac{\beta}{I_0} \exp(p_{\text{true}})\right)
$$
Unlike the gain error, this bias is highly dependent on the true projection value $p_{\text{true}}$. It is not constant. Therefore, an offset error does not produce a uniform vertical stripe in the sinogram but rather a complex, object-dependent pattern. These types of errors are a primary cause of **cupping artifacts**, not the sharp, well-defined rings caused by gain errors [@problem_id:4920439].

### From Sinogram Stripe to Reconstructed Ring

The final step in the artifact's formation is the reconstruction process itself, most commonly **Filtered Backprojection (FBP)**. The "[backprojection](@entry_id:746638)" step can be visualized as smearing each projection view back across the image grid at the angle from which it was acquired. A single point $(s_0, \theta_0)$ in the [sinogram](@entry_id:754926) is backprojected as a line in the image.

The vertical stripe in the sinogram at $s = s_k$, caused by the faulty detector, represents a data point at that same radial position for *every* angle $\theta$. The [backprojection](@entry_id:746638) algorithm will therefore superimpose an infinite number of lines in the image plane. Each line is [tangent to a circle](@entry_id:173370) of a specific radius. The geometric envelope of this family of [tangent lines](@entry_id:168168) is a sharply defined circle. This is the ring artifact [@problem_id:4828904].

More formally, the "filtered" part of FBP involves convolving each projection with a filter kernel, typically a [ramp filter](@entry_id:754034), before [backprojection](@entry_id:746638). The sinogram stripe can be mathematically modeled as a Dirac delta function, $\delta(s-s_k)$. The FBP process effectively backprojects the filter's impulse response. The central profile of the resulting ring artifact in the image is therefore determined by the shape of this impulse response, which explains the characteristic sharp peak and negative side-lobes often observed [@problem_id:4920417].

### Characterizing the Ring Artifact

The precise geometric and densitometric properties of a ring artifact are determined by the system geometry and the nature of the detector error.

#### Ring Radius

The radius of the ring corresponds to the geometric path of the X-ray that strikes the faulty detector element. This radius depends on the scanner's geometry.
- In an idealized **parallel-beam** system, the relationship is simple: the ring radius $r$ is the absolute radial distance of the detector element from the center, $r = |s_k|$.
- In a more practical **third-generation fan-beam** system, where the source and detector rotate together, the geometry is more complex. The radius $r$ of the ring in the reconstructed image depends on the source-to-isocenter distance, $R$, the source-to-detector distance, $D$, and the arc length position of the faulty channel, $s_0$. The radius is given by the [perpendicular distance](@entry_id:176279) from the isocenter to the ray path, which can be derived as [@problem_id:4920404]:
$$
r = R \left|\sin\left(\frac{s_0}{D}\right)\right|
$$
- This principle extends to **cone-beam CT**, where a faulty detector *column* at lateral position $u_0$ creates a ring in each axial slice. For the central slice ($z=0$), the radius $r$ is given by [@problem_id:4920400]:
$$
r = \frac{R_{s} |u_{0}|}{\sqrt{R_{d}^{2} + u_{0}^{2}}}
$$
where $R_s$ is the source-to-isocenter distance and $R_d$ is the source-to-detector distance.

#### Ring Intensity and Sign

The appearance of the ring as brighter (hyperdense) or darker (hypodense) than the surrounding tissue depends directly on the sign of the gain error $g_k$ [@problem_id:4828904]. As shown previously, the error in the [sinogram](@entry_id:754926) is $\Delta p = -\ln(g_k)$.
- If a detector **over-responds** ($g_k > 1$), then $\ln(g_k)$ is positive, and the sinogram bias $\Delta p$ is negative. The system interprets this as lower attenuation. Consequently, the reconstructed artifact is a **hypodense (dark) ring**.
- If a detector **under-responds** ($g_k  1$), then $\ln(g_k)$ is negative, and the sinogram bias $\Delta p$ is positive. The system interprets this as higher attenuation, and the reconstructed artifact is a **hyperdense (bright) ring**.

#### Ring Sharpness and Texture

The visual appearance of the ring—its sharpness and the presence of ringing or overshoots—is directly influenced by the reconstruction filter, or kernel, used in FBP. The standard **[ramp filter](@entry_id:754034)** is designed to perfectly reverse the blurring inherent in [backprojection](@entry_id:746638) but is very sensitive to high-frequency signals, including both noise and the sharp stripe from a detector error. This results in a very sharp, distinct ring.

To manage noise in clinical images, smoother filters are often used. These filters, such as the **Shepp-Logan** or **Hanning-windowed ramp** filters, work by attenuating the high-frequency components of the signal before [backprojection](@entry_id:746638). While this successfully reduces image noise, it also smooths the sharp [sinogram](@entry_id:754926) stripe. As a result, the reconstructed ring artifact will appear softer, broader, and less conspicuous. For example, a Hanning-windowed filter aggressively rolls off high frequencies, which can significantly reduce the contrast and sharpness of a ring artifact compared to a standard [ramp filter](@entry_id:754034) [@problem_id:4920461]. Therefore, the same underlying detector fault can produce artifacts of varying visual severity depending on the reconstruction kernel selected by the operator.

### Differentiating Rings from Similar Artifacts

Finally, it is crucial to distinguish true ring artifacts from other phenomena that can produce circular or arc-like features. As mentioned, beam hardening and scatter produce broad, low-frequency cupping, not sharp rings. Another important mimicker is an **arc artifact**, which appears as an incomplete ring. Arcs are typically caused by transient errors or by **detector lag** (afterglow), where a detector element's signal does not decay instantly. This lag causes a smearing of high-contrast information along the direction of gantry rotation. In the [sinogram](@entry_id:754926), this appears as an exponential tail following a bright feature, rather than a uniform vertical stripe. The resulting artifact is an arc, not a full, symmetric ring [@problem_id:4920408]. The symmetry and completeness of a ring artifact are key features pointing to a persistent, angle-independent detector calibration issue.