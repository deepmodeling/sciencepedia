## Introduction
In advanced optical systems, from the steppers used in semiconductor manufacturing to high-resolution microscopes, the nature of illumination is rarely simple. It exists in the regime of [partial coherence](@entry_id:176181), lying between the idealized limits of fully coherent and fully incoherent light. This reality presents a significant challenge: how to accurately model and predict the complex interference and diffraction phenomena that form an image? Simple models that are linear in either field amplitude or intensity are insufficient, failing to capture the nuanced interactions that define [image quality](@entry_id:176544) and fidelity in cutting-edge applications.

The Hopkins formulation for [partially coherent imaging](@entry_id:186712) provides the definitive theoretical and computational answer to this challenge. It offers a rigorous framework that correctly describes [image formation](@entry_id:168534) as a bilinear process, establishing a precise mathematical link between the object, the illumination source, and the projection optics. This article delves into the Hopkins formulation, beginning with the fundamental **Principles and Mechanisms** that describe light statistics and the bilinear imaging process. We then explore its extensive **Applications and Interdisciplinary Connections**, demonstrating its central role in computational lithography and its relevance to fields like microscopy. Finally, a series of **Hands-On Practices** will allow you to apply these concepts to practical problems in [system analysis](@entry_id:263805) and mask design.

## Principles and Mechanisms

The formation of an aerial image in a projection optical system is governed by the principles of [diffraction and interference](@entry_id:1123687). While imaging with a single point source ([coherent illumination](@entry_id:185438)) or a completely random, uncorrelated source (incoherent illumination) represent tractable theoretical limits, practical lithography systems operate in the domain of **[partial coherence](@entry_id:176181)**. The Hopkins formulation provides the definitive theoretical and computational framework for modeling [image formation](@entry_id:168534) in this regime. This chapter delineates the fundamental principles of this formulation, from the statistical description of light to the structure of the imaging operator and its practical implementation.

### The Statistical Description of Partially Coherent Fields

An optical field from a quasi-monochromatic, extended source is not deterministic but stochastic. Its properties must be described by statistical correlation functions. The fundamental quantity describing the [second-order statistics](@entry_id:919429) of a stationary optical field $E(\mathbf{r}, t)$ is the **[mutual coherence function](@entry_id:167961)**, defined as the ensemble average of the cross-correlation of the field at two spatial points, $\mathbf{r}_1$ and $\mathbf{r}_2$, with a time delay $\tau$:

$$
\Gamma(\mathbf{r}_1, \mathbf{r}_2, \tau) = \langle E(\mathbf{r}_1, t+\tau) E^*(\mathbf{r}_2, t) \rangle
$$

The temporal characteristics of this correlation are often more conveniently analyzed in the frequency domain. The Wiener-Khinchin theorem generalizes to the **[cross-spectral density](@entry_id:195014)** $W(\mathbf{r}_1, \mathbf{r}_2, \omega)$, which forms a Fourier transform pair with the [mutual coherence function](@entry_id:167961) with respect to the time-delay variable $\tau$ :

$$
W(\mathbf{r}_1, \mathbf{r}_2, \omega) = \frac{1}{2\pi} \int_{-\infty}^{\infty} \Gamma(\mathbf{r}_1, \mathbf{r}_2, \tau) e^{i\omega\tau} d\tau
$$

The [cross-spectral density](@entry_id:195014) has a profound physical interpretation. Its diagonal element, $W(\mathbf{r}, \mathbf{r}, \omega)$, represents the [power spectral density](@entry_id:141002) of the field at position $\mathbf{r}$. The total time-averaged intensity (or [irradiance](@entry_id:176465)) at that point is the integral of the [power spectral density](@entry_id:141002) over all frequencies :

$$
I(\mathbf{r}) = \Gamma(\mathbf{r}, \mathbf{r}, 0) = \int_0^{\infty} W(\mathbf{r}, \mathbf{r}, \omega) d\omega
$$

The off-diagonal elements, $W(\mathbf{r}_1, \mathbf{r}_2, \omega)$ for $\mathbf{r}_1 \neq \mathbf{r}_2$, quantify the correlation of the spectral component at frequency $\omega$ between two different points in space. To provide a normalized measure of this correlation, we define the **complex degree of spectral coherence**:

$$
\mu(\mathbf{r}_1, \mathbf{r}_2, \omega) = \frac{W(\mathbf{r}_1, \mathbf{r}_2, \omega)}{\sqrt{W(\mathbf{r}_1, \mathbf{r}_1, \omega) W(\mathbf{r}_2, \mathbf{r}_2, \omega)}}
$$

The magnitude $|\mu(\mathbf{r}_1, \mathbf{r}_2, \omega)|$, which ranges from $0$ (completely incoherent) to $1$ (fully coherent), measures the degree of correlation, while its phase indicates the effective phase relationship between the fields at the two points .

For the quasi-monochromatic fields typical of lithography, where the [spectral bandwidth](@entry_id:171153) $\Delta\omega$ is much smaller than the central frequency $\omega_0$, the frequency dependence can often be suppressed. We then work with the **mutual intensity**, $J(\mathbf{r}_1, \mathbf{r}_2) = \Gamma(\mathbf{r}_1, \mathbf{r}_2, 0)$, which describes the [spatial coherence](@entry_id:165083) of the field at a single instant.

### Image Formation as a Bilinear Process

The [propagation of mutual intensity](@entry_id:182564) through an optical system forms the basis of the Hopkins theory. Consider a thin photomask with a [complex amplitude](@entry_id:164138) transmission function $t(\mathbf{r})$. When an incident field with mutual intensity $J_0(\mathbf{r}_1, \mathbf{r}_2)$ illuminates this mask, the field immediately after the mask is $E_m(\mathbf{r}) = t(\mathbf{r}) E_0(\mathbf{r})$. The mutual intensity of the transmitted field, $J_m(\mathbf{r}_1, \mathbf{r}_2)$, is found by taking the [ensemble average](@entry_id:154225):

$$
J_m(\mathbf{r}_1, \mathbf{r}_2) = \langle E_m(\mathbf{r}_1) E_m^*(\mathbf{r}_2) \rangle = \langle [t(\mathbf{r}_1) E_0(\mathbf{r}_1)] [t(\mathbf{r}_2) E_0(\mathbf{r}_2)]^* \rangle
$$

Assuming the mask is a deterministic element, its transmission function can be factored out of the average, yielding a simple but powerful relationship :

$$
J_m(\mathbf{r}_1, \mathbf{r}_2) = t(\mathbf{r}_1) t^*(\mathbf{r}_2) J_0(\mathbf{r}_1, \mathbf{r}_2)
$$

The image intensity is found by propagating this masked mutual intensity through the projection system, which is characterized by a coherent impulse response (or amplitude [point-spread function](@entry_id:183154)) $h(\mathbf{r})$. The field at an image point $\mathbf{r}'$ is the convolution of the masked field with this impulse response. The resulting image intensity is found to be a quadruple integral:

$$
I(\mathbf{r}') = \iint \iint J_0(\mathbf{r}_1, \mathbf{r}_2) t(\mathbf{r}_1) t^*(\mathbf{r}_2) h(\mathbf{r}' - \mathbf{r}_1) h^*(\mathbf{r}' - \mathbf{r}_2) d\mathbf{r}_1 d\mathbf{r}_2
$$

This equation is the heart of the Hopkins theory in the space domain. It reveals that [image formation](@entry_id:168534) under [partial coherence](@entry_id:176181) is a **bilinear** process in the object's [complex amplitude](@entry_id:164138) $t(\mathbf{r})$. Physically, this means the final image is a sum of contributions from the interference of light waves emanating from every possible pair of points $(\mathbf{r}_1, \mathbf{r}_2)$ on the mask. The term $h(\mathbf{r}' - \mathbf{r}_1) h^*(\mathbf{r}' - \mathbf{r}_2)$ represents the elemental interference pattern from two such points, while the mutual intensity $J_0(\mathbf{r}_1, \mathbf{r}_2)$ acts as a weighting factor, modulating the visibility of this interference based on how correlated the illumination is between those two points. The cross-terms $t(\mathbf{r}_1) t^*(\mathbf{r}_2)$ are preserved as long as the illumination has some degree of coherence over the separation distance $|\mathbf{r}_1 - \mathbf{r}_2|$ .

This bilinear nature contrasts sharply with the limiting cases. In fully [coherent imaging](@entry_id:171640) ($J_0(\mathbf{r}_1, \mathbf{r}_2)$ is constant), the system is linear in the field amplitude $t(\mathbf{r})$. In fully [incoherent imaging](@entry_id:178214), the illumination is delta-correlated: $J_0(\mathbf{r}_1, \mathbf{r}_2) \propto \delta(\mathbf{r}_1 - \mathbf{r}_2)$. In this limit, all interference cross-terms for $\mathbf{r}_1 \neq \mathbf{r}_2$ vanish. The bilinear integral collapses, and the system becomes linear in the object's intensity, $|t(\mathbf{r})|^2$, convolved with the system's intensity [point-spread function](@entry_id:183154) $|h(\mathbf{r})|^2$ .

### The Hopkins Formulation in the Frequency Domain

While the space-domain integral provides physical insight, the Hopkins formulation is most powerfully and practically expressed in the [spatial frequency](@entry_id:270500) domain. This requires defining the Fourier-space representations of the three key components of the imaging system: the mask, the source, and the pupil.

#### Mask Spectrum $M(\mathbf{f})$

The mask is described by its [complex amplitude](@entry_id:164138) transmission function $t(\mathbf{r})$, and its frequency-domain representation is the **mask spectrum** $M(\mathbf{f})$, given by the spatial Fourier transform:

$$
M(\mathbf{f}) = \int t(\mathbf{r}) e^{-i 2 \pi \mathbf{f} \cdot \mathbf{r}} d\mathbf{r}
$$

Different mask technologies, which are central to Resolution Enhancement Techniques (RET), manifest as distinct spectral distributions. For a periodic binary amplitude mask (BAM) with pitch $p$ and duty cycle $D$, the spectrum consists of discrete diffraction orders at frequencies $f_n = n/p$. The weights of these orders are given by the Fourier series coefficients, with the zeroth order (DC term) being $a_0 = D$ and higher orders having amplitudes that follow a [sinc function](@entry_id:274746) envelope: $a_n = \frac{\sin(\pi n D)}{\pi n}$ for $n \neq 0$ .

A more advanced technology is the **alternating phase-shift mask (Alt-PSM)**, where adjacent transmitting apertures have a [relative phase](@entry_id:148120) shift of $\pi$. This seemingly simple modification has a dramatic effect on the spectrum. The effective period of the mask doubles to $2p$, and a crucial consequence is the complete suppression of the zeroth [diffraction order](@entry_id:174263) ($a_0 = 0$). This pushes the diffracted energy into [higher-order modes](@entry_id:750331), which can then interfere to produce higher-contrast images for dense features—a key goal of RET .

#### Source Distribution $S(\mathbf{f}_s)$ and Pupil Function $P(\mathbf{f})$

The illumination system and projection optics are also described in the frequency domain.

The illuminator, or **source**, is modeled as a collection of mutually incoherent point sources, each emitting a [plane wave](@entry_id:263752) that illuminates the mask from a different direction. Each direction corresponds to a transverse [spatial frequency](@entry_id:270500) $\mathbf{f}_s$. The **source distribution** $S(\mathbf{f}_s)$ is a real, non-negative function describing the intensity of the source as a function of this spatial frequency. It is typically normalized such that $\int S(\mathbf{f}_s) d\mathbf{f}_s = 1$. The spatial extent of the source is characterized by the **illumination [numerical aperture](@entry_id:138876)**, $\text{NA}_{\text{ill}}$, which defines the support of $S(\mathbf{f}_s)$ in the frequency plane: $S(\mathbf{f}_s) = 0$ for $|\mathbf{f}_s| > \text{NA}_{\text{ill}} / \lambda$ .

The projection optics are characterized by the **[pupil function](@entry_id:163876)** $P(\mathbf{f})$. This is a complex function describing the transmission of the lens pupil as a function of [spatial frequency](@entry_id:270500) $\mathbf{f}$. Its support is a circular disk defined by the **objective numerical aperture**, $\text{NA}_{\text{obj}}$, such that $|P(\mathbf{f})| = 0$ for $|\mathbf{f}| > \text{NA}_{\text{obj}} / \lambda$. The magnitude of the [pupil function](@entry_id:163876), $|P(\mathbf{f})|$, represents any [apodization](@entry_id:147798) or non-uniform transmission, while its phase, $\arg\{P(\mathbf{f})\}$, represents [optical aberrations](@entry_id:163452). These phase errors are directly related to the **Optical Path Difference (OPD)**, denoted $W(\mathbf{f})$, via the relation :

$$
P(\mathbf{f}) = A(\mathbf{f}) \exp\left( i \frac{2\pi}{\lambda} W(\mathbf{f}) \right)
$$

where $A(\mathbf{f})$ is the real amplitude transmission of the pupil.

The degree of [spatial coherence](@entry_id:165083) in the imaging system is conveniently parameterized by the **[partial coherence](@entry_id:176181) factor** $\sigma$. It is defined as the dimensionless ratio of the illumination NA to the objective NA:

$$
\sigma = \frac{\text{NA}_{\text{ill}}}{\text{NA}_{\text{obj}}}
$$

In a [normalized frequency](@entry_id:273411) coordinate system where the radius of the pupil is scaled to unity, the radius of the source disk is simply $\sigma$ . A small $\sigma$ value (approaching 0) corresponds to near-[coherent imaging](@entry_id:171640), while a large $\sigma$ value (approaching 1 or greater) corresponds to near-[incoherent imaging](@entry_id:178214).

### The Transmission Cross-Coefficient (TCC)

With these frequency-domain definitions, the Hopkins bilinear integral can be transformed into an equivalent, and computationally more direct, frequency-domain expression. The image intensity is given by:

$$
I(\mathbf{r}) = \iint TCC(\mathbf{f}_1, \mathbf{f}_2) M(\mathbf{f}_1) M^*(\mathbf{f}_2) e^{i 2 \pi (\mathbf{f}_1 - \mathbf{f}_2) \cdot \mathbf{r}} d\mathbf{f}_1 d\mathbf{f}_2
$$

The kernel of this transformation is the **Transmission Cross-Coefficient (TCC)**, sometimes denoted $T(\mathbf{f}_1, \mathbf{f}_2)$, which encapsulates all the properties of the illumination and the projection optics:

$$
TCC(\mathbf{f}_1, \mathbf{f}_2) = \int S(\mathbf{f}_s) P(\mathbf{f}_s + \mathbf{f}_1) P^*(\mathbf{f}_s + \mathbf{f}_2) d\mathbf{f}_s
$$

The TCC describes the transfer of information for a pair of spatial frequencies, $(\mathbf{f}_1, \mathbf{f}_2)$, from the mask to the image. Its value represents the integrated overlap of the source distribution with two shifted versions of the [pupil function](@entry_id:163876). An off-diagonal element $TCC(\mathbf{f}_1, \mathbf{f}_2)$ with $\mathbf{f}_1 \neq \mathbf{f}_2$ is non-zero only if there are source points that allow both diffraction orders $\mathbf{f}_1$ and $\mathbf{f}_2$ to pass through the pupil simultaneously. These non-zero off-diagonal elements are precisely what give rise to the interference terms—the spatial beats at frequency $(\mathbf{f}_1 - \mathbf{f}_2)$—that create [image contrast](@entry_id:903016) .

To illustrate this mechanism, consider a simplified one-dimensional system with a two-[point source](@entry_id:196698) at $\pm \alpha_0$ and a mask whose spectrum consists of only two diffraction orders at $\pm k_0$ (as with an idealized Alt-PSM). Let the mask spectrum be $M(k_0)=1$ and $M(-k_0)=e^{i\pi}=-1$. The TCC for the frequency pair $(k_0, -k_0)$ is calculated by summing the contributions from the two source points:

$$
TCC(k_0, -k_0) = \frac{1}{2} [P(k_0 - \alpha_0) P^*(-k_0 - \alpha_0) + P(k_0 + \alpha_0) P^*(-k_0 + \alpha_0)]
$$

If all four shifted pupil arguments fall within the lens [passband](@entry_id:276907) (i.e., the [pupil function](@entry_id:163876) values are 1), the TCC element becomes $TCC(k_0, -k_0) = 1$. Similarly, all other relevant TCC elements can be shown to be 1. The intensity at the center of the image ($x=0$) is then the sum of all terms in the [bilinear form](@entry_id:140194):

$$
I(0) = \sum_{k_i, k_j \in \{\pm k_0\}} M(k_i) M^*(k_j) TCC(k_i, k_j)
$$
$$
I(0) = |M(k_0)|^2 TCC(k_0,k_0) + |M(-k_0)|^2 TCC(-k_0,-k_0) + M(k_0)M^*(-k_0)TCC(k_0,-k_0) + M(-k_0)M^*(k_0)TCC(-k_0,k_0)
$$
$$
I(0) = (1)(1) + (1)(1) + (1)(-1)(1) + (-1)(1)(1) = 1 + 1 - 1 - 1 = 0
$$
This perfect destructive interference at the center is a direct consequence of the phase relationship in the mask spectrum being faithfully transmitted by the non-zero off-diagonal TCC elements, demonstrating the power of the Hopkins formalism to predict the performance of advanced reticle technologies .

### Mathematical Structure and Numerical Eigenmode Decomposition

The TCC can be viewed as the kernel of a linear [integral operator](@entry_id:147512) that acts on the mask spectrum. This operator possesses several crucial mathematical properties that are exploited in modern computational lithography. The TCC kernel is **Hermitian** (or self-adjoint), satisfying $TCC(\mathbf{f}_1, \mathbf{f}_2) = TCC^*(\mathbf{f}_2, \mathbf{f}_1)$, and **positive semidefinite**. The latter property is a direct consequence of physics: the image intensity, which is the result of the [quadratic form](@entry_id:153497) involving the TCC, must always be non-negative .

For such a kernel on a [compact domain](@entry_id:139725), **Mercer's Theorem** guarantees that the TCC can be decomposed into a series of its eigenfunctions $\phi_n(\mathbf{f})$ and non-negative eigenvalues $\lambda_n$:

$$
TCC(\mathbf{f}_1, \mathbf{f}_2) = \sum_{n=1}^{\infty} \lambda_n \phi_n(\mathbf{f}_1) \phi_n^*(\mathbf{f}_2)
$$

The [eigenfunctions](@entry_id:154705) $\phi_n$ are known as the **[coherent modes](@entry_id:194070)** of the imaging system, and they form a complete [orthonormal basis](@entry_id:147779) for the space of mask spectra. This decomposition is profoundly important. It allows the complex, bilinear [partially coherent imaging](@entry_id:186712) problem to be expressed as an incoherent sum of simple [coherent imaging](@entry_id:171640) processes:

$$
I(\mathbf{r}) = \sum_{n=1}^{\infty} \lambda_n \left| \int \phi_n(\mathbf{f}) M(\mathbf{f}) e^{i 2 \pi \mathbf{f} \cdot \mathbf{r}} d\mathbf{f} \right|^2
$$

In practice, the eigenvalues $\lambda_n$ decay rapidly. This means that the imaging process is dominated by a small number of [coherent modes](@entry_id:194070) with the largest eigenvalues. Numerical simulations can therefore truncate the expansion after a few dozen modes, capturing the vast majority of the image information while dramatically reducing [computational complexity](@entry_id:147058) compared to evaluating the full quadruple integral. The convergence of this series is guaranteed in an $L^2$ sense, which is sufficient for [global error](@entry_id:147874) metrics, although uniform [pointwise convergence](@entry_id:145914) depends on stronger continuity properties of the kernel .

### Limitations of the Scalar Model and Vectorial Extensions

The Hopkins formulation as presented thus far is a **scalar theory**—it treats the electric field as a single scalar quantity. This approximation is highly accurate for systems with low numerical aperture ($\text{NA} \ll 1$) where all propagation angles are small (paraxial). However, modern lithography systems operate at very high NA (near or above 1), where this approximation breaks down for two main reasons :

1.  **Vector Diffraction Effects:** At high angles of diffraction and convergence, the electric field is inherently a vector. It cannot be assumed to be purely transverse to the direction of propagation, and its components transform in complex ways upon focusing.

2.  **Polarization-Dependent Interactions:** The mask itself, with its three-dimensional topography, can diffract different polarizations of light differently. More importantly, the interaction of light with the wafer stack (including anti-reflective coatings and the resist itself) is strongly dependent on whether the electric field is polarized parallel (Transverse Magnetic, TM) or perpendicular (Transverse Electric, TE) to the plane of incidence.

These effects necessitate a **vectorial imaging model**. In this extension, the electric field is treated as a two-component vector $\mathbf{E} = [E_x, E_y]^T$. The [partial coherence](@entry_id:176181) state is no longer described by a scalar mutual intensity but by a $2 \times 2$ **[coherency matrix](@entry_id:192731)** $\mathbf{J}(\mathbf{r}_1, \mathbf{r}_2)$, whose elements describe the correlations between all pairs of polarization components.

Consequently, the scalar TCC must be replaced by a more complex vectorial TCC. This generalized kernel is a fourth-rank tensor, $H_{pqrs}(\mathbf{f}_1, \mathbf{f}_2)$, which can be arranged as a $4 \times 4$ matrix. This matrix acts on a four-component vector representing the object's coherency spectrum (e.g., the set of all cross-products of mask spectrum components like $M_x(\mathbf{f}_1)M_y^*(\mathbf{f}_2)$). This $4 \times 4$ structure is required to capture all possible polarization couplings in the system, such as an $x$-polarized component of one [diffraction order](@entry_id:174263) coupling with a $y$-polarized component of another. This vectorial TCC matrix is also Hermitian and positive semidefinite, and it can be similarly decomposed into eigenmodes, forming the basis for advanced vectorial computational lithography models .