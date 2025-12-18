## Introduction
In the landscape of [computational electromagnetics](@entry_id:269494), the selection of a source excitation is a critical first step that defines the very purpose and validity of a [time-domain simulation](@entry_id:755983). Among the vast array of possible signals, the Gaussian pulse and the [modulated sinusoid](@entry_id:752103) stand out as foundational tools, offering unparalleled control over the temporal and spectral energy injected into a numerical experiment. However, leveraging these sources effectively requires more than a superficial understanding; a failure to appreciate their underlying principles and numerical subtleties can lead to inaccurate results, instability, and misinterpreted physics. This article addresses this knowledge gap by providing a comprehensive guide to designing, implementing, and analyzing these essential source functions.

Across three focused chapters, you will build a robust theoretical and practical foundation. The journey begins in **Principles and Mechanisms**, where we will dissect the mathematical properties of Gaussian pulses and their derivatives, exploring the profound relationship between their temporal shape and spectral content. Next, in **Applications and Interdisciplinary Connections**, we will translate theory into practice, demonstrating how these sources are implemented in [numerical algorithms](@entry_id:752770) like FDTD and used to investigate complex physical systems, revealing deep connections to signal processing and [systems theory](@entry_id:265873). Finally, **Hands-On Practices** will challenge you to apply this knowledge through guided analytical and computational problems. We begin by establishing the fundamental principles that make these sources so versatile and powerful.

## Principles and Mechanisms

In [computational electromagnetics](@entry_id:269494), the choice of source excitation is a foundational step that dictates the nature and scope of the simulation. Whether the goal is to characterize a device over a broad frequency range, probe a specific resonance, or simulate the propagation of a transient waveform, the temporal and spectral properties of the source must be precisely controlled. This chapter details the principles and mathematical mechanisms of the most common and versatile source functions used in time-domain methods: the Gaussian pulse and its derivatives, and the modulated sinusoidal source.

### The Archetypal Source: The Gaussian Pulse

The most fundamental broadband source used in numerical simulations is the **Gaussian pulse**. Its mathematical simplicity, combined with its unique and desirable spectral properties, makes it an ideal starting point for understanding source design. In the time domain, a Gaussian pulse is defined by the function:

$$
s(t) = A \exp\left(-\frac{(t - t_{0})^{2}}{2\sigma^{2}}\right)
$$

Here, $A$ is the peak amplitude, $t_0$ is the temporal shift that determines the time at which the pulse reaches its peak, and $\sigma$ is the temporal standard deviation, a parameter that controls the duration of the pulse.

To understand the physical significance of these parameters, we can characterize the pulse's key temporal features. The **[peak time](@entry_id:262671)**, $t_{\text{peak}}$, is the instant at which $s(t)$ is maximum. By taking the first derivative of $s(t)$ with respect to time and setting it to zero, we find that the maximum occurs precisely at $t = t_0$. Thus, $t_{\text{peak}} = t_0$. The parameter $t_0$ is critical in numerical methods; it ensures the pulse peak occurs away from the simulation start time of $t=0$, providing a "grace period" that helps enforce causality and avoid numerical artifacts associated with abrupt turn-on phenomena.

The pulse's duration is quantified by its **full width at half maximum (FWHM)**. This is defined as the time difference between the two points, $t_1$ and $t_2$, where the pulse's amplitude is half of its peak value, $s(t_{\text{peak}}) = A$. We solve the equation $s(t) = A/2$:

$$
A \exp\left(-\frac{(t - t_{0})^{2}}{2\sigma^{2}}\right) = \frac{A}{2}
$$

Solving for $t$ yields two solutions, $t_1 = t_0 - \sigma\sqrt{2\ln(2)}$ and $t_2 = t_0 + \sigma\sqrt{2\ln(2)}$. The FWHM is the difference $\Delta t = t_2 - t_1$. This derivation  reveals a direct, [linear relationship](@entry_id:267880) between the FWHM and the standard deviation:

$$
\Delta t_{\text{FWHM}} = 2\sigma\sqrt{2\ln(2)} \approx 2.355\sigma
$$

This relation provides an intuitive meaning to $\sigma$: it is a direct measure of the pulse's temporal spread. A larger $\sigma$ corresponds to a longer-lasting pulse, while a smaller $\sigma$ results in a more sharply peaked, transient excitation.

### Spectral Characteristics and the Time-Bandwidth Principle

The utility of a source is ultimately determined by its spectral content. The spectrum of the Gaussian pulse is found by taking its Fourier transform. Using the definition $S(f) = \int_{-\infty}^{\infty} s(t)\exp(-i2\pi f t) dt$, we can derive the spectrum of the Gaussian pulse from first principles. By [completing the square](@entry_id:265480) in the exponent of the integral, one finds that the Fourier transform of a Gaussian is also a Gaussian :

$$
S(f) = A \sigma \sqrt{2\pi} \exp(-2\pi^2\sigma^2 f^2) \exp(-i2\pi f t_0)
$$

This expression is highly revealing. It consists of two parts: a real-valued Gaussian amplitude spectrum, $|S(f)| = A\sigma\sqrt{2\pi}\exp(-2\pi^2\sigma^2 f^2)$, and a complex phase term, $\exp(-i2\pi f t_0)$. The phase term is linear in frequency, with a slope determined by the time shift $t_0$. This is a direct manifestation of the **[time-shifting property](@entry_id:275667)** of the Fourier transform: a delay of $t_0$ in the time domain corresponds to the addition of a linear phase, $-2\pi f t_0$, in the frequency domain. This phase term shifts the temporal position of the pulse but does not alter its shape or its energy distribution across frequencies.

The amplitude spectrum reveals a fundamental trade-off. The standard deviation of the frequency-domain Gaussian is $\sigma_f = 1/(2\pi\sigma)$. This inverse relationship between the temporal width $\sigma$ and the [spectral width](@entry_id:176022) $\sigma_f$ is known as the **time-bandwidth principle** or the uncertainty principle. A pulse that is very short in time (small $\sigma$) will have a very broad spectrum (large $\sigma_f$), making it an excellent broadband source. Conversely, a pulse that is long in time (large $\sigma$) will have a narrow spectrum.

This principle can be quantified by the **[time-bandwidth product](@entry_id:195055)**. Let us define the temporal duration $\Delta t$ as the FWHM of the temporal power envelope $P(t) = |s(t)|^2 = A^2 \exp(-(t-t_0)^2/\sigma^2)$, and the bandwidth $\Delta f$ as the FWHM of the power spectral density $S_{power}(f) = |S(f)|^2$. Following a similar procedure as for the pulse FWHM, we find that $\Delta t = 2\sigma\sqrt{\ln(2)}$ and $\Delta f = \frac{\sqrt{\ln(2)}}{\pi\sigma}$. The product is therefore a constant, independent of $\sigma$ :

$$
\Delta t \cdot \Delta f = \left(2\sigma\sqrt{\ln(2)}\right) \left(\frac{\sqrt{\ln(2)}}{\pi\sigma}\right) = \frac{2\ln(2)}{\pi} \approx 0.441
$$

This constant product is a hallmark of Gaussian pulses and demonstrates the unavoidable compromise between temporal and [spectral resolution](@entry_id:263022).

### Generating Band-Limited Excitations: The Modulated Gaussian Pulse

While a baseband Gaussian pulse is an excellent broadband source, many applications require exciting a system within a specific, limited frequency band. This is achieved through [amplitude modulation](@entry_id:266006), where a high-frequency carrier signal is modulated by a low-frequency envelope. The most common band-limited source is the **modulated Gaussian pulse**, also known as a Gabor pulse or a Gaussian-windowed [sinusoid](@entry_id:274998).

A general modulated signal can be written as $s(t)=E(t)\cos(\theta(t))$, where $E(t)$ is the **envelope** and $\theta(t)$ is the instantaneous phase. For a modulated Gaussian pulse, the envelope is a Gaussian, and the phase is linear in time :

$$
s(t) = A \exp\left(-\frac{(t-t_0)^2}{2\sigma^2}\right) \cos(2\pi f_0 (t-t_0) + \phi)
$$

Here, $f_0$ is the **carrier frequency**, and $\phi$ is a constant phase offset. The time-domain signal is an oscillation at frequency $f_0$ whose amplitude is shaped by the Gaussian envelope.

The spectral properties of this signal are best understood through the **modulation theorem** of the Fourier transform. The theorem states that multiplying a signal $m(t)$ by a cosine, $\cos(2\pi f_0 t)$, is equivalent in the frequency domain to convolving the signal's spectrum $M(f)$ with two Dirac delta functions at $\pm f_0$. This has the effect of splitting the baseband spectrum into two halves and shifting them to be centered at the carrier frequencies $\pm f_0$:

$$
\mathcal{F}\{m(t)\cos(2\pi f_0 t)\} = \frac{1}{2} [M(f-f_0) + M(f+f_0)]
$$

Applying this to our modulated Gaussian pulse, where the envelope $m(t)$ is a Gaussian, we find that its spectrum $S(f)$ consists of two Gaussian lobes, centered at $f_0$ and $-f_0$  . The width of these spectral lobes is determined by the width of the time-domain envelope. Specifically, if the time-domain Gaussian envelope has a standard deviation $\sigma$, each of the frequency-domain Gaussian lobes will have a standard deviation of $\sigma_f = 1/(2\pi\sigma)$ . This allows for precise control over the center frequency and bandwidth of the excitation: $f_0$ sets the band's center, and $\sigma$ controls its width.

### Pulses with Zero DC Content: The Ricker Wavelet

The Gaussian pulse has its maximum spectral energy at zero frequency, or DC ($f=0$). In some applications, such as wave propagation in certain plasma or metallic media, or when using specific numerical formulations, a non-zero DC component can introduce unphysical static fields or long-term drifts. It is therefore desirable to use a pulse with zero DC content.

A powerful method to create such a pulse is to use the **differentiation property** of the Fourier transform, which states that differentiation in the time domain corresponds to multiplication by $i\omega$ (or $i2\pi f$) in the frequency domain: $\mathcal{F}\{d^n x(t)/dt^n\} = (i2\pi f)^n X(f)$. This means that the spectrum of a derivative of a pulse $x(t)$ will be the spectrum $X(f)$ multiplied by a factor of $(i2\pi f)^n$. For $n \ge 1$, this guarantees that the resulting spectrum is zero at $f=0$.

The most prominent example of this family is the **Ricker wavelet**, which is mathematically equivalent to the negative second derivative of a Gaussian pulse. A common form is parameterized by a central frequency $f_c$ :

$$
s_R(t) = A \left(1 - 2\pi^{2} f_{c}^{2} t^{2}\right) \exp\left(-\pi^{2} f_{c}^{2} t^{2}\right)
$$

The spectrum of this wavelet, $S_R(f)$, is proportional to $f^2 \exp(-f^2/f_c^2)$. The $f^2$ term, a direct consequence of the two time derivatives, forces the spectrum to be zero at DC. The spectrum peaks at a frequency $f_{\text{max}} = f_c$, making the parameter $f_c$ an intuitive control for the pulse's dominant frequency content.

By matching the functional form, it can be shown that the Ricker [wavelet](@entry_id:204342) is exactly proportional to the second derivative of a Gaussian pulse, $g(t; \sigma) = \exp(-t^2/(2\sigma^2))$, provided that the parameters are related by $\sigma = 1/(\sqrt{2}\pi f_c)$. This establishes a formal link between the Ricker [wavelet](@entry_id:204342) and the derivative-of-Gaussian family of pulses .

### Advanced Topics and Practical Considerations

A final, crucial consideration in implementing these sources is **causality**. An ideal Gaussian function $s(t)$ is non-zero for all time $t \in (-\infty, \infty)$, making it non-causal. In a [numerical simulation](@entry_id:137087) that begins at $t=0$, we cannot implement a signal that existed at $t0$. A common practice is to truncate the pulse, for example by multiplying it by a [unit step function](@entry_id:268807) $u(t)$, creating a [causal signal](@entry_id:261266) $s_c(t) = s(t)u(t)$.

However, this abrupt truncation has spectral consequences. Multiplication in the time domain is convolution in the frequency domain. Truncating a signal convolves its spectrum with the spectrum of the truncation window, which can introduce unwanted spectral oscillations (Gibbs phenomenon). Even a simple analysis shows that truncating a symmetric pulse at its peak halves its DC component, fundamentally altering its spectrum . A more practical and spectrally cleaner approach is to choose the time delay $t_0$ to be sufficiently large (e.g., $t_0 \ge 4\sigma$ to $6\sigma$) such that the pulse amplitude is numerically negligible for $t \le 0$. The pulse is then "effectively causal" for the simulation, without suffering the spectral artifacts of a hard truncation.

Finally, it is worth noting that while different pulses like the Ricker [wavelet](@entry_id:204342) and the Gabor pulse can be designed to have the same peak frequency, their spectral shapes and relative bandwidths can be quite different. A comparative analysis shows that for the same nominal center frequency, the Ricker [wavelet](@entry_id:204342) typically has a broader relative bandwidth than a Gabor pulse . The choice between them depends on whether the simulation requires a wider, more broadband excitation (favoring the Ricker [wavelet](@entry_id:204342)) or a more spectrally concentrated, quasi-monochromatic excitation (favoring the Gabor pulse).